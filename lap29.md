import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt


df = pd.read_csv("day29_correlations.csv")

ss = df[["feature_x","feature_y","feature_z","target"
]]
sns.heatmap(ss, annot=True,cmap="coolwarm",vmin=-1,vmax=1)
plt.show()
sns.scatterplot(x="feature_x",y="target",data=df)
plt.show()
sns.scatterplot(x="feature_y",y="feature_z",data=df)
plt.show()
