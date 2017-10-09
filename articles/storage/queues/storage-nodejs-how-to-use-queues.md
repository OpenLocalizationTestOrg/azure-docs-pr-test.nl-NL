---
title: aaaHow toouse Queue storage met Node.js | Microsoft Docs
description: Ontdek hoe toocreate toouse hello Azure Queue-service en delete-wachtrijen en invoegen, ophalen en verwijderen van berichten. Voorbeelden die zijn geschreven in Node.js.
services: storage
documentationcenter: nodejs
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a8a92db0-4333-43dd-a116-28b3147ea401
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 7e9778da4efa69f2e9d8fd480b9b6f5ace85951e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a>Hoe toouse Queue storage met Node.js
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Overzicht
Deze handleiding wordt getoond hoe tooperform algemene scenario's met behulp van Microsoft Azure Queue-service Hallo. Hallo-voorbeelden zijn geschreven met behulp van Hallo Node.js-API. Hallo scenario's worden behandeld: **invoegen**, **inspecteren**, **ophalen**, en **verwijderen** wachtrij berichten, evenals  **maken en verwijderen van wachtrijen**.

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Een Node.js-toepassing maken
Maak een lege Node.js-toepassing. Zie voor instructies over het maken van een Node.js-toepassing [een Node.js-web-app maken in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md), [bouwen en implementeren van een Node.js-toepassing tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) met Windows PowerShell of [ Bouw en implementeer een Node.js web-app tooAzure met behulp van Web Matrix](https://www.microsoft.com/web/webmatrix/).

## <a name="configure-your-application-tooaccess-storage"></a>Uw toepassing tooAccess opslag configureren
toouse Azure-opslag, moet u hello Azure-opslag-SDK voor Node.js, waaronder een set van gemak bibliotheken die met de Hallo storage REST-services communiceren.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Knooppunt Package Manager (NPM) tooobtain Hallo pakket gebruiken
1. Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac), of **Bash** (Unix), gaat u toohello map waar u uw voorbeeldtoepassing hebt gemaakt.
2. Type **npm Installeer azure-opslag** in Hallo-opdrachtvenster. Uitvoer van de opdracht Hallo is vergelijkbaar toohello voorbeeld te volgen.
 
    ```
    azure-storage@0.5.0 node_modules\azure-storage
    +-- extend@1.2.1
    +-- xmlbuilder@0.4.3
    +-- mime@1.2.11
    +-- node-uuid@1.4.3
    +-- validator@3.22.2
    +-- underscore@1.4.4
    +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
    +-- xml2js@0.2.7 (sax@0.5.2)
    +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    ```

3. U kunt handmatig uitvoeren Hallo **ls** tooverify opdracht die een **knooppunt\_modules** map is gemaakt. In deze map vindt u Hallo **azure-opslag** , dit pakket bevat Hallo-bibliotheken die u moet toegang hebben tot opslag.

### <a name="import-hello-package"></a>Hallo-pakket importeren
Hallo na toohello boven in Kladblok of een andere teksteditor toevoegen de **server.js** -bestand van de toepassing hello waar u van plan toouse opslag bent:

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a>Een Azure-opslag-verbinding instellen
Hello azure module lezen omgevingsvariabelen hello AZURE\_opslag\_ACCOUNT en AZURE\_opslag\_toegang\_sleutel of AZURE\_opslag\_verbinding \_Tekenreeks voor de vereiste informatie op tooconnect tooyour Azure storage-account. Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens Hallo opgeven bij het aanroepen van **createQueueService**.

