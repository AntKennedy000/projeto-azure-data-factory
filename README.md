# ☁️ Projeto Azure Data Factory

## 📌 Sobre o projeto

Este projeto foi desenvolvido como parte de uma atividade prática de estudos em **Cloud Computing** e **Data Engineering**, utilizando o ambiente **Microsoft Azure**.

O objetivo foi criar e organizar um ambiente utilizando o **Azure Data Factory**, aplicar conceitos de **Infrastructure as Code (IaC)** por meio de **ARM Templates**, utilizar o **Azure Cloud Shell** para implantação via linha de comando e configurar recursos relacionados ao **monitoramento, métricas e controle de custos**.

Durante a execução também foram analisadas algumas particularidades e limitações encontradas em uma assinatura **Azure Free Trial**, permitindo observar na prática como o gerenciamento de recursos e custos funciona dentro do Azure.

---

## 🎯 Objetivos

- Criar um **Resource Group** para organização dos recursos;
- Provisionar um **Azure Data Factory**;
- Acessar e explorar o **Data Factory Studio**;
- Utilizar o **Azure Cloud Shell**;
- Aplicar conceitos de **Infrastructure as Code (IaC)**;
- Criar e utilizar um **ARM Template**;
- Realizar uma implantação utilizando o Azure CLI;
- Configurar um **orçamento de custos**;
- Configurar **alertas de custo**;
- Explorar as **métricas do Azure Data Factory**;
- Personalizar um **Azure Dashboard**;
- Analisar as limitações do gerenciamento de custos em uma conta Azure Free Trial.

---

## 🏗️ Ambiente utilizado

| Recurso | Configuração |
|---|---|
| Provedor | Microsoft Azure |
| Assinatura | Azure subscription 1 |
| Tipo de conta | Azure Free Trial |
| Resource Group | `rg-dio-datafactory` |
| Data Factory | `adf-dio-kennedy-2026` |
| Região | Brazil South |
| Ferramentas | Azure Portal, Azure Cloud Shell e Azure CLI |
| IaC | ARM Template |

---

# 🚀 Etapas do projeto

## 1. Criação do Resource Group

O primeiro passo foi criar um **Resource Group**, utilizado para organizar e gerenciar os recursos relacionados ao projeto.

O grupo criado foi:

`rg-dio-datafactory`

A utilização de Resource Groups facilita a organização dos recursos, além de permitir o gerenciamento conjunto de permissões, configurações e ciclo de vida.

### 📷 Evidência

![Resource Manager](./01%20resources%20manager.png)

---

## 2. Criação do Azure Data Factory

Após a criação do Resource Group, foi provisionado um recurso do tipo **Azure Data Factory (V2)**.

Configurações principais:

- Nome: `adf-dio-kennedy-2026`
- Região: `Brazil South`
- Resource Group: `rg-dio-datafactory`

O Azure Data Factory é um serviço de integração de dados utilizado para criar e gerenciar pipelines capazes de movimentar e transformar dados entre diferentes fontes e destinos.

### 📷 Evidência

![Azure Data Factory](./02%20data%20factory.png)

---

## 3. Exploração do Data Factory Studio

Com o Data Factory provisionado, foi acessado o ambiente **Data Factory Studio**, responsável pela criação e gerenciamento dos componentes de integração de dados.

O Studio permite trabalhar com elementos como:

- Pipelines;
- Datasets;
- Linked Services;
- Data Flows;
- Triggers;
- Monitoramento das execuções.

Nesta etapa foi possível conhecer a interface e a estrutura de desenvolvimento do Azure Data Factory.

### 📷 Evidência

![Data Factory Studio](./03%20data%20factory%20studio.png)

---

## 4. Azure Cloud Shell e ARM Template

Uma das etapas do projeto foi utilizar o **Azure Cloud Shell** para executar comandos do Azure CLI diretamente pelo navegador.

Foi utilizado um **ARM Template** para representar a infraestrutura como código.

O template foi utilizado para realizar a implantação do Azure Data Factory no Resource Group:

`rg-dio-datafactory`

