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
- **Integration with other Azure services**

#### [Key Rotation & Versioning](https://app.pluralsight.com/player?course=microsoft-azure-data-securing&author=reza-salehi&name=83d87507-3bef-4754-a046-46980dbdfc55&clip=3&mode=live)  

This feature is necessary as it is desirable to make sure that encryption keys do not remain the same and are changed overtime. However, an audit of the version is kept so that if data  is encrypted with a key that is then rotated it is still possible to decrypt it later on. Whenever a secret is created in a Vault **the ID of the secret is a URL whose last fragment identifies the version**. For example in the example below the `https://myapplicationvault.vault.azure.net/secrets/thenameofthesecret/` indentifies the secret as a resource in Azure Key Vault while `8e3e459w3747wq85387eqw98e728e937949` is its version at the time of the creation. The `https://myapplicationvault.vault.azure.net/secrets/thenameofthesecret/` fragment always gives access to the latest versions but other versions are available as well as long as the corresponding version fragment is known.

```
https://myapplicationvault.vault.azure.net/secrets/thenameofthesecret/8e3e459w3747wq85387eqw98e728e937949
```

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

### [Demo: Configuring Azure Key Vault](https://app.pluralsight.com/player?course=microsoft-azure-data-securing&author=reza-salehi&name=83d87507-3bef-4754-a046-46980dbdfc55&clip=3&mode=live)  

 - Create a new Vault in Azure Key Vault
 - Store a connection string to the Vault as a secret
 - Register an AppService with **Azure AD** to obtain a **Client ID secret** to be used for the Key Vault authentication
 - Configure the AppService with the **secret from the Key Vault**
 - **Add the logic in the AppService that reads the configuration string from the Key Vault using the Client ID  and the KeyVault secret**
 - Deploy the AppService

#### [Create a new Vault in Azure Key Vault & Store a connection string to the Vault as a secret](https://app.pluralsight.com/player?course=microsoft-azure-data-securing&author=reza-salehi&name=83d87507-3bef-4754-a046-46980dbdfc55&clip=3&mode=live)  

The following Powershell script which must be run in `admin` mode is pretty self-explanatory. Notice that when when the ` Connect-AzureRmAccount` is run then the user might be promt to log in their Azure Microsoft Account in order to authorize the Powershell session. This cmdlet as it is sets the session to use the `default subscription`. In cases in which multiple subscriptions for the same account exist and you do not want to use the default subscription add the subscription swith to the statement that creates the Powershell session or to the other statement that create the assets.

 ```
 Connect-AzureRmAccount
 New-AzureRmKeyVault - VaultName 'MyApplicationVault' - ResourceGroup 'MyResourceGroup' -Location 'North Europe'
 # convert the item to store as a secret in teh Vault to a secure string
 $secureString = ConvertTo-SecureString -String "connection_string" -AsPlainText -Force
 # add the item to the vault and get the secret in return to use in your app
 $secret = SetAzureKeyVaultSecret -VaultName 'MyApplicationVault' - Name 'ConnectionString1' -SecretValue  $secureString  
 # print the ID of the secret as a feedback to make sure that it has been actually created in Key Vault
 # the id of the secret is also to be used in the apps that needs to retrieve the secret from the Vault 
 $secureString.Id
 ```

 #### [Register an AppService with **Azure AD** to obtain a **Client ID secret**](https://app.pluralsight.com/player?course=microsoft-azure-data-securing&author=reza-salehi&name=83d87507-3bef-4754-a046-46980dbdfc55&clip=3&mode=live)  

 By registering an AppService with **Azure AD** a **Application ID (aka Client ID) and a secret** are generated that will be used for

 - Authenticate to Azure AD
 - Authenticate to Azure Key Vault

 #### Steps to register the AppService with Azure AD

 1. Search **App Registration** in the Azure Portal
 2. Select a new application registration (Name, Type, Sign-on URL)
 3. The **Application ID** is easily found 
 4. The **secret** for this **Application ID** can be created is in the **Settings >> Keys** and you can choose an **Expiration** and a **cryptographic Value** is generated on saving
  
#### Powershell Script to register the AppService with Azure KeyVault

Notice that `-PermissionToSecrets Get` specifies that the **Application ID** set with `-ServicePrincipalName` is granted the **permission** to read the value of the keys from the vault of name `MyApplicationVault`. Clearly, other permissiones other than `Get (read)` can be set such as `Post (update)`.

```
Set-AzureRmKeyVaultAcessPolicy -VaultName MyApplicationVault' -ServicePrincipalName "...app ID secret..." -PermissionToSecrets Get
``` 

 #### [Read the key values from KeyVault](https://app.pluralsight.com/player?course=microsoft-azure-data-securing&author=reza-salehi&name=83d87507-3bef-4754-a046-46980dbdfc55&clip=3&mode=live)  

For the **AppService** to be able to talk to a **KeyVault on a Azure subscription** the **Nuget Pakage** below must be installed to it.

`Microsoft.IdentityModel.Clients.ActiveDirectory`  
`Microsoft.Azure.KeyVault`

Then the **web.config** must be edited so that the **connection strings and other sensitive information is replaced with the ID of the secret that corresponds to it in the Azure KeyVault**. In the **web.config** is it also possible to leave in the two pieces of information that the **AppService code** will need in order to gain access to the Key Vault that is

1. ClientId
2. ClientSecret
3. The URI of the keys that the AppService needs to access the values of from the KeyVault

It is important to understand that **it is now safe to leave these two pieces of information in the web.config** because they can only be used to access the KeyVault from the **Azure AppService** that has been **registered with Azure AD for a particular registered domain that is URL**. In the unfortunate case the any of all of the items **ClientID, ClientSecret or KeyVault Keys** were leaked these could not be used from any other domain but the registered domain for this specific **ServiceApp** to which any third-party should not have access unless they are the account managers. Moreover, the **ClientSecret can be revoked and a new one can be genereated** in case it was compromized.


The following code exerpt shows hot to use the client library to retrive a secret from the vault. 

```
var kv = new KeyVaultClient(KeyVaultClient.AuthenticationCallback(KeyVaultService.GetToken));
var secret = kv.GetSecretAsync(WebConfigiration.AppSettings["ConnectionString"]).Result;
KeyVaultService.ConnectionString = secret.Value;

---

