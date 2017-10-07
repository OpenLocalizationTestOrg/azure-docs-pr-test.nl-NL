---
title: aaaDesign uw eerste Azure SQL database | Microsoft Docs
description: Meer informatie over toodesign uw eerste Azure SQL-database.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/03/2017
ms.author: carlrab
ms.openlocfilehash: 65f0a1594cbdda7480abf32a847266a073e7560d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-sql-database"></a>Ontwerp van uw eerste Azure SQL database

Azure SQL-Database is een relationele database als een service (DBaaS) in Hallo Microsoft Cloud ('Azure'). In deze zelfstudie leert u hoe toouse hello Azure-portal en [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) naar: 

> [!div class="checklist"]
> * Maak een database in hello Azure-portal
> * Een firewallregel op serverniveau in hello Azure-portal instellen
> * Verbinding maken met toohello database met SSMS
> * Tabellen maken met SSMS
> * Gegevens voor bulksgewijs laden met BCP
> * Opvragen van die gegevens met SSMS
> * Hallo database tooa vorige herstellen [wijst naar een bepaald tijstip](sql-database-recovery-using-backups.md#point-in-time-restore) in hello Azure-portal

Als u een Azure-abonnement geen [een gratis account maken](https://azure.microsoft.com/free/) voordat u begint.

## <a name="prerequisites"></a>Vereisten

toocomplete deze zelfstudie, zorg ervoor dat u hebt geïnstalleerd:
- de nieuwste versie Hallo van [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).
- de nieuwste versie Hallo van [BCP en SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).

## <a name="log-in-toohello-azure-portal"></a>Meld u bij toohello Azure-portal

Meld u bij toohello [Azure-portal](https://portal.azure.com/).

## <a name="create-a-blank-sql-database"></a>Een lege SQL-database maken

Een Azure SQL-database wordt gemaakt met een gedefinieerde set [reken- en opslagresources](sql-database-service-tiers.md). Hallo-database wordt gemaakt binnen een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) en in een [logische Azure SQL Database-server](sql-database-features.md). 

Volg deze stappen toocreate een lege SQL-database. 

1. Klik op Hallo **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.

2. Selecteer **Databases** van Hallo **nieuw** pagina en selecteer **SQL-Database** van Hallo **Databases** pagina. 

   ![lege database maken](./media/sql-database-design-first-database/create-empty-database.png)

3. Hallo SQL-Database formulier invullen Hello volgende informatie, zoals wordt weergegeven op Hallo voorafgaand aan de installatiekopie:   

   | Instelling       | Voorgestelde waarde | Beschrijving | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Databasenaam** | mySampleDatabase | Zie [Database-id's](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) voor geldige databasenamen. | 
   | **Abonnement** | Uw abonnement  | Zie [Abonnementen](https://account.windowsazure.com/Subscriptions) voor meer informatie over uw abonnementen. |
   | **Resourcegroep** | myResourceGroup | Zie [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Naamgevingsconventies) voor geldige resourcegroepnamen. |
   | **Bron selecteren** | Lege database | Hiermee geeft u op dat een lege database moet worden gemaakt. |

4. Klik op **Server** toocreate en een nieuwe server configureren voor de nieuwe database. Hallo invullen **nieuwe serverformulier** Hello volgende informatie: 

   | Instelling       | Voorgestelde waarde | Beschrijving | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servernaam** | Een wereldwijd unieke naam | Zie [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Naamgevingsconventies) voor geldige servernamen. | 
   | **Aanmeldgegevens van serverbeheerder** | Een geldige naam | Zie [Database-id's](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) voor geldige aanmeldingsnamen.|
   | **Wachtwoord** | Een geldig wachtwoord | Uw wachtwoord moet ten minste 8 tekens bestaan en moet tekens bevatten uit drie van de volgende categorieën Hallo: hoofdletters, kleine letters, cijfers en niet-alfanumerieke tekens. |
   | **Locatie** | Een geldige locatie | Zie [Azure-regio's](https://azure.microsoft.com/regions/) voor informatie over regio's. |

   ![database-server maken](./media//sql-database-design-first-database/create-database-server.png)

5. Klik op **Selecteren**.

6. Klik op **prijscategorie** toospecify Hallo prijscategorie en prestatieniveau serviceniveau voor de nieuwe database. Selecteer voor deze zelfstudie **20 dtu's** en **250** GB aan opslagruimte.

   ![database-s1 maken](./media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. Klik op **Toepassen**.  

8. Selecteer een **sortering** voor Hallo lege database (voor deze zelfstudie gebruik Hallo standaardwaarde). Zie voor meer informatie over sorteringen [sorteringen](https://docs.microsoft.com/sql/t-sql/statements/collations)

9. Klik op **maken** tooprovision Hallo-database. Neemt over een minuut en een halve toocomplete inrichten. 

10. Op de werkbalk Hallo **meldingen** toomonitor Hallo-implementatieproces.

   ![melding](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a>Een serverfirewallregel maken

Hallo SQL Database-service maakt een firewall op Hallo-serverniveau waarmee wordt voorkomen dat externe toepassingen en hulpprogramma's verbinden toohello server of een database op de server Hallo tenzij een firewallregel tooopen Hallo firewall voor specifieke IP-adressen is gemaakt. Volg deze stappen toocreate een [SQL-Database firewallregel op serverniveau](sql-database-firewall-configure.md) voor uw client-IP-adressen en inschakelen van externe connectiviteit via Hallo SQL Database-firewall voor uw IP-adres. 

> [!NOTE]
> SQL Database communiceert via poort 1433. Als u tooconnect van binnen een bedrijfsnetwerk probeert, kan uitgaand verkeer via poort 1433 niet worden toegestaan door de firewall van uw netwerk. Als dit het geval is, kunt u tooyour Azure SQL Database-server kan geen verbinding tenzij uw IT-afdeling poort 1433 wordt geopend.
>

1. Nadat het Hallo-implementatie is voltooid, klikt u op **SQL-databases** van Hallo links menu en klik vervolgens op **mySampleDatabase** op Hallo **SQL-databases** pagina. Hallo overzichtspagina voor uw database wordt geopend, waarin u Hallo volledig gekwalificeerde servernaam (zoals **mynewserver20170313.database.windows.net**) en biedt opties voor verdere configuratie. Kopieer deze volledig gekwalificeerde servernaam voor later gebruik.

   > [!IMPORTANT]
   > U moet deze server volledig gekwalificeerde naam tooconnect tooyour server en de databases in de volgende snel aan de slag.
   > 

   ![servernaam](./media/sql-database-connect-query-dotnet/server-name.png) 

2. Klik op **serverfirewall ingesteld** op Hallo werkbalk zoals weergegeven in de vorige afbeelding Hallo. Hallo **Firewall-instellingen** pagina voor Hallo SQL Database-server wordt geopend. 

   ![serverfirewallregel](./media/sql-database-get-started-portal/server-firewall-rule.png) 


3. Klik op **client-IP toevoegen** op Hallo werkbalk tooadd nieuwe firewallregel tooa van uw huidige IP-adressen. Een firewallregel kan poort 1433 openen voor een afzonderlijk IP-adres of voor een aantal IP-adressen.

4. Klik op **Opslaan**. Een firewallregel op serverniveau is gemaakt voor uw huidige IP-adres poort 1433 op Hallo logische server te openen.

   ![serverfirewallregel instellen](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. Klik op **OK** en sluit vervolgens Hallo **Firewall-instellingen** pagina.

U kunt nu verbinding toohello SQL Database-server en de databases met SQL Server Management Studio of een ander hulpprogramma naar keuze van deze IP-adres met Hallo beheerder serveraccount eerder hebt gemaakt.

> [!IMPORTANT]
> Toegang via Hallo SQL Database-firewall is standaard ingeschakeld voor alle Azure-services. Klik op **OFF** op deze pagina toodisable voor alle Azure-services.

## <a name="sql-server-connection-information"></a>SQL Server-verbindingsgegevens

Hallo volledig gekwalificeerde servernaam voor uw Azure SQL Database-server ophalen in hello Azure-portal. U Hallo volledig gekwalificeerde naam tooconnect tooyour servers met SQL Server Management Studio gebruiken.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Selecteer **SQL-Databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina. 
3. In Hallo **Essentials** deelvenster in Azure portal-pagina voor uw database Hallo Zoek en kopieer de Hallo **servernaam**.

   ![verbindingsgegevens](./media/sql-database-connect-query-dotnet/server-name.png)

## <a name="connect-toohello-database-with-ssms"></a>Verbinding maken met toohello database met SSMS

Gebruik [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) tooestablish een verbinding tooyour Azure SQL Database-server.

1. Open SQL Server Management Studio.

2. In Hallo **tooServer verbinding** dialoogvenster Voer Hallo volgende informatie:

   | Instelling       | Voorgestelde waarde | Beschrijving | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | Servertype | Database-engine | Deze waarde is vereist |
   | Servernaam | de volledig gekwalificeerde servernaam Hallo | Hallo naam moet er ongeveer als volgt: **mynewserver20170313.database.windows.net**. |
   | Authentication | SQL Server-verificatie | SQL-verificatie is Hallo alleen verificatie die we in deze zelfstudie hebt geconfigureerd. |
   | Aanmelden | Hallo server-beheerdersaccount | Dit is Hallo-account die u hebt opgegeven tijdens het Hallo-server maken. |
   | Wachtwoord | Hallo-wachtwoord voor uw server admin-account | Dit is Hallo wachtwoord die u hebt opgegeven tijdens het Hallo-server maken. |

   ![verbinding maken met tooserver](./media/sql-database-connect-query-ssms/connect.png)

3. Klik op **opties** in Hallo **tooserver verbinding** in het dialoogvenster. In Hallo **verbinding toodatabase** sectie, voert u **mySampleDatabase** tooconnect toothis database.

   ![verbinding maken met toodb op server](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. Klik op **Verbinden**. Hallo Object Explorer-venster wordt geopend in SSMS. 

5. Vouw in Object Explorer **Databases** en vouw vervolgens **mySampleDatabase** tooview Hallo objecten in Hallo-voorbeelddatabase.

   ![database-objecten](./media/sql-database-connect-query-ssms/connected.png)  

## <a name="create-tables-in-hello-database"></a>Tabellen maken in Hallo-database 

Het schema van een database maken met vier tabellen die een beheersysteem studenten voor universiteiten met model [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):

- Persoon
- Loop
- Studenten
- Dit model van een beheersysteem studenten voor universiteiten creditcard

Hallo volgende diagram toont hoe deze tabellen zijn voor andere verwante tooeach. Sommige van deze tabellen verwijzen naar kolommen in andere tabellen. Hallo studenten tabel verwijst bijvoorbeeld naar Hallo **PersonId** kolom Hallo **persoon** tabel. Onderzoek Hallo diagram toounderstand hoe Hallo tabellen in deze zelfstudie zijn verwante tooone een andere. Voor een diepgaande blik op hoe toocreate effectieve databasetabellen, Zie [effectieve databasetabellen maken](https://msdn.microsoft.com/library/cc505842.aspx). Zie voor meer informatie over het kiezen van gegevenstypen [gegevenstypen](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).

> [!NOTE]
> U kunt ook Hallo [tabelontwerp in SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) toocreate en ontwerpen van uw tabellen. 

![Relaties tussen tabellen](./media/sql-database-design-first-database/tutorial-database-tables.png)

1. Klik in Objectverkenner met de rechtermuisknop op **mySampleDatabase** en klik vervolgens op **Nieuwe query**. Een lege queryvenster wordt geopend die verbonden tooyour database.

2. Uitvoeren in het queryvenster hello, Hallo query toocreate vier tabellen in de database te volgen: 

   ```sql 
   -- Create Person table

   CREATE TABLE Person
   (
   PersonId   INT IDENTITY PRIMARY KEY,
   FirstName   NVARCHAR(128) NOT NULL,
   MiddelInitial NVARCHAR(10),
   LastName   NVARCHAR(128) NOT NULL,
   DateOfBirth   DATE NOT NULL
   )
   
   -- Create Student table
 
   CREATE TABLE Student
   (
   StudentId INT IDENTITY PRIMARY KEY,
   PersonId  INT REFERENCES Person (PersonId),
   Email   NVARCHAR(256)
   )
   
   -- Create Course table
 
   CREATE TABLE Course
   (
   CourseId  INT IDENTITY PRIMARY KEY,
   Name   NVARCHAR(50) NOT NULL,
   Teacher   NVARCHAR(256) NOT NULL
   ) 

   -- Create Credit table
 
   CREATE TABLE Credit
   (
   StudentId   INT REFERENCES Student (StudentId),
   CourseId   INT REFERENCES Course (CourseId),
   Grade   DECIMAL(5,2) CHECK (Grade <= 100.00),
   Attempt   TINYINT,
   CONSTRAINT  [UQ_studentgrades] UNIQUE CLUSTERED
   (
   StudentId, CourseId, Grade, Attempt
   )
   )
   ```

   ![Tabellen maken](./media/sql-database-design-first-database/create-tables.png)

3. Hallo 'tabellen' Vouw in de Hallo SQL Server Management Studio Object explorer toosee Hallo tabellen die u hebt gemaakt.

   ![SSMS tabellen gemaakt](./media/sql-database-design-first-database/ssms-tables-created.png)

## <a name="load-data-into-hello-tables"></a>Gegevens laden in Hallo tabellen

1. Maak een map **SampleTableData** in uw voorbeeldgegevens Downloads map toostore voor uw database. 

2. Klik met de rechtermuisknop Hallo volgende koppelingen en deze opslaan in Hallo **SampleTableData** map. 

   - [SampleCourseData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCourseData)
   - [SamplePersonData](https://sqldbtutorial.blob.core.windows.net/tutorials/SamplePersonData)
   - [SampleStudentData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleStudentData)
   - [SampleCreditData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCreditData)

3. Open een opdrachtvenster en navigeer toohello SampleTableData map.

4. Uitvoeren van opdrachten tooinsert voorbeeldgegevens in Hallo tabellen vervangen Hallo waarden voor volgende Hallo **ServerName**, **DatabaseName**, **gebruikersnaam**, en **Wachtwoord** met Hallo waarden voor uw omgeving.
  
   ```bcp
   bcp Course in SampleCourseData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Person in SamplePersonData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Student in SampleStudentData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Credit in SampleCreditData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   ```

U hebt nu voorbeeldgegevens geladen in Hallo-tabellen die u eerder hebt gemaakt.

## <a name="query-data"></a>Querygegevens

Hallo volgende query's tooretrieve informatie uit Hallo databasetabellen worden uitgevoerd. Zie [SQL-query's schrijven](https://technet.microsoft.com/library/bb264565.aspx) toolearn meer over het schrijven van SQL-query's. de eerste query Hallo koppelt alle vier tabellen toofind alle Hallo studenten geleerd door ' Dominick Pope' die een klasse die hoger is dan 75% hebben in de klasse. de tweede query Hallo lid wordt van alle vier tabellen en vindt alle cursussen waarin 'Noe Coleman' ooit is ingeschreven.

1. Uitvoeren in een SQL Server Management Studio query-venster Hallo query te volgen:

   ```sql 
   -- Find hello students taught by Dominick Pope who have a grade higher than 75%

   SELECT  person.FirstName,
   person.LastName,
   course.Name,
   credit.Grade
   FROM  Person AS person
   INNER JOIN Student AS student ON person.PersonId = student.PersonId
   INNER JOIN Credit AS credit ON student.StudentId = credit.StudentId
   INNER JOIN Course AS course ON credit.CourseId = course.courseId
   WHERE course.Teacher = 'Dominick Pope' 
   AND Grade > 75
   ```

2. Uitvoeren na de query in een SQL Server Management Studio query-venster:

   ```sql
   -- Find all hello courses in which Noe Coleman has ever enrolled

   SELECT  course.Name,
   course.Teacher,
   credit.Grade
   FROM  Course AS course
   INNER JOIN Credit AS credit ON credit.CourseId = course.CourseId
   INNER JOIN Student AS student ON student.StudentId = credit.StudentId
   INNER JOIN Person AS person ON person.PersonId = student.PersonId
   WHERE person.FirstName = 'Noe'
   AND person.LastName = 'Coleman'
   ```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Een database tooa eerder punt herstellen in-time

Stel dat u een tabel per ongeluk hebt verwijderd. Dit is iets dat die u eenvoudig niet vanuit herstellen. Azure SQL Database kunt u toogo back tooany punt in tijd in Hallo laatste too35 dagen en dit punt in tijd tooa nieuwe database te herstellen. U kunt u deze database toorecover uw verwijderde gegevens. Hallo herstelpunt volgt Hallo voorbeeld database tooa voordat het Hallo-tabellen zijn toegevoegd.

1. Hallo pagina van de SQL-Database voor uw database, klik op **herstellen** op Hallo-werkbalk. Hallo **herstellen** pagina wordt geopend.

   ![herstellen](./media/sql-database-design-first-database/restore.png)

2. Hallo invullen **herstellen** formulier met Hallo vereist informatie:
    * Databasenaam: voer een naam in voor de database 
    * Punt in tijd: Selecteer Hallo **punt in tijd** tabblad op formulier voor Hallo terugzetten 
    * Herstelpunt: Selecteer een tijd die deze gebeurtenis treedt op voordat het Hallo-database is gewijzigd
    * Doelserver: U kunt deze waarde niet wijzigen wanneer een database herstellen 
    * Pool voor elastische database: Selecteer **None**  
    * Prijscategorie: Selecteer **20 dtu's** en **250 GB** van opslag.

   ![herstelpunt](./media/sql-database-design-first-database/restore-point.png)

3. Klik op **OK** toorestore Hallo database te[tooa herstelpunt in de tijd](sql-database-recovery-using-backups.md#point-in-time-restore) voordat het Hallo-tabellen zijn toegevoegd. Een dubbele database herstellen van een database tooa ander punt in tijd gemaakt in Hallo dezelfde server als de oorspronkelijke database Hallo vanaf Hallo punt in tijd u opgeeft, mits dit binnen de bewaarperiode Hallo voor uw [servicelaag](sql-database-service-tiers.md).

## <a name="next-steps"></a>Volgende stappen 
In deze zelfstudie hebt u geleerd basic databasetaken, zoals een database en tabellen maken, laden en gegevens opvragen en tijdstip Hallo database tooa eerder punt herstellen. U hebt geleerd hoe u:
> [!div class="checklist"]
> * Een database maken
> * Een firewallregel instellen
> * Verbinding maken met database met toohello [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)
> * Tabellen maken
> * Gegevens voor bulksgewijs laden
> * Deze gegevens opvragen
> * Hallo database tooa eerder punt herstellen met behulp van SQL-Database [wijst naar een bepaald tijstip](sql-database-recovery-using-backups.md#point-in-time-restore) mogelijkheden

Ga toohello volgende zelfstudie toolearn over het ontwerpen van een database met behulp van Visual Studio en C#.

> [!div class="nextstepaction"]
>[Ontwerp van een Azure SQL database en verbinding maken met C# en ADO.NET](sql-database-design-first-database-csharp.md)
