# Cloud Computing Basics
[
### Fontes:
- <a src="https://www.sistemas24horas.com.br/aulas/files_semi2018/livro-computacao-em-nuvem-taurion.pdf"> *![Cloud computing: Trasnformando o Mundo da Tecnologia da Informação]*</a>
- <a src =" https://medium.com/criando-o-futuro-com-a-nuvem-aws/como-usar-amazon-ec2-s3-e-rds-na-aws-um-guia-prático-para-iniciantes-4d4e75823be9">*![Como Usar Amazon EC2, S3 e RDS na AWS: Um Guia Prático para Iniciantes]*</a>
-  <a src = "https://medium.com/rpedroni/finalmente-entendendo-vpc-e-subnets-na-aws-4fcced1ee405">*![Finalmente entendendo VPC e Subnets na AWS]*</a>
]


## Oque é Cloud Computing ?
Em etmors simples computação nuvem é alugar um poder de processamento e armazenamento de outra empresa,(no nosso caso seria da Amazon) via internet, em vez de comprar e montar e manter seus proprios servidores fisicos, a vantagem que voce paga apenas pelo oque usa pode aumentar ou diminuir recursos em questaões de minutos 

## Tipos de Oferta de Seviços em Cloud computing 
```O Nivel que nos Interessa nesse Estudo apenas o 1 ou 2 o resto fica a nivel de conhecimento  ```

 - **Nivel 1:** camada IaaS(Infrastruct as  a service), com oferta de serviço de hospedagem, camada basica da Cloud computing, ex: EC2, S3, VPC comumente encontrado na AWS.<br>
 - **Nivel 2** Camada de desenvolvimento e serviços de gerenciamento em nuvem, exemplo de platarforma de desenvolvimento como oferecidas pelo Google AppEngine, Muitas vezes estas camadas usam serviços da anterior.<br>
 - **Nivel 3** Camada de SaaS como google docs, Muitas das aplicações web são serviços baseado em nuvem como Likedin Facebook.<br>
 - **Nivel 4** Camada de processos, que envolvem processos de negocios baseadas nas teconologias ofertadas exemplos de serviços são serviços de BPO(BUsiness Processing OutSoucing).


### Os 3 serviços Fundamentais da AWS 
para entender a AWS ou qualquer serviço de numve voce precisa conhcer a triade basica de processamento e armazenamento e rede 

#### 1. EC2(Elastic Compute Cloud): O "Computador"(processamento)
 * Oque é: O EC2 fornece servidores virtuais, chamados de "instâncias". Pense nele como o computador propriamente dito (CPU, memoria RAM, Sistema Operacional), o SO normalmente é Linux
 * Para que Ele Serve: É no EC2 que o codigo da sua aplicação roda, onde voce hospeda o sistema de um site, onde um banco de dados tradicional é instalado.

 * Porque "Elastico"? : Porque se sua aplicação de repente escalar muito e receber milhares de acessos, voce pode pedir para AWS criar mais servidores iguais a ele instantaneamente, depois fechalos/destruilos quando o trafego cair 

* Como funciona:
  
         -Com um User na AWS  cria um AMI(Amazon Machine Imagem)
           contendo apliações e de programas e componentes 
           pode usar templates e imagens pre-configuradas.

         - Selecione o tipo de instancia( o poder de processamento)
  
         - Configure o armazenamento 
         
         - Clique em lançar e espere a AWS fazer sua magica, uma vez lançada é possivel acessar via SSH.


#### 2. S3(Simple Storage Service): O "Armazenamento"
* Oque é : O S3 é um serviço de objetos. Diferentes Hd de um computador, ele é feito para guardar arquivos indenpendentes, que são chamados de "objetos" e colocados em pastas chamadas de "Bucketes", em persistencia é um serviço de object storage

* Para que serve: Serve para guardar Imagens Videos, backups, documentos e arquvios de logs.

* **! *Importante*:O S3 não roda Sistemas operacionais nem aplicativos, ele é apenas um lugar segura e com espaço virtualmente ilimitado para guardar dados estáticos**

* Como funciona:
  
      Ja na Console  selecionada o S3 

      1 - crie um bucket: Um container onde seus arquivos irão ficar armazenados 

      2-Passo de padrões: 
       - propriedades do objeto  deixe desabilitado.
       - em configurções de bloqueio deixe o padrão
       - versionamento fica a criteiro <br>
      
      3-criptografia use a SSE-S3 de melhor configuração <br>
      
      4- Clique em criar<br>

      Voce pode tanto carregar ou arrastar o arquivo para fazer o upload

#### 3. VPC(Virtual Private Cloud): A "Cerca Virtual"(Rede)
``` NA VPC detalhei um pouco mais foi o que mais tive dificuldade de configurar e entender como funciona no painel da AWS```
* Oque é : VPC é uma rede privada e isolada logicamente para voce dentro da nuvem publica da AWS
* Para que Serve: Ela garante a segurança e a organização do seus recursos. Com a VPC, voce pode criar o "terreno" onde seus servidores EC2 vão ficar. Voce define quem pode acessar a internet, quais servidores ficam escodidos do público(como um banco de dados) e como regras de firewall funcionam
* Como funciona:
      
      Ja na Console selecione o VPC 
      - Inicie a Criação: No painel principal (Dashboard) da VPC, clique no botão laranja "Create VPC" (Criar VPC).

      - Escolha o Assistente Visual: Selecione a opção "VPC and more" (VPC e muito mais). Essa opção é fantástica porque ela gera um mapa visual e cria as sub-redes e rotas de forma automática para você.

      - Defina o Nome e o Tamanho:
      Em Name tag auto-generation, dê um nome para o seu projeto (ex: meu-projeto-vpc).

      - Em IPv4 CIDR block, você define o tamanho da sua rede. O padrão sugerido pela AWS (geralmente 10.0.0.0/16) é ótimo para começar, pois disponibiliza mais de 65 mil endereços IP internos.

      - Divida os Lotes (Subnets):
      Escolha quantas Availability Zones (Zonas de Disponibilidade, que são data centers físicos diferentes) você quer usar. O ideal é no mínimo 2 para que seu sistema não caia se um prédio da AWS tiver problemas.

      - Defina o número de Public Subnets (redes que terão acesso à internet, ideais para o servidor web do seu site) e Private Subnets (redes trancadas sem acesso à internet, onde você deve colocar seu banco de dados).

      Finalize a Construção: Revise o diagrama gerado na lateral direita da tela para confirmar se a estrutura faz sentido. Role até o final da página e clique em "Create VPC

## Como eles trabalham juntos? (Exemplo Prático)

   Imagine que você está criando um aplicativo estilo Instagram:

   Você cria uma VPC para garantir que todo o seu sistema esteja em uma rede privada e protegida contra invasores.

   Dentro dessa VPC, você coloca servidores EC2 rodando o código do seu aplicativo. Esses servidores recebem os acessos dos usuários pelo celular.

   Quando um usuário posta uma foto nova, o servidor EC2 processa o pedido, mas ele não salva a imagem no próprio disco rígido. Ele envia a foto para o S3, que guarda a imagem de forma segura e barata.

# ⚠️OBSERVAÇÃO APÓS POR EM PRATICA TUDO QUE VOCE TESTOU COM ESSE GUIA EXCLUA DA SUA AWS PARA NAO RECEBER UMA SUPRESA NO CARTÃO DE CREDITO⚠️