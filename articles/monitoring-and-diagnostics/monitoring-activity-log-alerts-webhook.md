---
title: aaaUnderstand hello webhook schema gebruikt in activiteit logboek waarschuwingen | Microsoft Docs
description: Meer informatie over het Hallo-schema van Hallo JSON die wordt gepost tooa webhook-URL wanneer een activiteit logboek waarschuwing wordt geactiveerd.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a>Webhooks voor Azure activiteit logboek waarschuwingen
Als onderdeel van het Hallo-definitie van een actiegroep, kunt u de webhook eindpunten tooreceive activiteit logboek meldingen van waarschuwingen configureren. Met webhooks, kunt u deze meldingen tooother systemen voor na verwerking of aangepaste acties te routeren. Dit artikel laat zien welke Hallo nettolading voor Hallo HTTP POST tooa webhook lijkt.

Zie hoe te voor meer informatie over activiteit logboek waarschuwingen[Azure activiteit logboek waarschuwingen maken](monitoring-activity-log-alerts.md).

Zie hoe te voor informatie over actiegroepen[Actiegroepen maken](monitoring-action-groups.md).

## <a name="authenticate-hello-webhook"></a>Hallo webhook verifiëren
Hallo webhook kan eventueel autorisatie op basis van tokens gebruiken voor verificatie. Hallo webhook URI wordt opgeslagen met een token ID, bijvoorbeeld `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.

## <a name="payload-schema"></a>De nettolading van schema
Hallo JSON-nettolading is opgenomen in Hallo POST-bewerking verschilt op basis van Hallo-nettolading data.context.activityLog.eventSource veld.

###<a name="common"></a>Algemene
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a>Beheerdersrechten
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a>ServiceHealth
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

Zie voor specifieke schema-informatie over de service health melding activiteit logboek waarschuwingen, [Service health meldingen](monitoring-service-notifications.md).

Zie voor meer informatie voor een specifiek schema bij alle waarschuwingen van andere activiteit logboek, [overzicht van hello Azure activiteitenlogboek](monitoring-overview-activity-logs.md).

| Elementnaam | Beschrijving |
| --- | --- |
| status |Gebruikt voor metrische waarschuwingen. Altijd ingesteld te 'actief' voor activiteit logboek waarschuwingen. |
| Context |De context van Hallo-gebeurtenis. |
| resourceProviderName |de resourceprovider Hallo Hallo beïnvloed resource. |
| conditionType |Altijd 'gebeurtenis'. |
| naam |Naam van de waarschuwingsregel Hallo. |
| id |Bron-ID van het Hallo-waarschuwing. |
| description |Beschrijving van de waarschuwing ingesteld wanneer Hallo waarschuwing wordt gemaakt. |
| subscriptionId |Azure-abonnement-ID. |
| tijdstempel |De tijd op welke Hallo gebeurtenis is gegenereerd door hello Azure-service die Hallo aanvraag verwerkt. |
| resourceId |Bron-ID van Hallo beïnvloed resource. |
| resourceGroupName |Naam van de resourcegroep Hallo voor Hallo beïnvloed resource. |
| properties |Een set `<Key, Value>` paren (dat wil zeggen, `Dictionary<String, String>`) die bevat details over Hallo-gebeurtenis. |
| Gebeurtenis |Element met metagegevens over Hallo-gebeurtenis. |
| Autorisatie |Hallo eigenschappen van gebeurtenis Hallo toegangsbeheer op basis van rollen. Deze eigenschappen zijn meestal Hallo actie, Hallo-rol en Hallo bereik. |
| category |De categorie van het Hallo-gebeurtenis. Ondersteunde waarden zijn Administrative, waarschuwing, beveiliging, ServiceHealth en aanbeveling. |
| aanroeper |E-mailadres van Hallo-gebruiker die heeft uitgevoerd Hallo bewerking, UPN-claim of SPN claim op basis van beschikbaarheid. Kan niet null zijn voor bepaalde systeemaanroepen zijn. |
| correlationId |Meestal een GUID in de indeling van tekenreeks. Gebeurtenissen met correlationId behoren toohello dezelfde groter actie en meestal een correlationId delen. |
| eventDescription |De beschrijving van de statische tekst hello gebeurtenis. |
| eventDataId |De unieke id voor Hallo-gebeurtenis. |
| EventSource |Naam van hello Azure-service of de infrastructuur die gegenereerde Hallo-gebeurtenis. |
| httpRequest |Hallo aanvraag omvat gewoonlijk Hallo clientRequestId clientIpAddress en HTTP-methode (bijvoorbeeld plaatsen). |
| niveau |Een van de volgende waarden Hallo: kritiek, fout, waarschuwing, informatief van aard en uitgebreid. |
| operationId |Meestal een GUID gedeeld door Hallo gebeurtenissen toosingle bewerking hoort. |
| operationName |Naam van Hallo-bewerking. |
| properties |Eigenschappen van gebeurtenis Hallo. |
| status |De tekenreeks. De status van Hallo-bewerking. Algemene waarden zijn gestart, wordt uitgevoerd, geslaagd, mislukt, actief en opgelost. |
| subStatus |Omvat gewoonlijk Hallo HTTP-statuscode van de bijbehorende REST-aanroep Hallo. Het kan ook andere tekenreeksen die een substatus beschrijven omvatten. Algemene substatus waarden zijn OK (HTTP-statuscode: 200), gemaakt (HTTP-statuscode: 201), geaccepteerde (HTTP-statuscode: 202), geen inhoud (HTTP-statuscode: 204), ongeldige aanvraag (HTTP-statuscode: 400), niet vinden (HTTP-statuscode: 404), Conflict (HTTP-statuscode: 409), interne serverfout (HTTP-statuscode: 500), Service niet beschikbaar (HTTP-statuscode: 503), en de time-out van Gateway (HTTP-statuscode : 504). |

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over het activiteitenlogboek Hallo](monitoring-overview-activity-logs.md).
* [Azure automatiseringsscripts (Runbooks) uitvoeren op Azure waarschuwingen](http://go.microsoft.com/fwlink/?LinkId=627081).
* [Gebruik van een logische app toosend een SMS-bericht via Twilio vanuit een Azure waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). In dit voorbeeld is voor metrische waarschuwingen, maar het gewijzigde toowork logboek met een activiteit kan zijn.
* [Gebruik van een logische app toosend een toegestane bericht van een Azure waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). In dit voorbeeld is voor metrische waarschuwingen, maar het gewijzigde toowork logboek met een activiteit kan zijn.
* [Gebruik van een logische app toosend een bericht tooan Azure wachtrij door een Azure-waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). In dit voorbeeld is voor metrische waarschuwingen, maar het gewijzigde toowork logboek met een activiteit kan zijn.
