# 📊 Comcast Telecom Consumer Complaint Analysis

[![Python](https://img.shields.io/badge/Python-3.7%2B-blue?logo=python)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-1.x-150458?logo=pandas)](https://pandas.pydata.org/)
[![Gensim](https://img.shields.io/badge/Gensim-LDA-orange)](https://radimrehurek.com/gensim/)
[![NLTK](https://img.shields.io/badge/NLTK-NLP-green)](https://www.nltk.org/)
[![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-F37626?logo=jupyter)](https://jupyter.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> An end-to-end data analysis project exploring over **2,000 consumer complaints** filed against Comcast Telecommunications. This project combines **Exploratory Data Analysis (EDA)**, **time-series analysis**, **geospatial aggregation**, and **NLP topic modeling** to surface actionable insights about customer dissatisfaction.

---

## 📌 Business Context

Comcast, one of America's largest telecommunications companies, faced significant public backlash over its customer service quality. In October 2016, the FCC fined Comcast **\$2.3 million** after receiving over 1,000 consumer complaints. This project digs into the public complaint database to answer:

- **When** do complaints spike?
- **Where** (which states) are customers most dissatisfied?
- **What** are customers actually complaining about?
- **How effectively** are complaints being resolved?

---

## 🗂️ Project Structure

```
comcast_Telecom_cunsumer_complaint/
│
├── comcast.ipynb                          # Main analysis notebook
├── Comcast_telecom_complaints_data.csv    # Raw dataset (2015–2016)
├── comcast.pdf                            # Exported notebook (PDF)
├── writeup.docx                           # Analysis writeup document
└── README.md                              # This file
```

---

## 📋 Dataset Description

**File:** `Comcast_telecom_complaints_data.csv`  
**Source:** Public consumer complaint database  
**Period:** April 2015 – October 2015

| Column | Description |
|--------|-------------|
| `Ticket #` | Unique complaint identifier |
| `Customer Complaint` | Free-text description of the issue |
| `Date` | Date the complaint was filed |
| `Date_month_year` | Reformatted date column |
| `Time` | Time the complaint was filed |
| `Received Via` | Channel — *Internet* or *Customer Care Call* |
| `City` | Customer's city |
| `State` | Customer's US state |
| `Zip code` | Customer's zip code |
| `Status` | Complaint status — *Open*, *Pending*, *Closed*, *Solved* |
| `Filing on Behalf of Someone` | Whether complaint is on behalf of another person |

---

## 🔬 Analysis Pipeline

### 1. 🔧 Data Loading & Feature Engineering
- Load the CSV into a Pandas DataFrame
- Combine `Date_month_year` and `Time` into a unified `date_index` datetime column
- Set `date_index` as the DataFrame index for time-series operations

### 2. 📈 Complaint Volume Trends
- **Daily granularity**: Plot daily complaint counts to identify day-level spikes
- **Monthly granularity**: Use `pd.Grouper(freq="M")` to aggregate by month and visualize the complaint trajectory over time

### 3. 🔖 Status Classification
Create a simplified binary `newStatus` feature:
- **Open** ← `Open` + `Pending` (unresolved)
- **Closed** ← `Closed` + `Solved` (resolved)

### 4. 🗺️ State-wise Analysis
- Rank states by total complaint volume (top 5)
- Generate a **horizontal stacked bar chart** (State × Open/Closed) for all 50+ states
- Identify:
  - 🔴 State with the **most complaints**
  - 🟡 State with the **highest unresolved complaint rate**

### 5. 🧹 NLP Text Preprocessing
Apply a standard NLP pipeline to the `Customer Complaint` column:
1. **Lowercasing** — normalize text casing
2. **Stop-word removal** — filter common English words using NLTK
3. **Punctuation removal** — strip special characters
4. **Lemmatization** — reduce words to their root form using `WordNetLemmatizer`

### 6. 🧠 LDA Topic Modeling
- Build a **Bag-of-Words corpus** using Gensim's `corpora.Dictionary`
- Train an **LDA model** with `9 topics` and `30 passes` for stable topic discovery
- Display the top 20 keywords per topic to interpret complaint categories

### 7. 📞 Resolution Rate by Channel
Calculate and compare the **percentage of resolved complaints** for:
- Internet (online submissions)
- Customer Care Calls

---

## 💡 Key Findings

| Insight | Details |
|---------|---------|
| 📈 **Peak complaint month** | Complaints rose sharply mid-2015 |
| 🗺️ **Highest complaint volume** | Georgia led in total complaint count |
| 🔴 **Highest unresolved rate** | Certain states show >50% open complaints |
| 🧠 **Top complaint themes** | Internet speed · Billing disputes · Service outages · Data caps · Payment failures |
| 📡 **Resolution gap** | Customer Care Call complaints show a higher resolution rate vs Internet-filed ones |

---

## 🛠️ Tech Stack

| Library | Purpose |
|---------|---------|
| `pandas` | Data loading, manipulation, groupby, time-series |
| `numpy` | Numerical operations |
| `matplotlib` | Visualization (trend charts, stacked bar charts) |
| `nltk` | Text preprocessing — stopwords, lemmatization |
| `gensim` | LDA topic modeling, dictionary, corpus |
| `wordcloud` | (Optional) Word cloud visualization |

---

## 🚀 Getting Started

### Prerequisites

```bash
pip install pandas numpy matplotlib nltk gensim wordcloud
```

### NLTK Downloads (first run only)

```python
import nltk
nltk.download('stopwords')
nltk.download('wordnet')
```

### Run the Notebook

```bash
# Clone/navigate to the project directory
cd comcast_Telecom_cunsumer_complaint

# Launch Jupyter
jupyter notebook comcast.ipynb
```

> **Note:** Ensure `Comcast_telecom_complaints_data.csv` is in the same directory as the notebook.

---

## 📊 Sample Visualizations

The notebook generates the following charts:

- **Daily Complaint Trend** — line chart of day-wise complaint volume
- **Monthly Complaint Trend** — month-over-month complaint count with markers
- **State-wise Stacked Bar Chart** — horizontal bar chart showing Open vs Closed complaints per US state
- **LDA Topic Keywords Table** — DataFrame showing top 20 words per discovered topic

---

## 🏗️ Future Improvements

- [ ] Add interactive visualizations with **Plotly** or **Bokeh**
- [ ] Apply **sentiment analysis** to classify complaints by urgency/severity
- [ ] Build a **complaint classifier** using supervised ML (Logistic Regression, SVM)
- [ ] Create a **Streamlit dashboard** for real-time complaint exploration
- [ ] Add **pyLDAvis** for interactive topic model visualization
- [ ] Perform **zip-code level** geospatial mapping with folium

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 🙋 Author

**Kailash**  
Data Analyst | Python · ML · NLP Enthusiast  

---

*This project was completed as part of a data analytics case study on consumer sentiment and complaint resolution efficiency in the US telecom sector.*
