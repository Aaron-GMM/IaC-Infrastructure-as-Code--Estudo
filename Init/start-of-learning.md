# IaC (infraestruct as code)
[
   ### Fontes:
- <a src = "https://github-com.translate.goog/resources/articles/what-is-infrastructure-as-code?_x_tr_sl=en&_x_tr_tl=pt&_x_tr_hl=pt&_x_tr_pto=sge">![What is Infrastructure as Code (IaC)?]</a>
- <a src =" https://thenewstack.io/introduction-to-infrastructure-as-code/">*![ Infrastructure as Code: Introduction to IaC ]*</a>

]

### Oque é ?
 **É o gerencimento da Infraestrtura como servidores, redes, banco de dados, por meio de arquivos de definição com codigos/scripts subistituindo configuração manual**

### Para que serve?
 
 **-Ele server para gerenciar o ambiente por completo da aplicação como adicionar firewall, configurar DNS a rede e todo ambiente na nuvem por meio de scripts de codigo<br>-Ele serve para padronizar o ambiente de teste e de produção, como a infraestrutura se torna codigos, conseguimos versionar com git, fazer auditoriar e reverter erros rapidamente**

### Tecnologias 
* Terraform: a mais popular gerenciar recursos em multiplos provedores de nuvem (AWS, Azure, Google Cloud).
* Ansible: Focada em automação de tarefas e gerenciamento de configuração em servidores já existentes.
* Cloud-specific (Nativas): AWS CloudFormation, Azure Resource Manager (ARM) e Google Cloud Deployment Manager.
* Pulumi: Permite usar linguagens de programação comuns (Python, JavaScript) para definir a infraestrutura.
* Chef e Puppet: Focadas em manter o estado desejado da configuração de servidores

### Oque aprender agr de inicio?
* Cloud Computing Basics: Entenda os serviços fundamentais (EC2, S3, VPC) em uma nuvem como a AWS.
* Provisionamento com Terraform: Comece aprendendo a sintaxe HCL e o gerenciamento de state.
* Integração com CI/CD:Estude como rodar seus scripts de IaC automaticamente via ferramentas como GitHub Actions ou GitLab CI