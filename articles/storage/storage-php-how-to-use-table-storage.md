---
title: aaaHow toouse table storage uit het PHP | Microsoft Docs
description: Ontdek hoe toouse Hallo PHP toocreate tabel-service en een tabel, invoegen, verwijderen en query Hallo tabel verwijderen.
services: storage
documentationcenter: php
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 1e1036118e208280b4c205da7d7eea61e79359c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-php"></a>Hoe toouse tabel PHP-opslag
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Overzicht
Deze handleiding wordt getoond hoe tooperform algemene scenario's met behulp van hello Azure Table-service. Hallo-voorbeelden zijn geschreven in PHP en gebruiken van Hallo [Azure SDK voor PHP][download]. Hallo scenario's worden behandeld: **maken en verwijderen van een tabel en invoegen, verwijderen en opvragen van entiteiten in een tabel**. Zie voor meer informatie over hello Azure Table-service Hallo [Vervolgstappen](#next-steps) sectie.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Een PHP-toepassing maken
alleen de vereiste voor het maken van een PHP-toepassing die toegang heeft tot hello Azure Table-service is Hallo Hallo verwijst naar klassen in hello Azure SDK voor PHP vanuit uw code. U kunt extra ontwikkeling toocreate uw toepassing, met inbegrip van Kladblok gebruiken.

In deze handleiding gebruikt u functies van de tabel die kunnen worden aangeroepen vanuit binnen een PHP-toepassing lokaal of in de code die wordt uitgevoerd binnen een Azure-Webrol, werkrol of website.

## <a name="get-hello-azure-client-libraries"></a>Hello Azure-clientbibliotheken ophalen
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a>Uw toepassing tooaccess Hallo tabel-service configureren
toouse hello Azure Table service API's, moet u:

1. Hallo autoloader referentiebestand Hallo met [require_once] [ require_once] -instructie en
2. Verwijst naar alle klassen die u kunt gebruiken.

Hallo volgende voorbeeld laat zien hoe tooinclude autoloader bestands- en Hallo Hallo **ServicesBuilder** klasse.

> [!NOTE]
> Hallo-voorbeelden in dit artikel wordt ervan uitgegaan dat u Hallo PHP-clientbibliotheken voor Azure via Composer hebt geïnstalleerd. Als u handmatig Hallo bibliotheken geïnstalleerd, moet u tooreference hello <code>WindowsAzure.php</code> autoloader-bestand.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

In onderstaande Hallo voorbeelden, Hallo `require_once` instructie wordt altijd weergegeven, maar alleen Hallo klassen nodig zijn voor Hallo voorbeeld tooexecute wordt verwezen.

## <a name="set-up-an-azure-storage-connection"></a>Een Azure-opslag-verbinding instellen
een client van de service Azure Table tooinstantiate, moet u eerst een geldige verbindingsreeks hebben. Hallo-indeling voor Hallo verbindingsreeks voor de tabel is:

Voor toegang tot een service voor live:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Voor toegang tot Hallo emulator opslag:

```php
UseDevelopmentStorage=true
```

toocreate een Azure-service-client, moet u toouse hello **ServicesBuilder** klasse. U kunt:

* Hallo verbinding doorgeven string rechtstreeks tooit of
* Gebruik Hallo **CloudConfigurationManager (CCM)** toocheck meerdere externe voor Hallo-verbindingsreeks gegevensbronnen:
  * Standaard wordt geleverd met ondersteuning voor een externe bron - omgevingsvariabelen
  * u kunt nieuwe bronnen toevoegen door uit te breiden Hallo **ConnectionStringSource** klasse

Voor Hallo voorbeelden die hier wordt beschreven, worden de verbindingsreeks Hallo rechtstreeks doorgegeven.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a>Een tabel maken
Een **TableRestProxy** object kunt u een tabel maken met de Hallo **createTable** methode. Bij het maken van een tabel, kunt u Hallo tabel service time-out kunt instellen. (Zie voor meer informatie over Hallo tabel service time-out [time-outs instellen voor tabel servicebewerkingen][table-service-timeouts].)

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Create table.
    $tableRestProxy->createTable("mytable");
}
catch(ServiceException $e){
    $code = $e->getCode();
    $error_message = $e->getMessage();
    // Handle exception based on error codes and messages.
    // Error codes and messages can be found here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
}
```

Zie voor meer informatie over de beperkingen op tabelnamen [Understanding Hallo Table Service Data Model][table-data-model].

## <a name="add-an-entity-tooa-table"></a>Een entiteit tooa tabel toevoegen
tooadd een entiteit tooa tabel, maakt u een nieuwe **entiteit** object en geef dit door te**TableRestProxy -> insertEntity**. Houd er rekening mee dat wanneer u een entiteit maakt, moet u een `PartitionKey` en `RowKey`. Deze Hallo unieke id's voor een entiteit zijn en zijn waarden die veel sneller dan andere entiteitseigenschappen kunnen worden opgevraagd. gebruikt Hallo systeem `PartitionKey` tooautomatically hello tabelentiteiten distribueren via veel opslagknooppunten. Entiteiten met dezelfde Hallo `PartitionKey` zijn opgeslagen op Hallo hetzelfde knooppunt. (Bewerkingen voor meerdere entiteiten die zijn opgeslagen op hetzelfde knooppunt uitvoeren Hallo beter dan op entiteiten die zijn opgeslagen op verschillende knooppunten.) Hallo `RowKey` Hallo unieke ID van een entiteit binnen een partitie is.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$entity = new Entity();
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity->addProperty("Location", EdmType::STRING, "Home");

try{
    $tableRestProxy->insertEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
}
```

