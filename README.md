# Insert Data from One Database to Another using Python

## Description:
 - This Python script inserts data from a table in one MySQL database (source_dba) to another database (target_dba) on the same server.

## ✅ Features:
- Takes table name as input
- Inserts all data from source table to target table
- Works for tables with same structure and columns
- Uses mysql-connector-python for database operations

## 💡 Notes
- Both source_dba and target_dba must be on the same MySQL server.
- The table structures in both databases should be identical.
- For inserting data between different servers, modify the script to fetch data from source and insert into target in separate connections.

## 📝 Example Use Cases
- Data migration between schemas
- ETL automation scripts
- Backup table population
- Moving tables in Dev → Test → Prod databases

## 🔗 License
- This project is licensed under the MIT License – see the LICENSE file for details.

## 🙏 Acknowledgements
- MySQL Connector Python Documentation
- Python official documentation

## ✨ Contributions
- Contributions, issues, and feature requests are welcome! Feel free to open an issue or submit a pull request.
