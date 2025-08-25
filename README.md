# Capstone Data Repository

This repository contains the submission package for the Capstone project.  
It includes data, the data dictionary, and outputs for Research Questions (RQ1–RQ4).

---

## 📂 Contents
- `data/` – Raw and processed datasets (large Excel files tracked with Git LFS)
- `data_dictionary/` – FDIC SOD Data Dictionary
- `RQ1_outputs/` to `RQ4_outputs/` – Outputs and results for each research question

---

## ⚡ How to Access Large Files
Some Excel files are larger than 100 MB. They are stored with **Git LFS**.

### Clone with LFS
```bash
git lfs install
git clone https://github.com/ranjorite/capstone-data.git
cd capstone-data
git lfs pull
