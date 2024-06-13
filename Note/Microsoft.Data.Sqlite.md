Something about Microsoft.Data.Sqlite:

- Parameters are used to protect against SQL injection attacks. **However, it will prevent the program from running when use parameters while creating table. It also can't be used to replace table names. PLUS, never use it if the command will be run by SqliteCommand.ExecuteScalar(), or you'll get the column name instead of the value you want(I don't know why).**
