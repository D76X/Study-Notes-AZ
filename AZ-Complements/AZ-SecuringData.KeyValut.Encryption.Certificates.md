# AZ Complements - KeyVault

## Main Resources

1. [Microsoft Azure Developer: Securing Data by by Reza Salehi](https://app.pluralsight.com/library/courses/microsoft-azure-data-securing/table-of-contents)
2. [Securing Virtual Machines with Azure Key Vault by Gary Grudzinskas](https://app.pluralsight.com/library/courses/securing-virtual-machines-azure-key-vault/table-of-contents) 

## Realted Resources

- [Protecting Encryption Keys with Azure Key Vault - Stephen Haunts](https://www.youtube.com/watch?v=WIgUmnwKdas)  

- [Managing User Secrets](https://www.youtube.com/watch?v=KDgNJKZ0oiA)  

## Complementary Resources

- [Understanding Hardware Security Modules (HSMs)](https://www.cryptomathic.com/news-events/blog/understanding-hardware-security-modules-hsms)  

- [BREACH LEVEL INDEX](https://breachlevelindex.com/)

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
 # convert the item to store as a secret in the Vault to a secure string
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
```

---

### [Enabling Soft Delete and Do Not Purge on a Key Vault](https://app.pluralsight.com/player?course=microsoft-azure-data-securing&author=reza-salehi&name=83d87507-3bef-4754-a046-46980dbdfc55&clip=5&mode=live)  

#### [Demo on KeyVault Soft Delete & Do Not Purge](https://app.pluralsight.com/player?course=microsoft-azure-data-securing&author=reza-salehi&name=83d87507-3bef-4754-a046-46980dbdfc55&clip=6&mode=live)  

#### Soft Delete

In the event of any of the KeyVault resources being accidentally deleted users would be unable to retrieve their secrets which could result in serious consequences. The typical scenario is that of a key used to encrypt the HDD of virtual machine i.e. for backups. If the key were deleted being the deletion permanent would result in the VHD become unrecoverable.

For this reason **Zure Key Vault** offer a **soft delete option** whic **allows recovery of deleted vaults and vault abjects including keys, secrets and certificates**. ThePowershell script exerpt below enables the softt delete optionson an Azure KeyVault.

```
$kv = Get-AzureRmKeyVault -VaultName "MyVault1"
$resource = Get-AzureRmResource -ResourceId $kv.Id
($resource).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"
Set-AzureRmResource -ResourceId $resource.Id -Properties $resource.Properties
```

The following script recovers a KeyVault that has been soft deleted

```
Undo-AzureRmKeyVaultRemoval -VaultName "MyVault1" -ResourceGroupName "MyRG1" -Location "North-Europe"
```

#### Do Not Purge

**Do Not Purge** is to **prevent accidental purge of deleted vaults including keys, secrets and certificates**. As **Soft-Deleted KeyVault items can still be purged** by default the **Do Not Purge** features prevents the accidental permanent deletion of such soft-deleted resources. The Powershell script that enables this feature si virtually the same as the one obove expect for the `-Name "enablePurgeProtection"` switch.

```
$kv = Get-AzureRmKeyVault -VaultName "MyVault1"
$resource = Get-AzureRmResource -ResourceId $kv.Id
($resource).Properties | Add-Member -MemberType "NoteProperty" -Name "enablePurgeProtection" -Value "true"
Set-AzureRmResource -ResourceId $resource.Id -Properties $resource.Properties
```

The following Powershell may be used in order to remove a KeyVault. The switch `-RemovedState` causes Azure to **permanently delete**  the KeyVault 
**even if it is in soft-deleted state**. The only way to prevent this permanent deletion is to enable **Do Not Purge** on it.

```
RemoveAzureRmKeyVault -VaultName -ResourceGroupName "MyRG1" -Location "North-Europe" -RemovedState
```
---

## [Managed Service Identity (MSI)](https://app.pluralsight.com/player?course=microsoft-azure-data-securing&author=reza-salehi&name=83d87507-3bef-4754-a046-46980dbdfc55&clip=7&mode=live)  

**Managed Service Identity (MSI)** is a **different approach to security** with respect to **Azure KeyVault**. 
However, they share the same purpose.

---

## Azure KeVault vs. MSI

In the following the typical case in which an application needs to access a SQL database at run-time is considered. In this scenario the application will need to read the connection at run-time and of course leaving the connection string in any form of test in the web.config or app.config is bad practice. 

**Azure KeyVault and Managed Service Identity (MSI)** offer two alternative ways to solve this problem.

### How this problem is solved in Azure KeyVault

1. There is a text-based value that must kept secret, stored and accessed securely.
2. The text-based value is stored as encrypted value on the KeyVault.
3. An Application is registered with **Azure AD** and in the same context permissions can be granted to its **client identity (client ID & Sectret)** in regard to the KeyVault from which the application will need to be granted access to. 
4. The AppService can now retrieve the text-based value at run-time from teh KeyVault
 
### How this problem is solved by Managed Service Identity (MSI)

In this case we must somehow **configure Azure SQL Server** to **accept connections from one or more specific AppService**. In other words, this is the process of **authoirization of an application (AppService) to a third-party backend such as Azure SQL Server**. This can be achieved by means of **Azure AD** and the **Authorization Grant Flow**.

1. Create a new **Azure AD Identity for the AppService**.
2. Configure the third-party (Azure SQL Server) to grant this identity the permissions it needs. 
3. The client application (AppSevice) presents itself to the third party with its Azure ID identity.

---

### [Which one is best Azure KeyVault and Managed Service Identity (MSI)?](https://app.pluralsight.com/player?course=microsoft-azure-data-securing&author=reza-salehi&name=83d87507-3bef-4754-a046-46980dbdfc55&clip=7&mode=live)  

**Managed Service Identity (MSI) is recommended over Azure KeyVault** as the latter still relies on **clent ID + client secret (client identity)** to access the KeyVault. This employs the classic **OAuth Autorization Code Grant Flow** which is very secure but relays on the **secure storage of client secretes**. Coversely, Managed Service Identity **(MSI) does not need client secrets at all** it allows direct access to the `third-party` resource i.e. Azure SQL Server simply leveragin **Azure ID and the identity issued to the AppService**. 

- MSI does not require the client application (AppService) to hold secrets in its web.config while this is necessary in the cas

| MSI          | Azure Key Vault     |
| ------------ | ------------------- |
| Does not need to store client secrets in web.config   | Must store client secrest to access KeyVault in web.config|  
| easier to configure that Azure KeyVault | - |
| Can be used to authenticate any service that support Azure AD authentication | Can be used to any service that need secrets |
| **Cannot test locally** | Can test Locally |

---

### Some Azure Sevices that support Azure AD Authentication

- Azure SQL
- Azure Service Bus
- Azure Storage
- Azure Key Vault
- Azure Resource Manager
- Azure Data Lake

---

### [Demo: Configuring Managed Service Identity](https://app.pluralsight.com/player?course=microsoft-azure-data-securing&author=reza-salehi&name=83d87507-3bef-4754-a046-46980dbdfc55&clip=8&mode=live)  

The steps involved in setting up **Microsft Managed Identity (MSI)** between a Azure SQL instance and an AppService are the following.

1. Create a new **Azure AD Identity** for the AppService
2. Create a **login** in the Azure SQL instance for such identity
3. As an admin of the Azure SQL instance grant the login the permission that it needs
4. **Remove the username and password credentials from the connection string in the web.config of the AppService and replace it with the new AppService identity**
5. Modify the server side code of teh AppService to make use of this new connection string.

The following set of Azure CLI commands illustrate the process of

1. Creation of an Azure AD identity for an existing AppService
2. Creation of a Azure SQL login with read/write permissions and the given identity

```
az webapp identity assign 
--resource-group MyRG 
--name MyApp
```

The reuturns a JSON susch as

```
{
    "pincipalId": "...GUID...",
    "tenantId": "...GUID...",
    "type": "SystemAssigned",
}
```

Then the `pincipalId` can be used to set up the user on Azure SQL Server for the database that the AppService with such identity needs to run queries against.

```
az sql server ad-admin create 
--resource-group MyRG 
--server-name MyServer
-display-name msiadmin
-object-id  `pincipalId`
```

Also this command returns some JSON that describes the resource created in Azure. This time it is a **login on an Azure SQL instance**. 

With the new Azure AD identity for teh AppService and the Azure SQL login and permission already set up it is now possible to modify the server side code of the AppService in order to make it possible for it to direcctly connect to the Azure SQL instance and authenticate to it via Azure AD by means of its own Azure AD identity. 

In order to achieve this the server side code of the AppService mustuse the API provided in the following NuGet package.

```
Microsoft.Azure.Services.AppAuthentication
```

The `connectionString` in the `web.config` of teh AppService can now be changed from the following which clearly still **insecurely exposes the password and username** to the edited form where these details are entirely removed.  

```
<add 
name="SqlDataConnection"
connectionString = "data source=...;
initial catalog=...; 
pesist security info=True;
user id=AppServiceLogin";
password=p@$$word;
MultipleActiveResultSets=True
>
```

```
<add 
name="SqlDataConnection"
connectionString = "data source=...;
initial catalog=...; 
pesist security info=True;
MultipleActiveResultSets=Tru
>
```

As the **insecure and exposed password and username details have been completely removed** there is now no possible way these details could be leaked into source control and to the wider public or even stolen by developers for malicious purposes. However, it is now necessary to **supplement in code the connection string with teh Azure ID of the AppService** at the time a connection to the Azure SQL instance is attempted.

This can be achieved very easily thanks to the Authentication API made available in the `Microsoft.Azure.Services.AppAuthentication` package that has been installed. The following code exerpt illustrates the logic
of this abstraction.

Without MSI you would do something like what it is shown by the code below. Either username and password are hardcoded into the connection string directly which is the least secure solution. Otherwise, the process of generating the connection string **could be made more secure by using KeyVault to store username and password instead of hardcoding it into the connection string** and then composing the connection string via dynamic strings where the username and password details come from Azure KeyVault at runtime.

However, **even with such approach the secrets to access KeyVault would have to be stored in the web.config in place of the username and password** and the username and password would utlimately be read from the KeyVault at run time by using these secrets and letting the server code of the AppService  authenticate to Azure AD first all secured by teh fact that the AppService not only holds the KeyVault secrets but also runs under a **trusted Azure AD domain**.

```
var cnnectionString = ConfigirationManager.ConnectionStrings["SqlDataConnection"];

db = new SqlConnection(connectionString);
```

However, with the **Microsoft Managed Identity (MSI) approach** the **username and password are no longer necessary**. The Azure SQL service will be able to authorize teh AppService once this is authenticated with Azure AD and Azure AD set up so that the AppSevice Azure AD identity has a valid login on the Azure SQL instance which is the case in thi example thanks to the Azure CLI scripts run previously.  

```
var connectionString = ConfigirationManager.ConnectionStrings["SqlDataConnection"];

string sqlServerInstanceUrl = "https://database.windows.net/"
var tp = new AzureServiceTokenProvider();
var accessToken = tp.GetAccessTokenAsync(sqlServerInstanceUrl).Result;

db = new SqlConnection(){
    AccessToken = accessToken,
    ConnectionString = connectionString
};
```

---

## [Protecting Encryption Keys with Azure Key Vault - Stephen Haunts](https://www.youtube.com/watch?v=WIgUmnwKdas)  

### Learning Goals

- Setup Azure key Vault
- Authorize your application to access the vault with AzureAD
- Accessing the vault from your applications
- Using the Vault to wrap local encryption keys for performance
- Encrypting connection strings as Key Vault secrets to get flexible database routing in the cloud
- Audit logging for compliance

---

[BREACH LEVEL INDEX](https://breachlevelindex.com/)

This vompany collects statistics related to data breaches and their web sites condenses this information nicely on their [homepage](https://breachlevelindex.com/).

The number of **wordwide** breaches is huge. However, **what is even more startling is the statement that can be read on this homepage and that is reported below.

```
ONLY  4%  of breaches were “Secure Breaches” where encryption was used and the stolen data was rendered useless.
```
---

### Consequence of databreaches for companies

- Reputational damage
- Loss of sales
- Customers switching to competitors
- Legal Actions taken by customers, other companies or authorities
- Compliance costs
- Damage to customers

### Consequence of databreaches for individuals

- Thefts of identity and personal data
- Risk of impersonation
- Financial loss or of financial data
- Compromised credit cards
- Compromized transaction history

---

### Examples of data breaches and exploits

- [Bounty pregnancy club fined £400,000 over data handling](https://www.bbc.com/news/technology-47908222)

- [Zain Qaiser: Student jailed for blackmailing porn users worldwide](https://www.bbc.com/news/uk-47800378)  

---

### Types of threats

1. External
2. Internal i.e. employees

---

### [ General Data Protection Regulation (GDPR) - GDPR EU.org](https://www.gdpreu.org/)  

- [GDPR Overview](https://www.gdpreu.org/)  
- [Fines and Penalties](https://www.gdpreu.org/compliance/fines-and-penalties/)
- [Who Must Comply](https://www.gdpreu.org/the-regulation/who-must-comply/)  
- [Timeline](https://www.gdpreu.org/the-regulation/timeline/)
- [FAQ](https://www.gdpreu.org/faq/)

#### The main aims of GDPR 

- personal data protection
- personal dat safe storage 
- personal data safe handling 
- collection of personal data  provided explicit consents 

#### What happens if I do not comply?
You may be fined **for up to €20mm or 4% of your worldwide turnover (revenue), whichever is greater**. You may also be subject to lawsuits by affected data subjects. Learn more here.

---

