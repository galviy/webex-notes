# 1. XSS Payload
    <script>alert(1)</script>
# 2. DOM XSS
- DOM XSS Tergantung pada sink nya
  ## 1. document.write sink
  memanfaatkan unsanitized query pada searching yang memungkan attacker melakukan penitupan atribut src pada tag <img> dan menyisipkan fungsi berbahaya (event handler).
      
     Contoh source code:
     ```html
         <img src="...?searchTerms=INPUT">
     ```
     exploit
    - ` "><svg onload=alert(1)>`
    - `" onload="alert()`

    Contoh Vuln pada javascript
  
  ```js
  function trackSearch(query) {
       document.write('<img src="/resources/images/tracker.gif?searchTerms='+query+'">');
  }
  var query = (new URLSearchParams(window.location.search)).get('search');
   if(query) {
      trackSearch(query);
  }   
  ```
  
  `document.write('<img src="/resources/images/tracker.gif?searchTerms='+query+'">');`
   Menerima Teks Mentah: document.write akan mengambil string apa pun di dalamnya dan langsung menerjemahkannya sebagai kode HTML aktif di browser

  patching

  ```js
  function trackSearch(query) {

    const img = document.createElement('img');
    
    img.src = '/resources/images/tracker.gif?searchTerms=' + encodeURIComponent(query);
    
    document.body.appendChild(img);
  }
  ```
  atau gunakan `encodeURIComponent` jika terpaksa menggunakan document.write
  
  ## 2. innerHTML sink
  Properti .innerHTML akan execute string apa pun yang dimasukkan ke dalamnya sebagai kode HTML. Jika attacker mengirim teks yang mengandung tag <script> atau elemen HTML dengan event handler          berbahaya, browser korban akan langsung mengeksekusinya.
  
  Contoh source code:
   ```html
    <div id="searchMessage">INPUT</div>
   ```
    ```js
     function doSearchQuery(query) {
        document.getElementById('searchMessage').innerHTML = query;
     }
    var query = (new URLSearchParams(window.location.search)).get('search');
    if(query) {
         doSearchQuery(query);
    }                
    ```
    
   exploit
  -  `<img src=x onerror=alert(1)>`
  - `<svg onload=alert(1)>`
     
# 3. Stored XSS

# 4. Reflected XSS

    
