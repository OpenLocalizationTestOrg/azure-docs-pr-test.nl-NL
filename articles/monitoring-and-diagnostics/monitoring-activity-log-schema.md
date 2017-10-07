---
title: aaaAzure activiteit logboek gebeurtenis Schema | Microsoft Docs
description: Hallo gebeurtenis schema voor gegevens die in Hallo activiteitenlogboek begrijpen
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a>Azure Activity Log gebeurtenis schema
Hallo **Azure Activity Log** is een logboek die biedt inzicht in een abonnement op gebeurtenissen die hebben plaatsgevonden in Azure. Dit artikel wordt beschreven Hallo gebeurtenis schema per categorie van gegevens.

## <a name="administrative"></a>Beheerdersrechten
Deze rubriek bevat Hallo-record van alle maken, update, delete en actie bewerkingen uitgevoerd via Resource Manager. Voorbeelden van Hallo soorten gebeurtenissen u in deze categorie ziet zijn 'virtuele machine maken' en 'verwijderen netwerkbeveiligingsgroep' elke actie op die door een gebruiker of toepassing die met Resource Manager is gemodelleerd als een bewerking op een bepaald resourcetype. Als Hallo bewerkingstype schrijven, verwijderen of actie Hallo-records van zowel Hallo start en het slagen of mislukken van die bewerking worden vastgelegd in Hallo beheercategorie. Hallo beheercategorie bevat ook eventuele wijzigingen toorole toegangsbeheer op basis van een abonnement.

### <a name="sample-event"></a>Voorbeeld van de gebeurtenis
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a>Eigenschapbeschrijvingen
| Elementnaam | Beschrijving |
| --- | --- |
| Autorisatie |De BLOB van eigenschappen van gebeurtenis Hallo RBAC. Omvat gewoonlijk Hallo 'action', 'rol' en 'bereik' Eigenschappen. |
| aanroeper |E-mailadres van Hallo-gebruiker die is uitgevoerd op het Hallo-bewerking, UPN-claim of SPN claim op basis van beschikbaarheid. |
| kanalen |Een van de volgende waarden Hallo: 'Admin', 'Operation' |
| Claims |Hallo JWT-token gebruikt door Active Directory tooauthenticate Hallo gebruiker of toepassing tooperform deze bewerking in de resourcemanager. |
| correlationId |Meestal een GUID in de indeling van tekenreeks Hallo. Gebeurtenissen die een correlationId delen behoren toohello dezelfde uber actie. |
| description |De beschrijving van de statische tekst van een gebeurtenis. |
| eventDataId |De unieke id van een gebeurtenis. |
| httpRequest |BLOB met een beschrijving hello Http-aanvraag. Omvat gewoonlijk Hallo 'clientRequestId', "clientIpAddress" en "method" (HTTP-methode. For example, plaatsen). |
| niveau |Niveau van het Hallo-gebeurtenis. Een van de volgende waarden Hallo: 'Kritiek', 'Fout', 'Waarschuwing', 'Ter informatie' en 'Verbose' |
| resourceGroupName |Naam van de resourcegroep Hallo voor Hallo beïnvloed resource. |
| resourceProviderName |Naam van de resourceprovider Hallo voor Hallo beïnvloed resource |
| resourceId |Bron-id van Hallo beïnvloed resource. |
| operationId |Een GUID die wordt gedeeld door Hallo-gebeurtenissen die overeenkomen met tooa één bewerking. |
| operationName |Naam van Hallo-bewerking. |
| properties |Een set `<Key, Value>` paren (dat wil zeggen, een woordenlijst) Hallo details van gebeurtenis Hallo beschrijven. |
| status |Tekenreeks die Hallo status van Hallo-bewerking. Sommige algemene waarden zijn: In voortgang, geslaagd, mislukt, actief, opgelost gestart. |
| subStatus |Meestal Hallo HTTP-statuscode van de bijbehorende REST-aanroep hello, maar kan ook andere tekenreeksen met een beschrijving van een substatus, zoals deze algemene waarden bevatten: OK (HTTP-statuscode: 200), gemaakt (HTTP-statuscode: 201), geaccepteerde (HTTP-statuscode: 202), geen inhoud (HTTP Statuscode: 204), onjuiste aanvraag (HTTP-statuscode: 400), niet is gevonden (HTTP-statuscode: 404), Conflict (HTTP-statuscode: 409), interne serverfout (HTTP-statuscode: 500), Service niet beschikbaar (HTTP-statuscode: 503), time-out van Gateway (HTTP-statuscode: 504). |
| eventTimestamp |Tijdstempel wanneer het Hallo-gebeurtenis is gegenereerd door hello Azure-service verwerken Hallo aanvragen overeenkomende Hallo-gebeurtenis. |
| submissionTimestamp |Tijdstempel wanneer het Hallo-gebeurtenis beschikbaar voor het uitvoeren van query's zijn geworden. |
| subscriptionId |Azure-abonnement-id. |

