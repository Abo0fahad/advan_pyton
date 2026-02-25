
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv("data/day27_boxplots.csv")

plt.figure(figsize=(6,4))
sns.histplot(data=df, x="score", bins=10, kde=True)
plt.title("Histogram of score")
plt.xlabel("score")
plt.ylabel("Frequency")
plt.show()

plt.figure(figsize=(6,4))
sns.boxplot(data=df, x="group", y="score")
plt.title("Boxplot of score by group")
plt.xlabel("group")
plt.ylabel("score")
plt.show()

group_stats = df.groupby("group")["score"].describe()
print(group_stats)
