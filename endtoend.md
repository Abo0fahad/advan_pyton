import pandas as pd
import numpy as np

# ----------------------------------------------------
# 1) Load raw dataset
# ----------------------------------------------------
def load_raw_data(path="data/day15_real_dataset.csv"):
    df = pd.read_csv(path)
    return df


# ----------------------------------------------------
# 2) Cleaning function
# ----------------------------------------------------
def clean_data_project(df):

    # --- Fix data types ---
    # Example: convert date columns if they exist
    for col in df.columns:
        if "date" in col.lower():
            try:
                df[col] = pd.to_datetime(df[col], errors="coerce")
            except:
                pass

    # --- Handle missing values ---
    # Numeric: fill with median
    numeric_cols = df.select_dtypes(include=["int64", "float64"]).columns
    df[numeric_cols] = df[numeric_cols].fillna(df[numeric_cols].median())

    # Categorical: fill with mode
    categorical_cols = df.select_dtypes(include=["object"]).columns
    for col in categorical_cols:
        if df[col].isna().sum() > 0:
            df[col] = df[col].fillna(df[col].mode()[0])

    # --- Remove outliers (simple IQR method) ---
    for col in numeric_cols:
        Q1 = df[col].quantile(0.25)
        Q3 = df[col].quantile(0.75)
        IQR = Q3 - Q1
        lower = Q1 - 1.5 * IQR
        upper = Q3 + 1.5 * IQR
        df[col] = np.where(df[col] < lower, lower,
                           np.where(df[col] > upper, upper, df[col]))

    # --- Clean string columns ---
    for col in categorical_cols:
        df[col] = df[col].astype(str).str.strip().str.lower()

    return df


# ----------------------------------------------------
# 3) Save cleaned dataset
# ----------------------------------------------------
def save_cleaned_data(df, path="data/day15_cleaned.csv"):
    df.to_csv(path, index=False)


# ----------------------------------------------------
# 4) Run the full pipeline
# ----------------------------------------------------
if __name__ == "__main__":
    raw_df = load_raw_data()
    cleaned_df = clean_data_project(raw_df)
    save_cleaned_data(cleaned_df)
    print("Cleaning completed and file saved!")
