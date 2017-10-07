---
title: aaaHow toouse Azure Service Bus-onderwerpen en abonnementen met behulp van Node.js | Microsoft Docs
description: Meer informatie over hoe toouse Service Bus-onderwerpen en abonnementen in Azure van een Node.js-app.
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b9f5db85-7b6c-4cc7-bd2c-bd3087c99875
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: e8f6e7ad6ed16d844c408337ac9e50f990e3fafd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a>Hoe tooUse Service Bus-onderwerpen en abonnementen met behulp van Node.js

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Deze handleiding wordt beschreven hoe toouse Service Bus-onderwerpen en abonnementen van Node.js-toepassingen. Hallo scenario's worden behandeld: **maken van onderwerpen en abonnementen**, **maken van abonnementsfilters**, **verzenden van berichten** tooa onderwerp **ontvangen berichten van een abonnement**, en **verwijderen van onderwerpen en abonnementen**. Zie voor meer informatie over onderwerpen en abonnementen Hallo [Vervolgstappen](#next-steps) sectie.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a>Een Node.js-toepassing maken
Maak een lege Node.js-toepassing. Zie voor instructies over het maken van een Node.js-toepassing [maken en implementeren van een Node.js-toepassing tooan Azure-website], [Node.js-Cloudservice] [ Node.js Cloud Service] met behulp van Windows PowerShell of website met WebMatrix.

## <a name="configure-your-application-toouse-service-bus"></a>Configureren van uw toepassing toouse Service Bus
Service Bus toouse downloaden Hallo Node.js Azure-pakket. Dit pakket bevat een set van bibliotheken die met Hallo Service Bus REST-services communiceren.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Knooppunt Package Manager (NPM) tooobtain Hallo pakket gebruiken
1. Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac), of **Bash** (Unix), gaat u toohello map waar u uw voorbeeldtoepassing hebt gemaakt.
2. Type **npm installeren azure** in Hallo opdrachtvenster moet die leiden tot Hallo volgende uitvoer:

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
3. U kunt handmatig uitvoeren Hallo **ls** tooverify opdracht die een **knooppunt\_modules** map is gemaakt. In deze map te zoeken naar de **azure** , dit pakket bevat, moet u Service Bus-onderwerpen tooaccess Hallo-bibliotheken.

### <a name="import-hello-module"></a>Hallo-module importeren
Hallo toohello bovenaan hello te volgen in Kladblok of een andere teksteditor toevoegen **server.js** bestand van de toepassing hello:

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a>Een Service Bus-verbinding instellen
Hello Azure module leest Hallo omgevingsvariabelen `AZURE_SERVICEBUS_NAMESPACE` en `AZURE_SERVICEBUS_ACCESS_KEY` vereist tooconnect tooService Bus voor meer informatie. Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens Hallo opgeven bij het aanroepen van `createServiceBusService`.

Zie voor een voorbeeld van het Hallo-omgevingsvariabelen instellen voor een Azure Cloud Service [Node.js-Cloudservice met Storage][Node.js Cloud Service with Storage].

Zie voor een voorbeeld van het instellen van de omgevingsvariabelen Hallo voor een Azure-Website [Node.js-webtoepassing met Storage][Node.js Web Application with Storage].

## <a name="create-a-topic"></a>Een onderwerp maken
Hallo **ServiceBusService** object kunt u toowork met onderwerpen. De volgende code maakt een **ServiceBusService** object. Voeg deze toe aan de bovenkant van Hallo **server.js** bestand na Hallo instructie tooimport hello azure module:

```javascript
var serviceBusService = azure.createServiceBusService();
```

Door het aanroepen van `createTopicIfNotExists` op Hallo **ServiceBusService** object, Hallo opgegeven onderwerp worden geretourneerd (indien aanwezig) of een nieuw onderwerp met de opgegeven naam hello wordt gemaakt. Hallo volgende code gebruikt `createTopicIfNotExists` toocreate of verbinding maken met de naam toohello-onderwerp `MyTopic`:

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

