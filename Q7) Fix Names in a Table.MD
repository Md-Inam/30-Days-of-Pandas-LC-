✅ Goal         
For each name:                         
only the first letter uppercase             
the rest lowercase              

---
  
“How can one line do TWO operations: first letter uppercase AND rest lowercase?”    

---

You can do this in TWO ways:   
  

✅ Best (one operation that already contains both rules)             
users["name"] = users["name"].str.capitalize()                    

---
    
✅ Manual (shows two explicit operations)   
users["name"] = users["name"].str[0].str.upper() + users["name"].str[1:].str.lower()    


---------
  
| Method              | What it does                           |
| ------------------- | -------------------------------------- |
| `.str.lower()`      | all lowercase                          |
| `.str.upper()`      | ALL UPPERCASE                          |
| `.str.capitalize()` | First letter uppercase, rest lowercase |
| `.str.title()`      | First Letter Of Every Word Uppercase   |
