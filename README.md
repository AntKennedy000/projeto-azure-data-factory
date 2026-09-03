# ☁️ Projeto Azure Data Factory

## 📌 Sobre o projeto

Este projeto foi desenvolvido como parte de uma atividade prática de estudos em **Cloud Computing e Data Engineering**, utilizando o **Microsoft Azure**.

O objetivo foi criar e organizar um ambiente utilizando o **Azure Data Factory**, aplicar conceitos de **Infrastructure as Code (IaC)** por meio de **ARM Templates**, utilizar o **Azure Cloud Shell** para implantação via linha de comando e configurar recursos relacionados ao **monitoramento, métricas e controle de custos**.

O projeto também possibilitou analisar, na prática, algumas limitações e particularidades encontradas em uma assinatura **Azure Free Trial**.

---

## 🎯 Objetivos

- Criar um Resource Group para organização dos recursos;
- Provisionar um Azure Data Factory;
- Acessar e explorar o Data Factory Studio;
- Utilizar o Azure Cloud Shell;
- Criar e utilizar um ARM Template;
- Validar e implantar infraestrutura por linha de comando;
- Configurar orçamento e alertas de custos;
- Consultar informações de custos da assinatura;
- Consultar métricas do Azure Data Factory;
- Personalizar um dashboard no Azure Portal;
- Documentar o ambiente e os principais aprendizados obtidos.

---

## 🛠️ Tecnologias e serviços utilizados

- Microsoft Azure
- Azure Data Factory
- Azure Resource Manager (ARM)
- Azure Cloud Shell
- Azure CLI
- Azure Cost Management
- Azure Monitor / Metrics
- Azure Portal
- GitHub

---

## ☁️ Ambiente utilizado

| Recurso | Configuração |
|---|---|
| Plataforma | Microsoft Azure |
| Assinatura | Azure Free Trial |
| Resource Group | `rg-dio-datafactory` |
| Data Factory | `adf-dio-kennedy-2026` |
| Região | Brazil South |
| Orçamento mensal | R$ 100 |
| Alertas de custo | 50%, 80% e 100% |
| Infrastructure as Code | ARM Template |
| Linha de comando | Azure Cloud Shell + Azure CLI |

---

# 🏗️ Arquitetura do projeto

A estrutura criada para o projeto foi organizada da seguinte forma:

```text
Azure Free Trial
       │
       ▼
Azure Subscription
       │
       ▼
Resource Group
rg-dio-datafactory
       │
       ▼
Azure Data Factory
adf-dio-kennedy-2026
       │
       ├── Data Factory Studio
       │
       ├── Monitoramento
       │     └── Métricas
       │
       └── Infraestrutura
             └── ARM Template
                    │
                    ▼
              Azure Cloud Shell
                    │
                    ▼
                Azure CLI
```

Além disso, foi configurado o gerenciamento de custos da assinatura com um orçamento mensal e alertas.

---

# 🚀 Etapas do projeto

## 1. Criação do Resource Group

Foi criado o Resource Group `rg-dio-datafactory` na região **Brazil South**.

O Resource Group é utilizado para organizar e gerenciar os recursos relacionados ao projeto dentro da assinatura do Azure.

![Resource Group](./imagens/01%20resources%20manager.png)

---

## 2. Criação do Azure Data Factory

Dentro do Resource Group foi provisionado o Azure Data Factory:

```text
adf-dio-kennedy-2026
```

O recurso foi criado na região **Brazil South** e apresentou status de execução bem-sucedida.

![Azure Data Factory](./imagens/02%20data%20factory.png)

---

## 3. Acesso ao Data Factory Studio

Após a criação do recurso, foi realizado o acesso ao **Data Factory Studio**, ambiente utilizado para desenvolver e administrar soluções de integração de dados no Azure.

O Studio permite trabalhar com elementos como pipelines, atividades, conjuntos de dados, integrações e monitoramento.

![Data Factory Studio](./imagens/03%20data%20factory%20studio.png)

---

# 💻 4. Infrastructure as Code com ARM Template

Uma das etapas do projeto foi trabalhar com o conceito de **Infrastructure as Code (IaC)**.

