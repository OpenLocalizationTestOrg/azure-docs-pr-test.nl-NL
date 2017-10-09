---
title: aaaRun ad-hocquery analytics's over meerdere Azure SQL-databases | Microsoft Docs
description: Ad-hoc analytics query's via meerdere SQL-databases in Hallo Wingtip SaaS multitenant app uitvoeren.
keywords: zelfstudie sql-database
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: billgib; sstein
ms.openlocfilehash: 140cd51fdd03b5a548147282b51ceb0ad80c944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-ad-hoc-analytics-queries-across-all-wingtip-saas-tenants"></a>Ad-hoc analytics query's uitvoeren op alle Wingtip SaaS-tenants

In deze zelfstudie maakt uitvoeren u gedistribueerde query's op Hallo volledige set van databases van de tenant tooenable ad-hoc analytics. Elastische Query gebruikte tooenable gedistribueerde query's, is hiervoor een extra analytics-database wordt geïmplementeerd (toohello catalogusserver). Deze query's kunnen overspoeld in Hallo dagelijkse operationele gegevens van Hallo Wingtip SaaS app insights extraheren.


In deze zelfstudie komen deze onderwerpen aan bod:

> [!div class="checklist"]

> * Hallo globale weergaven in elke database waardoor efficiënter uitvoeren van query's over tenants
> * Hoe toodeploy een ad-hoc analytics-database
> * Hoe toorun query's verdeeld over alle databases voor tenant



toocomplete in deze zelfstudie, zorg ervoor dat Hallo volgende vereisten zijn voltooid:

