# Guia Definitivo: Controle de Gastos e Alertas na AWS

Este guia foi criado para ajudar você a configurar camadas de proteção financeira na sua conta AWS, garantindo que você nunca seja pego de surpresa por cobranças indesejadas.

---

## 1. Habilitar o Monitoramento de Faturamento
Antes de criar os alertas, você precisa garantir que a AWS tenha permissão para monitorar e enviar esses dados para o CloudWatch.

1.  Faça login no [Console AWS](https://console.aws.aws.com/).
2.  No canto superior direito, clique no seu **Nome de Usuário** e selecione **Billing and Cost Management** (Faturamento).
3.  No menu lateral esquerdo, em **Preferences** (Preferências), clique em **Billing Preferences**.
4.  Marque a opção **Receive CloudWatch Billing Alerts**.
5.  Clique em **Save preferences**.

---

## 2. Criar um Orçamento (AWS Budgets)
O AWS Budgets permite definir um limite de gastos e enviar alertas por e-mail quando você atingir (ou estiver prestes a atingir) esse valor.

1.  No painel de Billing, clique em **Budgets** no menu lateral.
2.  Clique em **Create budget**.
3.  Escolha o tipo **Cost budget - Recommended** (Orçamento de custo) e clique em **Next**.
4.  **Configurações do Orçamento:**
    * **Name:** Ex: `Orcamento_Mensal_Limite`.
    * **Budget amount:** Defina o valor máximo (ex: $5.00).
    * **Scope:** Deixe em "All AWS Services".
5.  **Configurar Alertas:**
    * Clique em **Add an alert threshold**.
    * Defina para ser notificado quando o custo **Real** atingir 80% do valor.
    * Adicione seu e-mail no campo de destinatários.
    * Adicione outro alerta para 100% da **Previsão (Forecasted)**.
6.  Clique em **Next** até o fim e finalize em **Create budget**.

---

## 3. Configurar Alarme de Faturamento no CloudWatch
O CloudWatch pode monitorar o faturamento total acumulado e disparar um alarme específico.

1.  Pesquise por **CloudWatch** na barra de busca superior.
2.  No menu lateral, vá em **Alarms** > **All alarms** e clique em **Create alarm**.
3.  Clique em **Select metric** > **Billing** > **Total Estimated Charge**.
4.  Marque a moeda (USD) e clique em **Select metric**.
5.  Em **Conditions**, defina o limite (Static). Ex: `Greater/Equal` a `10`.
6.  Em **Notification**, selecione um tópico SNS existente ou crie um novo (Create new topic) inserindo seu e-mail para receber o aviso.
7.  Dê um nome ao alarme e salve.

---

##  Dica de Ouro: A Camada de Proteção Bancária

Mesmo com alertas, erros de configuração podem gerar cobranças. Para uma segurança de "nível ninja", utilize a estratégia do cartão isolado:

1.  **Cartão Virtual com Limite Baixo:** Nunca use seu cartão de crédito principal ou físico na AWS. Crie um **cartão virtual** pelo app do seu banco e defina o limite dele exatamente para o valor que você planeja gastar (ou o mínimo permitido, como R$ 10,00).
2.  **Cartão de Uso Único (24 horas):** Se o seu banco oferecer a opção de **Cartão Virtual Temporário/24 horas**, esta é a **melhor opção**. 
    * Use-o para validar a conta. 
    * Após o prazo, o cartão expira e a AWS não conseguirá realizar cobranças automáticas recorrentes sem que você atualize os dados, servindo como uma trava de segurança física contra gastos exponenciais.

---
