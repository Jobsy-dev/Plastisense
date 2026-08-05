# PlastiSense

**AI-based Plastic Waste Detection System in Water Bodies**

## Overview

Plastic pollution in water bodies is a major environmental problem, and traditional water quality monitoring methods are slow, expensive, and require direct human involvement. PlastiSense addresses this by using machine learning to detect plastic contamination in real time from water quality readings, with automated alerts sent to relevant authorities when contamination is detected.

## Dataset

- Sourced from Kaggle (Water Quality Prediction dataset), containing ~1 million data points
- Cleaned using standard preprocessing: missing value handling, outlier removal via **IQR** and **Isolation Forest**, and feature scaling with **StandardScaler**

## Key Features Used

Identified through research as the most predictive indicators of plastic contamination:
- **pH** — water alkalinity/acidity
- **Turbidity** — water transparency (high turbidity indicates contamination)
- **TDS (Total Dissolved Solids)** — includes dissolved matter like microplastics
- **Conductivity** — presence of contaminants via electrical conductivity

## Model

- Compared **Random Forest** and **XGBoost** classifiers
- **XGBoost** selected as the final model — achieved **86.09% accuracy**
- 80/20 train-test split with hyperparameter tuning

Prediction confidence is scaled for interpretability:
- If predicted "no plastic" (0): confidence = raw probability × 65 (0–65% range)
- If predicted "plastic detected" (1): confidence = 65 + (raw probability × 35) (65–100% range)

## Tech Stack

- **Backend:** Flask (Python)
- **Frontend:** HTML, CSS, Bootstrap, JavaScript
- **ML:** XGBoost, Scikit-Learn
- **Alerts:** Gmail SMTP API for real-time email notifications to authorities upon contamination detection

## How It Works

1. User inputs water quality readings (pH, Turbidity, TDS, Conductivity)
2. The trained XGBoost model predicts contamination status with a confidence score
3. If plastic waste is detected, an automated email alert is sent to the relevant authority

## Setup & Running Locally

1. **Clone the repository**
   ```bash
   git clone https://github.com/Jobsy-dev/Plastisense.git
   cd Plastisense
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up environment variables**
   Create a `.env` file in the project root with your own email credentials for alerts:
   ```
   SENDER_EMAIL=your-email@gmail.com
   SENDER_PASSWORD=your-app-password
   RECEIVER_EMAIL=recipient-email@gmail.com
   ```
   

4. **Run the app**
   ```bash
   python app.py
   ```

5. Open your browser at `http://localhost:5000` (or the port shown in the terminal)

## Project Structure

```
Plastisense/
├── app.py                  # Flask backend + prediction logic
├── xgb_best_model.pkl      # Trained XGBoost model
├── scaler.pkl              # Fitted StandardScaler
├── templates/               # HTML templates
├── static/                  # CSS, JS, images
└── requirements.txt
```

## References

- [XGBoost Documentation](https://xgboost.readthedocs.io/en/latest/)
- [Scikit-learn Documentation](https://scikit-learn.org/stable/)
- [Flask Documentation](https://flask.palletsprojects.com/en/stable/)
- [Dataset Source (Kaggle)](https://www.kaggle.com/datasets/vanthanadevi08/water-quality-prediction)
