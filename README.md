import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
np.random.seed(42)
n = 200
df = pd.DataFrame({
    'total_bill': np.random.normal(loc=20, scale=8, size=n).clip(5, 50),
    'tip': np.random.normal(loc=3, scale=1.2, size=n).clip(1, 10),
    'sex': np.random.choice(['Male', 'Female'], size=n),
    'day': np.random.choice(['Thur', 'Fri', 'Sat', 'Sun'], size=n),
    'size': np.random.randint(1, 6, size=n)
})
sns.set_theme(style="whitegrid")
fig, axs = plt.subplots(2, 2, figsize=(15, 12))
sns.scatterplot(data=df, x="total_bill", y="tip", hue="sex", ax=axs[0, 0])
axs[0, 0].set_title("Total Bill vs Tip (by Sex)")
sns.histplot(df["total_bill"], kde=True, color="skyblue", ax=axs[0, 1])
axs[0, 1].set_title("Distribution of Total Bill")
sns.boxplot(data=df, x="day", y="tip", hue="sex", ax=axs[1, 0])
axs[1, 0].set_title("Tips by Day and Gender")
corr = df.corr(numeric_only=True)
sns.heatmap(corr, annot=True, cmap="coolwarm", fmt=".2f", ax=axs[1, 1])
axs[1, 1].set_title("Correlation Heatmap")
plt.tight_layout()
plt.savefig("sample_data_viz_output.png")
plt.show()
