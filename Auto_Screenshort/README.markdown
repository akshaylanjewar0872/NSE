# MySQL Workbench Automation Script

## Overview
This Python script automates interactions with MySQL Workbench to execute a predefined SQL query, save the query in a new tab, and capture a screenshot of the query results. The script uses `pyautogui` for GUI automation, `pyperclip` for clipboard operations, and `subprocess` to launch and close MySQL Workbench.

The script performs the following steps:
1. Launches MySQL Workbench.
2. Creates a new SQL tab.
3. Renames the tab with a timestamped name.
4. Pastes a predefined SQL query (`SELECT * FROM nse.employee LIMIT 10;`).
5. Executes the query.
6. Navigates to the result grid.
7. Captures a screenshot of the results.
8. Closes MySQL Workbench.

## Prerequisites
- **Python 3.6+**: Ensure Python is installed.
- **MySQL Workbench**: Installed at the specified path (default: `C:\Program Files\MySQL\MySQL Workbench 8.0\MySQLWorkbench.exe`).
- **Python Libraries**:
  - `pyautogui`: For GUI automation.
  - `pyperclip`: For clipboard operations.
  - Install them using:
    ```bash
    pip install pyautogui pyperclip
    ```
- **Operating System**: Windows (due to the MySQL Workbench path and `taskkill` command).
- **MySQL Database**: A database with the `nse.employee` table accessible via MySQL Workbench.

## Setup
1. **Install Dependencies**:
   - Install Python libraries:
     ```bash
     pip install pyautogui pyperclip
     ```
2. **Verify MySQL Workbench Path**:
   - Ensure MySQL Workbench is installed at `C:\Program Files\MySQL\MySQL Workbench 8.0\MySQLWorkbench.exe`. Update the `mysql_workbench_path` variable if it’s installed elsewhere.
3. **Database Access**:
   - Ensure MySQL Workbench is configured to connect to a MySQL database with the `nse.employee` table.
4. **Output Directory**:
   - The script saves screenshots to `~/Downloads/sacreenshoret/`. Ensure you have write permissions in this directory.

## Usage
1. **Update User Inputs** (if needed):
   - Modify the `query`, `table_name`, `mysql_workbench_path`, or `screenshot_folder` variables in the script to match your environment.
   - Example:
     ```python
     query = "SELECT * FROM your_schema.your_table LIMIT 10;"
     table_name = "your_table"
     mysql_workbench_path = r"C:\Path\To\MySQLWorkbench.exe"
     screenshot_folder = r"C:\Path\To\Output\Folder"
     ```
2. **Run the Script**:
   - Execute the script in a Python environment:
     ```bash
     python script.py
     ```
3. **Script Execution**:
   - The script will:
     - Launch MySQL Workbench.
     - Create and rename a new SQL tab (e.g., `employee_YYYYMMDD_HHMMSS.sql`).
     - Paste and execute the query.
     - Save a screenshot of the results to `~/Downloads/sacreenshoret/mysql_output_YYYYMMDD_HHMMSS.png`.
     - Close MySQL Workbench.

## Output
- **SQL Tab**: A new tab in MySQL Workbench named `employee_YYYYMMDD_HHMMSS.sql` containing the query.
- **Screenshot**: A PNG file (`mysql_output_YYYYMMDD_HHMMSS.png`) in `~/Downloads/sacreenshoret/` containing a screenshot of the MySQL Workbench window, including the query results grid.
- **Console Output**: Progress messages indicating each step (e.g., "🟡 Opening MySQL Workbench...", "✅ Screenshot saved...").

## Limitations
- **GUI Dependency**: Requires MySQL Workbench and a GUI environment (Windows). Not suitable for headless servers.
- **Automation Reliability**: `pyautogui` relies on screen resolution, window focus, and timing (`time.sleep`). Changes in the UI or system performance may cause failures.
- **Hardcoded Query**: The query is specific to the `nse.employee` table. Update the `query` variable for other tables or schemas.
- **Error Handling**: Minimal error handling. Failures (e.g., wrong MySQL Workbench path, database connection issues) may cause the script to crash.
- **Timing Sensitivity**: Fixed `time.sleep` delays may not work on slower or faster systems. Adjust delays if needed.

## Troubleshooting
- **MySQL Workbench Doesn’t Open**:
  - Verify the `mysql_workbench_path` is correct.
  - Ensure MySQL Workbench is installed and accessible.
- **Screenshot Misses Results**:
  - Increase `time.sleep` values in steps 5 or 6 to allow more time for query execution or navigation.
  - Check if the `tab` and `down` keys correctly focus the result grid.
- **Database Errors**:
  - Ensure MySQL Workbench is configured to connect to the database and the `nse.employee` table exists.
- **Permission Issues**:
  - Verify write permissions in the `screenshot_folder` directory.

## Notes
- The script assumes MySQL Workbench’s default keyboard shortcuts (e.g., `Ctrl+T` for new tab, `Ctrl+Shift+Enter` for query execution). Update hotkeys if your Workbench configuration differs.
- For non-Windows systems, modify the `mysql_workbench_path` and replace `os.system("taskkill /f /im MySQLWorkbench.exe")` with an appropriate command (e.g., `pkill` on Linux/Mac).
- To enhance reliability, consider adding error handling or using a programmatic approach (e.g., PySpark with JDBC) instead of GUI automation.