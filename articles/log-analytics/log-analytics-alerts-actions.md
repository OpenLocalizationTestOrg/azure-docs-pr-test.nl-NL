---
title: Antwoorden op waarschuwingen in OMS Log Analytics | Microsoft Docs
description: Waarschuwingen in logboekanalyse kunnen belangrijke informatie in de OMS-opslagplaats te identificeren en proactief zullen u informeren over problemen of acties uit om te proberen op te lossen ze aanroepen.  In dit artikel beschrijft het maken van een waarschuwingsregel en details van de verschillende acties die ze kunnen ondernemen.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b8731e1fe48b7d809b113eb5273e3962542b8f34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-actions-to-alert-rules-in-log-analytics"></a>Acties toevoegen aan de regels voor waarschuwingen in Log Analytics
Wanneer een [waarschuwing is gemaakt in logboekanalyse](log-analytics-alerts.md), hebt u de optie [configureren van de waarschuwingsregel](log-analytics-alerts.md) een of meer acties uit te voeren.  In dit artikel beschrijft de verschillende acties die beschikbaar zijn en meer informatie over het configureren van elk type.

| Actie | Beschrijving |
|:--|:--|
| [E-mail](#email-actions) | Verzend een e-mailbericht met de details van de waarschuwing naar een of meer geadresseerden. |
| [Webhook](#webhook-actions) | Een extern proces via één HTTP POST-aanvraag worden aangeroepen. |
| [Runbook](#runbook-actions) | Starten van een runbook in Azure Automation. |


## <a name="email-actions"></a>E-acties
E-acties verzend een e-mailbericht met de details van de waarschuwing naar een of meer geadresseerden.  Kunt u het onderwerp van het e-mailbericht, maar de inhoud is een standaardindeling samengesteld door logboekanalyse.  Dit omvat samenvattende informatie zoals de naam van de waarschuwing naast de details van maximaal tien records geretourneerd door het logboek zoeken.  Het bevat ook een koppeling naar een zoekopdracht logboek logboekanalyse dat de volledige set van records uit de query die wordt geretourneerd.   De afzender van het e-mailbericht is *Microsoft Operations Management Suite-Team &lt; noreply@oms.microsoft.com &gt;* . 

E-bewerkingen moet de eigenschappen in de volgende tabel.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Onderwerp |Onderwerpen in het e-mailbericht.  U kunt de hoofdtekst van het e-mailbericht niet wijzigen. |
| ontvangers |De adressen van alle e-mailgeadresseerden.  Als u meer dan één adres opgeeft, scheidt u de adressen met een puntkomma (;). |


## <a name="webhook-actions"></a>Webhookacties

Webhookacties kunnen u een extern proces via één HTTP POST-aanvraag worden aangeroepen.  De service die wordt aangeroepen moet webhooks ondersteunen en bepaal hoe het door middel van elke nettolading wordt ontvangen.  U kunt ook een REST-API die niet specifiek webhooks ondersteunt, zolang de aanvraag heeft een indeling die werkt met de API aanroepen.  Voorbeelden van het gebruik van een webhook in reactie op een waarschuwing een bericht verzendt [Slack](http://slack.com) of het maken van een incident in [PagerDuty](http://pagerduty.com/).  Een volledige procedure voor het maken van een waarschuwingsregel met een webhook aanroepen Slack is beschikbaar op [Webhooks in logboekanalyse waarschuwingen](log-analytics-alerts-webhooks.md).

Webhookacties vereisen de eigenschappen in de volgende tabel.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Webhook-URL |De URL van de webhook. |
| Aangepaste JSON-nettolading |Aangepaste nettolading met de webhook moeten worden verzonden.  Zie hieronder voor meer informatie. |


Webhooks omvatten een URL en een nettolading opgemaakt in JSON is de gegevens naar de externe service verzonden.  De nettolading van de neemt standaard de waarden in de volgende tabel.  U kunt deze nettolading vervangen door een aangepaste van uzelf.  In dat geval kunt u de variabelen in de tabel voor elk van de parameters voor hun waarde bevatten in de aangepaste nettolading.

| Parameter | Variabele | Beschrijving |
|:--- |:--- |:--- |
| AlertRuleName |#alertrulename |Naam van de waarschuwingsregel. |
| AlertThresholdOperator |#thresholdoperator |Drempelwaarde voor de operator voor de waarschuwingsregel.  *Groter dan* of *minder dan*. |
| AlertThresholdValue |#thresholdvalue |Drempelwaarde voor de waarschuwingsregel. |
| LinkToSearchResults |#linktosearchresults |Koppelen aan logboekanalyse logboek zoeken waarmee de records geretourneerd van de query die de waarschuwing wordt gemaakt. |
| ResultCount |#searchresultcount |Het aantal records in de zoekresultaten. |
| SearchIntervalEndtimeUtc |#searchintervalendtimeutc |De eindtijd voor de query in UTC-notatie. |
| SearchIntervalInSeconds |#searchinterval |Tijdvenster voor de waarschuwingsregel. |
| SearchIntervalStartTimeUtc |#searchintervalstarttimeutc |Begintijd voor de query in UTC-notatie. |
| searchQuery |#searchquery |Logboek zoekquery gebruikt door de waarschuwingsregel. |
| Zoekresultaten |Hieronder vindt u de |Records geretourneerd door de query in JSON-indeling.  Beperkt tot de eerste 5000 records. |
| WorkspaceID |#workspaceid |ID van de OMS-werkruimte. |

Bijvoorbeeld, kunt u opgeven de volgende aangepaste nettolading met een enkele parameter aangeroepen *tekst*.  De service die deze webhook aanroepen, zou deze parameter worden verwacht.

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

De nettolading van dit voorbeeld zou worden omgezet naar ongeveer het volgende wanneer u naar de webhook verzonden.

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

Als u wilt opnemen zoekresultaten in een aangepaste nettolading, voeg de volgende regel als een eigenschap van het hoogste niveau in de json-nettolading.  

    "IncludeSearchResults":true

Bijvoorbeeld: voor het maken van een aangepaste nettolading met alleen de naam van de waarschuwing en de zoekresultaten, u kunt de volgende. 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


U kunt een compleet voorbeeld van een waarschuwingsregel maken met een webhook om een externe service op te starten doorlopen [maken van een actie waarschuwing webhook in OMS Log Analytics bericht te verzenden naar Slack](log-analytics-alerts-webhooks.md).

## <a name="runbook-actions"></a>Runbook-acties
Runbook-acties starten van een runbook in Azure Automation.  Om dit type actie gebruiken, hebt u de [Automation-oplossing](log-analytics-add-solutions.md) geïnstalleerd en geconfigureerd in de OMS-werkruimte.  U kunt kiezen uit de runbooks in het automation-account die u hebt geconfigureerd in de Automation-oplossing.

Runbook-bewerkingen moet de eigenschappen in de volgende tabel.

| Eigenschap | Beschrijving |
|:--- |:---|
| Runbook | Een Runbook dat u starten wilt wanneer een waarschuwing wordt gemaakt. |
| Voer op | Geef **Azure** voor het uitvoeren van het runbook in de cloud.  Geef **hybride worker** voor het uitvoeren van het runbook op een agent met [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) geïnstalleerd.  |

Runbook-acties, start het runbook met behulp van een [webhook](../automation/automation-webhooks.md).  Wanneer u de waarschuwingsregel maakt, wordt deze automatisch een nieuwe webhook voor het runbook maken met de naam **OMS waarschuwing herstel** gevolgd door een GUID.  

U kan niet rechtstreeks vullen met de parameters van het runbook, maar de [$WebhookData parameter](../automation/automation-webhooks.md) bevat de details van de waarschuwing, met inbegrip van de resultaten van de zoekopdracht logboek waarvan deze is gemaakt.  Het runbook moet definiëren **$WebhookData** als parameter voor deze toegang krijgt tot de eigenschappen van de waarschuwing.  Gegevens van de waarschuwing is beschikbaar in json-indeling in één eigenschap aangeroepen **zoekresultaten** in de **RequestBody** eigenschap van **$WebhookData**.  Dit heeft met de eigenschappen in de volgende tabel.

| Knooppunt | Beschrijving |
|:--- |:--- |
| id |Pad en de GUID van de zoekopdracht. |
| __metadata |Informatie over de waarschuwing waaronder het aantal records en status van de zoekresultaten. |
| waarde |Afzonderlijke vermelding voor elke record in de zoekresultaten.  De details van het item komt overeen met de eigenschappen en waarden van de record. |

De volgende runbook zou bijvoorbeeld uitpakken van de records geretourneerd door het logboek zoeken en toewijzen van andere eigenschappen op basis van het type van elke record.  Denk eraan dat het runbook met het converteren van begint **RequestBody** van json zodanig dat deze kan worden gewerkt met als een object in PowerShell.

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a>Volgende stappen
- Een stapsgewijze Kennismaking voltooien [configureren van een webook](log-analytics-alerts-webhooks.md) met een waarschuwingsregel.  
- Meer informatie over het schrijven van [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) oplossen van problemen die worden aangeduid met waarschuwingen.