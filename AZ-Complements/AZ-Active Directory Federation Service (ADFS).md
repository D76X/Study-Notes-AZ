### [What is Active Directory Federation Services (ADFS)](https://www.youtube.com/watch?v=xwWb7S6OvFI)  

- AFDS is an **integrated** **claim-based identity management solution**.
- Provides **SSO** for web applications.
- Send **claims** to a web application **on behalf of AD**.
- helps to **support web service interoperability** between vendors.

### The most common authentication mechanics used by ADFS - SAML 2.0

When a request at the URL of a reource or service is received it replies to the request (from the browser) with a **HTTP 302 URL redirection to the URL of the on-premise ADFS server**.

The **on-premise ADFS server**  receives the **authentication request** from the user's browser **for the cloud service or resource** the user tried to access. It then **authenticates** the user against the **on-premise AD Service** and replies to the uthentication request from the user's browser with **a set of claims for the authenticated user and the cloud resource that the user tried to access** all wrapped-up in a **cookie**.

Finally the user brower is redirected by the **ADFS HTTP 302 response** back to the same URL of the cloud resource or service it wanted to access in the first place but this time it is able to present its **identity and the claims for the requested cloud service or resource**.

### Credentials are never exposed to the cloud 

One of **the most important facts** to keep in mind about the mechanics of ADFS is that users who want or need to access resources or services made available in the cloud are **never** requested to provide any credentials to any part of the cloud infrastructure at the time they attempt to consume those services. **Users are authenticated entirely on premise and any username o passoword** inputted by users in their browser are aonly transmitted to the ADFS Server and then relayed to AD and are kept within the confine of the enterprise IT infrastructure.

### Attributes included in the claim

The **claim-based** cookie that is presented to the cloud resource at the end of the authentication process is **agreed in advance** between the cloud service and the ADFS Server. Claims might be a set of information tokes such as **Firstname, Lastname, email adress, department, etc.**. 

---
