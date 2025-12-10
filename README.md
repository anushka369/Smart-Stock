# 🧊 SmartStock – Inventory Heatmap & Early Stock-Out Alerts

*AI for Good Hackathon – Snowflake x YourStory*

SmartStock helps hospitals, public distribution systems, NGOs and social programs maintain availability of essential goods (medicines, vaccines, food supplies) through **data-driven inventory visibility**, **early warnings**, and **simple reorder suggestions** — fully running **inside Snowflake**.

---

## 🚨 Problem

Inventory, usage and procurement systems are often disconnected, leading to:

* Stock-outs of critical supplies
* Emergency purchases
* Waste due to expiry or over-purchasing
* Lack of early visibility & analytics

This impacts **health outcomes**, **supply chain efficiency**, and **budget utilisation**.

---

## 💡 Solution

SmartStock aggregates daily stock data in Snowflake, continuously computes risk scores, detects upcoming shortages, and provides:

* Inventory Heatmap (item × location)
* “Likely to run out in X days”
* Suggested reorder quantity
* Exportable procurement list
* Plain-language summaries using AI SQL

---

## 🌟 Features

✔ Daily inventory/usage ingestion
✔ Rolling demand estimation
✔ Days-of-cover + Stock-out probability
✔ Streamlit dashboard & heatmap
✔ Reorder suggestion engine
✔ Downloadable procurement CSV
✔ Action logging with Unistore
✔ Optional Cortex / AI SQL summaries

---

## 🧱 Architecture

### Built using

* Snowflake Dynamic Tables
* Streams & Tasks (CDC + scheduling)
* Snowpark Python (forecast UDFs)
* Unistore (Hybrid Tables for action logs)
* Streamlit UI
* (Optional) Cortex / AI SQL for summarization

### Data flow

```
Source → Landing Tables → Streams/Tasks → Dynamic Tables
 → Stock-risk Model → Action List → Streamlit UI
```
---

## 🧪 Data Schema

### inventory_daily

| column         | type      |
| -------------- | --------- |
| location       | string    |
| item_name      | string    |
| opening_stock  | number    |
| received       | number    |
| issued         | number    |
| closing_stock  | number    |
| lead_time_days | number    |
| updated_at     | timestamp |

### usage_daily

| column          | type   |
| --------------- | ------ |
| location        | string |
| item_name       | string |
| issued_quantity | number |
| date            | date   |

---

## ⚙ Setup & Run

### 1️⃣ Clone repo

```
git clone https://github.com/anushka369/smart-stock.git
cd smartstock
```

### 2️⃣ Load sample CSV files

Upload to Snowflake stage:

```
PUT file://sample_data/*.csv @STAGE_NAME;
```

### 3️⃣ Run database setup SQL

```
/sql/create_tables.sql
/sql/create_streams_and_tasks.sql
/sql/create_dynamic_tables.sql
```

### 4️⃣ Start Streamlit

```
streamlit run app.py
```

---

## 🤖 AI Logic

SmartStock uses:

* Rolling averages
* Weighted moving average
* Safety-stock + lead-time calculation
* Snowpark UDF forecast (7/14/28 day)

---

## 🔒 Privacy

Sensitive records stay fully inside Snowflake. Only aggregated, non-PII insights are exported.

---

## 🚀 Roadmap

* Auto-create purchase orders
* SMS / WhatsApp alerts
* Mobile-first UI
* Multi-agency clean room sharing
* LLM explanations for why reorder is recommended

---

## 🧰 Tech Stack

**Snowflake**

* Dynamic Tables
* Streams & Tasks
* Snowpark
* Unistore
* Cortex (optional)

**Frontend**

* Streamlit

---

## 🤝 Contributing

PRs welcome!
Please open issues or feature requests.

---
