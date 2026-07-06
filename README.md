# Projeto de Análise Exploratória de Dados (EDA) - Vendas

## Descrição

Este projeto tem como objetivo realizar uma **Análise Exploratória de Dados (EDA)** utilizando um dataset de vendas, com foco na identificação de padrões, tratamento de inconsistências e geração de insights para apoio à tomada de decisão.

---

## Objetivos

- Explorar e tratar uma base de dados real
- Identificar padrões, tendências e inconsistências
- Gerar insights estratégicos para negócios
- Praticar integração com armazenamento em nuvem (Azure)

---

## Tecnologias e Ferramentas

- Python (Pandas, Matplotlib)
- Excel
- Azure Blob Storage
- Azure Machine Learning (Notebook)

---

## Dataset

- Fonte: Kaggle (Sample Sales Data)
- Arquivo original: `sales_data_sample.csv`
- Arquivo utilizado: `datavendas.csv`

---

## Armazenamento em Nuvem

### Azure Storage Account

- Resource Group: `rg-dados-estudo`
- Storage Account: `storagepaoladados`
- Container: `dados-vendas`

O arquivo CSV foi carregado no container para simular um ambiente real de ingestão de dados em nuvem.

---

## Conexão com Azure Blob Storage

</> Python

from azure.storage.blob import BlobServiceClient

connection_string = "SUA_CONNECTION_STRING"

container_name = "dados-vendas"
blob_name = "datavendas.csv"

blob_service_client = BlobServiceClient.from_connection_string(connection_string)

blob_client = blob_service_client.get_blob_client(
    container=container_name,
    blob=blob_name
)

with open("arquivo.csv", "wb") as f:
    f.write(blob_client.download_blob().readall())

print("Download concluído!")

Ambiente de Desenvolvimento
Plataforma: Azure Machine Learning
Workspace: mlw-paola
Notebook: eda-vendas.ipynb

Etapas da Análise
1. Carregamento dos dados
import pandas as pd

df = pd.read_csv('data/vendas.csv', encoding='latin1')
df.head()

Entendimento da base
df.info()
df.describe()
df.columns

Análises realizadas:

Tipos de dados
Valores nulos
Estrutura das colunas
Estatísticas descritivas

Tratamento de dados

Verificação de valores nulos:

df.isnull().sum()

Conversão de datas:

df['ORDERDATE'] = pd.to_datetime(df['ORDERDATE'])

Análises exploratórias
Faturamento total
df['SALES'].sum()

Vendas por ano
df.groupby('YEAR_ID')['SALES'].sum()

Vendas por mês
df.groupby('MONTH_ID')['SALES'].sum().sort_values(ascending=False)

Vendas por país
df.groupby('COUNTRY')['SALES'].sum().sort_values(ascending=False)

Top 10 clientes
df.groupby('CUSTOMERNAME')['SALES'].sum().sort_values(ascending=False).head(10)

Produtos mais vendidos
df.groupby('PRODUCTLINE')['SALES'].sum().sort_values(ascending=False)

Criação de métricas
Ticket médio
df["TICKET_MEDIO"] = df["SALES"] / df["QUANTITYORDERED"]
df["TICKET_MEDIO"].mean()

Visualizações
Vendas por ano
import matplotlib.pyplot as plt

df.groupby('YEAR_ID')['SALES'].sum().plot()
plt.show()

Vendas por mês
df.groupby("MONTH_ID")["SALES"].sum().plot(kind="line")
plt.title("Vendas por Mês")
plt.show()

Principais Insights
Identificação dos países com maior volume de vendas
Descoberta das linhas de produtos mais lucrativas
Análise da sazonalidade das vendas ao longo dos meses
Identificação dos principais clientes (maior receita)
Cálculo do ticket médio por pedido