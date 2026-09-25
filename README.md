## Overview
The goal of this project is to predict market values of Premier League players based of their statistics during the 25/26 Premier League season.

## Method
Most of the data used to predict the market values were extracted from a football api, while the rest was collected from csv files.
I used One-Hot-Encoding for the position metric and had to take care of missing values in the dataset.
After Preprocessing, I trained different models and analyzed the feature importance of one model to know which features are of highest and least importance.
Due to analyzing the importance of metrics, I left out some feature that weren't of importance during training.
To conclude I compared the models with each other.

## Results
|Model|R2 score|RMSE in €|
|---|---|---|
|Ridge Regression|0.43|18,401,541 €|
|Random Forest Regressor|0.53|16,634,252 €|
|LightGBM|0.60|15,487,182 €|

## Limitations
- Shortage of metrics (e.g. contract duration or other in-game advanced metrics).
- The model underestimates players with high market values (> 80 m.) allegedly because of under representation in training.
- NaN-Handling when market values were missing or name mismatches occured during merging (which was handled via Fuzzy-Matching and manual verification).
- During analyzation of feature importance it was obvious that the models favoured offensive players, due to high importance in metrics that are primarily relevant to attackers (e.g. expected goals or expected assists).

## Setup

### Requirements
- Python 3.11+
- Free API-Key from [football-data.org](https://www.football-data.org/)

### clone Repository
\`\`\`bash
git clone https://github.com/ng7211/MarketValuePrediction2526.git
cd MarketValuePrediction2526
\`\`\`
  
### Dependencies installation
\`\`\`bash
pip install pandas
pip install requests
pip install python-dotenv
pip install scikit-learn
pip install lightgbm
pip install yellowbrick
pip install matplotlib
pip install numpy
pip install notebook
\`\`\`

### API-Key Configuration
1. Get free API-Key from https://www.football-data.org/client/register
2. Create a file named .env in the project structure with this content:
   FOOTBALL_DATA_API_TOKEN=your_api_key
> **Note:** Never commit your `.env` file — it's already excluded via `.gitignore`.
     
### Additional data sources
Besides the API following csv-files from [fbref.com](https://fbref.com) are needed and must be placed in the root directory of the project.
- `goalkeeper_stats.csv`
- `stats_relevant_for_defenders.csv`
- `all_player_profiles.csv`
- `all_player_stats.csv`
I got all data from this link: [Prem Stats](https://fbref.com/en/comps/9/2025-2026/2025-2026-Premier-League-Stats), by copying contents from the table and adding them to a csv-file.

### Run the notebook
\`\`\`bash
jupyter notebook prototype_market_value_pred.ipynb
\`\`\`
