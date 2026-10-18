# Contributing to Customer Behavior Analytics

Thank you for your interest in contributing to **Customer Behavior Analytics (K-Means Customer Segmentation & RFM Analytics Dashboard)** — an open-source unsupervised machine learning and business intelligence platform.

This project is maintained by **Luthfi Muthathohirin**.

---

## 🛠️ Architecture & Development Setup

The repository is structured as a standalone Python / Streamlit machine learning application:

```text
customer-behavior-analytics/
├── main.py                        # Streamlit Interactive Dashboard & ML Pipeline
├── requirements.txt               # Python package dependencies
├── LICENSE                        # MIT License
├── docs/                          # D2 architecture specification (architecture.d2)
├── assets/                        # Compiled vector SVG architecture and formula diagrams
└── .streamlit/config.toml         # Streamlit UI theme configuration
```

### 1. Prerequisites

- **Python**: Version 3.10, 3.11, or 3.12 (Python 3.11+ recommended)
- **Pip / Virtual Environment**: Standard Python toolchain

### 2. Local Setup & Virtual Environment

```bash
# Clone the repository
git clone https://github.com/HyLuthfi/customer-behavior-analytics.git
cd customer-behavior-analytics

# Create virtual environment
python -m venv .venv

# Activate virtual environment
source .venv/bin/activate       # Linux/macOS
.venv\Scripts\activate          # Windows

# Upgrade pip and install package dependencies
pip install --upgrade pip
pip install -r requirements.txt
```

### 3. Running Local Application

Launch the Streamlit dashboard locally:

```bash
streamlit run main.py
```

The application will be accessible at `http://localhost:8501`. Test dataset upload functionality, inspect the 3D Plotly cluster visualization, and verify segment metric breakdowns.

---

## 🌿 Contribution Workflow

1. **Fork** the repository on GitHub.
2. **Clone** your fork locally and configure upstream tracking:
   ```bash
   git clone https://github.com/<your-username>/customer-behavior-analytics.git
   cd customer-behavior-analytics
   git remote add upstream https://github.com/HyLuthfi/customer-behavior-analytics.git
   ```
3. **Create a feature branch** from `main`:
   ```bash
   git checkout -b feat/your-feature-name
   ```
4. Implement your enhancements adhering to unsupervised ML validation standards and code hygiene.
5. Verify local numerical outputs and UI rendering via `streamlit run main.py`.
6. Commit your changes following the Conventional Commits specification.
7. Open a **Pull Request** against `main` of the upstream repository.

---

## 📐 Commit Convention

This repository strictly enforces [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/):

| Prefix | Scope / Usage |
|---|---|
| `feat(scope):` | New feature, clustering algorithm, or analytics view |
| `fix(scope):` | Bug fix in data preprocessing, RFM computation, or UI rendering |
| `docs(scope):` | Documentation updates, mathematical formulations, README edits |
| `chore(scope):` | Tooling, dependencies, repository hygiene |
| `refactor(scope):` | Code refactoring without behavioral mutation |
| `perf(scope):` | Performance optimization (vectorization via NumPy/Pandas, caching) |
| `test(scope):` | Adding numerical verification test cases |
| `security(scope):` | Security hardening, input sanitization, dependency patches |

**Valid Examples:**
```text
feat(clustering): implement DBSCAN density-based clustering algorithm
fix(rfm): resolve timezone offset discrepancy during Recency delta calculation
perf(pipeline): optimize Pandas aggregation using categorical InvoiceNo grouping
docs(readme): add mathematical formulation for K-Means inertia minimization
```

---

## 🔬 Guidelines for Contributing New Clustering Algorithms

We welcome contributions of alternative unsupervised machine learning and clustering algorithms (e.g. **DBSCAN**, **Hierarchical Agglomerative Clustering**, **Gaussian Mixture Models (GMM)**, **OPTICS**, **Spectral Clustering**):

### 1. Mathematical & Algorithmic Standards

- **Input Dimension Uniformity**: New clustering algorithms must ingest the normalized 3D RFM feature vector $[R_{\text{scaled}}, F_{\text{scaled}}, M_{\text{scaled}}] \in [0, 1]^3$.
- **Cluster Index Determinism**: Implement centroid sorting or density-ordered cluster labeling so that cluster assignments (e.g. Cluster 0, 1, 2) remain consistent across multiple runs on similar datasets.
- **Evaluation Metrics**: Pull Requests introducing new algorithms should report:
  - Silhouette Score
  - Davies-Bouldin Index
  - Computational scalability for datasets exceeding 50,000 transactions

### 2. Implementation Architecture in `main.py`

When adding a new clustering technique (e.g. `ALGORITHM_NAME`):
1. **Pipeline Function**: Implement a clean function accepting `(df_rfm, **hyperparameters)` returning cluster labels and evaluation scores.
2. **Caching Strategy**: Decorate expensive computation functions with `@st.cache_data` to ensure fluid UI interaction.
3. **3D Visualization Integration**: Connect output cluster labels to the Plotly 3D scatter plot palette for visual inspection.

---

## 🔒 Customer Privacy & In-Memory Zero-Residue Ethics

When working with commercial transaction data and customer analytics:

1. **Strict In-Memory Processing**: Never write or persist uploaded retail transaction files (`.csv`, `.xlsx`) to the server filesystem or external databases. Data must reside solely in transient RAM buffers (`io.BytesIO`).
2. **Zero Personally Identifiable Information (PII)**: The application processes pseudonymized customer keys (`CustomerID`) and transaction metrics. Never log, persist, or transmit customer names, email addresses, phone numbers, or payment card details.
3. **Sanitization Best Practices**: Always filter out corrupted records, negative unit prices, and return transactions (`Quantity < 0`) before clustering to prevent distortion of Euclidean distances.

---

## 🔒 Security Vulnerability Reporting

If you identify a security issue, vulnerability, or secret leakage, **please do not open a public GitHub issue**. Contact the maintainer directly via email: `luthfirg2502@gmail.com`.

---

## 📄 License

By contributing, you agree that your contributions will be licensed under the [MIT License](LICENSE).
