# AZ Complements - KeyVault

## Main Resources

1. [Microsoft Azure Developer: Securing Data by by Reza Salehi](https://app.pluralsight.com/library/courses/microsoft-azure-data-securing/table-of-contents)
2. [Securing Virtual Machines with Azure Key Vault by Gary Grudzinskas](https://app.pluralsight.com/library/courses/securing-virtual-machines-azure-key-vault/table-of-contents)  


## Realted Resources

## Complementary Resources

---

### [Leaning Goals for Microsoft Azure Developer: Securing Data by by Reza Salehi](https://app.pluralsight.com/player?course=securing-virtual-machines-azure-key-vault&author=gary-grudzinskas&name=securing-virtual-machines-azure-key-vault-m0&clip=0&mode=live) 

- How to avoid exposing secrets stored in configuration files such as **web.config or app.config**.
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


---

