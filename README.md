# Basic-Sales-Summary-from-a-Tiny-SQLite-Database-using-Python
## Project Overview
This project demonstrates how to use **SQLite** inside **Python** to pull simple sales information from a database, perform basic aggregations (like total quantity sold and total revenue per product), nd visualize the results using a **Matplotlib** bar chart.

It is a beginner-friendly exercise that covers:
- Connecting to an SQLite database
- Running SQL queries from Python
- Loading results into Pandas DataFrame
- Printing results to the console
- Creating and saving a simple bar chart

---

## Dataset
We created a small SQLite database file named `sales_data.db` containing a single table:

**`sales` Table Structure:**
| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| product     | TEXT      | Name of the product |
| quantity    | INTEGER   | Number of units sold |
| price       | REAL      | Price per unit |

---

## Steps Performed

### Connect to the Database
```python
import sqlite3
conn = sqlite3.connect("sales_data.db")
````

We connected to the SQLite database file `sales_data.db` using Python's built-in `sqlite3` module.

---

### Run SQL Query

```python
query = """
SELECT 
    product, 
    SUM(quantity) AS total_qty, 
    SUM(quantity * price) AS revenue
FROM sales
GROUP BY product
"""
```

This query:

* Groups sales data by `product`
* Calculates total quantity sold (`total_qty`)
* Calculates total revenue (`revenue`) as `quantity * price`

---

###Load Data into Pandas DataFrame

```python
import pandas as pd
df = pd.read_sql_query(query, conn)
```

We loaded the SQL query results into a Pandas DataFrame for easy manipulation and visualization.

---

#print Results

```python
print(df)
```

Displayed the summary table in the terminal/Jupyter Notebook.

**Example Output:**

| product | total\_qty | revenue |
| ------- | ---------- | ------- |
| Apple   | 10         | 50.00   |
| Banana  | 20         | 80.00   |
| Orange  | 15         | 60.00   |

---

###Create and Save a Bar Chart

```python
import matplotlib.pyplot as plt
df.plot(kind='bar', x='product', y='revenue', legend=False)
plt.title("Revenue by Product")
plt.ylabel("Revenue ($)")
plt.xlabel("Product")
plt.savefig("sales_chart.png")
plt.show()
```

We created a bar chart showing **Revenue by Product** and saved it as `sales_chart.png`.

---

##Final Insights

* **Top-Selling Product by Revenue:** The chart quickly shows which product generated the most revenue.
* **Total Quantity vs. Revenue:** Even if a product sold more units, it might not have the highest revenue due to pricing differences.
* **Visual Advantage:** The bar chart makes it easy to spot the best and worst-performing products.

---

## 📁 Files in This Project

* `sales_data.db` — SQLite database containing sales data
* `sales_analysis.ipynb` — Python script or notebook with the analysis
* `sales_chart.png` — Bar chart visualization of revenue by product
* `README.md` — This documentation

---

## How to Run

1. Install dependencies:

   ```bash
   pip install pandas matplotlib
   ```
2. Place `sales_data.db` in the project folder.
3. Run the Python script:

   ```bash
   python sales_analysis.py
   ```
4. Check the console for printed results and open `sales_chart.png` to view the chart.

