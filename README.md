# 🚀 SQL Query Automation Using Selenium

This project automates executing SQL queries on the **Programiz Online SQL Compiler** using Selenium.  
It opens the compiler, inserts your SQL query, runs it, detects whether the query executed successfully, and saves a screenshot of the results.

---

## 📌 Features

- 🌐 Opens Programiz SQL compiler automatically  
- 📝 Inputs SQL query into CodeMirror editor  
- ▶️ Executes the query  
- ✔️ Detects whether output is a *result table* or *error*  
- 📸 Automatically captures screenshot **only when query succeeds**  
- 💾 Saves screenshots in a dedicated folder on Desktop  
- 🔧 Works with updated Programiz selectors (no iframe required)

---

## 🛠️ Technologies Used

- **Python 3**
- **Selenium WebDriver**
- **ChromeDriver**
- **WebDriverWait / Expected Conditions**
- **OS + DateTime modules**

---

## 📂 Project Structure

```
📁 sql-automation-selenium
│
├── README.md
├── selenium_sql_automation.py
└── sql_screenshots/   (auto-created)
```

---

## ▶️ How to Run

### **1. Install dependencies**

```bash
pip install selenium
```

### **2. Download ChromeDriver**

Ensure your ChromeDriver version matches your Chrome browser.

Download: https://chromedriver.chromium.org/

### **3. Update the ChromeDriver path in the script**

```python
service = Service(r"C:\Users\aksha\Downloads\chromedriver-win64\chromedriver.exe")
```

### **4. Run the script**

```bash
python selenium_sql_automation.py
```

---

## 📸 Screenshots Output

Screenshots of successful query runs are saved automatically at:

```
~/Desktop/sql_screenshots/
```

---

## ⚠️ Important Notes

- Ensure ChromeDriver & Chrome versions match  
- Works with updated Programiz UI  
- Uses `.any_of()` to detect results or errors  
- Automatically clears the editor before inserting the new query  

---

## 🤝 Contributing

Pull requests are welcome!  
If you find improvements, feel free to submit a PR.

---

## 📜 License

This project is licensed under the **MIT License**.
