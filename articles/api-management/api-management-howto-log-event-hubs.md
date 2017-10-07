---
title: aaaHow toolog gebeurtenissen tooAzure Event Hubs in Azure API Management | Microsoft Docs
description: Meer informatie over hoe toolog gebeurtenissen tooAzure Event Hubs in Azure API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 88f6507d-7460-4eb2-bffd-76025b73f8c4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 09ca65fc48a874467c6662858f7594e9b19fcdb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a>Hoe toolog gebeurtenissen tooAzure Event Hubs in Azure API Management
Azure Event Hubs is een uiterst schaalbare inkomend gegevensservice die miljoenen gebeurtenissen per seconde opnemen kan, zodat u kunt verwerken en analyseren van Hallo enorme hoeveelheden gegevens die worden geproduceerd door verbonden apparaten en toepassingen. Event Hubs fungeert als Hallo 'voordeur' van een gebeurtenispijplijn en zodra gegevens zijn verzameld in een event hub, kunnen worden omgezet en opgeslagen met een realtime-analyseprovider of batchverwerking/opslagadapters. Event Hubs worden losgekoppeld Hallo productie van een stream van gebeurtenissen van Hallo gebruik van deze gebeurtenissen, zodat gebeurtenisconsumers Hallo gebeurtenissen op basis van hun eigen planning kunnen openen.

