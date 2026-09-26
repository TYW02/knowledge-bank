---
title: W5 Web Security
---

# Sessions
- Store user data across **multiple pages**
- Can be done **server** side or **client** side
- **Avoid** having to log in all the time
- Most sessions set a **key** on the user's computer

```php
<?php
session_start();
$_SESSION["uname"] = "Rose";
?>
```


# Cookies
- **Small text files** placed by the browser on your computer to monitor your **interaction** on a given website
- Webserver uses it to present you with **personalized** info when you next visit the website

## Web Security Preliminary Assessment

- **Explore** the web application (Vulnerabilities)
- Right click -> **View source** might be helpful
- "**Inspect**" in chrome 
- Javascript & HTML are executed **client side**
	- Inspect in chrome can be used to alter values in HTML & Javascript
- Web App Vulnerability Scanning tools



# OWASP Top 10 Web App Security Risk
1. SQL Injection
2. Broken Authentication & Session Management
3. Sensitive Data Exposure
4. XML External Entities
5. Broken Access Control (Unvalidated re-directs & forwards)
6. Security Misconfiguration
7. Cross Site Scripting (XSS), Cross Site Request Forgery
8. Insecure Serialization (Insecure Direct Object References)
9. Using Components with Known Vulnerabilities
10. Insufficient Logging and Monitoring

# SQL Injection
- Result from **untrusted data** from user being used as **part of a query**
- Data tricks the server (SQL interpreter) into **executing commands** or queries which it shouldn't
- **Access data** that the user does not have authorisation for

![[Pasted image 20260926212223.png]]

- Server side **script** takes a username & password from a **form**
- Connects to database
- Executes query **DIRECTLY** with username and password values from the form
- If username & password **match** then **re-direct** to another page

![[Pasted image 20260926212427.png]]


![[Pasted image 20260926212533.png]]


![[Pasted image 20260926212604.png]]


## Problem allowing `'`
- The use of `'` means the interpreter **switches context** (Control (command) <-> Data (Literal String))

> `'` => SQL opening / closing of chars

- **Sanitise** user input
	- **Escape characters** which result in a context switch
	- **Context is switched** from a string value to an SQL command and vice versa

![[Pasted image 20260926212921.png]]


![[Pasted image 20260926213022.png]]

![[Pasted image 20260926213030.png]]


## Escaping User Defined Input
- You can **escape characters** which could be **related to SQL injection**
- In PHP \ escapes the followed character 

```SQL
username = '\';DELETE FROM accounts\'");

// You can add another \ to escape the \
username = '\\';DELETE FROM accounts\'
```


# Avoiding SQL Injections


## Prepared Statements
- Uses variable binding (Parameterized queries)
- Defines the SQL and then the parameter are passed in later
- Parameter is indicated by `?`

```python
cursor.execute("INSERT INTO products (name, price) VALUES (?, ?)", ("bike", 10900))
```

![[Pasted image 20260926213543.png]]


## Stored Procedures
![[Pasted image 20260926214516.png]]

## Stored Procedures vs Prepared Statements
> Difference is that they are in the **SQL DB itself**, and then called from the DB application as opposed to in the **program** as with prepared statements

## Additional Defences (Restricted Access)

- SQL Views: **Restricts access** to data so users can only **access their info**
- Privileges: Granted by **schema owner** to restrict access to objects in schema
- Reduce user input: Date Picker

# Broken Authentication & Session Management
- Errors in **implementation**

## Weak or Default Credentials

### Password Spraying
> [!Definition]
> Attack technique that attempts to target a large number of usernames with a few known or commonly used passwords

- Usually target Single Sign-On (SSO) applications, cloud-based application, and email applications

## Defence

### Control Session Duration
- Keep session duration **as short as possible** without affecting the **user experience**
- Implement **idle** session **timeouts**

### Rotate & Invalidate Session IDs
- Changing the **session ID** after a certain **period** or after certain **critical operations**
- **Invalidate** them when they are **no longer needed**

### Multi-Factor Authentication
- Requires users to provide two or more **verification factors** to gain access to a resource

### Implement Brute-Force Protection
- **Limiting** the number of failed **login attempts**
- Introducing **time delays** after a certain number of failed attempts
- Using **CAPTCHAs** to prevent **automated attacks**


## Cross-Site Scripting (XSS

 > [!Definition]
 > Attackers **inject** client-side scripting into web pages of a site which are **shown** to other users
 > 
 > Those users **view** the website with the **malicious code**, which is **executed in their browser**

![[Pasted image 20260926215608.png]]

### Reflected or Non-Persistent XSS

- User click on link with **malicious scripts**
- Malicious script **bounces** off a website to **victim's browser**
- It may be passed via a query or URL, **payload is not stored**
- If attack via URL **webpage**, need some **social engineering** to trick victim to **click** or hover the mouse pointer over the link

### Stored or Persistent XSS

> [!Note]
> Stored means the malicious input is stored on the target server, database, message forum, blog, image, comment field

- Attacker identifies a forum as **vulnerable**
- Start new topic and **insert malicious scripts** in the topic title or body
- Malicious content of the forum post is **stored by the server**
- When **topic loads**, malicious content is sent to victim's browser & **payload executes**


### DOM-Based XSS
- Attacker crafts **malicious code** as part of a **search query** for a vulnerable website
- Victim is then tricked by attacker to **click on link** and **sends code to server**
- Server returns a **search page as response** and victim's browser executes legit script
- Adds html between the two \<div\> tags with the id "searchquery" (Mal code runs)


