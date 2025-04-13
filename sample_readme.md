
# 📊 AWS Data Pipeline: CSV → Glue → MySQL  

## 📋 Project Overview  
This project demonstrates a simple **serverless data pipeline** built on AWS, where:
- CSV files are **uploaded to an S3 bucket**  
- **AWS Glue** processes and transforms the data  
- The processed data is **stored in a MySQL database**

The project can serve as a base framework for data ingestion, transformation, and loading pipelines in real-world scenarios.

---

## 🗄️ Data Sources

### 📦 customer_data.csv  
**Description:** Contains customer personal details and metadata.  
**Source:** CSV uploaded manually to `s3://my-data-pipeline-bucket/customer_data/`  

**Schema:**

| Column Name | Data Type | Description |
|:------------|:------------|:------------|
| customer_id  | INTEGER | Unique identifier |
| first_name   | STRING  | First name |
| last_name    | STRING  | Last name |
| email        | STRING  | Email address |
| signup_date  | DATE    | Signup date |

---

## 🏗️ Architecture  

```
[S3: CSV Files] 
      │
      ▼
[AWS Glue: ETL Job]
      │
      ▼
[MySQL Database (RDS)]
```

**Components:**
- **AWS S3** — Storage for raw CSV files  
- **AWS Glue** — Serverless ETL service for processing and transforming data  
- **MySQL (Amazon RDS)** — Relational database for storing cleaned, transformed data  

---

## 🔄 Pipeline Workflow  

1. **Upload CSV files** into the `customer_data/` folder in S3.
2. Trigger the **AWS Glue ETL Job** to:
   - Extract data from S3
   - Clean and transform the data (e.g., date formatting, deduplication)
   - Load the processed data into a **MySQL database**
3. Use **SQL queries** or BI tools to visualize or analyze the data.

---

## 💾 Setup Instructions  

### 1️⃣ Requirements  
- AWS account  
- AWS CLI installed and configured  
- AWS Glue permissions  
- MySQL RDS instance set up  

### 2️⃣ Upload Data to S3  
```bash
aws s3 cp customer_data.csv s3://my-data-pipeline-bucket/customer_data/
```

### 3️⃣ Run the Glue Job  
In AWS Console:
- Go to **AWS Glue > Jobs**
- Select **customer-data-etl-job**
- Click **Run Job**

Or via CLI:
```bash
aws glue start-job-run --job-name customer-data-etl-job
```

---

## 💡 Usage Examples  

### 🔍 Query Processed Data in MySQL  
```sql
SELECT 
    customer_id, 
    CONCAT(first_name, ' ', last_name) AS full_name, 
    email, 
    signup_date 
FROM 
    customers 
WHERE 
    signup_date >= '2023-01-01'
ORDER BY 
    signup_date DESC;
```

---

## ✅ Project Features  

- ✅ S3-based raw data ingestion  
- ✅ Serverless ETL processing using AWS Glue  
- ✅ Data loading into MySQL (Amazon RDS)  
- ✅ Ready for integration with BI tools (like Power BI, QuickSight)

---

## 📁 Project Structure  

```
├── data/
│   └── customer_data.csv          # Sample CSV file
├── glue_jobs/
│   └── customer_etl_script.py     # Glue ETL Python script
├── scripts/
│   └── upload_to_s3.sh            # S3 upload helper
└── README.md                      # Project guide
```

---

## 📚 Documentation  

- **Glue Job Script:** [glue_jobs/customer_etl_script.py](glue_jobs/customer_etl_script.py)  
- **MySQL Table DDL:** [schemas/customers.sql](schemas/customers.sql)  
- **Troubleshooting:** See [docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md)

---

## 🙌 Contributing  

1. Fork this repository  
2. Create your feature branch (`git checkout -b feature/my-new-feature`)  
3. Commit your changes (`git commit -m 'Add some feature'`)  
4. Push to the branch (`git push origin feature/my-new-feature`)  
5. Create a new Pull Request  

---

## 📬 Contact  

**Your Name**  
- LinkedIn: [linkedin.com/in/yourname](#)  
- GitHub: [github.com/yourname](#)

---

## 📌 License  

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
