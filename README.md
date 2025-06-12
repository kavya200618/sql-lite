# sql-lite
# 📊 Task 7 - Basic Sales Summary from SQLite using Python

This task was completed as part of the **Data Analyst Internship** program. The goal was to extract and visualize basic sales information using SQL queries embedded in Python.

To achieve this, I used Python and SQLite to:
- Connect to a database file named `sales_data.db`
- Run a query to find the total quantity sold and total revenue per product
- Display the results using `print()`
- Visualize the revenue by product using a bar chart created with `matplotlib`

The tools used include:
- Python (with sqlite3, pandas, matplotlib)
- SQLite (built-in with Python)
- Jupyter Notebook or a `.py` file

The SQLite database contains a single table named `sales` with the following columns:
- `product` (TEXT)
- `quantity` (INTEGER)
- `price` (REAL)

The process is as follows:

```python
import sqlite3
import pandas as pd
import matplotlib.pyplot as plt

# Connect to the database
conn = sqlite3.connect("sales_data.db")

# Run SQL query to get total quantity and revenue per product
query = """
SELECT product, 
       SUM(quantity) AS total_qty, 
       SUM(quantity * price) AS revenue 
FROM sales 
GROUP BY product
"""

# Load result into a pandas DataFrame
df = pd.read_sql_query(query, conn)

# Print the DataFrame
print(df)

# Plot revenue by product
df.plot(kind='bar', x='product', y='revenue', title='Revenue by Product')
plt.xlabel("Product")
plt.ylabel("Revenue")
plt.tight_layout()
plt.savefig("sales_chart.png")  # Optional: saves the chart as a PNG file
plt.show()
