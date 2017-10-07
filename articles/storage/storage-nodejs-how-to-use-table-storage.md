---
title: aaaHow toouse Azure Table storage met Node.js | Microsoft Docs
description: Gestructureerde gegevens opslaan in Hallo cloud met Azure Table storage, een NoSQL-gegevensarchief.
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 990a71337b806d759d0277a7691712346db7b355
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a>Hoe toouse Azure Table storage met Node.js
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Overzicht
Dit onderwerp leest hoe tooperform algemene scenario's met behulp van hello Azure Table-service in een Node.js-toepassing.

Hallo-codevoorbeelden in dit onderwerp wordt ervan uitgegaan dat u hebt al een Node.js-toepassing. Voor informatie over het toocreate een Node.js-toepassing in Azure, Zie een van de volgende onderwerpen:

* [Een Node.js-web-app maken in Azure App Service](../app-service-web/app-service-web-get-started-nodejs.md)
* [Bouw en implementeer een Node.js web-app tooAzure met WebMatrix](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* [Bouw en implementeer een Node.js-toepassing tooan Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (met behulp van Windows PowerShell)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a>Configureren van uw toepassing tooaccess Azure Storage
toouse Azure Storage, moet u hello Azure-opslag-SDK voor Node.js, waaronder een set van gemak bibliotheken die met de Hallo storage REST-services communiceren.

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a>Knooppunt Package Manager (NPM) tooinstall Hallo pakket gebruiken
1. Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Unix) en navigeer toohello map waar u uw toepassing hebt gemaakt.
2. Type **npm Installeer azure-opslag** in Hallo-opdrachtvenster. Uitvoer van de opdracht Hallo is vergelijkbaar toohello voorbeeld te volgen.

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
3. U kunt handmatig uitvoeren Hallo **ls** tooverify opdracht die een **knooppunt\_modules** map is gemaakt. In deze map vindt u Hallo **azure-opslag** , dit pakket bevat, moet u tooaccess opslag Hallo-bibliotheken.

### <a name="import-hello-package"></a>Hallo-pakket importeren
Toevoegen van de volgende code toohello bovenaan Hallo Hallo **server.js** bestand in uw toepassing:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Een Azure Storage-verbinding instellen
Hello azure module lezen omgevingsvariabelen hello AZURE\_opslag\_ACCOUNT en AZURE\_opslag\_toegang\_sleutel of AZURE\_opslag\_verbinding \_Tekenreeks voor de vereiste informatie op tooconnect tooyour Azure storage-account. Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens Hallo opgeven bij het aanroepen van **TableService**.

Voor een voorbeeld van het Hallo-omgevingsvariabelen instellen in Hallo [Azure-portal](https://portal.azure.com) Zie voor een Azure-Website [Node.js web app met behulp van hello Azure Table-Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).

## <a name="create-a-table"></a>Een tabel maken
Hallo volgende code maakt een **TableService** object en gebruikt deze toocreate een nieuwe tabel. Voeg de volgende Hallo aan de bovenkant Hallo van **server.js**.

```nodejs
var tableSvc = azure.createTableService();
```

Hallo aanroep te**createTableIfNotExists** wordt een nieuwe tabel maken met de opgegeven naam Hallo als deze niet al bestaat. Hallo wordt volgende voorbeeld een nieuwe tabel MijnTabel "' als deze niet al bestaat:

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

Hallo `result.created` worden `true` als een nieuwe tabel is gemaakt, en `false` als Hallo tabel al bestaat. Hallo `response` bevat informatie over het Hallo-aanvraag.

### <a name="filters"></a>Filters
Optionele filteren bewerkingen kunnen worden toegepast toooperations uitgevoerd met behulp van **TableService**. Bewerkingen voor het filteren kunt opnemen logboekregistratie, automatisch opnieuw, enzovoort. Filters zijn objecten die een methode met Hallo handtekening te implementeren:

```nodejs
function handle (requestOptions, next)
```

Hierna moet u de voorverwerking op Hallo aanvraag opties, moet Hallo-methode toocall 'volgende' doorgeven van een retouraanroep Hello handtekening te volgen:

```nodejs
function (returnObject, finalCallback, next)
```

In deze retouraanroep en na het verwerken van Hallo returnObject (Hallo reactie van Hallo aanvraag toohello server), Hallo callback tooeither moet vervolgens worden aangeroepen als deze bestaat toocontinue verwerking van andere filters of gewoon finalCallback-aanroep anders tooend Hallo het aanroepen van de service.

Twee filters die Pogingslogica implementeren zijn opgenomen in hello Azure SDK voor Node.js, **ExponentialRetryPolicyFilter** en **LinearRetryPolicyFilter**. Hallo volgende maakt een **TableService** object dat gebruikmaakt van Hallo **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a>Een entiteit tooa tabel toevoegen
tooadd een entiteit maakt eerst een object dat de entiteitseigenschappen van uw definieert. Alle entiteiten moeten bevatten een **PartitionKey** en **RowKey**, die de unieke id's voor Hallo entiteit zijn.

* **PartitionKey** -bepaalt Hallo partitie die de entiteit Hallo is opgeslagen in
* **RowKey** - unieke wijze identificeert Hallo entiteit binnen Hallo partitie

Beide **PartitionKey** en **RowKey** moet tekenreekswaarden. Zie voor meer informatie [Understanding Hallo Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Hallo Hieronder volgt een voorbeeld van het definiëren van een entiteit. Houd er rekening mee dat **dueDate** is gedefinieerd als een soort **Edm.DateTime**. Geven Hallo-type is optioneel en typen zal worden afgeleid indien niet opgegeven.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> Er is ook een **tijdstempel** veld voor elke record, die door Azure wordt ingesteld wanneer een entiteit wordt ingevoegd of bijgewerkt.
>
>

U kunt ook Hallo **entityGenerator** toocreate entiteiten. Hallo volgende voorbeeld maakt Hallo dezelfde taak entiteit met Hallo **entityGenerator**.

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

een tabel entity tooyour tooadd doorgeven Hallo entiteit object toohello **insertEntity** methode.

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

Als Hallo-bewerking voltooid is, `result` bevat Hallo [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) Hallo ingevoegd record en `response` bevat informatie over het Hallo-bewerking.

Voorbeeld van een antwoord:

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> Standaard **insertEntity** resulteert niet in de entiteit ingevoegd Hallo als onderdeel van Hallo `response` informatie. Als u van plan bent andere bewerkingen uitvoert op deze entiteit of toocache Hallo informatie wilt, kan zijn nuttig toohave geretourneerd als onderdeel van Hallo `result`. U kunt dit doen door in te schakelen **echoContent** als volgt:
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a>Bijwerken van een entiteit
Er zijn meerdere methoden beschikbaar tooupdate van een bestaande entiteit:

* **replaceEntity** -updates van een bestaande entiteit door deze te vervangen
* **mergeEntity** -updates van een bestaande entiteit door de nieuwe eigenschapswaarden samenvoegen in een bestaande Hallo-entiteit
* **insertOrReplaceEntity** -updates van een bestaande entiteit door deze te vervangen. Als er is geen entiteit bestaat, wordt een nieuwe ingevoegd
* **insertOrMergeEntity** -updates van een bestaande entiteit door nieuwe eigenschapswaarden in Hallo bestaande samen te voegen. Als er is geen entiteit bestaat, wordt een nieuwe ingevoegd

Hallo volgende voorbeeld ziet u het bijwerken van een entiteit met **replaceEntity**:

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> Standaard wordt bijwerken van een entiteit niet gecontroleerd toosee als Hallo gegevens wordt bijgewerkt eerder is gewijzigd door een ander proces. gelijktijdige toosupport-updates:
>
> 1. Haal Hallo ETag van Hallo-object wordt bijgewerkt. Dit wordt geretourneerd als onderdeel van Hallo `response` voor elke entiteit-gerelateerde bewerking en kan worden opgehaald via `response['.metadata'].etag`.
> 2. Bij het uitvoeren van een updatebewerking op een entiteit toevoegen Hallo ETag informatie die eerder werden nieuwe entiteit toohello opgehaald. Bijvoorbeeld:
>
>       entity2 [.metadata] .etag = currentEtag;
> 3. Hallo updatebewerking niet uitvoeren. Als Hallo entiteit is gewijzigd sinds u opgehaald Hallo ETag-waarde, zoals een ander exemplaar van uw toepassing een `error` wordt geretourneerd met de mededeling dat Hallo update voorwaarde die is opgegeven in Hallo-aanvraag is niet voldaan aan.
>
>

Met **replaceEntity** en **mergeEntity**als Hallo-entiteit die wordt bijgewerkt niet bestaat, Hallo updatebewerking zullen mislukken. Als u toostore een entiteit wenst ongeacht of deze al bestaat, Gebruik daarom **insertOrReplaceEntity** of **insertOrMergeEntity**.

Hallo `result` voor geslaagde update bevat operations Hallo **Etag** Hallo bijgewerkt entiteit.

## <a name="work-with-groups-of-entities"></a>Werken met groepen van entiteiten
Soms is het zin toosubmit meerdere bewerkingen samen in een batch-tooensure atomic verwerken door Hallo-server. tooaccomplish die gebruik Hallo **TableBatch** toocreate een batch klasse en gebruik vervolgens Hallo **executeBatch** methode van **TableService** tooperform Hallo operations batch verwerkt.

 Hallo volgende voorbeeld ziet u twee entiteiten in een batch te verzenden:

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

Voor een geslaagde batchbewerkingen, `result` bevat informatie voor elke bewerking in Hallo batch.

### <a name="work-with-batched-operations"></a>Werken met batchbewerkingen
Bewerkingen toegevoegd tooa batch kan worden gecontroleerd door het bekijken van Hallo `operations` eigenschap. U kunt ook Hallo methoden toowork met bewerkingen te volgen:

* **Schakel** -Hiermee wist u alle bewerkingen van een batch
* **getOperations** -opgehaald van een bewerking van het Hallo-batch
* **hasOperations** -retourneert true als Hallo batch bewerkingen bevat
* **removeOperations** -Hiermee verwijdert u een bewerking
* **de grootte van** -retourneert het aantal bewerkingen in batch Hallo Hallo

## <a name="retrieve-an-entity-by-key"></a>Een entiteit sleutel ophalen
een specifieke entiteit op basis van Hallo tooreturn **PartitionKey** en **RowKey**, gebruik Hallo **retrieveEntity** methode.

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

Zodra deze bewerking voltooid is, `result` Hallo entiteit bevat.

## <a name="query-a-set-of-entities"></a>Query uitvoeren op een verzameling entiteiten
een tabel tooquery gebruiken Hallo **TableQuery** toobuild van een query-expressie met behulp van de volgende componenten Hallo object:

* **Selecteer** -Hallo velden toobe geretourneerde Hallo query
* **waar** - hello waar component

  * **en** - een `and` where-voorwaarde
  * **of** - een `or` where-voorwaarde
* **Top** -het aantal items toofetch Hallo

Hallo wordt volgende voorbeeld een query die Hallo bovenste vijf items met een PartitionKey van 'hometasks' wordt geretourneerd.

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

Aangezien **Selecteer** niet wordt gebruikt, alle velden worden geretourneerd. tooperform Hallo-query op een tabel, gebruik **queryEntities**. Hallo volgende voorbeeld maakt gebruik van deze query tooreturn entiteiten from "MijnTabel".

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

Als dit lukt, `result.entries` bevat een matrix van entiteiten die overeenkomen met Hallo-query. Als het Hallo-query kan niet tooreturn is alle entiteiten `result.continuationToken` worden niet -*null* en kunnen worden gebruikt als de derde parameter van Hallo **queryEntities** tooretrieve meer resultaten. Gebruik voor de eerste query hello, *null* voor de derde parameter Hallo.

### <a name="query-a-subset-of-entity-properties"></a>Een query uitvoeren op een subset van entiteitseigenschappen
Een query tooa tabel ophalen slechts enkele velden van een entiteit.
Dit verbruikt minder bandbreedte en kan de queryprestaties verbeteren, vooral bij grote entiteiten. Gebruik Hallo **Selecteer** component en pass Hallo-namen van Hallo velden toobe geretourneerd. Bijvoorbeeld: hello volgende query retourneert alleen Hallo **beschrijving** en **dueDate** velden.

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a>Een entiteit verwijderen
U kunt een entiteit met behulp van de sleutels van de partitie en rij verwijderen. In dit voorbeeld Hallo **task1** object bevat Hallo **RowKey** en **PartitionKey** waarden van Hallo entiteit toobe verwijderd. Vervolgens Hallo-object toohello doorgegeven **deleteEntity** methode.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> Overweeg het gebruik van ETags bij het verwijderen van items, tooensure die Hallo item niet is gewijzigd door een ander proces. Zie [bijwerken van een entiteit](#update-an-entity) voor informatie over het gebruik van ETags.
>
>

## <a name="delete-a-table"></a>Een tabel verwijderen
Hallo volgende code wordt een tabel uit een opslagaccount verwijderd.

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

Als u niet zeker of Hallo tabel bestaat weet, gebruikt u **deleteTableIfExists**.

## <a name="use-continuation-tokens"></a>Voortzetting tokens gebruiken
Wanneer u in de tabellen voor grote hoeveelheden resultaten zoekt, zoekt u voortzetting tokens. Mogelijk zijn er grote hoeveelheden gegevens beschikbaar voor uw query dat u niet beseft waarschijnlijk als u niet toorecognize maken kan wanneer een vervolgtoken aanwezig is.

Hallo resultaten object geretourneerd tijdens het opvragen van entiteiten stelt een `continuationToken` eigenschap bij dergelijke token aanwezig is. U kunt deze vervolgens gebruiken bij het uitvoeren van een query toocontinue toomove over Hallo partitie en tabel entiteiten.

Wanneer een query uitvoert, kan een parameter continuationToken tussen Hallo query objectexemplaar en Hallo callback-functie worden opgegeven:

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

Als u Hallo inspecteren `continuationToken` object, vindt u eigenschappen zoals `nextPartitionKey`, `nextRowKey` en `targetLocation`, wat kan gebruikte tooiterate via alle Hallo resultaten zijn.

Er is een voorbeeld van een voortzetting binnen hello Azure Storage Node.js-opslagplaats op GitHub. Zoek naar `examples/samples/continuationsample.js`.

## <a name="work-with-shared-access-signatures"></a>Werken met handtekeningen voor gedeelde toegang
Shared access signatures (SAS) zijn een veilige manier tooprovide gedetailleerde toegang tootables zonder dat de naam van het opslagaccount of sleutels. SAS zijn vaak gebruikte tooprovide beperkte toegang tooyour gegevens, zoals het toestaan van een mobiele app tooquery records.

Een vertrouwde toepassing zoals een cloud-gebaseerde service genereert een SAS met Hallo **generateSharedAccessSignature** Hallo **TableService**, en biedt dit tooan niet-vertrouwde of semi vertrouwde toepassing zoals een mobiele app. Hallo SAS is gegenereerd met behulp van een beleid, waarin wordt beschreven Hallo begin- en einddatums tijdens welke Hallo SAS geldig is, evenals Hallo toegang niveau toegekende toohello SAS-houder.

Hallo volgende voorbeeld genereert een nieuw beleid voor gedeelde toegang waarmee Hallo SAS houder tooquery (r) Hallo tabel en 100 minuten na aanmaak Hallo-tijd is verstreken.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

Houd er rekening mee dat Hallo hostinformatie worden moet verstrekt, zoals vereist is wanneer Hallo SAS houder ook tooaccess Hallo tabel probeert.

Hallo-clienttoepassing en gebruik Hallo SAS met **TableServiceWithSAS** tooperform bewerkingen op Hallo tabel. Hallo volgt verbindt toohello tabel en een query uitvoeren.

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

Aangezien hello SAS is gegenereerd met alleen query toegang als er een poging tooinsert, bijwerken of verwijderen van entiteiten zijn aangebracht, wordt een fout geretourneerd.

### <a name="access-control-lists"></a>Access Control Lists
U kunt ook een lijst met ACL (Access Control) tooset Hallo-beleid gebruiken voor een SAS. Dit is handig als u tooallow meerdere clients tooaccess Hallo tabel wilt, maar verschillende toegangsbeleid voor elke client bieden.

Een ACL die is geïmplementeerd met behulp van een matrix van toegangsbeleid, met een ID die is gekoppeld aan elk beleid. Hallo volgende voorbeeld definieert twee beleidsregels, één voor 'gebruiker1' en één voor 'gebruiker2':

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Hallo voorbeeld opgehaald na huidige ACL voor Hallo Hallo **hometasks** tabel en wordt vervolgens toegevoegd Hallo nieuwe beleidsregels met behulp van **setTableAcl**. Met deze aanpak kunt:

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Eenmaal Hallo die ACL is ingesteld, kunt u vervolgens maken een SAS op basis van Hallo-ID voor een beleid. Hallo volgende voorbeeld maakt een nieuwe SAS voor 'gebruiker2':

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a>Volgende stappen
Zie Hallo volgende bronnen voor meer informatie.

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u toowork visueel met Azure Storage-gegevens op Windows-, Mac OS- en Linux.
* [Azure-opslag-SDK voor knooppunt](https://github.com/Azure/azure-storage-node) opslagplaats op GitHub.
* [Node.js Developer Center](/develop/nodejs/)
* [Maken en implementeren van een Node.js-toepassing tooan Azure-website](../app-service-web/app-service-web-get-started-nodejs.md)
