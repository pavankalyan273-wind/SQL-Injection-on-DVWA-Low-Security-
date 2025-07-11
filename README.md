# SQL-Injection-on-DVWA-Low-Security

## What is DVWA?

**DVWA (Damn Vulnerable Web Application)** is a PHP/MySQL web application that is intentionally built with vulnerabilities. It is widely used for:

- Learning about common web security issues like SQL Injection, XSS, CSRF, etc.
- Practicing ethical hacking and penetration testing in a safe environment.
- Demonstrating how different security levels affect exploitation (Low, Medium, High, Impossible).

In this task, we use **DVWA's SQL Injection vulnerability (Low Security)** to simulate how attackers can extract data from an insecure web application.

> DVWA is for educational purposes only and should only be run in a **local or controlled environment**.

---

## Objective
Demonstrate how SQL Injection works on a vulnerable web application using DVWA (Damn Vulnerable Web Application) with the security level set to **Low**.

---

## 🛠Tools Used
- DVWA (Damn Vulnerable Web Application)
- Kali Linux / XAMPP
- Web Browser (for manual testing)
- Optional: `curl` (for simulation in shell script)

---

## ⚙Setup Instructions

1. **Install DVWA** on your local machine or VM:
   ```bash
   sudo apt update
   sudo apt install apache2 mariadb-server php php-mysqli git
   git clone https://github.com/digininja/DVWA.git /var/www/html/dvwa
   sudo service apache2 start
   sudo service mysql start
   ```

2. **Configure the database**:
   - Edit: `/var/www/html/dvwa/config/config.inc.php`
   - Set DB credentials and `allow_url_include`

3. **Access DVWA**:
   - Open `http://localhost/dvwa`
   - Click on "Create / Reset Database"

4. **Set Security Level**:
   - Navigate to the **DVWA Security** tab
   - Set **Security Level** to `Low`

---

## Performing SQL Injection

1. Go to the **SQL Injection** module:
   ```
   http://localhost/dvwa/vulnerabilities/sqli/
   ```

2. Enter the following payload in the ID field:
   ```
   1' OR '1'='1
   ```

3. Click **Submit**.

4. **Result**: The page displays all user records from the database. This confirms a successful SQL injection.

---

## Screenshots

- `sqli_payload_entry.png`: Shows the injection payload input.
- `sqli_results_output.png`: Displays the extracted user data.

---

## Vulnerability Explanation

- DVWA directly places user input into an SQL query without validation.
- Payload like `' OR '1'='1` always returns true and bypasses logic.
- This leads to exposure of **all database records**, showing how unvalidated input leads to full compromise.

---

## Script Used (Optional)

The following script simulates an injection attempt using `curl`:

```bash
#!/bin/bash
# sql_injection_exploit.sh

URL="http://localhost/dvwa/vulnerabilities/sqli/"
PAYLOAD="id=1' OR '1'='1&Submit=Submit"

curl -X GET "$URL?$PAYLOAD"
```

> Note: You must be logged in and have a valid session/cookie.

---

## Demo Video Idea

**Title**: Exploiting SQL Injection in DVWA (Low Security)

**Steps to record**:
1. Launch DVWA
2. Set security level to **Low**
3. Perform the SQL Injection
4. Explain how the payload bypasses security
5. Show output of exposed data

---

## Conclusion

This task proves how dangerous SQL injection can be when input validation is ignored. Even on a low-security test app like DVWA, attackers can easily retrieve sensitive information using basic logic injection.

**Always use input sanitization, validation, and prepared statements.**
