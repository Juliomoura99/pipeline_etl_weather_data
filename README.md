# 🌦️ Weather Data ETL Pipeline (OpenWeather API)

Data engineering project that implements a complete ETL pipeline using the **Medallion Architecture (Bronze, Silver, Gold)** for the ingestion, transformation, and storage of weather data from the city of São Paulo.

---

## 📌 Overview

This project collects real-time data from the **OpenWeather API**, processes the data across different layers, and makes it available in a structured format for analysis.

The pipeline is orchestrated with **Apache Airflow** and executed in a containerized environment with **Docker**.

---

## 🏗️ Architecture

The architecture follows the **Medallion Architecture** pattern:

```text
OpenWeather API → Bronze → Silver → Gold → PostgreSQL
