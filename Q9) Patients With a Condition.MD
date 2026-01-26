Optimal:        
return patients.loc[patients["conditions"].fillna("").str.split().apply(lambda words:any(word.startswith("DIAB1") for word in words))]
   
| Operation Type      | What NaN does                   | Need fillna?       |     
| ------------------- | ------------------------------- | ------------------ |             
| `.str.method()`     | Can break logic or later loops  | ✅ Usually YES      |         
| `.sum()`, `.mean()` | Ignored automatically           | ❌ Usually NO       |         
| `+ - * /` math      | Spreads NaN but doesn’t crash   | 🤔 Depends on goal |         
| Custom `.apply()`   | Often crashes if NaN unexpected | ✅ Often YES        |             

lambda words: receives a list of condition codes for one patient, like ["ACNE", "DIAB100"].        
The loop checks each individual code (word) in that list.                     
any(word.startswith("DIAB1") ...) returns True if at least one code begins with DIAB1           
          
                  
---   

Also FAIL:
return patients.loc[patients["conditions"].str.contains(r"(^|\s)DIAB1\w*", na=False, regex=True),["patient_id","patient_name","conditions"]]

---  


Error:   
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


conditions contains codes separated by spaces      
Type I Diabetes always starts with DIAB1 prefix  
That means each condition is a token, and we match any token that starts with DIAB1, not equals DIAB1  


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
  