## <a name="service-health"></a>Servicestatus
Deze rubriek bevat Hallo record service health incidenten die hebben plaatsgevonden in Azure. Een voorbeeld van Hallo type gebeurtenis u in deze categorie ziet is "SQL Azure in VS-Oost ondervindt uitvaltijd." Gebeurtenissen van de health service in vijf soorten komen: actie vereist, ondersteunde herstel, Incident, onderhoud, gegevens of beveiliging, en worden alleen weergegeven als u hebt een resource in het Hallo-abonnement dat zou worden beïnvloed door het Hallo-gebeurtenis.

### <a name="sample-event"></a>Voorbeeld van de gebeurtenis
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a>Eigenschapbeschrijvingen
Elementnaam | Beschrijving
-------- | -----------
kanalen | Is een van de volgende waarden Hallo: 'Admin', 'Operation'
correlationId | Is meestal een GUID in de indeling van tekenreeks Hallo. Gebeurtenissen met die deel uitmaken van dezelfde uber actie meestal delen toohello dezelfde correlationId Hallo.
description | Beschrijving van gebeurtenis Hallo.
eventDataId | Hallo unieke id van een gebeurtenis.
EventName | Hallo titel van Hallo-gebeurtenis.
niveau | Niveau van het Hallo-gebeurtenis. Een van de volgende waarden Hallo: 'Kritiek', 'Fout', 'Waarschuwing', 'Ter informatie' en 'Verbose'
resourceProviderName | Naam van de resourceprovider Hallo voor Hallo beïnvloed resource. Als u niet bekend is, wordt dit niet null zijn.
resourceType| Hallo type resource Hallo beïnvloed resource. Als u niet bekend is, wordt dit niet null zijn.
subStatus | Meestal null voor Service Health-gebeurtenissen.
eventTimestamp | Tijdstempel wanneer Hallo van het gebeurtenislogboek is gegenereerd en toohello activiteitenlogboek verzonden.
submissionTimestamp |   Tijdstempel wanneer het Hallo-gebeurtenis is beschikbaar in Hallo activiteitenlogboek geworden.
subscriptionId | Hallo Azure-abonnement in waarmee deze gebeurtenis is vastgelegd.
status | Tekenreeks die Hallo status van Hallo-bewerking. Sommige algemene waarden zijn: actief, opgelost.
operationName | Naam van Hallo-bewerking. Meestal Microsoft.ServiceHealth/incident/action.
category | 'ServiceHealth'
resourceId | Bron-id van Hallo beïnvloed resource, indien bekend. Abonnements-ID is anders opgegeven.
Properties.title | Hallo gelokaliseerd titel in voor deze communicatie. Engels is de standaardtaal Hallo.
Properties.Communication | Hallo gelokaliseerd details Hallo communicatie met de HTML-opmaak. Engels is standaard Hallo.
Properties.incidentType | Mogelijke waarden: AssistedRecovery, ActionRequired, informatie, Incident-, onderhoud, beveiliging
Properties.trackingId | Identificeert Hallo incident die deze gebeurtenis is gekoppeld. Gebruik dit incident toocorrelate Hallo-gebeurtenissen gerelateerde tooan.
Properties.impactedServices | Een escape-teken JSON-blob waarin Hallo services en regio's die worden beïnvloed door Hallo incident worden beschreven. Een lijst met Services, die allemaal een servicenaam en een lijst met ImpactedRegions, die allemaal een RegionName.
Properties.defaultLanguageTitle | Hallo-communicatie in het Engels
Properties.defaultLanguageContent | Hallo-communicatie in het Engels als HTML-indeling of tekst zonder opmaak
Properties.Stage | Mogelijke waarden voor AssistedRecovery, ActionRequired, informatie, Incident-, beveiliging: actief, zijn opgelost. Ze zijn voor onderhoud: actief, gepland, InProgress, geannuleerd, Rescheduled, opgelost, voltooid
Properties.communicationId | Hallo communicatie deze gebeurtenis is gekoppeld.

