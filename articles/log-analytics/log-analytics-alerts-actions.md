---
title: aaaResponses tooalerts in OMS Log Analytics | Microsoft Docs
description: Waarschuwingen in logboekanalyse belangrijke informatie in de OMS-opslagplaats te identificeren en op de proactief kunnen zullen u informeren over problemen of acties tooattempt toocorrect aanroepen ze.  Dit artikel wordt beschreven hoe een waarschuwingsregel toocreate en details Hallo verschillende acties kunnen nemen.
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
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a>Acties tooalert regels in logboekanalyse toevoegen
Wanneer een [waarschuwing is gemaakt in logboekanalyse](log-analytics-alerts.md), hebt u de optie Hallo van [configureren Hallo waarschuwingsregel](log-analytics-alerts.md) tooperform een of meer acties.  In dit artikel beschrijft Hallo verschillende acties die beschikbaar zijn en meer informatie over het configureren van elk type.

| Actie | Beschrijving |
|:--|:--|
| [E-mail](#email-actions) | Stuur een e-mail met Hallo details van de waarschuwing tooone Hallo of meer geadresseerden. |
| [Webhook](#webhook-actions) | Een extern proces via één HTTP POST-aanvraag worden aangeroepen. |
| [Runbook](#runbook-actions) | Starten van een runbook in Azure Automation. |


## <a name="email-actions"></a>E-acties
E-acties Stuur een e-mail met Hallo details van de waarschuwing tooone Hallo of meer geadresseerden.  U kunt Hallo onderwerp van e-mail Hallo opgeven, maar de inhoud is een standaardindeling samengesteld door logboekanalyse.  Samenvattende informatie zoals de naam van de Hallo van Hallo waarschuwing in toodetails toevoeging van tooten records geretourneerd door de zoekfunctie Hallo opgenomen.  Het bevat ook een koppeling tooa logboek zoekopdracht logboekanalyse dat Hallo volledige set van records uit deze query wordt geretourneerd.   Hallo afzender Hallo mail *Microsoft Operations Management Suite-Team &lt; noreply@oms.microsoft.com &gt;* . 

E-acties vereisen Hallo eigenschappen in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Onderwerp |Onderwerpen in Hallo e-mailbericht.  U kunt Hallo hoofdtekst van e-mail Hallo niet wijzigen. |
| ontvangers |De adressen van alle e-mailgeadresseerden.  Als u meer dan één adres vervolgens afzonderlijke hello-mailadressen opgeven met een puntkomma (;). |


## <a name="webhook-actions"></a>Webhookacties

Webhookacties kunnen u tooinvoke een extern proces via één HTTP POST-aanvraag.  Hallo-service wordt aangeroepen moet webhooks ondersteunen en bepaal hoe het door middel van elke nettolading wordt ontvangen.  U kunt ook een REST-API die niet specifiek webhooks ondersteunt, zolang het Hallo-aanvraag heeft een indeling die Hallo API begrijpt aanroepen.  Voorbeelden van het gebruik van een webhook in antwoord tooan waarschuwing een bericht verzendt [Slack](http://slack.com) of het maken van een incident in [PagerDuty](http://pagerduty.com/).  Een volledige procedure voor het maken van een waarschuwingsregel met een webhook toocall Slack is beschikbaar op [Webhooks in logboekanalyse waarschuwingen](log-analytics-alerts-webhooks.md).

Webhookacties vereisen Hallo eigenschappen in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Webhook-URL |Hallo-URL van de webhook Hallo. |
| Aangepaste JSON-nettolading |Aangepaste nettolading toosend met Hallo webhook.  Zie hieronder voor meer informatie. |


Een URL opnemen naar Webhooks en een nettolading opgemaakt in JSON is Hallo gegevens toohello externe service verzonden.  Standaard wordt Hallo nettolading in de volgende tabel Hallo Hallo waarden bevatten.  U kunt deze nettolading met een van uw eigen aangepaste tooreplace.  In dat geval kunt u variabelen in de tabel Hallo Hallo voor elk Hallo parameters tooinclude hun waarde in de aangepaste nettolading.

| Parameter | Variabele | Beschrijving |
|:--- |:--- |:--- |
| AlertRuleName |#alertrulename |Naam van de waarschuwingsregel Hallo. |
| AlertThresholdOperator |#thresholdoperator |Drempelwaarde voor de operator voor Hallo waarschuwingsregel.  *Groter dan* of *minder dan*. |
| AlertThresholdValue |#thresholdvalue |Drempelwaarde voor het Hallo-waarschuwingsregel. |
| LinkToSearchResults |#linktosearchresults |Koppeling tooLog Analytics logboek zoekquery waarmee Hallo records in de Hallo-query die Hallo waarschuwing gemaakt. |
| ResultCount |#searchresultcount |Het aantal records in de zoekresultaten Hallo. |
| SearchIntervalEndtimeUtc |#searchintervalendtimeutc |De eindtijd voor de query Hallo in UTC-notatie. |
| SearchIntervalInSeconds |#searchinterval |Tijdvenster voor Hallo waarschuwingsregel. |
| SearchIntervalStartTimeUtc |#searchintervalstarttimeutc |Begintijd voor de query Hallo in UTC-notatie. |
| searchQuery |#searchquery |Logboek zoekquery gebruikt door de waarschuwingsregel Hallo. |
| Zoekresultaten |Hieronder vindt u de |Records geretourneerd door de query Hallo in JSON-indeling.  Beperkte toohello eerste 5000 records. |
| WorkspaceID |#workspaceid |ID van de OMS-werkruimte. |

Bijvoorbeeld, kunt u opgeven Hallo aangepaste nettolading met een enkele parameter aangeroepen na *tekst*.  Hallo-service die deze webhook aanroept, zou deze parameter worden verwacht.

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

De nettolading van dit voorbeeld zou oplossen toosomething zoals Hallo volgen wanneer toohello webhook verzonden.

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

tooinclude zoekresultaten in een aangepaste nettolading toevoegen Hallo volgt regel als een eigenschap van het hoogste niveau in de json-nettolading Hallo.  

    "IncludeSearchResults":true

Bijvoorbeeld, toocreate een aangepaste nettolading met NET Hallo naam van waarschuwing en Hallo zoekresultaten, u kunt hello te volgen. 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


U kunt een compleet voorbeeld van een waarschuwingsregel maken met een toostart webhook met een externe service op doorlopen [maakt een actie waarschuwing webhook in OMS Log Analytics toosend bericht tooSlack](log-analytics-alerts-webhooks.md).

## <a name="runbook-actions"></a>Runbook-acties
Runbook-acties starten van een runbook in Azure Automation.  In volgorde toouse dit type actie, moet u hebben Hallo [Automation-oplossing](log-analytics-add-solutions.md) geïnstalleerd en geconfigureerd in de OMS-werkruimte.  U kunt kiezen uit runbooks Hallo in Hallo automation-account die u hebt geconfigureerd in Hallo Automation-oplossing.

Runbook-bewerkingen moet Hallo eigenschappen in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:---|
| Runbook | Het Runbook dat het gewenste toostart wanneer een waarschuwing wordt gemaakt. |
| Voer op | Geef **Azure** toorun hello runbook in de cloud Hallo.  Geef **hybride worker** toorun hello runbook op een agent met [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) geïnstalleerd.  |

Runbook-acties aan de slag Hallo runbook met een [webhook](../automation/automation-webhooks.md).  Wanneer u een waarschuwingsregel Hallo maakt, wordt deze automatisch een nieuwe webhook voor Hallo runbook maken met Hallo naam **OMS waarschuwing herstel** gevolgd door een GUID.  

U kan niet rechtstreeks vullen van de parameters van Hallo runbook maar Hallo [$WebhookData parameter](../automation/automation-webhooks.md) bevat details op Hallo van Hallo waarschuwing, met inbegrip van Hallo resultaten van Hallo logboek zoekopdracht waarvan deze is gemaakt.  Hallo runbook moet toodefine **$WebhookData** als parameter voor deze tooaccess eigenschappen van de waarschuwing Hallo Hallo.  Hallo waarschuwingsgegevens is beschikbaar in json-indeling in één eigenschap aangeroepen **zoekresultaten** in Hallo **RequestBody** eigenschap van **$WebhookData**.  Dit heeft met de eigenschappen in de volgende tabel Hallo Hallo.

| Knooppunt | Beschrijving |
|:--- |:--- |
| id |Pad en de GUID van Hallo zoeken. |
| __metadata |Informatie over Hallo waarschuwing inclusief Hallo aantal records en status van Hallo zoekresultaten. |
| waarde |Afzonderlijke vermelding voor elke record in de zoekresultaten Hallo.  Hallo-details van Hallo vermelding komt overeen met Hallo eigenschappen en waarden van Hallo record. |

Bijvoorbeeld zou hello volgende runbook pak Hallo records geretourneerd door Hallo logboek zoeken en toewijzen van verschillende eigenschappen die zijn gebaseerd op het Hallo-type van elke record.  Houd er rekening mee dat runbook Hallo begint met het converteren van **RequestBody** van json zodanig dat deze kan worden gewerkt met als een object in PowerShell.

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
- Meer informatie over hoe toowrite [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) tooremediate problemen geïdentificeerd met waarschuwingen.
