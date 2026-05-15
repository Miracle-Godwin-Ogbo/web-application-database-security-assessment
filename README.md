# Web Application Database Security Assessment (SQLMap)

## Objective

To identify and assess SQL Injection vulnerabilities in a controlled web application environment using manual testing techniques, request analysis, and SQLMap.

---

## Scope

* Target: OWASP Juice Shop
* Environment: Local Lab Environment (Docker on Kali Linux)

---

## Tools Used

* SQLMap
* OWASP Juice Shop
* Firefox Developer Tools
* Kali Linux

---

## Methodology

The assessment followed a structured process:

1. Target setup
2. Manual input testing
3. Request interception and analysis
4. Parameter identification
5. Automated SQL Injection testing using SQLMap
6. Database enumeration
7. Risk analysis and mitigation review

---

# 1. Target Setup

Purpose:
To deploy and access the vulnerable web application in a controlled lab environment.

### Output

![Juice Shop Homepage](screenshots_juice-shop_homepage.png)

---

# 2. Manual Input Testing

Purpose:
To identify abnormal application behavior through manual SQL Injection testing.

### Test Payload

```sql
'
```

### Analysis

Special character input triggered abnormal application behavior, indicating improper input handling within the authentication process.

### Output

![Manual Input Test](screenshots_manual_input_test.png)

---

# 3. Request Capture & Analysis

Purpose:
To inspect authentication requests and identify parameters submitted to the backend application.

### Analysis

The login request was analyzed using browser developer tools to identify request methods, endpoints, and submitted parameters.

### Output

![Login Request Capture](screenshots_login_request_capture.png)

---

# 4. Parameter Identification

Purpose:
To identify potentially injectable parameters within the authentication request.

### Identified Parameters

* email
* password

### Output

![Request Payload](screenshots_request_payload.png)

---

# 5. SQLMap Testing

Purpose:
To automate SQL Injection testing against identified parameters.

### Command Used

```bash
sqlmap -r request.txt --batch
```

### Analysis

SQLMap was used to analyze the captured request and test application parameters for possible SQL Injection vulnerabilities.

### Output

![SQLMap Initial Scan](screenshots_sqlmap_initial_scan.png)

---

# 6. SQL Injection Detection

Purpose:
To verify whether backend database interaction could be manipulated through user-controlled input.

### Analysis

SQLMap identified injectable behavior within the tested request and detected backend database interaction.

### Output

![SQLMap Injection Detection](screenshots_sqlmap_injection_detection.png)

---

# 7. Database Enumeration

Purpose:
To enumerate accessible databases through identified SQL Injection vulnerabilities.

### Command Used

```bash
sqlmap -r request.txt --dbs --batch
```

### Analysis

Database enumeration demonstrated the potential impact of insecure input handling within the application.

### Output

![Database Enumeration](screenshots/database-enumeration.png)

---

# 8. Table Enumeration

Purpose:
To identify available database tables within the enumerated database.

### Command Used

```bash
sqlmap -r request.txt -D DATABASE_NAME --tables --batch
```

### Output

![Table Enumeration](screenshots/table-enumeration.png)

---

# Findings

* Improper input handling behavior was identified
* Authentication requests exposed potentially injectable parameters
* SQLMap successfully analyzed backend database interaction
* Database and table enumeration were possible within the lab environment

---

# Risk Analysis

SQL Injection vulnerabilities may allow attackers to:

* Access backend databases
* Bypass authentication mechanisms
* Extract sensitive information
* Manipulate application data
* Escalate attacks against backend systems

---

# Mitigation

* Use parameterized queries and prepared statements
* Implement proper input validation and sanitization
* Deploy Web Application Firewalls (WAF)
* Conduct regular security testing
* Follow secure coding practices

---

# Conclusion

This lab demonstrates how SQL Injection vulnerabilities can be identified and assessed through manual testing, request analysis, and automated SQLMap testing within a controlled environment.

---

# Disclaimer

All activities performed in this repository were conducted in a controlled lab environment for educational and ethical purposes only. The target application used was intentionally vulnerable and authorized for testing.