## <a name="alert"></a>Waarschuwing
Deze rubriek bevat Hallo-record van alle activeringen van waarschuwingen van Azure. Een voorbeeld van Hallo type gebeurtenis u in deze categorie ziet is "CPU-percentage op myVM is meer dan 80 voor Hallo afgelopen vijf minuten." Een verscheidenheid aan Azure systemen hebben een waarschuwingsmethoden concept--u kunt een regel bepaalde hardwaresleutel definiëren en een melding ontvangen wanneer voorwaarden overeenkomen met die regel. Elke keer dat een ondersteunde Azure Waarschuwingstype 'wordt geactiveerd,' of hello voorwaarden wordt voldaan toogenerate een melding, toothis categorie Hallo activiteitenlogboek wordt ook doorgeschoven, is een record van Hallo activering.

### <a name="sample-event"></a>Voorbeeld van de gebeurtenis

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a>Eigenschapbeschrijvingen
| Elementnaam | Beschrijving |
| --- | --- |
| aanroeper | Altijd Microsoft.Insights/alertRules |
| kanalen | Altijd 'Admin, bewerking' |
| Claims | JSON-blob met Hallo SPN (service principal name) of de resource type, Hallo waarschuwings-engine. |
| correlationId | Een GUID in de indeling van tekenreeks Hallo. |
| description |Statische tekstbeschrijving van waarschuwing Hallo-gebeurtenis. |
| eventDataId |De unieke id van de waarschuwing gebeurtenis Hallo. |
| niveau |Niveau van het Hallo-gebeurtenis. Een van de volgende waarden Hallo: 'Kritiek', 'Fout', 'Waarschuwing', 'Ter informatie' en 'Verbose' |
| resourceGroupName |Naam van de resourcegroep Hallo voor Hallo beïnvloed resource als deze een metrische waarschuwing. Dit is voor de overige Waarschuwingstypen Hallo-naam van resourcegroep Hallo met Hallo waarschuwing zelf. |
| resourceProviderName |Naam van de resourceprovider Hallo voor Hallo beïnvloed resource als deze een metrische waarschuwing. Dit is voor overige Waarschuwingstypen Hallo-naam van de resourceprovider Hallo voor Hallo waarschuwing zelf. |
| resourceId | Naam van de resource-ID Hallo voor Hallo beïnvloed resource als deze een metrische waarschuwing. Dit is voor de overige Waarschuwingstypen Hallo bron-ID van de waarschuwing resource Hallo zelf. |
| operationId |Een GUID die wordt gedeeld door Hallo-gebeurtenissen die overeenkomen met tooa één bewerking. |
| operationName |Naam van Hallo-bewerking. |
| properties |Een set `<Key, Value>` paren (dat wil zeggen, een woordenlijst) Hallo details van gebeurtenis Hallo beschrijven. |
| status |Tekenreeks die Hallo status van Hallo-bewerking. Sommige algemene waarden zijn: In voortgang, geslaagd, mislukt, actief, opgelost gestart. |
| subStatus | Meestal null voor waarschuwingen. |
| eventTimestamp |Tijdstempel wanneer het Hallo-gebeurtenis is gegenereerd door hello Azure-service verwerken Hallo aanvragen overeenkomende Hallo-gebeurtenis. |
| submissionTimestamp |Tijdstempel wanneer het Hallo-gebeurtenis beschikbaar voor het uitvoeren van query's zijn geworden. |
| subscriptionId |Azure-abonnement-id. |

