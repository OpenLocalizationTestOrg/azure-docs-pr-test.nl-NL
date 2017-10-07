---
title: aaaCall een webhook op Azure Activity Log waarschuwingen | Microsoft Docs
description: Route activiteit logboek gebeurtenissen tooother services voor aangepaste acties. Bijvoorbeeld SMS-bericht verzenden, meld bugs of hoogte van een team via chat/messaging-service.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a>Een webhook aanroepen in Azure Activity Log waarschuwingen
Webhooks kunt u een Azure tooroute melding tooother systemen voor na verwerking of aangepaste acties een waarschuwing. U kunt een webhook gebruiken op een waarschuwing tooroute het tooservices die verzenden SMS, meld bugs, melding van een team via chat/berichtenservices of komen een aantal andere acties. Dit artikel wordt beschreven hoe een webhook toobe tooset wordt aangeroepen wanneer een waarschuwing wordt geactiveerd voor een Azure Activity Log. U ziet ook welke Hallo nettolading voor Hallo HTTP POST tooa webhook lijkt. Voor informatie over het Hallo-installatie en het schema voor een Azure metrische waarschuwing [deze pagina vindt u in plaats daarvan](insights-webhooks-alerts.md). U kunt ook een activiteitenlogboek waarschuwing toosend e-mailbericht wanneer geactiveerd instellen.

> [!NOTE]
> Deze functie is momenteel in preview en op een bepaald moment in toekomstige hello wordt verwijderd.
>
>

U kunt een activiteitenlogboek waarschuwing met Hallo instellen [Azure PowerShell-Cmdlets](insights-powershell-samples.md#create-metric-alerts), [platformoverschrijdende CLI](insights-cli-samples.md#work-with-alerts), of [REST-API van Azure-Monitor](https://msdn.microsoft.com/library/azure/dn933805.aspx). U instellen niet op dit moment een met behulp van hello Azure-portal.

## <a name="authenticating-hello-webhook"></a>Hallo webhook verifiëren
Hallo webhook kunt verifiëren met behulp van deze methoden:

1. **Op basis van tokens autorisatie** -Hallo webhook URI wordt opgeslagen met een token ID, bijvoorbeeld:`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`
2. **Basisverificatie** -Hallo webhook URI wordt opgeslagen met een gebruikersnaam en wachtwoord, bijvoorbeeld:`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`

## <a name="payload-schema"></a>De nettolading van schema
Hallo POST-bewerking bevat Hallo volgende JSON-nettolading en het schema voor alle activiteitenlogboek op basis van waarschuwingen. Dit schema is vergelijkbaar toohello één door waarschuwingen op basis van metrische gegevens gebruikt.

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| Elementnaam | Beschrijving |
| --- | --- |
| status |Gebruikt voor metrische waarschuwingen. Altijd ingesteld te 'actief' voor activiteitenlogboek van waarschuwingen. |
| Context |De context van Hallo-gebeurtenis. |
| resourceProviderName |de resourceprovider Hallo Hallo beïnvloed resource. |
| conditionType |Altijd 'gebeurtenis'. |
| naam |Naam van de waarschuwingsregel Hallo. |
| id |Bron-ID van het Hallo-waarschuwing. |
| description |Beschrijving van de waarschuwing als set tijdens het maken van Hallo waarschuwing. |
| subscriptionId |Azure-abonnement-ID. |
| tijdstempel |De tijd op welke Hallo gebeurtenis is gegenereerd door hello Azure-service die Hallo aanvraag verwerkt. |
| resourceId |Bron-ID van Hallo beïnvloed resource. |
| resourceGroupName |Naam van de resourcegroep Hallo voor Hallo beïnvloed resource |
| properties |Een set `<Key, Value>` paren (dat wil zeggen `Dictionary<String, String>`) die bevat details over Hallo-gebeurtenis. |
| Gebeurtenis |Element met metagegevens over Hallo-gebeurtenis. |
| Autorisatie |Hallo RBAC eigenschappen van gebeurtenis Hallo. Hierbij doorgaans Hallo 'action', 'rol' en Hallo 'bereik." |
| category |De categorie van het Hallo-gebeurtenis. Ondersteunde waarden zijn: administratieve, waarschuwing, beveiliging, ServiceHealth, aanbeveling. |
| aanroeper |E-mailadres van Hallo-gebruiker die heeft uitgevoerd Hallo bewerking, UPN-claim of SPN claim op basis van beschikbaarheid. Kan niet null zijn voor bepaalde systeemaanroepen zijn. |
| correlationId |Meestal een GUID in de indeling van tekenreeks. Gebeurtenissen met correlationId behoren toohello dezelfde groter actie en meestal een correlationId delen. |
| eventDescription |De beschrijving van de statische tekst hello gebeurtenis. |
| eventDataId |De unieke id voor Hallo-gebeurtenis. |
| EventSource |Naam van hello Azure-service of de infrastructuur die gegenereerde Hallo-gebeurtenis. |
| httpRequest |Omvat gewoonlijk Hallo 'clientRequestId', "clientIpAddress" en "method" (bijv. HTTP-methode plaatsen). |
| niveau |Een van de volgende waarden Hallo: 'Kritiek', 'Fout', 'Waarschuwing', 'Ter informatie' en "Verbose." |
| operationId |Meestal een GUID gedeeld door Hallo gebeurtenissen toosingle bewerking hoort. |
| operationName |Naam van Hallo-bewerking. |
| properties |Eigenschappen van gebeurtenis Hallo. |
| status |De tekenreeks. De status van Hallo-bewerking. Algemene waarden zijn: 'Gestart', 'Wordt uitgevoerd', 'Geslaagd', 'Is mislukt', 'Active', 'Opgelost'. |
| subStatus |Omvat gewoonlijk Hallo HTTP-statuscode van de bijbehorende REST-aanroep Hallo. Het kan ook andere tekenreeksen met een beschrijving van een substatus omvatten. Algemene substatus waarden zijn: OK (HTTP-statuscode: 200), gemaakt (HTTP-statuscode: 201), geaccepteerde (HTTP-statuscode: 202), geen inhoud (HTTP-statuscode: 204), ongeldige aanvraag (HTTP-statuscode: 400), niet vinden (HTTP-statuscode: 404), Conflict (HTTP-statuscode: 409), interne serverfout (HTTP-statuscode: 500), Service niet beschikbaar (HTTP-statuscode: 503), time-out van Gateway (HTTP-statuscode: 504) |

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over Hallo Activity Log](monitoring-overview-activity-logs.md)
* [Azure Automation-scripts (Runbooks) op waarschuwingen van Azure uitvoeren](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Gebruik van de logische App toosend een SMS-bericht via Twilio vanuit een Azure waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). In dit voorbeeld is voor metrische waarschuwingen, maar het gewijzigde toowork met een waarschuwing activiteitenlogboek kan worden.
* [Gebruik van de logische App toosend een toegestane bericht van een Azure waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). In dit voorbeeld is voor metrische waarschuwingen, maar het gewijzigde toowork met een waarschuwing activiteitenlogboek kan worden.
* [Gebruik toosend logische App een bericht tooan Azure Queue vanuit een Azure waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). In dit voorbeeld is voor metrische waarschuwingen, maar het gewijzigde toowork met een waarschuwing activiteitenlogboek kan worden.
