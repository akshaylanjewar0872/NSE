# SQL Query Automation Using Selenium  
This script automates running a SQL query on Programiz Online SQL Compiler using Selenium.  
It opens Chrome, pastes the SQL query, executes it, and takes a screenshot **only if** the query runs successfully.

---

## 🧩 Features
- Opens Programiz SQL compiler automatically  
- Pastes your SQL query into the CodeMirror editor  
- Runs the query  
- Detects whether the output is a **result table** or an **error**  
- Saves a **screenshot** of the results if the query succeeds  
- Stores screenshots in a dedicated folder on Desktop  

---

## 📌 Python Code

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.common.exceptions import TimeoutException, WebDriverException
from datetime import datetime
import os
import sys
import time

# --- CONFIGURATION & USER INPUT ---
QUERY = "SELECT * FROM Customers left join Orders on customers.customer_id = Orders.customer_id" 
URL = "https://www.programiz.com/sql/online-compiler"

# Updated selectors (no iframe needed)
EDITOR_AREA_CLASS = "CodeMirror"
TEXTAREA_SELECTOR = ".CodeMirror textarea"
RUN_BUTTON_SELECTOR = ".cta-btn"
RESULT_TABLE_SELECTOR = ".output-table__table"
ERROR_OUTPUT_SELECTOR = ".output-area__error"

# Screenshot folder
SCREENSHOT_FOLDER = os.path.join(os.path.expanduser("~"), "Desktop", "sql_screenshots")
os.makedirs(SCREENSHOT_FOLDER, exist_ok=True)
print(f"Screenshots will be saved to: {SCREENSHOT_FOLDER}")

# --- SETUP CHROME DRIVER ---
try:
    service = Service(r"C:\Users\aksha\Downloads\chromedriver-win64\chromedriver.exe")
    chrome_options = Options()
    chrome_options.add_argument("--start-maximized")
    # chrome_options.add_argument("--headless=new")  # optional silent mode
    driver = webdriver.Chrome(service=service, options=chrome_options)
    wait = WebDriverWait(driver, 20)
except Exception as e:
    print(f"❌ Could not start Chrome driver: {e}")
    sys.exit(1)

# --- MAIN AUTOMATION ---
try:
    print(f"\n🌐 Opening Programiz SQL compiler...")
    driver.get(URL)

    # 1️⃣ Wait until editor is visible
    print("🧩 Waiting for SQL editor to load...")
    editor = wait.until(EC.presence_of_element_located((By.CLASS_NAME, EDITOR_AREA_CLASS)))
    editor.click()

    # 2️⃣ Enter the SQL query
    print("💾 Entering SQL query...")
    textarea = wait.until(EC.presence_of_element_located((By.CSS_SELECTOR, TEXTAREA_SELECTOR)))
    textarea.send_keys(Keys.CONTROL, "a")
    textarea.send_keys(Keys.DELETE)
    textarea.send_keys(QUERY)

    # 3️⃣ Click Run SQL
    print("▶️ Executing query...")
    run_button = wait.until(EC.element_to_be_clickable((By.CSS_SELECTOR, RUN_BUTTON_SELECTOR)))
    run_button.click()

    # 4️⃣ Wait for results
    print("⏳ Waiting for results (max 15 seconds)...")
    wait_for_result = WebDriverWait(driver, 20)
    wait_for_result.until(
        EC.any_of(
            EC.presence_of_element_located((By.CSS_SELECTOR, RESULT_TABLE_SELECTOR)),
            EC.presence_of_element_located((By.CSS_SELECTOR, ERROR_OUTPUT_SELECTOR))
        )
    )

    # 5️⃣ Check if results or error appeared
    result_tables = driver.find_elements(By.CSS_SELECTOR, RESULT_TABLE_SELECTOR)
    if result_tables:
        print("✅ Query successful! Taking screenshot...")
        time.sleep(2)
        timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
        screenshot_path = os.path.join(SCREENSHOT_FOLDER, f"query_result_{timestamp}.png")
        driver.save_screenshot(screenshot_path)
        print(f"📸 Screenshot saved: {screenshot_path}")
    else:
        try:
            error_element = driver.find_element(By.CSS_SELECTOR, ERROR_OUTPUT_SELECTOR)
            print("❌ Query failed with error:")
            print("----------------------------------------")
            print(error_element.text.strip())
            print("----------------------------------------")
        except:
            print("⚠️ No visible output found (no table or error).")

except TimeoutException:
    print("❌ Timeout: Editor or result not loaded in time.")
except Exception as e:
    print(f"💥 Unexpected error: {e}")
finally:
    print("🔒 Closing browser...")
    driver.quit()
```

---

## 📎 Notes
- Make sure your **ChromeDriver version matches your Chrome version**  
- Folder `sql_screenshots` is created automatically on Desktop  
- Works even if the result takes time (up to 20 seconds)

---