Zie voor meer informatie over de eigenschappen van de tabel en typen [Understanding Hallo Table Service Data Model][table-data-model].

Hallo **TableRestProxy** klasse biedt twee alternatieve methoden voor het invoegen van entiteiten: **insertOrMergeEntity** en **insertOrReplaceEntity**. toouse deze methoden, maak een nieuwe **entiteit** en geven deze als een parameter tooeither-methode. Elke methode worden Hallo entiteit ingevoegd als deze niet bestaat. Als Hallo entiteit al bestaat, **insertOrMergeEntity** eigenschapswaarden bijgewerkt als Hallo eigenschappen al bestaat en worden nieuwe eigenschappen toegevoegd als ze niet bestaan, terwijl **insertOrReplaceEntity** volledig vervangt een bestaande entiteit. Hallo volgende voorbeeld wordt getoond hoe toouse **insertOrMergeEntity**. Als de entiteit met de Hallo `PartitionKey` 'tasksSeattle' en `RowKey` '1' niet al bestaat, wordt ingevoegd. Echter, als deze eerder is ingevoegd (zoals weergegeven in bovenstaande Hallo voorbeeld), Hallo `DueDate` eigenschap wordt bijgewerkt en Hallo `Status` eigenschap wordt toegevoegd. Hallo `Description` en `Location` eigenschappen ook worden bijgewerkt, maar met waarden die effectief blijven ongewijzigd. Als deze laatste twee eigenschappen zijn niet toegevoegd, zoals in Hallo voorbeeld, maar op Hallo doelentiteit bestonden, blijft hun bestaande waarden ongewijzigd.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

//Create new entity.
$entity = new Entity();

// PartitionKey and RowKey are required.
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");

// If entity exists, existing properties are updated with new values and
// new properties are added. Missing properties are unchanged.
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified hello DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace hello entity with PartitionKey "tasksSeattle" and RowKey "1".
    $tableRestProxy->insertOrMergeEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="retrieve-a-single-entity"></a>Eén entiteit ophalen
Hallo **TableRestProxy -> getEntity** methode kunt u tooretrieve één entiteit via het opvragen van de `PartitionKey` en `RowKey`. In onderstaande Hallo voorbeeld, Hallo partitiesleutel `tasksSeattle` en rijsleutel `1` toohello worden doorgegeven **getEntity** methode.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    $result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entity = $result->getEntity();

