ERROR:   
return patients.loc[patients["conditions"].str.startswith("DIAB1"),["patient_id","patient_name","conditions"]]    

---

That only catches rows where the string begins with "DIAB1"
Fails For  

| patient_id | patient_name | conditions   |   
| ---------- | ------------ | ------------ | 
| 3          | Bob          | DIAB100 MYOP |    
| 4          | George       | ACNE DIAB100 |  

---  
FIX:  

return patients.loc[
    patients["conditions"].str.contains("DIAB1", na=False),
    ["patient_id", "patient_name", "conditions"]]
---  

How:
str.contains("DIAB1") → finds it anywhere inside the text
na=False → avoids crashing if a row has missing values  

---  
 
| conditions         | startswith | contains |  
| ------------------ | ---------- | -------- |  
| DIAB1              | ✅          | ✅        |  
| ACNE DIAB1         | ❌          | ✅        |  
| DIAB1 HYPERTENSION | ✅          | ✅        |  
  
