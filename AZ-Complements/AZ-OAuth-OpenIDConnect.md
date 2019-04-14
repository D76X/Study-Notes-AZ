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
    - There is **no user involvement in this flow**
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

## Client Credential Grant Flow

This is the easiest of the OAuth Flows

- The client is a backend systemthat is some code on a server!
- The **is no access delegation in this specific flow** it is just **machine to machine communication**
- There is **no user involvement in this flow**
- Direct Access by the client application
- Access Token obtained using the client credential

1. The client presents the client application secrets to the AS
2. The AS returns an AT to the client
3. The client go to the RS and presents the AT
4. The RS authorizes the client by means of the access token
5. The RS returns the required resource to the client application

#### Scenario

---