### <a name="properties-field-per-alert-type"></a>Van eigenschappenveld per type waarschuwing
Hallo eigenschappenveld bevat verschillende waarden, afhankelijk van het Hallo-bron van de waarschuwing gebeurtenis Hallo. Twee gebeurtenisproviders voor algemene waarschuwing zijn activiteitenlogboek van waarschuwingen en metrische waarschuwingen.

#### <a name="properties-for-activity-log-alerts"></a>Eigenschappen van activiteitenlogboek van waarschuwingen
| Elementnaam | Beschrijving |
| --- | --- |
| properties.subscriptionId | Hallo abonnements-ID van het gebeurtenislogboek van het Hallo-activiteit waardoor deze activiteit logboek waarschuwingsregel toobe geactiveerd. |
| properties.eventDataId | Hallo gebeurtenis gegevens-ID van het gebeurtenislogboek van het Hallo-activiteit waardoor deze activiteit logboek waarschuwingsregel toobe geactiveerd. |
| properties.resourceGroup | Hallo-resourcegroep uit het gebeurtenislogboek van het Hallo-activiteit waardoor deze activiteit logboek waarschuwingsregel toobe geactiveerd. |
| properties.resourceId | Hallo resource-ID van het gebeurtenislogboek van het Hallo-activiteit waardoor deze activiteit logboek waarschuwingsregel toobe geactiveerd. |
| properties.eventTimestamp | Hallo gebeurtenis tijdstempel van het gebeurtenislogboek van het Hallo-activiteit waardoor deze activiteit logboek waarschuwingsregel toobe geactiveerd. |
| properties.operationName | Hallo naam van de bewerking van het gebeurtenislogboek van het Hallo-activiteit waardoor deze activiteit logboek waarschuwingsregel toobe geactiveerd. |
| Properties.status | Hallo-status van het gebeurtenislogboek van het Hallo-activiteit waardoor deze activiteit logboek waarschuwingsregel toobe geactiveerd.|

#### <a name="properties-for-metric-alerts"></a>Eigenschappen van metrische waarschuwingen
| Elementnaam | Beschrijving |
| --- | --- |
| Eigenschappen. RuleUri | Bron-ID van Hallo metrische waarschuwingsregel zelf. |
| Eigenschappen. RuleName | Hallo-naam van de metrische waarschuwingsregel Hallo. |
| Eigenschappen. RuleDescription | Hallo beschrijving van Hallo metrische waarschuwingsregel (zoals gedefinieerd in de waarschuwingsregel Hallo). |
| Eigenschappen. Drempelwaarde | Hallo-drempelwaarde in Hallo evaluatie van de metrische waarschuwingsregel Hallo gebruikt. |
| Eigenschappen. WindowSizeInMinutes | Hallo-venstergrootte in Hallo evaluatie van de metrische waarschuwingsregel Hallo gebruikt. |
| Eigenschappen. Aggregatie | Hallo samenvoegingstype in Hallo metrische waarschuwingsregel gedefinieerd. |
| Eigenschappen. Operator | Hallo voorwaardelijke operator die wordt gebruikt in de evaluatie van metrische waarschuwingsregel Hallo Hallo. |
| Eigenschappen. MetricName | Hallo metrische naam van Hallo metric in Hallo evaluatie van de metrische waarschuwingsregel Hallo gebruikt. |
| Eigenschappen. MetricUnit | Hallo metrische eenheid voor Hallo metriek gebruikt in Hallo evaluatie van de metrische waarschuwingsregel Hallo. |

