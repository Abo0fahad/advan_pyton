import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
df = pd.read_csv("day31_seaborn.csv")

sns.histplot(df["age"], bins=30,)
plt.title("Age informisn--histplot")
plt.show()

sns.kdeplot(data=df, x="income", hue="segment", fill=True, )
plt.title("Income Density --kdeplot ")
plt.show()

sns.boxplot(data=df, x="segment", y="income")
plt.title("Income by Segment — Boxplot")
plt.show()


sns.countplot(data=df, x="segment")
plt.title("Segment Distribution--countplot")
plt.show()
