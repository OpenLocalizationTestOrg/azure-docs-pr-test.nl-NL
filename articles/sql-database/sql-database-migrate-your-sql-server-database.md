---
title: SQL Server database migreren naar Azure SQL Database | Microsoft Docs
description: Meer informatie over uw SQL Server-database migreren naar Azure SQL Database.
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
ms.openlocfilehash: 375d3ea0230e7d3fd0fc02ca7e0b8a7a76c24a27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-sql-server-database-to-azure-sql-database"></a>De SQL Server-database migreren naar Azure SQL Database

Het verplaatsen van uw SQL Server-database naar Azure SQL Database bestaat uit drie fasen: u eerst voorbereiden, vervolgens exporteren en vervolgens de database te importeren. In deze zelfstudie leert hoe u u kunt:

> [!div class="checklist"]
> * Een database in een SQL-Server voorbereiden voor migratie naar Azure SQL Database met behulp van de [gegevens migratie-assistent](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)
> * De database naar een Bacpac-bestand exporteren
> * Het Bacpac-bestand importeren in een Azure SQL Database

Als u een Azure-abonnement geen [een gratis account maken](https://azure.microsoft.com/free/) voordat u begint.

## <a name="prerequisites"></a>Vereisten

U kunt deze zelfstudie alleen voltooien als aan de volgende vereisten wordt voldaan:

- De nieuwste versie van geïnstalleerd [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). SSMS installeren, installeert ook de nieuwste versie van SQLPackage, een opdrachtregelprogramma dat kan worden gebruikt om een scala aan database ontwikkeling taken automatiseren. 
- Geïnstalleerd de [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).
- U hebt geïdentificeerd en hebben toegang tot een database te migreren. Deze zelfstudie wordt gebruikgemaakt van de [SQL Server 2008 R2 AdventureWorks OLTP-database](https://msftdbprodsamples.codeplex.com/releases/view/59211) op een exemplaar van SQL Server 2008 R2 of hoger, maar u kunt een database van uw keuze. U kunt met het oplossen van compatibiliteitsproblemen door gebruik [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)

## <a name="prepare-for-migration"></a>Voorbereiden voor migratie

U bent klaar voorbereiden voor migratie. Volg deze stappen voor het gebruik van de  **[gegevens migratie-assistent](https://www.microsoft.com/download/details.aspx?id=53595)**  vast te stellen van de gereedheid van de database voor migratie naar Azure SQL Database.

1. Open de **Data Migration Assistant**. U DMA kunt uitvoeren op elke computer met de connectiviteit met het SQL Server-exemplaar met de database die u wilt migreren, u hoeft niet te installeren op de computer die als host fungeert voor de SQL Server-exemplaar.

     ![gegevens migreren assistent openen](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. Klik in het menu links op **+ nieuw** maken een **Assessment** project. Vul in het formulier met een **projectnaam** (alle andere waarden moeten links op hun standaardwaarden) en klik op **maken**. De **opties** pagina wordt geopend.

     ![nieuwe gegevens migratie assistent project](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. Op de **opties** pagina, klikt u op **volgende**. De **bronnen selecteren** pagina wordt geopend.

     ![nieuwe opties voor de migratie van gegevens](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. Op de **bronnen selecteren** pagina, voer de naam van SQL Server-exemplaar waarin de server die u wilt migreren. De andere waarden op deze pagina indien nodig wijzigen. Klik op **Verbinden**.

     ![nieuwe migratie selecteert gegevensbronnen](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. In de **bronnen toevoegen** gedeelte van de **bronnen selecteren** pagina, schakel de selectievakjes in voor de databases voor compatibiliteit moet worden getest. Klik op **Add**.

     ![nieuwe migratie selecteert gegevensbronnen](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. Klik op **Start evaluatie**.

     ![nieuwe start beoordeling van de gegevens migreren](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. Wanneer de beoordeling is voltooid, wordt eerst gezocht om te zien als de database voldoende compatibel is te migreren. Zoek naar het vinkje in een groene cirkel.

     ![nieuwe gegevens assessment resultaten van de migratie compatibel](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. Bekijk de resultaten. De **pariteit voor SQL Server-functie** resultaten weergegeven worden de standaard-resultaten te bekijken. Specifiek Bekijk de informatie over niet-ondersteunde en gedeeltelijk ondersteunde functies en de opgegeven informatie over aanbevolen acties. 

     ![nieuwe gegevens migratie assessment pariteit](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. Controleer de **compatibiliteitsproblemen** door te klikken op deze optie in de linkerbovenhoek. De informatie over migratie blockers, gedragswijzigingen en afgeschafte functies voor elke compatibiliteitsniveau specifiek controleren. Voor de database AdventureWorks2008R2, Controleer u de wijzigingen in de zoekopdracht in volledige tekst omdat SQL Server 2008 en de wijzigingen in SERVERPROPERTY('LCID') omdat SQL Server 2000. Voor meer informatie over deze wijzigingen vindt u koppelingen voor meer informatie. Veel zoekopties en instellingen voor zoeken in volledige tekst zijn gewijzigd 

   > [!IMPORTANT] 
   > Nadat u de database naar Azure SQL Database migreert, kunt u de werking van de database op het huidige compatibiliteitsniveau (level 100 voor de database AdventureWorks2008R2) of op een hoger niveau. Zie voor meer informatie over de gevolgen en opties voor de werking van een database op een specifieke compatibiliteitsniveau [databasecompatibiliteitsniveau ALTER](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Zie ook [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) voor meer informatie over aanvullende databaseniveau instellingen met betrekking tot compatibiliteitsniveaus.
   >

10. Klik desgewenst op **rapport exporteren** op te slaan van het rapport als een JSON-bestand.
11. Sluit de assistent van de migratie van gegevens.

## <a name="export-to-bacpac-file"></a>Exporteren naar Bacpac-bestand 

Een Bacpac-bestand is een ZIP-bestand met de extensie BACPAC die de metagegevens en gegevens uit een SQL Server-database. Een Bacpac-bestand kan worden opgeslagen in Azure blob-opslag of lokale opslag voor het archiveren of voor de migratie - zoals van SQL Server naar Azure SQL Database. Exporteren van een transactioneel consistent, moet u ervoor zorgen die geen schrijven activiteit optreedt tijdens het exporteren.

Volg deze stappen voor het gebruik van het opdrachtregelprogramma SQLPackage exporteren van de database AdventureWorks2008R2 naar de lokale opslag.

1. Open een Windows-opdrachtprompt en wijzig de directory naar een map waarin u hebt de **130** versie van SQLPackage - zoals **C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin**.

2. De volgende SQLPackage opdracht bij de opdrachtprompt om te exporteren de **AdventureWorks2008R2** uit de database **localhost** naar **AdventureWorks2008R2.bacpac**. Wijzig deze waarden naargelang nodig is voor uw omgeving.

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![sqlpackage exporteren](./media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

Zodra de uitvoering voltooid is wordt het gegenereerde Bacpac-bestand wordt opgeslagen in de map waar de uitvoerbare sqlpackage bevindt. In dit voorbeeld C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin. 

## <a name="log-in-to-the-azure-portal"></a>Aanmelden bij Azure Portal

Meld u aan bij [Azure Portal](https://portal.azure.com/). Aanmelden van de computer van waaruit u het opdrachtregelprogramma SQLPackage uitvoert, kan het maken van de firewallregel vergemakkelijken in stap 5.

## <a name="create-a-sql-server-logical-server"></a>Maken van een logische SQL server-server

Een [SQL server-logische server](sql-database-features.md) fungeert als een administratieve middelpunt voor meerdere databases. Volg deze stappen voor het maken van een logische SQL server-server zodat de gemigreerde Adventure Works OLTP SQL Server-database bevat. 

1. Klik op de knop **Nieuw** in de linkerbovenhoek van Azure Portal.

2. Type **sql server** in het zoekvenster op de **nieuw** pagina en selecteer **SQL-database (logische server)** uit de gefilterde lijst.

    ![logische server selecteren](./media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. Op de **Alles** pagina, klikt u op **SQL server (logische server)** en klik vervolgens op **maken** op de **SQL Server (logische server)** pagina.

    ![logische server maken](./media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. Vul het formulier SQL-server (logische server) in met de volgende informatie, zoals in de voorgaande afbeelding wordt weergegeven:     

   | Instelling       | Voorgestelde waarde | Beschrijving | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servernaam** | Een globaal unieke naam invoeren | Zie [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Naamgevingsconventies) voor geldige servernamen. | 
   | **Aanmeldgegevens van serverbeheerder** | Voer een geldige naam | Zie [Database-id's](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) voor geldige aanmeldingsnamen. |
   | **Wachtwoord** | Geef een geldig wachtwoord | Uw wachtwoord moet ten minste 8 tekens bestaan en moet tekens bevatten uit drie van de volgende categorieën: hoofdletters, kleine letters, cijfers en niet-alfanumerieke tekens. |
   | **Abonnement** | Een abonnement selecteren | Zie [Abonnementen](https://account.windowsazure.com/Subscriptions) voor meer informatie over uw abonnementen. |
   | **Resourcegroep** | Kies een bestaande resourcegroep of maak een nieuwe groep, zoals **myResourceGroup** |  Zie [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Naamgevingsconventies) voor geldige resourcegroepnamen. |
   | **Locatie** | Geef een geldige locatie voor de nieuwe server | Zie [Azure-regio's](https://azure.microsoft.com/regions/) voor informatie over regio's. |

   ![logische server voltooid formulier maken](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. Klik op **maken** voor het inrichten van de logische server. De inrichting duurt een paar minuten. 

> [!IMPORTANT]
> Vergeet niet de servernaam, de aanmeldingsnaam voor server-beheerder en het wachtwoord. Verderop in deze zelfstudie moet u deze waarden.
>

## <a name="create-a-server-level-firewall-rule"></a>Een serverfirewallregel maken

De SQL-Database-service maakt een [firewall op het serverniveau](sql-database-firewall-configure.md) die externe toepassingen en hulpprogramma's kan geen verbinding maken met de server of een database op de server, tenzij een firewallregel is gemaakt om de firewall voor specifieke IP-adressen te openen. Volg deze stappen voor het maken van een SQL-Database firewallregel niveau van de server voor het IP-adres van de computer van waaruit u het opdrachtregelprogramma SQLPackage uitvoert. Hierdoor SQLPackage verbinding maken met de logische SQL serverDatabase-server via de Azure SQL Database-firewall. 

1. Klik op **alle resources** uit in het menu links en klikt u op de nieuwe server in de **alle resources** pagina. De overzichtspagina voor uw server wordt geopend en biedt opties voor verdere configuratie.

     ![overzicht van de logische server](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. Klik op **Firewall** links in het menu onder **instellingen** op de overzichtspagina. De pagina **Firewallinstellingen** voor de SQL Database-server wordt geopend. 

3. Klik op **client-IP toevoegen** op de werkbalk om het toevoegen van het IP-adres van de computer u momenteel gebruikt en klik vervolgens op **opslaan**. Een firewallregel op serverniveau is gemaakt voor dit IP-adres.

     ![serverfirewallregel instellen](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. Klik op **OK**.

U kunt nu verbinding op alle databases op deze server met SQL Server Management Studio of een ander hulpprogramma naar keuze van deze IP-adres met de server admin-account eerder hebt gemaakt.

> [!NOTE]
> SQL Database communiceert via poort 1433. Als u verbinding probeert te maken vanuit een bedrijfsnetwerk, wordt uitgaand verkeer via poort 1433 mogelijk niet toegestaan door de firewall van uw netwerk. In dat geval kunt u geen verbinding maken met uw Azure SQL Database-server, tenzij de IT-afdeling poort 1433 openstelt.
>

## <a name="import-a-bacpac-file-to-azure-sql-database"></a>Een Bacpac-bestand importeren in Azure SQL Database 

De nieuwste versies van het opdrachtregelprogramma SQLPackage bieden ondersteuning voor het maken van een Azure SQL database op een opgegeven [service prijscategorie en prestatieniveau](sql-database-service-tiers.md). Voor de beste prestaties tijdens het importeren van een hoog serviceniveau prijscategorie en prestatieniveau niveau selecteert en daarna geschaald verkleinen na het importeren als het serviceniveau prijscategorie en prestatieniveau groter is dan u onmiddellijk moet.

Volg deze stappen gebruik het opdrachtregelprogramma SQLPackage voor het importeren van de database AdventureWorks2008R2 in Azure SQL Database. Voor deze taak kunt u SQL Server Management Studio, is SQLPackage de voorkeursmethode voor de meeste productieomgevingen voor maximale flexibiliteit en de beste prestaties. Zie [migreren van SQL Server naar Azure SQL Database Bacpac-bestanden met](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

- De volgende SQLPackage opdracht bij de opdrachtprompt voor het importeren van de **AdventureWorks2008R2** -database van lokale opslag voor de SQL server logische server die u eerder hebt gemaakt naar een nieuwe database, een servicelaag van **Premium**, en een Servicedoelstelling van **P6**. Vervang de waarden in punthaken met de juiste waarden voor de logische server waarop SQL server wordt uitgevoerd en geef een naam voor de nieuwe database (ook de punthaken vervangen). U kunt ook wijzigen de waarden voor database-editie en service objectgive naar gelang van toepassing op uw omgeving. Voor deze zelfstudie naam van de database van de gemigreerde **myMigratedDatabase**.

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=<your_server_name>.database.windows.net;Initial Catalog=<your_new_database_name>;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![sqlpackage importeren](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Een logische SQL server-server luistert op poort 1433. Als u probeert verbinding maken met een SQL server logische server uit binnen een bedrijfsfirewall bevindt, is deze poort moet openen in de firewall van het bedrijf voor u om verbinding te maken.
>

## <a name="connect-using-sql-server-management-studio-ssms"></a>Verbinding maken met behulp van SQL Server Management Studio (SSMS)

SQL Server Management Studio gebruiken tot stand brengen van een verbinding met uw Azure SQL Database-server en een nieuwe database, een zogenaamde gemigreerd **myMigratedDatabase** in deze zelfstudie. Als u SQL Server Management Studio op een andere computer van waaruit u SQLPackage hebt uitgevoerd uitvoert, maakt u een firewallregel voor deze computer met de stappen in de vorige procedure.

1. Open SQL Server Management Studio.

2. Voer in het dialoogvenster **Verbinding maken met server** de volgende informatie in:
   - **Servertype**: geef de database-engine op
   - **Servernaam**: Voer de volledig gekwalificeerde servernaam zoals **mynewserver20170403.database.windows.net**
   - **Verificatie**: geef de SQL Server-verificatie op
   - **Aanmelding**: gebruik het beheerdersaccount voor de server
   - **Wachtwoord**: voer het wachtwoord in voor het beheerdersaccount voor de server
 
    ![verbinding maken met ssms](./media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. Klik op **Verbinden**. Het Object Explorer-venster wordt geopend. 

4. Vouw in Object Explorer **Databases** en vouw vervolgens **myMigratedDatabase** om de objecten in de database weer te geven.

## <a name="change-database-properties"></a>Database-eigenschappen wijzigen

U kunt de servicelaag, prestatieniveau en compatibiliteitsniveau met SQL Server Management Studio wijzigen. Tijdens de fase importeren wordt aangeraden dat u importeert met een hogere prestaties laag database voor de beste prestaties, maar dat u omlaag schalen nadat het importeren is voltooid om geld besparen totdat u klaar bent voor de geïmporteerde database actief gebruiken. Het wijzigen van het compatibiliteitsniveau kan opleveren betere prestaties en toegang tot de nieuwste mogelijkheden van de Azure SQL Database-service. Wanneer u een oudere database migreert, wordt het compatibiliteitsniveau van de database behouden op het laagste ondersteunde niveau van die compatibel is met de database wordt geïmporteerd. Zie voor meer informatie [verbeterde prestaties van query's met de compatibiliteit van niveau 130 in Azure SQL Database](sql-database-compatibility-level-query-performance-130.md).

1. In Object Explorer met de rechtermuisknop op **myMigratedDatabase** en klik op **nieuwe Query**. Een query-venster wordt geopend is verbonden met uw database.

2. De volgende opdracht in te stellen van de servicetier op **standaard** en het prestatieniveau naar **S1**.

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

3. De volgende opdracht om te wijzigen van het databasecompatibiliteitsniveau **130**.

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![compatibiliteitsniveau wijzigen](./media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a>Volgende stappen 
In deze zelfstudie u hebt voorbereid, geëxporteerd en de database geïmporteerd. U hebt geleerd aan:

> [!div class="checklist"]
> * Een database in een SQL-Server voorbereiden voor migratie naar Azure SQL Database
> * De database naar een Bacpac-bestand exporteren
> * Het Bacpac-bestand importeren in een Azure SQL Database

Ga naar de volgende zelfstudie voor informatie over het beveiligen van uw database.

> [!div class="nextstepaction"]
> [Beveiligen van uw Azure SQL Database](sql-database-security-tutorial.md).


