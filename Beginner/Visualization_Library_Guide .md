# Visualization Library Documentation Guide: Matplotlib & Seaborn

## 1. Library Overview

### 1.1 Matplotlib
Matplotlib is the original Python plotting library, and nearly every other visualization tool in the Python ecosystem (including Seaborn) is built on top of it. Its defining trait is low-level control: every axis, tick, label, and color can be set explicitly. This makes it verbose for simple charts but indispensable when a project needs a custom or unusual figure.

**Typical use cases:** publication-ready figures, custom annotations, multi-panel layouts, and any chart type that doesn't fit a standard statistical mold.

### 1.2 Seaborn
Seaborn is a statistical plotting library built on top of Matplotlib. It works directly with pandas DataFrames, so a chart can usually be built by naming columns instead of manually extracting arrays. It ships with attractive default themes and can compute statistical summaries (like confidence intervals or regression fits) automatically.

**Typical use cases:** exploratory data analysis, comparing distributions across groups, and visualizing relationships between several variables at once with minimal code.

---

## 2. Graph Types

### 2.1 Line Plot
**Description:** Connects sequential data points, best suited to showing change across a continuous axis such as time.
**Use case:** Tracking a website's daily visitor count over a month.

```python
# Matplotlib
import matplotlib.pyplot as plt

months = ["Jan", "Feb", "Mar", "Apr", "May"]
visitors = [1200, 1450, 1100, 1700, 2000]

plt.plot(months, visitors, color="darkorange", marker="s")
plt.title("Monthly Website Visitors")
plt.xlabel("Month")
plt.ylabel("Visitors")
plt.show()
```

```python
# Seaborn
import seaborn as sns
import pandas as pd

df = pd.DataFrame({"month": months, "visitors": visitors})
sns.lineplot(data=df, x="month", y="visitors", marker="s")
```

### 2.2 Scatter Plot
**Description:** Plots individual data points along two numeric axes, used to reveal correlation or clustering.
**Use case:** Checking whether advertising spend relates to units sold.

```python
# Matplotlib
spend = [5, 10, 15, 20, 25, 30]
units_sold = [40, 55, 58, 72, 80, 95]

plt.scatter(spend, units_sold, color="teal")
plt.xlabel("Ad Spend ($100s)")
plt.ylabel("Units Sold")
plt.title("Ad Spend vs Units Sold")
plt.show()
```

```python
# Seaborn — includes a fitted trend line automatically
df2 = pd.DataFrame({"spend": spend, "units_sold": units_sold})
sns.regplot(data=df2, x="spend", y="units_sold")
```

### 2.3 Bar Chart
**Description:** Compares a numeric value across separate categories with rectangular bars.
**Use case:** Comparing quarterly revenue across four store branches.

```python
# Matplotlib
branches = ["North", "South", "East", "West"]
revenue = [32000, 28500, 41000, 25300]

plt.bar(branches, revenue, color="indianred")
plt.title("Quarterly Revenue by Branch")
plt.ylabel("Revenue ($)")
plt.show()
```

```python
# Seaborn — auto-adds error bars when multiple values exist per category
df3 = pd.DataFrame({"branch": branches, "revenue": revenue})
sns.barplot(data=df3, x="branch", y="revenue", hue="branch", legend=False)
```

### 2.4 Histogram
**Description:** Bins numeric data and displays how frequently values fall into each bin, revealing the shape of a distribution.
**Use case:** Understanding the spread of customer ages in a dataset.

```python
# Matplotlib
import numpy as np

ages = np.random.normal(35, 8, 300)

plt.hist(ages, bins=20, color="mediumseagreen", edgecolor="black")
plt.title("Distribution of Customer Ages")
plt.xlabel("Age")
plt.ylabel("Count")
plt.show()
```

```python
# Seaborn — adds a smoothed density curve
sns.histplot(ages, bins=20, kde=True, color="mediumseagreen")
```

### 2.5 Pie Chart
**Description:** Represents each category's proportion of a whole as a slice of a circle. Works best with a small number of categories.
**Use case:** Showing how a household budget is split across expense categories.

```python
# Matplotlib (Seaborn deliberately omits a pie-chart function, favoring bar charts for readability)
categories = ["Rent", "Food", "Transport", "Savings"]
share = [40, 25, 15, 20]

plt.pie(share, labels=categories, autopct="%1.0f%%", startangle=90)
plt.title("Household Budget Split")
plt.show()
```

### 2.6 Box Plot
**Description:** Summarizes a distribution using its median, quartiles, and outliers — useful for comparing spread across multiple groups.
**Use case:** Comparing delivery times across two courier services.

```python
# Matplotlib
courier_a = np.random.normal(48, 6, 100)
courier_b = np.random.normal(40, 10, 100)

plt.boxplot([courier_a, courier_b], tick_labels=["Courier A", "Courier B"])
plt.ylabel("Delivery Time (hrs)")
plt.title("Delivery Time Comparison")
plt.show()
```

```python
# Seaborn
df4 = pd.DataFrame({
    "time": np.concatenate([courier_a, courier_b]),
    "courier": ["Courier A"] * 100 + ["Courier B"] * 100
})
sns.boxplot(data=df4, x="courier", y="time")
```

### 2.7 Heatmap
**Description:** Displays a matrix of values as a grid of colors, where color intensity encodes magnitude — commonly used for correlation matrices.
**Use case:** Visualizing correlations between numeric features before building a model.

```python
# Seaborn — handles color mapping and cell annotation automatically
df5 = pd.DataFrame(np.random.rand(6, 6), columns=list("ABCDEF"))
corr = df5.corr()
sns.heatmap(corr, annot=True, cmap="viridis")
```

```python
# Matplotlib equivalent — requires manual color bar and tick labels
fig, ax = plt.subplots()
cax = ax.imshow(corr, cmap="viridis")
fig.colorbar(cax)
ax.set_xticks(range(len(corr.columns)))
ax.set_yticks(range(len(corr.columns)))
ax.set_xticklabels(corr.columns)
ax.set_yticklabels(corr.columns)
plt.show()
```

---

## 3. Comparison: Matplotlib vs Seaborn

| Criteria | Matplotlib | Seaborn |
|---|---|---|
| Ease of use | More code needed for common charts; steeper learning curve | Faster for standard statistical charts; sensible defaults |
| Customization | Full, granular control over every element | Good, but complex tweaks still require dropping to Matplotlib |
| Interactivity | None natively — static output | None natively — also static, since it renders through Matplotlib |
| Performance (large datasets) | Can slow down with very large point counts | Similar constraints, plus overhead from statistical aggregation |
| Best for | Custom, precise, or non-standard chart types | Fast exploratory analysis and DataFrame-driven workflows |

**Summary:** Seaborn is the faster starting point for exploring a dataset with good-looking statistical charts. Matplotlib is the right tool when a project needs fine-grained control — custom layouts, annotations, or a chart type outside Seaborn's statistical scope. In practice, the two are often combined: a Seaborn plot for speed, followed by a few Matplotlib calls to fine-tune titles, labels, or figure size.

---

## 4. Resources
- Matplotlib documentation: https://matplotlib.org/stable/users/explain/quick_start.html#quick-start
- Seaborn tutorial: https://seaborn.pydata.org/tutorial/introduction.html
