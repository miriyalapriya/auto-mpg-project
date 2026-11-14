# auto-mpg-project

Predicting car fuel efficiency (mpg) from design specifications, using the UCI Auto MPG dataset (398 cars, 1970 to 1982).

**Live website:** https://miriyalapriya.github.io/auto-mpg-project/

## What is in this repository

- `auto_mpg_project.ipynb`: the full analysis (data loading, exploration, split, baseline, cross-validation, tuning, final test, feature importance, error analysis, error range, model export)
- `auto_mpg.csv`: the data (car name column dropped; missing horsepower left empty)
- `model.json`: the final ridge model (means, scales, coefficients, intercept, error range) used by the website
- `index.html`: the project website (published with GitHub Pages)
- `pred_vs_actual.png`: predicted vs actual mpg plot used on the website

## Result

Final model: ridge regression on log(mpg). Test MAE 1.77 mpg (baseline 5.96), R squared 0.89. Model year and weight matter most.

## How to reproduce

1. Open `auto_mpg_project.ipynb` in Google Colab or Jupyter (Python 3, pandas, NumPy, scikit-learn, Matplotlib).
2. Run all cells in order. The data is loaded from the UCI repository, and a copy is saved as `auto_mpg.csv`.
3. Split: `train_test_split(test_size=0.2, random_state=42)`. Cross-validation: `KFold(5, shuffle=True, random_state=42)`.
4. The last cell exports `model.json`, which the website reads.

## Tools and AI use

Python, pandas, NumPy, scikit-learn, Matplotlib, Google Colab, GitHub Pages. An AI assistant (Claude) was used for planning, for help with some notebook code and for guidance while building the website. I ran and checked the outputs myself.
