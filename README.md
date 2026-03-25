# 🌦️ Pipeline ETL de Dados Meteorológicos (OpenWeather API)

Projeto de engenharia de dados que implementa um pipeline ETL completo utilizando arquitetura **Medallion (Bronze, Silver, Gold)** para ingestão, transformação e armazenamento de dados meteorológicos da cidade de São Paulo.

---

## 📌 Visão Geral

Este projeto coleta dados em tempo real da API **OpenWeather**, processa os dados em diferentes camadas e os disponibiliza em um formato estruturado para análise.

O pipeline é orquestrado com **Apache Airflow** e executado em ambiente containerizado com **Docker**.

---

## 🏗️ Arquitetura

A arquitetura segue o padrão **Medallion Architecture**:

```
OpenWeather API → Bronze → Silver → Gold → PostgreSQL
```

### 🔹 Bronze (Raw Layer)

* Extração direta da API
* Dados armazenados em formato JSON bruto
* Nenhuma transformação aplicada

### 🔹 Silver (Clean Layer)

* Normalização do JSON
* Flatten de estruturas aninhadas
* Padronização de colunas
* Conversão de timestamps para datetime

### 🔹 Gold (Curated Layer)

* Dados prontos para análise
* Estrutura tabular otimizada
* Padronização final para consumo analítico

---

## ⚙️ Tecnologias Utilizadas

* **Python**
* **Apache Airflow**
* **Docker & Docker Compose**
* **PostgreSQL**
* **Pandas**
* **OpenWeather API**

---

## 🔄 Pipeline ETL

### 1. Extração (Extract)

* Consumo da API OpenWeather
* Armazenamento dos dados em JSON (`weather_data.json`)

### 2. Transformação (Transform)

Principais etapas:

* Normalização da coluna `weather`
* Remoção de colunas desnecessárias
* Renomeação de colunas
* Conversão de timestamps Unix para datetime (timezone: America/Sao_Paulo)

### 3. Carga (Load)

* Inserção dos dados tratados no PostgreSQL
* Estrutura otimizada para consultas analíticas

---

## 📊 Estrutura dos Dados (Gold)

| Coluna              | Descrição              |
| ------------------- | ---------------------- |
| city_name           | Nome da cidade         |
| temperature         | Temperatura atual (°C) |
| feels_like          | Sensação térmica       |
| humidity            | Umidade (%)            |
| pressure            | Pressão atmosférica    |
| wind_speed          | Velocidade do vento    |
| weather_main        | Condição principal     |
| weather_description | Descrição detalhada    |
| datetime            | Data/hora da medição   |
| sunrise             | Nascer do sol          |
| sunset              | Pôr do sol             |

---

## 🧠 Orquestração com Airflow

* DAG responsável pelo pipeline completo
* Execução agendada (scheduler)
* Monitoramento via UI do Airflow
* Separação clara entre tarefas (extract, transform, load)

---

## 🐳 Ambiente com Docker

O projeto roda totalmente containerizado:

* Airflow (Scheduler + Webserver)
* PostgreSQL
* Serviços auxiliares

### Subir ambiente:

```bash
docker compose up -d
```

### Acessar Airflow:

```
http://localhost:8080
```

---

## 📁 Estrutura do Projeto

```
projeto_weather/
│
├── dags/                  # DAGs do Airflow
├── src/                   # Scripts de ETL
│   ├── extract/
│   ├── transform/
│   └── load/
│
├── data/                  # Dados locais (bronze/silver)
├── config/                # Variáveis de ambiente
├── docker/                # Configurações Docker
├── docker-compose.yml
└── README.md
```

---

## 🚀 Como Executar

1. Clone o repositório:

```bash
git clone https://github.com/seu-usuario/projeto_weather.git
cd projeto_weather
```

2. Configure o `.env`

3. Suba os containers:

```bash
docker compose up -d
```

4. Acesse o Airflow e ative a DAG

---

## 📈 Possíveis Melhorias

* Integração com Data Warehouse (BigQuery, Snowflake)
* Dashboard com Power BI / Streamlit
* Particionamento de dados
* Testes automatizados (Pytest)
* CI/CD com GitHub Actions

---

## 👨‍💻 Autor

**Julio**
Projeto desenvolvido para portfólio de Engenharia de Dados.

---

## ⭐ Objetivo do Projeto

Demonstrar habilidades em:

* Construção de pipelines ETL
* Arquitetura de dados (Medallion)
* Orquestração com Airflow
* Containerização com Docker
* Integração com APIs
* Modelagem de dados

---
