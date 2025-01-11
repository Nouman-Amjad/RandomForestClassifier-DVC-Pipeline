# RandomForestClassifier-DVC-Pipeline

## Overview
This project demonstrates a **DVC pipeline** to train and evaluate a **Random Forest Classifier**. The pipeline integrates various stages like data preparation, feature extraction, model training, and evaluation. It is built to showcase a scalable and reproducible machine learning workflow using **DVC (Data Version Control)**.

---

## Features
1. **Automated Pipeline**:
   - Data preparation
   - Feature engineering
   - Model training
   - Model evaluation
2. **Pipeline Configuration**:
   - Controlled using `dvc.yaml` and `params.yaml` for ease of parameter tuning.
3. **Reproducibility**:
   - Ensures consistent results with version-controlled data and models.
4. **Visualization**:
   - Evaluation plots like feature importance and ROC curves.

---

## Pipeline Stages
### **1. Data Preparation**
- **Script**: `src/prepare.py`
- **Input**: `data/data.xml`
- **Output**: `data/prepared/`
- **Parameters**:
  - `split`: Train-test split ratio (default: 0.40).
  - `seed`: Random seed for reproducibility (default: 20170428).

### **2. Feature Engineering**
- **Script**: `src/featurization.py`
- **Input**: `data/prepared/`
- **Output**: `data/features/`
- **Parameters**:
  - `max_features`: Maximum number of features to extract (default: 150).
  - `ngrams`: N-grams for text feature extraction (default: 1).

### **3. Model Training**
- **Script**: `src/train.py`
- **Input**: `data/features/`
- **Output**: `model.pkl`
- **Parameters**:
  - `n_est`: Number of estimators in the Random Forest (default: 50).
  - `min_split`: Minimum split for decision trees (default: 0.1).
  - `seed`: Random seed for reproducibility (default: 20170428).

### **4. Model Evaluation**
- **Script**: `src/evaluate.py`
- **Input**: `model.pkl`, `data/features/`
- **Output**: Evaluation metrics and plots.

---

## Parameters
### Configured in `params.yaml`:
```yaml
prepare:
  split: 0.40
  seed: 20170428

featurize:
  max_features: 150
  ngrams: 1

train:
  seed: 20170428
  n_est: 50
  min_split: 0.1
```
## Installation and Usage
### Prerequisites
- Python 3.8 or later
- DVC installed
- A virtual environment

### Steps
1. Clone the Repository:
```bash
git clone https://github.com/your-username/RandomForestClassifier-DVC-Pipeline.git
cd RandomForestClassifier-DVC-Pipeline
```
2. Install Dependencies:
```bash
pip install -r requirements.txt
```
3. Reproduce the Pipeline:
```bash
dvc repro
```
4. Run Specific Stages:
- Run only the **train** stage:
```bash
dvc repro train
```
5. Visualize Metrics and Plots:
```bash
dvc metrics show
dvc plots show eval/plots/images
```
## File Structure

- `dvc.yaml`: Defines pipeline stages and dependencies.
- `params.yaml`: Contains all hyperparameters and configurations.
- `src/`: Scripts for each pipeline stage.
  - `prepare.py`: Prepares and splits the data.
  - `featurization.py`: Extracts features from the data.
  - `train.py`: Trains the Random Forest Classifier.
  - `evaluate.py`: Evaluates the trained model.
- `assets/`: Contains evaluation plots and visualizations.

---

## Future Enhancements

- Add hyperparameter optimization for the Random Forest model.
- Extend the pipeline to include additional models.
- Incorporate data drift detection for real-world scenarios.

---

## Acknowledgments

This project was developed to showcase the power of **DVC** in managing and automating machine learning workflows. Special thanks to the open-source community for providing tools and resources.

---

## License

This project is licensed under the [MIT License](LICENSE).
