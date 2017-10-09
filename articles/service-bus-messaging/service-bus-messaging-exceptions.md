---
title: messaging-Service Bus-uitzonderingen aaaAzure | Microsoft Docs
description: Lijst met Service Bus messaging uitzonderingen en voorgestelde acties.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3d8526fe-6e47-4119-9f3e-c56d916a98f9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: sethm
ms.openlocfilehash: 0a206b7bbc808c1190044c1dfd6ffd47b9d454fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-exceptions"></a>Service Bus-berichtuitzonderingen
In dit artikel worden enkele uitzonderingen die worden gegenereerd door Microsoft Azure Service Bus Hallo messaging-API's. Deze verwijzing is onderwerp toochange, Controleer dus regelmatig op updates.

## <a name="exception-categories"></a>Uitzondering categorieën
Hallo berichtenservice-API's genereren uitzonderingen die in de volgende categorieën Hallo kunnen vallen, samen met de actie die is gekoppeld Hallo u tootry toofix kunt nemen ze. Houd er rekening mee dat Hallo betekenis en oorzaken van een uitzondering, afhankelijk van Hallo type Berichtentiteit (wachtrijen/onderwerpen of Event Hubs variëren kunnen):

1. Gebruiker fout codering ([System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [ System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx)). Algemene actie: probeer toofix Hallo code voordat u doorgaat.
2. Setup/configuratiefout ([Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception), [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). Algemene actie: Controleer de configuratie en wijzig indien nodig.
3. Tijdelijke uitzonderingen ([Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [ Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception)). Algemene actie: Hallo-bewerking opnieuw proberen of gebruikers een melding ontvangen.
4. Andere uitzonderingen ([System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception)). Algemene actie: uitzonderingstype voor specifieke toohello; Raadpleeg toohello tabel in de volgende sectie Hallo. 

## <a name="exception-types"></a>Uitzondering typen
Hallo volgende tabel bevat messaging uitzondering typen, en hun oorzaken en opmerkingen bij de voorgestelde actie die u kunt nemen.

| **Uitzonderingstype** | **Oorzaak-beschrijving/voorbeelden** | **Voorgestelde actie** | **Houd er rekening mee op automatische/direct opnieuw proberen** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Hallo server heeft niet gereageerd toohello aangevraagd bewerking binnen Hallo opgegeven tijd die wordt beheerd door [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout). Hallo-server mogelijk nog voltooid Hallo bewerking aangevraagd. Dit kan gebeuren vanwege toonetwork of andere vertragingen infrastructuur. |Controleer de systeemstatus Hallo voor consistentie en probeer indien nodig. Zie [time-out-uitzonderingen](#timeoutexception). |Probeer het opnieuw kan helpen in sommige gevallen; Probeer het opnieuw logica toocode toevoegen. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Hallo aangevraagd bewerking van de gebruiker is niet toegestaan binnen het Hallo-server of -service. Zie Hallo-bericht van uitzondering voor meer informatie. Bijvoorbeeld: [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) deze uitzondering wordt gegenereerd als het Hallo-bericht is ontvangen [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) modus. |Controleer Hallo code en Hallo-documentatie. Zorg ervoor dat Hallo aangevraagde bewerking is ongeldig. |Probeer het opnieuw helpt niet. |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Een poging is gedaan tooinvoke een bewerking op een object dat al is gesloten, afgebroken of verwijderd. In zeldzame gevallen, is Hallo ambient transactie al verwijderd. |Controleer Hallo code en zorg ervoor dat deze bewerkingen worden uitgevoerd op een verwijderd object niet gestart. |Probeer het opnieuw helpt niet. |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Hallo [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) object kan niet een token verkrijgen of Hallo token bevat geen Hallo claims vereist tooperform Hallo bewerking Hallo-token is ongeldig. |Zorg ervoor dat de tokenprovider Hallo wordt gemaakt met de juiste waarden Hallo. Controleer de configuratie van Hallo Hallo Access Control-service. |Probeer het opnieuw kan helpen in sommige gevallen; Probeer het opnieuw logica toocode toevoegen. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Een of meer argumenten opgegeven toohello methode zijn ongeldig.<br /> Hallo URI opgegeven te[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) of [maken](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) pad segment(en) bevat.<br /> Hallo-URI-schema te opgegeven[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) of [maken](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) is ongeldig. <br />Hallo-eigenschapswaarde is groter dan 32KB. |Controleer de aanroepende code Hallo en zorg ervoor dat Hallo argumenten juist zijn. |Probeer het opnieuw helpt niet. |
| [MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) |Entiteit gekoppeld Hallo-bewerking is niet aanwezig of is verwijderd. |Zorg ervoor dat Hallo entiteit bestaat. |Probeer het opnieuw helpt niet. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |Poging tooreceive een bericht met een bepaalde volgnummer. Dit bericht is niet gevonden. |Zorg ervoor dat het Hallo-bericht niet al is ontvangen. Controleer Hallo onbestelbare wachtrij toosee als het Hallo-bericht deadlettered is. |Probeer het opnieuw helpt niet. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |Client is geen kunnen tooestablish een verbinding tooService Bus. |Zorg ervoor dat de opgegeven Hallo-hostnaam juist is en Hallo host kan worden bereikt. |Probeer het opnieuw kan u helpen als er onregelmatige verbindingsproblemen. |
| [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |Service is niet kunnen tooprocess Hallo aanvraag op dit moment. |Client kan wachten op een bepaalde tijd en probeer opnieuw Hallo. |Client kan opnieuw na een bepaalde interval. Als een nieuwe poging in een andere uitzondering resulteert, controleert u gedrag van deze uitzondering voor het opnieuw. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Vergrendelingstoken die is gekoppeld aan het Hallo-bericht is verlopen of Hallo Vergrendelingstoken is niet gevonden. |Verwijderen van het Hallo-bericht. |Probeer het opnieuw helpt niet. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |Vergrendeling die zijn gekoppeld aan deze sessie wordt verbroken. |Hallo afbreken [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) object. |Probeer het opnieuw helpt niet. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |Een algemene uitzondering die kan worden gegenereerd in de volgende gevallen Hallo messaging:<br /> Er wordt geprobeerd toocreate een [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) met een naam of het pad dat verschillende entiteitstype tooa (bijvoorbeeld een onderwerp) behoort.<br />  Een poging is gedaan toosend een bericht groter is dan 256KB. Hallo-server of -service is een fout opgetreden tijdens het verwerken van Hallo-aanvraag. Zie Hallo-bericht van uitzondering voor meer informatie. Dit is meestal een tijdelijke uitzondering. |Hallo code controleren en ervoor te zorgen dat alleen serialiseerbaar objecten worden gebruikt voor de berichttekst hello (of gebruik een aangepaste serialisatiefunctie). Raadpleeg de documentatie Hallo voor waardetypen Hallo ondersteund van Hallo eigenschappen en alleen de gebruikstypen die worden ondersteund. Controleer de Hallo [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) eigenschap. Als het **true**, kunt u Hallo-bewerking opnieuw. |Gedrag voor opnieuw proberen is niet gedefinieerd en niet kan helpen. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |Poging toocreate een entiteit met een naam die al door een andere entiteit in de naamruimte van die service gebruikt wordt. |Hallo bestaande entiteit verwijderen of kies een andere naam voor Hallo entiteit toobe gemaakt. |Probeer het opnieuw helpt niet. |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |Hallo entiteit messaging de maximaal toegestane grootte heeft bereikt of Hallo kunt u het maximum aantal verbindingen tooa naamruimte is overschreden. |Maak schijfruimte vrij in Hallo entiteit door berichten ontvangt van Hallo entiteit of de onderliggende wachtrijen. Zie [QuotaExceededException](#quotaexceededexception). |Probeer het opnieuw kan u helpen als berichten zijn verwijderd in Hallo tussentijd. |
| [RuleActionException](/dotnet/api/microsoft.servicebus.messaging.ruleactionexception) |Service Bus retourneert deze uitzondering als u een ongeldige regelactie toocreate probeert. Service Bus wordt dit bericht van uitzondering tooa deadlettered toegevoegd als een fout optreedt tijdens het verwerken van Hallo regelactie voor het desbetreffende bericht. |Controleer de regelactie Hallo op juistheid. |Probeer het opnieuw helpt niet. |
| [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) |Service Bus retourneert deze uitzondering als u een ongeldig filter toocreate probeert. Service Bus wordt dit bericht van uitzondering tooa deadlettered toegevoegd als een fout opgetreden tijdens het verwerken van Hallo filter voor het desbetreffende bericht. |Controleer Hallo-filter op juistheid. |Probeer het opnieuw helpt niet. |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |Poging een sessie met een bepaalde sessie-ID, maar het Hallo-sessie is momenteel vergrendeld door een andere client tooaccept. |Zorg ervoor dat het Hallo-sessie wordt ontgrendeld door andere clients. |Probeer het opnieuw kan u helpen als Hallo-sessie in Hallo tussentijdse is vrijgegeven. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |Te veel bewerkingen maken deel uit van Hallo transactie. |Verminder het aantal bewerkingen die deel uitmaken van deze transactie Hallo. |Probeer het opnieuw helpt niet. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |Aanvraag voor een Runtimebewerking op een uitgeschakelde entiteit. |Hallo entiteit activeren. |Probeer het opnieuw kan u helpen als Hallo entiteit in Hallo tussentijdse is geactiveerd. |
| [NoMatchingSubscriptionException](/dotnet/api/microsoft.servicebus.messaging.nomatchingsubscriptionexception) |Service Bus retourneert deze uitzondering als u een bericht tooa onderwerp dat is vooraf filtering ingeschakeld en geen van de filters Hallo overeenkomt met verzendt. |Zorg ervoor dat minstens één filter overeenkomt met. |Probeer het opnieuw helpt niet. |
| [MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |Een bericht nettolading overschrijdt Hallo 256 KB. Houd er rekening mee dat Hallo 256 KB limiet Hallo totale grootte, waaronder Systeemeigenschappen en een .NET-overhead. |Hallo verkleinen van nettolading voor Hallo-bericht en probeer Hallo opnieuw. |Probeer het opnieuw helpt niet. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |Hallo ambient transactie (*Transaction.Current*) is ongeldig. Mogelijk is het voltooid of afgebroken. De binnenste uitzondering biedt mogelijk meer informatie. | |Probeer het opnieuw helpt niet. |
| [TransactionInDoubtException](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |Een bewerking wordt uitgevoerd voor een transactie is onzeker, of een poging is gedaan toocommit Hallo transactie en Hallo transactie is onzeker. |Uw toepassing moet deze uitzondering (als een speciaal geval), verwerken, zoals Hallo transactie al doorgevoerd is mogelijk. |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) geeft aan dat een quotum voor een specifieke entiteit is overschreden.

### <a name="queues-and-topics"></a>Wachtrijen en onderwerpen
Voor wachtrijen en onderwerpen is dit vaak Hallo grootte van Hallo wachtrij. Fout bij het Hallo-berichteigenschap bevat meer informatie, zoals in het volgende voorbeeld Hallo:

```
Microsoft.ServiceBus.Messaging.QuotaExceededException
Message: hello maximum entity size has been reached or exceeded for Topic: ‘xxx-xxx-xxx’. 
    Size of entity in bytes:1073742326, Max entity size in bytes:
1073741824..TrackingId:xxxxxxxxxxxxxxxxxxxxxxxxxx, TimeStamp:3/15/2013 7:50:18 AM
```

Hallo-bericht geeft aan dat onderwerp Hallo overschrijdt de maximale grootte in deze case 1 GB (Hallo standaard maximale grootte). 

### <a name="namespaces"></a>Naamruimten

Voor naamruimten, [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) kan erop wijzen dat een toepassing hello kunt u het maximum aantal verbindingen tooa naamruimte heeft overschreden. Bijvoorbeeld:

```
Microsoft.ServiceBus.Messaging.QuotaExceededException: ConnectionsQuotaExceeded for namespace xxx.
<tracking-id-guid>_G12 ---> 
System.ServiceModel.FaultException`1[System.ServiceModel.ExceptionDetail]: 
ConnectionsQuotaExceeded for namespace xxx.
```

#### <a name="common-causes"></a>Algemene oorzaken
Er zijn twee algemene oorzaken voor deze fout: Hallo wachtrij voor onbestelbare berichten en niet-functionerende bericht ontvangers.

1. **Wachtrij voor onbestelbare berichten** een lezer mislukt toocomplete berichten en het Hallo-berichten toohello wachtrij/onderwerp worden geretourneerd wanneer Hallo vergrendeling is verlopen. Dit kan gebeuren als er een uitzondering die voorkomt dat het aanroepen van optreedt bij Hallo lezer [BrokeredMessage.Complete](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.brokeredmessage.complete.aspx). Nadat een bericht 10 keer gelezen is, gaat de wachtrij voor onbestelbare berichten toohello standaard. Dit gedrag wordt beheerd door Hallo [QueueDescription.MaxDeliveryCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.maxdeliverycount.aspx) eigenschap en heeft een standaardwaarde van 10. Als berichten in wachtrij voor onbestelbare berichten Hallo worden opstapelen, innemen deze ruimte.
   
    tooresolve hello probleem, lezen en volledig Hallo-berichten van Hallo-wachtrij voor onbestelbare berichten, zoals u zou uit een andere wachtrij. Hallo [QueueClient](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.aspx) klasse bevat ook een [FormatDeadLetterPath](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.formatdeadletterpath.aspx) methode toohelp indeling Hallo wachtrij voor onbestelbare berichten pad.
2. **Ontvanger gestopt** een ontvanger ontvangen van berichten van een wachtrij of het abonnement is gestopt. Hallo manier tooidentify dit toolook op Hallo is [QueueDescription.MessageCountDetails](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.messagecountdetails.aspx) eigenschap die u de volledige uitsplitsing Hallo van Hallo-berichten kunt. Als hello [ActiveMessageCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagecountdetails.activemessagecount.aspx) eigenschap hoge of groeiende, wordt de Hallo-berichten niet snel bent wordt geschreven wordt gelezen.

### <a name="event-hubs"></a>Event Hubs
Event Hubs is een limiet van 20 consumergroepen per Event Hub. Wanneer u meer toocreate probeert, krijgt u een [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception). 

## <a name="timeoutexception"></a>TimeoutException
Een [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) geeft aan dat een gebruiker gestart bewerking langer dan de time-out voor Hallo-bewerking duurt. 

Controleer Hallo-waarde van Hallo [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) eigenschap, kunt u deze limiet door kan ook leiden tot een [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx).

### <a name="queues-and-topics"></a>Wachtrijen en onderwerpen
Wachtrijen en onderwerpen, Hallo time-out is opgegeven in Hallo [MessagingFactorySettings.OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout) eigenschap als onderdeel van de verbindingsreeks Hallo of via [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). Hallo foutbericht zelf kan variëren, maar bevat altijd Hallo time-outwaarde voor de huidige bewerking Hallo opgegeven. 

### <a name="event-hubs"></a>Event Hubs
Event Hubs Hallo time-out is opgegeven als onderdeel van de verbindingsreeks Hallo of via [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). Hallo foutbericht zelf kan variëren, maar bevat altijd Hallo time-outwaarde voor de huidige bewerking Hallo opgegeven. 

### <a name="common-causes"></a>Algemene oorzaken
Er zijn twee algemene oorzaken voor deze fout: onjuiste configuratie of een tijdelijke servicefout.

1. **Onjuiste configuratie** time-out voor Hallo-bewerking is mogelijk te klein voor Hallo operationele voorwaarde. de standaardwaarde Hallo voor time-out van de bewerking Hallo in Hallo client SDK is 60 seconden. Controleer toosee als uw code Hallo-waarde heeft ingesteld toosomething te klein. Houd er rekening mee die voorwaarde Hallo van Hallo netwerk en CPU-gebruik Hallo-tijd die nodig is voor een bepaalde bewerking toocomplete, zodat de time-out voor Hallo-bewerking mag niet worden ingesteld tooa zeer kleine waarde kan beïnvloeden.
2. **Tijdelijke servicefout** soms Hallo Service Bus-service kan vertragingen bij het verwerken van aanvragen, bijvoorbeeld tijdens perioden met intensief verkeer. In dergelijke gevallen kunt u de bewerking na een vertraging opnieuw proberen totdat het Hallo-bewerking is voltooid. Als hello dezelfde bewerking steeds na meerdere pogingen mislukt, gaat u naar Hallo [Azure service status site](https://azure.microsoft.com/status/) toosee als er bekende serviceonderbrekingen.

## <a name="next-steps"></a>Volgende stappen

Zie voor volledige Service Bus-.NET API-verwijzing hello, Hallo [Azure .NET API-verwijzingen](/dotnet/api/overview/azure/servicebus).

meer informatie over toolearn [Service Bus](https://azure.microsoft.com/services/service-bus/), Zie de volgende onderwerpen Hallo.

* [Overzicht van Service Bus-berichten](service-bus-messaging-overview.md)
* [Grondbeginselen van Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Service Bus-architectuur](service-bus-architecture.md)

