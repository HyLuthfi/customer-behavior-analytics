# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-10-19

Initial stable release of **Customer Behavior Analytics (K-Means Customer Segmentation & RFM Analytics Dashboard)** — an enterprise-grade unsupervised machine learning platform integrating Recency, Frequency, and Monetary (RFM) feature engineering, K-Means clustering, and interactive 3D spatial decomposition in Streamlit.

### Added

- **Unsupervised Machine Learning Clustering Core**:
  - Implementation of **K-Means Clustering** ($k=3$) with `k-means++` initialization and multi-seed convergence (`n_init=10`, `random_state=42`).
  - Iterative minimization of Within-Cluster Sum of Squares (WCSS / Inertia):
    $$J = \sum_{j=1}^k \sum_{i \in S_j} \lVert x_i - \mu_j \rVert^2$$
  - Automated cluster re-indexing ordered by mean monetary value to ensure deterministic, interpretable labeling across arbitrary datasets.
- **RFM Feature Engineering Engine**:
  - Automated transformation of raw retail transaction logs into quantitative behavioral metrics per `CustomerID`:
    - **Recency ($R$)**: Days elapsed since customer's last purchase ($T_{\text{snapshot}} - \max(T_{\text{transaction}})$).
    - **Frequency ($F$)**: Count of distinct transactions (`count_distinct(InvoiceNo)`).
    - **Monetary ($M$)**: Cumulative gross spending ($\sum \text{Quantity} \times \text{UnitPrice}$).
  - Performance optimization leveraging Streamlit's `@st.cache_data` for sub-second reactive re-computation.
- **Feature Scaling & Space Harmonization**:
  - Ingestion of feature vectors into `MinMaxScaler` mapping $R, F, M \in [0.0, 1.0]$.
  - Balanced Euclidean distance geometry preventing high-magnitude monetary values from dominating the clustering space.
- **3D Spatial Visualization & Interactive Analytics**:
  - Interactive **Plotly 3D Scatter Plot** rendering customer vectors in 3D coordinate space $(R, F, M)$ with full 360-degree orbit, pan, and zoom.
  - Hover tooltips displaying exact Customer ID, raw RFM metrics, normalized coordinates, and assigned cluster label.
- **Executive Business Intelligence Dashboard**:
  - 4-tab modular workflow: Data Schema Guide, Executive Overview Dashboard, 3D Cluster Explorer, and Raw RFM Dataset Table with CSV export.
  - Granular segment profiling across 3 behavioral tiers:
    - **High-Value (Champions / Platinum)**: High frequency, top monetary spend, low recency.
    - **Medium-Value (Regulars / Core Base)**: Moderate frequency and spend, steady activity.
    - **Low-Value (At-Risk / Hibernating)**: High recency, infrequent transactions, low cumulative spend.
- **Zero-Residue In-Memory Data Pipeline**:
  - Ephemeral processing via `st.file_uploader` consuming CSV and Excel (`.xlsx`, `.xls`) files purely in memory buffers without persisting customer transactions to disk.
- **Showcase DX & Visual Documentation**:
  - D2 vector architecture diagram (`assets/architecture.svg`) compiled in Terminal Dark palette with ELK layout engine documenting all 5 pipeline layers.
  - Standalone 3-panel mathematical formula vector SVG (`assets/rfm_kmeans_formulas.svg`) featuring true horizontal fraction bars and scientific typography.
  - Standard 9-element portfolio `README.md` with dynamic typing header, verified segment matrix, and zero promotional buzzwords.
  - Live deployment integration on Streamlit Community Cloud (`customer-behavior-analytics-hyfhi.streamlit.app`).

### Changed

- **Data Ingestion Robustness**: Automated pre-clustering sanitization filtering out canceled invoices, missing `CustomerID` records, and non-positive `Quantity`/`UnitPrice` anomalies.
- **Cluster Sorting Stability**: Dynamically mapped cluster labels based on ascending monetary centroid rankings to preserve semantic consistency across new dataset uploads.

### Security

- **[P0] SPDX MIT License**: Issued official `LICENSE` file under MIT License with legal copyright attributed to `Luthfi Muthathohirin`.
- **[P0] Zero Leak Certification**: Passed comprehensive 5-commit repository history scan with Gitleaks v8.30.1 (**0 leaks detected**, Health Score 98/100).
- **[P0] Hardened `.gitignore`**: Implemented comprehensive 102-rule exclusion filter protecting Python bytecode (`__pycache__/`), virtual environments (`.venv/`), Streamlit secrets (`secrets.toml`), retail transaction dumps (`*.csv`, `*.xlsx`), and model checkpoint artifacts.
- **Customer Privacy Protection**: Verified zero persistence of retail transaction records on host disk, guaranteeing compliance with enterprise data retention best practices.