Após a implantação, foi utilizado o Azure CLI para verificar os recursos existentes no Resource Group.

O resultado confirmou o recurso:

`adf-dio-kennedy-2026`

com status:

`Succeeded`

Essa etapa demonstrou na prática o conceito de **Infrastructure as Code (IaC)**, permitindo que a infraestrutura seja descrita por meio de arquivos e implantada de forma automatizada.

### 📷 Evidência

![Cloud Shell ARM Deployment](./04%20cloud%20shell%20arm%20deployment.png)

---

## 5. Configuração do orçamento de custos

Para praticar o controle financeiro dos recursos Azure, foi criado um orçamento mensal no **Cost Management**.

Configuração utilizada:

- Nome: `budget-dio-datafactory`
- Periodicidade: Mensal
- Orçamento: **R$ 100**
- Alertas: **50%, 80% e 100%**
- Tipo de alerta: **Custo real**

O orçamento permite acompanhar o consumo da assinatura e estabelecer limites para receber notificações conforme os gastos se aproximam do valor definido.

### 📷 Evidência

![Orçamento custos](./05%20orçamento%20custos.png)

---

## 6. Análise de custos da assinatura

Também foi acessada a área de **Análise de custo** da assinatura Azure.

Durante a atividade, a assinatura apresentou uma limitação relacionada à disponibilidade dos dados de Cost Management.

Mesmo com o orçamento configurado corretamente, a análise detalhada de custos não apresentou dados de utilização naquele momento.

A própria visão geral da assinatura indicava:

- Custo atual: **R$ 0,00**
- Previsão: **R$ 0,00**
- Nenhum uso emitido de recurso ativo.

Essa situação foi importante para compreender que a disponibilidade das informações de custos pode variar conforme o tipo de oferta/assinatura e o tempo necessário para que os dados de consumo sejam processados.

### 📷 Evidência

![Análise de custo da assinatura](./06%20analise%20de%20custo%20assinatura.png)

---

## 7. Monitoramento por métricas

Foi acessada a área de **Métricas** do Azure Data Factory para visualizar informações de monitoramento do recurso.

Uma das métricas analisadas foi:

**Failed pipeline runs metrics (Count)**

A métrica apresentou valor igual a **0**, indicando que não havia execuções de pipelines com falha no período analisado.

Essa etapa demonstrou como o Azure Monitor pode ser utilizado para acompanhar indicadores relacionados aos recursos implantados.

### 📷 Evidência

![Métricas do Data Factory](./07%20metricas%20data.png)

---

## 8. Personalização do Azure Dashboard

Por fim, foi criado e personalizado um **Azure Dashboard** para centralizar informações importantes do projeto.

O dashboard foi configurado com informações relacionadas ao ambiente criado, incluindo:

- Azure Data Factory;
- Resource Group;
- Região;
- Orçamento mensal;
- Alertas de custo;
- ARM Template;
- Azure Cloud Shell.

A utilização de dashboards facilita a visualização e organização das informações relevantes em um único ambiente.

### 📷 Evidência

![Azure Dashboard](./08%20dashboard%20azure.png)

---

# 🧩 Infrastructure as Code

Um dos principais aprendizados do projeto foi a utilização do conceito de **Infrastructure as Code (IaC)**.

Em vez de depender exclusivamente da criação manual dos recursos pelo Portal do Azure, o ambiente pode ser representado por meio de um template.

O **ARM Template** utilizado descreve a criação do Azure Data Factory e suas principais propriedades.

Exemplo simplificado da estrutura:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "factoryName": {
      "type": "string",
      "defaultValue": "adf-dio-kennedy-2026"
    },
    "location": {
      "type": "string",
      "defaultValue": "Brazil South"
    }
  },
  "resources": [
    {
      "type": "Microsoft.DataFactory/factories",
      "apiVersion": "2018-06-01",
      "name": "[parameters('factoryName')]",
      "location": "[parameters('location')]",
      "identity": {
        "type": "SystemAssigned"
      },
      "properties": {}
    }
  ]
}
