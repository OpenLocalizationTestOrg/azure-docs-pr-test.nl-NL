---
title: aaaUsing OMS Log Analytics waarschuwing REST-API
description: Hallo Log Analytics waarschuwing REST-API kunt u toocreate en waarschuwingen beheren in logboekanalyse die deel uitmaakt van de Operations Management Suite (OMS).  Dit artikel bevat de details van Hallo API en enkele voorbeelden voor het uitvoeren van verschillende bewerkingen.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a>Maken en beheren van waarschuwingsregels in logboekanalyse met REST-API
Hallo Log Analytics waarschuwing REST-API kunt u toocreate en waarschuwingen in Operations Management Suite (OMS) beheren.  Dit artikel bevat de details van Hallo API en enkele voorbeelden voor het uitvoeren van verschillende bewerkingen.

Hallo Log Analytics Search REST-API RESTful is en toegankelijk zijn via Hallo REST-API van Azure Resource Manager. In dit document vindt u voorbeelden waarbij Hallo API worden geopend vanuit een PowerShell-opdrachtregel met [ARMClient](https://github.com/projectkudu/ARMClient), een open-source opdrachtregel-hulpprogramma dat wordt aangeroepen vereenvoudigt hello Azure Resource Manager-API. Hallo-gebruik van ARMClient en PowerShell is een van de vele opties tooaccess Hallo Log Analytics zoeken-API. Met deze hulpprogramma's kunt u gebruikmaken van Hallo RESTful API van Azure Resource Manager toomake aanroepen tooOMS werkruimten en zoekvariabelen binnen deze. Hallo API wordt zoeken resultaten tooyou in JSON-indeling, zodat u toouse Hallo zoekresultaten in veel verschillende manieren programmatisch uitvoer.

## <a name="prerequisites"></a>Vereisten
Waarschuwingen kunnen op dit moment kunnen alleen worden gemaakt met een opgeslagen zoekopdracht in logboekanalyse.  U kunt verwijzen toohello [logboek Search REST-API](log-analytics-log-search-api.md) voor meer informatie.

## <a name="schedules"></a>Planningen
Een opgeslagen zoekopdracht kan een of meer planningen hebben. Hallo schema wordt gedefinieerd hoe vaak hello zoekopdracht wordt uitgevoerd en de tijdsinterval Hallo via welke criteria hello wordt aangeduid.
Schema's hebben Hallo eigenschappen in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Interval |Hoe vaak hello zoekopdracht wordt uitgevoerd. Gemeten in minuten. |
| QueryTimeSpan |Hallo tijdsinterval welke Hallo criteria wordt geëvalueerd. Moet gelijk tooor groter dan het Interval. Gemeten in minuten. |
| Versie |Hallo API-versie die wordt gebruikt.  Op dit moment is moet dit altijd worden ingesteld too1. |

Neem bijvoorbeeld een event-query met een Interval van 15 minuten en een TimeSpan-waarde van 30 minuten. In dit geval Hallo query wilt uitvoeren om de 15 minuten en een waarschuwing zou worden geactiveerd als Hallo criteria nog steeds tooresolve tootrue gedurende een bepaalde 30 minuten.

### <a name="retrieving-schedules"></a>Bij het ophalen van schema 's
Gebruik Hallo ophalen methode tooretrieve alle schema's voor een opgeslagen zoekopdracht.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

Gebruik Hallo ophalen methode met een schema-ID tooretrieve een bepaalde planning voor een opgeslagen zoekopdracht.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

Hier volgt een voorbeeldantwoord voor een schema.

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a>Een schema maken
Hallo Put-methode gebruiken met een uniek schema-ID toocreate een nieuw schema.  Opmerking dat twee planningen kan niet hebben Hallo dezelfde ID zelfs als ze zijn gekoppeld aan verschillende opgeslagen zoekopdrachten.  Wanneer u een planning in Hallo OMS-console maakt, wordt een GUID gemaakt voor Hallo-schema.

> [!NOTE]
> Hallo-naam voor alle opgeslagen zoekopdrachten, schema's en acties die zijn gemaakt met de Hallo Log Analytics-API moet in kleine letters.

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a>Het bewerken van een planning
Hallo Put-methode met een bestaand schema-ID voor dezelfde opgeslagen Hallo toomodify die plant zoeken gebruiken.  Hallo-hoofdtekst van Hallo-aanvraag moet Hallo etag Hallo schema bevatten.

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a>Schema's verwijderen
Hallo-Delete-methode gebruiken met een schema-ID toodelete een planning.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a>Acties
Een planning kan meerdere acties hebben. Een actie kan definiëren een of meer processen tooperform zoals een e-mailbericht verzenden of een runbook starten, of het kan een drempelwaarde die bepaalt wanneer Hallo resultaten van een zoekopdracht voldoen aan bepaalde criteria definiëren.  Sommige acties definiëren beide zodat Hallo processen worden uitgevoerd wanneer Hallo drempelwaarde wordt voldaan.

Alle acties hebben Hallo eigenschappen in de volgende tabel Hallo.  Verschillende soorten waarschuwingen hebben verschillende aanvullende eigenschappen die hieronder worden beschreven.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Type |Type Hallo actie.  Hallo mogelijke waarden zijn momenteel waarschuwing en Webhook. |
| Naam |Weergavenaam voor Hallo waarschuwing. |
| Versie |Hallo API-versie die wordt gebruikt.  Op dit moment is moet dit altijd worden ingesteld too1. |

### <a name="retrieving-actions"></a>Bij het ophalen van acties
Gebruik Hallo ophalen methode tooretrieve alle acties voor een schema.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

Gebruik Hallo ophalen methode met Hallo actie-ID tooretrieve een bepaalde actie voor een schema.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a>Maken of bewerken van acties
Hallo Put-methode gebruiken met een actie-ID is uniek toohello planning toocreate een nieuwe actie.  Wanneer u een actie in Hallo OMS-console maakt, is een GUID voor Hallo actie-ID.

> [!NOTE]
> Hallo-naam voor alle opgeslagen zoekopdrachten, schema's en acties die zijn gemaakt met de Hallo Log Analytics-API moet in kleine letters.

Hallo Put-methode met een bestaande actie-ID voor dezelfde opgeslagen Hallo toomodify die plant zoeken gebruiken.  Hallo-hoofdtekst van Hallo-aanvraag moet Hallo etag Hallo schema bevatten.

De aanvraagindeling Hallo voor het maken van een nieuwe actie varieert per actietype zodat deze voorbeelden u in de volgende secties voor Hallo vindt.

### <a name="deleting-actions"></a>Acties worden verwijderd
Hallo-Delete-methode gebruiken met Hallo actie-ID toodelete een actie.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a>Waarschuwing acties
Een planning hebt slechts één meldingsactie.  Waarschuwing acties hebben een of meer van de secties in de volgende tabel Hallo Hallo.  Elk wordt nader hieronder beschreven.

| Sectie | Beschrijving |
|:--- |:--- |
| Drempelwaarde |Criteria voor wanneer Hallo actie wordt uitgevoerd. |
| EmailNotification |E-mail toomultiple ontvangers verzenden. |
| Herstel |Start een runbook in Azure Automation tooattempt toocorrect geïdentificeerd probleem. |

#### <a name="thresholds"></a>Drempelwaarden
Een waarschuwing actie mag slechts één drempelwaarde hebben.  Wanneer resultaten van een opgeslagen zoekopdracht Hallo Hallo drempelwaarde in een actie die is gekoppeld aan die zoekopdracht overeenkomen, worden andere processen in die actie uitgevoerd.  Een actie kan alleen een drempelwaarde ook bevatten, zodat deze kan worden gebruikt met de acties die van andere typen die geen drempelwaarden bevatten.

Drempelwaarden hebben Hallo eigenschappen in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Operator |De operator voor Hallo drempelwaarde voor vergelijking. <br> gt = groter dan <br> lt = kleiner dan |
| Waarde |Waarde voor Hallo drempelwaarde. |

Neem bijvoorbeeld een event-query met een Interval van 15 minuten, een TimeSpan-waarde van 30 minuten en een drempel van meer dan 10. In dit geval Hallo query wilt uitvoeren om de 15 minuten en een waarschuwing zou worden geactiveerd als het 10 gebeurtenissen die zijn gemaakt via een reeks van 30 minuten geretourneerd.

Hier volgt een voorbeeldantwoord voor een actie met alleen een drempelwaarde.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

Hallo Put-methode gebruiken met een unieke actie-ID toocreate een nieuwe drempelwaarde-actie voor een schema.  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

Hallo Put-methode gebruiken met een bestaande actie-ID toomodify een actie drempelwaarde voor een schema.  Hallo-hoofdtekst van Hallo-aanvraag moet Hallo etag Hallo actie opnemen.

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a>E-mailmeldingen
E-mailmeldingen verzenden van e-mail tooone of meer geadresseerden.  Ze bevatten Hallo eigenschappen in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| ontvangers |Lijst met e-mailadressen. |
| Onderwerp |Hallo onderwerp Hallo mail. |
| Bijlage |Bijlagen worden momenteel niet ondersteund, zodat dit altijd de waarde 'None'. |

Hier volgt een voorbeeldantwoord voor een actie van de melding e-mailbericht met een drempelwaarde.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

Hallo Put-methode gebruiken met een unieke actie-ID toocreate een nieuwe e-actie voor een schema.  Hallo wordt volgende voorbeeld een e-mailbericht met een drempelwaarde daarom Hallo e-mail wordt verzonden wanneer het Hallo-resultaten van de opgeslagen zoekopdracht Hallo Hallo drempelwaarde overschrijden.

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

Hallo Put-methode gebruiken met een bestaande actie-ID toomodify een e-actie voor een schema.  Hallo-hoofdtekst van Hallo-aanvraag moet Hallo etag Hallo actie opnemen.

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a>Herstelacties
Herstelbewerkingen starten van een runbook in Azure Automation waarmee wordt geprobeerd toocorrect Hallo probleem geïdentificeerd door Hallo waarschuwing.  U moet een webhook voor Hallo runbook gebruikt in een herstelactie maken en geeft vervolgens Hallo URI in Hallo WebhookUri-eigenschap.  Wanneer u deze actie met Hallo OMS-console maakt, wordt automatisch een nieuwe webhook gemaakt voor runbook Hallo.

Hallo-eigenschappen bevatten herstelbewerkingen in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| RunbookName |Naam van Hallo runbook. Dit moet overeenkomen met een gepubliceerd runbook in Hallo automation-account is geconfigureerd in Hallo Automation-oplossing in de OMS-werkruimte. |
| WebhookUri |De URI van de webhook Hallo. |
| Verloopdatum |Hallo datum en tijd van de webhook Hallo.  Als Hallo webhook geen een verlopen, kan dit een geldige datum in de toekomst zijn. |

Hier volgt een voorbeeldantwoord voor een herstelactie met een drempelwaarde.

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

Hallo Put-methode gebruiken met een unieke actie-ID toocreate een nieuwe herstelactie voor een schema.  Hallo wordt volgende voorbeeld een herstelbewerking met een drempelwaarde daarom Hallo runbook wordt gestart wanneer het Hallo-resultaten van de opgeslagen zoekopdracht Hallo Hallo drempelwaarde overschrijden.

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

Hallo Put-methode gebruiken met een bestaande actie-ID toomodify een herstelactie voor een schema.  Hallo-hoofdtekst van Hallo-aanvraag moet Hallo etag Hallo actie opnemen.

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a>Voorbeeld
Hier volgt een voorbeeld van de volledige toocreate een nieuw e-mailmelding.  Hiermee maakt u een nieuw schema samen met een actie met een drempelwaarde en e-mailbericht.

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a>Webhookacties
Een proces starten webhookacties door het aanroepen van een URL en het eventueel geven een nettolading toobe verzonden.  Ze zijn vergelijkbaar tooRemediation acties maar ze zijn bedoeld voor webhooks die van processen dan Azure Automation-runbooks gebruikmaken mogelijk.  Ze bieden ook een extra optie Hallo van het bieden van een nettolading toobe bezorgd toohello extern proces.

Webhookacties hebben geen een drempelwaarde, maar in plaats daarvan moeten tooa schema met de actie van een waarschuwing met een drempelwaarde worden toegevoegd.  U kunt meerdere webhookacties die al worden uitgevoerd wanneer Hallo drempelwaarde wordt voldaan toevoegen.

Webhookacties bevatten Hallo eigenschappen in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| WebhookUri |Hallo onderwerp Hallo mail. |
| CustomPayload |Aangepaste nettolading toobe toohello webhook verzonden.  Hallo-indeling afhankelijk van welke webhook hello wordt verwacht. |

Hier volgt een voorbeeldantwoord voor webhook actie en een bijbehorende waarschuwingen met een drempelwaarde.

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a>Maken of bewerken van een webhook-actie
Hallo Put-methode gebruiken met een unieke actie-ID toocreate een nieuwe webhook-actie voor een schema.  Hallo maakt volgende voorbeeld een actie Webhook en een waarschuwing met een drempelwaarde zodat Hallo webhook wordt geactiveerd wanneer het Hallo-resultaten van de opgeslagen zoekopdracht Hallo Hallo drempelwaarde overschrijden.

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

Hallo Put-methode gebruiken met een bestaande actie-ID toomodify een webhook-actie voor een schema.  Hallo-hoofdtekst van Hallo-aanvraag moet Hallo etag Hallo actie opnemen.

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a>Volgende stappen
* Gebruik Hallo [REST-API tooperform logboek zoekopdrachten](log-analytics-log-search-api.md) in logboekanalyse.

