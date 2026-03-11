# Cloud Computing Basics
[
### Fontes:
-<a src="https://www.sistemas24horas.com.br/aulas/files_semi2018/livro-computacao-em-nuvem-taurion.pdf"> Cloud computing: Trasnformando o Mundo da Tecnologia da Informação</a>
- <a src =" https://medium.com/criando-o-futuro-com-a-nuvem-aws/como-usar-amazon-ec2-s3-e-rds-na-aws-um-guia-prático-para-iniciantes-4d4e75823be9">*![Como Usar Amazon EC2, S3 e RDS na AWS: Um Guia Prático para Iniciantes]*</a>

]


## Oque é Cloud Computing ?
Em etmors simples computação nuvem é alugar um poder de processamento e armazenamento de outra empresa,(no nosso caso seria da Amazon) via internet, em vez de comprar e montar e manter seus proprios servidores fisicos, a vantagem que voce paga apenas pelo oque usa pode aumentar ou diminuir recursos em questaões de minutos 

### Tipos de Oferta de Seviços em Cloud computing 
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

* como funciona: Com um User na AWS  cria um AMI(Amazon Machine Imagem), contendo apliações e Bibliotecas de programas e componentes, pode usar templates e imagens pre-configuradas,
selecione o tipo de instancia( o poder de processamento), configure o armazenamento e lançar espere a AWS fazer sua magica, uma vez lançada é possivel acessar via SSH


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

   voce pode tanto carregar ou arrastar o arquivo para fazer o upload

