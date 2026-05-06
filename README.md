# Industrial EDA Dashboard — AI4I 2020 Predictive Maintenance

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Portfolio-orange)

End-to-end exploratory data analysis on the [AI4I 2020 Predictive Maintenance Dataset](https://www.kaggle.com/datasets/stephanmatzka/predictive-maintenance-dataset-ai4i-2020) (10,000 synthetic machine-sensor records, UCI ML Repository). This project answers three industrial business questions — how often do machines fail, where do failures cluster in the operating envelope, and what is the financial cost — and delivers findings as a standalone interactive HTML dashboard. It is the first step in a three-project portfolio targeting data analyst roles in Thai manufacturing and industrial IoT sectors.

---

## Key Findings

1. **Failure rate is 3.39%** (339 / 10,000 records). In a 24/7 factory that translates to roughly **8 unplanned stoppages per day** — each carrying downtime, labor, and lost-output costs.
2. **Heat Dissipation Failure (HDF) is the #1 mode** — 115 cases (34% of all failures). Cooling and ventilation are the first maintenance priority; the other four modes combined account for only 66%.
3. **A two-variable alert rule catches the danger zone** — machines at Torque > 60 Nm AND RPM < 1,400 show a **40.1% failure rate** (12× the overall baseline). This threshold is deployable as a real-time alert with no machine learning required.
4. **Low-grade machines fail nearly twice as often** — Grade L: 3.92% vs Grade H: 2.09%. Procurement and preventive-maintenance schedules should be differentiated by grade.
5. **Severe class imbalance (96.6% healthy / 3.4% failed)** — any predictive model trained on this data must use SMOTE or `class_weight` correction, or it will learn to predict "healthy" 100% of the time and achieve 96.6% accuracy while detecting zero failures.

---

## Dashboard Preview

> 📊 Open `dashboard/index_en.html` in any browser — no server needed. Alternatively, you may copy the code into an online editor such as JSFiddle (https://jsfiddle.net/) for immediate browser-based access and testing.

The dashboard visualises all five findings interactively (Chart.js): failure-mode breakdown, machine-grade comparison, operating-window scatter, sensor distributions by failure type, and the ฿3M/month ROI calculation.

---

## Folder Structure

```
industrial-eda-dashboard/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── notebooks/
│   └── 01_eda.ipynb                  ← Main analysis — start here
│
├── data/
│   ├── raw/                          ← Empty (raw CSV gitignored — see Dataset section)
│   │   └── .gitkeep
│   └── processed/
│       └── ai4i_clean.csv            ← Cleaned, analysis-ready dataset
│
├── reports/
│   ├── AI4I_EDA_Report.pdf           ← Full written report (EN)
│   └── AI4I_EDA_Report_TH.html       ← Thai-language version
│
├── dashboard/
│   └── index_en.html                 ← Interactive HTML dashboard
│
└── figures/
    ├── fig1_histograms.png
    ├── fig2_zscore.png
    ├── fig3_type_dist.png
    ├── fig4_failure_rate.png
    ├── fig5_failure_modes.png
    ├── fig6_bivariate.png
    ├── fig7_heatmap.png
    ├── fig8_op_window.png
    └── fig9_temp_gap.png
```

---

## Quick Start

```bash
# 1. Clone the repository
git clone https://github.com/win-nk/industrial-eda-dashboard.git
cd industrial-eda-dashboard

# 2. Install dependencies
pip install -r requirements.txt

# 3. Open the EDA notebook
jupyter notebook notebooks/01_eda.ipynb

# 4. Open the interactive dashboard
#    Simply open dashboard/index_en.html in any browser — no server required
```

> **Raw data not included.** Download `ai4i2020.csv` from [Kaggle](https://www.kaggle.com/datasets/stephanmatzka/predictive-maintenance-dataset-ai4i-2020) and place it at `data/raw/ai4i2020.csv` before running the notebook.

---

## Dataset

| Field | Detail |
|---|---|
| Name | AI4I 2020 Predictive Maintenance Dataset |
| Author | Stephan Matzka — HTW Berlin |
| Source | [Kaggle](https://www.kaggle.com/datasets/stephanmatzka/predictive-maintenance-dataset-ai4i-2020) · [UCI ML Repository](https://archive.ics.uci.edu/dataset/601/ai4i+2020+predictive+maintenance+dataset) |
| Records | 10,000 rows · 14 features · 5 failure-mode labels |
| Note | Synthetic dataset designed to reflect real predictive maintenance scenarios in manufacturing environments |

---

## Business Impact

A factory running 24/7 with estimated downtime cost of **฿20,000/hour** (labor + lost throughput + expedited parts):

| Scenario | Monthly Cost |
|---|---|
| No model — all failures undetected | ฿6,780,000 |
| Model with 50% recall on failures | ฿3,390,000 |
| **Estimated monthly savings** | **฿3,390,000 (~฿3M)** |

**Formula:**
```
Savings = Failure rate × Monthly machine-hours × Downtime cost/hr × Model recall
        = 3.39% × 10,000 hr × ฿20,000 × 50%
        = ฿3,390,000 / month
```

This estimate is conservative — it excludes secondary costs such as equipment damage, safety incidents, and customer SLA penalties.

---

## Roadmap

| # | Project | Status |
|---|---|---|
| 1 | EDA — AI4I 2020 Predictive Maintenance *(this repo)* | ✅ Complete |
| 2 | ML Model — Binary Failure Classifier (SMOTE + XGBoost) | 🔄 In Progress |
| 3 | Deployment — Real-time Alert Dashboard | ⬜ Planned |

---

## Author

**Nawin Khamtha**  
B.Eng. Automation Robotics & Intelligent System · Khon Kaen University  
[LinkedIn](www.linkedin.com/in/nawin-khamtha-754562377) · [GitHub](https://github.com/win-nk)

