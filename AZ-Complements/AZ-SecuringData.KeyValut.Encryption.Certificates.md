# AZ Complements - KeyVault

## Main Resources

1. [Microsoft Azure Developer: Securing Data by by Reza Salehi](https://app.pluralsight.com/library/courses/microsoft-azure-data-securing/table-of-contents)
2. [Securing Virtual Machines with Azure Key Vault by Gary Grudzinskas](https://app.pluralsight.com/library/courses/securing-virtual-machines-azure-key-vault/table-of-contents)  


## Realted Resources

## Complementary Resources

- [Protecting Encryption Keys with Azure Key Vault - Stephen Haunts](https://www.youtube.com/watch?v=WIgUmnwKdas)  
- [Understanding Hardware Security Modules (HSMs)](https://www.cryptomathic.com/news-events/blog/understanding-hardware-security-modules-hsms)  

---

### [Leaning Goals for Microsoft Azure Developer: Securing Data by by Reza Salehi](https://app.pluralsight.com/player?course=securing-virtual-machines-azure-key-vault&author=gary-grudzinskas&name=securing-virtual-machines-azure-key-vault-m0&clip=0&mode=live) 

- How to avoid exposing secrets stored in configuration files such as **web.config or app.config**.
- How to prevent **secrets to be hard coded and checked in to repos**
- Encryption of SQL databases by defaul with the **Azure SQL Always Encrypted** feature to avoid exposing plain data to anyone outside of the application that is designated to consume such data.
- Encryption of SQL databases with a private key securely storedin KeyValut
- How to secure HTTP communication with SSL/TSL.
- How to replace the default **Microfost Managed Encryption keys** of the blob storage with **custom keys** and store them in KeyVault.
- How to use **SQL Server support for Managed Service Identity** to allow the **authentication** of **AppService(s)** with **Azure SQL Server** and do with any connection string

#### Notes on the liability of Unencrypted Data at rest stored on SQL Database.

This is a strong liability as it would be possible for anyone with access to the database and with the appropriate rights to perform a backup of the database and restore it to some other server. This process would result in them to gain free access to all the information in the original dataset. The same could happen if an attacker where able to somehow determine the  connection string to the SQL Database Server instance i.e. by managing to download the **web.config or app.config** if this file is still used to hold such information.

#### [Summary of Solutions](https://app.pluralsight.com/player?course=microsoft-azure-data-securing&author=reza-salehi&name=5ec24f62-8bfc-40cb-8aa7-e731cbcb451d&clip=4&mode=live)  

- **Microsoft Azure KeValut** to store secrets privately.
- **Encryption of Data at rest**.
- **Microsoft Secret Identity (MSI)** to securely access Azure SQL Server DBs from **AppService**. 
- **Certificates and SSL** in Azurefor protection in transit.

---

### [Leaning Goals for Securing VMs with Key Vault](https://app.pluralsight.com/player?course=securing-virtual-machines-azure-key-vault&author=gary-grudzinskas&name=securing-virtual-machines-azure-key-vault-m0&clip=0&mode=live)  

- What Key Vault is, how to deploy and use it 
- How to use Disk Encryption for a Azure VM
- How to deploy certificates via the Azure KeyVault
- How to encrypt and decript VHDs

---

### [Protecting Application Keys and Secrets with Azure Key Vault and Microsoft Secret Identity (MSI)](https://app.pluralsight.com/player?course=microsoft-azure-data-securing&author=reza-salehi&name=83d87507-3bef-4754-a046-46980dbdfc55&clip=0&mode=live)   

- What **Microsoft Azure Key Vault** is and how to use it
- What **Microsoft Secret Identity (MSI)** and how to use it
- How to use the **Microsoft Visusal Studio Extension for the management of Identities** which allows developers to authenticate to **Azure AD** and obtain **access tokens** to test **MSI0related code** locally before deplying to AppService

### Microsoft Azure KeyVault

Use **Microsoft Azure KeyVault** to protect **secrets** such as

- Any storage **connection strings** i.e. for (Azure) SQL Server Database, Azure Storage, Azure Cache, etc.
- Any **Encryption Keys** used by your applications i.e. for **Azure SQL Always-Encrypted feature**, **Azure Storage Data Encryption at rest**, etc.
- Any kind of **Cryptographic Keys** in general
- Any kind of **secrets**
- Any **certificates both public and privat keys such as for x509 certificates used in HTTPS/SSL communication**

---

### [How to Enable Azure SQL Server Database Transparent Data Encryption](https://app.pluralsight.com/player?course=microsoft-azure-data-securing&author=reza-salehi&name=83d87507-3bef-4754-a046-46980dbdfc55&clip=1&mode=live)  

With **Transparent Data Encryption** the encryption of the data is performed by using **Microsoft Managed Encryption Keys**. This feasutes is **not enabled by default** but it is avalable from the **Transparent Data Encryption** menu item of the **SQL Databases pane**. However, it is also **possible to create your own encryption keys which should then be stored in KeyVault**. This features encrypts the **databases, the backups and logs**.

---

### [Storage Account Encryption Keys](https://app.pluralsight.com/player?course=microsoft-azure-data-securing&author=reza-salehi&name=83d87507-3bef-4754-a046-46980dbdfc55&clip=1&mode=live)  

All data in **Azure Storage Accounts** are **by default encrypted at rest by means of Microsoft Managed Encryption Keys**. However, it is possible at any time to produce **private keys** from the **Encryption** menu item of the storage account pane by simply ticking teh checkbox **use your own keys**. 

---

### [What is Microsoft Azure Key Vault?](https://app.pluralsight.com/player?course=microsoft-azure-data-securing&author=reza-salehi&name=83d87507-3bef-4754-a046-46980dbdfc55&clip=1&mode=live)   

**Microsoft Azure Key Vault** works exaclty as the real world **Bank Safety Box**. The user provides **authentication details** to **Microsoft Azure Key Vault** and then **Microsoft Azure Key Vault** returns a **access key**.
On returning to **Microsoft Azure Key Vault** it **authenticates** against the provided credentials and **authorizes** the user to use their **access key** to retrieve any secretes they might have stored in their vault. 

**Microsoft Azure Key Vault** makes use of **Azure AD** to **authenticate the AppService** that needs to access data from the vault. Therefore, teh application **must be registered with Azure AD** beforehand. When an **AppService** or application is registered with **Azure AD** they obtain in return **a client ID & a secret** which will make up the **authentication token** on the following access.
 
 **Microsoft Azure Key Vault** offers the following features

- **Grant or Revoke access** to individual **Azure AD** entities
- **Auditing & Logging**
- **Key Rotation & Versioning**

#### Key Rotation & Versioning

This feature is necessary as it is desirable to make sure that encryption keys do not remain the same and are changed overtime. However, an audit of the version is kept so that if data  is encrypted with a key that is then rotated it is still possible to decrypt it later on.

---

## [Harware Security Modules (HSM)](https://azure.microsoft.com/en-us/services/azure-dedicated-hsm/)  

 ---
### Complementary Resources on HSM Harware Security Modules (HSM)

- [Understanding Hardware Security Modules (HSMs)](https://www.cryptomathic.com/news-events/blog/understanding-hardware-security-modules-hsms)  
- [Protecting Encryption Keys with Azure Key Vault - Stephen Haunts](https://www.youtube.com/watch?v=WIgUmnwKdas) 

---
#### [What are HSMs?](https://www.cryptomathic.com/news-events/blog/understanding-hardware-security-modules-hsms)  

**Harware Security Modules (HSM)** are physical computing devices that **safeguards and manages digital keys** for strong authentication and provides **cryptoprocessing**. These modules traditionally come in the form of a plug-in card or an external device that attaches directly to a computer or network server. HSM is a special trusted network computer **performing a variety of cryptographic operations: key management, key exchange, encryption etc.** **Cryptographic operations must be performed in a trusted environment** that is no viruses, no malware, no exploit, no unauthorized access thus a fully-vetted and fully-controlled deeviced is best suited.

The simplest working model of a HSM can be described by the case in which a server which runs buisiness logic uses the HSM as a cryptographic service. The server sends some information to be encrypted to the HSM device on a trusted network and the devices uses the internally stored cryptographic keys to encrypt the information very efficiently and return it to the server. Conversely, the server can also use the HSM to decrypt information be means of the same process. 

#### Advantages

- The cryptographic keys never leave the safety of the HSM
- The server has more resources available for the business logic as the crytographic power is provided by the HSM
- The computational resources of the HSM are much higher than that of any tradional server hardware
- If the cryptographic keys are generated by the HSM itself these are much stronger than if they would be if generated by traditional server hardware

#### Summary of the features of HSM

1. Is built on top of specialized hardware. 
2. The hardware is well-tested and certified in special laboratories.
3. Has a security-focused OS.
4. Has limited access via a network interface that is strictly controlled by internal rules.
5. Actively hides and protects cryptographic material.
6. Can generate well-randomized keys

#### Separation of Concers

An ordinary, run-of-the-mill program writer mixes the database access code, business-logic and cryptographic calls in one big application. This is a dangerous approach as an attacker can use crafted data and vulnerabilities to access cryptographic material, steal keys, install an arbitrary X.509 certificate and so on.
To prevent scenarios like this, we need to separate the operations into two different areas. 

- Business logic 
- Cryptography. 

#### Generation of  well-randomized Cryptographic Keys (Weak Key vs Strong Key)

A cryptographic key must be truly random. A computer by design, is unable to generate a really random value because it is a finite-state machine. Therefore, we need a special physical process to generate random numbers and keys. An HSM has special hardware that uses a physical process to create a good source of randomness (entropy) that in turn is used to generate good quality and “perfectly” random keys.

#### Designed for Performance

HSMs have **outstanding and incomparable performance**. The maximum you can get in any server is n * 1000 digital signatures per second, but an HSM can achieve millions.

#### HSMs and Key Management

HSMs are built to protect cryptographic keys.
 
---

