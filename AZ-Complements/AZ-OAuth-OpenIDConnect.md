# AZ AZ-OAuth-OpenIDConnect

## Main Resources

1. [GOTO 2018 • Introduction to OAuth 2.0 and OpenID Connect • Philippe De Ryck](https://www.youtube.com/watch?v=GyCL8AJUhww)  

## Realted Resources

## Complementary Resources

- [Which OAuth 2.0 Grant should I use?
](https://auth0.com/docs/api-auth/which-oauth-flow-to-use)  
- [What is the purpose of the 'state' parameter in OAuth authorization request](https://stackoverflow.com/questions/26132066/what-is-the-purpose-of-the-state-parameter-in-oauth-authorization-request)  
- [Difference between a querystring and a fragment?](https://stackoverflow.com/questions/1956378/difference-between-a-querystring-and-a-fragment)  
- [OAuth2: query string vs. fragment](https://stackoverflow.com/questions/14707345/oauth2-query-string-vs-fragment)   
- [OAuth 2.0 Client Credentials Grant](https://oauth.net/2/grant-types/client-credentials/)  
- [Authorization Code Grant Flow](https://oauth.net/2/grant-types/authorization-code/)      
- [OAuth 2.0 Implicit Grant](https://oauth.net/2/grant-types/implicit/)  
- [How to implement the Implicit Grant](https://auth0.com/docs/api-auth/tutorials/implicit-grant)    

---

### [Leaning Goals Introduction to OAuth 2.0 and OpenID Connect • Philippe De Ryck](https://www.youtube.com/watch?v=GyCL8AJUhww) 

- What OAuth is
- Why we need OAuth
- What OpenID Connect is
- What the main OAuth flows are and when to use each
- What the main OpenID Connect flows are and when to use each

---

### Main Subjects

The following discusses the **three main authorization and authentication flows and their uses cases**. In order to fully understand the corresponding user cases it is neccessary to define the conncepts of Backend Application and  Frontend Application as the types of flow that can be employed to Authenticate and/or Authorize a user, application or device depends on this attributes.

#### Backend Application

A Backend Application is any application which can guarantee a way to store secrets securely. For example, the server-side code that runs an a server is a backend application as the OS that hosts the application provides ways to safely store cryptographic secrets, the same goes for a WPF application on a user Windows OS PC. Likewise he case of an application in the clould i.e. an AppService on Microsoft Azure or aother cloud infrastructure which can use means such as Azure Key Vault to safely store cryptographic secrets.

#### Frontend Application

A Frontend Application is any application which **cannot** guarantee a way to store secrets securely. For example, applications such SPA running i a browser or application on mobile devices do not have a way to to safely store cryptographic secrets on the device or the browser. 

---
#### Summary  

1. Client Credential Grant Flow
    - The client is a backend system that is some code on a server
    - The **is no access delegation in this specific flow** it is just **machine to machine communication** 
    - There is **no user involvement in this flow** everything happens in name of the client application
    - Direct Access by the client application
    - Access Token obtained using the client credential
    - Typically the backend application here needs only read-only access to public resources on some authoritation server that is information that is publiccly available which may or may not be related to some users but that are anyway publicly available anyway

2. [Authorization Code Grant Flow](https://oauth.net/2/grant-types/authorization-code/)  
    - User **Delegates access** to resources on thrird-party RSs but owned by them to a **Native Application**
    - **Access Token and Refresh Token obtained by exchanging** an **Authorization Token** 
    - **Refresh Token** can be used with **Client Credentials** to obtain a new **Access Token**
    - Can only be used with **Native Apps** where the **Client Application Secrets** can be stored securely and that have the right to open the browser on the user's system.  Notice tha a **AppService** which is a **backend application** counts as a **Native Application** as it has a way to securely store Client Secrets. 
    - This flow is typically used to delegate access to user-specifi, user-reserved information as read-only resources or to even delegate write access to user owned resources

3. [OAuth 2.0 Implicit Grant](https://oauth.net/2/grant-types/implicit/) 
    - **Delegated Access** to a **frontend application**
    - **Access Token directly obtained through redirection**
    - It **does not** have or need a **refresh token**

---

## The Concept of Delegation

The concept of **delegation is central to OAuth**. 

Let's consider a practical example to set the scene. You have developed an **application**  and one of its features is that it should be capable to post tweets on someone's Tweeter account. In order to accomplish this task something lihe [Buffer](https://buffer.com/) might be employed. 

**In order for Buffer to be able to post tweets on behalf of the user of the application it must have access to the users' Tweeter Profile**. 

The user can **delegate access to Buffer to access their Tweeter Profile on their behalf and be able to post tweets according to the user's preferences as set in the application**.

If you look at this from **the point of you of the user's Tweeter account** this must **grand access to the user's feed to a number of applications. One of these will be Buffer**.

### Summary

**OAuth** allow a **user** to grandt an **a client application (Buffer)** **access** to **a third-party resource which is controlled by the user** i.e. Tweeter account/profile of the user. 

---

### The parts of a Delegated Access Flow

1. The **Authorization Server (AS)**
2. The **Client Application (CA)**
3. The **Resource Server (RS)**
4. The **Access Token (AT)**

---

### The genaral Delegated Access Flow

1. The **CA** asks the **AS** to be **authorized access some protected reource on the RS on behalf of the user**
2. The **AS** responds to the **CA** with an **AT**  
3. The **CA** presents the **AT** to the **RS** to gain access to the resource it needs
4. The **RS** USES THE **at** to verify on the **AS** that the token is genuine and the **CA** is allowed to access the resource on it

### What is OAuth?

**OAuth** is a **specification** that provides the details of the communication between **AS and CA** in order to fulfill the first tow steps (1 & 2) described above that is up to the issuance of the **AT**. 

However, **all implememnations** will also include the details of the last two steps (3 & 4)

---

### Why we need OAuth

The advantage of OAuth become apparent when you think that **a single authorization server AS can issue Access Tokes to a large number of Client Application for a large number of Resource Servers**. OAuth provides a standard mechanism to achieve delegated access independent of the client application and the resource server.

---

### Registration of the Client Application with the Authorization Server

In order of the **AS** to be able to **authorize** a client application to access on behalf of the user of the client application a third-party resource which belongs to the user of the client application and that is resident on some resource server **the Client Application must first be registered with te Authorization Server**.

Normally the **AS** requires the following details at the time of teh registration.

1. The name of the Client Application
2. The URL of the domain under which your application is hosted (if it is a web application)
3. **The Callback URL** that is the **URL to which the client is redirected to in case of successful authorization**

### What the AS gives back to the CA after registration

After registration of the **CA** with the **AS** the latter provides the **CA** with the so called **Client Secrets** normally these are some subset of the folowing. The **CA** will later use this **secrets** to try to negotiate the issuance of an **AT to the RS** by the **AS**.

One **very important note** here is that **client secrets should be protected** that is it is **responsibility of the Client Application** to make usre that these secrets are stored safely and cannot be stolen.

#### Sore the Client Secret Securely!

In the relm of **Azure** you can use **Azure Key Vault** to store client secrets and **keep them away from web.config or app.configor worse the source code where they might inadvertently be cheked in source control or even downloaded from a server**.

#### Typical set of Client Secrets

1. Client Access Token to the AS
2. Client Secrets
3. Consumer API Key(s)

---

### The Authorization Server of OAuth

The **Autorizan Server** might be any server that **implements the OAuth Flow** for example **Google, Tweeter or Facebook** all have such **ASs** and these organizations provide some web application to let **designers of Client Application register their application with the AS** and hence **obtain the client secrets**. It is important to note that **the client secrets identify the client application to the AS and not the user of teh application**.

In **enterprise environment** the Authorization Server might be something like **Active Directory or Azure AD**. In this cases the public facing application where developer register the application with the AS might be replaced by an admin that does the same on the AD or Azure AD Server.

The registration and the client secrets allow **the user of the application** to use the application and reach the AS to which the client application passes the secrets. However, this step only authenticate the application on the AS the user will have to be provided with some means to authorize **the application to access some thrid-party resource owned by them on their behalf**.

---

### Scenario 1 - Machine to Machine

A web site wants to show a number of tweeter feeds on the website. In this case the client application is the website thus there is no real user and the resource is the tweeter api. There is no actual user involved. The application only need to be registered with the tweeter api and get the secrets and then use those to get an access token to be able to access the resources exposed by teh tweeter api.

### Client Credential Grant Flow

This is the easiest of the OAuth Flows

- The client is a backend systemthat is some code on a server!
- The **is no access delegation in this specific flow** it is just **machine to machine communication**
- There is **no user involvement in this flow** everything happens in name of the client application
- Direct Access by the client application
- Access Token obtained using the client credential
- Typically the backend application here needs only read-only access to public resources on some authoritation server that is information that is publiccly available which may or may not be related to some users but that are anyway publicly available anyway

#### The nodes

1. The Client Application
2. The Authorization Sever
3. The Resource Server

#### The flow 

1. The client presents the client application secrets to the AS
2. The AS returns an AT to the client
3. The client go to the RS and presents the AT
4. The RS authorizes the client by means of the access token
5. The RS returns the required resource to the client application

---

### Scenario 2 - Native App (Backend App) on behalf of the user

In this scenario an application offers a feature such that the user of the application can schedule tweets to be posted on his tweeter account with a selected schedule. In this case the user must delegate access to his or her tweeter profile to the application. In this case there **must be a way for the ... of asking the user to authorize the application to post tweets on their account**. 

### Autorization Code Grant Flow 

This is **the most secure OAuth flow and the only one for which it is possible to issue a refresh token in addition to the access token**. 

- User **Delegates access** to resources on thrird-party RSs but owned by them to a **Native Application**
- **Access Token and Refresh Token obtained by exchanging** an **Authorization Token** 
- **Refresh Token** can be used with **Client Credentials** to obtain a new **Access Token**
- Can only be used with **Native Apps** where the **Client Application Secrets** can be stored securely and that have the right to open the browser on the user's system. Notice tha a **AppService** which is a **backend application** counts as a **Native Application** as it has a way to securely store Client Secrets. 
 - This flow is typically used to delegate access to user-specifi, user-reserved information as read-only resources or to even delegate write access to user owned resources

#### The nodes

1. The User
2. The Browser
3. The Client Application
4. The Authorization Sever
5. The Resource Server

#### The flow 

0. The Client Application does not have an access token to access the rsource on beahlf of the user
1. The Client Application opens a the default Browser on the User's system to reach the Authorization Server at its URL
2. The AS (i.e. Azure AD, ADFS or Tweeter's AS) redirect the browser thus the user to a log-inpage in order to **authenticate the user with the AS**.
3. The User authenticates on the AS
4. The AS redirects the user in the browser to a page where they are asked whether they wish to grant the Client Application access their protected resource on their bahalf that is **AS asks the user whether they wish to delegate the CA to access the user resource**
5. The user **delegates** the **Client Application**
6. The **AS** issues an **Autorization Tonen** to the **Client Application** by **redirecting the browser to the registered redireted URI**
7. The **Authorization Token** does not grant any access and must be **exchanged** by the Client Application with a **Access Token** by presenting the **Authorization Token** to the **AS** **together with the Client Application Secrets**. The **AS** checks that the provided **Authorization Token & Cleint Secrets are genuine and still valid** and returns to the Client Application an **Access Token & Refresh Token**.
8. Finally with the **Access Token** the application can now access the resource on the RS i.e. the Tweeter Api.

#### The most important steps in this flow are 6 & 7

**Step 6 is crucial for the security of this flow** the **AS** can redirect the Browser on the user machine **only to the URI that the Client Application has previously registered with it**. This makes it impossible for the **Access Token** to be send to any unregistered application i.e. the URI of an attacker. The client application has started the whole process but up to step 6 the Authorization Server knows nothing about the Client Application involvement it has only interacted with the user through the brower and let them **delegate** access to some of their resources on some resource server. In aknowlegment of this the AS has issued a **Authorization Token** that will only be sent to the **registered URL**.

Also the **Authorization code** is only valid for **1-time used and very short-lived i.e. under a minute**.

#### The role of the Refresh Token

While the **Authorization Token** is short lived the **Refresh Token** is long lived i.e. months or even years. In this flow the user goes through the **Authentication** on the **AS** and clearly we want this to happen only occasionally for usability reasons. Without a **Refresh Token** on the expiration of the **Authorization Token** the **Authentication of teh user** and the **delegation** would have to be rpeated. Howver, with the **Refresh Token** the **Client Application** acquires the right to **requiest a new short-lived Access Token** in order to access the resources to which the user has agreed **delegated access**. Howver, in order to obtain a new **Access Token** it must present to the **AS** the following

- Refresh Token
- The Client Application Secrets

Only if both are presented and still valid the AS issues

- A new Access Token
- A new Refresh Token

This mechanism makes sure that **in those cases in which an Access Token has been compromised (stolen) it cannot be used by attackrs for long period of time thus limiting the liability**. Howeverm this **security feature** relies on the **Client Secrets to be stored securely by the Client Application** as even the Refresh Token could beleaked but it would be worthless without the cleint secrets.

This is also why **this flow is not suitable for application that runs in a broweser** as a Browser does not make it possible to safely store the Client Application Secrets. It is only used with **Native Applications** that is applications that runs on a Operation System.

### Request example

#### Simple Request For The Autorization Code Grant Flow
```
https://twitter.example.com/auth
    ?response_type=code  
    &client_id=MyCrazuApp  
    &scope=read write  
    &redirect_uri=https://mydomain/..../mycallback.asp
    &state=65976ushdaD
```

The **?response_type=code** is the bit that specifies that the Client Application wants to enage in this flow **(Autorization Code Grant Flow )**. 

The `&state=65976ushdaD` prevents certain attacks. More information on the meaning of this query parameter is available at the following resource - [What is the purpose of the 'state' parameter in OAuth authorization request](https://stackoverflow.com/questions/26132066/what-is-the-purpose-of-the-state-parameter-in-oauth-authorization-request).

### Simple Response For The Autorization Code Grant Flow

```
https://mydomain/..../mycallback.asp
    ?code=735nnwrj804nm    
    &state=65976ushdaD
```

`code=735nnwrj804nm ` is the **Authorization Code** to be exchanged.

### Simple Request of the Client Server to Exchange the Authorization Token with an Acess Token - Server to Server

```
POST /auth
Authorization: Basic fhf09r4ekls;dk
Host: twitter.example.com

    grant_type=authorization_code
    &redirect_uri=https//mydomain...../twittercallback.asp
    &client_id=MyCrazuApp 
    ?code=735nnwrj804nm     
```

`Basic fhf09r4ekls;dk` transmitts the **Client Credentials (Secrets)**
`?code=735nnwrj804nm` is the **Authorization Code to be exchanged for an Access Token**.

### The Exchange Response - Server to Server

```
{
    "access_token": "j48508rfivnt80895fdj",
    "expires_in": 300,
    "token_type": "bearer",
    "refresh_token": "768jnfdp842809nmfsl"
}
```

The **Backend Application** can now **securely store the response** for example on the hard drive of the OS or in Azure Key Vault and make use of `access_token` and `refresh_token` **repetedly** that is as long as a refresh token is available to regenerate a new access token.

---

### Scenario 3 - Frontend App (i.e JavaScript or SPA) on behalf of the user

In scenario 2 it could be relied on the fact that the client application secrets can be stored safely on a backend for example

- A WPF application on the User OS
- A iOS app
- An AppService which hosts a stateless ASP.Net Core site

However, think of the scenario in which the application runs as a SPA in the user's browser. **The user's browser is not a safe place to store the client application credentials** thus **the Autorization Code Grant Flow cannot be employed**. Still we would like the user of this app to be able for example to post tweets to their tweet account directly from this SPA which means that the user needs some means to **delegate** the authorization to write tweets to their accounts to the application **without the need to hold client secrets in the app,the browser or the device**. 

A SPA running in a web browser can in principle provide the same functionality as those available to users of a web site. However, while user of a web site use the backend code running on the server to access third-party resources which are then sent back to the user's browser by the server (Autorization Code Grant Flow) in the case of the API there is no such server and the communication is carried out directly by the client code in teh browser with the servers and APIs olding the resources the application needs to interact with.

### Implicit Grant Flow
    
- **Delegated Access** to a **frontend application** 
- **Access Token directly obtained through redirection** that is there is no exchange of client secrets for an access token
- It **does not** have or need a **refresh token**

#### The nodes

1. The User
2. The Client Application
3. The Authorization Sever
4. The Resource Server

#### The flow 

1. Client (i.e. SPA) requests access to the Authorization Server i.e. through httService
2. The AS redirects the user browser to the authentication page of fro the resource the SPA wants to gain access to
3. The user authenticates on the **Authorization Server** i.e. the Tweeter Authorization Server or Azure AD in an enterprise
4. The AS asks the user whether they want to **delegate access to the protected resources to the client application that is the SPA**
5. The AS **redirects the browser to the application redirect URI that was registered with it and in the redirect URI it provides the Access Token directly** that is **there is no Authorization Token to echange as in the Autorization Code Grant Flow** 
6. The client can now use the **Acess Token** to access the resource on the Resource Server
7. The Resource Token returns the resource if requested

---

#### Request for an Access Token in the Implicit Grant Flow

```
https://twitter.example.com/auth
    ?response_type=token  
    &client_id=MyCrazuApp  
    &scope=read write  
    &redirect_uri=https://mydomain/..../mycallback.asp
    &state=65976ushdaD
```

The **?response_type=token** is the bit that specifies that the Client Application wants to enage in this flow **(Implicit Grant Flow)**. 

The `&state=65976ushdaD` prevents certain attacks. More information on the meaning of this query parameter is available at the following resource - [What is the purpose of the 'state' parameter in OAuth authorization request](https://stackoverflow.com/questions/26132066/what-is-the-purpose-of-the-state-parameter-in-oauth-authorization-request).

#### Response with an Access Token in the Implicit Grant Flow

```
http://mydomain/mytwittercallback.apsx
 #access_token=j48508rfivnt80895fdj
 &token_type=bearer
 &expires_in=300
 &state=65976ushdaD
```

---

## Difference between the Authorization Code Grant Flow & The Implicit Grant Flow

In the response **the most important fact to notice** is the `#` that precedes the `access_token=j48508rfivnt80895fdj`. This is a **big difference** with respect the **Autorization Code Grant Flow**. The `#` defines a `URI fragment` which is **never sent to the server as a Queery Parameter**.  

For security, the token response is provided as a hash (#) fragment on the URL. It prevents the token from being passed to the server or to any other servers in referral headers. 

More about this specific fact can be learned at the following resource.

- [OAuth2: query string vs. fragment](https://stackoverflow.com/questions/14707345/oauth2-query-string-vs-fragment)

Note that  the `#` prevents any redirect. Once the response is back to teh client application (Frontend Application) its code reads the `access_token` and uses it to **access the resourcethe application needs a single time**. This means taht the application will have to obtain a new access token in order access any other resource or the same resorce after a short time (in this case 300 seconds). **Storing the access token on the device or the application memory or the browser will have no use after the access token expires**. This is very different from the way the Authorization Code Grant Flow works.

---



