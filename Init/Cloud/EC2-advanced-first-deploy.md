#  Guia de Deploy : Microserviço Go + Postgres na AWS

Este guia documenta o processo de implantação otimizada. 

Pratique o Linux o sucesso no deploy não é decorar comandos, mas se sentir confortável no terminal. Quanto mais você mexer, mais fácil fica.

Este guia foi feito para entender como funciona o passo a passo de como colocar um aplicação no ar. Configurações contra ataques (DDoS), HTTPS e travas de segurança ficam para um próximo nível de estudo.

Erros são seus Professores: É normal algo dar errado no meio do caminho. Resolver esses "bugs" inesperados é exatamente o que treina sua mente para ser um desenvolvedor . Não desanime, investigue o log e pesquise!
##  1. Configuração da Instância EC2 (Console AWS)

### Onde configurar e o que escolher:

* **Nome:** `micro-service-auth` (ou o nome do seu projeto).
* **Imagem (AMI):** **Amazon Linux 2023**. É a mais atual e otimizada para a nuvem da AWS.
* **Tipo de Instância:** **t2.micro**. Ela possui 1GB de RAM, o que é pouco para compilar, mas suficiente para rodar se usarmos este guia.
* **Segurança (Security Group):**
* **Regra 1 (SSH):** Porta 22 (Acesso ao terminal).
* **Regra 2 (TCP):** Porta **8080**. É aqui que sua API Go "escuta". Defina a origem como `0.0.0.0/0`.



###  Dados do Usuário (User Data)

Role até o final em **Detalhes Avançados**. O script abaixo prepara a máquina "do zero" assim que ela liga pela primeira vez.

```bash
#!/bin/bash
# 1. Atualiza o sistema e instala Docker e Git
sudo dnf update -y
sudo dnf install docker git -y
sudo systemctl start docker
sudo systemctl enable docker

# 2. Permite que o usuário 'ec2-user' use o Docker sem precisar de 'sudo' em tudo
sudo usermod -aG docker ec2-user

# 3. Instala o Docker Compose V2 (Gerenciador de múltiplos containers)
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# 4. Instala o Buildx (Plugin para builds modernos e rápidos)
mkdir -p /home/ec2-user/.docker/cli-plugins/
sudo curl -SL https://github.com/docker/buildx/releases/download/v0.17.1/buildx-v0.17.1.linux-amd64 -o /home/ec2-user/.docker/cli-plugins/docker-buildx
sudo chmod +x /home/ec2-user/.docker/cli-plugins/docker-buildx
sudo chown -R ec2-user:ec2-user /home/ec2-user/.docker

# 5. Clona o projeto. Se mudar de projeto, altere o link abaixo!
cd /home/ec2-user
sudo git clone https://github.com/Aaron-GMM/auth-jwt-go.git app
sudo chown -R ec2-user:ec2-user /home/ec2-user/app

```

---

##  2. Localizando IP e Conexão

Após lançar a instância, você precisa de duas informações no Dashboard:

1. **IP Público:** Na aba **Detalhes**, procure por **Endereço IPv4 público** (ex: `54.234.251.84`).
2. **Comando SSH:** Clique em **Conectar** (topo da tela) > Aba **Cliente SSH**. Copie o exemplo no final da página.

---

##  3. Build da Aplicação (Local - WSL2/Linux)

**Por que fazer isso?** Compilar Go na AWS consome 100% da CPU e RAM, travando a máquina. Fazendo localmente, você gera um "executável" pronto.

Na raiz do seu projeto local, rode:

```bash
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o main-linux ./main.go

```

* **`CGO_ENABLED=0`**: Cria um binário estático (sem dependências externas). Essencial para rodar em imagens leves como Alpine.
* **`GOOS=linux`**: Diz que o destino é um sistema Linux.
* **`GOARCH=amd64`**: Define a arquitetura do processador da AWS (x86_64).

---

##  4. Envio de Arquivos (SCP)

No seu terminal local, envie o binário e seu arquivo de segredos (`.env`):

```bash
# 1. Proteja sua chave .pem (SSH exige isso)
chmod 400 ~/chave-aws.pem

# 2. Envie os arquivos para a pasta 'app' criada pelo UserData
scp -i ~/chave-aws.pem main-linux .env ec2-user@SEU-IP-AWS:/home/ec2-user/app/

```

---

##  5. Configuração Final no Servidor (SSH)

Conecte-se: `ssh -i ~/chave-aws.pem ec2-user@SEU-IP-AWS`

### 5.1 Memória Swap (O Seguro de RAM)

A `t2.micro` pode "morrer" se o Postgres ocupar muita RAM. O Swap usa o disco como memória extra.

```bash
sudo dd if=/dev/zero of=/swapfile bs=1M count=1024
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile

```

### 5.2 Otimização do Dockerfile

Para ganhar velocidade e leveza, mude o `Dockerfile` para apenas executar o arquivo que você enviou.

```bash
nano ~/app/Dockerfile

```

**Substitua por:**

```dockerfile
FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /app
COPY main-linux ./main
RUN chmod +x ./main
CMD ["./main"]

```
### `ctrl + O | Enter | ctrl + X`
---

##  6. Deploy e Teste Final

### Execução:

```bash
cd ~/app
newgrp docker # Atualiza as permissões de grupo sem precisar deslogar
docker-compose up -d --build

```

* **`newgrp docker`**: É o comando que ativa sua permissão de usar Docker na sessão atual.

###  Campo de Teste (cURL para Linux/WSL2)

> **Observação Importante:** Como não configuramos SSL, use sempre **HTTP** e não HTTPS. O erro `SSL_ERROR_RX_RECORD_TOO_LONG` ocorre se você tentar usar `https` sem ter um certificado configurado.

**Teste de Registro de Usuário:**

```bash
curl -X POST http://SEU-IP-AWS:8080/api/v1/register \
     -H "Content-Type: application/json" \
     -d '{
           "name": "Aaron",
           "email": "aaron@exemplo.com",
           "password": "senha_segura_123"
         }'

```

**Teste de Login (Gerar JWT):**

```bash
curl -X POST http://SEU-IP-AWS:8080/api/v1/login \
     -H "Content-Type: application/json" \
     -d '{
           "email": "aaron@exemplo.com",
           "password": "senha_segura_123"
         }'

```

---
