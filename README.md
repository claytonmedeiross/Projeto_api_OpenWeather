Documentação do Projeto: Pipeline de Dados OpenWeather (Medallion Architecture)
1. Visão Geral
Este projeto implementa um pipeline de dados automatizado no Databricks para ingestão e processamento de dados climáticos em tempo real da cidade de Curitiba, utilizando a API da OpenWeather. O objetivo é estruturar os dados para alimentar um dashboard no Power BI com atualizações horárias.

2. Arquitetura da Solução
A arquitetura segue o padrão Medallion, garantindo qualidade e linhagem dos dados:

Ingestão (API): Consumo via Python (requests) extraindo dados JSON.

Camada Bronze (Raw): Armazenamento dos dados brutos em formato Delta, incluindo metadados como ingestion_timestamp.

Camada Silver (Trusted): Limpeza e "achatamento" (flattening) das estruturas JSON. Conversão de tipos e ajuste de fuso horário para America/Sao_Paulo.

Camada Gold (Refined): Deduplicação de registros e consolidação final em uma tabela otimizada para consumo analítico.

3. Detalhes Técnicos
Stack Tecnológica
Linguagens: Python (PySpark, Pandas) e SQL.

Plataforma: Databricks com Unity Catalog.

Armazenamento: Delta Lake (Volumes Gerenciados).

Orquestração: Databricks Workflows (Job agendado de 1h em 1h).

Visualização: Power BI (Conectado via Databricks SQL Warehouse com Token de Acesso Pessoal - PAT).

Estrutura de Dados (Data Modeling)
A tabela final projeto_api.pro_clima.clima_consolidado contém:

cidade: Nome da localidade.

temperatura: Valor em Celsius.

umidade: Percentual de umidade relativa.

condicao_tempo: Descrição textual do clima.

velocidade_vento: Velocidade convertida.

data_referencia: Timestamp do momento da medição da API.

4. Implementação do Pipeline
Camada de Governança
O projeto utiliza o Unity Catalog para organizar os dados:

SQL
CREATE CATALOG IF NOT EXISTS projeto_API;
CREATE SCHEMA IF NOT EXISTS projeto_API.pro_clima;
Automação (Jobs)
Frequência: Recorrência horária (0 * * * *).

Token de Conexão: A segurança da integração com o Power BI é mantida via PAT (Personal Access Token), configurado no SQL Warehouse do Databricks para garantir que o dashboard reflita sempre a última extração da camada Gold.

5. Como Reproduzir
Obtenha uma chave de API no OpenWeather.

Configure os Volumes no seu ambiente Databricks.

Execute o notebook de ingestão para criar as tabelas iniciais.

Configure o Databricks SQL Warehouse e conecte o Power BI utilizando o Server Hostname e o HTTP Path fornecidos.
<img width="1558" height="900" alt="image" src="https://github.com/user-attachments/assets/2a2fa0b2-9634-497b-ad2b-e68a548189d1" />
<img width="1332" height="722" alt="image" src="https://github.com/user-attachments/assets/ea0e2ec4-4ea7-4d4f-99cd-3195103ef491" />

