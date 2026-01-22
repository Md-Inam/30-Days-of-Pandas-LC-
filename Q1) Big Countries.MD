Wrong:
df=world.loc[[world["area"]>3000000 | world["population"]>25000000,["name",    "population","area"]]]
return df


---
   
or → works only with single True/False values
pandas uses bitwise operators
df.loc[ row_condition , column_list ]

------ 
  
Conditions must be wrapped individually: (condition1) | (condition2)

>   >=    evaluated AFTER
|         evaluated BEFORE

----  

A)
    df=world.loc[(world["area"]>2999999) | (world["population"]>24999999),["name",    "population","area"]]
    return df

---  
   
A2)
    return world.loc[(world["area"] >= 3000000) | (world["population"] >= 25000000),["name", "population", "area"]]