Para isso, foi utilizado um **ARM Template**, permitindo representar a infraestrutura do Azure por meio de código.

O template utilizado define a criação de um recurso do tipo:

```text
Microsoft.DataFactory/factories
```

### Exemplo do template utilizado

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
```

O uso de templates permite padronizar a infraestrutura e facilita a reprodução do ambiente em outros contextos.

---

# ⌨️ 5. Azure Cloud Shell e Azure CLI

O **Azure Cloud Shell** foi utilizado para executar comandos da **Azure CLI** diretamente no ambiente do Azure.

Primeiramente, o template foi validado:

```bash
az deployment group validate \
  --resource-group rg-dio-datafactory \
  --template-file template.json
```

Em seguida, foi realizada a implantação:

```bash
az deployment group create \
  --resource-group rg-dio-datafactory \
  --template-file template.json
```

Por fim, foi realizada uma consulta aos recursos existentes no Resource Group:

```bash
az resource list \
  --resource-group rg-dio-datafactory \
  --output table
```

O resultado confirmou a existência do Azure Data Factory com status:

```text
Succeeded
```

![Cloud Shell ARM Deployment](./imagens/04%20cloud%20shell%20arm%20deployment.png)

---

# 💰 6. Gerenciamento de custos

O projeto também abordou o controle e monitoramento dos custos dos recursos do Azure.

Foi utilizado o **Azure Cost Management** para configurar um orçamento mensal.

### Orçamento configurado

```text
Nome: budget-dio-datafactory
Periodicidade: Mensal
Valor: R$ 100
```

Foram configurados alertas para os seguintes níveis de consumo:

- 50%;
- 80%;
- 100%.

No momento da configuração, o gasto avaliado estava em:

```text
R$ 0
```

![Orçamento de custos](./imagens/05%20orçamento%20custos.png)

---

# 📊 7. Consulta de custos da assinatura

Também foi realizada a consulta das informações gerais de custos da assinatura Azure.

Naquele momento, a assinatura apresentava:

```text
Custo atual: R$ 0
Previsão: R$ 0
```

A página também apresentou informações sobre os serviços gratuitos disponíveis e seus respectivos limites de utilização.

![Análise de custo da assinatura](./imagens/06%20analise%20de%20custo%20assinatura.png)

### ⚠️ Observação

Durante o projeto, a funcionalidade detalhada de **Cost Analysis** apresentou uma limitação relacionada ao tipo de oferta da assinatura Free Trial, retornando uma mensagem relacionada ao tipo de oferta `WebDirect/AIRS`.

Por esse motivo, a documentação não apresenta essa funcionalidade como se estivesse funcionando normalmente.

Essa situação foi importante para compreender que determinadas funcionalidades do Azure podem apresentar diferenças de disponibilidade dependendo do tipo de assinatura utilizada.

---

# 📈 8. Monitoramento por métricas

Foi realizada também a consulta de métricas do Azure Data Factory utilizando o recurso **Métrica** do Azure Monitor.

A métrica observada foi:

```text
Failed pipeline runs metrics
```

Essa métrica representa a quantidade de execuções de pipelines que apresentaram falha.

Durante o período analisado, o valor apresentado foi:

```text
0
```

Isso significa que não havia execuções de pipelines com falha registradas naquele período.

![Métricas do Data Factory](./imagens/07%20metricas%20data.png)

---

# 🖥️ 9. Personalização do Dashboard

Como parte da organização do ambiente, foi criado um **dashboard personalizado no Azure Portal**.

O dashboard foi configurado para centralizar informações relevantes do projeto, incluindo:

- Azure Data Factory;
- Resource Group;
- Região utilizada;
- Orçamento mensal;
- Alertas de custo;
- ARM Template;
- Azure Cloud Shell.

A personalização do dashboard facilita a visualização das principais informações do ambiente em um único local.

![Dashboard Azure](./imagens/08%20dashboard%20azure.png)

---

# 🧠 Aprendizados

A realização do projeto permitiu compreender, de forma prática, conceitos importantes relacionados à computação em nuvem e engenharia de dados.

### Resource Groups

Os Resource Groups facilitam a organização dos recursos do Azure, permitindo agrupar componentes relacionados a uma mesma solução.

### Azure Data Factory

O Azure Data Factory é uma plataforma de integração de dados que permite construir e gerenciar fluxos de dados e processos de integração.

### Infrastructure as Code

O uso de ARM Templates demonstra como a infraestrutura pode ser representada como código, permitindo maior padronização e repetibilidade na criação de recursos.

### Azure Cloud Shell

O Cloud Shell permite executar comandos de gerenciamento do Azure diretamente pelo navegador, sem a necessidade de instalar localmente todas as ferramentas utilizadas.

### Azure CLI

A Azure CLI possibilita automatizar operações de gerenciamento dos recursos por meio de comandos.

### Monitoramento

As métricas permitem acompanhar informações operacionais dos recursos e identificar possíveis problemas, como falhas na execução de pipelines.

### Gerenciamento de custos

A configuração de orçamentos e alertas permite acompanhar o consumo financeiro e estabelecer limites para reduzir o risco de gastos inesperados.

---

# 🔎 Insights e possibilidades

Durante a realização do projeto, alguns pontos importantes foram observados.

## 1. Automação da infraestrutura

A utilização de ARM Templates permite transformar uma configuração manual em uma infraestrutura reproduzível.

Em um projeto maior, esse conceito pode ser expandido para criar ambientes completos de desenvolvimento, homologação e produção.

## 2. Monitoramento preventivo

A configuração de métricas e alertas permite acompanhar o comportamento dos recursos e identificar problemas antes que eles se tornem maiores.

No caso do Data Factory, métricas relacionadas às execuções de pipelines podem ser utilizadas para acompanhar a estabilidade dos processos de integração.

## 3. Controle financeiro

A configuração de um orçamento mensal de R$ 100 demonstra a importância do controle de custos em ambientes de nuvem.

Em ambientes corporativos, esse conceito pode ser utilizado juntamente com políticas de governança, tags, centros de custo e alertas.

## 4. Limitações relacionadas à assinatura

O projeto também demonstrou que os recursos disponíveis podem variar de acordo com o tipo de assinatura do Azure.

A identificação da limitação no Cost Analysis foi um aprendizado prático importante, pois mostrou a necessidade de considerar o modelo de contratação e as características da assinatura durante o planejamento de uma solução em nuvem.

## 5. Evolução do projeto

Uma possível evolução seria criar uma solução completa de engenharia de dados utilizando:

```text
Azure Data Factory
        │
        ▼
