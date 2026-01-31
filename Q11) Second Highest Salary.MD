A1) 

df=employee.drop_duplicates(subset="salary").sort_values("salary",ascending=False)
N=2
if len(df)<N or N<=0:
    ans= None
else:
    ans= df.iloc[N-1]["salary"]
return pd.DataFrame({"SecondHighestSalary":[ans]})

--- 

A2) 

df = (employee[["salary"]]
      .drop_duplicates()
      .sort_values("salary", ascending=False)
      .reset_index(drop=True))

if len(df) < 2:
    ans = None
else:
    ans = df.loc[1, "salary"]
return pd.DataFrame({"SecondHighestSalary": [ans]})

---

A3) 

s = employee['salary'].drop_duplicates().nlargest(2)
ans= s.iloc[-1] if len(s) == 2 else None
return pd.DataFrame({"SecondHighestSalary":[ans]})