Hallo `createServiceBusService` methode biedt ook ondersteuning voor extra opties waarmee u toooverride standaardinstellingen onderwerp zoals bericht of grootte van het maximum aantal onderwerp. Hallo volgende voorbeeld wordt Hallo onderwerp maximale grootte too5GB met een tijd toolive van 1 minuut:

```javascript
var topicOptions = {
        MaxSizeInMegabytes: '5120',
        DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createTopicIfNotExists('MyTopic', topicOptions, function(error){
    if(!error){
        // topic was created or exists
    }
});
```

### <a name="filters"></a>Filters
Optionele filteren bewerkingen kunnen worden toegepast toooperations uitgevoerd met behulp van **ServiceBusService**. Bewerkingen voor het filteren kunt opnemen logboekregistratie, automatisch opnieuw, enzovoort. Filters zijn objecten die een methode met Hallo handtekening te implementeren:

```javascript
function handle (requestOptions, next)
```

Na het uitvoeren van voorverwerking op Hallo certificaataanvraagopties Hallo methodeaanroepen `next`, een retouraanroep wordt doorgegeven met Hallo handtekening te volgen:

```javascript
function (returnObject, finalCallback, next)
```

In deze retouraanroep en na verwerking Hallo `returnObject` (hello reactie van Hallo aanvraag toohello server), Hallo callback tooeither moet vervolgens worden aangeroepen als het verwerken van andere filters toocontinue al bestaat of aan te roepen `finalCallback` anders tooend Hallo het aanroepen van de service.

Twee filters die Pogingslogica implementeren zijn opgenomen in hello Azure SDK voor Node.js, **ExponentialRetryPolicyFilter** en **LinearRetryPolicyFilter**. Hallo volgende maakt een **ServiceBusService** object dat gebruikmaakt van Hallo **ExponentialRetryPolicyFilter**:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a>Abonnementen maken
Onderwerpabonnementen worden ook gemaakt met de Hallo **ServiceBusService** object. Abonnementen kunnen worden genoemd en een optioneel filter waarmee Hallo verzameling berichten dat de virtuele wachtrij van het abonnement toohello wordt beperkt.

> [!NOTE]
> Abonnementen worden permanent en tooexist zal worden voortgezet totdat beide ze of hello onderwerp ze zijn gekoppeld, worden verwijderd. Als uw toepassing bevat de logica toocreate een abonnement, moet deze eerst controleren als Hallo abonnement bestaat al met behulp van de `getSubscription` methode.
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Een abonnement maken met de Hallo standaardfilter (MatchAll)
Hallo **MatchAll** filter is Hallo standaardfilter dat wordt gebruikt als geen filter is opgegeven als een nieuw abonnement wordt gemaakt. Wanneer Hallo **MatchAll** filter wordt gebruikt, worden alle berichten gepubliceerde toohello onderwerp in de virtuele wachtrij van het abonnement geplaatst. Hallo volgende voorbeeld maakt u een abonnement genaamd 'AllMessages' en gebruikt standaard Hallo **MatchAll** filter.

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a>Abonnementen met filters maken
U kunt ook filters waarmee u welke berichten verzonden tooa onderwerp weergegeven binnen een bepaald onderwerpabonnement tooscope maken.

Hallo meest flexibele type filter dat wordt ondersteund door abonnementen is de **SqlFilter**, waarmee een subset van SQL92 wordt geïmplementeerd implementeert. SQL-filters worden uitgevoerd op Hallo eigenschappen van Hallo-berichten die gepubliceerd toohello onderwerp zijn. Bekijk voor meer informatie over Hallo expressies die kunnen worden gebruikt met een SQL-filter Hallo [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] syntaxis.

Filters kunnen tooa abonnement worden toegevoegd met behulp van Hallo `createRule` methode Hallo **ServiceBusService** object. Deze methode kunt u nieuwe filters tooan bestaande abonnement toevoegen.

