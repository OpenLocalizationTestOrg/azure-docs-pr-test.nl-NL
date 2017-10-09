---
title: aaaMigrate SQL Server-database tooAzure SQL-Database | Microsoft Docs
description: Meer informatie over toomigrate uw SQL Server-database tooAzure SQL-Database.
services: sql-database
documentationcenter: 
author: janeng
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/27/2017
ms.author: janeng
ms.openlocfilehash: d10ad1d26576194f1dd6858bae5c3e7c1ec4fb91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-server-database-tooazure-sql-database"></a>Migreren van uw SQL Server-database tooAzure SQL-Database

Het verplaatsen van uw SQL Server database tooAzure SQL-Database bestaat uit drie fasen: eerst voorbereiden, en vervolgens exporteren en vervolgens importeren Hallo-database. In deze zelfstudie leert hoe u u kunt:

> [!div class="checklist"]
> * Een database in een SQL-Server voorbereiden voor migratie tooAzure SQL-Database met behulp van Hallo [gegevens migratie-assistent](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)
> * Hallo database tooa Bacpac-bestand exporteren
> * Hallo Bacpac-bestand importeren in een Azure SQL Database

Als u een Azure-abonnement geen [een gratis account maken](https://azure.microsoft.com/free/) voordat u begint.

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie, zorg ervoor dat Hallo volgende vereisten zijn voltooid:

- Meest recente versie van geïnstalleerde Hallo [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). SSMS installeert, worden ook Hallo nieuwste versie van SQLPackage, een opdrachtregelprogramma waarmee gebruikte tooautomate een bereik van database ontwikkeling taken kan worden geïnstalleerd. 
- Geïnstalleerde Hallo [gegevens migratie-assistent](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).
- U hebt geïdentificeerd en hebben toegang tot tooa database toomigrate. Deze zelfstudie wordt gebruikgemaakt van Hallo [SQL Server 2008 R2 AdventureWorks OLTP-database](https://msftdbprodsamples.codeplex.com/releases/view/59211) op een exemplaar van SQL Server 2008 R2 of hoger, maar u kunt een database van uw keuze. compatibiliteitsproblemen toofix, gebruik [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)

## <a name="prepare-for-migration"></a>Voorbereiden voor migratie

U bent klaar tooprepare voor migratie. Volg deze stappen toouse hello  **[gegevens migratie-assistent](https://www.microsoft.com/download/details.aspx?id=53595)**  tooassess Hallo gereedheid van de database voor de migratie tooAzure SQL-Database.

1. Open Hallo **gegevens migratie-assistent**. U kunt DMA uitvoeren op elke computer met connectiviteit toohello SQL Server-exemplaar met Hallo-database dat u van plan bent toomigrate, hoeft u geen tooinstall op Hallo computer die hostgebruik biedt Hallo SQL Server-exemplaar.

     ![gegevens migreren assistent openen](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. Hallo links menu en klik op **+ nieuw** toocreate een **Assessment** project. Vul Hallo formulier met een **projectnaam** (alle andere waarden moeten links op hun standaardwaarden) en klik op **maken**. Hallo **opties** pagina wordt geopend.

     ![nieuwe gegevens migratie assistent project](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. Op Hallo **opties** pagina, klikt u op **volgende**. Hallo **bronnen selecteren** pagina wordt geopend.

     ![nieuwe opties voor de migratie van gegevens](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. Op Hallo **bronnen selecteren** pagina, Voer Hallo-naam van SQL Server-exemplaar dat u van plan bent toomigrate Hallo-server bevat. Wijziging Hallo andere waarden op deze pagina, indien nodig. Klik op **Verbinden**.

     ![nieuwe migratie selecteert gegevensbronnen](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. In Hallo **bronnen toevoegen** gedeelte Hallo **bronnen selecteren** pagina, selecteert u de selectievakjes Hallo van Hallo databases toobe getest op compatibiliteit. Klik op **Add**.

     ![nieuwe migratie selecteert gegevensbronnen](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. Klik op **Start evaluatie**.

     ![nieuwe start beoordeling van de gegevens migreren](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. Wanneer Hallo assessment is voltooid, er eerst toosee als Hallo-database voldoende compatibel toomigrate is. Zoek naar een groene cirkel Hallo is ingeschakeld.

     ![nieuwe gegevens assessment resultaten van de migratie compatibel](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. Hallo resultaten bekijken. Hallo **pariteit voor SQL Server-functie** resultaten weergegeven Hallo standaard resultaten tooreview zijn. Bekijk specifiek Hallo informatie over niet-ondersteunde en gedeeltelijk ondersteunde functies en Hallo opgegeven informatie over aanbevolen acties. 

     ![nieuwe gegevens migratie assessment pariteit](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. Bekijk Hallo **compatibiliteitsproblemen** door te klikken op deze optie in de linkerbovenhoek Hallo. Specifiek leest informatie over migratie blockers, gedragswijzigingen, Hallo en afgeschafte functies voor elke compatibiliteitsniveau. Voor de database Hallo AdventureWorks2008R2, Controleer Hallo wijzigingen tooFull tekst zoeken omdat SQL Server 2008 en Hallo tooSERVERPROPERTY('LCID') wijzigingen sinds de SQL Server 2000. Voor meer informatie over deze wijzigingen vindt u koppelingen voor meer informatie. Veel zoekopties en instellingen voor zoeken in volledige tekst zijn gewijzigd 

   > [!IMPORTANT] 
   > Nadat u uw database tooAzure SQL-Database migreert, kunt u toooperate Hallo database op het huidige compatibiliteitsniveau (level 100 voor Hallo AdventureWorks2008R2 database) of op een hoger niveau. Zie voor meer informatie over Hallo gevolgen en opties voor de werking van een database op een specifieke compatibiliteitsniveau [databasecompatibiliteitsniveau ALTER](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Zie ook [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) voor meer informatie over overige instellingen op databaseniveau gerelateerde toocompatibility niveaus.
   >

10. Klik desgewenst op **rapport exporteren** toosave Hallo rapport als een JSON-bestand.
11. Sluit hello assistent migratie van gegevens.

## <a name="export-toobacpac-file"></a>TooBACPAC-bestand exporteren 

Een Bacpac-bestand is een ZIP-bestand met de extensie BACPAC met Hallo metagegevens en gegevens uit een SQL Server-database. Een Bacpac-bestand kan worden opgeslagen in Azure blob-opslag of lokale opslag voor het archiveren of voor de migratie - zoals van SQL Server-tooAzure SQL-Database. Een export toobe transactioneel consistent is, moet u ervoor zorgen die geen schrijven activiteit optreedt tijdens het Hallo exporteren.

Volg deze stappen toouse hello SQLPackage opdrachtregelprogramma tooexport hello AdventureWorks2008R2 toolocal databaseopslag.

1. Open een Windows-opdrachtprompt en wijzig de directory tooa map waarin u Hallo hebt **130** versie van SQLPackage - zoals **C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin**.

2. Uitvoeren van de volgende SQLPackage-opdracht op Hallo opdrachtprompt tooexport Hallo Hallo **AdventureWorks2008R2** uit de database **localhost** te**AdventureWorks2008R2.bacpac**. Wijzig deze waarden als de juiste tooyour omgeving.

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![sqlpackage exporteren](./media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

Zodra de Hallo-uitvoering is voltooid wordt gegenereerd Hallo Bacpac-bestand wordt opgeslagen in Hallo directory waar Hallo sqlpackage uitvoerbare bestand zich bevindt. In dit voorbeeld C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin. 

## <a name="log-in-toohello-azure-portal"></a>Meld u bij toohello Azure-portal

Meld u bij toohello [Azure-portal](https://portal.azure.com/). Aanmelden van Hallo computer van waaruit u Hallo SQLPackage opdrachtregel-hulpprogramma uitvoert, kan Hallo maken van de firewallregel Hallo vergemakkelijken in stap 5.

## <a name="create-a-sql-server-logical-server"></a>Maken van een logische SQL server-server

Een [SQL server-logische server](sql-database-features.md) fungeert als een administratieve middelpunt voor meerdere databases. Volg deze stappen een SQL server logische server toocontain hello toocreate gemigreerd Adventure Works OLTP SQL Server-database. 

1. Klik op Hallo **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.

2. Type **sql server** in het zoekvenster Hallo op Hallo **nieuw** pagina en selecteer **SQL-database (logische server)** van Hallo gefilterde lijst.

    ![logische server selecteren](./media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. Op Hallo **Alles** pagina, klikt u op **SQL server (logische server)** en klik vervolgens op **maken** op Hallo **SQL Server (logische server)** pagina .

    ![logische server maken](./media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. Hallo SQL server (logische server) formulier invullen Hello volgende informatie, zoals wordt weergegeven op Hallo voorafgaand aan de installatiekopie:     

   | Instelling       | Voorgestelde waarde | Beschrijving | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servernaam** | Een globaal unieke naam invoeren | Zie [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Naamgevingsconventies) voor geldige servernamen. | 
   | **Aanmeldgegevens van serverbeheerder** | Voer een geldige naam | Zie [Database-id's](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) voor geldige aanmeldingsnamen. |
   | **Wachtwoord** | Geef een geldig wachtwoord | Uw wachtwoord moet ten minste 8 tekens bestaan en moet tekens bevatten uit drie van de volgende categorieën Hallo: hoofdletters, kleine letters, cijfers en niet-alfanumerieke tekens. |
   | **Abonnement** | Een abonnement selecteren | Zie [Abonnementen](https://account.windowsazure.com/Subscriptions) voor meer informatie over uw abonnementen. |
   | **Resourcegroep** | Kies een bestaande resourcegroep of maak een nieuwe groep, zoals **myResourceGroup** |  Zie [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Naamgevingsconventies) voor geldige resourcegroepnamen. |
   | **Locatie** | Geef een geldige locatie voor de nieuwe server Hallo | Zie [Azure-regio's](https://azure.microsoft.com/regions/) voor informatie over regio's. |

   ![logische server voltooid formulier maken](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. Klik op **maken** tooprovision Hallo logische server. De inrichting duurt een paar minuten. 

> [!IMPORTANT]
> Vergeet niet de servernaam, de aanmeldingsnaam voor server-beheerder en het wachtwoord. Verderop in deze zelfstudie moet u deze waarden.
>

## <a name="create-a-server-level-firewall-rule"></a>Een serverfirewallregel maken

Hallo SQL Database-service maakt een [firewall op serverniveau Hallo](sql-database-firewall-configure.md) die externe toepassingen en hulpprogramma's kan geen verbinding maken toohello server of een database op de server Hallo tenzij een firewallregel tooopen Hallo is gemaakt Firewall voor specifieke IP-adressen. Volg deze stappen toocreate een SQL-Database firewallregel serverniveau voor Hallo IP-adres van Hallo computer van waaruit u Hallo SQLPackage opdrachtregel-hulpprogramma uitvoert. Hiermee kan SQLPackage tooconnect toohello SQL serverDatabase logische server via hello Azure SQL Database-firewall. 

1. Klik op **alle resources** in Hallo links menu en klik op de nieuwe server op Hallo **alle resources** pagina. Hallo overzichtspagina voor de server wordt geopend en biedt opties voor verdere configuratie.

     ![overzicht van de logische server](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. Klik op **Firewall** in Hallo links menu onder **instellingen** op de pagina overzicht Hallo. Hallo **Firewall-instellingen** pagina voor Hallo SQL Database-server wordt geopend. 

3. Klik op **client-IP toevoegen** op Hallo werkbalk tooadd Hallo IP-adres van de computer Hallo u momenteel gebruikt en klik vervolgens op **opslaan**. Een firewallregel op serverniveau is gemaakt voor dit IP-adres.

     ![serverfirewallregel instellen](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. Klik op **OK**.

U kunt nu verbinding tooall databases op deze server met SQL Server Management Studio of een ander hulpprogramma naar keuze van deze IP-adres met Hallo beheerder serveraccount eerder hebt gemaakt.

> [!NOTE]
> SQL Database communiceert via poort 1433. Als u tooconnect van binnen een bedrijfsnetwerk probeert, kan uitgaand verkeer via poort 1433 niet worden toegestaan door de firewall van uw netwerk. Als dit het geval is, kunt u tooyour Azure SQL Database-server kan geen verbinding tenzij uw IT-afdeling poort 1433 wordt geopend.
>

## <a name="import-a-bacpac-file-tooazure-sql-database"></a>Een Bacpac-bestand tooAzure SQL-Database importeren 

de nieuwste versies Hallo Hallo SQLPackage opdrachtregelprogramma bieden ondersteuning voor het maken van een Azure SQL database op een opgegeven [service prijscategorie en prestatieniveau](sql-database-service-tiers.md). Voor de beste prestaties tijdens het importeren van een hoog serviceniveau prijscategorie en prestatieniveau niveau selecteert en daarna geschaald verkleinen na het importeren als Hallo prijscategorie en prestatieniveau serviceniveau groter is dan u onmiddellijk moet.

Volg deze stappen gebruik Hallo SQLPackage opdrachtregelprogramma tooimport hello AdventureWorks2008R2 database tooAzure SQL-Database. Hoewel voor deze taak kunt u SQL Server Management Studio, is SQLPackage Hallo voorkeurs-methode voor de meeste productieomgevingen voor maximale flexibiliteit en de beste prestaties. Zie [migreren van SQL Server-tooAzure SQL-Database Bacpac-bestanden met](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

- Uitvoeren van de volgende SQLPackage-opdracht op Hallo opdrachtprompt tooimport Hallo Hallo **AdventureWorks2008R2** die u eerder gemaakte tooa nieuwe database, een service van de logische server voor lokale opslag toohello SQL server-database laag van **Premium**, en een Servicedoelstelling van **P6**. Hallo waarden punthaken vervangt door de juiste waarden voor de logische SQL server-server en geef een naam voor de nieuwe Hallo-database (ook vervangen Hallo punthaken). U kunt ook toochange Hallo waarden voor de database-editie en service objectgive als de juiste tooyour omgeving. Hallo-doel van deze zelfstudie, Hallo gemigreerde database heet **myMigratedDatabase**.

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=<your_server_name>.database.windows.net;Initial Catalog=<your_new_database_name>;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![sqlpackage importeren](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Een logische SQL server-server luistert op poort 1433. Als u tooconnect tooa SQL server logische server vanuit een bedrijfsfirewall probeert, moet deze poort openen in de bedrijfsfirewall Hallo voor u toosuccessfully verbinding maken.
>

## <a name="connect-using-sql-server-management-studio-ssms"></a>Verbinding maken met behulp van SQL Server Management Studio (SSMS)

Gebruik SQL Server Management Studio tooestablish een verbinding tooyour Azure SQL Database-server en gemigreerde database, een zogenaamde **myMigratedDatabase** in deze zelfstudie. Als u SQL Server Management Studio op een andere computer van waaruit u SQLPackage hebt uitgevoerd uitvoert, maakt u een firewallregel voor deze computer met Hallo stappen in de vorige procedure Hallo.

1. Open SQL Server Management Studio.

2. In Hallo **tooServer verbinding** dialoogvenster Voer Hallo volgende informatie:
   - **Servertype**: geef de database-engine op
   - **Servernaam**: Voer de volledig gekwalificeerde servernaam zoals **mynewserver20170403.database.windows.net**
   - **Verificatie**: geef de SQL Server-verificatie op
   - **Aanmelding**: gebruik het beheerdersaccount voor de server
   - **Wachtwoord**: Voer Hallo wachtwoord voor uw server admin-account
 
    ![verbinding maken met ssms](./media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. Klik op **Verbinden**. Hallo Object Explorer-venster wordt geopend. 

4. Vouw in Object Explorer **Databases** en vouw vervolgens **myMigratedDatabase** tooview Hallo objecten in Hallo-voorbeelddatabase.

## <a name="change-database-properties"></a>Database-eigenschappen wijzigen

U kunt de servicelaag Hallo prestatieniveau en compatibiliteitsniveau met SQL Server Management Studio wijzigen. Het is raadzaam tijdens Importfase hello, het importeren van tooa hogere prestaties laag database voor de beste prestaties, maar dat u omlaag schalen nadat Hallo importeren toosave geld totdat u klaar tooactively gebruik Hallo geïmporteerde database bent. Wijzigen van het compatibiliteitsniveau Hallo mogelijk resulteert in betere prestaties en de nieuwste mogelijkheden voor toegang tot toohello van hello Azure SQL Database-service. Wanneer u een oudere database migreert, wordt het compatibiliteitsniveau van de database behouden op Hallo laagste ondersteund niveau die compatibel is met het Hallo-database wordt geïmporteerd. Zie voor meer informatie [verbeterde prestaties van query's met de compatibiliteit van niveau 130 in Azure SQL Database](sql-database-compatibility-level-query-performance-130.md).

1. In Object Explorer met de rechtermuisknop op **myMigratedDatabase** en klik op **nieuwe Query**. Een query-venster verbonden tooyour database wordt geopend.

2. Uitvoeren van de opdracht tooset Hallo servicelaag te volgen Hallo**standaard** en prestatieniveau te Hallo**S1**.

    ```
    ALTER DATABASE myMigratedDatabase 
    MODIFY 
        (
        EDITION = 'Standard'
        , MAXSIZE = 250 GB
        , SERVICE_OBJECTIVE = 'S1'
    );
    ```

    ![servicelaag wijzigen](./media/sql-database-migrate-your-sql-server-database/service-tier.png)

3. Uitvoeren van de opdracht toochange Hallo databasecompatibiliteitsniveau te volgen Hallo**130**.

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![compatibiliteitsniveau wijzigen](./media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a>Volgende stappen 
In deze zelfstudie u hebt voorbereid, geëxporteerd en de database geïmporteerd. U hebt geleerd aan:

> [!div class="checklist"]
> * Een database in een SQL-Server voorbereiden voor migratie tooAzure SQL-Database
> * Hallo database tooa Bacpac-bestand exporteren
> * Hallo Bacpac-bestand importeren in een Azure SQL Database

Hoe gaan van de volgende zelfstudie toolearn toohello toosecure uw database.

> [!div class="nextstepaction"]
> [Beveiligen van uw Azure SQL Database](sql-database-security-tutorial.md).


