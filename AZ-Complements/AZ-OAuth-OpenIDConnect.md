# AZ AZ-OAuth-OpenIDConnect

## Main Resources

1. [GOTO 2018 • Introduction to OAuth 2.0 and OpenID Connect • Philippe De Ryck](https://www.youtube.com/watch?v=GyCL8AJUhww)  

## Realted Resources

## Complementary Resources

- [Buffer - Save time managing social media for your business](https://buffer.com/)

---

### [Leaning Goals Introduction to OAuth 2.0 and OpenID Connect • Philippe De Ryck](https://www.youtube.com/watch?v=GyCL8AJUhww) 

- What OAuth is
- What OpenID Connect is
- What the main OAuth flows are and when to use each
- What the main OpenID Connect flows are and when to use each

---

### Main Subjects

The following discusses the **three main authorization and authentication flows and their uses cases**.

---
#### Summary  

1. Client Credential Grant
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