echo $entity->getPartitionKey().":".$entity->getRowKey();
```

## <a name="retrieve-all-entities-in-a-partition"></a>Alle entiteiten in een partitie ophalen
Entiteit-query's worden gemaakt met behulp van filters (Zie voor meer informatie [opvragen van tabellen en entiteiten][filters]). tooretrieve alle entiteiten in partitie, gebruikt u Hallo filter ' PartitionKey eq *partitienaam*'. Hallo volgende voorbeeld wordt getoond hoe tooretrieve alle entiteiten in Hallo `tasksSeattle` partitie door een filter toohello **queryEntities** methode.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "PartitionKey eq 'tasksSeattle'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a>Een subset van entiteiten in een partitie ophalen
hetzelfde patroon dat wordt gebruikt in het vorige voorbeeld Hallo Hallo gebruikte tooretrieve een subset van entiteiten in een partitie kan worden. Hallo subset van de entiteiten die u ophalen worden bepaald door Hallo filter dat u gebruikt (Zie voor meer informatie [opvragen van tabellen en entiteiten][filters]) .hello volgende voorbeeld ziet u hoe een filter tooretrieve toouse alle entiteiten met een specifieke `Location` en een `DueDate` kleiner is dan een opgegeven datum.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "Location eq 'Office' and DueDate lt '2012-11-5'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entity-properties"></a>Ophalen van een subset van entiteitseigenschappen
Een query kunt een subset van entiteitseigenschappen ophalen. Deze methode, aangeroepen *projectie*, verbruikt minder bandbreedte en kan de queryprestaties verbeteren, vooral bij grote entiteiten. toospecify een eigenschap toobe opgehaald, Hallo-naam van Hallo eigenschap toohello doorgeeft **Query -> addSelectField** methode. U kunt deze methode tooadd meerdere keren aanroepen meer eigenschappen. Na het uitvoeren van **TableRestProxy -> queryEntities**, Hallo geretourneerd entiteiten wordt alleen geselecteerd Hallo eigenschappen hebben. (Als u tooreturn een subset van de tabelentiteiten wilt, gebruikt u een filter zoals weergegeven in de bovenstaande Hallo query's.)

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\QueryEntitiesOptions;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$options = new QueryEntitiesOptions();
$options->addSelectField("Description");

try    {
    $result = $tableRestProxy->queryEntities("mytable", $options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

// All entities in hello table are returned, regardless of whether
// they have hello Description field.
// toolimit hello results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a>Bijwerken van een entiteit
Een bestaande entiteit kan worden bijgewerkt met behulp van Hallo **entiteit -> setProperty** en **entiteit -> addProperty** methoden op Hallo entiteit en vervolgens aanroepen **TableRestProxy-updateEntity >** . Hallo volgende voorbeeld worden opgehaald van een entiteit, één eigenschap wijzigt, verwijdert u een andere eigenschap en wordt een nieuwe eigenschap toegevoegd. Opmerking dat u een eigenschap verwijderen kunt door de waarde ervan te**null**.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);

$entity = $result->getEntity();

$entity->setPropertyValue("DueDate", new DateTime()); //Modified DueDate.

$entity->setPropertyValue("Location", null); //Removed Location.

$entity->addProperty("Status", EdmType::STRING, "In progress"); //Added Status.

try    {
    $tableRestProxy->updateEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-an-entity"></a>Een entiteit verwijderen
een entiteit toodelete Hallo tabelnaam en van Hallo entiteit doorgeven `PartitionKey` en `RowKey` toohello **TableRestProxy -> deleteEntity** methode.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete entity.
    $tableRestProxy->deleteEntity("mytable", "tasksSeattle", "2");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Houd er rekening mee dat voor controles gelijktijdigheid van taken, u Hallo Etag voor een entiteit toobe verwijderd instellen kunt met behulp van Hallo **DeleteEntityOptions -> setEtag** methode en geven Hallo **DeleteEntityOptions** object te**deleteEntity** als een vierde parameter.

## <a name="batch-table-operations"></a>Batchbewerkingen tabel
Hallo **TableRestProxy -> batch** methode kunt u tooexecute meerdere bewerkingen in een afzonderlijke aanvraag. Hallo patroon hier omvat het toevoegen van bewerkingen te**BatchRequest** object en vervolgens doorgegeven Hallo **BatchRequest** object toohello **TableRestProxy -> batch** methode. een bewerking tooa tooadd **BatchRequest** object, kunt u een van de volgende methoden meerdere keren Hallo aanroepen:

* **addInsertEntity** (toevoegen van een bewerking insertEntity)
* **addUpdateEntity** (toevoegen van een bewerking updateEntity)
* **addMergeEntity** (toevoegen van een bewerking mergeEntity)
* **addInsertOrReplaceEntity** (toevoegen van een bewerking insertOrReplaceEntity)
* **addInsertOrMergeEntity** (toevoegen van een bewerking insertOrMergeEntity)
* **addDeleteEntity** (toevoegen van een bewerking deleteEntity)

Hallo volgende voorbeeld wordt getoond hoe tooexecute **insertEntity** en **deleteEntity** bewerkingen in een afzonderlijke aanvraag:

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;
use MicrosoftAzure\Storage\Table\Models\BatchOperations;

    // Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

// Create list of batch operation.
$operations = new BatchOperations();

$entity1 = new Entity();
$entity1->setPartitionKey("tasksSeattle");
$entity1->setRowKey("2");
$entity1->addProperty("Description", null, "Clean roof gutters.");
$entity1->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity1->addProperty("Location", EdmType::STRING, "Home");

// Add operation toolist of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation toolist of batch operations.
$operations->addDeleteEntity("mytable", "tasksSeattle", "1");

try    {
    $tableRestProxy->batch($operations);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Zie voor meer informatie over batchverwerking tabelbewerkingen [uitvoeren entiteit groepstransacties][entity-group-transactions].

## <a name="delete-a-table"></a>Een tabel verwijderen
Ten slotte toodelete een tabel Hallo tabel naam toohello doorgeven **TableRestProxy -> deleteTable** methode.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete table.
    $tableRestProxy->deleteTable("mytable");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van hello Azure Table-service hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken.

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u toowork visueel met Azure Storage-gegevens op Windows-, Mac OS- en Linux.

* [PHP-ontwikkelaarscentrum](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
