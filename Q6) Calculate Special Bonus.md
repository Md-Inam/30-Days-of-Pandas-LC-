1) Row selection (filtering)        
This removes rows.                         
df.loc[condition, ["cols"]]     ->Output = only rows that match.             
           
2)Column creation (conditional assignment)                 
This keeps all rows and sets values.   
This is what you need.   

A “conditional statement” in pandas means:   
IF condition is true → give value A   
ELSE → give value B   
Because pandas can’t use normal if/else on an entire column (Series), it uses vectorized conditional tools   

 
A bonus is given only if:  
- `employee_id` is **odd**   
- `name` does **NOT** start with `"M"`  
  
Return a DataFrame with:    
- `employee_id`                            
- `bonus`                     
sorted by `employee_id`.               
              
---            
                    
✅ 1) `.where()` solution (cleanest, pandas-native)            
import pandas as pd                 
def calculate_special_bonus(employees: pd.DataFrame) -> pd.DataFrame:                     
    cond = (employees["employee_id"] % 2 == 1) & (~employees["name"].str.startswith("M"))           
    employees["bonus"] = employees["salary"].where(cond, 0)             
    return employees[["employee_id", "bonus"]].sort_values("employee_id")              
---            
            
✅ 2) np.where() solution (classic IF-ELSE)            
import pandas as pd           
import numpy as np          
def calculate_special_bonus(employees: pd.DataFrame) -> pd.DataFrame:                         
    cond = (employees["employee_id"] % 2 == 1) & (~employees["name"].str.startswith("M"))           
    employees["bonus"] = np.where(cond, employees["salary"], 0)             
    return employees[["employee_id", "bonus"]].sort_values("employee_id")           
    
---                  
            
✅ 3) .loc assignment solution                     
import pandas as pd                    
def calculate_special_bonus(employees: pd.DataFrame) -> pd.DataFrame:             
    employees["bonus"] = 0                 
    cond = (employees["employee_id"] % 2 == 1) & (~employees["name"].str.startswith("M"))         
    employees.loc[cond, "bonus"] = employees.loc[cond, "salary"]            
    return employees[["employee_id", "bonus"]].sort_values("employee_id")          
    
