

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

Before browsers implemented **Single Origin Policy (SOP)**, malicious websites were able to exploit cookies stored by your browser to make unauthorized requests to other domains. Some of these unauthorized requests could do things like make purchases, delete user information, fetch sensitive data, etc. As an example, you might go to a banking website and provide some credentials to log into your account. Your username is stored in a secure browser cookie for a certain period of time so the bank can tell you are still logged in instead of having you login another time with each page you access. Later on, you go to an innocent-seeming webpage listing some facts about bunnies. Unbeknownst to you, the webpage’s HTML also has a little Javascript script to make an AJAX request (see: XMLHttpRequest) to the previous banking website to make a wire transaction to another account. Because your session is still authenticated with the cookie that was stored earlier, the banking website thinks it’s just you clicking on a link on their site to submit a wire transaction. The easy fix was for browsers to detect when a request is made from one website to another and prevent the response from being readable. This is the Same-Origin Policy.

---