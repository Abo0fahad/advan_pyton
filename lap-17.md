import pandas as pd
from sklearn.preprocessing import OneHotEncoder


df18 = pd.read_csv("day18_binning.csv")



bin_edges = [0, 18, 35, 50, 100]
labels = ["Child", "YoungAdult", "Adult", "Senior"]
df18["age_bins_width"] = pd.cut(df18["age"], bins=bin_edges, labels=labels, right=False)
print(df18["age_bins_width"].value_counts())

df18["age_bins_quantiles"] = pd.qcut(df18["age"], q=4, labels=["Q1", "Q2", "Q3", "Q4"])
print(df18["age_bins_quantiles"].value_counts())

age_edges = [0, 13, 18, 65, 120]
age_labels = ["Child", "Teen", "Adult", "Senior"]
df18["age_group"] = pd.cut(df18["age"], bins=age_edges, labels=age_labels, right=False)
print(df18["age_group"].value_counts())

ohe = OneHotEncoder(handle_unknown="ignore")
age_encoded = ohe.fit_transform(df18[["age"]])
print("Encoded shape:", age_encoded.shape, "Categories:", ohe.categories_)
