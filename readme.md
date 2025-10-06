# DATA 226 – Homework 5: Airflow DAG

**Author:** Vaheedur Rehman Mahmed  
**Course:** DATA 226 – Data Engineering  
**Instructor:** Prof. Vishnu Pendyala  
**University:** San José State University  

---

## 🧠 Overview
This assignment extends Homework 4 by porting the ETL pipeline into **Apache Airflow**.  
The DAG fetches 90 days of stock price data from the **Alpha Vantage API**, performs light transformations using Pandas, and loads the data into **Snowflake** using a full-refresh transaction.

---

## ⚙️ Files in This Repository
| File | Description |
|------|--------------|
| `data226_hw5_dag.py` | Airflow DAG file implementing the ETL pipeline |
| `docker-compose.yaml` | Airflow environment setup for Docker Compose |

---

## 🧩 DAG Structure
**DAG ID:** `data226_hw5_stock_pipeline`

**Tasks:**
1. `fetch_data` → Fetches stock data from Alpha Vantage API  
2. `transform_data` → Cleans and filters the last 90 days of data  
3. `load_to_snowflake` → Loads transformed data into Snowflake via full-refresh SQL transaction

**Task Flow:**
fetch_data → transform_data → load_to_snowflake

---

## 🔑 Airflow Setup Steps
1. **Add Variable**
   - Go to: *Admin → Variables → + Add*
   - Key: `ALPHA_VANTAGE_API_KEY`
   - Value: `<your Alpha Vantage API key>`

2. **Add Connection**
   - Go to: *Admin → Connections → + Add*
   - Conn ID: `snowflake_conn`
   - Conn Type: `Snowflake`
   - Fill in your Snowflake credentials (Account, User, Password, Warehouse, Database, Schema)

3. **Place DAG**
   - Copy `data226_hw5_dag.py` into your Airflow `/dags/` folder

4. **Run Airflow**
   ```bash
   docker compose up -d
