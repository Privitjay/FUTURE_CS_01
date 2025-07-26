# FUTURE_CS_01
# 🧪 Web Application Testing Report – DVWA

## 1. Project Information

| Field             | Details                                      |
|------------------|----------------------------------------------|
| **Application**   | Damn Vulnerable Web Application (DVWA)       |
| **Test Date**     | [11/07/2025 – 11/08/2025]                      |                  |
| **Environment**   | Hostinger VPS |
| **Security Level**| Low / Medium / High / Impossible             |
| **Tools Used**    | Burp Suite, OWASP ZAP, Nikto, curl, etc.     |

---

## 2. Test Objectives

- Identify and exploit vulnerabilities in DVWA modules.
- Validate known web application weaknesses.
- Practice manual and automated testing techniques.
- Demonstrate mitigation strategies for common security flaws.

---

## 3. Scope of Testing

**Modules Tested**
- [x] Brute Force  
- [x] Command Injection  
- [x] File Inclusion  
- [x] File Upload  
- [x] SQL Injection  
- [x] XSS (Reflected & Stored)  
- [x] Security Level Validation  


## 4. Methodology

| Aspect         | Description                                         |
|----------------|-----------------------------------------------------|
| **Approach**    | Manual testing with automated tool assistance      |
| **Test Types**  | Penetration Testing, Vulnerability Assessment      |
| **Tools Used**  | Burp Suite, OWASP ZAP, Nikto, browser devtools |
| **Security Levels Tested** | Low / Medium / High / Impossible        |

---

## 5. Summary of Findings

| Vulnerability         | Module            | Severity | Exploited | Status     | Notes                              |
|-----------------------|-------------------|----------|-----------|------------|------------------------------------|
| SQL Injection         | SQL Injection     | High     | ✅        | Confirmed  | `' OR 1=1--` exploited             |
| Stored XSS            | XSS (Stored)      | High     | ✅        | Confirmed  | Persistent `<script>` executed    |
| Reflected XSS         | XSS (Reflected)   | Medium   | ✅        | Confirmed  | Alert triggered                    |
| Command Injection     | Command Injection | High     | ✅        | Confirmed  | Executed OS commands via input    |
| File Upload Bypass    | File Upload       | High     | ✅        | Confirmed  | Uploaded web shell `.php`         |            |
| Brute Force           | Brute Force       | Medium   | ✅        | Confirmed  | Weak creds discovered             |
| Local File Inclusion  | File Inclusion    | High     | ✅        | Confirmed  |Accessed `/etc/passwd,systeminfo`  |

---

## 6. Detailed Vulnerabilities

#### 6.1.1  Nikto

I used Nikto to scan for vulnerabilities on the webpage.. 
Nikto found a login.php databases and config files.

![Alt text](./images/Nikto.PNG)


### 6.2 🛠️🔓 Brute Force Login Page

- **Module:** Brute Force  
- **Level:** Low-Impossible
- **Payload:** Dictionary Attack
- **Result:** Login Page accessed  
- **Mitigation:** Use stronger Password and implement strong password policies

#### 6.2.1 Hydra

i used hydra a bruteforcing tool to carry out a dictionary attack on the login.php to test for weak credentials if possible.

![Alt text](./images/Hydra.PNG)

weak creds were found via my dictionary attack and i gained access to the webpage via the login form.

![Alt text](./images/dvwa.PNG)


### 6.3 🧨 Command Injection

on the cloud i inputed commands like: 


```bash
google.com | pwd && whoami 
```
```bash
google.com | cat /etc/passwd
```
in similar fashion i accessed the systeminfo when i installed the DVWA on XAMP windows machine 

```bash
google.com | dir && systeminfo
```



![Alt text](./images/systeminfo.png)



### 6.4 🧨 SQL Injection

```bash
first i tested the login page for a potential sql error with just closing the  syntax | ' and this created the error seen below and this let me know there was an error shown and a possilbe potential for a code injection
```

![Alt text](./images/image.png)

```bash
In easy mode i ran ( 1' OR '1'='1)
```
![Alt text](./images/sqleasy.png)



i found the number of existing columns by just inputing numbers 1 and i saw the two colums name and surname but one can also find this by inputing ' ORDER BY 1 and change numbers until failure, and that tells how manys columns are there.




[Alt text](./images/sqlunion.png)

## 7. Tools Used

| Tool         | Purpose                          |
|--------------|----------------------------------|
| Burp Suite   | Proxy, request tampering         |
| OWASP ZAP    | Active vulnerability scanning    |
| Nikto        | Web server scanner               |
| curl         | HTTP request crafting            |
| Firefox DevTools | Input/output inspection      |



## 9. Recommendations

| Area              | Recommendation                                   |
|-------------------|--------------------------------------------------|
| Input Validation  | Sanitize and validate all user input server-side |
| Output Encoding   | Use HTML/JS escaping for outputs                 |
| File Handling     | Restrict file types, validate MIME types         |
| Authentication    | Implement rate limiting, strong password rules   |
| CSRF Protection   | Use CSRF tokens with same-site cookie flags      |
| Logging & Alerts  | Monitor unusual activity                         |



## 10. Conclusion

DVWA successfully demonstrated the impact of common web application vulnerabilities under various security levels. The hands-on testing reinforces best practices in secure coding, vulnerability mitigation, and the need for continuous security assessments in real-world applications.


