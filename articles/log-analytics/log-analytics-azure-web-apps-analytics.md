---
title: aaaView analytische gegevens van Azure Web Apps | Microsoft Docs
description: U kunt hello Azure Web Apps Analytics-oplossing toogain insights over uw Azure-Web-Apps gebruiken door het verzamelen van verschillende metrische gegevens over alle resources in uw Azure-Web-App.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 20ff337f-b1a3-4696-9b5a-d39727a94220
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: banders
ms.openlocfilehash: 7e9725f95c9faf01da89184975ad5444dd19ff95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-analytic-data-for-metrics-across-all-your-azure-web-app-resources"></a>Analytische gegevens weergeven voor de metrische gegevens over alle resources in uw Azure-Web-App

![Symbool van Web-Apps](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-symbol.png)  
Hello Azure Web Apps Analytics (Preview)-oplossing biedt inzicht in uw [Azure Web Apps](../app-service-web/app-service-web-overview.md) door het verzamelen van verschillende metrische gegevens over alle resources in uw Azure-Web-App. U kunt met Hallo-oplossing, analyseren en zoeken naar metrische gegevens van web-app resource.

Hallo-oplossing met, vindt u de:

- Bovenste Web-Apps met de hoogste reactietijd Hallo
- Het aantal aanvragen in uw Web-Apps, met inbegrip van geslaagde en mislukte aanvragen
- Bovenste Web-Apps met de hoogste binnenkomend en uitgaand verkeer
- Bovenste serviceplannen met hoog gebruik van CPU en geheugen
- Azure Web Apps activiteit logboek-bewerkingen

## <a name="connected-sources"></a>Verbonden bronnen

In tegenstelling tot de meeste andere Log Analytics-oplossingen, is niet gegevens voor Azure Web Apps verzameld door agents. Alle gegevens die worden gebruikt door Hallo oplossing komt rechtstreeks uit Azure.

| Verbonden bron | Ondersteund | Beschrijving |
| --- | --- | --- |
| [Windows-agents](log-analytics-windows-agents.md) | Nee | Hallo oplossing verzamelt geen informatie van Windows-agents. |
| [Linux-agents](log-analytics-linux-agents.md) | Nee | Hallo-oplossing worden geen gegevens verzameld van Linux-agents. |
| [SCOM-beheergroep](log-analytics-om-agents.md) | Nee | Hallo-oplossing worden geen gegevens verzameld van agents in een verbonden SCOM-beheergroep. |
| [Azure Storage-account](log-analytics-azure-storage.md) | Nee | Hallo-oplossing heeft geen gegevens naar Azure storage. |

## <a name="prerequisites"></a>Vereisten

- tooaccess metrische resourcegegevens Azure-Web-App, moet u een Azure-abonnement hebben.

## <a name="configuration"></a>Configuratie

Volgende stappen tooconfigure hello Azure Web Apps Analytics-oplossing voor uw werkruimten Hallo uitvoeren.

1. Inschakelen van hello Azure Web Apps Analytics-oplossing van [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) of met behulp van Hallo procedure beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).
2. [Inschakelen van Azure-resource metrische gegevens logboekregistratie tooOMS met behulp van PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell).

Hello Azure Web Apps Analytics-oplossing worden verzameld van twee sets van metrische gegevens van Azure:

- Azure Web Apps metrische gegevens
  - Gemiddelde geheugen werkset
  - Gemiddelde reactietijd
  - Ontvangen/verzonden bytes
  - CPU-tijd
  - Aanvragen
  - Geheugen werkset
  - Httpxxx
- App Service-Plan metrische gegevens
  - Ontvangen/verzonden bytes
  - CPU-percentage
  - Wachtrijlengte voor schijf
  - HTTP-wachtrijlengte
  - Geheugenpercentage

App Service Plan metrische gegevens worden alleen verzameld als u van een specifieke service-abonnement gebruikmaakt. Dit is niet van toepassing toofree of shared App Service-abonnementen.

Als u Hallo-oplossing met behulp van de OMS-portal Hallo toevoegt, ziet u Hallo volgende tegel. U moet te[inschakelen van Azure-resource metrische gegevens logboekregistratie tooOMS met behulp van PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell).

![Melding van de Assessment uitvoeren](./media/log-analytics-azure-web-apps-analytics/performing-assessment.png)

