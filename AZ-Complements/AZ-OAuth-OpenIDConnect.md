# AZ AZ-OAuth-OpenIDConnect

## Main Resources

1. [GOTO 2018 • Introduction to OAuth 2.0 and OpenID Connect • Philippe De Ryck](https://www.youtube.com/watch?v=GyCL8AJUhww)  

## Realted Resources

## Complementary Resources

- [Buffer - Save time managing social media for your business](https://buffer.com/)

---

### [Leaning Goals Introduction to OAuth 2.0 and OpenID Connect • Philippe De Ryck](https://www.youtube.com/watch?v=GyCL8AJUhww) 

- What OAuth is
- Why we need OAuth
- What OpenID Connect is
- What the main OAuth flows are and when to use each
- What the main OpenID Connect flows are and when to use each

---

### Main Subjects

The following discusses the **three main authorization and authentication flows and their uses cases**.

---
#### Summary  

1. Client Credential Grant
    - The client is a backend systemthat is some code on a server!
    - The **is no access delegation in this specific flow** it is just **machine to machine communication** 
    - There is **no user involvement in this flow** everything happens in name of the client application
    - Direct Access by the client application
    - Access Token obtained using the client credential

2. Autorization Code Grant 
    - **Delegated access** to a **ackend application**
    - **Access Token** obtained by **exchanging** a **client code** with **client credentials**
    - **Refresh Token** can be used with **Client Credentials**

3. Implicit Grant
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

#### Scenario 1 - Machine to Machine

A web site wants to show a number of tweeter feeds on the website. In this case the client application is the website thus there is no real user and the resource is the tweeter api. There is no actual user involved. The application only need to be registered with the tweeter api and get the secrets and then use those to get an access token to be able to access the resources exposed by teh tweeter api.

## Client Credential Grant Flow

This is the easiest of the OAuth Flows

- The client is a backend systemthat is some code on a server!
- The **is no access delegation in this specific flow** it is just **machine to machine communication**
- There is **no user involvement in this flow** everything happens in name of the client application
- Direct Access by the client application
- Access Token obtained using the client credential

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

#### Scenario 2 - Operation on bahalf of the user

In this scenario an application offers a feature such that the user of the application can schedule tweets to be posted on his tweeter account with a selected schedule. In this case the user must delegate access to his or her tweeter profile to the application. In this case there **must be a way for the ... of asking the user to authorize the application to post tweets on their account**. 

2. Autorization Code Grant Flow 

This is **the most secure OAuth flow and the only one for which it is possible to issue a refresh token in addition to the access token**. 

- **Delegated access** to a **ackend application**
- **Access Token and Refresh Token obtained by exchanging** an **Authorization Token** 
- **Refresh Token** can be used with **Client Credentials**

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

---



