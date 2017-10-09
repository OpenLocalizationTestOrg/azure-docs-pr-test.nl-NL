---
title: aaaAzure Event Hubs uitzonderingen messaging | Microsoft Docs
description: Lijst met Azure Event Hubs messaging-uitzonderingen en voorgestelde acties.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2c6273de-0106-47e5-b45d-59040e51f2c5
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 9c164e76612c26607219f08407f689aaab4050a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-messaging-exceptions"></a>Event Hubs-berichtuitzonderingen
In dit artikel vindt u enkele van Hallo uitzonderingen die worden gegenereerd door hello Azure Service Bus-berichtenservice-API's, waaronder Event Hubs. Deze verwijzing is onderwerp toochange, Controleer dus regelmatig op updates.

## <a name="exception-categories"></a>Uitzondering categorieën
Hallo Event Hubs-API's genereren uitzonderingen die in de volgende categorieën Hallo kunnen vallen, samen met de actie die is gekoppeld Hallo u tootry toofix kunt nemen ze.

1. Gebruiker coderen fout: [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [ System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). Algemene actie: probeer toofix Hallo code voordat u doorgaat.
2. Setup/configuratiefout: [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception), [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception), [ System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). Algemene actie: Controleer de configuratie en wijzig indien nodig.
3. Tijdelijke uitzonderingen: [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](#serverbusyexception), [ Microsoft.Azure.EventHubs.ServerBusyException](#serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). Algemene actie: Hallo-bewerking opnieuw proberen of gebruikers een melding ontvangen.
4. Andere uitzonderingen: [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](#timeoutexception), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception). Algemene actie: uitzonderingstype voor specifieke toohello; Raadpleeg toohello tabel in de volgende sectie Hallo. 

## <a name="exception-types"></a>Uitzondering typen
Hallo volgende tabel bevat messaging uitzondering typen, en hun oorzaken en opmerkingen bij de voorgestelde actie die u kunt nemen.

| **Uitzonderingstype** | **Oorzaak-beschrijving/voorbeelden** | **Voorgestelde actie** | **Houd er rekening mee op automatische/direct opnieuw proberen** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Hallo server heeft niet gereageerd toohello aangevraagd bewerking binnen Hallo opgegeven tijd, die wordt beheerd door [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout). Hallo-server mogelijk nog voltooid Hallo bewerking aangevraagd. Dit kan gebeuren vanwege toonetwork of andere vertragingen infrastructuur. |Controleer de systeemstatus Hallo voor consistentie en probeer indien nodig.<br /> Zie [TimeoutException](#timeoutexception). |Probeer het opnieuw kan helpen in sommige gevallen; Probeer het opnieuw logica toocode toevoegen. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Hallo aangevraagd bewerking van de gebruiker is niet toegestaan binnen het Hallo-server of -service. Zie Hallo-bericht van uitzondering voor meer informatie. Bijvoorbeeld: [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) deze uitzondering wordt gegenereerd als het Hallo-bericht is ontvangen [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) modus. |Controleer Hallo code en Hallo-documentatie. Zorg ervoor dat Hallo aangevraagde bewerking is ongeldig. |Probeer het opnieuw helpt niet. |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Een poging is gedaan tooinvoke een bewerking op een object dat al is gesloten, afgebroken of verwijderd. In zeldzame gevallen, is Hallo ambient transactie al verwijderd. |Controleer Hallo code en zorg ervoor dat deze bewerkingen worden uitgevoerd op een verwijderd object niet gestart. |Probeer het opnieuw helpt niet. |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Hallo [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) object kan niet een token verkrijgen of Hallo token bevat geen Hallo claims vereist tooperform Hallo bewerking Hallo-token is ongeldig. |Zorg ervoor dat de tokenprovider Hallo wordt gemaakt met de juiste waarden Hallo. Controleer de configuratie van Hallo Hallo Access Control-service. |Probeer het opnieuw kan helpen in sommige gevallen; Probeer het opnieuw logica toocode toevoegen. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Een of meer argumenten opgegeven toohello methode zijn ongeldig. Hallo URI opgegeven te[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) of [maken](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) pad segment(en) bevat. Hallo-URI-schema te opgegeven[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) of [maken](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) is ongeldig. Hallo-eigenschapswaarde is groter dan 32KB. |Controleer de aanroepende code Hallo en zorg ervoor dat Hallo argumenten juist zijn. |Probeer het opnieuw helpt niet. |
| [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) <br /> [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception) |Entiteit gekoppeld Hallo-bewerking is niet aanwezig of is verwijderd. |Zorg ervoor dat Hallo entiteit bestaat. |Probeer het opnieuw helpt niet. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |Poging tooreceive een bericht met een bepaalde volgnummer. Dit bericht is niet gevonden. |Zorg ervoor dat het Hallo-bericht niet al is ontvangen. Controleer Hallo onbestelbare wachtrij toosee als het Hallo-bericht deadlettered is. |Probeer het opnieuw helpt niet. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |Client is geen kunnen tooestablish een verbinding tooEvent Hub. |Zorg ervoor dat de opgegeven Hallo-hostnaam juist is en Hallo host kan worden bereikt. |Probeer het opnieuw kan u helpen als er onregelmatige verbindingsproblemen. |
| [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) <br /> [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) |Service is niet kunnen tooprocess Hallo aanvraag op dit moment. |Client kan wachten op een bepaalde tijd en probeer opnieuw Hallo. <br /> Zie [ServerBusyException](#serverbusyexception). |Client kan opnieuw na een bepaalde interval. Als een nieuwe poging in een andere uitzondering resulteert, controleert u gedrag van deze uitzondering voor het opnieuw. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Vergrendelingstoken die is gekoppeld aan het Hallo-bericht is verlopen of Hallo Vergrendelingstoken is niet gevonden. |Verwijderen van het Hallo-bericht. |Probeer het opnieuw helpt niet. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |Vergrendeling die zijn gekoppeld aan deze sessie wordt verbroken. | Hallo afbreken [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) object. |Probeer het opnieuw helpt niet. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |Algemene uitzondering die kan worden gegenereerd in de volgende gevallen Hallo messaging: er wordt geprobeerd toocreate een [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) met een naam of het pad dat verschillende entiteitstype tooa (bijvoorbeeld een onderwerp) behoort. Een poging is gedaan toosend een bericht groter is dan 256KB. Hallo-server of -service is een fout opgetreden tijdens het verwerken van Hallo-aanvraag. Zie Hallo-bericht van uitzondering voor meer informatie. Dit is meestal een tijdelijke uitzondering. |Hallo code controleren en ervoor te zorgen dat alleen serialiseerbaar objecten worden gebruikt voor de berichttekst hello (of gebruik een aangepaste serialisatiefunctie). Raadpleeg de documentatie Hallo voor waardetypen Hallo ondersteund van Hallo eigenschappen en alleen de gebruikstypen die worden ondersteund. Controleer de Hallo [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) eigenschap. Als het **true**, kunt u Hallo-bewerking opnieuw. |Gedrag voor opnieuw proberen is niet gedefinieerd en niet kan helpen. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |Poging toocreate een entiteit met een naam die al door een andere entiteit in de naamruimte van die service gebruikt wordt. |Hallo bestaande entiteit verwijderen of kies een andere naam voor Hallo entiteit toobe gemaakt. |Probeer het opnieuw helpt niet. |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |Hallo messaging entiteit heeft de maximaal toegestane grootte bereikt. Dit kan gebeuren als Hallo maximum aantal ontvangers (dit is 5) is al geopend op een groepeerniveau per gebruiker. |Maak schijfruimte vrij in Hallo entiteit door berichten ontvangt van Hallo entiteit of de onderliggende wachtrijen. <br /> Zie [QuotaExceededException](#quotaexceededexception) |Probeer het opnieuw kan u helpen als berichten zijn verwijderd in Hallo tussentijd. |
|  | | | |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |Poging een sessie met een bepaalde sessie-ID, maar het Hallo-sessie is momenteel vergrendeld door een andere client tooaccept. |Zorg ervoor dat het Hallo-sessie wordt ontgrendeld door andere clients. |Probeer het opnieuw kan u helpen als Hallo-sessie in Hallo tussentijdse is vrijgegeven. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |Te veel bewerkingen maken deel uit van Hallo transactie. |Verminder het aantal bewerkingen die deel uitmaken van deze transactie Hallo. |Probeer het opnieuw helpt niet. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |Aanvraag voor een Runtimebewerking op een uitgeschakelde entiteit. |Hallo entiteit activeren. |Probeer het opnieuw kan u helpen als Hallo entiteit in Hallo tussentijdse is geactiveerd. |
| [Microsoft.ServiceBus.Messaging.MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) <br /> [Microsoft.Azure.EventHubs.MessageSizeExceededException](/dotnet/api/microsoft.azure.eventhubs.messagesizeexceededexception) | Een bericht nettolading overschrijdt de limiet van 256 kB Hallo. Houd er rekening mee deze limiet van 256 kB Hallo Hallo totale grootte, waaronder Systeemeigenschappen en een .NET-overhead. |Hallo verkleinen van nettolading voor Hallo-bericht en probeer Hallo opnieuw. |Probeer het opnieuw helpt niet. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |Hallo ambient transactie (*Transaction.Current*) is ongeldig. Mogelijk is het voltooid of afgebroken. De binnenste uitzondering biedt mogelijk meer informatie. | |Probeer het opnieuw helpt niet. |
| [TransactionInDoubtException](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |Een bewerking wordt uitgevoerd voor een transactie is onzeker, of een poging is gedaan toocommit Hallo transactie en Hallo transactie is onzeker. |Uw toepassing moet deze uitzondering (als een speciaal geval), verwerken, zoals Hallo transactie al doorgevoerd is mogelijk. |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) geeft aan dat een quotum voor een specifieke entiteit is overschreden.

Dit kan gebeuren als Hallo kunt u het maximum aantal ontvangers (5) is al geopend op een groepeerniveau per gebruiker.

### <a name="event-hubs"></a>Event Hubs
Event Hubs is een limiet van 20 consumergroepen per Event Hub. Wanneer u meer toocreate probeert, krijgt u een [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception). 

## <a name="timeoutexception"></a>TimeoutException
Een [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) geeft aan dat een gebruiker gestart bewerking langer dan de time-out voor Hallo-bewerking duurt. 

Event Hubs Hallo time-out is opgegeven als onderdeel van de verbindingsreeks Hallo of via [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). Hallo foutbericht zelf kan variëren, maar bevat altijd Hallo time-outwaarde voor de huidige bewerking Hallo opgegeven. 

### <a name="common-causes"></a>Algemene oorzaken
Er zijn twee algemene oorzaken voor deze fout: onjuiste configuratie of een tijdelijke servicefout.

1. **Onjuiste configuratie** time-out voor Hallo-bewerking is mogelijk te klein voor Hallo operationele voorwaarde. de standaardwaarde Hallo voor time-out van de bewerking Hallo in Hallo client SDK is 60 seconden. Controleer toosee als uw code Hallo-waarde heeft ingesteld toosomething te klein. Houd er rekening mee die voorwaarde Hallo van Hallo netwerk en CPU-gebruik Hallo-tijd die nodig is voor een bepaalde bewerking toocomplete, zodat de time-out voor Hallo-bewerking mag niet worden ingesteld tooa zeer kleine waarde kan beïnvloeden.
2. **Tijdelijke servicefout** soms Hallo Event Hubs-service kan vertragingen bij het verwerken van aanvragen, bijvoorbeeld tijdens perioden met intensief verkeer. In dergelijke gevallen kunt u de bewerking na een vertraging opnieuw proberen totdat het Hallo-bewerking is voltooid. Als hello dezelfde bewerking steeds na meerdere pogingen mislukt, gaat u naar Hallo [Azure service status site](https://azure.microsoft.com/status/) toosee als er bekende serviceonderbrekingen.

## <a name="serverbusyexception"></a>ServerBusyException

Een [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) of [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) geeft aan dat een server overbelast is. Er zijn twee relevante foutcodes voor deze uitzondering.

### <a name="error-code-50002"></a>Foutcode 50002

Deze fout kan optreden vanwege een van twee redenen:

1. Hallo load niet evenredig verdeeld over alle partities op Hallo Event Hub en één partitie treffers Hallo lokale doorvoer eenheid beperking.
    
    Oplossing: Hallo partitie distributiestrategie herzien of probeert [EventHubClient.Send(eventDataWithOutPartitionKey)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) kan helpen.

2. Hallo Event Hubs-naamruimte heeft geen voldoende doorvoereenheden (u kunt controleren Hallo **metrische gegevens** blade in Event Hubs naamruimte blade in Hallo [Azure-portal](https://portal.azure.com) tooconfirm). Houd er rekening mee dat Hallo portal informatie weer geaggregeerde (1 minuut geeft), maar we Hallo doorvoer in realtime – meten dus is het een schatting maken.

    Oplossing: Hallo doorvoer eenheden op Hallo naamruimte kunnen helpen te verbeteren. U kunt dit doen op Hallo-portal in Hallo **Scale** blade van Hallo Event Hubs naamruimte blade.

### <a name="error-code-50001"></a>Foutcode 50001

Deze fout moet zelden optreden. Dit gebeurt wanneer het Hallo-container met code voor de naamruimte is weinig CPU – niet meer dan een paar seconden alvorens het Hallo Event Hubs niet laden balancer begint.


## <a name="next-steps"></a>Volgende stappen
U meer informatie over Event Hubs via Hallo koppelingen te volgen:

* [Event Hubs-overzicht](event-hubs-what-is-event-hubs.md)
* [Een Event Hub maken](event-hubs-create.md)
* [Veelgestelde vragen over Event Hubs](event-hubs-faq.md)