> [!NOTE]
> Omdat het standaardfilter hello wordt automatisch toegepast tooall nieuwe abonnementen, moet u eerst het standaardfilter Hallo verwijderen of de **MatchAll** overschrijft alle andere filters die u kunt opgeven. U kunt de standaardregel Hallo verwijderen via Hallo `deleteRule` methode van de **ServiceBusService** object.
>
>

Hallo volgende voorbeeld maakt u een abonnement met de naam `HighMessages` met een **SqlFilter** die alleen berichten selecteert die een aangepaste `messagenumber` eigenschap groter is dan 3:

```javascript
serviceBusService.createSubscription('MyTopic', 'HighMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'HighMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber > 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'HighMessages',
            'HighMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

Op deze manier hello volgende voorbeeld maakt u een abonnement met de naam `LowMessages` met een **SqlFilter** die alleen berichten selecteert die een `messagenumber` eigenschap kleiner dan of gelijk too3:

```javascript
serviceBusService.createSubscription('MyTopic', 'LowMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'LowMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber <= 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'LowMessages',
            'LowMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

Wanneer een bericht nu te verzonden`MyTopic`, worden altijd geleverd naar ontvangers die zijn geabonneerd toohello `AllMessages` onderwerpabonnement en selectief bezorgd tooreceivers geabonneerd toohello `HighMessages` en `LowMessages` onderwerpabonnementen (al naar gelang de inhoud van de Hallo-bericht).

## <a name="how-toosend-messages-tooa-topic"></a>Hoe toosend tooa onderwerp berichten
een bericht tooa Service Bus-onderwerp toosend, uw toepassing moet gebruiken de `sendTopicMessage` methode Hallo **ServiceBusService** object.
Berichten verzonden tooService Bus-onderwerpen zijn **BrokeredMessage** objecten.
**BrokeredMessage** objecten hebben een aantal standaardeigenschappen (zoals `Label` en `TimeToLive`), een woordenlijst die wordt gebruikt toohold aangepaste toepassingsspecifieke eigenschappen en een hoofdtekst met tekenreeksen. Een toepassing hello hoofdtekst van het Hallo-bericht worden ingesteld door een string-waarde wordt doorgegeven aan Hallo `sendTopicMessage` en alle vereiste standaardeigenschappen standaardwaarden worden ingevuld.

Hallo volgende voorbeeld laat zien hoe toosend vijf testberichten naar `MyTopic`. Houd er rekening mee dat Hallo `messagenumber` eigenschapswaarde van elk bericht varieert op Hallo herhaling van Hallo lus (dit wordt bepaald welke abonnementen ontvangen):

```javascript
var message = {
    body: '',
    customProperties: {
        messagenumber: 0
    }
}

for (i = 0;i < 5;i++) {
    message.customProperties.messagenumber=i;
    message.body='This is Message #'+i;
    serviceBusService.sendTopicMessage(topic, message, function(error) {
      if (error) {
        console.log(error);
      }
    });
}
```

Service Bus-onderwerpen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md). Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben. Er is geen limiet voor het aantal berichten in een onderwerp hello, maar er is een limiet voor de totale grootte van berichten in een onderwerp Hallo Hallo. De grootte van het onderwerp wordt gedefinieerd tijdens het maken, met een bovengrens van 5 GB.

## <a name="receive-messages-from-a-subscription"></a>Berichten ontvangen van een abonnement
Berichten worden ontvangen van een abonnement met de `receiveSubscriptionMessage` methode op Hallo **ServiceBusService** object. Standaard worden berichten verwijderd uit het Hallo-abonnement als ze worden gelezen; echter (peek) lezen en vergrendelen Hallo-bericht zonder het te verwijderen uit het Hallo-abonnement door de optionele parameter Hallo instelling `isPeekLock` te**true**.

standaardgedrag Hallo van lezen en verwijderen van het Hallo-bericht als onderdeel van de bewerking receive het eenvoudigste model Hallo is en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een fout. toounderstand dit, Neem bijvoorbeeld een scenario waarin de consument problemen Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt. Omdat Service Bus heeft gemarkeerd als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.

