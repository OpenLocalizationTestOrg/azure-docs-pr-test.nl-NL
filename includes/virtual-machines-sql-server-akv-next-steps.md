## <a name="next-steps"></a>Volgende stappen

Nadat de Azure Sleutelkluis-integratie is ingeschakeld, kunt u SQL Server-versleuteling inschakelen op de SQL-VM. Eerst moet u een asymmetrische sleutel toocreate in de sleutelkluis en een symmetrische sleutel vanuit SQL Server op de virtuele machine. Vervolgens kunt u zich kunt tooexecute T-SQL-instructies tooenable versleuteling voor de databases en de back-ups.

Er zijn verschillende vormen van versleuteling die u van profiteren kunt:

* [Transparante gegevensversleuteling (TDE)](https://msdn.microsoft.com/library/bb934049.aspx)
* [Versleutelde back-ups](https://msdn.microsoft.com/library/dn449489.aspx)
* [Kolom: versleuteling op bestandsniveau (wissen)](https://msdn.microsoft.com/library/ms173744.aspx)

Hallo bevatten volgende Transact-SQL-scripts voorbeelden voor elk van deze gebieden.

### <a name="prerequisites-for-examples"></a>Vereisten voor voorbeelden

Elk voorbeeld is gebaseerd op Hallo twee vereisten: een asymmetrische sleutel van de sleutelkluis aangeroepen **CONTOSO_KEY** en een referentie die zijn gemaakt door hello Azure Sleutelkluis-integratie functie **Azure_EKM_TDE_cred**. Hallo volgende Transact-SQL-opdrachten het instellen van deze vereisten voor het uitvoeren van Hallo voorbeelden.

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

### <a name="transparent-data-encryption-tde"></a>Transparante gegevensversleuteling (TDE)

1. Maken van een SQL Server-aanmelding toobe door Hallo Database-Engine gebruikt voor TDE vervolgens Hallo referentie tooit toevoegen.

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

1. Coderingssleutel van het Hallo-database die wordt gebruikt voor TDE maken.

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

### <a name="encrypted-backups"></a>Versleutelde back-ups

1. Een SQL Server-aanmelding toobe die wordt gebruikt door Hallo Database-Engine voor het versleutelen van back-ups maken en toevoegen van Hallo referentie tooit.

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

1. Back-up Hallo database versleuteling opgeven met de asymmetrische sleutel Hallo Hallo sleutelkluis opgeslagen.

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a>Kolom: versleuteling op bestandsniveau (wissen)

Dit script maakt een symmetrische sleutel is beveiligd door Hallo asymmetrische sleutel in de sleutelkluis Hallo en gebruikt vervolgens Hallo symmetrische sleutel tooencrypt gegevens in de database Hallo.

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

## <a name="additional-resources"></a>Aanvullende bronnen

Voor meer informatie over hoe toouse deze versleutelingsfuncties zien [EKM met functies van SQL Server-codering met behulp van](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).

Let op Hallo stappen in dit artikel wordt ervan uitgegaan dat u al hebt uitgevoerd op een virtuele machine van Azure SQL-Server. Als dit niet het geval is, Zie [een SQL Server-machine inrichten in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md). Zie voor andere instructies over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines-overzicht](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).