Dit artikel is een aanvullende toohello [Azure API Management integreren met Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video en beschrijft hoe toolog API Management-gebeurtenissen met Azure Event Hubs.

## <a name="create-an-azure-event-hub"></a>Een Azure Event Hub maken
een nieuwe Event Hub, aanmelden toohello toocreate [klassieke Azure-portal](https://manage.windowsazure.com) en klik op **nieuw**->**App Services**->**Service Bus**  -> **Event Hub**->**snelle invoer**. Voer een naam Event Hub, regio, selecteer een abonnement en selecteer een naamruimte. Als u nog niet eerder hebt gemaakt met een naamruimte kunt u een door een naam te typen in Hallo **Namespace** textbox. Nadat alle eigenschappen zijn geconfigureerd, klikt u op **maken van een nieuwe Event Hub** toocreate Hallo Event Hub.

![Event hub maken][create-event-hub]

Vervolgens gaat u toohello **configureren** tabblad voor uw nieuwe Event Hub en maak twee **gedeeld toegangsbeleid**. Naam Hallo eerste **verzenden** en hieraan **verzenden** machtigingen.

![Verzenden van beleid][sending-policy]

Naam Hallo tweede **ontvangen**, geeft u het **luisteren** machtigingen en klik op **opslaan**.

![Beleid ontvangen][receiving-policy]

Elk gedeeld toegangsbeleid kunt toepassingen toosend en tooand gebeurtenissen ontvangen van Hallo Event Hub. tooaccess Hallo-verbindingsreeksen voor deze beleidsregels Navigeer toohello **Dashboard** tabblad Hallo Event Hub en klik op **verbindingsgegevens**.

![Verbindingsreeks][event-hub-dashboard]

Hallo **verzenden** verbindingsreeks wordt gebruikt bij het vastleggen van gebeurtenissen, en Hallo **ontvangen** verbindingsreeks wordt gebruikt bij het downloaden van gebeurtenissen van Hallo Event Hub.

![Verbindingsreeks][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a>Maken van een API Management-logboek
Nu dat u een Event Hub hebt, de volgende stap Hallo tooconfigure is een [berichtenlogboek](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in uw API Management-service zodat deze zich gebeurtenissen toohello Event Hub aanmelden kan.

API Management voorkomen zijn geconfigureerd met Hallo [API Management REST API](http://aka.ms/smapi). Controleer voordat u Hallo REST-API voor Hallo eerst gebruikt, Hallo [vereisten](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) en zorg ervoor dat er [toegang toohello REST-API ingeschakeld](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).

toocreate een logboek maken een HTTP PUT-aanvraag met Hallo URL sjabloon te volgen.

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* Vervang `{your service}` met Hallo-naam van uw API Management-service-exemplaar.
* Vervang `{new logger name}` met Hallo gewenste naam voor uw nieuwe berichtenlogboek. U verwijst bij het configureren van Hallo deze naam [logboek voor eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) beleid

Hallo na headers toohello aanvraag toevoegen.

* Content-Type: application/json
* Autorisatie: SharedAccessSignature 58...
  * Voor instructies voor het genereren van Hallo `SharedAccessSignature` Zie [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).

Hallo aanvraagtekst met behulp van de volgende sjabloon Hallo opgeven.

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of hello Event Hub from hello Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* `type`te moet worden ingesteld`AzureEventHub`.
* `description`biedt een optionele beschrijving van Hallo berichtenlogboek en tekenreekslengte van nul kan zijn, indien gewenst.
* `credentials`Hallo bevat `name` en `connectionString` van uw Azure Event Hub.

Wanneer u indienen hello, als Hallo berichtenlogboek statuscode is gemaakt `201 Created` wordt geretourneerd.

> [!NOTE]
> Zie voor andere mogelijke retourcodes en hun redenen [maken van een logboek](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT). andere bewerkingen toosee hoe uitvoeren, zoals de lijst, bijwerken en verwijderen, Zie Hallo [berichtenlogboek](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entiteit documentatie.
>
>

## <a name="configure-log-to-eventhubs-policies"></a>Logboek-eventhubs-beleid configureren
Nadat uw berichtenlogboek in API Management is geconfigureerd, kunt u uw logboek-eventhubs-beleid toolog Hallo gewenst gebeurtenissen configureren. Hallo logboek-eventhubs-beleid kan worden gebruikt in beide Hallo binnenkomende of beleidssectie Hallo uitgaande beleid.

beleid voor tooconfigure aanmelden toohello [Azure-portal](https://portal.azure.com), gaat u tooyour API Management-service en klik op **publicatieportal** tooaccess Hallo publicatieportal.

![Publicatieportal][publisher-portal]

Klik op **beleid** Selecteer de gewenste product Hallo en API Hallo API Management-menu op Hallo links, en klik op **beleid toevoegen**. In dit voorbeeld wordt bij het toevoegen van een beleid toohello **Echo-API** in Hallo **onbeperkt** product.

![Beleid toevoegen][add-policy]

Plaats de cursor in Hallo `inbound` beleid sectie en klikt u op Hallo **logboek tooEventHub** beleid tooinsert hello `log-to-eventhub` beleidssjabloon-instructie.

![Beleidseditor][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

Vervang `logger-id` met de naam van Hallo API Management berichtenlogboek die u hebt geconfigureerd in de vorige stap Hallo Hallo.

U kunt een expressie die een tekenreeks als waarde voor Hallo Hallo retourneert `log-to-eventhub` element. In dit voorbeeld is een tekenreeks met Hallo datum en tijd, servicenaam, aanvraag-id, aanvraag IP-adres en naam van de bewerking wordt vastgelegd.

Klik op **opslaan** toosave Hallo beleidsconfiguratie bijgewerkt. Zodra deze is opgeslagen Hallo beleid actief is en gebeurtenissen worden vastgelegd toohello aangewezen Event Hub.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over Azure Event Hubs
  * [Aan de slag met Azure Event Hubs](../event-hubs/event-hubs-c-getstarted-send.md)
  * [Berichten ontvangen met EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [Programmeerhandleiding voor Event Hubs](../event-hubs/event-hubs-programming-guide.md)
* Meer informatie over de integratie van API Management en Event Hubs
  * [Entiteitsverwijzing berichtenlogboek](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [documentatie voor logboek-eventhub-beleid](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [Uw API's met Azure API Management, Event Hubs en Runscope bewaken](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a>Bekijk een video-overzicht
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Integrate-Azure-API-Management-with-Event-Hubs/player]
>
>

[publisher-portal]: ./media/api-management-howto-log-event-hubs/publisher-portal.png
[create-event-hub]: ./media/api-management-howto-log-event-hubs/create-event-hub.png
[event-hub-connection-string]: ./media/api-management-howto-log-event-hubs/event-hub-connection-string.png
[event-hub-dashboard]: ./media/api-management-howto-log-event-hubs/event-hub-dashboard.png
[receiving-policy]: ./media/api-management-howto-log-event-hubs/receiving-policy.png
[sending-policy]: ./media/api-management-howto-log-event-hubs/sending-policy.png
[event-hub-policy]: ./media/api-management-howto-log-event-hubs/event-hub-policy.png
[add-policy]: ./media/api-management-howto-log-event-hubs/add-policy.png
