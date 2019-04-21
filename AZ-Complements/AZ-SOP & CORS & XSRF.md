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

#### [Cross Origin Resource Sharing (CORS)](https://www.codecademy.com/articles/what-is-cors)   

---

### WHY IS CORS NECESSARY?

The CORS standard is needed because it allows servers to specify not just **who** can access its assets, but also **how** the assets can be accessed. With CORS, a server can specify **who** can access its assets and **which HTTP** request methods are allowed from external resources.

Most servers will allow GET requests, meaning they will allow resources from external origins (say, a web page) to read their assets. HTTP requests methods like PATCH, PUT, or DELETE, however, may be denied to prevent malicious behavior.

---

### HOW DOES CORS MANAGE REQUESTS FROM EXTERNAL RESOURCES?

An HTTP header is a piece of information associated with a request or a response passed back and forth between your web browser (cleint) and a server. The CORS standard manages cross-origin requests by adding **CORS HTTP headers** to the standard list of headers. 

- Access-Control-Allow-Origin
- Access-Control-Allow-Credentials
- Access-Control-Allow-Headers
- Access-Control-Allow-Methods
- Access-Control-Expose-Headers
- Access-Control-Max-Age
- Access-Control-Request-Headers
- Access-Control-Request-Method
- Origin

#### Access-Control-Allow-Origin

The **Access-Control-Allow-Origin** header allows **servers** to specify how their resources are shared with external domains. CORS allows servers to specify certain trusted ‘origins’ they are willing to permit requests from. 

Origins are defined as the combination of protocol (http or https), host (a domain like www.example.com or an IP address) and port. 

To instruct the browser to expose server responses to a HTTP requests from certain origin, the web server **must** respond to the request with an additional HTTP response header, ‘Access-Control-Allow-Origin: <origin>’. 

When a GET request is made to access a resource on Server A, Server A will respond with a value for the Access-Control-Allow-Origin header. Many times, this value will be *, meaning that Server A will share the requested resources with any domain on the Internet. Other times, the value of this header may be set to a particular domain (or list of domains), meaning that Server A will share its resources with that specific domain (or list of domains).

---

#### PRE-FLIGHT REQUESTS  

As mentioned before, most servers will allow GET requests but may block requests to modify resources on the server. Servers don’t just blindly block such requests though; they have a process in place that first checks and then communicates to the client (your web browser) which requests are allowed.

The preflight request is an OPTIONS request made to the same HTTP path as the actual request, with a couple of HTTP headers.

- `Origin` — The origin header that would be included with the actual request being made by the website.
- `Access-Control-Request-Method` — The method of the actual request being made by the website.
- `Access-Control-Request-Headers` — A comma-separated list of headers that would be included in the actual request.

Web servers that wish to support CORS requests must respond to preflight requests with the following HTTP headers:

- `Access-Control-Allow-Origin` — The whitelisted origin, or ‘*’
- `Access-Control-Allow-Methods` — A comma-separated list of HTTP methods the web server wishes to permit for cross-origin requests
- `Access-Control-Allow-Headers` — A comma-separated list of HTTP headers the web server wishes to permit for cross-origin requests

If any of the information in the response headers does not match the actual parameters of the request, the browser will not send the actual request.

When a request is made using any of the following HTTP request methods,a standard preflight request will be made before the original request.
Preflight requests use the OPTIONS header. The preflight request is sent before the original request, hence the term “preflight.” The purpose of the preflight request is to determine whether or not the original request is safe (for example, a DELETE request). The server will respond to the preflight request and indicate whether or not the original request is safe. If the server specifies that the original request is safe, it will allow the original request. Otherwise, it will block the original request.

- PUT
- DELETE
- CONNECT
- OPTIONS
- TRACE
- PATCH

---

#### [WHY HAVE CORS and SOP BEEN INTRODUCED?](https://medium.com/@electra_chong/what-is-cors-what-is-it-used-for-308cafa4df1a)  

**The Cross-Origin Resource Sharing** policy was introduce to **prevent cross-site request forgery (CSRF or XSRF)**.

Before browsers implemented **Single Origin Policy (SOP)**, malicious websites were able to exploit cookies stored by your browser to make **authorized** requests to other domains if **authorization cookies fir that web sites were found in the user broweser**. 

Some of these requests could do things like make purchases, delete user information, fetch sensitive data, etc. This class of attacs is called **Cross Site Request Forgery (XSRF/CSRF)**. 

---

#### An Example of XSRF/CSRF

You might go to a banking website and provide some credentials to log into your account. Your **credenitals is stored in a secure browser cookie i.e. a session cookies** for a certain period of time so the bank can tell you are still logged in instead of having you login another time with each page you access. 

Later on, you go to an innocent-seeming webpage listing some facts about bunnies. Unbeknownst to you, the webpage’s HTML also has a little Javascript script to make an AJAX request (see: XMLHttpRequest) to the previous banking website to make a wire transaction to another account **POST/PUT** or retrive bank accountdetails **GET** that can ultimately then be sent to the attacker's domain. 

Because your session is still authenticated with the cookie that was stored earlier, the banking website thinks it’s just you clicking on a link on their site to submit a wire transaction. 

---

### The Essence of Same-Origin Policy & CORS

**The easy fix for GET requests** is for browsers to detect when a request is made from one origin to another and **prevent the response from being readable by teh browser if teh origins do not match of the server does not list the calling page domain as a whitelisted domain**.

**In the cases of PUT/POST requests** it is the **Preflight** mechanism implemented in the broswers that prevents transactions to be made by the attackes in their favour at the back of an authenticated user. **The answer to the preflight request tha tprecedes the actual PUT/POST** will of course always deny the domain of the attacker from issuing the POST/PUT request **from a legittimate browser**. 

---