* Hallo Wingtip SaaS-app wordt geïmplementeerd. Zie toodeploy in minder dan vijf minuten [implementeren en verkennen Hallo Wingtip SaaS-toepassing](sql-database-saas-tutorial.md)
* Azure PowerShell is geïnstalleerd. Zie [Aan de slag met Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps) voor meer informatie.
* SQL Server Management Studio (SSMS) is geïnstalleerd. toodownload en installeer SSMS, Zie [Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


## <a name="ad-hoc-analytics-pattern"></a>Ad-hoc analytics patroon

Een van de grote kansen Hallo met SaaS-toepassingen is toouse Hallo enorme hoeveelheid tenant gegevens centraal worden opgeslagen in de cloud Hallo. Gebruik deze gegevens toogain inzichten Hallo bewerking en het gebruik van uw toepassing, uw tenants, hun gebruikers, voorkeuren, gedrag, enzovoort. Deze inzichten kunnen leiden functie ontwikkeling, bruikbaarheid verbeteringen en andere investeringen in uw apps en services.

U kunt gemakkelijk toegang tot deze gegevens krijgen in een database met meerdere tenants, maar dit is niet zo gemakkelijk als de gegevens op schaal zijn verdeeld over misschien wel duizenden databases. Een aanpak is toouse [elastische Query](sql-database-elastic-query-overview.md), waardoor query in een gedistribueerde set van databases met algemene schema. Elastische Query gebruikt een enkel *head* database waarin externe tabellen worden gedefinieerd met het mirror-tabellen of weergaven in hello (tenant)-databases wordt gedistribueerd. Query's verzonden toothis head database zijn gecompileerde tooproduce een plan gedistribueerde query met delen van Hallo query omlaag toohello tenant databases gedrukt, indien nodig. Elastische Query gebruikt Hallo shard-toewijzing in Hallo catalogus tooprovide Hallo databaselocatie van Hallo tenant databases. Installatie en query zijn simpel met behulp van standaard [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference), en ondersteuning voor ad-hoc opvragen van hulpprogramma's zoals Power BI en Excel.

Door query's over Hallo tenant databases verdeeld, biedt elastische Query onmiddellijk inzicht in live productiegegevens. Als elastische Query gegevens op uit mogelijk veel databases haalt, verzonden query latentie kan soms hoger zijn dan voor gelijkwaardige query's tooa één multitenant-database. Voorzichtig bij het ontwerpen van query's toominimize Hallo gegevens die worden geretourneerd. Elastische Query is vaak het meest geschikt voor kleine hoeveelheden realtime gegevens opvragen als tegengestelde toobuilding veelgebruikte of complexe analytics query's of rapporten. Als het uitvoeren van query's niet goed, bekijkt hello [uitvoeringsplan](https://docs.microsoft.com/sql/relational-databases/performance/display-an-actual-execution-plan) toosee welk gedeelte van het Hallo-query heeft omlaag toohello externe database en hoeveel gegevens wordt geretourneerd is gedrukt. Query's waarvoor complexe analytische verwerking is wellicht beter afgehandeld in sommige gevallen door tenant-gegevens in te pakken op een specifieke database of het datawarehouse is geoptimaliseerd voor analysequery's. Dit patroon wordt uitgelegd in Hallo [tenant analytics zelfstudie](sql-database-saas-tutorial-tenant-analytics.md). 

## <a name="get-hello-wingtip-application-scripts"></a>Hallo Wingtip toepassingsscripts ophalen

Hallo Wingtip SaaS-scripts en broncode van toepassing zijn beschikbaar in Hallo [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github-opslagplaats. [Stappen toodownload Hallo Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="create-ticket-sales-data"></a>Ticket verkoopgegevens maken

toorun query's op basis van een gegevensset interessanter maken ticket verkoopgegevens met Hallo ticket-generator.

1. In Hallo *PowerShell ISE*Open Hallo... \\Learning-Modules\\operationele Analytics\\ad-hoc Analytics\\*Demo AdhocAnalytics.ps1* script en stel Hallo volgende waarden:
   * **$DemoScenario** = 1, **tickets voor gebeurtenissen op alle plaatsen aanschaffen**.
2. Druk op **F5** Hallo-script uitvoeren en ticket verkoop genereren. Tijdens het Hallo-script wordt uitgevoerd, blijven Hallo stappen in deze zelfstudie. Hallo ticket gegevens query wordt uitgevoerd in Hallo *ad-hoc gedistribueerde query's uitvoeren* sectie, dus als deze nog wordt uitgevoerd als u krijgt dat oefening toothat Hallo ticket generator toocomplete wachten.

## <a name="explore-hello-global-views"></a>Algemene weergaven Hallo verkennen

Hallo Wingtip SaaS-toepassing is gebouwd met behulp van een model tenant per database zodat Hallo tenant-databaseschema vanuit het perspectief van een één-tenant is gedefinieerd. Tenant-specifieke informatie in een tabel bestaat *wilt*, die altijd is één rij en wordt geïmplementeerd als een heap, zonder een primaire sleutel. Andere tabellen in het schema Hallo hoeft niet toobe gerelateerde toohello *wetten* tabel, omdat bij normaal gebruik er nooit twijfel welke tenant Hallo gegevens behoort.

Bij het uitvoeren van query's voor alle databases, is het echter belangrijk dat elastische Query Hallo-gegevens kunnen worden behandeld alsof deze een onderdeel van één logische database shard door tenant is. tooachieve dit een reeks 'global' weergaven zijn toegevoegd toohello tenant-database die een tenant-id in elk van de Hallo-tabellen die zijn opgevraagd globaal project. Bijvoorbeeld, Hallo *VenueEvents* weergave toegevoegd een berekende *VenueId* toohello kolommen geprojecteerd vanuit Hallo *gebeurtenissen* tabel. Met het definiëren van de externe tabel Hallo in Hallo head-database via *VenueEvents* (in plaats van de onderliggende hello *gebeurtenissen* tabel), elastische Query is kunnen toopush omlaag joins op basis van *VenueId* zodat ze kunnen worden uitgevoerd parallel op elke externe database (in plaats van op Hallo head database). Dit vermindert aanzienlijk Hallo en de hoeveelheid gegevens die wordt geretourneerd, wat tot een aanzienlijke toename van de prestaties voor veel query's leidt. Deze globale weergaven zijn vooraf gemaakte in alle databases van de tenant (en in *basetenantdb*).

1. Open SSMS en [verbinding toohello tenants1 -&lt;gebruiker&gt; server](sql-database-wtp-overview.md#explore-database-schema-and-execute-sql-queries-using-ssms).
2. Vouw **Databases**, met de rechtermuisknop op **contosoconcerthall**, en selecteer **nieuwe Query**.
3. Voer Hallo query's tooexplore Hallo verschil tussen Hallo één tenant tabellen en algemene weergaven hello te volgen:

   ```T-SQL
   -- hello base Venue table, that has no VenueId associated.
   SELECT * FROM Venue

   -- Notice hello plural name 'Venues'. This view projects a VenueId column.
   SELECT * FROM Venues

   -- hello base Events table, which has no VenueId column.
   SELECT * FROM Events

   -- This view projects hello VenueId retrieved from hello Venues table.
   SELECT * FROM VenueEvents
   ```

In deze weergaven Hallo *VenueId* wordt berekend, zoals een hash van hello wilt naam maar een benadering gebruikte toointroduce een unieke waarde zijn. Deze aanpak is vergelijkbaar toohello manier Hallo-tenantsleutel wordt berekend voor gebruik in Hallo-catalogus.

tooexamine hello definitie van Hallo *plaatsen* weergeven:

1. In **Objectverkenner**, vouw **contosoconcethall** > **weergaven**:

   ![Weergaven](media/sql-database-saas-tutorial-adhoc-analytics/views.png)

2. Met de rechtermuisknop op **dbo. Plaatsen**.
3. Selecteer **weergeven als een Script** > **maken naar** > **nieuw venster van de Query-Editor**

Script voor Hallo andere *wilt* toosee weergaven hoe ze Hallo toevoegen *VenueId*.

## <a name="deploy-hello-database-used-for-ad-hoc-distributed-queries"></a>Hallo-database gebruikt voor ad-hoc gedistribueerde query's implementeren

In deze oefening implementeert Hallo *adhocanalytics* database. Dit is head Hallo-database met Hallo schema voor het uitvoeren van query's voor alle databases van de tenant. Hallo-database is geïmplementeerde toohello bestaande catalogusserver Hallo-server gebruikt voor alle beheer-gerelateerde databases in Hallo voorbeeld-app.

1. Open... \\Learning-Modules\\operationele Analytics\\ad-hoc Analytics\\*Demo AdhocAnalytics.ps1* in Hallo *PowerShell ISE* en set Hallo de volgende waarden:
   * **$DemoScenario** = 2, **Ad-hoc Analytics-database implementeren**.

2. Druk op **F5** toorun Hallo script en maak Hallo *adhocanalytics* database.

In de volgende sectie hello voegt u schema toohello database zodat deze gebruikt toorun gedistribueerde query's worden kan.

## <a name="configure-hello-database-for-running-distributed-queries"></a>Hallo-database voor het uitvoeren van gedistribueerde query's configureren

In deze oefening voegt schema (Hallo externe gegevensbron en externe tabeldefinities) toohello ad-hoc analytics-database waarmee een query voor alle databases van de tenant.

1. Open SQL Server Management Studio en toohello ad-hoc Analytics-database die u hebt gemaakt in de vorige stap Hallo verbinding. Hallo-naam van de database Hallo is adhocanalytics.
2. Open ...\Learning Modules\Operational Analytics\Adhoc Analytics\ *initialiseren AdhocAnalyticsDB.sql* in SSMS.
3. Bekijk Hallo SQL-script en Let op Hallo volgende:

   Elastische Query gebruikt een database-scoped referentie tooaccess elke Hallo tenant databases. Deze referentie moet toobe beschikbaar in alle Hallo-databases en moet normaal gesproken worden verleend Hallo minimale rechten vereist tooenable deze ad-hocquery's.

    ![referentie maken](media/sql-database-saas-tutorial-adhoc-analytics/create-credential.png)

   Hallo externe gegevensbron die is gedefinieerd toouse hello tenant shard-toewijzing in Hallo catalogusdatabase. Bij gebruik van deze als de externe gegevensbron hello, zijn query's gedistribueerde tooall databases die zijn geregistreerd in de catalogus Hallo wanneer Hallo query wordt uitgevoerd. Omdat servernamen verschillend voor elke implementatie zijn, dit Initialisatiescript Hallo-locatie van Hallo catalogusdatabase opgehaald door op te halen van de huidige server hello (@@servername) waarop Hallo script wordt uitgevoerd.

    ![externe gegevensbron maken](media/sql-database-saas-tutorial-adhoc-analytics/create-external-data-source.png)

   externe tabellen die verwijzen naar Hallo algemene weergaven beschreven in de vorige sectie Hallo en gedefinieerd met Hallo **DISTRIBUTION = SHARDED(VenueId)**. Omdat elke *VenueId* tooa één database, wijst dit verbetert de prestaties voor veel scenario's zoals weergegeven in de volgende sectie Hallo.

    ![externe tabellen maken](media/sql-database-saas-tutorial-adhoc-analytics/external-tables.png)

   Hallo lokale tabel *VenueTypes* die is gemaakt en ingevuld. Deze gegevens verwijzingstabel is gemeenschappelijk in alle databases voor tenant, zodat kan worden weergegeven als een lokale tabel hier en ingevuld met de algemene gegevens Hallo. Voor sommige query's hierdoor Hallo hoeveelheid gegevens verplaatst tussen Hallo tenant databases en Hallo *adhocanalytics* database.

    ![Tabel maken](media/sql-database-saas-tutorial-adhoc-analytics/create-table.png)

   Als u verwijzingsdimensies op deze manier opneemt, worden ervoor tooupdate Hallo-tabelschema en gegevens wanneer u Hallo tenant databases bijwerken.

4. Druk op **F5** toorun Hallo script en Hallo initialiseren *adhocanalytics* database. 

U kunt nu gedistribueerde query's uitvoeren en inzichten te verzamelen over alle huurders!

## <a name="run-ad-hoc-distributed-queries"></a>Ad-hoc gedistribueerde query's uitvoeren

Nu dat Hallo *adhocanalytics* database is ingesteld, gaat u verder gaan en sommige gedistribueerde query's uitvoeren. Hallo-uitvoeringsplan voor een beter begrip van waar de queryverwerking Hallo gebeurt er bevatten. 

Bij de inspectie van Hallo uitvoeringsplan Beweeg de muisaanwijzer over Hallo plan pictogrammen voor meer informatie. 

Belangrijke toonote is die instelling **DISTRIBUTION = SHARDED(VenueId)** wanneer we de externe gegevensbron Hallo gedefinieerd, verbetert de prestaties voor veel scenario's. Omdat elke *VenueId* tooa toegewezen individuele database eenvoudig gereed op afstand, terugkerende alleen Hallo gegevens we moeten filteren is.

1. Open ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalyticsQueries.sql* in SSMS.
2. Zorg ervoor dat u bent verbonden toohello **adhocanalytics** database.
3. Selecteer Hallo **Query** en klik op **werkelijke uitvoeringsplan opnemen**
4. Markeer Hallo *welke plaatsen zijn momenteel geregistreerd?* query en druk op **F5**.

   Hallo query retourneert Hallo gehele wetten lijst ter illustratie van hoe snel en eenvoudig het is tooquery voor alle tenants en gegevens vanaf elke tenant.

   Inspecteer de Hallo-abonnement en dat alle kosten voor Hallo Hallo externe query is omdat we gewoon gaat tooeach tenant-database en hello wilt informatie te selecteren.

   ![Selecteer * uit dbo. Plaatsen](media/sql-database-saas-tutorial-adhoc-analytics/query1-plan.png)

5. De volgende query selecteert Hallo en druk op **F5**.

   Gegevens van Hallo tenant databases en Hallo lokaal lid wordt van deze query *VenueTypes* tabel (lokale computer, zoals deze wordt een tabel in Hallo *adhocanalytics* database).

   Inspecteer de Hallo-plan en Zie dat Hallo meerderheid van de kosten Hallo externe query is omdat we query uitvoeren op elke tenant wilt info (dbo. Plaatsen) en voert u een snelle lokale koppelen met Hallo lokale *VenueTypes* tabel toodisplay Hallo beschrijvende naam.

   ![Lid worden van lokale en externe gegevens](media/sql-database-saas-tutorial-adhoc-analytics/query2-plan.png)

6. Nu selecteren Hallo *op welke dag zijn de meeste tickets verkocht Hallo?* query en druk op **F5**.

   Deze query heeft iets meer complexe lid worden en cumulatie-instellingen. Wat belangrijk toonote is is dat de meeste Hallo verwerking op afstand wordt uitgevoerd, en nogmaals we alleen Hallo rijen die we nodig hebben terugbrengen, slechts één rij voor elke wetten cumulatieve ticket verkoop aantal per dag retourneren.

   ![query](media/sql-database-saas-tutorial-adhoc-analytics/query3-plan.png)


## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u het volgende geleerd:

> [!div class="checklist"]

> * Gedistribueerde query's uitvoeren voor alle databases van de tenant
> * Implementeren van een ad-hoc analytics-database en voeg schema tooit toorun gedistribueerde query's.


Nu proberen Hallo [Tenant Analytics zelfstudie](sql-database-saas-tutorial-tenant-analytics.md) tooexplore gegevens tooa afzonderlijke analytics-database voor complexere analytics verwerking extraheren...

## <a name="additional-resources"></a>Aanvullende bronnen

* Aanvullende [zelfstudies waarin voort op Hallo Wingtip SaaS-toepassing bouwen](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Elastische query](sql-database-elastic-query-overview.md)
