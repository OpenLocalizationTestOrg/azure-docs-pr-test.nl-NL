---
title: aaaHow toouse Service Bus-wachtrijen in Node.js | Microsoft Docs
description: Meer informatie over hoe toouse Service Bus wachtrijen in Azure vanuit een Node.js-app.
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a87a00f9-9aba-4c49-a0df-f900a8b67b3f
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: c55354b2061c41aba1093cc3f12ce2a1bc37a3cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-nodejs"></a>Hoe toouse Service Bus wachtrijen met behulp van Node.js

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Dit artikel wordt beschreven hoe toouse Service Bus wachtrijen met behulp van Node.js. Hallo-voorbeelden zijn geschreven in JavaScript en hello Node.js Azure-module gebruiken. Hallo scenario's worden behandeld: **maken van wachtrijen**, **verzenden en ontvangen berichten**, en **verwijderen van wachtrijen**. Zie voor meer informatie over wachtrijen Hallo [Vervolgstappen](#next-steps) sectie.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a>Een Node.js-toepassing maken
Maak een lege Node.js-toepassing. Voor instructies over het toocreate een Node.js-toepassing Zie [maken en implementeren van een Node.js-toepassing tooan Azure-Website][Create and deploy a Node.js application tooan Azure Website], of [Node.js-Cloudservice] [ Node.js Cloud Service] met Windows PowerShell.

## <a name="configure-your-application-toouse-service-bus"></a>Configureren van uw toepassing toouse Service Bus
Azure Service Bus toouse downloaden en gebruiken van Hallo Node.js Azure-pakket. Dit pakket bevat een set van bibliotheken die met Hallo Service Bus REST-services communiceren.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Knooppunt Package Manager (NPM) tooobtain Hallo pakket gebruiken
1. Gebruik Hallo **Windows PowerShell voor Node.js** opdracht venster toonavigate toohello **c:\\knooppunt\\sbqueues\\WebRole1** map waarin u hebt gemaakt uw Voorbeeld van een toepassing.
2. Type **npm installeren azure** in opdrachtvenster hello, moet die leiden tot uitvoer vergelijkbare toohello volgende:

    ```
    azure@0.7.5 node_modules\azure
        ├── dateformat@1.0.2-1.2.3
        ├── xmlbuilder@0.4.2
        ├── node-uuid@1.2.0
        ├── mime@1.2.9
        ├── underscore@1.4.4
        ├── validator@1.1.1
        ├── tunnel@0.0.2
        ├── wns@0.5.3
        ├── xml2js@0.2.7 (sax@0.5.2)
        └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
    ```
3. U kunt handmatig uitvoeren Hallo **ls** tooverify opdracht die een **node_modules** map is gemaakt. Binnen die map zoeken Hallo **azure** , dit pakket bevat, moet u Service Bus-wachtrijen tooaccess Hallo-bibliotheken.