## <a name="autoscale"></a>Automatisch schalen
Deze categorie bevat Hallo-record van een bewerking van de gerelateerde toohello gebeurtenissen van Hallo automatisch schalen-engine op basis van de instellingen voor automatisch schalen die u hebt gedefinieerd in uw abonnement. Een voorbeeld van Hallo type gebeurtenis u in deze categorie ziet is "Automatisch schalen opschaling van de actie is mislukt." Met automatisch schalen, kunt u automatisch geschaald uitbreiden of schalen in Hallo aantal exemplaren in een ondersteunde brontype op basis van tijd van de dag en/of laden (metrische) gegevens met behulp van een instelling voor automatisch schalen. Wanneer Hallo voorwaarden wordt voldaan tooscale omhoog of omlaag Hallo gestart en is voltooid of mislukte gebeurtenissen worden vastgelegd in deze categorie.

### <a name="sample-event"></a>Voorbeeld van de gebeurtenis
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a>Eigenschapbeschrijvingen
| Elementnaam | Beschrijving |
| --- | --- |
| aanroeper | Altijd Microsoft.Insights/autoscaleSettings |
| kanalen | Altijd 'Admin, bewerking' |
| Claims | JSON-blob met Hallo SPN (service principal name) of de resource-type, van Hallo-engine voor automatisch schalen. |
| correlationId | Een GUID in de indeling van tekenreeks Hallo. |
| description |Statische tekstbeschrijving van gebeurtenis voor Hallo-automatisch schalen. |
| eventDataId |De unieke id van Hallo automatisch schalen gebeurtenis. |
| niveau |Niveau van het Hallo-gebeurtenis. Een van de volgende waarden Hallo: 'Kritiek', 'Fout', 'Waarschuwing', 'Ter informatie' en 'Verbose' |
| resourceGroupName |De naam van de resourcegroep Hallo voor Hallo-instelling voor automatisch schalen. |
| resourceProviderName |Naam van de resourceprovider Hallo voor Hallo-instelling voor automatisch schalen. |
| resourceId |Bron-id van het Hallo-instelling voor automatisch schalen. |
| operationId |Een GUID die wordt gedeeld door Hallo-gebeurtenissen die overeenkomen met tooa één bewerking. |
| operationName |Naam van Hallo-bewerking. |
| properties |Een set `<Key, Value>` paren (dat wil zeggen, een woordenlijst) Hallo details van gebeurtenis Hallo beschrijven. |
| Eigenschappen. Beschrijving | Gedetailleerde beschrijving van wat Hallo-engine voor automatisch schalen die werd uitgevoerd. |
| Eigenschappen. ResourceName | Bron-ID van Hallo van invloed op resource (Hallo resource op welke Hallo schaalactie werd uitgevoerd) |
| Eigenschappen. OldInstancesCount | het aantal exemplaren vóór Hallo automatisch schalen actie Hallo van kracht. |
| Eigenschappen. NewInstancesCount | het aantal exemplaren na Hallo automatisch schalen actie Hallo van kracht. |
| Eigenschappen. LastScaleActionTime | Hallo tijdstempel van waarop Hallo automatisch schalen actie is uitgevoerd. |
| status |Tekenreeks die Hallo status van Hallo-bewerking. Sommige algemene waarden zijn: In voortgang, geslaagd, mislukt, actief, opgelost gestart. |
| subStatus | Meestal null voor automatisch schalen. |
| eventTimestamp |Tijdstempel wanneer het Hallo-gebeurtenis is gegenereerd door hello Azure-service verwerken Hallo aanvragen overeenkomende Hallo-gebeurtenis. |
| submissionTimestamp |Tijdstempel wanneer het Hallo-gebeurtenis beschikbaar voor het uitvoeren van query's zijn geworden. |
| subscriptionId |Azure-abonnement-id. |

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over Hallo activiteitenlogboek (voorheen controlelogboeken)](monitoring-overview-activity-logs.md)
* [Stream hello Azure Activity Log tooEvent Hubs](monitoring-stream-activity-logs-event-hubs.md)