### XSS Malicious script examples
- Hijack user sessions: **Access cookies**, **session token**, other sensitive info retained by browser
- Deface website: Potentially **change HTML** and **deface website**
- Redirect user to **malicious** sites

## Defence
- Have HTML "Slots" where you can put **untrusted data**
- HTML **Escape** before inserting untrusted data into HTML element content
	- < replaced with &lt, > replaced with &gt
	- **Prevent** switching into any **execution** context, such as script, style, or event handlers
- User input **sanitization**: Within server-side input processing code

![[Pasted image 20260926223103.png]]


# Insecure Direct Object References (IDOR)

> [!Definition]
> Attackers can **access or modify** objects by manipulating identifiers (ID in a URL) used in a web application's **URL or parameters**. 
> 
> It occurs due to **missing access control checks**, which **fail to verify** whether a user should be allowed to access specific data

## IDOR Defence
- Check access for each object (Authorisation / Permissions)
- Use indirect object references
	- Associate user-specific tokens with internal non-sequential object references like database ID or file path

> [!Note]
> Every web-application should **validate ALL** untrusted inputs received with each HTTP(S) request.
> 
> The app should at least perform "**whitelist validation**" on each input. This means verifying that the **incoming value** meets the **applications expectations** for that input, such as

- Minimum or maximum **length**
- Minimum or maximum **bounds** (For numeric values)
- Acceptable characters
- Data Type 


# Security Misconfiguration
- Web-based system security setting can be **misconfigured** at many levels
- **Unnecessary** features are enabled or installed
- Misconfiguration includes issues like not keeping **software up to date**, not **patching vulnerabilities** which could be exploited
- Using **default** user accounts with **default** password
- Threat agents: External attackers as well as insiders

![[Pasted image 20260926224448.png]]

## Defence

- Run **scans** and **audits**
- Have **processes in place** for checking software is **up to date**
- Don't use default settings (Configure to your specific needs)
- After **validating** the supplied input, append the input to the **base directory** and use a platform filesystem API to **canonicalize the path**. Verify that the path starts with the expected base directory
- Apply **Principle Of Least Privilege**

# Sensitive Data Exposure
> [!Definition]
> It occurs when an application, company, or other entity inadvertently **exposes personal data** (eg. weak or no encryption, phishing attacks)

- Occurs as a result of **not adequately protecting** a database where information is stored

## Defence
- Encrypt data in **transport** and at **rest** via strong encryption **SSL/TLS**
- Store passwords with **salted hashes**
- Applying proper **access controls** to both **files** and **directories**
- Monitor account **access logs** for unusual activity
- **Disable** caching and **auto-complete** on forms that collect data 
- Employee training / awareness
- Web Vulnerability scanning


# Missing Function Level Access Control

> [!Definition]
> Occurs when requests for functionality are fulfilled **without checking** the user has authorisation


## Defence
- **Don't show** the user functions which they **should not** be able to access
- **Check access** to functionality before providing it
- Authorisation should be implemented for **all functionality**


# Cross Site Request Forgery (CSRF)
> [!Definition]
> Attack that tricks users to execute undesired actions on a web app in which they are currently authenticated

- Targets **state-changing requests**, not data theft because attacker **cannot see response** to forged request
- Utilises **social engineering** support

![[Pasted image 20260926230036.png]]

## Defence
- Include **unpredictable** "Challenge" **tokens** for each session
- **Sensitive operations**, include a challenge token **in the HTML forms and links** which execute sensitive server-side operations
- Hidden challenge token is then **sent to server** when user tries to perform that operation
- If CSRF attack is performed using malicious site, attacker needs to know the current token. Your server will not process a request without this token, so the attack fails.

![[Pasted image 20260926230325.png]]


## Challenge Token Generation
- Use a **less predictable**, well-established random number generator with enough **entropy**
- **Expire tokens** after a short amount of time so that they **cannot be reused**
- Use **safe ways** to **verify** whether the received token is the **same** as the set token (Compare hashes)

# Using Components with Known Vulnerabilities

> [!Definition]
> Vulnerabilities that were discovered in open-source components and published in the NVD, CVE, security advisories or issue trackers.
> 
> National Vulnerability Database
> Common Vulnerabilities and Exposures

- From the **moment of publication**, a vulnerability can be **exploited by hackers** who find the documentation
- Use of open-source components is widespread (Components may run with full privileges)

## Defence
- **Evaluate** a component's **vulnerability** before using it
- Keep components **up to date** (Patched)
- Maintain **complete** software component **inventory** (Origin, Version)
- Keep track of **attack surface baseline** of endpoints that components are installed on


# Unvalidated re-directs and forwards

- Web application may **redirect** and **forward** users to other pages and websites
- Problem **arises** when **untrusted data** is used to determine the **destination** (From a parameter passed into a URL)

![[Pasted image 20260926231043.png]]

![[Pasted image 20260926231025.png]]

## Defence
- **Avoid** re-direct and forwards
	- **Don't allow** URL as user input for the **destination**
		- Have a list of "**Trusted**" URLs
		- Have user **confirm** they are **leaving your site**
		- Simply avoid using redirects and forwards


# OWASP Security Risks Summary
1. It's a **standard awareness document** for developers and web application security
2. It represents a **broad consensus** about the **most critical security risks** to web applications
3. Provide **guidance** to developers and security professionals on the **most critical vulnerabilities** that are **commonly found** in web applications, which are also **easy to exploit**
4. **Globally recognized** by developers as the **first step** towards more secure coding
5. Companies can **adopt this document** and **start the process** of ensuring that their web applications **minimize these risks**


















































