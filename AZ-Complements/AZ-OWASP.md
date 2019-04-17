
# AZ Complements - OWASP

## Main Resources

1. [Play by Play: OWASP Top 10 2017 by Troy Hunt](https://app.pluralsight.com/library/courses/play-by-play-owasp-top-ten-2017/table-of-contents)  

2. [Web Security and the OWASP Top 10: The Big Picture by Troy Hunt](https://app.pluralsight.com/library/courses/web-security-owasp-top10-big-picture/table-of-contents)  
3. [OWASP Top 10 Web Application Security Risks for ASP.NET by Troy Hunt](https://app.pluralsight.com/library/courses/owasp-top10-aspdotnet-application-security-risks/table-of-contents)  

## Related Resources

- [OWASP Top 10 - 2017 PDF](https://www.owasp.org/images/7/72/OWASP_Top_10-2017_%28en%29.pdf.pdf)  
- [What Is OWASP? What Are The OWASP Top 10?](https://www.cloudflare.com/learning/security/threats/owasp-top-10/)  
- [OWASP Top Ten Cheat Sheet](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet)  
- [OWASP Top Ten Cheat Sheet](https://azure.microsoft.com/en-us/blog/detecting-threats-with-azure-security-center/)  

## Complementary Resources

- [LulzSec](https://en.wikipedia.org/wiki/LulzSec)

---

#### Attack Vector  
A measure how hard is to fabricate the exploits which may depends on whether tools to assist in the design, deplyment and automation of the exploit exist.

#### Security Weakness 
A measure of the surface area available to the attack which in turn depends on two orthogonal factors.  

    1. Prevalence : a measure of the number of potential item exposed by an application which may become targets or doors for the exploit.

    2. Detectability: a measure of how difficult is for the attackers to dispover whether there exist entry points through with deliver their attack.

#### Technical Impact
How serious the consequences of a successful attack may be for the buisness, system or organization that falls victim of it.  

---

| Vulnerability   | Attack Vector        | Security Weaknesses                        | Technical Impact |
|-----------------| -------------------- | -------------------------------------------|------------------|
| (SQL) Injection | Exploitability Easy  | Prevalence Common - Detectability Average  | Severe           |
| Impersonation   | Exploitability Avg.  | Widespread - Average                       | Severe           |
|| `` | .||
|| `` | .||

---

## (SQL) Injection

### Typical Strategies to perform the attak

Strings manipulation and injection of query structure from query data.

### Typical Remedies

1. Whitelist untrusted data (expected data patterns or types).
2. Parameterization of statements by separation of the query structure from its data.
3. Restrict persmissions of the user to the minimum necessary inorder to achieve their purpose in each context. This is also known as **Principle of Least Priviledge.**

### References 

- [LulzSec](https://en.wikipedia.org/wiki/LulzSec)
- [Who or what is LulzSec?](https://www.youtube.com/watch?v=Esbk27dXxXc)  
- [The LulzSec hackers who boasted they were “Gods” await their sentence](https://nakedsecurity.sophos.com/2013/05/16/lulzsec-hackers-wait-sentence/)  

---

## Broken Authentication & Session Management (Impersonation Hijacking)

### Typical Strategies to perform the attak

1. **Retrieve secrets from the user PC (system)**    
This may be achieved through physical intrusion of malaware.
2. **Auth Cookie Theft**  
Typically achieved through sniffing over HTTP for example at an Internet Cafe or via Cross Site Scripting (XSS).
3. **Session ID Theft**  
This may happen when the system persist the session ID in the URL as it was in old ASP systems. It could also be logged to file by the web server and be available to whoever have access to the logs.
4. Exploitation of systems that employ **weak credentials**
5. Explotation of system that have a **weak policy on the number of failed logins** attemps before password recovery.
6. Explotation of **Weak Password Reset** 

### Typical Remedies

Normally the persistence of the authenticated state of a logged user relies on cookies thus is especially imprtant to make them secure.

1. **Use Cookies with HttpOnly flag**  
This flag on a cookie tells the Browser that 
2.

### References 

- []()

---
