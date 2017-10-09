## <a name="next-steps"></a><span data-ttu-id="cac79-101">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cac79-101">Next steps</span></span>

<span data-ttu-id="cac79-102">Nadat de Azure Sleutelkluis-integratie is ingeschakeld, kunt u SQL Server-versleuteling inschakelen op de SQL-VM.</span><span class="sxs-lookup"><span data-stu-id="cac79-102">After enabling Azure Key Vault Integration, you can enable SQL Server encryption on your SQL VM.</span></span> <span data-ttu-id="cac79-103">Eerst moet u een asymmetrische sleutel toocreate in de sleutelkluis en een symmetrische sleutel vanuit SQL Server op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="cac79-103">First, you will need toocreate an asymmetric key inside your key vault and a symmetric key within SQL Server on your VM.</span></span> <span data-ttu-id="cac79-104">Vervolgens kunt u zich kunt tooexecute T-SQL-instructies tooenable versleuteling voor de databases en de back-ups.</span><span class="sxs-lookup"><span data-stu-id="cac79-104">Then, you will be able tooexecute T-SQL statements tooenable encryption for your databases and backups.</span></span>

<span data-ttu-id="cac79-105">Er zijn verschillende vormen van versleuteling die u van profiteren kunt:</span><span class="sxs-lookup"><span data-stu-id="cac79-105">There are several forms of encryption you can take advantage of:</span></span>

