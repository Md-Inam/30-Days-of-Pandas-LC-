
A1) 

pattern = r'^([A-Za-z][A-Za-z0-9._-]*@leetcode\.com)$'      
return users[users["mail"].str.contains(pattern, regex=True)]           
  
---  
 
A2) 
 
pattern=r'^([A-Z]|[a-z])[A-Za-z0-9._-]*@leetcode\.com$'   
return users.loc[users["mail"].str.contains(pattern),["user_id","name","mail"]]   
    
---   
   
pattern = r'^[A-Za-z][A-Za-z0-9._-]*@leetcode\.com$'      
  
| Symbol | Normal Meaning | Regex Meaning |  
| ------ | -------------- | ------------- | 
| `.`    | Dot            | Any character |  
| `\.`   | Dot            | Literal dot   |  
    
----   
  
| Part  | Meaning              |         
| ----- | -------------------- |            
| `A-Z` | Any uppercase letter |        
| `a-z` | Any lowercase letter |       
| `0-9` | Any digit            |         
| `.`   | A literal dot        |       
| `_`   | Underscore           |      
| `-`   | Dash                 |            
            
---          
         
             
| Part              | Meaning                          |    
| ----------------- | -------------------------------- |              
| `^`               | Start of string                  |          
| `[A-Za-z]`        | First character must be a letter |          
| `[A-Za-z0-9._-]*` | Remaining prefix allowed chars   |             
| `@leetcode\.com`  | Exact domain                     |          
| `$`               | End of string                    |      


