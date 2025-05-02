# AI-Based-Anomaly-Detection-in-Web-Logs

# 🛡️ AI-based Anomalous Login Detection

A lightweight AI-powered system that analyzes real-world web server logs (NGINX format) to detect anomalous behavior such as excessive 404 responses, using unsupervised machine learning (Isolation Forest).

---

## 📌 Overview

This project demonstrates how to use actual NGINX logs to detect suspicious IPs that generate an abnormally high number of `404 Not Found` responses, which may indicate scanning, probing, or attack attempts.

It leverages:
- Python for data handling
- Regular expressions to parse raw logs
- Isolation Forest (unsupervised ML) to detect anomalies
- Simple matplotlib visualization

---

## 🚀 Features

- ✅ Real log data ingestion (not simulated)
- 🔍 Parsing IP address, timestamp, HTTP status, URL
- 🤖 Unsupervised anomaly detection using Isolation Forest
- 📊 Visual representation of detected anomalies

---

## 🧰 Tech Stack

| Category        | Tools                     |
|-----------------|---------------------------|
| Programming     | Python 3 (Colab-friendly) |
| Data Handling   | pandas, re                |
| ML Algorithm    | Isolation Forest (sklearn)|
| Visualization   | matplotlib                |
| Data Source     | [Elastic NGINX Logs](https://raw.githubusercontent.com/elastic/examples/master/Common%20Data%20Formats/nginx_logs/nginx_logs) |

---

## 📂 Project Structure

```bash
├── log_parser.py         # optional: modularize log parsing
├── anomaly_detector.ipynb # main notebook (Colab)
└── README.md             # project documentation
📈 Workflow

1. Load NGINX Logs
import requests
log_text = requests.get("https://raw.githubusercontent.com/elastic/examples/master/Common%20Data%20Formats/nginx_logs/nginx_logs").text
2. Parse Logs into Structured Data
Using re module, extract:

IP Address
Timestamp
URL
HTTP Status
3. Filter and Group
df_404 = df[df['status'] == 404]
ip_404_counts = df_404['ip'].value_counts().reset_index()
4. Anomaly Detection
from sklearn.ensemble import IsolationForest
model = IsolationForest(contamination=0.1)
model.fit(ip_404_counts[['404_count']])
ip_404_counts['anomaly'] = model.predict(ip_404_counts[['404_count']])
5. Visualization
plt.scatter(..., c=ip_404_counts['anomaly'], cmap='coolwarm')

✅ Sample Output


Red dots represent anomalous IPs (likely attackers)

📌 Use Cases

Entry-level AI-based log analysis system
Demonstration of unsupervised learning in security
Foundation for expanding to SIEM-like behavior monitoring

🧠 Future Work

Add user-agent analysis
Time-based anomaly detection (e.g., bursts of login attempts)
Integrate supervised learning with labeled attack data

👤 Author

Jacob Yim (Personal AI Security Project)
For learning purposes & portfolio only

📝 License

This project is open for educational use.