Nadat u Hallo oplossing hebt geconfigureerd, gegevens moet worden gestart stromende tooyour werkruimte binnen 15 minuten.

## <a name="using-hello-solution"></a>Met behulp van Hallo-oplossing

Wanneer u hello Azure Web Apps Analytics-oplossing tooyour werkruimte toevoegt, Hallo **Azure Web Apps Analytics** tegel tooyour Overzichtsdashboard is toegevoegd. Deze tegel wordt weergegeven voor een aantal hello Azure Web Apps dat Hallo-oplossing heeft voor toegang tot tooin uw Azure-abonnement.

![Azure Web Apps Analytics tegel](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-tile.png)

### <a name="view-azure-web-apps-analytics-information"></a>Azure Web Apps Analytics informatie weergeven

Klik op Hallo **Azure Web Apps Analytics** tegel tooopen hello **Azure Web Apps Analytics** dashboard. Hallo dashboard bevat Hallo blades Hallo volgende tabel. Elke blade geeft een lijst van tooten items die overeenkomen met die van de blade criteria voor Hallo bereik en tijdbereik opgegeven. U kunt een logboek-zoekquery waarmee alle records door te klikken op uitvoeren **alle** onderin Hallo van Hallo-blade of door te klikken op Hallo blade-header.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| Kolom | Beschrijving |
| --- | --- |
| Azure Webapps |   |
| Web-Apps aanvraag Trends | Toont een lijndiagram Hallo trend van Web-Apps-aanvraag voor Hallo datumbereik dat u hebt geselecteerd en bevat een overzicht van Hallo top tien webaanvragen aangegeven. Klik op Hallo regel grafiek toorun logboek zoekt<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* (MetricName=Requests OR MetricName=Http*) &#124; measure avg(Average) by MetricName interval 1HOUR</code> <br>Klik op een webserver aanvraag item toorun logboek zoekt Hallo web aanvraag metrische trend die aanvragen. |
| Reactietijd van Web-Apps | Toont een lijndiagram van Hallo Web-Apps-reactietijd voor Hallo datumbereik dat u hebt geselecteerd. Ook bevat een overzicht van een lijst met Hallo top tien Web Apps antwoord time-out. Klik op Hallo grafiek toorun logboek zoekt<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* MetricName="AverageResponseTime" &#124; measure avg(Average) by Resource interval 1HOUR</code><br> Klik op een Web-App toorun een logboek zoekopdracht responstijden voor Web-App Hallo retourneren. |
| Verkeer van Web-Apps | Geeft een lijndiagram voor verkeer van de Web-Apps, in MB en lijsten Hallo boven verkeer van de Web-Apps. Klik op Hallo grafiek toorun logboek zoekt<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"*  MetricName=BytesSent OR BytesReceived &#124; measure sum(Average) by Resource interval 1HOUR</code><br> Deze bevat alle Web-Apps met verkeer voor Hallo laatste minuut. Klik op een Web-App toorun een logboek zoekopdracht met bytes ontvangen en verzonden voor Hallo Web-App. |
| Azure App Service-plannen |   |
| App Service-plannen met CPU-gebruik &gt; 80% | Toont Hallo totale aantal App Service-abonnementen die CPU-gebruik is groter dan 80% en lijsten Hallo top 10-App Service-plannen door CPU-gebruik hebben. Klik op Hallo totale gebied toorun logboek zoekt<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=CpuPercentage &#124; measure Avg(Average) by Resource</code><br> Het bevat een overzicht van uw App Service-abonnementen en het gemiddelde CPU-gebruik. Klik op een App Service-Plan toorun een logboek zoeken met de gemiddelde CPU-gebruik. |
| App Service-plannen met geheugengebruik &gt; 80% | Toont Hallo totale aantal App Service-abonnementen die groter is dan 80% en lijsten Hallo top 10-App Service-plannen door geheugengebruik geheugengebruik hebben. Klik op Hallo totale gebied toorun logboek zoekt<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=MemoryPercentage &#124; measure Avg(Average) by Resource</code><br> Het bevat een overzicht van uw App Service-abonnementen en hun gemiddelde geheugengebruik. Klik op een App Service-Plan toorun een logboek zoeken met het gemiddelde geheugengebruik. |
| Activiteitenlogboeken Azure-Web-Apps |   |
| Azure-Web-Apps activiteit Audit | Toont Hallo totaal aantal Web-Apps met [activiteitenlogboeken](log-analytics-activity.md) en lijsten Hallo logboekbewerkingen voor top 10 activiteit. Klik op Hallo totale gebied toorun logboek zoekt<code>Type=AzureActivity ResourceProvider= "Azure Web Sites" &#124; measure count() by OperationName</code><br> Het bevat een overzicht van Hallo logboekbewerkingen voor de activiteit. Klik op een activiteit logboek bewerking toorun een zoekopdracht logboek met een lijst met records Hallo voor Hallo-bewerking. |



