 🛒 Pipeline E-commerce | Azure + Databricks + Power BI

Projeto de Engenharia de Dados que implementa um pipeline completo para análise de vendas de e-commerce utilizando Azure Data Lake Storage Gen2, Azure Databricks, Delta Lake e Power BI, seguindo a arquitetura Medallion (Bronze → Silver → Gold).

 Objetivo

Construir uma solução moderna de processamento de dados capaz de:

* Ingerir dados brutos de vendas
* Realizar limpeza e transformação dos dados
* Criar camadas analíticas escaláveis
* Disponibilizar métricas para consumo em dashboards executivos
* Demonstrar boas práticas de Engenharia de Dados em ambiente Azure

Arquitetura da Solução

text
Azure Data Lake Storage Gen2
        │
        ▼
┌─────────────────────────────────────────────┐
│              01_bronze.ipynb                │
│   Ingestão do CSV bruto → camada Bronze     │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│              02_silver.ipynb                │
│  Limpeza, tipagem e transformações → Silver │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│          04_registro_tabelas.ipynb          │
│     Agregações e registro no metastore      │
│              → camada Gold                  │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│            Power BI Desktop                 │
│     Dashboard Executivo de Vendas           │
└─────────────────────────────────────────────┘

Estrutura do Repositório

text
pipeline-ecommerce-azure-databricks/
│
├── notebooks/
│   ├── 00_config.ipynb
│   ├── 01_bronze.ipynb
│   ├── 02_silver.ipynb
│   └── 04_registro_tabelas.ipynb
│
├── dados/
│   └── vendas_ecommerce.csv
│
├── powerbi/
│   └── Dashboard_Vendas_Ecommerce.pbix
│
└── README.md

Tecnologias Utilizadas

| Tecnologia                   | Finalidade                             |
| ---------------------------- | -------------------------------------- |
| Azure Data Lake Storage Gen2 | Armazenamento das camadas de dados     |
| Azure Databricks             | Processamento distribuído              |
| PySpark                      | Transformações e agregações            |
| Delta Lake                   | Persistência das camadas Silver e Gold |
| Power BI Desktop             | Visualização e análise de dados        |


 Dataset

Base fictícia de vendas de e-commerce contendo 500 registros e 17 colunas.

| Coluna            | Descrição                     |
| ----------------- | ----------------------------- |
| `order_id`        | Identificador único do pedido |
| `data_pedido`     | Data da compra                |
| `cliente_id`      | Identificador do cliente      |
| `nome_cliente`    | Nome do cliente               |
| `cidade`          | Cidade do cliente             |
| `estado`          | Estado do cliente             |
| `produto_nome`    | Produto adquirido             |
| `categoria`       | Categoria do produto          |
| `quantidade`      | Quantidade comprada           |
| `preco_unitario`  | Valor unitário                |
| `desconto_pct`    | Percentual de desconto        |
| `valor_total`     | Valor final da compra         |
| `frete`           | Valor do frete                |
| `canal_venda`     | Canal de venda                |
| `forma_pagamento` | Método de pagamento           |
| `status_pedido`   | Status do pedido              |


Camadas do Pipeline

Bronze

Camada responsável pela ingestão dos dados brutos.

Atividades

* Leitura do arquivo CSV
* Armazenamento sem transformações
* Preservação da fonte original

Silver

Camada de tratamento e padronização dos dados.

 Transformações realizadas

* Remoção de registros nulos
* Filtragem de pedidos cancelados
* Conversão da coluna `data_pedido` para `DateType`
* Criação da coluna:

python
receita_liquida = valor_total + frete


* Padronização de estados para letras maiúsculas
* Ajustes de tipagem

 Gold

Camada analítica destinada ao consumo por BI.

 Tabelas Geradas

| Tabela           | Descrição                                        |
| ---------------- | ------------------------------------------------ |
| `gold_categoria` | Receita, ticket médio e quantidade por categoria |
| `gold_canal`     | Receita por canal de venda                       |
| `gold_estado`    | Receita e pedidos por estado                     |
| `gold_status`    | Quantidade de pedidos por status                 |

Todas as tabelas são registradas no Metastore do Databricks para consulta SQL.

 Dashboard Power BI

O dashboard executivo disponibiliza os seguintes indicadores:

 KPIs

* Receita Total
* Total de Pedidos
* Ticket Médio
* Taxa de Devoluções

Visualizações

* Receita por Categoria
* Pedidos por Canal de Venda
* Receita por Estado
* Evolução de Vendas

 Como Executar o Projeto

 1. Clonar o Repositório

bash
git clone https://github.com/seu-usuario/pipeline-ecommerce-azure-databricks.git


 2. Configurar o Azure Data Lake

* Criar uma conta Storage Gen2
* Criar o container de dados
* Fazer upload do arquivo:

text
dados/vendas_ecommerce.csv


3. Configurar o Databricks

Importar os notebooks da pasta:

text
notebooks/


Substituir:

python
SUA_CHAVE_AQUI


pela chave de acesso do Storage Account.

Executar os notebooks na seguinte ordem:

text
00_config.ipynb
        ↓
01_bronze.ipynb
        ↓
02_silver.ipynb
        ↓
04_registro_tabelas.ipynb


 4. Abrir o Dashboard

Abrir:

text
powerbi/Dashboard_Vendas_Ecommerce.pbix


Atualizar a conexão para o seu Workspace Databricks.

Principais Conceitos Demonstrados

* Arquitetura Medallion
* Data Lakehouse
* Delta Lake
* ETL com PySpark
* Data Quality
* Data Governance
* Modelagem Analítica
* Integração Azure + Power BI

Resultados Obtidos

* Pipeline completo de Engenharia de Dados
* Dados organizados em camadas Bronze, Silver e Gold
* Tabelas analíticas otimizadas para consumo
* Dashboard executivo para tomada de decisão
* Integração entre Azure, Databricks e Power BI

 Autor

**Seu Nome**

Projeto desenvolvido para fins de estudo e prática em Engenharia de Dados utilizando tecnologias modernas do ecossistema Azure.

LinkedIn: adicione seu perfil aqui

 Importante

> Nunca publique credenciais, tokens ou chaves de acesso em repositórios públicos.
>
> Utilize sempre variáveis de ambiente, Azure Key Vault ou substitua por:
>
> ```python
> SUA_CHAVE_AQUI
> ```
>
> antes de realizar qualquer commit.