Voor een voorbeeld van het Hallo-omgevingsvariabelen instellen in Hallo [Azure Portal](https://portal.azure.com) Zie [Node.js web app met behulp van Azure Table Service Hallo] voor een Azure-Website.

## <a name="how-to-create-a-queue"></a>Procedure: Een wachtrij maken
Hallo volgende code maakt een **QueueService** object, waarmee u toowork met wachtrijen.

```
var queueSvc = azure.createQueueService();
```

Gebruik Hallo **createQueueIfNotExists** methode, die de opgegeven wachtrij Hallo retourneert als dit al bestaat of maakt een nieuwe wachtrij met de opgegeven naam Hallo als deze niet al bestaat.

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

Als het Hallo-wachtrij is gemaakt, `result.created` is ingesteld op true. Als Hallo wachtrij bestaat, `result.created` is ingesteld op false.

### <a name="filters"></a>Filters
Optionele filteren bewerkingen kunnen worden toegepast toooperations uitgevoerd met behulp van **QueueService**. Bewerkingen voor het filteren kunt opnemen logboekregistratie, automatisch opnieuw, enzovoort. Filters zijn objecten die een methode met Hallo handtekening te implementeren:

```
function handle (requestOptions, next)
```

Hallo-methode moet hierna moet u de voorverwerking op Hallo certificaataanvraagopties, toocall doorgeven van een retouraanroep 'volgende' Hello handtekening te volgen:

```
function (returnObject, finalCallback, next)
```

In deze retouraanroep en na het verwerken van Hallo returnObject (Hallo reactie van Hallo aanvraag toohello server), Hallo callback tooeither moet vervolgens worden aangeroepen als deze bestaat toocontinue verwerking van andere filters of gewoon finalCallback-aanroep anders tooend up Hallo het aanroepen van de service.

Twee filters die Pogingslogica implementeren zijn opgenomen in hello Azure SDK voor Node.js, **ExponentialRetryPolicyFilter** en **LinearRetryPolicyFilter**. Hallo volgende maakt een **QueueService** object dat gebruikmaakt van Hallo **ExponentialRetryPolicyFilter**:

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Procedure: Een bericht in een wachtrij invoegen
een bericht in een wachtrij, gebruik Hallo tooinsert **createMessage** methode voor het maken van een nieuw bericht en deze wachtrij toohello toevoegen.

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a>Procedure: Inspecteren Hallo het Volgendebericht
U kunt bekijken van Hallo-bericht in Hallo begin van een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aanroepen Hallo **peekMessages** methode. Standaard **peekMessages** geeft een enkel bericht weer.

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

Hallo `result` Hallo-bericht bevat.

> [!NOTE]
> Met behulp van **peekMessages** wanneer er geen berichten in wachtrij Hallo zijn niet retourneren een foutmelding, maar er zijn geen berichten worden geretourneerd.
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a>Procedure: Hallo het Volgendebericht uit de wachtrij halen
Verwerken van een bericht is een proces in twee fasen:

1. Hallo-bericht in wachtrij.
2. Verwijder het Hallo-bericht.

gebruik van een bericht toodequeue **getMessages**. Hierdoor Hallo-berichten in wachtrij Hallo onzichtbaar zodat er geen andere clients kunnen verwerken. Wanneer een bericht is verwerkt door uw toepassing, aanroepen **deleteMessage** toodelete op Hallo wachtrij. Hallo volgende voorbeeld wordt een bericht en vervolgens wordt verwijderd:

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
    var message = result[0];
    queueSvc.deleteMessage('myqueue', message.messageId, message.popReceipt, function(error, response){
      if(!error){
        //message deleted
      }
    });
  }
});
```

> [!NOTE]
> Standaard wordt een bericht alleen verborgen voor 30 seconden, waarna deze zichtbaar tooother clients. U kunt een andere waarde opgeven met behulp van `options.visibilityTimeout` met **getMessages**.
> 
> [!NOTE]
> Met behulp van **getMessages** wanneer er geen berichten in wachtrij Hallo zijn niet retourneren een foutmelding, maar er zijn geen berichten worden geretourneerd.
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Procedure: Hallo inhoud van een bericht in de wachtrij wijzigen
U kunt inhoud van een bericht in-place aan Hallo wachtrij met Hallo wijzigen **updateMessage**. Hallo updates Hallo voorbeeldtekst van een bericht te volgen:

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got hello message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Procedure: Aanvullende opties voor waarbij berichten
Er zijn twee manieren u ophalen van berichten uit een wachtrij kunt aanpassen:

* `options.numOfMessages`-Ophalen van een batch met berichten (omhoog too32.)
* `options.visibilityTimeout`-Er is een time-out voor onzichtbaarheid langer of korter zijn ingesteld.

Hallo volgende voorbeeld wordt Hallo **getMessages** methode tooget 15 berichten in één aanroep. Vervolgens wordt verwerkt elke bericht met een for-lus. Hallo onzichtbaarheid toofive minuten voor de time-out voor alle berichten die zijn geretourneerd door deze methode wordt ook ingesteld.

```
queueSvc.getMessages('myqueue', {numOfMessages: 15, visibilityTimeout: 5 * 60}, function(error, result, response){
  if(!error){
    // Messages retreived
    for(var index in result){
      // text is available in result[index].messageText
      var message = result[index];
      queueSvc.deleteMessage(queueName, message.messageId, message.popReceipt, function(error, response){
        if(!error){
          // Message deleted
        }
      });
    }
  }
});
```

## <a name="how-to-get-hello-queue-length"></a>Procedure: Hallo wachtrijlengte ophalen
Hallo **getQueueMetadata** metagegevens over Hallo wachtrij, met inbegrip van de geschatte aantal berichten in wachtrij Hallo Hallo retourneert.

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a>Procedure: Lijst wachtrijen
een lijst van wachtrijen, gebruik tooretrieve **listQueuesSegmented**. tooretrieve een lijst gefilterd op een bepaald voorvoegsel, gebruikt u **listQueuesSegmentedWithPrefix**.

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

Als alle wachtrijen kunnen niet worden geretourneerd, `result.continuationToken` kunnen worden gebruikt als eerste parameter van Hallo **listQueuesSegmented** of Hallo van de tweede parameter van **listQueuesSegmentedWithPrefix** tooretrieve meer resultaten.

## <a name="how-to-delete-a-queue"></a>Procedure: Een wachtrij verwijderen
toodelete een wachtrij en alle Hallo-berichten die dit, neemt u contact de **deleteQueue** methode op Hallo wachtrij-object.

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

alle berichten uit een wachtrij zonder te verwijderen, gebruikt u tooclear **clearMessages**.

## <a name="how-to-work-with-shared-access-signatures"></a>How to: werken met handtekeningen voor gedeelde toegang
Shared Access Signatures (SAS) zijn een veilige manier tooprovide gedetailleerde toegang tooqueues zonder dat de naam van het opslagaccount of sleutels. SAS zijn vaak gebruikte tooprovide beperkte toegang tooyour wachtrijen, zoals het toestaan van een mobiele app toosubmit berichten.

Een vertrouwde toepassing zoals een cloud-gebaseerde service genereert een SAS met Hallo **generateSharedAccessSignature** Hallo **QueueService**, en biedt dit tooan niet-vertrouwde of semi vertrouwde toepassing. Bijvoorbeeld: een mobiele app. Hallo SAS is gegenereerd met behulp van een beleid, waarin wordt beschreven Hallo begin- en einddatums tijdens welke Hallo SAS geldig is, evenals Hallo toegang niveau toegekende toohello SAS-houder.

Hallo volgt genereert een nieuw beleid voor gedeelde toegang waarmee Hallo SAS houder tooadd berichten toohello wachtrij en 100 minuten na aanmaak Hallo-tijd is verstreken.

```
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};

