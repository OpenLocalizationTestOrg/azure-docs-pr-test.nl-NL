---
title: waarschuwingen voor Azure-services - PowerShell aaaCreate | Microsoft Docs
description: Trigger e-mailberichten, meldingen, worden URL's van websites (webhooks) of automation aanroepen wanneer Hallo door u opgegeven voorwaarden wordt voldaan.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a>Metrische waarschuwingen in de Azure-Monitor maken voor Azure-services - PowerShell
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Overzicht
Dit artikel laat zien hoe tooset up Azure metriek waarschuwingen met behulp van PowerShell.  

U kunt een waarschuwing op basis van bewaking metrische gegevens voor of gebeurtenissen op uw Azure-services kunt ontvangen.

* **Metrische waarden** - hello triggers waarschuwen wanneer Hallo-waarde van een opgegeven metriek overschrijdt de drempelwaarde die u in beide richtingen toewijst. Dat wil zeggen, deze beide wordt geactiveerd wanneer eerst aan Hallo voorwaarde wordt voldaan en vervolgens later wanneer die voorwaarde wordt niet langer wordt voldaan.    
* **Activiteit logboekgebeurtenissen** -een waarschuwing kunt activeren voor *elke* gebeurtenis of alleen wanneer een bepaalde gebeurtenissen optreden. meer informatie over de activiteit logboek waarschuwingen toolearn [Klik hier](monitoring-activity-log-alerts.md)

Een metriek waarschuwing toodo Hallo volgen wanneer deze wordt geactiveerd, kunt u configureren:

* verzenden van e-mailmeldingen toohello servicebeheerder en medebeheerders
* e-mail verzenden tooadditional e-mails die u opgeeft.
* een webhook aanroepen
* starten van de uitvoering van een Azure-runbook (alleen van hello Azure-portal)

U kunt configureren en informatie ophalen over met behulp van regels voor waarschuwingen

* [Azure Portal](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [opdrachtregelinterface (CLI)](insights-alerts-command-line-interface.md)
* [Monitor voor Azure REST-API](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Voor meer informatie, kunt u altijd typen ```Get-Help``` en vervolgens Hallo PowerShell-opdracht op het gewenste help.

## <a name="create-alert-rules-in-powershell"></a>Maken van regels voor waarschuwingen in PowerShell
1. Meld u bij tooAzure.   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. Een lijst met abonnementen Hallo er beschikbaar zijn. Controleer of u met het juiste abonnement Hallo werkt. Als niet zo is, stelt u deze toohello rechts een met behulp van de uitvoer van Hallo `Get-AzureRmSubscription`.

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. toolist bestaande regels voor een resourcegroep Hallo volgende opdracht gebruiken:

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. toocreate een regel, moet u toohave belangrijke stukjes informatie eerst.

  * Hallo **Resource-ID** voor Hallo resource gewenste tooset een waarschuwing voor
  * Hallo **metrische definities** beschikbaar voor die bron

     Eenzijdige tooget Hallo Resource-ID is toouse hello Azure-portal. Hallo-bron ervan uitgaande dat al is gemaakt, selecteert u deze in Hallo-portal. Selecteer in de volgende blade Hallo *eigenschappen* onder Hallo *instellingen* sectie. **De RESOURCE-ID** is een veld in de volgende Hallo-blade. Een andere manier is toouse hello [Azure Resource Explorer](https://resources.azure.com/).

     Een voorbeeld van de Resource-ID voor een web-app is

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     U kunt `Get-AzureRmMetricDefinition` tooview Hallo lijst met alle metrische definities voor een specifieke bron.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     Hallo volgende voorbeeld genereert een tabel met Hallo metriek naam en het Hallo eenheid voor deze metriek.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     Een volledige lijst met beschikbare opties voor Get-AzureRmMetricDefinition is beschikbaar door het uitvoeren van Get-MetricDefinitions.
5. Hallo volgende voorbeeld wordt u een waarschuwing voor een bron voor de website. Hallo waarschuwing activeert wanneer het consistent verkeer ontvangt voor 5 minuten en opnieuw wanneer er geen verkeer ontvangen gedurende vijf minuten.

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. toocreate webhook verzenden e-mailadres of wanneer een waarschuwing activeert, maakt u eerst Hallo e-mailadres en/of webhooks. Maak vervolgens onmiddellijk Hallo regel daarna met Hallo - tag acties en zoals weergegeven in het volgende voorbeeld Hallo. Kan geen koppelt u webhook of e-mailberichten met regels via PowerShell al is gemaakt.

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. tooverify dat uw waarschuwingen correct zijn gemaakt door te kijken Hallo afzonderlijke regels.

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. Uw waarschuwingen verwijderen. Deze opdrachten verwijderen Hallo regels eerder hebt gemaakt in dit artikel.

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a>Volgende stappen
* [Een overzicht van Azure monitoring](monitoring-overview.md) inclusief Hallo typen gegevens u kunt verzamelen en controleren.
* Meer informatie over [configureren van webhooks in waarschuwingen](insights-webhooks-alerts.md).
* Meer informatie over [waarschuwingen configureren op activiteit logboekgebeurtenissen](monitoring-activity-log-alerts.md).
* Meer informatie over [Azure Automation-Runbooks](../automation/automation-starting-a-runbook.md).
* Ophalen van een [overzicht van het verzamelen van diagnostische logboeken](monitoring-overview-of-diagnostic-logs.md) toocollect gedetailleerde hoge frequentie metrische gegevens over uw service.
* Ophalen van een [overzicht van metrische gegevens verzameling](insights-how-to-customize-monitoring.md) toomake ervoor dat uw service beschikbaar is en reageert.
