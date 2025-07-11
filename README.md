## Apartment Price Regression README


### Table of Contents
1. [Folder Structure](#folder-structure)  
2. [Notebook Summaries](#notebook-summaries)  
   - [1) Data Preparation](#1-data-preparation)  
   - [2) Feature Selection](#2-feature-selection)  
   - [3) Linear Regression](#3-linear-regression)  
3. [How to Run](#how-to-run)  
4. [Instructor Notes](#instructor-notes)  

---

### Folder Structure


ApartmentPriceRegression/
├── 1- df\_preperartion\_regression.ipynb
├── 1- df\_feature\_selection\_regression.ipynb
├── 1- df\_model\_regression.ipynb
├── apartment\_price\_predictions.csv
├── apartment\_prepared.pkl
├── appartments\_train.csv
├── appartments\_test.csv
└── README.md


 **Notebooks**  
  1. `df_preperartion_regression.ipynb`: Clean & preprocess `appartments_train.csv` → `apartment_prepared.pkl`.  
  2. `df_feature_selection_regression.ipynb`: Load `apartment_prepared.pkl`, analyze correlations/VIF/SelectKBest, save `selected_features`.  
  3. `df_linear_regression.ipynb`: Train/evaluate models (OLS, Lasso, etc.) on selected features; generate `apartment_price_predictions.csv` for `appartments_test.csv`.  

 **Data Files**  
  - `appartments_train.csv`: Raw training data (features + price).  
  - `appartments_test.csv`: Hold-out set (features only).  
  - `apartment_prepared.pkl`: Preprocessed training DataFrame.  
  - `apartment_price_predictions.csv`: Final test-set predictions.  



### Notebook Summaries

#### 1) Data Preparation (`df_preperartion_regression.ipynb`)
- **Load & Inspect**: Read `appartments_train.csv` → `DataFrame.head()`, `.info()`, `.describe()`.  
- **Clean & Engineer**: Handle missing values, remove outliers, encode categorical (e.g., `location` → dummies), create “age_of_building = 2025 – year_built.”  
- **Save Output**: Export cleaned DataFrame as `apartment_prepared.pkl` for downstream use.  

#### 2) Feature Selection (`df_feature_selection_regression.ipynb`)
- **Load Prepared Data**: Read `apartment_prepared.pkl`.  
- **Analyze Correlations**: Correlation heatmap → drop features with |corr| > 0.8.  
- **Select Features**: Compute VIF, run `SelectKBest(f_regression)`, optionally Lasso; choose a concise set (e.g., `size_m2`, `rooms`, `location_*`, `age_of_building`).  
- **Save Features**: Store selected feature names (e.g., in a Python list or JSON).  

#### 3) Regression (`df_model_regression.ipynb`)
- **Import & Setup**: Load `apartment_prepared.pkl` & `selected_features`.  
- **Train & Validate**: Split train data, fit models (OLS, Ridge, Lasso, SVR, ElasticNet, KNN), compare R²/RMSE/MAE.  
- **Test-Set Predictions**: Preprocess `appartments_test.csv` identically, apply best model (Lasso), save predictions to `apartment_price_predictions.csv`.  

---

### How to Run
1. Launch Jupyter in the project folder.  
2. **Notebook 1**: Open `df_preperartion_regression.ipynb` → run all cells → generates `apartment_prepared.pkl`.  
3. **Notebook 2**: Open `df_feature_selection_regression.ipynb` → run all cells → identifies and saves `selected_features`.  
4. **Notebook 3**: Open `df_linear_regression.ipynb` → run all cells → outputs `apartment_price_predictions.csv`.  

> Ensure each notebook has access to its inputs (`.ipynb` files, CSVs, and any intermediate files). No manual path edits should be necessary if you run them sequentially in the same directory.

---

### Instructor Notes
- If you see missing-value errors, confirm that Notebook 1 ran fully and produced `apartment_prepared.pkl`.  
- Verify that one-hot–encoded column names in `selected_features` match those in `apartment_prepared.pkl`.  
- Model performance may vary slightly based on library versions; all notebooks set a random seed for reproducibility.  

---

Thank you for reviewing! For questions, refer to the notebooks’ markdown comments or contact z.eshtiaghi@student.uw.edu.pl.  
```
