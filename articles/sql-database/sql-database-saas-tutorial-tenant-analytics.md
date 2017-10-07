---
title: aaaRun analytics query's op meerdere Azure SQL-databases | Microsoft Docs
description: Gegevens ophalen uit de tenant-databases in een database analytics voor offline-analyse
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
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a>Gegevens ophalen uit de tenant-databases in een database analytics voor offline-analyse

In deze zelfstudie maakt u een taak elastische toorun een query uitgevoerd op elke tenant-database. Hallo taak ticket verkoopgegevens extraheert en laadt deze in een analytics-database (of het datawarehouse) voor analyse. Hallo analytics-database is vervolgens tooextract inzicht in deze dagelijkse operationele gegevens van alle tenants opgevraagd.


In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Hallo tenant analytics-database maken
> * Een geplande taak tooretrieve gegevens maken en vullen Hallo analytics-database

toocomplete in deze zelfstudie, zorg ervoor dat Hallo volgende vereisten wordt voldaan:

* Hallo Wingtip SaaS-app wordt geïmplementeerd. Zie toodeploy in minder dan vijf minuten [implementeren en verkennen Hallo Wingtip SaaS-toepassing](sql-database-saas-tutorial.md)
* Azure PowerShell is geïnstalleerd. Zie [Aan de slag met Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps) voor meer informatie.
* Hallo meest recente versie van SQL Server Management Studio (SSMS) is geïnstalleerd. [SSMS downloaden en installeren](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a>Operational Analytics-patroon van tenant

Een van de grote kansen Hallo met SaaS-toepassingen is toouse Hallo uitgebreide tenant gegevens die zijn opgeslagen in de cloud Hallo. Gebruik deze gegevens toogain inzichten Hallo bewerking en het gebruik van uw toepassing en uw tenants. Deze gegevens kunt leiden functie ontwikkeling, bruikbaarheid verbeteringen en andere investeringen in Hallo-app en -platform. U kunt gemakkelijk toegang tot deze gegevens krijgen in een database met meerdere tenants, maar dit is niet zo gemakkelijk als de gegevens op schaal zijn gedistribueerd over misschien wel duizenden databases. Een benadering tooaccessing deze gegevens zijn toouse elastische taken, waarmee de queryresultaten retourneren van resultaat van taak uitvoering toobe vastgelegd in een Uitvoerdatabase en tabel.

## <a name="get-hello-wingtip-application-scripts"></a>Hallo Wingtip toepassingsscripts ophalen

Hallo Wingtip SaaS-scripts en broncode van toepassing zijn beschikbaar in Hallo [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github-opslagplaats. [Stappen toodownload Hallo Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="deploy-a-database-for-tenant-analytics-results"></a>Implementeer een database voor de analytics-resultaten van de tenant

Deze zelfstudie moet u een database geïmplementeerde toocapture Hallo resultaat is van een taak uitvoeren van scripts query's retourneren van resultaten bevatten toohave. We maken hiervoor een database met de naam tenantanalytics.

1. Open... \\Learning-Modules\\operationele Analytics\\Tenant Analytics\\*Demo TenantAnalyticsDB.ps1* in Hallo *PowerShell ISE* en instellen Hallo waarde te volgen:
   * **$DemoScenario** = **2** *Operational analytics-database implementeren*
1. Druk op **F5** toorun hello demoscript (die Hallo aanroepen *implementeren TenantAnalyticsDB.ps1* script) die Hallo tenant analytics-database wordt gemaakt.

## <a name="create-some-data-for-hello-demo"></a>Sommige gegevens voor Hallo demo maken

1. Open... \\Learning-Modules\\operationele Analytics\\Tenant Analytics\\*Demo TenantAnalyticsDB.ps1* in Hallo *PowerShell ISE* en instellen Hallo waarde te volgen:
   * **$DemoScenario** = **1** *Tickets kopen voor voorstellingen bij alle theaters*
1. Druk op **F5** toorun Hallo script en ticket Historie inkoop te maken.


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a>Maken van een geplande taak tooretrieve tenant analytics over ticket aankopen

Dit script maakt een taak tooretrieve ticket-aankoopgegevens van alle tenants. Zodra samengevoegd in één tabel, kunt u uitgebreide begrijpelijke manier mee metrische gegevens over ticket patronen aanschaffen via Hallo tenants toegang.

1. Open SSMS en verbind toohello catalogus -&lt;gebruiker&gt;. database.windows.net server
1. Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*
1. Wijzig &lt;gebruiker&gt;, gebruik Hallo-gebruikersnaam gebruikt wanneer u geïmplementeerd Hallo Wingtip SaaS app Hallo boven aan het Hallo-script **sp\_toevoegen\_doel\_groep\_lid** en **sp\_toevoegen\_taakstap**
1. Klik met de rechtermuisknop, selecteer **verbinding**, en maak verbinding toohello catalogus -&lt;gebruiker&gt;. database.windows.net server, indien nog niet verbonden
1. Zorg ervoor dat u bent verbonden toohello **jobaccount** database en druk op **F5** Hallo-script uit te voeren

* **SP\_toevoegen\_doel\_groep** Hallo doelgroepnaam maakt *TenantGroup*, nu we tooadd doelleden moeten.
* **SP\_toevoegen\_doel\_groep\_lid** voegt een *server* doeltype lid, die alle databases binnen die server (Opmerking Dit is Hallo customer1 - acht &lt;Gebruiker&gt; -server op Hallo tenant databases met) op het moment van taak uitvoering moet worden opgenomen in Hallo-taak.
* **sp\_add\_job** maakt een nieuwe wekelijks geplande taak met de naam “Ticket Purchases from all Tenants”
* **SP\_toevoegen\_taakstap** Hallo taakstap met T-SQL-opdracht tekst tooretrieve alle aankoopgegevens voor Hallo ticket maakt van alle tenants en kopiëren Hallo retourneren resultaten in een tabel met de naam  *AllTicketsPurchasesfromAllTenants*
* Hallo resterende weergaven in Hallo script weergegeven Hallo bestaan Hallo-objecten en uitvoeren van de monitor-taak. Bekijk Hallo statuswaarde van Hallo **lifecycle** kolom toomonitor Hallo status. Eenmaal is voltooid, Hallo-taak is voltooid voor alle databases van de tenant en hello twee extra databases met Hallo verwijzen naar tabel.

Correct functioneert Hallo script moet resulteren in vergelijkbare resultaten:

![resultaten](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a>Een taak tooretrieve samenvatting aantal ticket van alle tenants koopt maken

Dit script maakt een taak tooretrieve som van alle ticket aankopen van alle tenants.

1. Open van SSMS en maak verbinding toohello *catalogus -&lt;gebruiker&gt;. database.windows.net* server
1. Open Hallo bestand... \\Learning-Modules\\inrichten en catalogus\\operationele Analytics\\Tenant Analytics\\*resultaten TicketPurchasesfromAllTenants.sql*
1. Wijzig &lt;gebruiker&gt;, gebruik Hallo-gebruikersnaam gebruikt wanneer u geïmplementeerd in Hallo-script in Hallo Hallo Wingtip SaaS-app **sp\_toevoegen\_taakstap** opgeslagen procedure
1. Klik met de rechtermuisknop, selecteer **verbinding**, en maak verbinding toohello catalogus -&lt;gebruiker&gt;. database.windows.net server, indien nog niet verbonden
1. Zorg ervoor dat u bent verbonden toohello **tenantanalytics** database en druk op **F5** Hallo-script uit te voeren

Correct functioneert Hallo script moet resulteren in vergelijkbare resultaten:

![resultaten](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* **sp\_add\_job** maakt een nieuwe wekelijks geplande taak met de naam “ResultsTicketsOrders”

* **SP\_toevoegen\_taakstap** Hallo taakstap met T-SQL-opdracht tekst tooretrieve alle aankoopgegevens voor Hallo ticket maakt van alle tenants en kopiëren Hallo retourneren resultaten in een tabel met de naam CountofTicketOrders

* Hallo resterende weergaven in Hallo script weergegeven Hallo bestaan Hallo-objecten en uitvoeren van de monitor-taak. Bekijk Hallo statuswaarde van Hallo **lifecycle** kolom toomonitor Hallo status. Eenmaal is voltooid, Hallo-taak is voltooid voor alle databases van de tenant en hello twee extra databases met Hallo verwijzen naar tabel.


## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u het volgende geleerd:

> [!div class="checklist"]
> * U hebt een tenant analytics-database geïmplementeerd
> * Een geplande taak tooretrieve analytische gegevens maken voor tenants

Gefeliciteerd.

## <a name="additional-resources"></a>Aanvullende bronnen

* Aanvullende [zelfstudies waarin voort op Hallo Wingtip SaaS-toepassing bouwen](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Elastische taken](sql-database-elastic-jobs-overview.md)
