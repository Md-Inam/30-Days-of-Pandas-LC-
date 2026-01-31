What is the Nth highest DISTINCT salary?” 
  
So we need to:             
Remove duplicates                 -> employee = employee.drop_duplicates(subset="salary")     
Order salaries from high to low   -> employee = employee.sort_values("salary", ascending=False)    
Pick the Nth one                 
-> if len(employee) < n:
    return None
else:
    return employee.iloc[n-1]["salary"]


---  
    
df.iloc[1]["salary"]          # row first, then column name  
df.loc[1, "salary"]           # label-based selection  
df.iloc[1, 1]                 # pure position-based  

---
  
| Requirement       | What we return            |   
| ----------------- | ------------------------- |           
| Must be DataFrame | `pd.DataFrame(...)`       |           
| One column        | `"getNthHighestSalary"`   |          
| One value         | `[ value ]` inside a list |      



Because the task is not:   
“Show the Nth highest salary column”  
   
The task is:   
“Implement a function called getNthHighestSalary”   


---

A) 

    df = employee.drop_duplicates(subset=["salary"])
    df = df.sort_values("salary", ascending=False)

    if N<=0 or len(df) < N:
        ans = None
    else:
        ans = df.iloc[N-1]["salary"]

    return pd.DataFrame({f"getNthHighestSalary({N})": [ans]})

---  




