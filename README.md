# Integrated-Pipeline-for-Breast-Cancer-Mutation-Analysis-Using-ClinVar-and-Ensembl-VEP
Integrated Pipeline for Breast Cancer Mutation Analysis Using ClinVar and Ensembl VEP
# 🧬 ClinVar Filtering and Functional Annotation Pipeline (BRCA1/2)

This repository contains a **Jupyter Notebook** pipeline designed for the large-scale analysis of clinical mutation data. The workflow targets filtering the full **ClinVar** database to identify rare, breast cancer-associated mutations in **BRCA1/BRCA2** and attempting functional annotation using the **Ensembl VEP REST API**.

The script demonstrates crucial techniques for handling massive bioinformatics datasets, including **chunk-wise data loading** to manage memory efficiently.

## ⚠️ Important Note

The VEP annotation step in the notebook may fail to find the specific variants from the ClinVar file's ID format. Consequently, the pathogenicity scores (PolyPhen and SIFT) are **simulated** in the latter half of the script for demonstration purposes. The final `pathogenic_mutations.csv` file should be interpreted with this context.

## 🚀 Key Features

* **Massive Data Handling:** Downloads the complete, multi-gigabyte **`variant_summary.txt.gz`** file from ClinVar (NCBI).
* **Chunk-wise Processing:** Loads the large compressed file in small **chunks** using `pandas` to ensure memory efficiency.
* **Targeted Filtering:** Filters the data for mutations meeting three strict criteria:
    1.  **Gene:** `BRCA1` or `BRCA2`.
    2.  **Phenotype:** Associated with "Breast" cancer.
    3.  **Rarity:** Minor Allele Frequency (**MAF $\leq 0.01$**).
* **VEP Integration (Demonstrative):** Constructs VCF-like identifiers and attempts to query the **Ensembl VEP `/id` REST API** to retrieve functional consequences.
* **Pathogenicity Filtering:** Identifies "pathogenic" variants based on predefined thresholds for the simulated PolyPhen and SIFT scores.

---

## 🔬 Workflow Steps

| Step | Action | Output |
| :--- | :--- | :--- |
| **1-3** | Download, Chunk Load, and Filter ClinVar | `filtered_mutations.csv` (BRCA1/2, Breast Phenotype, MAF $\leq 0.01$) |
| **4** | Attempt VEP Annotation | Console Output / `annotated_variant` (JSON format) |
| **6-7** | **Simulate and Filter Pathogenicity** | `pathogenic_mutations.csv` (Filtered by simulated PolyPhen/SIFT scores) |
| **8** | Download Results (Colab only) | Download links for CSV outputs. |

---

## 🛠️ Prerequisites and Execution

### Requirements

To run this notebook, you need a Python environment with the following libraries:

* `pandas`
* `numpy`
* `requests`
* `gzip`
* `json`
* `os`

### How to Run

1.  Open the **`Integrated Pipeline for Breast Cancer Mutation Analysis Using ClinVar and Ensembl VEP.ipynb`** file in Google Colab or a Jupyter environment.
2.  Execute all cells sequentially. The first three cells handle data acquisition and filtering; subsequent cells manage the annotation attempt and final filtering.

---

## 📁 Output Files

The pipeline generates the following key data files in the execution directory:

| Filename | Type | Content |
| :--- | :--- | :--- |
| `filtered_mutations.csv` | CSV | The large dataset of BRCA1/2 mutations filtered by rarity and phenotype. |
| `pathogenic_mutations.csv` | CSV | The final list of mutations filtered by **simulated** PolyPhen/SIFT scores. |
| `vep_annotation.json` | JSON | (Only created if a successful VEP annotation occurs in Step 4). |
