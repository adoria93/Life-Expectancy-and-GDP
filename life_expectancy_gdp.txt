from matplotlib import pyplot as plt
import pandas as pd
import seaborn as sns

# Read in the data
df = pd.read_csv("all_data.csv")

# Countries in the dataset:
# Zimbabwe
# USA
# Germany
# Mexico
# China
# Chile

# Range of Years:
# 2000 - 2015

# Looking at the first few rows
print(df.head())

# Doing a slight rename for one of the columns. It has a very long time which is good for labeling, but not so nice
# for using in a plot.
df.rename(columns= {"Life expectancy at birth (years)" : "LEABY"}, inplace= True)

# Checking to see if the rename worked
df.head()


# Bar Charts To Compare Average
# First high level look

plt.bar(df.Country, df.GDP)
plt.show()

plt.bar(df.Country, df.LEABY)
plt.show()


# Violin Plots To Compare Life Expectancy Distributions 

fig = plt.subplots(figsize=(15, 10)) 

sns.violinplot(
    data = df,
    x = df.Country,
    y = df.LEABY
)
plt.savefig("violinplot.png")
plt.show()


# Bar Plots Of GDP and Life Expectancy over time

f, ax = plt.subplots(figsize=(10, 15))
ax = sns.barplot(
    x = df.Country,
    y = df.GDP,
    hue = df.Year, 
    data = df
)
plt.xticks(rotation= 90)
plt.ylabel("GDP in Trillions of U.S. Dollars")
plt.show()


f, ax = plt.subplots(figsize=(10, 15)) 
ax = sns.barplot(
    x = df.Country,
    y = df.LEABY,
    hue = df.Year, 
    data = df
)
plt.xticks(rotation= 90)
plt.ylabel("Life expectancy at birth in years")
plt.show()


# Scatter Plots of GDP and Life Expectancy Data

g = sns.FacetGrid(df, col="Country", hue="Year", col_wrap=4, height=2)
g = (g.map(plt.scatter, "GDP", "LEABY", edgecolor="w").add_legend())
plt.savefig("GDP vs LEABY.png")
plt.show()


# Line Plots for Life Expectancy

g3 = sns.FacetGrid(df, col="Country", col_wrap=3, height=4)
g3 = (g3.map(plt.scatter, "Year", "LEABY").add_legend())
plt.savefig("LEABY Comparision.png")
plt.show()


# Line Plots for GDP

g4 = sns.FacetGrid(df, col="Country", col_wrap=3, height=4)
g4 = (g4.map(plt.scatter, "Year", "GDP").add_legend())
plt.savefig("GDP comparision.png")
plt.show()
