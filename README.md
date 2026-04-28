# ☁️ Weather Data Pipeline: OpenWeather + Databricks (Medallion Architecture)

Este projeto demonstra um pipeline de engenharia de dados de ponta a ponta, realizando a ingestão, transformação e disponibilização de dados meteorológicos de Curitiba, utilizando a API da **OpenWeather** e a plataforma **Databricks**.

## 🚀 Visão Geral

O objetivo principal é capturar dados climáticos em tempo real, processá-los através das camadas **Bronze**, **Silver** e **Gold** (Arquitetura Medalhão) e servir uma tabela final otimizada para um dashboard no **Power BI**.

## 🏗️ Arquitetura do Projeto

O pipeline foi estruturado seguindo as melhores práticas de engenharia de dados:

1.  **Ingestão:** Script Python utilizando a biblioteca `requests` para consumo da API OpenWeather.
2.  **Bronze (Raw):** Dados brutos armazenados em formato **Delta** com adição de metadados (`ingestion_timestamp`).
3.  **Silver (Trusted):** Tratamento de tipos de dados (Casting), achatamento de JSON e conversão de fuso horário para `America/Sao_Paulo`.
4.  **Gold (Refined):** Deduplicação de registros e criação de tabela consolidada no **Unity Catalog** para consumo analítico.

## 🛠️ Tecnologias Utilizadas

* **Linguagens:** Python (PySpark), SQL.
* **Data Lakehouse:** Databricks & Delta Lake.
* **Governança:** Unity Catalog (Catalogs, Schemas e Volumes).
* **Orquestração:** Databricks Workflows (Job agendado de 1h em 1h).
* **Visualização:** Power BI (Conectado via Databricks SQL Warehouse com Personal Access Token).

## 📊 Estrutura do Pipeline (Notebook)

O código está dividido em células que realizam:
* A configuração do catálogo e esquemas.
* A extração da API para um DataFrame Spark.
* A persistência histórica na camada Bronze.
* A limpeza e transformação para a Silver.
* A consolidação final na tabela `projeto_api.pro_clima.clima_consolidado`.

## ⚙️ Automação e Integração

* **Agendamento:** Um Job no Databricks foi configurado para rodar o pipeline a cada hora, garantindo que o dashboard esteja sempre atualizado.
* **Conexão Power BI:** A integração é feita via conector nativo do Databricks, utilizando autenticação por **Token (PAT)** para garantir segurança e performance na atualização dos dados.

---
⭐ *Projeto desenvolvido por Clayton Antonio Medeiros da Silva*
<img width="1558" height="900" alt="image" src="https://github.com/user-attachments/assets/2a2fa0b2-9634-497b-ad2b-e68a548189d1" />
<img width="1332" height="722" alt="image" src="https://github.com/user-attachments/assets/ea0e2ec4-4ea7-4d4f-99cd-3195103ef491" />