Als hello `isPeekLock` parameter is ingesteld, te**true**, Hallo ontvangen, wordt een bewerking met twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren. Wanneer Service Bus een aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing.
Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is Hallo tweede fase van het ontvangstproces voltooid door het aanroepen van **deleteMessage** methode en het geven van het bericht toobe Als een parameter is verwijderd. Hallo **deleteMessage** methode wordt het Hallo-bericht als verbruikt markeren en verwijderen uit het Hallo-abonnement.

Hallo volgende voorbeeld laat zien hoe berichten kunnen worden ontvangen en verwerkt met behulp `receiveSubscriptionMessage`. Hallo voorbeeld eerst ontvangt en wordt een bericht uit de Hallo 'LowMessages' abonnement verwijderd en vervolgens een bericht ontvangt van het gebruik van Hallo 'HighMessages' abonnement `isPeekLock` tootrue ingesteld. Vervolgens wordt verwijderd Hallo-bericht met `deleteMessage`:

```javascript
serviceBusService.receiveSubscriptionMessage('MyTopic', 'LowMessages', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
        console.log(receivedMessage);
    }
});
serviceBusService.receiveSubscriptionMessage('MyTopic', 'HighMessages', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        console.log(lockedMessage);
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
                console.log('message has been deleted.');
            }
        }
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Hoe toohandle toepassing is vastgelopen en onleesbare berichten
Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht. Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo `unlockMessage` methode op de **ServiceBusService** object. Dit wordt Service Bus toounlock veroorzaken binnen Hallo-abonnement en beschikbare toobe opnieuw ontvangen, ofwel Hallo door dezelfde toepassing of door een andere consumerende toepassing verbruikt.

Daarnaast is er een time-out gekoppeld aan een bericht in het abonnement is vergrendeld en als de toepassing hello tooprocess Hallo-bericht voordat mislukt Hallo vergrendelingstime-out verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus Hiermee ontgrendelt u het Hallo-bericht automatisch en wordt het beschikbaar toobe opnieuw ontvangen.

In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo `deleteMessage` methode wordt aangeroepen, is het Hallo-bericht altijd opnieuw bezorgd toohello toepassing opnieuw wordt gestart. Dit wordt vaak genoemd *tenminste eenmaal verwerken*, dat wil zeggen elk bericht ten minste één keer wordt verwerkt maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd. Als Hallo scenario kan geen dubbele verwerking tolereren, moeten toepassingsontwikkelaars levering van aanvullende logica tootheir toepassing toohandle dubbele berichten toevoegen. Dit wordt vaak bereikt met behulp van de **MessageId** eigenschap van Hallo-bericht dat gelijk bij meerdere bezorgingspogingen blijft.

## <a name="delete-topics-and-subscriptions"></a>Onderwerpen en abonnementen verwijderen
Onderwerpen en abonnementen worden permanent en expliciet moet worden verwijderd via Hallo [Azure-portal] [ Azure portal] of via een programma.
Hallo volgende voorbeeld laat zien hoe toodelete Hallo onderwerp met de naam `MyTopic`:

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

Als u een onderwerp verwijdert, verwijdert ook alle abonnementen die zijn geregistreerd bij Hallo onderwerp. Abonnementen kunnen ook afzonderlijk worden verwijderd. Het volgende voorbeeld ziet u hoe toodelete een abonnement met de naam `HighMessages` van Hallo `MyTopic` onderwerp:

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a>Volgende stappen
Nu u de basisprincipes van Service Bus-onderwerpen Hallo hebt geleerd, volgt u deze koppelingen toolearn meer.

* Zie [wachtrijen, onderwerpen en abonnementen][Queues, topics, and subscriptions].
* API-naslaginformatie voor [SqlFilter][SqlFilter].
* Ga naar Hallo [Azure SDK voor knooppunt] [ Azure SDK for Node] opslagplaats op GitHub.

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[maken en implementeren van een Node.js-toepassing tooan Azure-website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
