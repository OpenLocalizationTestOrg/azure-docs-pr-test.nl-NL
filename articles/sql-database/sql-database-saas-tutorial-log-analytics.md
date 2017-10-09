---
title: Log Analytics aaaUse met een SQL-Database multitenant-app | Microsoft Docs
description: Instellen en gebruiken van logboekanalyse (OMS) met hello Azure SQL Database voorbeeld Wingtip SaaS-app
keywords: zelfstudie sql-database
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: billgib; sstein
ms.openlocfilehash: fa9085ce3462939e66853faa2a3cd71e0f6c2581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="setup-and-use-log-analytics-oms-with-hello-wingtip-saas-app"></a>Instellen en gebruiken van logboekanalyse (OMS) met Hallo Wingtip SaaS-app

In deze zelfstudie maakt u instellen en gebruiken *logboekanalyse ([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))* voor het bewaken van elastische pools en databases. Dit is gebaseerd op Hallo [prestatiebewaking en beheer zelfstudie](sql-database-saas-tutorial-performance-monitoring.md), en wordt weergegeven hoe toouse *logboekanalyse* tooaugment Hallo bewaking en waarschuwingen die zijn opgegeven in hello Azure-portal. Logboek Analytics is met name geschikt voor bewaking en waarschuwingen op schaal omdat het ondersteuning biedt voor honderden pools en honderdduizenden databases. Bovendien is het een centrale bewakingsoplossing, met mogelijkheden om bewakingsfuncties van andere toepassingen en Azure-services te integreren. Deze integratie is overigens ook mogelijk voor verschillende Azure-abonnementen.

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Log Analytics (OMS) installeren en configureren
> * Log Analytics toomonitor pools en databases gebruiken

toocomplete in deze zelfstudie, zorg ervoor dat Hallo volgende vereisten zijn voltooid:

* Hallo Wingtip SaaS-app wordt geïmplementeerd. Zie toodeploy in minder dan vijf minuten [implementeren en verkennen Hallo Wingtip SaaS-toepassing](sql-database-saas-tutorial.md)
* Azure PowerShell is geïnstalleerd. Zie [Aan de slag met Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps) voor meer informatie.

Zie Hallo [prestatiebewaking en beheer zelfstudie](sql-database-saas-tutorial-performance-monitoring.md) voor een beschrijving van Hallo SaaS-scenario's en patronen en van invloed op Hallo-vereisten voor een oplossing voor controle.

## <a name="monitoring-and-managing-performance-with-log-analytics-oms"></a>Prestaties bewaken en beheren met Log Analytics (OMS)

Voor SQL Database zijn bewaking en waarschuwingen beschikbaar voor databases en pools. Deze ingebouwde bewaking en waarschuwingen is resource-specifieke en handig voor kleine hoeveelheden van resources, maar is minder geschikt toomonitoring grote installaties of voor het ontwikkelen van een uniform overzicht over de verschillende bronnen en -abonnementen.

Voor scenario's met grote volumes kan Log Analytics worden gebruikt. Dit is een afzonderlijke Azure-service die in analyse via verzonden diagnostische logboeken voorziet en telemetrie verzameld in een log analytics-werkruimte, die telemetrie van veel verzamelen kunt services en gebruikte tooquery en waarschuwingen instellen. Log Analytics beschikt over een ingebouwde querytaal en hulpprogramma's voor gegevensvisualisatie voor analyse en visualisatie van operationele gegevens. Hallo SQL Analytics-oplossing biedt verschillende vooraf gedefinieerde elastische pool en database bewaking en waarschuwingen, weergaven en query's en kunt u uw eigen ad-hocquery's toevoegen en sla deze indien nodig. OMS biedt ook een functie voor het ontwerpen van aangepaste weergaven.

Log Analytics-werkruimten en analytics-oplossingen kunnen worden geopend in hello Azure-portal en in OMS. Hello Azure-portal is Hallo nieuwere toegangspunt maar kan ook achter Hallo OMS-portal in bepaalde gebieden.

