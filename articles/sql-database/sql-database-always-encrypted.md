---
title: 'Altijd versleuteld: Azure SQL Database - Windows-certificaatarchief | Microsoft Docs'
description: Dit artikel laat zien hoe toosecure gevoelige gegevens in een SQL-database met versleuteling van de database met behulp van Hallo altijd versleuteld Wizard in SQL Server Management Studio (SSMS). Ook ziet u hoe toostore de versleutelingssleutels in het certificaat van de Windows hello opslaan.
keywords: versleutelen van gegevens, sql-versleuteling, versleuteling van de database, gevoelige gegevens altijd versleuteld.
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: 483f9a2120cc42b732142fc07807d3d8830a0c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a>Altijd versleuteld: Beveiligen van gevoelige gegevens in SQL-Database en de versleutelingssleutels in het certificaatarchief van de Windows hello

Dit artikel laat zien hoe toosecure gevoelige gegevens in een SQL-database met versleuteling van de database met behulp van Hallo [Wizard altijd versleuteld](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx). Ook ziet u hoe toostore de versleutelingssleutels in het certificaat van de Windows hello opslaan.

Versleutelde is altijd een nieuwe technologie voor het versleuteling van gegevens in Azure SQL Database en SQL-Server die helpt beveiligen van gevoelige gegevens in rust op Hallo-server tijdens het verkeer tussen client en server en tijdens het Hallo-gegevens wordt gebruikt, nooit ervoor te zorgen dat gevoelige gegevens weergegeven als de platte tekst binnen Hallo database-systeem. Nadat u gegevens worden versleuteld, alleen clienttoepassingen of appservers met toohello toegangstoetsen hebben toegang tot gecodeerde gegevens. Zie voor gedetailleerde informatie [altijd versleuteld (Database-Engine)](https://msdn.microsoft.com/library/mt163865.aspx).

Na het configureren van Hallo database toouse altijd versleuteld, maakt u een clienttoepassing in C# met Visual Studio toowork met Hallo versleutelde gegevens.

Stappen Hallo in dit artikel toolearn hoe tooset up altijd versleuteld voor een Azure SQL database. In dit artikel leert u hoe tooperform Hallo volgende taken:

* Hallo altijd versleuteld wizard gebruiken in SSMS toocreate [sleutels altijd versleuteld](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).
  * Maak een [hoofdsleutel van kolom (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).
  * Maak een [Kolomversleutelingssleutel (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).
* Een databasetabel maken en kolommen te versleutelen.
* Maak een toepassing die wordt ingevoegd, selecteert en gegevens uit Hallo versleutelde kolommen worden weergegeven.

## <a name="prerequisites"></a>Vereisten
Voor deze zelfstudie hebt u het volgende nodig:

* Een Azure-account en -abonnement. Als u niet hebt, zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).
* [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versie 13.0.700.242 of hoger.
* [.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) of hoger (op Hallo van client-computer).
* [Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).

## <a name="create-a-blank-sql-database"></a>Een lege SQL-database maken
1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Klik op **nieuwe** > **gegevens en opslag** > **SQL-Database**.
3. Maak een **leeg** database met de naam **kliniek** op een nieuwe of bestaande server. Zie voor gedetailleerde instructies over het maken van een database in Azure-portal Hallo [uw eerste Azure SQL database](sql-database-get-started-portal.md).
   
    ![Een lege database maken](./media/sql-database-always-encrypted/create-database.png)

Hallo-verbindingsreeks moet u later in de zelfstudie Hallo. Nadat het Hallo-database is gemaakt, gaat u toohello nieuwe kliniek database en kopieer Hallo verbindingsreeks. U kunt Hallo-verbindingsreeks ophalen op elk gewenst moment, maar het is gemakkelijk toocopy wanneer u zich in hello Azure-portal.

1. Klik op **SQL-databases** > **kliniek** > **databaseverbindingsreeksen tonen**.
2. Kopieer de verbindingsreeks Hallo voor **ADO.NET**.
   
    ![Kopieer de verbindingsreeks Hallo](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a>Verbinding maken met toohello database met SSMS
Open SSMS en toohello server verbinden met Hallo kliniek database.

1. Open SSMS. (Klik op **Connect** > **Database-Engine** tooopen hello **tooServer verbinding** venster als dit niet geopend is).
2. Voer uw servernaam en referenties. Hallo-servernaam kan worden gevonden op de blade Hallo SQL-database en in de verbindingsreeks Hallo u eerder hebt gekopieerd. Type Hallo volledige server naam waaronder *database.windows.net*.
   
    ![Kopieer de verbindingsreeks Hallo](./media/sql-database-always-encrypted/ssms-connect.png)

Als hello **nieuwe firewallregel** venster wordt geopend Meld u aan tooAzure en laat SSMS een nieuwe firewallregel voor u.

## <a name="create-a-table"></a>Een tabel maken
In deze sectie maakt u een tabel toohold patiënt gegevens. Dit is een normale tabel in eerste instantie--u versleuteling in de volgende sectie hello wilt configureren.

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
SSMS biedt een wizard tooeasily configureren altijd versleuteld door stellen Hallo CMK CEK en versleutelde kolommen voor u.

1. Vouw **Databases** > **kliniek** > **tabellen**.
2. Klik met de rechtermuisknop Hallo **patiënten** tabel en selecteer **versleutelen kolommen** tooopen Hallo altijd versleuteld wizard:
   
    ![Kolommen versleutelen](./media/sql-database-always-encrypted/encrypt-columns.png)

Hallo altijd versleuteld wizard omvat Hallo uit te voeren: **kolomselectie**, **hoofdsleutel configuratie** (CMK) **validatie**, en  **Samenvatting**.

### <a name="column-selection"></a>Kolom selecteren
Klik op **volgende** op Hallo **inleiding** pagina tooopen hello **kolomselectie** pagina. Op deze pagina wordt u selecteren welke kolommen u wilt dat tooencrypt, [Hallo type versleuteling, en welke kolomversleutelingssleutel (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.

Versleutelen **SSN** en **geboortedatum** informatie voor elke geduld. Hallo **SSN** kolom deterministische versleuteling, die ondersteuning biedt voor gelijkheid zoekacties, samenvoegingen en gegroepeerd wordt gebruikt. Hallo **geboortedatum** kolom willekeurige versleuteling, die geen ondersteuning biedt voor bewerkingen worden gebruikt.

Set Hallo **versleutelingstype** voor Hallo **SSN** kolom te**Deterministic** en Hallo **geboortedatum** kolom te **Ingedeeld**. Klik op **Volgende**.

![Kolommen versleutelen](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a>Configuratie van de hoofdsleutel
Hallo **hoofdsleutel configuratie** pagina is waar u uw CMK en instellen Selecteer Hallo sleutelopslagplaatsprovider waar hello CMK worden opgeslagen. Op dit moment kunt u een CMK opslaan in het certificaatarchief van de Windows hello Azure Key Vault of een hardware security module (HSM). Deze zelfstudie laat zien hoe toostore uw sleutels in het certificaat van de Windows hello opslaan.

Controleer **Windows-certificaatarchief** is geselecteerd en klik op **volgende**.

![Configuratie van de hoofdsleutel](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a>Validatie
U kunt nu Hallo kolommen versleutelen of een PowerShell-script toorun later opslaan. Selecteer voor deze zelfstudie **toofinish nu doorgaan** en klik op **volgende**.

### <a name="summary"></a>Samenvatting
Controleer of Hallo-instellingen juist zijn en klik op **voltooien** toocomplete Hallo setup voor altijd versleuteld.

![Samenvatting](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a>Hallo wizardacties controleren
Nadat het Hallo-wizard is voltooid, wordt uw database instellen voor altijd versleuteld. Hallo wizard uitgevoerd Hallo van de volgende activiteiten:

* Een CMK gemaakt.
* Een CEK gemaakt.
* Geconfigureerde Hallo geselecteerde kolommen voor versleuteling. Uw **patiënten** tabel momenteel geen gegevens bevat, maar alle bestaande gegevens in de kolommen geselecteerd Hallo nu versleuteld.

U kunt maken van sleutels in SSMS Hallo Hallo controleren door te gaan**kliniek** > **beveiliging** > **sleutels altijd versleuteld**. U ziet nu Hallo nieuwe sleutels die Hallo wizard voor u gegenereerd.

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a>Maken van een clienttoepassing die met Hallo versleutelde gegevens werkt
Nu dat altijd versleuteld is ingesteld, kunt u een toepassing die wordt uitgevoerd *voegt* en *selecteert* op Hallo versleutelde kolommen. toosuccessfully hello voorbeeldtoepassing uitvoeren, moet u het uitvoeren op Hallo dezelfde computer waarop u Hallo altijd versleuteld wizard uitgevoerd. toorun hello toepassing op een andere computer, moet u uw altijd versleuteld certificaten toohello computer met Hallo client-app implementeren.  

> [!IMPORTANT]
> Uw toepassing moet gebruiken [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objecten als tekst zonder opmaak gegevens toohello server met kolommen altijd versleuteld wordt doorgegeven. Letterlijke waarden doorgeven zonder SqlParameter objecten leidt tot een uitzondering.
> 
> 

1. Open Visual Studio en maak een nieuwe C#-consoletoepassing. Zorg ervoor dat uw project te is ingesteld**.NET Framework 4.6** of hoger.
2. Naam Hallo project **AlwaysEncryptedConsoleApp** en klik op **OK**.

![Nieuwe consoletoepassing](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a>Uw verbinding tekenreeks tooenable altijd versleuteld wijzigen
Deze sectie wordt uitgelegd hoe tooenable altijd versleuteld in de verbindingsreeks voor de database. Wijzigt u Hallo-consoletoepassing die u zojuist hebt gemaakt in de volgende sectie hello, "Altijd versleuteld console voorbeeldtoepassing."

tooenable altijd versleuteld, moet u tooadd hello **Kolomversleutelingsinstelling** sleutelwoord tooyour connection string en stel deze in te**ingeschakeld**.

U kunt dit rechtstreeks in de verbindingsreeks Hallo instellen of kunt u dit instellen met behulp van een [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx). volgende sectie toont hoe de voorbeeldtoepassing Hallo in Hallo toouse **SqlConnectionStringBuilder**.

> [!NOTE]
> Dit is de enige wijziging Hallo vereist in een toepassing specifieke tooAlways versleutelde van client. Als u een bestaande toepassing die wordt de verbindingsreeks extern opgeslagen (dat wil zeggen, in een configuratiebestand), bent u mogelijk kunnen tooenable altijd versleuteld zonder een code te wijzigen.
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a>Altijd versleuteld inschakelen in de verbindingsreeks Hallo
Hallo sleutelwoord tooyour verbindingsreeks volgende toevoegen:

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a>Altijd versleuteld met een SqlConnectionStringBuilder inschakelen
Hallo volgende code toont hoe tooenable altijd versleuteld door in te stellen Hallo [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) te[ingeschakeld](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a>Altijd versleutelde console voorbeeldtoepassing
Dit voorbeeld laat zien hoe:

* Wijzig uw verbinding tekenreeks tooenable altijd versleuteld.
* Gegevens invoegen in Hallo versleutelde kolommen.
* Een record met een filter voor een specifieke waarde in een versleutelde kolom selecteren.

Vervang de inhoud Hallo van **Program.cs** Hello code te volgen. Hallo-verbindingsreeks voor Hallo globale connectionString variabele in Hallo regel rechtstreeks boven Hallo Main-methode vervangen door uw geldige verbindingsreeks uit hello Azure-portal. Dit is de enige wijziging Hallo u toomake toothis code nodig.

Hallo app toosee altijd versleuteld in actie uitgevoerd.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
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

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
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
Kunt u snel controleren dat actuele gegevens op de server Hallo Hallo worden versleuteld door het uitvoeren van query's Hallo **patiënten** gegevens met SSMS. (Gebruik de huidige verbinding waarbij Hallo kolomversleutelingsinstelling nog niet is ingeschakeld.)

Hallo volgende query uit op Hallo kliniek database worden uitgevoerd.

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

U kunt zien Hallo versleutelde kolommen bevatten geen gecodeerde gegevens.

   ![Nieuwe consoletoepassing](./media/sql-database-always-encrypted/ssms-encrypted.png)

toouse SSMS tooaccess Hallo gecodeerde gegevens, kunt u Hallo toevoegen **Kolomversleutelingsinstelling = ingeschakeld** parameter toohello verbinding.

1. SSMS, met de rechtermuisknop op uw server in **Objectverkenner**, en klik vervolgens op **Disconnect**.
2. Klik op **Connect** > **Database-Engine** tooopen hello **verbinding tooServer** venster en klik vervolgens op **opties**.
3. Klik op **extra verbindingsparameters** en het type **Kolomversleutelingsinstelling = ingeschakeld**.
   
    ![Nieuwe consoletoepassing](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. Voer hello volgende query op Hallo **kliniek** database.
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     U ziet nu Hallo gecodeerde gegevens in Hallo versleutelde kolommen.

    ![Nieuwe consoletoepassing](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> Als u verbinding met SSMS (of een client) vanaf een andere computer maakt, hebben geen toegang tot toohello versleutelingssleutels en worden niet kunnen toodecrypt Hallo gegevens.
> 
> 

## <a name="next-steps"></a>Volgende stappen
Nadat u een database die gebruikmaakt van altijd versleuteld maakt, kunt u toodo Hallo volgende:

* Dit voorbeeld uitvoert vanaf een andere computer. Deze hebben geen toegang toohello versleutelingssleutels, zodat deze geen toegang tot toohello gecodeerde gegevens en kan niet worden uitgevoerd.
* [Draaien en opschonen van uw sleutels](https://msdn.microsoft.com/library/mt607048.aspx).
* [Migreren van gegevens die al is versleuteld met altijd versleuteld](https://msdn.microsoft.com/library/mt621539.aspx).
* [Certificaten tooother clientcomputers altijd versleuteld implementeren](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (Zie de sectie voor Hallo 'Voor het maken van certificaten beschikbaar tooApplications en gebruikers').

## <a name="related-information"></a>Gerelateerde informatie
* [Altijd versleuteld (ontwikkeling client)](https://msdn.microsoft.com/library/mt147923.aspx)
* [Transparante gegevensversleuteling](https://msdn.microsoft.com/library/bb934049.aspx)
* [SQL Server-versleuteling](https://msdn.microsoft.com/library/bb510663.aspx)
* [Altijd versleutelde Wizard](https://msdn.microsoft.com/library/mt459280.aspx)
* [Altijd versleutelde Blog](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

