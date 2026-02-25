import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv("data/day26_distributions.csv")

num_cols = df.select_dtypes(include=[np.number]).columns

for col in num_cols:
    sns.histplot(df[col], kde=True)
    plt.title(col)
    plt.show()

print(df[num_cols].mean())
print(df[num_cols].median())
print(df[num_cols].std())
print(df[num_cols].skew())

col_skewed = df[num_cols].skew().idxmax()
df[col_skewed + "_log1p"] = np.log1p(df[col_skewed])

sns.histplot(df[col_skewed], kde=True)
plt.title(col_skewed)
plt.show()

sns.histplot(df[col_skewed + "_log1p"], kde=True)
plt.title(col_skewed + " log1p")
plt.show()
