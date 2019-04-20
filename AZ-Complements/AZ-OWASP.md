
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
- [Use Cookies with HttpOnly flag](https://www.owasp.org/index.php/HttpOnly)  
- [**Use Cookies with Secure flag**](https://www.owasp.org/index.php/SecureFlag)   
- [Broken Authentication and Session Management](https://www.owasp.org/index.php/Broken_Authentication_and_Session_Management)
- [The problem with OAuth for Authentication](http://www.thread-safe.com/2012/01/problem-with-oauth-for-authentication.html)  
- [XSS Payload List - Cross Site Scripting Vulnerability Payload List](https://www.kitploit.com/2018/05/xss-payload-list-cross-site-scripting.html)  
- [XSS Tutorial #1 - What is Cross Site Scripting?](https://www.youtube.com/watch?v=M_nIIcKTxGk)  
- [How does CORS prevent XSS?](https://security.stackexchange.com/questions/108835/how-does-cors-prevent-xss)  
- [Same origin Policy and CORS (Cross-origin resource sharing)](https://stackoverflow.com/questions/14681292/same-origin-policy-and-cors-cross-origin-resource-sharing)  
- [Single Origine Policy (SOP)](https://en.wikipedia.org/wiki/Same-origin_policy) 


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
| XSS             | Exploitability Avg.  | Very Widespread - Easy                     | Moderate         |
||||
||||

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

Normally the **persistence of the authenticated state of a logged user relies on cookies** thus is especially imprtant to **make them secure**.

1. [**Use Cookies with HttpOnly flag**](https://www.owasp.org/index.php/HttpOnly)     
This flag on a cookie **makes it immune to a Criss Site Scripting (XSS) attack** tells the Browser that the cookie cannot be accessed through client side script As a result, even if a cross-site scripting (XSS) flaw exists, and a user accidentally accesses a link that exploits this flaw, the browser (primarily Internet Explorer) will not reveal the cookie to a third party.
2. [**Use Cookies with Secure flag**](https://www.owasp.org/index.php/SecureFlag)  
When a Cookie is set with this flag can only be sent over SSL (HTTPS). For example, the Cookie cannot be sent when the user is logged on a public wireless network in a Cafe. This prevents the Cookie and so the session secrects to be hijacked by network traffic sniffer, monitors or proxies.
3. **Decrease the Window Risk**  
By setting a suffiently short time window before the authenication credentials stored in a cookie expires it is possible to decrese the likelyhood that a hijacked cookies may be used to perform an impersonation. The expiration window should be a balanced compromise between security and usability in order not to force the user to repeat their logins too offen.  
4. **Hardening of the Account Management**    
This implies employing **strong password policy, frequent password update, no-reuse password, log-out strategies after failed login attempts**. 

### References 

- [Broken Authentication and Session Management](https://www.owasp.org/index.php/Broken_Authentication_and_Session_Management)
- [The problem with OAuth for Authentication](http://www.thread-safe.com/2012/01/problem-with-oauth-for-authentication.html)  

---

## [Important Security Concepts](https://security.stackexchange.com/questions/108835/how-does-cors-prevent-xss) 

### [Single Origine Policy (SOP)](https://en.wikipedia.org/wiki/Same-origin_policy)  

**Single Origine Policy (SOP) aka the same-origin policy** is a security mechanism **implemented in Web Browsers**. The policy permits scripts contained in a web page to access data only if obtained from the same **origin** the web page comes from. **An origin is defined as a combination of URI scheme, host name, and port number**. **This policy prevents a malicious script on one page from obtaining access to sensitive data on another web page**. 

It is very important to remember that the **same-origin policy applies only to scripts**. This means that resources such as **images, CSS, and dynamically-loaded scripts**, can be accessed across origins via the corresponding HTML tags.

### Security Applications of SOP

**The same-origin policy helps protect sites that use authenticated sessions**. The following example illustrates a potential security risk that could arise without the same-origin policy. Assume that a user is visiting a banking website and doesn't log out. Then, the user goes to another site that has some malicious JavaScript code running in the background that requests data from the banking site. Because the user is still logged in on the banking site, the malicious code could do anything the user could do on the banking site. For example, it could get a list of the user's last transactions, create a new transaction, etc. This is because the browser can send and receive session cookies to the banking site based on the domain of the banking site. **The user visiting the malicious site would expect that the site he or she is visiting has no access to the banking session cookie. While it is true that the JavaScript has no direct access to the banking session cookie, it could still send and receive requests to the banking site with the banking site's session cookie. The script can essentially do the same as the user would**. 

However, when the browser implements SOP then any script may still use the authentication cookies for another origin to query for data however....

---

## [Cross Origin Resource Sharing (CORS) - Relaxing the same-origin policy](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) 

In some circumstances, the same-origin policy is too restrictive, posing problems for large websites that use multiple subdomains. Cross-origin resource sharing (CORS) is a mechanism that allows restricted resources on a web page to be requested from another domain outside the domain from which the first resource was served. A web page may freely embed cross-origin images, stylesheets, scripts, iframes, and videos.  Certain "cross-domain" requests, notably Ajax requests, are forbidden by default by the same-origin security policy.

**CORS defines a way in which a browser and server can interact to determine whether or not it is safe to allow the cross-origin request**.

The CORS standard describes new **HTTP headers** which **provide browsers a way to request remote URLs** only when they have permission. **Although some validation and authorization can be performed by the server, it is generally the browser's responsibility to support these headers and honor the restrictions they impose**.  

### [Request Preflight Specification](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)  

**For Ajax and HTTP request methods that can modify data** (usually HTTP methods **other than** GET, or for POST usage with certain MIME types), **the specification mandates** that browsers **preflight the request**, soliciting supported methods from the server with an **HTTP OPTIONS request** method, and then, upon **approval from the server**, sending the **actual request** with the actual HTTP request method. Servers can also notify clients whether credentials (including Cookies and HTTP Authentication data) should be sent with requests.

### [Simple example of CORS](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)  

Suppose a user visits http://www.example.com and the page attempts a cross-origin request to fetch the user's data from http://service.example.com. A CORS-compatible browser will attempt to make a cross-origin request to service.example.com as follows.

1. The browser sends the OPTIONS request with an Origin HTTP header to service.example.com containing the domain that served the parent page:

```
Origin: http://www.example.com
```

2. The server at service.example.com may respond with

```
Access-Control-Allow-Origin: http://www.example.com
```

3. Since www.example.com matches the parent page, the browser then performs the cross-origin request. Otherwise it shows a error page if the server does not allow a cross-origin request.

### [Simple Example of Preflight Request](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)   

When performing certain types of **cross-domain Ajax requests i.e. HTTP request methods that can modify data**, modern browsers that support CORS will insert an extra "preflight" request to determine whether they have permission to perform the action.

```
OPTIONS /
Host: service.example.com
Origin: http://www.example.com
```

If service.example.com is willing to accept the action, it may respond with the following headers

```
Access-Control-Allow-Origin: http://www.example.com
Access-Control-Allow-Methods: PUT, DELETE
```
---

### CORS and XSS

**[CORS is unrelated to XSS](https://security.stackexchange.com/questions/108835/how-does-cors-prevent-xss)** because any attacker who can place an evil piece of JavaScript into a website can also set up a server that sends correct CORS headers. **CORS cannot prevent malicious JavaScript from sending session ids and permlogin cookies back to the attacker's domain**. if a person with malicious intent injects some JavaScript into a page to steal users' cookies and send them to a URL **he controls**, all he has to do is add the following header on the server side to make the request work.

```
Access-Control-Allow-Origin: *
```
---
## Cross Site Scripting (XSS)

This attack is based on the attacker providing the victim with some JavaScript which is dubbed **XSS Payload**. For example a link on a web page may have a URL with a XSS Payload.  

When the link is cliked **the browser** navigates to the **target web site**. The website that receives the request returns a resource to the browser that has requested it. This is usually described as **the server reflects back to the user the XSS Payload**. The recepient Browser **executes the XSS Payload which when properly crafted may be able to send back to the attacker the information resident in the user's browser such as their session cookies**. At this point the attacker may hold valid authentication cookies for the web site the user was originally directed to which might have been their trusted Bank's website. If the user was logged in on their Bank's website prior to clicking on the crafted URL with XSS Payload then the attacker holds a valid authorization cookie for this user and may be able to impersonate them.

There are many ways in which an attacker may be able to append a XSS Payload to a legitimate URL.

1. Crafting URI links that have the **XSS Payload in the query parameters**.
2. **By a successful SQL Injection on the DB of a site** so that one or more links on one or more pages of the websites whose URL are dynamically produced permanently contains the XSS Payload.  

### Typical Strategies to perform the attack  

### A Simple Example

```
http://www.mysite.com/Search?q=Lager
You searched for <strong>Lager</strong>
```

```
http://www.mysite.com/Search?q=<script>alert(document.cookies)</script>
You searched for <strong><script>alert(document.cookies)</script></strong>
```

### Typical Remedies  

1. **Always validate untrasted data** by using a **whitelist of trusted values and trusted patterns**.
2. **Always encode the output** that is prevent anything like `<script>..</script>` to be allowed as part of the HTML document. When any dynamic content is provided to a web page the server must enocode it i.e. `< and >` as `&lth; and &gth;` and the same goes for other special characters so that the browser will print them as characters. This guideline is also know as **never reflect to the browser untrusted data that has come with the request i.e. within its query string and data that comes from the database**. On this last point it must be kept in mind that the database might have already been targeted by SQL injection and contain malicious script content thus it cannot be trusted and the data returned by it must be encoded too before reaching the DOM. 
3. Use encoding libraries do not try to do the encoding yourself.

### References 

- [XSS Payload List - Cross Site Scripting Vulnerability Payload List](https://www.kitploit.com/2018/05/xss-payload-list-cross-site-scripting.html)
- [How does CORS prevent XSS?](https://security.stackexchange.com/questions/108835/how-does-cors-prevent-xss) 
- [XSS Tutorial #1 - What is Cross Site Scripting?](https://www.youtube.com/watch?v=M_nIIcKTxGk)  
- [Same origin Policy and CORS (Cross-origin resource sharing)](https://stackoverflow.com/questions/14681292/same-origin-policy-and-cors-cross-origin-resource-sharing)

---

## Cross SiteRequest Forgery (CSRF)

### Typical Strategies to perform the attack  

### Typical Remedies

### References 


---

## Insecure Direct Object References

### Typical Strategies to perform the attack  

### Typical Remedies

### References 

---

## Security Misconfiguration

### Typical Strategies to perform the attack  

### Typical Remedies

### References 

---

## Sensitive Data Exposure

### Typical Strategies to perform the attack  

### Typical Remedies

### References 

---

## Missinf Functional Level Access Control

### Typical Strategies to perform the attack  

### Typical Remedies

### References 

---
