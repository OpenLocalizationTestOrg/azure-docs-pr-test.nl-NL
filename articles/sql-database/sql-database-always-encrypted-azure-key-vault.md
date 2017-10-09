---
title: 'Altijd versleuteld: SQL Database - Azure Sleutelkluis | Microsoft Docs'
description: Dit artikel laat zien hoe toosecure gevoelige gegevens in een SQL-database met gegevens met behulp van versleuteling Hallo altijd versleuteld Wizard in SQL Server Management Studio. Bevat ook instructies die wordt uitgelegd hoe u toostore elke versleutelingssleutel in Azure Sleutelkluis.
keywords: versleuteling van gegevens, de versleutelingssleutel, cloud-versleuteling
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: 6ca16644-5969-497b-a413-d28c3b835c9b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: sstein
ms.openlocfilehash: 8226bfef584e979643f5bb0747d4df16569f8204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a>Altijd versleuteld: Beveiligen van gevoelige gegevens in SQL-Database en de versleutelingssleutels in Azure Sleutelkluis

Dit artikel laat zien hoe toosecure gevoelige gegevens in een SQL-database met versleuteling van gegevens met behulp van Hallo [Wizard altijd versleuteld](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx). Bevat ook instructies die wordt uitgelegd hoe u toostore elke versleutelingssleutel in Azure Sleutelkluis.

