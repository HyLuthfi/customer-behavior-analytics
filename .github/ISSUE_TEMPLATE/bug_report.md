---
name: Bug Report
about: Report a data processing anomaly, calculation error, or UI issue in Customer Behavior Analytics
title: "[BUG] "
labels: bug
assignees: ''
---

## Description

A clear and concise description of what the data processing, clustering, or application bug is.

## Steps to Reproduce

1. Open application locally or via Streamlit Cloud
2. Upload transaction file '...' (CSV or Excel)
3. Select tab '...' (Panduan Dataset / Dashboard Bisnis / 3D Cluster Explorer / Data RFM)
4. Trigger data processing or clustering analysis
5. Observe error, anomalous cluster distribution, or visualization failure at '...'

## Expected Behavior

A clear and concise description of what you expected to happen (e.g. valid RFM aggregation completed under 1s, K-Means converges to 3 clusters, Plotly 3D scatter plot renders with responsive 360-degree orbit).

## Actual Behavior / Error Traceback

What actually happened (e.g. `ValueError: Input contains NaN`, date parsing failure on `InvoiceDate`, division by zero during `MinMaxScaler`, Plotly WebGL context lost error).

```text
Paste terminal error output or browser console traceback here
```

## Dataset & Transaction Schema Details

| Parameter | Value |
|---|---|
| **File Format** | CSV / XLSX / XLS |
| **Row Count** | e.g. 5,000 transactions / 1,200 unique customers |
| **Date Format in Data** | e.g. `YYYY-MM-DD HH:MM:SS` / `DD/MM/YYYY` |
| **Monetary Currency** | e.g. USD / EUR / IDR |
| **Missing Customer IDs Present?** | Yes / No |

## System & Execution Environment

| Parameter | Value |
|---|---|
| **Execution Environment** | Streamlit Community Cloud / Local Python venv |
| **Operating System** | Windows 11 / Ubuntu 22.04 / macOS |
| **Python Version** | e.g. Python 3.10.12 / 3.11.8 / 3.12.2 |
| **Streamlit Version** | e.g. 1.32.0 |
| **Scikit-Learn Version** | e.g. 1.4.1 |
| **Plotly Version** | e.g. 5.19.0 |
| **Browser & Version** | e.g. Chrome 129 / Edge / Firefox |

## Additional Context

Add any other context about the problem here (e.g. sample anonymized transaction rows, screenshots of anomalous cluster distributions).
