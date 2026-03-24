# Case-Based Temporal Disambiguator (CBTD) 🕒

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Conference](https://img.shields.io/badge/ICCBR-2026-red.svg)](https://iccbr2026.org/)

This repository contains the official implementation of the **Case-Based Temporal Disambiguator (CBTD)**, as presented in our paper: *"Neuro-Symbolic Temporal Reasoning: A Hybrid Case-Based Approach for Robust Expiration Date Recognition"*.

## 📖 Overview

Automated expiration date recognition for assistive technology faces two major hurdles: **unconstrained orientation** and **semantic ambiguity** (e.g., is `05.06` May 6th or June 5th?). 

Our system solves this using a **Hybrid Neuro-Symbolic** approach:
1.  **Perception Layer:** A lightweight RepViT-driven DBNet (Detection) and RepSVTR (Recognition) pipeline optimized for high-speed, full-angle text extraction.
2.  **Reasoning Layer (CBTD):** A logic engine governed by the **4R Case-Based Reasoning (CBR) cycle** that utilizes a format-voting memory bank to resolve structural ambiguities.

---

## 🧠 The CBR Logic (4R Cycle)

The CBTD module resolves ambiguous dates through four distinct stages:
* **Retrieve:** Generates all mathematically valid date candidates from the raw OCR string.
* **Reuse:** Each candidate is assigned a score based on the historical success frequency of its format (e.g., `YEAR_FIRST`) stored in the Case Base.
* **Revise:** In the event of a tie, the system selects the candidate with the minimum temporal distance to the current system year.
* **Retain:** The winning format is saved to memory. A global exponential decay ($\lambda = 0.995$) is applied to allow the system to adapt to new regional packaging trends.

---

## 🚀 Performance

Evaluated on the **Date-Real** dataset (Seker et al., 2022), our hybrid approach significantly outperforms static heuristic-based parsers.

| Model | Overall Accuracy | Ambiguity Accuracy |
| :--- | :---: | :---: |
| Static Heuristic Baseline | 90.20% | 83.08% |
| **Proposed CBTD (Ours)** | **99.61%** | **100.00%** |

---

## 🛠️ Installation & Usage

### 1. Requirements
* Python 3.8+
* PyTorch / TorchVision
* `python-dateutil`

```bash
git clone [https://github.com/AnanasPizzaMigliore/OpenOCR.git](https://github.com/AnanasPizzaMigliore/OpenOCR.git)
cd OpenOCR
pip install -r requirements.txt
