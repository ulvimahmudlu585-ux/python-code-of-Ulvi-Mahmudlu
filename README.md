# python-code-of-Ulvi-Mahmudlu
stat 112 final project

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("my_csv3.csv")



# 1) smoking_status filtered
# none and current are removed
df = df[~df["smoking_status"].isin(["none", "current"])]

# 2) order for sleep_disorder
sleep_order = ["none", "sleep apnea", "insomnia"]
df["sleep_disorder"] = pd.Categorical(
    df["sleep_disorder"],
    categories=sleep_order,
    ordered=True
)
# 3) catplot
g = sns.catplot(
    data=df,
    x="smoking_status",
    hue="bmi_category",     # underweight / normal / overweight / obese
    col="sleep_disorder",   # seperate graphs
    kind="count"
)

g.set_axis_labels("Smoking status", "Count")
g.set_titles("Sleep disorder: {col_name}")
plt.show()

