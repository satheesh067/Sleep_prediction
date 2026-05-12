# Sleep Prediction: EEG Sleep Staging and Lifestyle Sleep Quality Analysis

This repository contains a two-part machine learning project:

1. EEG sleep stage classification using Sleep-EDF physiological signals.
2. Lifestyle-based sleep quality prediction using survey data.

The project includes end-to-end notebooks, trained models, evaluation plots, CSV outputs, and a full report.

## Overview

### Pipeline A: EEG Sleep Staging
- Data source: PhysioNet Sleep-EDF PSG + hypnogram files.
- Preprocessing: 30-second epoching and feature extraction.
- Models: Random Forest, SVM, XGBoost, 1D CNN, BiLSTM, CNN+LSTM.
- Split strategy: subject-level train/validation/test split to prevent leakage.

### Pipeline B: Lifestyle Sleep Quality
- Data source: Sleep health and lifestyle survey dataset.
- Task: predict sleep quality score with regression.
- Models: Random Forest Regressor and XGBoost Regressor.

## Key Results

### EEG Sleep Staging (Classification)
Best model: CNN+LSTM
- Accuracy: 70.17%
- F1 (Macro): 0.6766
- F1 (Weighted): 0.7014
- Cohen's Kappa: 0.6191

### Lifestyle Sleep Quality (Regression)
Best model: XGBoost
- R2: 0.9956
- MAE: 0.0183
- RMSE: 0.0817

## Repository Structure

```text
sleep_prediction/
|-- 1.ipynb
|-- lifestyle.ipynb
|-- eeg_epochs_features.csv
|-- eeg_sleep_quality.csv
|-- model_comparison_results.csv
|-- lifestyle_model_results.csv
|-- best_cnn_lstm_model.pt
|-- best_model.h5
|-- report/
|   |-- index.html
|   |-- README.md
|   `-- sections/
|-- *.png (evaluation and dashboard figures)
`-- README.md
```

## Environment

Validated with:
- Python 3.12
- PyTorch 2.5.1+cu121
- MNE 1.11.0
- scikit-learn 1.7.2
- XGBoost 3.0.5
- SciPy 1.15.3
- pandas 2.3.2
- matplotlib 3.9.0
- seaborn 0.13.2
- NumPy 2.4.2

## Setup

### 1. Clone the repository
```bash
git clone <your-repo-url>
cd sleep_prediction
```

### 2. Create and activate a virtual environment

Windows PowerShell:
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Linux or macOS:
```bash
python -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies
```bash
pip install torch mne scikit-learn xgboost scipy pandas matplotlib seaborn numpy jupyter
```

## How to Run

1. Open Jupyter and run the EEG pipeline notebook:
   - `1.ipynb`
2. Run the lifestyle pipeline notebook:
   - `lifestyle.ipynb`
3. Review generated outputs:
   - `model_comparison_results.csv`
   - `lifestyle_model_results.csv`
   - generated `.png` figures
4. Open the report:
   - `report/index.html`

## Leakage Prevention (Important)

The EEG pipeline uses subject-level splitting so that epochs from the same subject do not appear across train/validation/test simultaneously. This prevents identity leakage and provides realistic cross-subject performance estimates.

## Outputs Produced

- Trained models:
  - `best_cnn_lstm_model.pt`
  - `best_model.h5`
- Tables:
  - `model_comparison_results.csv`
  - `lifestyle_model_results.csv`
- Figures:
  - confusion matrices
  - per-class F1
  - training curves
  - feature importance
  - hypnogram comparisons
  - EEG vs survey visual summaries

## Report

The full write-up is available in:
- `report/index.html`

To export as PDF, open `report/index.html` in Chrome and print to PDF with background graphics enabled.

## Notes

- Large model and data files are included in this repository. For long-term hosting on GitHub, consider Git LFS for large artifacts.
- Exact scores can vary slightly across environments due to random seeds and hardware differences.

## References

- Gramfort, A., Luessi, M., Larson, E., Engemann, D. A., Strohmeier, D., Brodbeck, C., ... & Hämäläinen, M. S. (2013). MEG and EEG data analysis with MNE-Python. *Frontiers in neuroscience*, 7, 267. https://doi.org/10.3389/fnins.2013.00267

## License


### MNE-Python

- Authors: Alexandre Gramfort <alexandre.gramfort@inria.fr>, Stanislas Chambon <stan.chambon@gmail.com>, Joan Massich <mailsik@gmail.com>
- License: BSD-3-Clause
- Copyright: MNE-Python contributors