* [<span data-ttu-id="cac79-106">Transparante gegevensversleuteling (TDE)</span><span class="sxs-lookup"><span data-stu-id="cac79-106">Transparent Data Encryption (TDE)</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="cac79-107">Versleutelde back-ups</span><span class="sxs-lookup"><span data-stu-id="cac79-107">Encrypted backups</span></span>](https://msdn.microsoft.com/library/dn449489.aspx)
* [<span data-ttu-id="cac79-108">Kolom: versleuteling op bestandsniveau (wissen)</span><span class="sxs-lookup"><span data-stu-id="cac79-108">Column Level Encryption (CLE)</span></span>](https://msdn.microsoft.com/library/ms173744.aspx)

<span data-ttu-id="cac79-109">Hallo bevatten volgende Transact-SQL-scripts voorbeelden voor elk van deze gebieden.</span><span class="sxs-lookup"><span data-stu-id="cac79-109">hello following Transact-SQL scripts provide examples for each of these areas.</span></span>

### <a name="prerequisites-for-examples"></a><span data-ttu-id="cac79-110">Vereisten voor voorbeelden</span><span class="sxs-lookup"><span data-stu-id="cac79-110">Prerequisites for examples</span></span>

<span data-ttu-id="cac79-111">Elk voorbeeld is gebaseerd op Hallo twee vereisten: een asymmetrische sleutel van de sleutelkluis aangeroepen **CONTOSO_KEY** en een referentie die zijn gemaakt door hello Azure Sleutelkluis-integratie functie **Azure_EKM_TDE_cred**.</span><span class="sxs-lookup"><span data-stu-id="cac79-111">Each example is based on hello two prerequisites: an asymmetric key from your key vault called **CONTOSO_KEY** and a credential created by hello AKV Integration feature called **Azure_EKM_TDE_cred**.</span></span> <span data-ttu-id="cac79-112">Hallo volgende Transact-SQL-opdrachten het instellen van deze vereisten voor het uitvoeren van Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="cac79-112">hello following Transact-SQL commands setup these prerequisites for running hello examples.</span></span>

``` sql
USE master;
GO

sp_configure [show advanced options], 1;
GO
RECONFIGURE;
GO

-- Enable EKM provider
sp_configure [EKM provider enabled], 1;
GO
RECONFIGURE;

--create provider
CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov
FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';
GO

--create credential
CREATE CREDENTIAL sysadmin_ekm_cred
    WITH IDENTITY = 'keytestvault', --keyvault
    SECRET = '<<SECRET>>'
FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;


--must have sysadmin
ALTER LOGIN [TDE_Login]
ADD CREDENTIAL sysadmin_ekm_cred;


CREATE ASYMMETRIC KEY CONTOSO_KEY
FROM PROVIDER [AzureKeyVault_EKM_Prov]
WITH PROVIDER_KEY_NAME = 'keytestvault',  --key name
CREATION_DISPOSITION = OPEN_EXISTING;
```

### <a name="transparent-data-encryption-tde"></a><span data-ttu-id="cac79-113">Transparante gegevensversleuteling (TDE)</span><span class="sxs-lookup"><span data-stu-id="cac79-113">Transparent Data Encryption (TDE)</span></span>

1. <span data-ttu-id="cac79-114">Maken van een SQL Server-aanmelding toobe door Hallo Database-Engine gebruikt voor TDE vervolgens Hallo referentie tooit toevoegen.</span><span class="sxs-lookup"><span data-stu-id="cac79-114">Create a SQL Server login toobe used by hello Database Engine for TDE, then add hello credential tooit.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN TDE_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello TDE Login tooadd hello credential for use by the
   -- Database Engine tooaccess hello key vault
   ALTER LOGIN TDE_Login
   ADD CREDENTIAL Azure_EKM_TDE_cred;
   GO
   ```

1. <span data-ttu-id="cac79-115">Coderingssleutel van het Hallo-database die wordt gebruikt voor TDE maken.</span><span class="sxs-lookup"><span data-stu-id="cac79-115">Create hello database encryption key that will be used for TDE.</span></span>

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello database tooenable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a><span data-ttu-id="cac79-116">Versleutelde back-ups</span><span class="sxs-lookup"><span data-stu-id="cac79-116">Encrypted backups</span></span>

1. <span data-ttu-id="cac79-117">Een SQL Server-aanmelding toobe die wordt gebruikt door Hallo Database-Engine voor het versleutelen van back-ups maken en toevoegen van Hallo referentie tooit.</span><span class="sxs-lookup"><span data-stu-id="cac79-117">Create a SQL Server login toobe used by hello Database Engine for encrypting backups, and add hello credential tooit.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it is encrypting hello backup.
   CREATE LOGIN Backup_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello Encrypted Backup Login tooadd hello credential for use by
   -- hello Database Engine tooaccess hello key vault
   ALTER LOGIN Backup_Login
   ADD CREDENTIAL Azure_EKM_Backup_cred ;
   GO
   ```

1. <span data-ttu-id="cac79-118">Back-up Hallo database versleuteling opgeven met de asymmetrische sleutel Hallo Hallo sleutelkluis opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="cac79-118">Backup hello database specifying encryption with hello asymmetric key stored in hello key vault.</span></span>

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a><span data-ttu-id="cac79-119">Kolom: versleuteling op bestandsniveau (wissen)</span><span class="sxs-lookup"><span data-stu-id="cac79-119">Column Level Encryption (CLE)</span></span>

<span data-ttu-id="cac79-120">Dit script maakt een symmetrische sleutel is beveiligd door Hallo asymmetrische sleutel in de sleutelkluis Hallo en gebruikt vervolgens Hallo symmetrische sleutel tooencrypt gegevens in de database Hallo.</span><span class="sxs-lookup"><span data-stu-id="cac79-120">This script creates a symmetric key protected by hello asymmetric key in hello key vault, and then uses hello symmetric key tooencrypt data in hello database.</span></span>

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open hello symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data tooencrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close hello symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a><span data-ttu-id="cac79-121">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="cac79-121">Additional resources</span></span>

<span data-ttu-id="cac79-122">Voor meer informatie over hoe toouse deze versleutelingsfuncties zien [EKM met functies van SQL Server-codering met behulp van](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span><span class="sxs-lookup"><span data-stu-id="cac79-122">For more information on how toouse these encryption features, see [Using EKM with SQL Server Encryption Features](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span></span>

<span data-ttu-id="cac79-123">Let op Hallo stappen in dit artikel wordt ervan uitgegaan dat u al hebt uitgevoerd op een virtuele machine van Azure SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="cac79-123">Note that hello steps in this article assume that you already have SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="cac79-124">Als dit niet het geval is, Zie [een SQL Server-machine inrichten in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="cac79-124">If not, see [Provision a SQL Server virtual machine in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="cac79-125">Zie voor andere instructies over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines-overzicht](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cac79-125">For other guidance on running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
