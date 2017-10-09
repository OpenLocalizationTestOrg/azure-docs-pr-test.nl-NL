---
title: aaaGetting gestart met het synchroniseren van Azure SQL-gegevens (Preview) | Microsoft Docs
description: Deze zelfstudie helpt u aan de slag met Azure SQL-gegevenssynchronisatie (Preview).
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a>Aan de slag met het synchroniseren van Azure SQL-gegevens (Preview)
In deze zelfstudie leert u hoe tooset up synchroniseren van Azure SQL-gegevens door te maken van een groep voor synchronisatie met hybride die zowel Azure SQL Database en SQL Server-exemplaren bevat. nieuwe groep voor synchronisatie Hallo is volledig geconfigureerd en synchroniseert op Hallo schema dat u instelt.

Deze zelfstudie wordt ervan uitgegaan dat er ten minste enige ervaring met SQL-Database en SQL Server. 

Zie voor een overzicht van de SQL-gegevenssynchronisatie [synchroniseren van gegevens](sql-database-sync-data.md).

Voor volledige PowerShell-voorbeelden laten zien hoe tooconfigure synchroniseren van de SQL-gegevens, Hallo artikelen volgende zien:
-   [Gebruik PowerShell toosync tussen meerdere Azure SQL-databases](scripts/sql-database-sync-data-between-sql-databases.md)
-   [Gebruik PowerShell toosync tussen een Azure SQL Database en een lokale SQL Server-database.](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> Hallo volledige technische documentatie voor Azure SQL synchroniseren van gegevens, voorheen ondergebracht op MSDN, is beschikbaar als een. PDF-document. Download deze [hier](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).

## <a name="step-1---create-sync-group"></a>Stap 1: het maken van de groep voor synchronisatie

### <a name="locate-hello-data-sync-settings"></a>Instellingen voor het synchroniseren van gegevens van Hallo vinden

1.  Navigeer in uw browser toohello Azure-portal.

2.  Zoek uw SQL-databases van het Dashboard of van Hallo SQL-Databases pictogram op de werkbalk Hallo in Hallo-portal.

    ![Lijst met Azure SQL-databases](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  Op Hallo **SQL-databases** blade, selecteer Hallo bestaande SQL-database die u toouse wilt zoals Hallo hub database voor synchronisatie van gegevens. Hallo SQL databaseblade wordt geopend.

4.  Selecteer op Hallo SQL database-blade voor de geselecteerde database Hallo, **tooother databases synchroniseren**. Hallo gegevenssynchronisatie blade wordt geopend.

    ![Synchronisatieoptie tooother databases](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a>Maak een nieuwe groep voor synchronisatie

1.  Selecteer op de blade voor het synchroniseren van gegevens van Hallo **groep voor synchronisatie met nieuwe**. Hallo **groep voor synchronisatie met nieuwe** er wordt een blade geopend met stap 1, **groep maken-sync**, gemarkeerde. Hallo **groep voor synchronisatie maken** blade ook wordt geopend.

2.  Op Hallo **groep voor synchronisatie maken** blade volgende dingen Hallo:

    1.  In Hallo **Sync groepsnaam** en voer een naam voor de nieuwe groep voor synchronisatie Hallo.

    2.  In Hallo **metagegevens synchronisatiedatabase** sectie, kiest u of toocreate een nieuwe database (aanbevolen) of toouse een bestaande database.

        > [!NOTE]
        > Microsoft raadt aan dat u een nieuwe, lege database toouse zoals Hallo synchronisatiedatabase metagegevens maken. Synchroniseren van gegevens maakt tabellen in deze database en voert een regelmatige werkbelasting. Deze database wordt automatisch gedeeld als Hallo metagegevens synchronisatiedatabase voor alle van de synchronisatie-groepen in de geselecteerde regio Hallo. U kunt Hallo metagegevens-synchronisatiedatabase, de naam of het serviceniveau niet wijzigen zonder slepen en neerzetten.

        Als u hebt gekozen **nieuwe database**, selecteer **nieuwe database maken.** Hallo **SQL-Database** blade wordt geopend. Op Hallo **SQL-Database** blade een naam geven en Hallo nieuwe database te configureren. Selecteer vervolgens **OK**.

        Als u hebt gekozen **bestaande database gebruiken**, selecteer Hallo-database van Hallo-lijst.

    3.  In Hallo **automatische synchronisatie** sectie, selecteert u eerst **op** of **uit**.

        Als u hebt gekozen **op**, in Hallo **Synchronisatiefrequentie** sectie, voer een getal in en selecteert u seconden, minuten, uren of dagen.

        ![Geef de synchronisatiefrequentie](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  In Hallo **conflictoplossing** sectie, selecteert u 'Hub wins' of "WINS-lid."

        ![Opgeven hoe conflicten worden opgelost](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  Selecteer **OK** en wachten op Hallo nieuwe synchronisatie groep toobe gemaakt en geïmplementeerd.

## <a name="step-2---add-sync-members"></a>Stap 2: synchronisatie leden toevoegen

Nadat de nieuwe groep voor synchronisatie hello wordt gemaakt en geïmplementeerd, stap 2 **sync leden toevoegen**, is gemarkeerd in Hallo **groep voor synchronisatie met nieuwe** blade.

In Hallo **Hub Database** sectie, voert u de bestaande referenties Hallo voor Hallo SQL Database-server op welke Hallo hub database zich bevindt. Voer geen *nieuwe* referenties in deze sectie.

![Hub database is toosync groep toegevoegd](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a>Toevoegen van een Azure SQL Database

In Hallo **Liddatabase** sectie eventueel een groep voor synchronisatie met Azure SQL Database toohello toevoegen door te selecteren **toevoegen van een Azure-Database**. Hallo **Azure-Database configureren** blade wordt geopend.

Op Hallo **Azure-Database configureren** blade volgende dingen Hallo:

1.  In Hallo **Sync lidnaam** veld, Geef een naam op voor de nieuwe synchronisatie lid Hallo. Deze naam is niet hetzelfde Hallo-naam van het Hallo-database zelf.

2.  In Hallo **abonnement** optie hello Azure-abonnement voor factureringsdoeleinden die is gekoppeld.

3.  In Hallo **Azure SQL Server** optie Hallo bestaande SQL-databaseserver.

4.  In Hallo **Azure SQL Database** optie Hallo bestaande SQL-database.

5.  In Hallo **Sync richtingen** bidirectionele Sync, toohello Hub, selecteer of van Hallo Hub.

    ![Het toevoegen van een nieuwe SQL-Database sync lid](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  In Hallo **gebruikersnaam** en **wachtwoord** velden, Voer Hallo bestaande referenties voor Hallo SQL Database-server op welke Hallo liddatabase zich bevindt. Voer geen *nieuwe* referenties in deze sectie.

7.  Selecteer **OK** en wachten op Hallo nieuwe synchronisatie lid toobe gemaakt en geïmplementeerd.

    ![Nieuw lid van de SQL-Database-synchronisatie is toegevoegd](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a>Toevoegen van een lokale SQL Server-database.

In Hallo **Liddatabase** sectie eventueel een lokale SQL Server-groep voor synchronisatie van toohello toevoegen door te selecteren **toevoegen van een On-Premises Database**. Hallo **configureren On-Premises** blade wordt geopend.

Op Hallo **configureren On-Premises** blade volgende dingen Hallo:

1.  Selecteer **Kies Hallo Sync-Agent Gateway**. Hallo **Sync-Agent Selecteer** blade wordt geopend.

    ![Kies Hallo sync-agent-gateway](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  Op Hallo **Kies Hallo Sync-Agent Gateway** blade kiezen of een bestaande agent toouse of maak een nieuwe agent.

    Als u hebt gekozen **bestaande agents**, selecteer de bestaande agent uit de lijst Hallo Hallo.

    Als u hebt gekozen **maken van een nieuwe agent**, volgende dingen Hallo:

    1.  Synchronisatie Hallo-agent clientsoftware downloaden uit Hallo koppeling en installeer deze op Hallo-computer waarop SQL Server Hallo zich bevindt.
 
        > [!IMPORTANT]
        > U hebt tooopen uitgaande TCP-poort 1433 Hallo firewall toolet Hallo client agent communiceren met Hallo-server.


    2.  Voer een naam voor Hallo-agent.

    3.  Selecteer **maken en sleutel genereren**.

    4.  Hallo agent sleutel toohello Klembord kopiëren.
        
        ![Maken van een nieuwe sync-agent](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  Selecteer **OK** tooclose hello **Sync-Agent Selecteer** blade.

    6.  Zoek en Hallo Sync-Agent voor Client-app uitvoeren op Hallo SQL Server-computer.

        ![Hallo gegevens synchroniseren client agent-app](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  Selecteer in de Hallo sync-agent app **Agentcode indienen**. Hallo **synchroniseren metagegevens databaseconfiguratie** dialoogvenster wordt geopend.

    8.  In Hallo **synchroniseren metagegevens databaseconfiguratie** in het dialoogvenster Plakken in Hallo agent sleutel is gekopieerd uit hello Azure-portal. Bieden ook Hallo van bestaande referenties voor hello Azure SQL Database-server op welke Hallo metagegevensdatabase zich bevindt. (Als u een nieuwe metagegevensdatabase gemaakt, wordt deze database is op Hallo dezelfde server als Hallo hub-database.) Selecteer **OK** en wachten op Hallo configuratie toofinish.

        ![Hallo agent sleutel- en referenties invoeren](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   Als u een Firewallfout op dit moment krijgt, hebt u op toocreate een firewallregel op Azure tooallow inkomend verkeer van Hallo SQL Server-computer. U kunt Hallo regel maken in Hallo-portal, maar soms is het eenvoudiger toocreate het in SQL Server Management Studio (SSMS). Probeer in SSMS, tooconnect toohello hub-database in Azure. Voer de naam als \<hub_database_name\>. database.windows.net. Volg de stappen Hallo in Hallo dialoogvenster vak tooconfigure hello Azure firewallregel. Ga vervolgens terug toohello Sync-Agent voor Client-app.

    9.  Klik in Hallo Sync-Agent voor Client-app op **registreren** tooregister SQL Server-database met Hallo-agent. Hallo **SQL Server-configuratiebestand** dialoogvenster wordt geopend.

        ![Toevoegen en configureren van een SQL Server-database](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. In Hallo **SQL Server-configuratiebestand** dialoogvenster Kies of tooconnect met behulp van SQL Server-verificatie of Windows-verificatie. Als u SQL Server-verificatie hebt gekozen, voert u bestaande Hallo-referenties. Geef Hallo SQL Server-naam en Hallo-naam van Hallo-database die u toosync wilt. Selecteer **verbinding testen** tootest uw instellingen. Selecteer vervolgens **opslaan**. Hallo geregistreerde database weergegeven in de lijst Hallo.

        ![SQL Server-database is nu geregistreerd.](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. U kunt nu Hallo Sync-Agent voor Client-app sluiten.

    12. In de portal Hallo op Hallo **configureren On-Premises** blade Selecteer **Selecteer Hallo Database.** Hallo **Database selecteren** blade wordt geopend.

    13. Op Hallo **Database selecteren** blade in Hallo **Sync lidnaam** veld, Geef een naam op voor de nieuwe synchronisatie lid Hallo. Deze naam is niet hetzelfde Hallo-naam van het Hallo-database zelf. Hallo-database selecteren op Hallo-lijst. In Hallo **Sync richtingen** bidirectionele Sync, toohello Hub, selecteer of van Hallo Hub.

        ![Selecteer Hallo op de lokale database.](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. Selecteer **OK** tooclose hello **Database selecteren** blade. Selecteer vervolgens **OK** tooclose hello **configureren On-Premises** blade en wacht Hallo nieuwe synchroniseren lid toobe gemaakt en geïmplementeerd. Tot slot op **OK** tooclose hello **sync leden selecteren** blade.

        ![Op de lokale database toosync groep toegevoegd](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  tooconnect tooSQL synchroniseren van gegevens en lokale Hallo-agent, de gebruikersrol van de naam-toohello toevoegen `DataSync_Executor`. Synchroniseren van gegevens wordt deze rol op Hallo SQL Server-exemplaar gemaakt.

## <a name="step-3---configure-sync-group"></a>Stap 3 - groep voor synchronisatie configureren

Nadat de nieuwe synchronisatie Hallo-groepsleden worden gemaakt en geïmplementeerd, stap 3 **groep voor synchronisatie configureren**, is gemarkeerd in Hallo **groep voor synchronisatie met nieuwe** blade.

1.  Op Hallo **tabellen** blade, selecteer een database uit de lijst Hallo van synchronisatie leden en selecteer vervolgens **schema vernieuwen**.

2.  Selecteer in de Hallo lijst met beschikbare tabellen, Hallo tabellen die u toosync wilt.

    ![Selecteer tabellen toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  Standaard worden alle kolommen in tabel Hallo geselecteerd. Als u niet toosync wilt Hallo alle kolommen, uitschakelen Hallo selectievakje voor dat u niet dat toosync wilt Hallo-kolommen. Zorg ervoor dat tooleave Hallo primaire-sleutelkolom geselecteerd.

    ![Velden selecteren toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  Tot slot selecteert **opslaan**.

## <a name="next-steps"></a>Volgende stappen
Gefeliciteerd. U kunt een groep voor synchronisatie met zowel een exemplaar van SQL-Database en SQL Server-database hebt gemaakt.

Zie voor meer informatie over SQL-Database en synchroniseren van de SQL-gegevens:

-   [Hallo volledige gegevenssynchronisatie SQL technische documentatie downloaden](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [Hallo SQL gegevens synchroniseren REST-API-documentatie downloaden](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [Overzicht van de SQL-Database](sql-database-technical-overview.md)
-   [Database-levenscyclusbeheer](https://msdn.microsoft.com/library/jj907294.aspx)
