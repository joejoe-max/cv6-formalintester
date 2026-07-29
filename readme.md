# Fresh vs Formalin-mixed Orange Classifier

Binary image classification: MobileNetV2 transfer learning distinguishing Fresh Orange from
Formalin-mixed Orange, deployed as a Streamlit web app.

## Project files

| File | Purpose |
|---|---|
| `orange_train.ipynb` | Training notebook (Kaggle) — downloads FruitVision, curates the two orange classes, trains, evaluates, saves `model.keras` |
| `orange_train_colab.ipynb` | Same pipeline, adapted for Google Colab |
| `app.py` | Streamlit app — loads `model.keras` and serves predictions |
| `model.keras` | Trained model file (produced by the training notebook — copy it in here) |
| `requirements.txt` | Python package dependencies |
| `report.txt` | Project report |

## Training

Run either notebook top to bottom (Kaggle or Colab version). Both:
1. Download the FruitVision dataset directly (`wget`, no local upload needed)
2. Curate just the Fresh Orange and Formalin-mixed Orange classes out of FruitVision's 15 total classes
3. Split 70/15/15 into train/val/test
4. Train MobileNetV2 (frozen feature extraction, then fine-tuned on the top 30 layers)
5. Select the better checkpoint based on validation loss, precision, recall, F1, and AUC — not accuracy alone
6. Save the result as `model.keras`

## Running the app locally

```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

pip install -r requirements.txt

# Place model.keras (from the training notebook) in this same folder

streamlit run app.py
```

Opens automatically at `http://localhost:8501`.

## Deploying to Streamlit Community Cloud

1. Push this project (including `model.keras`) to a GitHub repository.
2. Sign in to [streamlit.io](https://streamlit.io/) with GitHub.
3. Click **New app**, select the repository/branch, set the main file to `app.py`.
4. Click **Deploy**.

## Model details

- **Architecture:** MobileNetV2 (ImageNet weights), frozen feature extraction then fine-tuned
  on the top 30 layers.
- **Input size:** 224×224×3
- **Output:** single sigmoid unit (binary: Fresh Orange vs Formalin-mixed Orange)
- **Loss:** binary cross-entropy with label smoothing (0.1), to avoid overconfident 0%/100% predictions
- **Dataset:** [FruitVision](https://data.mendeley.com/datasets/xkbjx8959c/2) (Bijoy et al., 2025, Mendeley Data, DOI 10.17632/xkbjx8959c.2)

## Known limitation

Formalin causes only subtle visual changes to fruit compared to obvious spoilage/rot — this is
noted in FruitVision's own accompanying paper. This model is a classroom engineering exercise
and should be treated as a screening aid, not a substitute for chemical lab testing.

## Contributors

| # | Full Name | Registration Number | GitHub Username |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |
| 6 | | | |
| 7 | | | |
| 8 | | | |
| 9 | | | |