Azure Storage / Data Lake
        │
        ▼
Processamento de dados
        │
        ▼
Banco de dados / Data Warehouse
        │
        ▼
Power BI
```

Também seria possível evoluir a infraestrutura como código utilizando ferramentas como **Terraform** ou pipelines de CI/CD para automatizar o provisionamento.

---

# 🧹 Limpeza dos recursos

Ao finalizar estudos ou testes no Azure, é importante avaliar a necessidade de manter os recursos ativos.

Como boa prática, recursos que não serão mais utilizados devem ser excluídos para evitar consumo desnecessário do crédito ou geração de custos após o término do período promocional.

Neste projeto, os principais recursos estão concentrados no Resource Group:

```text
rg-dio-datafactory
```

Dessa forma, o Resource Group pode ser utilizado como ponto central para gerenciamento e eventual limpeza do ambiente.

---

# 📁 Estrutura do repositório

```text
projeto-azure-data-factory/
│
├── README.md
├── template.json
│
└── imagens/
    ├── 01 resources manager.png
    ├── 02 data factory.png
    ├── 03 data factory studio.png
    ├── 04 cloud shell arm deployment.png
    ├── 05 orçamento custos.png
    ├── 06 analise de custo assinatura.png
    ├── 07 metricas data.png
    └── 08 dashboard azure.png
```

---

# 📚 Referências

- Microsoft Azure
- Azure Data Factory
- Azure Resource Manager
- Azure Cloud Shell
- Azure CLI
- Azure Cost Management
- Azure Monitor

---

# 👨‍💻 Autor

**Antony Kennedy**

Projeto desenvolvido para fins de estudo e portfólio na área de **Cloud Computing, Data Engineering e Data Science**.
