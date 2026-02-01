A)  

df=employee.sort_values(by=["departmentId","salary"],ascending=[True,False])
    df=df.merge(department,left_on="departmentId",right_on="id")
    df["max"]=df.groupby("departmentId")["salary"].transform("max")
    result=df[df["salary"]==df["max"]][["name_y","name_x","salary"]]
    result.columns = ["Department", "Employee", "Salary"]
    return result






No Renaming: 
df=employee.sort_values(by=["departmentId","salary"],ascending=[True,False])
    df=df.merge(department,left_on="departmentId",right_on="id")
    df["max"]=df.groupby("departmentId")["salary"].transform("max")
    return df[df["salary"]==df["max"]]



---  


Sorting by 2 or more columns in pandas  
df.sort_values(by=["col1", "col2", "col3"], ascending=[True, False, True])  

--- 

Our case (department first, then highest salary)  
df.sort_values(by=["departmentId", "salary"], ascending=[True, False])  

===  

Two identical ways to merge   

1️⃣ Function style  
pd.merge(left_df, right_df, how="inner", on="col_name")    
    
2️⃣ Method style (same thing, cleaner)    
left_df.merge(right_df, how="inner", on="col_name")   
They do the exact same thing.  

left_on and right_on expect column NAMES (strings)
---   
                       
pd.merge(    
    left,          # first dataframe          
    right,         # second dataframe          
    how="inner",   # type of join                 
    on=None,       # column name common in both          
    left_on=None,  # column in left df       
    right_on=None  # column in right df               
)           

--- 

What if both tables have the SAME column name?  

use on= 

df.merge(Department, on="departmentId")

---  
  
 Selecting columns AFTER grouping   
df.groupby("col")["value_col"]  
  
Group first ( ), select column [ ]

--- 

groupby() = Split
Aggregation = Apply
Result = Combine 

---  

df.groupby("departmentId")["salary"].max()                
This returns a summary table like:         
  
departmentId	salary                    
1	90000                         
2	80000             
So now you know the highest salary per departme nt.      
 
But the question asks:  
Which employees earn those salaries? 

--- 

We take those max salaries and match them back to employees.

Step 1: store the max salaries
max_sal = df.groupby("departmentId")["salary"].transform("max")

Step 2: keep only employees who match
df = df[df["salary"] == max_sal] 




--- 


df.groupby("departmentId")["salary"].transform("max")
Step 1 → Split into departments
Step 2 → Find max salary in each department
Step 3 → Paste that max salary onto every row in that department
---



---

df.groupby("departmentId")["salary"].transform("max")
Here, "max" is not a function call.
It is a label telling transform which operation to repeat for every row.
