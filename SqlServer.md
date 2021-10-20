# Sql Server

## Upgrade localDb

- Upgrade to LocalDb 2019
  - Install File https://go.microsoft.com/fwlink/?LinkID=866658
  - Docs: https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/sql-server-express-localdb?view=sql-server-ver15#install-localdb
  - run these commands
    - sqllocaldb info
      - Gets the instances.
    - sqllocaldb info MSSQLLocalDB
      - Gets the version info for MSSQLLocalDB
    - If the version info is still the old version, then delete and recreate the MSSQLLocalDB
      - sqllocaldb stop mssqllocaldb
      - sqllocaldb delete mssqllocaldb
      - sqllocaldb create MSSQLLocalDB
      - sqllocaldb info MSSQLLocalDB
        - Should see the correct version now!

Reference for upgrading: https://stackoverflow.com/a/68161382/523907