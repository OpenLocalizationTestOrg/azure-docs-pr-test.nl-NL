---
title: aaaUse Powershell tooset waarschuwingen in Application Insights | Microsoft Docs
description: Configuratie van Application Insights tooget e-mailberichten over metrische wijzigingen automatiseren.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a>Gebruik PowerShell tooset waarschuwingen in Application Insights
U kunt de configuratie Hallo van automatiseren [waarschuwingen](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).

Bovendien kunt u [webhooks tooautomate uw antwoord tooan waarschuwing instellen](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

> [!NOTE]
> Als u wilt toocreate bronnen en waarschuwingen op Hallo dezelfde tijd, overweeg dan [met een Azure Resource Manager-sjabloon](app-insights-powershell.md).
>
>

## <a name="one-time-setup"></a>Eenmalige instelling
Als u dit nog niet hebt PowerShell met uw Azure-abonnement voordat gebruikt:

Hello Azure Powershell-module installeren op Hallo machine waar u toorun Hallo scripts.

* Installeer [Microsoft Web Platform Installer (v5 of hoger)](http://www.microsoft.com/web/downloads/platform.aspx).
* Deze tooinstall Microsoft Azure Powershell gebruiken

## <a name="connect-tooazure"></a>Verbinding maken met tooAzure
Open Azure PowerShell en [tooyour abonnement verbinding](/powershell/azure/overview):

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a>Ontvang waarschuwingen
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a>Waarschuwing toevoegen
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a>Voorbeeld 1
Stuur mij een e-mail als Hallo-server antwoord tooHTTP aanvragen, meer dan 5 minuten, een gemiddelde waarde is lager dan 1 seconde. Mijn Application Insights-resource IceCreamWebApp wordt genoemd en is in de resourcegroep Fabrikam. Ik ben eigenaar Hallo Hallo Azure-abonnement.

Hallo GUID is Hallo abonnements-ID (geen Hallo instrumentatiesleutel van de toepassing hello).

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a>Voorbeeld 2
Ik heb een toepassing die ik gebruik [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport een waarde met de naam 'salesPerHour'. Een e-mail sturen toomy collega's als 'salesPerHour' onder de 100, meer dan 24 uur een gemiddelde waarde komt.

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

Hallo dezelfde regel kan worden gebruikt voor de metriek Hallo gerapporteerd via Hallo [meting parameter](app-insights-api-custom-events-metrics.md#properties) van bijhouden van een andere aanroep zoals TrackEvent of trackPageView.

## <a name="metric-names"></a>De namen van de metrische gegevens
| Metrische naam | De schermnaam van het | Beschrijving |
| --- | --- | --- |
| `basicExceptionBrowser.count` |Browseruitzonderingen |Het aantal niet-onderschepte uitzonderingen in de browser Hallo. |
| `basicExceptionServer.count` |Serveruitzonderingen |Aantal niet-verwerkte uitzonderingen door Hallo-app |
| `clientPerformance.clientProcess.value` |Verwerkingstijd van de client |Tijd tussen ontvangst Hallo laatste byte van een document totdat Hallo DOM wordt geladen. Asynchrone aanvragen kunnen nog worden verwerkt. |
| `clientPerformance.networkConnection.value` |Paginalaadtijd netwerk verbinding maken |Tijd Hallo browser duurt tooconnect toohello netwerk. Kan niet 0 zijn als in de cache. |
| `clientPerformance.receiveRequest.value` |Ontvangende reactietijd |Tijd tussen de browser aanvraag toostarting tooreceive reactie wordt verzonden. |
| `clientPerformance.sendRequest.value` |Aanvraagtijd verzenden |De tijd die een aanvraag toosend browser. |
| `clientPerformance.total.value` |Laadtijd van browserpagina |Tijd vanaf gebruikersaanvraag totdat DOM, opmaakmodellen, scripts en afbeeldingen zijn geladen. |
| `performanceCounter.available_bytes.value` |Beschikbaar geheugen |Fysiek geheugen die direct beschikbaar is voor een proces of voor systeemgebruik. |
| `performanceCounter.io_data_bytes_per_sec.value` |Verwerkingssnelheid van i/o |Totaal aantal bytes per tweede gelezen en geschreven toofiles, netwerk en apparaten. |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |snelheid van de uitzondering |Uitzonderingen per seconde. |
| `performanceCounter.percentage_processor_time.value` |Proces CPU |Hallo percentage verstreken tijd van alle procesthreads die worden gebruikt door Hallo processor tooexecution instructies voor het toepassingsproces Hallo. |
| `performanceCounter.percentage_processor_total.value` |Tijd van processor |Hallo percentage tijd dat de processor Hallo doorbrengt in niet-inactieve threads. |
| `performanceCounter.process_private_bytes.value` |Eigen bytes van proces |Geheugen exclusief toegewezen toohello bewaakt processen van de toepassing. |
| `performanceCounter.request_execution_time.value` |Uitvoeringstijd voor ASP.NET-aanvraag |Uitvoeringstijd van de meest recente aanvraag Hallo. |
| `performanceCounter.requests_in_application_queue.value` |ASP.NET-aanvragen in wachtrij voor uitvoering |Lengte van de wachtrij voor toepassingsaanvragen en Hallo. |
| `performanceCounter.requests_per_sec.value` |Snelheid van aanvragen voor ASP.NET |De snelheid van alle aanvragen toohello toepassing per seconde van ASP.NET. |
| `remoteDependencyFailed.durationMetric.count` |Afhankelijkheid fouten |Het aantal mislukte aanroepen van de toepassing hello-tooexternal serverbronnen. |
| `request.duration` |Serverreactietijd |Tijd tussen ontvangst van een HTTP-aanvraag en antwoord Hallo verzenden is voltooid. |
| `request.rate` |Snelheid van aanvragen voor |De snelheid van alle aanvragen toohello toepassing per seconde. |
| `requestFailed.count` |Mislukte aanvragen |Aantal HTTP-aanvragen dat heeft geresulteerd in een responscode > = 400 |
| `view.count` |Paginaweergaven |Het aantal aanvragen van clientgebruikers voor webpagina's. Synthetisch verkeer is gefilterd. |
| {uw aangepaste metrische naam} |{De naam van de meetwaarde} |De waarde van de metrische gegevens die zijn gerapporteerd door [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) of in Hallo [metingen parameter van een aanroep van bijhouden](app-insights-api-custom-events-metrics.md#properties). |

Hallo metrische gegevens worden verzonden door verschillende telemetrie modules:

| Metrische groep | Module collector |
| --- | --- |
| basicExceptionBrowser,<br/>clientPerformance,<br/>weergeven |[Browser JavaScript](app-insights-javascript.md) |
| performanceCounter |[Prestaties](app-insights-configuration-with-applicationinsights-config.md) |
| remoteDependencyFailed |[Afhankelijkheid](app-insights-configuration-with-applicationinsights-config.md) |
| aanvraag,<br/>requestFailed |[Serveraanvraag](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a>Webhooks.
U kunt [automatiseren uw antwoord tooan waarschuwing](../monitoring-and-diagnostics/insights-webhooks-alerts.md). Azure belt een webadres van uw keuze wanneer een waarschuwing wordt gegenereerd.

## <a name="see-also"></a>Zie ook
* [Script tooconfigure Application Insights](app-insights-powershell-script-create-resource.md)
* [Application Insights en test webbronnen van sjablonen maken](app-insights-powershell.md)
* [Koppeling van Microsoft Azure Diagnostics tooApplication Insights automatiseren](app-insights-powershell-azure-diagnostics.md)
* [Uw antwoord tooan waarschuwing automatiseren](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
