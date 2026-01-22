.isin() is how pandas checks membership.
.isin() does element-wise comparison
Series.isin(values)
SQL and pandas do not guarantee row order unless explicitly specified using ORDER BY or sort_values. Any apparent order is incidental and should not be relied upon.

EX:
import pandas as pd
s = pd.Series([1, 2, 3, 4])
s.isin([1, 3])

Output:
True
False
True
False

.isin() works with:
lists
sets
pandas Series
numpy arrays

.isin() checks membership and returns a boolean mask that pandas can filter on.
.isin() does NOT compare DataFrame vs DataFrame.
It works on Series vs values, not table vs table.

| Goal           | Method     |
| -------------- | ---------- |
| IN / NOT IN    | `.isin()`  |
| JOIN tables    | `merge()`  |
| Anti-join      | `~.isin()` |
| Match rows     | `merge()`  |
| Compare values | `==`       |


If the question says:
“exists in another table

df["key"].isin(other_df["key"])


Wrong:                  DF
      df = ~customers[["id"]].isin(orders["id"])
      return df
Returns:
      id
0   True
1  False
2   True
3  False


A)
df=customers.loc[~customers["id"].isin(orders["customerId"])].sort_values("id",ascending=True)
return df[["name"]].rename(columns={"name":"Customers"})