Altijd versleutelde is een technologie voor versleuteling van nieuwe gegevens in Azure SQL Database en SQL-Server waarmee beveiligen van gevoelige gegevens in rust op Hallo-server tijdens het verkeer tussen client en server, en wanneer deze hello worden gebruikt. Altijd versleutelde zorgt ervoor dat gevoelige gegevens nooit wordt weergegeven als tekst zonder opmaak binnen Hallo database-systeem. Nadat u gegevensversleuteling configureert, alleen clienttoepassingen of appservers met toohello toegangstoetsen hebben toegang tot gecodeerde gegevens. Zie voor gedetailleerde informatie [altijd versleuteld (Database-Engine)](https://msdn.microsoft.com/library/mt163865.aspx).

Nadat u Hallo database toouse altijd versleuteld configureert, maakt u een clienttoepassing in C# met Visual Studio toowork met Hallo versleutelde gegevens.

Hallo stappen in dit artikel en meer informatie over hoe tooset up altijd versleuteld voor een Azure SQL database. In dit artikel leert u hoe tooperform Hallo volgende taken:

* Hallo altijd versleuteld wizard gebruiken in SSMS toocreate [sleutels altijd versleuteld](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).
  * Maak een [kolomhoofdsleutel (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).
  * Maak een [kolomversleutelingssleutel (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).
* Een databasetabel maken en kolommen te versleutelen.
* Maak een toepassing die wordt ingevoegd, selecteert en gegevens uit Hallo versleutelde kolommen worden weergegeven.

## <a name="prerequisites"></a>Vereisten
Voor deze zelfstudie hebt u het volgende nodig:

* Een Azure-account en -abonnement. Als u niet hebt, zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).
* [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versie 13.0.700.242 of hoger.
* [.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) of hoger (op Hallo van client-computer).
* [Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).
* [Azure PowerShell](/powershell/azure/overview), versie 1.0 of hoger. Type **(Get-Module azure - ListAvailable). Versie** toosee welke versie van PowerShell uitgevoerd.

## <a name="enable-your-client-application-tooaccess-hello-sql-database-service"></a>Uw client-toepassing tooaccess Hallo SQL Database-service inschakelen
U moet uw client toepassing tooaccess Hallo SQL Database-service inschakelen door het instellen van de vereiste verificatie Hallo en verkrijgen Hallo *ClientId* en *geheim* moet u tooauthenticate uw toepassing in de volgende code Hallo.

1. Open Hallo [klassieke Azure-portal](http://manage.windowsazure.com).
2. Selecteer **Active Directory** en klik op Hallo Active Directory-exemplaar dat uw toepassing wordt gebruikt.
3. Klik op **toepassingen**, en klik vervolgens op **toevoegen**.
4. Typ een naam voor uw toepassing (bijvoorbeeld: *myClientApp*), selecteer **WEBTOEPASSING**, en klik op Hallo pijl toocontinue.
5. Voor Hallo **AANMELDINGS-URL** en **APP ID URI** kunt u een geldige URL invoeren (bijvoorbeeld *http://myClientApp*) en door te gaan.
6. Klik op **configureren**.
7. Kopieer uw **CLIENT-ID**. (U moet deze waarde in uw code later.)
8. In Hallo **sleutels** sectie **1 jaar** van Hallo **Selecteer duur** vervolgkeuzelijst. (Kopieert u de sleutel Hallo nadat u hebt opgeslagen in stap 13.)
9. Schuif naar beneden en klik op **toepassing toevoegen**.
10. Laat **weergeven** instellen te**Microsoft-Apps** en selecteer **Microsoft Azure Service Management API**. Klik op Hallo vinkje toocontinue.
11. Selecteer **Azure Service Management openen...**  van Hallo **gedelegeerde machtigingen** vervolgkeuzelijst.
12. Klik op **OPSLAAN**.
13. Na het Hallo opslaan is voltooid, Hallo sleutelwaarde in Hallo kopiëren **sleutels** sectie. (U moet deze waarde in uw code later.)

## <a name="create-a-key-vault-toostore-your-keys"></a>Een sleutelkluis toostore uw sleutels maken
Nu dat uw client-app is geconfigureerd en u hebt uw client-ID, is tijd toocreate een sleutelkluis en de toegangsbeleid configureren zodat u en uw toepassing toegang krijgen tot Hallo-kluis geheimen (Hallo altijd versleuteld sleutels). Hallo *maken*, *ophalen*, *lijst*, *aanmelding*, *controleren*, *wrapKey*, en *unwrapKey* machtigingen zijn vereist voor het maken van een nieuwe hoofdsleutel voor kolom- en voor het instellen van versleuteling met SQL Server Management Studio.

U kunt snel een sleutelkluis maken door het uitvoeren van script volgen Hallo. Zie voor een gedetailleerde uitleg van deze cmdlets en meer informatie over het maken en configureren van een sleutelkluis [aan de slag met Azure Key Vault](../key-vault/key-vault-get-started.md).

    $subscriptionName = '<your Azure subscription name>'
    $userPrincipalName = '<username@domain.com>'
    $clientId = '<client ID that you copied in step 7 above>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $vaultName = 'AeKeyVault'


    Login-AzureRmAccount
    $subscriptionId = (Get-AzureRmSubscription -SubscriptionName $subscriptionName).Id
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroupName -Location $location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
    Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list




## <a name="create-a-blank-sql-database"></a>Een lege SQL-database maken
1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Ga te**nieuw** > **gegevens en opslag** > **SQL-Database**.
3. Maak een **leeg** database met de naam **kliniek** op een nieuwe of bestaande server. Voor gedetailleerde instructies over hoe toocreate een database in Azure-portal Hallo zien [uw eerste Azure SQL database](sql-database-get-started-portal.md).
   
    ![Een lege database maken](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

U moet Hallo verbindingsreeks later in de zelfstudie hello, dus u Hallo database maakt, en blader vervolgens toohello nieuwe kliniek database en kopieer Hallo verbindingsreeks. U kunt Hallo-verbindingsreeks ophalen op elk gewenst moment, maar het is gemakkelijk toocopy in hello Azure-portal.

1. Ga te**SQL-databases** > **kliniek** > **databaseverbindingsreeksen tonen**.
2. Kopieer de verbindingsreeks Hallo voor **ADO.NET**.
   
    ![Kopieer de verbindingsreeks Hallo](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a>Verbinding maken met toohello database met SSMS
Open SSMS en toohello server verbinden met Hallo kliniek database.

1. Open SSMS. (Ga te**Connect** > **Database-Engine** tooopen hello **tooServer verbinding** venster als deze niet geopend is.)
2. Voer uw servernaam en referenties. Hallo-servernaam kan worden gevonden op de blade Hallo SQL-database en in de verbindingsreeks Hallo u eerder hebt gekopieerd. Type Hallo volledige servernaam, met inbegrip van *database.windows.net*.
   
    ![Kopieer de verbindingsreeks Hallo](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

Als hello **nieuwe firewallregel** venster wordt geopend Meld u aan tooAzure en laat SSMS een nieuwe firewallregel voor u.

## <a name="create-a-table"></a>Een tabel maken
In deze sectie maakt u een tabel toohold patiënt gegevens. Het is niet in eerste instantie versleuteld--kunt u versleuteling wilt configureren in de volgende sectie Hallo.

1. Vouw **Databases**.
2. Klik met de rechtermuisknop Hallo **kliniek** database en klik op **nieuwe Query**.
3. Plakken Hallo Transact-SQL (T-SQL) te volgen in de nieuwe queryvenster Hallo en **Execute** deze.

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a>Versleutelen van de kolommen (Configureer altijd versleuteld)
SSMS biedt een wizard waarmee u eenvoudig configureren altijd versleuteld door stellen Hallo kolomhoofdsleutel kolomversleutelingssleutel en versleutelde kolommen voor u.

1. Vouw **Databases** > **kliniek** > **tabellen**.
2. Klik met de rechtermuisknop Hallo **patiënten** tabel en selecteer **versleutelen kolommen** tooopen Hallo altijd versleuteld wizard:
   
    ![Kolommen versleutelen](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

Hallo altijd versleuteld wizard omvat Hallo uit te voeren: **kolomselectie**, **hoofdsleutel configuratie**, **validatie**, en **samenvatting** .

### <a name="column-selection"></a>Kolom selecteren
Klik op **volgende** op Hallo **inleiding** pagina tooopen hello **kolomselectie** pagina. Op deze pagina wordt u selecteren welke kolommen u wilt dat tooencrypt, [Hallo type versleuteling, en welke kolomversleutelingssleutel (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.

Versleutelen **SSN** en **geboortedatum** informatie voor elke geduld. Hallo SSN kolom gebruikt deterministische versleuteling, die ondersteuning biedt voor gelijkheid zoekacties, samenvoegingen en gegroepeerd. Hallo geboortedatum kolom gebruikt willekeurige versleuteling, die geen ondersteuning biedt voor bewerkingen.

Set Hallo **versleutelingstype** voor Hallo SSN kolom te**Deterministic** en kolom Geboortedatum te Hallo**Randomized**. Klik op **Volgende**.

![Kolommen versleutelen](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a>Configuratie van de hoofdsleutel
Hallo **hoofdsleutel configuratie** pagina is waar u uw CMK en instellen Selecteer Hallo sleutelopslagplaatsprovider waar hello CMK worden opgeslagen. Op dit moment kunt u een CMK opslaan in het certificaatarchief van de Windows hello Azure Key Vault of een hardware security module (HSM).

Deze zelfstudie laat zien hoe toostore uw sleutels in Azure Sleutelkluis.

1. Selecteer **Azure Sleutelkluis**.
2. Selecteer de gewenste sleutelkluis Hallo uit de vervolgkeuzelijst Hallo.
3. Klik op **Volgende**.

![Configuratie van de hoofdsleutel](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a>Validatie
U kunt nu Hallo kolommen versleutelen of een PowerShell-script toorun later opslaan. Selecteer voor deze zelfstudie **toofinish nu doorgaan** en klik op **volgende**.

### <a name="summary"></a>Samenvatting
Controleer of Hallo-instellingen juist zijn en klik op **voltooien** toocomplete Hallo setup voor altijd versleuteld.

![Samenvatting](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-hello-wizards-actions"></a>Hallo wizardacties controleren
Nadat het Hallo-wizard is voltooid, wordt uw database instellen voor altijd versleuteld. Hallo wizard uitgevoerd Hallo van de volgende activiteiten:

* Een hoofdsleutel van kolom gemaakt en opgeslagen in Azure Sleutelkluis.
* Een kolomversleutelingssleutel gemaakt en opgeslagen in Azure Sleutelkluis.
* Geconfigureerde Hallo geselecteerde kolommen voor versleuteling. Hallo patiënten tabel momenteel geen gegevens bevat, maar alle bestaande gegevens in de kolommen geselecteerd Hallo nu versleuteld.

U kunt maken van sleutels in SSMS Hallo Hallo controleren door het uitbreiden van **kliniek** > **beveiliging** > **sleutels altijd versleuteld**.

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a>Maken van een clienttoepassing die met Hallo versleutelde gegevens werkt
Nu dat altijd versleuteld is ingesteld, kunt u een toepassing die wordt uitgevoerd *voegt* en *selecteert* op Hallo versleutelde kolommen.  

> [!IMPORTANT]
> Uw toepassing moet gebruiken [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objecten als tekst zonder opmaak gegevens toohello server met kolommen altijd versleuteld wordt doorgegeven. Letterlijke waarden doorgeven zonder SqlParameter objecten leidt tot een uitzondering.
> 
> 

1. Open Visual Studio en maak een nieuwe C# **consoletoepassing** (Visual Studio 2015 en eerder) of **Console-App (.NET Framework)** (Visual Studio 2017 en hoger). Zorg ervoor dat uw project te is ingesteld**.NET Framework 4.6** of hoger.
2. Naam Hallo project **AlwaysEncryptedConsoleAKVApp** en klik op **OK**.
3. Hallo NuGet-pakketten te volgen door te gaan te installeren**extra** > **NuGet Package Manager** > **Package Manager Console**.

Deze twee regels code worden uitgevoerd in Hallo Package Manager-Console.

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-tooenable-always-encrypted"></a>Uw verbinding tekenreeks tooenable altijd versleuteld wijzigen
Deze sectie wordt uitgelegd hoe tooenable altijd versleuteld in de verbindingsreeks voor de database.

tooenable altijd versleuteld, moet u tooadd hello **Kolomversleutelingsinstelling** sleutelwoord tooyour connection string en stel deze in te**ingeschakeld**.

U kunt dit rechtstreeks in de verbindingsreeks Hallo instellen of kunt u dit instellen met behulp van [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx). volgende sectie toont hoe de voorbeeldtoepassing Hallo in Hallo toouse **SqlConnectionStringBuilder**.

### <a name="enable-always-encrypted-in-hello-connection-string"></a>Altijd versleuteld inschakelen in de verbindingsreeks Hallo
Hallo na sleutelwoord tooyour verbindingsreeks toevoegen.

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a>Altijd versleuteld met SqlConnectionStringBuilder inschakelen
Hallo van de volgende code wordt getoond hoe tooenable altijd versleuteld door in te stellen [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) te[ingeschakeld](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-hello-azure-key-vault-provider"></a>Hello Azure Key Vault provider registreren
Hallo volgende code toont hoe tooregister hello Azure Sleutelkluis-provider met Hallo ADO.NET-stuurprogramma.

    private static ClientCredential _clientCredential;

    static void InitializeAzureKeyVaultProvider()
    {
       _clientCredential = new ClientCredential(clientId, clientSecret);

       SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
          new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

       Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
          new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

       providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
       SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
    }



## <a name="always-encrypted-sample-console-application"></a>Altijd versleutelde console voorbeeldtoepassing
Dit voorbeeld laat zien hoe:

* Wijzig uw verbinding tekenreeks tooenable altijd versleuteld.
* Azure Key Vault registreren als Hallo sleutelopslagplaatsprovider van de toepassing.  
* Gegevens invoegen in Hallo versleutelde kolommen.
* Een record met een filter voor een specifieke waarde in een versleutelde kolom selecteren.

Vervang de inhoud Hallo van **Program.cs** Hello code te volgen. Vervang de verbindingsreeks Hallo voor Hallo globale connectionString variabele in Hallo regel dat direct vóór Hallo Main-methode met uw geldige verbindingsreeks uit hello Azure-portal. Dit is de enige wijziging Hallo u toomake toothis code nodig.

Hallo app toosee altijd versleuteld in actie uitgevoerd.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider;

    namespace AlwaysEncryptedConsoleAKVApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"<connection string from hello portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

            InsertPatient(new Patient()
            {
                SSN = "999-99-0001",
                FirstName = "Orlando",
                LastName = "Gee",
                BirthDate = DateTime.Parse("01/04/1964")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0002",
                FirstName = "Keith",
                LastName = "Harris",
                BirthDate = DateTime.Parse("06/20/1977")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0003",
                FirstName = "Donna",
                LastName = "Carreras",
                BirthDate = DateTime.Parse("02/09/1973")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0004",
                FirstName = "Janet",
                LastName = "Gates",
                BirthDate = DateTime.Parse("08/31/1985")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0005",
                FirstName = "Lucy",
                LastName = "Harrington",
                BirthDate = DateTime.Parse("05/06/1993")
            });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter tooexit...");
            Console.ReadLine();
        }


        private static ClientCredential _clientCredential;

        static void InitializeAzureKeyVaultProvider()
        {

            _clientCredential = new ClientCredential(clientId, clientSecret);

            SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
              new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
              new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

            providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        }

        public async static Task<string> GetToken(string authority, string resource, string scope)
        {
            var authContext = new AuthenticationContext(authority);
            AuthenticationResult result = await authContext.AcquireTokenAsync(resource, _clientCredential);

            if (result == null)
                throw new InvalidOperationException("Failed tooobtain hello access token");
            return result.AccessToken;
        }

        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
     VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in hello Patients table tooreset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }



## <a name="verify-that-hello-data-is-encrypted"></a>Controleer of dat Hallo gegevens worden versleuteld
U kunt snel controleren dat actuele gegevens op de server Hallo Hallo worden gecodeerd door een query Hallo patiënten met SSMS (met behulp van de huidige verbinding waarbij **Kolomversleutelingsinstelling** nog niet is ingeschakeld).

Hallo volgende query uit op Hallo kliniek database worden uitgevoerd.

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

U kunt zien Hallo versleutelde kolommen bevatten geen gecodeerde gegevens.

   ![Nieuwe consoletoepassing](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

toouse SSMS tooaccess Hallo gecodeerde gegevens, kunt u Hallo toevoegen *Kolomversleutelingsinstelling = ingeschakeld* parameter toohello verbinding.

1. SSMS, met de rechtermuisknop op uw server in **Objectverkenner** en kies **Disconnect**.
2. Klik op **Connect** > **Database-Engine** tooopen hello **verbinding tooServer** venster en klik op **opties**.
3. Klik op **extra verbindingsparameters** en het type **Kolomversleutelingsinstelling = ingeschakeld**.
   
    ![Nieuwe consoletoepassing](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. Hallo volgende query uit op Hallo kliniek database worden uitgevoerd.
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     U ziet nu Hallo gecodeerde gegevens in Hallo versleutelde kolommen.

    ![Nieuwe consoletoepassing](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a>Volgende stappen
Nadat u een database die gebruikmaakt van altijd versleuteld maakt, kunt u toodo Hallo volgende:

* [Draaien en opschonen van uw sleutels](https://msdn.microsoft.com/library/mt607048.aspx).
* [Migreren van gegevens die al is versleuteld met altijd versleuteld](https://msdn.microsoft.com/library/mt621539.aspx).

## <a name="related-information"></a>Gerelateerde informatie
* [Altijd versleuteld (ontwikkeling client)](https://msdn.microsoft.com/library/mt147923.aspx)
* [Transparante gegevensversleuteling](https://msdn.microsoft.com/library/bb934049.aspx)
* [SQL Server-versleuteling](https://msdn.microsoft.com/library/bb510663.aspx)
* [Altijd versleutelde wizard](https://msdn.microsoft.com/library/mt459280.aspx)
* [Altijd versleutelde blog](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

