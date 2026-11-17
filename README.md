# Predicting Car Fuel Efficiency from Design Specifications

ES 335 course project, IIT Gandhinagar. Author: Miriyala Sai Priya.

**Live website:** https://miriyalapriya.github.io/auto-mpg-project/

## Question
Can a car's mpg be predicted from its design specifications (cylinders, displacement, horsepower, weight, acceleration, model year, origin), and which specifications matter most? The data covers cars from 1970 to 1982, so the results describe that period only. The model shows prediction, not causation.

## Main result
Ridge regression on log(mpg) misses by 1.77 mpg on average on 80 held-out test cars (baseline: 5.96 mpg), with R squared 0.894. Model year and weight matter most. The full reasoning, tables and figures are on the website.

## Repository contents
- `index.html`: the project website (GitHub Pages)
- `auto_mpg_project.ipynb`: the full analysis notebook (run top to bottom)
- `auto_mpg.csv`: the data (UCI Auto MPG, car name column dropped)
- `model.json`: the exported ridge model (means, scales, coefficients, intercept, error range)
- `pred_vs_actual.png`: predicted vs actual mpg plot for the test set
- `data_overview.png`: histogram of mpg and weight vs mpg scatter plot
- `train_rows.csv`, `test_rows.csv`: the exact rows used for training and testing
- `requirements.txt`: Python libraries

## How to reproduce
1. Open `auto_mpg_project.ipynb` in Google Colab or Jupyter.
2. Install the libraries if needed: `pip install -r requirements.txt` (tested with pandas 2.2.3 and scikit-learn 1.6.1).
3. Run all cells in order. The data cell downloads the dataset from UCI. If the download fails, put `auto_mpg.csv` in the same folder and the notebook will use it.
4. The later cells write `model.json`, `train_rows.csv`, `test_rows.csv` and `data_overview.png`.

## Method summary
- Split: `train_test_split(test_size=0.2, random_state=42)` gives 318 training and 80 test cars.
- Cross-validation: `KFold(5, shuffle=True, random_state=42)` on the training set only.
- Pipeline: median imputation for horsepower, standardization of the six numeric columns, one-hot encoding of origin, then Ridge (alpha=1.0) on log(mpg).
- Compared against: baseline (training mean), linear regression, ridge, random forest, gradient boosting.
- Random forest (200 trees) and gradient boosting use scikit-learn default settings with `random_state=42` and were not tuned.
- Extra experiments in the notebook: ridge penalty sweep, raw vs. log target, and one-at-a-time feature removal.
- The test set was used only after the models and settings were fixed, and nothing was changed afterwards.

## Data access
The Auto MPG dataset is public and free on the UCI Machine Learning Repository (https://doi.org/10.24432/C5859H, licence CC BY 4.0). A copy is included as `auto_mpg.csv`. No passwords, keys or private data are used.

## Use of AI tools
I used an AI assistant (Claude) for planning, for writing and debugging some notebook code (feature importance, error analysis, the error range and the JSON export), and for help building the website. I ran and checked the code and results myself and I am responsible for them.

## References
- Quinlan, R. (1993). Auto MPG [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5859H
- Pedregosa, F. et al. (2011). Scikit-learn: Machine Learning in Python. Journal of Machine Learning Research, 12, 2825-2830.
