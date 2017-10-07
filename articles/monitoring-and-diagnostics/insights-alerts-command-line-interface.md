---
title: waarschuwingen voor Azure-services - platformoverschrijdende CLI aaaCreate | Microsoft Docs
description: Trigger e-mailberichten, meldingen, worden URL's van websites (webhooks) of automation aanroepen wanneer Hallo door u opgegeven voorwaarden wordt voldaan.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a>Metrische waarschuwingen maken in de Azure-Monitor voor Azure-services - platformoverschrijdende CLI
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Overzicht
Dit artikel laat zien hoe tooset Azure metrische waarschuwingen met behulp van Hallo platformoverschrijdende opdrachtregelinterface (CLI).

> [!NOTE]
> Nieuwe naam op voor het zogenoemde 'Azure Insights' hello is Azure Monitor tot 25 september 2016. Echter bevatten Hallo naamruimten, en daarom onderstaande Hallo-opdrachten nog steeds Hallo 'insights'.
>
>

U kunt een waarschuwing op basis van bewaking metrische gegevens voor of gebeurtenissen op uw Azure-services kunt ontvangen.

* **Metrische waarden** - hello triggers waarschuwen wanneer Hallo-waarde van een opgegeven metriek overschrijdt de drempelwaarde die u in beide richtingen toewijst. Dat wil zeggen, deze beide wordt geactiveerd wanneer eerst aan Hallo voorwaarde wordt voldaan en vervolgens later wanneer die voorwaarde wordt niet langer wordt voldaan.    
* **Activiteit logboekgebeurtenissen** -een waarschuwing kunt activeren voor *elke* gebeurtenis of alleen wanneer een bepaalde gebeurtenissen optreden. meer informatie over de activiteit logboek waarschuwingen toolearn [Klik hier](monitoring-activity-log-alerts.md)

Een metriek waarschuwing toodo Hallo volgen wanneer deze wordt geactiveerd, kunt u configureren:

* verzenden van e-mailmeldingen toohello servicebeheerder en medebeheerders
* e-mail verzenden tooadditional e-mails die u opgeeft.
* een webhook aanroepen
* uitvoering van een Azure-runbook (alleen van hello Azure-portal op dit moment) starten

U kunt configureren en ophalen van informatie over metrische waarschuwingsregels met

* [Azure Portal](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [opdrachtregelinterface (CLI)](insights-alerts-command-line-interface.md)
* [Monitor voor Azure REST-API](https://msdn.microsoft.com/library/azure/dn931945.aspx)

U kunt altijd help voor opdrachten ontvangen door een opdracht te typen en stellen - help aan Hallo einde. Bijvoorbeeld:

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a>Waarschuwingsregels met Hallo CLI maken
1. Hallo-vereisten en aanmelding tooAzure uitvoeren. Zie [Azure Monitor CLI voorbeelden](insights-cli-samples.md). Kort gezegd: Hallo CLI installeren en voer deze opdrachten. Ze u aangemeld, welk abonnement u gebruikt en u zich voorbereiden toorun Azure Monitor opdrachten weergeven.

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. toolist bestaande regels voor een resourcegroep gebruiken Hallo formulier na **inzicht van azure waarschuwingen regel lijst** *[opties] &lt;resourceGroup&gt;*

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. toocreate een regel, moet u toohave belangrijke stukjes informatie eerst.
  * Hallo **Resource-ID** voor Hallo resource gewenste tooset een waarschuwing voor
  * Hallo **metrische definities** beschikbaar voor die bron

     Eenzijdige tooget Hallo Resource-ID is toouse hello Azure-portal. Hallo-bron ervan uitgaande dat al is gemaakt, selecteert u deze in Hallo-portal. Selecteer in de volgende blade Hallo *eigenschappen* onder Hallo *instellingen* sectie. Hallo *RESOURCE-ID* is een veld in de volgende Hallo-blade. Een andere manier is toouse hello [Azure Resource Explorer](https://resources.azure.com/).

     Een voorbeeld van de resource-id voor een web-app is

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     tooget een lijst met beschikbare metrische gegevens Hallo en eenheden voor deze metrische gegevens bijvoorbeeld Hallo vorige resource gebruik Hallo CLI-opdracht te volgen:  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     *PT1M* Hallo granulatie van Hallo beschikbaar meting (1 minuut intervallen) is. Met andere granulaties hebt u verschillende metrische opties.
4. toocreate een metriek gebaseerde waarschuwingsregel, gebruikt u een opdracht Hallo formulier te volgen:

    **inzicht van Azure waarschuwingen metrische regelset** *[opties] &lt;ruleName&gt; &lt;locatie&gt; &lt;resourceGroup&gt; &lt;venstergrootte &gt; &lt;operator&gt; &lt;drempelwaarde&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt; timeAggregationOperator&gt;*

    Hallo volgende voorbeeld wordt u een waarschuwing voor een bron voor de website. Hallo waarschuwing activeert wanneer het consistent verkeer ontvangt voor 5 minuten en opnieuw wanneer er geen verkeer ontvangen gedurende vijf minuten.

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. toocreate webhook verzenden e-mailadres of wanneer een waarschuwing voor metrische wordt gestart, maakt u eerst Hallo e-mailadres en/of webhooks. Vervolgens maakt u de regel Hallo onmiddellijk daarna. Kan geen koppelt u webhook of e-mailberichten met regels die gebruikmaken van Hallo CLI al is gemaakt.

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. U kunt controleren of uw waarschuwingen correct zijn gemaakt door te kijken op een afzonderlijke regel.

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. toodelete regels, gebruikt u een opdracht Hallo vorm:

    **Waarschuwingen regel verwijderen Insights** [opties] &lt;resourceGroup&gt; &lt;ruleName&gt;

    Deze opdrachten Verwijder Hallo-regels die eerder in dit artikel hebt gemaakt.

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a>Volgende stappen
* [Een overzicht van Azure monitoring](monitoring-overview.md) inclusief Hallo typen gegevens u kunt verzamelen en controleren.
* Meer informatie over [configureren van webhooks in waarschuwingen](insights-webhooks-alerts.md).
* Meer informatie over [waarschuwingen configureren op activiteit logboekgebeurtenissen](monitoring-activity-log-alerts.md).
* Meer informatie over [Azure Automation-Runbooks](../automation/automation-starting-a-runbook.md).
* Ophalen van een [overzicht van het verzamelen van diagnostische logboeken](monitoring-overview-of-diagnostic-logs.md) toocollect gedetailleerde hoge frequentie metrische gegevens over uw service.
* Ophalen van een [overzicht van metrische gegevens verzameling](insights-how-to-customize-monitoring.md) toomake ervoor dat uw service beschikbaar is en reageert.