var queueSAS = queueSvc.generateSharedAccessSignature('myqueue', sharedAccessPolicy);
var host = queueSvc.host;
```

Houd er rekening mee dat Hallo hostinformatie worden moet verstrekt, zoals vereist is wanneer Hallo SAS houder ook tooaccess Hallo wachtrij probeert.

Hallo-clienttoepassing en gebruik Hallo SAS met **QueueServiceWithSAS** tooperform bewerkingen op Hallo wachtrij. Hallo volgt verbindt toohello wachtrij en een bericht wordt gemaakt.

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

Aangezien hello SAS is gegenereerd met de toegang voor toevoegen als een poging is gedaan tooread, bijwerken of verwijderen van berichten, wordt een fout geretourneerd.

### <a name="access-control-lists"></a>Toegangsbeheerlijsten
U kunt ook een lijst met ACL (Access Control) tooset Hallo-beleid gebruiken voor een SAS. Dit is handig als u tooallow meerdere clients tooaccess Hallo wachtrij wilt, maar verschillende toegangsbeleid voor elke client bieden.

Een ACL die is geïmplementeerd met behulp van een matrix van toegangsbeleid, met een ID die is gekoppeld aan elk beleid. Hallo volgende voorbeeld definieert twee beleidsregels; een voor 'gebruiker1' en één voor 'gebruiker2':

```
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.PROCESS,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Hallo volgende voorbeeld wordt de huidige ACL voor Hallo **rapportberichten**, voegt u vervolgens Hallo nieuwe beleidsregels met behulp van **setQueueAcl**. Met deze aanpak kunt:

```
var extend = require('extend');
queueSvc.getQueueAcl('myqueue', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    queueSvc.setQueueAcl('myqueue', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Eenmaal Hallo die ACL is ingesteld, kunt u vervolgens maken een SAS op basis van Hallo-ID voor een beleid. Hallo volgende voorbeeld maakt een nieuwe SAS voor 'gebruiker2':

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van queue storage hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken.

* Ga naar Hallo [Azure Storage Team Blog] [Azure Storage Team Blog].
* Ga naar Hallo [Azure-opslag-SDK voor knooppunt] [ Azure Storage SDK for Node] opslagplaats op GitHub.

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[Een Node.js-web-app maken in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md)   
[Node.js web-app met behulp van hello Azure Table-Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
  


[Bouw en implementeer een Node.js-toepassing tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md)   
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [bouwen en implementeren van een Node.js web-app tooAzure met behulp van Web Matrix]: https://www.microsoft.com/web/webmatrix/   
