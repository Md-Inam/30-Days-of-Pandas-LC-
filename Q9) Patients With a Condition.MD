A)
return patients.loc[patients["conditions"].str.contains(r"\bDIAB1\b", na=False, regex=True),
["patient_id","patient_name","conditions"]]    


r"\bDIAB1\b"  
r""
Raw string  

\b (word boundary)  
👉 “The character before/after must NOT be a letter, number, or underscore.”   
   
What matches ✅  
"DIAB1"                      
"ACNE DIAB1"              
"DIAB1 HYPERTENSION"           
"DIAB1, ASTHMA"                        
Because space, comma, start/end of string = valid boundaries.          
              
What does NOT match ❌              
"SADIAB100" → letters touching it                     
"DIAB12" → number touching it                   
"XDIAB1Y" → letters hugging it on both sides            

--- 

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

But Fails in Testcase
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
  