### <a name="import-hello-module"></a>Hallo-module importeren
Hallo toohello bovenaan hello te volgen in Kladblok of een andere teksteditor toevoegen **server.js** bestand van de toepassing hello:

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a>Een Azure Service Bus-verbinding instellen
Hello Azure module leest de omgevingsvariabele Hallo `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain informatie tooconnect tooService Bus vereist. Als deze omgevingsvariabele niet is ingesteld, moet u de accountgegevens Hallo opgeven bij het aanroepen van `createServiceBusService`.

Zie voor een voorbeeld van het Hallo omgevingsvariabelen instellen in een configuratiebestand voor een Azure Cloud Service [Node.js-Cloudservice met Storage][Node.js Cloud Service with Storage].

Voor een voorbeeld van het Hallo-omgevingsvariabelen instellen in Hallo [Azure-portal] [ Azure portal] Zie voor een Azure-Website [Node.js-webtoepassing met Storage] [ Node.js Web Application with Storage].

## <a name="create-a-queue"></a>Een wachtrij maken
Hallo **ServiceBusService** object kunt u toowork met Service Bus-wachtrijen. Hallo volgende code maakt een **ServiceBusService** object. Voeg deze toe aan de bovenkant Hallo Hallo **server.js** bestand na Hallo instructie tooimport hello Azure-module:

```javascript
var serviceBusService = azure.createServiceBusService();
```

Door het aanroepen van `createQueueIfNotExists` op Hallo **ServiceBusService** object, Hallo opgegeven wachtrij is geretourneerd (indien aanwezig) of een nieuwe wachtrij met de opgegeven naam hello wordt gemaakt. Hallo volgende code gebruikt `createQueueIfNotExists` toocreate of verbinding maken met de naam toohello-wachtrij `myqueue`:

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

Hallo `createServiceBusService` methode biedt ook ondersteuning voor extra opties waarmee u toooverride standaard wachtrij-instellingen zoals bericht tijd toolive of Maximale wachtrijgrootte. Hallo volgende voorbeeld wordt Hallo wachtrij maximale grootte too5 GB en een tijd toolive (TTL)-waarde van 1 minuut:

```javascript
var queueOptions = {
      MaxSizeInMegabytes: '5120',
      DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createQueueIfNotExists('myqueue', queueOptions, function(error){
    if(!error){
        // Queue exists
    }
});
```

### <a name="filters"></a>Filters
Optionele filteren bewerkingen kunnen worden toegepast toooperations uitgevoerd met behulp van **ServiceBusService**. Bewerkingen voor het filteren kunt opnemen logboekregistratie, automatisch opnieuw, enzovoort. Filters zijn objecten die een methode met Hallo handtekening te implementeren:

```javascript
function handle (requestOptions, next)
```

Hierna moet u de vooraf verwerken op Hallo aanvraag opties, Hallo-methode moet aanroepen `next`, een retouraanroep wordt doorgegeven met Hallo handtekening te volgen:

```javascript
function (returnObject, finalCallback, next)
```

In deze retouraanroep en na verwerking Hallo `returnObject` (hello reactie van Hallo aanvraag toohello server), Hallo callback moet ofwel aanroepen `next` als deze bestaat toocontinue verwerking van andere filters of gewoon aanroepen `finalCallback`, welke ends Hallo service aanroepen.

Twee filters die Pogingslogica implementeren zijn opgenomen in hello Azure SDK voor Node.js, `ExponentialRetryPolicyFilter` en `LinearRetryPolicyFilter`. Hallo volgende code maakt een `ServiceBusService` object dat gebruikmaakt van Hallo `ExponentialRetryPolicyFilter`:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a>Berichten tooa wachtrij verzenden
een bericht tooa Service Bus-wachtrij toosend, roept uw toepassing hello `sendQueueMessage` methode op Hallo **ServiceBusService** object. Berichten verzonden te (en ontvangen van) Service Bus-wachtrijen zijn **BrokeredMessage** objecten en hebben een aantal standaardeigenschappen (zoals **Label** en **TimeToLive**), een de woordenlijst die wordt gebruikt toohold aangepaste toepassingsspecifieke eigenschappen en een hoofdtekst met willekeurige toepassingsgegevens. Een toepassing kunt Hallo hoofdtekst van het Hallo-bericht instellen door een reeks wordt doorgegeven als het Hallo-bericht. Alle vereiste eigenschappen standaard worden ingevuld met standaardwaarden.

Hallo volgende voorbeeld laat zien hoe toosend een test toohello berichtenwachtrij genoemd `myqueue` met `sendQueueMessage`:

```javascript
var message = {
    body: 'Test message',
    customProperties: {
        testproperty: 'TestValue'
    }};
serviceBusService.sendQueueMessage('myqueue', message, function(error){
    if(!error){
        // message sent
    }
});
```

Service Bus-wachtrijen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md). Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben. Er is geen limiet voor het aantal berichten in een wachtrij hello, maar er is een limiet voor de totale grootte van berichten in een wachtrij Hallo Hallo. De grootte van de wachtrij wordt gedefinieerd tijdens het aanmaken, met een bovengrens van 5 GB. Zie voor meer informatie over quota [Service Bus-quota][Service Bus quotas].

## <a name="receive-messages-from-a-queue"></a>Berichten ontvangen uit een wachtrij
Berichten worden ontvangen van een wachtrij met Hallo `receiveQueueMessage` methode op Hallo **ServiceBusService** object. Standaard worden berichten uit Hallo wachtrij verwijderd als ze worden gelezen; echter (peek) lezen en vergrendelen Hallo-bericht zonder het te verwijderen uit de wachtrij Hallo door de optionele parameter Hallo instelling `isPeekLock` te**true**.

Hallo standaardgedrag van lezen en Hallo-bericht is verwijderd als onderdeel van Hallo ontvangstbewerking is Hallo eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een fout. toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt. Omdat Service Bus heeft gemarkeerd als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.

Als hello `isPeekLock` parameter is ingesteld, te**true**, Hallo ontvangen, wordt een bewerking met twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren. Wanneer Service Bus een aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing. Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces ontvangen door het aanroepen van `deleteMessage` methode en het Hallo-bericht toobe verwijderd als een parameter geven. Hallo `deleteMessage` methode markeert het Hallo-bericht als verbruikt en wordt deze verwijderd uit de wachtrij Hallo.

Hallo volgende voorbeeld laat zien hoe tooreceive en proces berichten met behulp van `receiveQueueMessage`. Hallo voorbeeld eerst ontvangt een bericht wordt verwijderd en vervolgens ontvangt een bericht met `isPeekLock` instellen te**true**, en vervolgens verwijdert Hallo bericht met `deleteMessage`:

```javascript
serviceBusService.receiveQueueMessage('myqueue', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
    }
});
serviceBusService.receiveQueueMessage('myqueue', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
            }
        });
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Hoe toohandle toepassing is vastgelopen en onleesbare berichten
Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht. Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo `unlockMessage` methode op Hallo **ServiceBusService** object. Dit wordt veroorzaakt toounlock Service Bus het bericht in de wachtrij Hallo en beschikbare toobe opnieuw ontvangen, ofwel Hallo door dezelfde toepassing of door een andere consumerende toepassing verbruikt.

Daarnaast is er een time-out gekoppeld aan een bericht in de wachtrij Hallo is vergrendeld en als Hallo toepassing mislukt tooprocess Hallo-bericht voordat Hallo time-out van de vergrendeling verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus wordt het Hallo-bericht automatisch ontgrendelen en het beschikbaar toobe ontvangen opnieuw maken.

In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo `deleteMessage` methode wordt aangeroepen, is het Hallo-bericht altijd opnieuw bezorgd toohello toepassing opnieuw wordt gestart. Dit wordt vaak genoemd *tenminste eenmaal verwerken*, dat wil zeggen elk bericht ten minste één keer wordt verwerkt maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd. Als Hallo scenario kan geen dubbele verwerking tolereren, moeten toepassingsontwikkelaars levering van aanvullende logica tootheir toepassing toohandle dubbele berichten toevoegen. Dit wordt vaak bereikt met behulp van Hallo **MessageId** eigenschap van Hallo-bericht dat gelijk bij meerdere bezorgingspogingen blijft.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over wachtrijen, Zie Hallo resources te volgen.

* [Wachtrijen, onderwerpen en abonnementen][Queues, topics, and subscriptions]
* [Azure SDK voor knooppunt] [ Azure SDK for Node] opslagplaats op GitHub
* [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
