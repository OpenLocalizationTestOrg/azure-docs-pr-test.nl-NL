---
title: aaaAzure Relay uitzonderingen en hoe tooresolve ze | Microsoft Docs
description: Een lijst met uitzonderingen van Azure Relay en aanbevolen maatregelen kunt toohelp deze kunt oplossen.
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5f9dd02c-cce0-43b3-8eb8-744f0c27f38c
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: de417c8e9e43407ef355fd44f6170cf2cdc46d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-exceptions"></a>Azure Relay-uitzonderingen

Dit artikel worden enkele uitzonderingen die door hello Azure Relay-API's kunnen worden gegenereerd. Deze verwijzing is onderwerp toochange, Controleer dus regelmatig op updates.

## <a name="exception-categories"></a>Uitzondering categorieën

Hallo Relay-API's genereren uitzonderingen die in de volgende categorieën Hallo mogelijk vallen. Ook vermeld zijn voorgestelde acties die u toohelp los Hallo uitzonderingen overwegen kunt.

*   **Gebruiker coderen fout**: [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [ System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). 

    **Algemene actie**: probeer toofix Hallo code voordat u doorgaat.
*   **Setup/configuratiefout**: [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). 

    **Algemene actie**: Controleer uw configuratie. Wijzig indien nodig, Hallo-configuratie.
*   **Tijdelijke uitzonderingen**: [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [ Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). 

    **Algemene actie**: Hallo-bewerking opnieuw proberen of gebruikers een melding ontvangen.
*   **Andere uitzonderingen**: [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx). 

    **Algemene actie**: specifieke toohello uitzonderingstype. Zie tabel in de volgende sectie Hallo Hallo. 

## <a name="exception-types"></a>Uitzondering typen

Hallo volgende tabel bevat messaging uitzondering typen en hun oorzaken. Ook ziet u voorgestelde maatregelen kunt toohelp los Hallo uitzonderingen.

| **Uitzonderingstype** | **Beschrijving** | **Voorgestelde actie** | **Houd er rekening mee op automatische of direct opnieuw proberen** |
| --- | --- | --- | --- |
| [Time-out](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Hallo server heeft niet gereageerd toohello aangevraagd bewerking binnen Hallo opgegeven tijd, die wordt beheerd door [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout). Hallo server mogelijk voltooide Hallo gevraagde bewerking. Dit kan gebeuren vanwege toonetwork of andere vertragingen infrastructuur. |Hallo systeemstatus voor consistentie te controleren, en probeer vervolgens, indien nodig. Zie [TimeoutException](#timeoutexception). |Probeer het opnieuw kan helpen in sommige gevallen; Probeer het opnieuw logica toocode toevoegen. |
| [Ongeldige bewerking](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Hallo aangevraagd bewerking van de gebruiker is niet toegestaan binnen het Hallo-server of -service. Zie Hallo-bericht van uitzondering voor meer informatie. |Controleer Hallo code en Hallo-documentatie. Zorg ervoor dat Hallo aangevraagde bewerking is ongeldig. |Probeer het opnieuw helpt niet. |
| [Bewerking is geannuleerd](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Een poging is gedaan tooinvoke een bewerking op een object dat al is gesloten, is afgebroken, of verwijderd. In zeldzame gevallen, is Hallo ambient transactie al verwijderd. |Controleer Hallo code en zorg ervoor dat deze bewerkingen worden uitgevoerd op een verwijderd object niet gestart. |Probeer het opnieuw helpt niet. |
| [Onbevoegde toegang](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Hallo [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) object kan niet een token verkrijgen of Hallo token bevat geen Hallo claims vereist tooperform Hallo bewerking Hallo-token is ongeldig. |Zorg ervoor dat tokenprovider Hallo is gemaakt met de juiste waarden Hallo. Controleer de configuratie van Hallo Hallo Access Control-service. |Probeer het opnieuw kan helpen in sommige gevallen; Probeer het opnieuw logica toocode toevoegen. |
| [Argumentuitzondering](https://msdn.microsoft.com/library/system.argumentexception.aspx),<br /> [Argument Null](https://msdn.microsoft.com/library/system.argumentnullexception.aspx),<br />[Argument buiten het bereik](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Een of meer van de volgende Hallo opgetreden:<br />Een of meer argumenten opgegeven toohello methode zijn ongeldig.<br /> Hallo URI opgegeven te[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) of [maken](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) bevat een of meer padsegmenten.<br />Hallo-URI-schema te opgegeven[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) of [maken](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) is ongeldig. <br />Hallo-eigenschapswaarde is groter dan 32 KB. |Controleer de aanroepende code Hallo en zorg ervoor dat Hallo argumenten juist zijn. |Probeer het opnieuw helpt niet. |
| [Server is bezet](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |Service is niet kunnen tooprocess Hallo aanvraag op dit moment. |Hallo-client kan wachten op een bepaalde tijd en probeer opnieuw Hallo. |Hallo-client mogelijk opnieuw na een bepaalde interval. Als een nieuwe poging resultaten in een andere uitzondering, controleert u Hallo opnieuw gedrag van deze uitzondering. |
| [Quota overschreden](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |Hallo messaging entiteit heeft de maximaal toegestane grootte bereikt. |Maak schijfruimte vrij in Hallo entiteit door berichten ontvangt van Hallo entiteit of de subwachtrijen. Zie [QuotaExceededException](#quotaexceededexception). |Probeer het opnieuw kan u helpen als berichten zijn verwijderd in Hallo tussentijd. |
| [Grootte van het bericht is overschreden](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |Een bericht nettolading overschrijdt Hallo 256 KB. Houd er rekening mee dat Hallo 256 KB limiet Hallo totale grootte. Hallo totale berichtgrootte kunt opnemen Systeemeigenschappen en eventuele Microsoft .NET-overhead. |Hallo verkleinen van nettolading voor Hallo-bericht en probeer Hallo opnieuw. |Probeer het opnieuw helpt niet. |

## <a name="quotaexceededexception"></a>QuotaExceededException

[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) geeft aan dat een quotum voor een specifieke entiteit is overschreden.

Voor Relay, verpakt deze uitzondering Hallo [System.ServiceModel.QuotaExceededException](https://msdn.microsoft.com/library/system.servicemodel.quotaexceededexception.aspx), wat aangeeft dat Hallo maximum aantal listeners voor dit eindpunt is overschreden. Hiermee wordt aangegeven in Hallo **MaximumListenersPerEndpoint** waarde van het Hallo-bericht van uitzondering.

## <a name="timeoutexception"></a>TimeoutException
Een [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) geeft aan dat een gebruiker gestart bewerking langer dan de time-out voor Hallo-bewerking duurt. 

Controleer de waarde van de Hallo Hallo [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) eigenschap. Kunt u deze limiet door kan leiden tot een [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx).

Voor Relay ontvangt u mogelijk time-out-uitzonderingen als u een relay afzender-verbinding voor het eerst opent. Er zijn twee algemene oorzaken voor deze uitzondering:

*   Hallo [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) waarde mogelijk te klein (of zelfs door een fractie van een seconde).
* Een lokale relay-listener mogelijk niet meer reageert (of deze problemen van de firewall-regels die listeners verbieden accepteert nieuwe clientverbindingen kan optreden), en Hallo [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) waarde is minder dan 20 seconden.

Voorbeeld:

```
'System.TimeoutException’: hello operation did not complete within hello allotted timeout of 00:00:10.
hello time allotted toothis operation may have been a portion of a longer timeout.
```

### <a name="common-causes"></a>Algemene oorzaken
Er zijn twee algemene oorzaken voor deze fout:

*   **Onjuiste configuratie**
    
    time-out voor Hallo-bewerking is mogelijk te klein voor Hallo operationele voorwaarde. de standaardwaarde Hallo voor time-out van de bewerking Hallo in Hallo client SDK is 60 seconden. Controleer toosee of Hallo waarde in uw code wordt ingesteld toosomething te klein. Houd er rekening mee dat CPU-gebruik en Hallo voorwaarde van Hallo netwerk Hallo tijd die nodig is voor een bewerking toocomplete kan beïnvloeden. Het is een goed idee niet tooset Hallo bewerking tooa zeer kleine-outwaarde.
*   **Tijdelijke servicefout**

    In sommige gevallen kan kan Hallo Relay-service vertragingen bij het verwerken van aanvragen. Dit kan bijvoorbeeld gebeuren tijdens perioden met intensief verkeer. Als dit het geval is, probeer het opnieuw nadat een vertraging totdat het Hallo-bewerking is voltooid. Als hello dezelfde bewerking toofail na meerdere pogingen blijft, controleert u Hallo [Azure service status site](https://azure.microsoft.com/status/) toosee als er zijn bekende serviceonderbrekingen.

## <a name="next-steps"></a>Volgende stappen
* [Veelgestelde vragen over Azure Relay](relay-faq.md)
* [Een relay-naamruimte maken](relay-create-namespace-portal.md)
* [Aan de slag met Azure Relay en .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Aan de slag met Azure Relay en knooppunt](relay-hybrid-connections-node-get-started.md)