### <a name="azure-web-apps"></a>Azure Web Apps

In het Hallo-dashboard kunt u inzoomen tooget meer inzicht in de metrische gegevens van uw Web-Apps. Deze eerste set blades weergeven Hallo trend van Hallo-aanvragen voor Web-Apps, aantal fouten (bijvoorbeeld HTTP404), verkeer en gemiddelde reactietijd gedurende een bepaalde periode. U ziet ook een verdeling van deze metrische gegevens voor verschillende Web-Apps.

![Azure Webapps blades](./media/log-analytics-azure-web-apps-analytics/web-apps-dash01.png)

Een primaire reden voor het weergeven van die gegevens is zodat u kunt een Web-App met hoge responstijd identificeren en toofind Hallo hoofdoorzaak onderzoeken. Een drempellimiet is ook toegepaste toohelp meer gemakkelijk herkennen Hallo toepassingsgroepen met problemen.

- Web-Apps in rood weergegeven hebben reactietijd hoger is dan 1 seconde.
- Web-Apps weergegeven in oranje hebben een reactietijd hoger is dan 0,7 seconde en minder dan 1 seconde.
- Web-Apps in het groen weergegeven hebben een reactietijd kleiner is dan 0,7 tweede.

In Hallo logboek afbeelding van zoekfunctie in voorbeeld te volgen, ziet u dat Hallo *anugup3* web-app heeft een veel hoger reactietijd dan Hallo andere web-apps.

![Voorbeeld van logboek zoeken](./media/log-analytics-azure-web-apps-analytics/web-app-search-example.png)

### <a name="app-service-plans"></a>App Service-abonnementen

Als u speciale serviceplannen gebruikt, kunt u ook metrische gegevens verzamelen voor uw App Service-abonnementen. In deze weergave ziet u uw App Service-abonnementen met hoog CPU of geheugen gebruik (&gt; 80%). Ook ziet u Hallo bovenste App services met hoge geheugen of CPU-gebruik. Op deze manier is een limiet drempelwaarde toegepaste toohelp meer gemakkelijk herkennen Hallo toepassingsgroepen met problemen.

- App Service-abonnementen in rood weergegeven, hebt een CPU/geheugengebruik hoger is dan 80%.
- App Service-abonnementen weergegeven in oranje hebben een CPU/geheugengebruik hoger is dan 60% en lager is dan 80%.
- App Service-abonnementen in het groen weergegeven, hebt een lager is dan 60% CPU/geheugen-gebruik.

![Azure App Service-abonnementen blades](./media/log-analytics-azure-web-apps-analytics/web-apps-dash02.png)

## <a name="azure-web-apps-log-searches"></a>Azure Web Apps logboek zoekopdrachten

Hallo **lijst van populaire Azure Web Apps zoekquery's** ziet u alle Hallo activiteitenlogboeken verwante voor Web-Apps, waarmee u inzicht in het Hallo-bewerkingen die zijn uitgevoerd op de resources van uw Web-Apps. Ook worden alle Hallo gerelateerde bewerkingen en Hallo aantal keren dat ze zich hebben voorgedaan.

Met een van de Hallo logboek zoekquery's als uitgangspunt, kunt u gemakkelijk maken een waarschuwing. Bijvoorbeeld, kunt u toocreate een waarschuwing als de gemiddelde reactietijd van een waarde groter dan elke 1 seconde is.

## <a name="next-steps"></a>Volgende stappen

- Maak een [waarschuwing](log-analytics-alerts-creating.md) voor specifieke metrische gegevens.
- Gebruik [logboek zoeken](log-analytics-log-searches.md) tooview gedetailleerde informatie uit de activiteitenlogboeken.
