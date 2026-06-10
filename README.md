# Grafana Banking Dashboard

This project generates synthetic banking transaction data, stores it in PostgreSQL, and visualizes the results in Grafana. It was built as a hands-on exercise to practice connecting a Python data generator, a relational database, and a monitoring dashboard.

Public dashboard: [Grafana Banking Dashboard](https://boldmarigold1768.grafana.net/public-dashboards/9f4f0068f2b4451b82293427866800be)

## Project Overview

The notebook creates a `banking_data` table and continuously inserts small batches of synthetic transactions. Each transaction is evaluated with simple rule-based checks before being stored:

- Real-time transactions from blacklisted accounts are rejected.
- Real-time transactions above the amount threshold are rejected.
- Other transactions are approved.

Grafana reads from the PostgreSQL table and displays summary metrics such as approved and rejected transactions, transaction amounts, transaction types, triggered rules, and blacklisted account activity.

## Tech Stack

- Python
- PostgreSQL
- Grafana
- pandas
- Faker
- psycopg2
- python-dotenv

## Repository Structure

```text
.
├── app.ipynb          # Data generator and PostgreSQL table setup
├── config.sample     # Example environment configuration
├── queries.txt       # SQL queries used for Grafana panels
├── requirements.txt  # Python dependencies
└── README.md
```

## Setup

Create and activate a virtual environment:

```bash
python3 -m venv env-grafana
source env-grafana/bin/activate
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

Create a local `.env` file from the sample configuration:

```bash
cp config.sample .env
```

Then update `.env` with your PostgreSQL connection details:

```text
DB_HOST="your-postgres-host"
DB_PORT=5432
DB_NAME="postgres"
DB_USER="postgres"
DB_PASSWORD="your-postgres-password"
```

The `.env` file is ignored by Git and should not be committed.

## Running the Data Generator

Open `app.ipynb` and run the cells in order. The final cell continuously inserts new records into PostgreSQL in small batches so the Grafana dashboard has fresh data to display.

Stop the notebook cell manually when you want to stop generating data.

## Grafana Panels

The dashboard is based on the SQL queries in `queries.txt`, including:

- Approved transaction count
- Rejected transaction count
- Total approved amount
- Total rejected amount
- Transaction type distribution
- Triggered fraud rules
- Blacklisted account transactions

## Notes

The generated data is fully synthetic and created with Faker. No real customer or banking data is used.

This is intentionally a simple exercise project. The focus is on practicing the end-to-end flow from data generation to database storage and dashboard visualization.