### <a name="start-hello-load-generator-toocreate-data-tooanalyze"></a>Hallo load generator toocreate gegevens tooanalyze starten

1. Open **Demo PerformanceMonitoringAndManagement.ps1** in Hallo **PowerShell ISE**. Houd dit script open gewenste toorun verschillende scenario's Hallo load generatie tijdens deze zelfstudie.
1. Als u minder dan vijf tenants hebt, richt u een batch van tenants tooprovide een interessanter bewaking context:
   1. Stel het volgende in: **$DemoScenario = 1,** **Batch met tenants inrichten**
   1. Druk op **F5** toorun Hallo script.

1. Stel het volgende in: **$DemoScenario = 2,** **Belasting met normale intensiteit genereren (ongeveer 40 DTU's)**.
1. Druk op **F5** toorun Hallo script.

## <a name="get-hello-wingtip-application-scripts"></a>Hallo Wingtip toepassingsscripts ophalen

Hallo Wingtip Tickets scripts en broncode van toepassing zijn beschikbaar in Hallo [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github-opslagplaats. Scriptbestanden bevinden zich in Hallo [map Learning-Modules](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules). Hallo downloaden **Learning-Modules** map tooyour lokale computer, onderhouden van de mapstructuur.

## <a name="installing-and-configuring-log-analytics-and-hello-azure-sql-analytics-solution"></a>Log Analytics en hello Azure SQL Analytics-oplossing installeren en configureren

Log Analytics is een afzonderlijke service die toobe geconfigureerd behoeften. Log Analytics verzamelt logboekgegevens en telemetrische en metrische gegevens in een speciale werkruimte voor logboekanalyse. Een werkruimte is een resource, net als andere resources in Azure, en moet eerst worden gemaakt. Tijdens het Hallo-werkruimte gemaakt in Hallo toobe niet hoeft dezelfde resourcegroep als Hallo toepassing(en) die wordt bewaakt, op die manier kunt Hallo verstandig. In geval van Hallo Wingtip SaaS app Hallo hierdoor Hallo werkruimte toobe eenvoudig verwijderd met de toepassing hello door gewoon Hallo resourcegroep te verwijderen.

1. Open... \\Learning-Modules\\prestatiebewaking en beheer\\logboekanalyse\\*Demo LogAnalytics.ps1* in Hallo **PowerShell ISE**.
1. Druk op **F5** toorun Hallo script.

U moet op dit moment kunnen openen logboekanalyse hello Azure-portal (of Hallo OMS-portal). Het duurt enkele minuten duren voordat de telemetrie toobe verzameld in de werkruimte voor logboekanalyse Hallo en toobecome zichtbaar. Hallo langer dat u Hallo systeem verzamelen van gegevens Hallo interessanter Hallo ervaring laten worden. Is een goed moment toograb een drank - alleen Zorg ervoor dat Hallo load generator nog steeds actief is.


## <a name="use-log-analytics-and-hello-sql-analytics-solution-toomonitor-pools-and-databases"></a>Log Analytics gebruiken en Hallo SQL Analytics-oplossing toomonitor pools en databases


In deze oefening, logboekanalyse en toolook Hallo OMS-portal gebruiken op Hallo telemetrie worden verzameld voor het Hallo-databases en pools te openen.

1. Blader toohello [Azure-portal](https://portal.azure.com) en Log Analytics openen door te klikken op meer services, en zoek vervolgens naar logboekanalyse:

   ![Log Analytics openen](media/sql-database-saas-tutorial-log-analytics/log-analytics-open.png)

1. Selecteer Hallo werkruimte met de naam *wtploganalytics -&lt;gebruiker&gt;*.

1. Selecteer **overzicht** tooopen Hallo Log Analytics-oplossing in hello Azure-portal.
   ![koppeling Overzicht](media/sql-database-saas-tutorial-log-analytics/click-overview.png)

    **BELANGRIJKE**: het duurt een paar minuten voordat het Hallo-oplossing actief is. Geduld is een schone zaak.

1. Klik op Hallo Azure SQL Analytics tegel tooopen deze.

    ![overview](media/sql-database-saas-tutorial-log-analytics/overview.png)

    ![analytics](media/sql-database-saas-tutorial-log-analytics/analytics.png)

1. Hallo weergave in Hallo oplossing blade schuift opzij, met een eigen schuifbalk Hallo onderin (Hallo blade vernieuwen indien nodig).

1. Verken Hallo verschillende weergaven door te klikken op deze of op afzonderlijke resources tooopen een inzoomen explorer, waar u tijd Hallo-schuifregelaar in Hallo gebruiken kunt linksboven of klik op in een verticale balk toofocus in op een smaller tijdsegment. Aan deze weergave kunt u afzonderlijke databases of groepen toofocus bepaalde resources selecteren:

    ![grafiek](media/sql-database-saas-tutorial-log-analytics/chart.png)

1. Terug op Hallo oplossing blade als u toohello uiterst rechts schuiven ziet u opgeslagen query's klikt u op tooopen en verkennen. U kunt experimenteren met deze query's door ze aan te passen. Interessante query's kunt u vervolgens opslaan en later gebruiken met andere resources.

1. Selecteer de OMS-Portal tooopen Hallo-oplossing er terug op Hallo logboekanalyse werkruimte blade.

    ![oms](media/sql-database-saas-tutorial-log-analytics/oms.png)

1. U kunt waarschuwingen configureren in Hallo OMS-portal. Klik op de waarschuwing deel van de Hallo van Hallo database DTU weergeven.

1. In Hallo logboek zoeken ziet weergave die wordt weergegeven dat u een staafdiagram van Hallo metrische gegevens die wordt weergegeven.

    ![zoeken in logboeken](media/sql-database-saas-tutorial-log-analytics/log-search.png)

1. Als u op de waarschuwing op Hallo werkbalk klikt wordt u kunnen toosee hello waarschuwingsconfiguratie en deze kunt wijzigen.

    ![waarschuwingsregel toevoegen](media/sql-database-saas-tutorial-log-analytics/add-alert.png)

Hallo bewaking en waarschuwingen in Log Analytics en OMS is gebaseerd op query's over Hallo gegevens in de werkruimte hello, in tegenstelling tot Hallo waarschuwen bij elke resource-blade specifiek voor resource is. Het is dus mogelijk om een waarschuwing te definiëren die voor alle databases geldt, zodat u niet voor elke database afzonderlijk waarschuwingen hoeft te definiëren. U kunt ook een waarschuwing maken die gebruikmaakt van een samengestelde query op meerdere resourcetypen. Query's zijn alleen beperkt door het Hallo-gegevens die beschikbaar zijn in de werkruimte Hallo.

Log Analytics voor SQL-Database wordt in rekening gebracht op basis van Hallo gegevensvolume in Hallo-werkruimte. In deze zelfstudie maakt u gemaakt een gratis werkruimte is beperkt too500MB per dag. Zodra deze limiet is bereikt. worden gegevens niet langer toohello werkruimte toegevoegd.


## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u het volgende geleerd:

> [!div class="checklist"]
> * Log Analytics (OMS) installeren en configureren
> * Log Analytics toomonitor pools en databases gebruiken

[Zelfstudie over tenant-analyse](sql-database-saas-tutorial-tenant-analytics.md)

## <a name="additional-resources"></a>Aanvullende bronnen

* [Aanvullende zelfstudies waarin voort op Hallo initiële Wingtip SaaS-toepassingsimplementatie bouwen](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Azure Log Analytics](../log-analytics/log-analytics-azure-sql.md)
* [OMS](https://blogs.technet.microsoft.com/msoms/2017/02/21/azure-sql-analytics-solution-public-preview/)
