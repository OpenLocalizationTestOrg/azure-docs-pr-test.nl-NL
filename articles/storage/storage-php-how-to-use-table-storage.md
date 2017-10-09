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
# <a name="how-toouse-table-storage-from-php"></a><span data-ttu-id="588dd-103">Hoe toouse tabel PHP-opslag</span><span class="sxs-lookup"><span data-stu-id="588dd-103">How toouse table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="588dd-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="588dd-104">Overview</span></span>
<span data-ttu-id="588dd-105">Deze handleiding wordt getoond hoe tooperform algemene scenario's met behulp van hello Azure Table-service.</span><span class="sxs-lookup"><span data-stu-id="588dd-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="588dd-106">Hallo-voorbeelden zijn geschreven in PHP en gebruiken van Hallo [Azure SDK voor PHP][download].</span><span class="sxs-lookup"><span data-stu-id="588dd-106">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="588dd-107">Hallo scenario's worden behandeld: **maken en verwijderen van een tabel en invoegen, verwijderen en opvragen van entiteiten in een tabel**.</span><span class="sxs-lookup"><span data-stu-id="588dd-107">hello scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="588dd-108">Zie voor meer informatie over hello Azure Table-service Hallo [Vervolgstappen](#next-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="588dd-108">For more information on hello Azure Table service, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="588dd-109">Een PHP-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="588dd-109">Create a PHP application</span></span>
<span data-ttu-id="588dd-110">alleen de vereiste voor het maken van een PHP-toepassing die toegang heeft tot hello Azure Table-service is Hallo Hallo verwijst naar klassen in hello Azure SDK voor PHP vanuit uw code.</span><span class="sxs-lookup"><span data-stu-id="588dd-110">hello only requirement for creating a PHP application that accesses hello Azure Table service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="588dd-111">U kunt extra ontwikkeling toocreate uw toepassing, met inbegrip van Kladblok gebruiken.</span><span class="sxs-lookup"><span data-stu-id="588dd-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="588dd-112">In deze handleiding gebruikt u functies van de tabel die kunnen worden aangeroepen vanuit binnen een PHP-toepassing lokaal of in de code die wordt uitgevoerd binnen een Azure-Webrol, werkrol of website.</span><span class="sxs-lookup"><span data-stu-id="588dd-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="588dd-113">Hello Azure-clientbibliotheken ophalen</span><span class="sxs-lookup"><span data-stu-id="588dd-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a><span data-ttu-id="588dd-114">Uw toepassing tooaccess Hallo tabel-service configureren</span><span class="sxs-lookup"><span data-stu-id="588dd-114">Configure your application tooaccess hello Table service</span></span>
<span data-ttu-id="588dd-115">toouse hello Azure Table service API's, moet u:</span><span class="sxs-lookup"><span data-stu-id="588dd-115">toouse hello Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="588dd-116">Hallo autoloader referentiebestand Hallo met [require_once] [ require_once] -instructie en</span><span class="sxs-lookup"><span data-stu-id="588dd-116">Reference hello autoloader file using hello [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="588dd-117">Verwijst naar alle klassen die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="588dd-117">Reference any classes you might use.</span></span>

<span data-ttu-id="588dd-118">Hallo volgende voorbeeld laat zien hoe tooinclude autoloader bestands- en Hallo Hallo **ServicesBuilder** klasse.</span><span class="sxs-lookup"><span data-stu-id="588dd-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="588dd-119">Hallo-voorbeelden in dit artikel wordt ervan uitgegaan dat u Hallo PHP-clientbibliotheken voor Azure via Composer hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="588dd-119">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="588dd-120">Als u handmatig Hallo bibliotheken geïnstalleerd, moet u tooreference hello <code>WindowsAzure.php</code> autoloader-bestand.</span><span class="sxs-lookup"><span data-stu-id="588dd-120">If you installed hello libraries manually, you need tooreference hello <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="588dd-121">In onderstaande Hallo voorbeelden, Hallo `require_once` instructie wordt altijd weergegeven, maar alleen Hallo klassen nodig zijn voor Hallo voorbeeld tooexecute wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="588dd-121">In hello examples below, hello `require_once` statement is always shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="588dd-122">Een Azure-opslag-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="588dd-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="588dd-123">een client van de service Azure Table tooinstantiate, moet u eerst een geldige verbindingsreeks hebben.</span><span class="sxs-lookup"><span data-stu-id="588dd-123">tooinstantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="588dd-124">Hallo-indeling voor Hallo verbindingsreeks voor de tabel is:</span><span class="sxs-lookup"><span data-stu-id="588dd-124">hello format for hello Table service connection string is:</span></span>

<span data-ttu-id="588dd-125">Voor toegang tot een service voor live:</span><span class="sxs-lookup"><span data-stu-id="588dd-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="588dd-126">Voor toegang tot Hallo emulator opslag:</span><span class="sxs-lookup"><span data-stu-id="588dd-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="588dd-127">toocreate een Azure-service-client, moet u toouse hello **ServicesBuilder** klasse.</span><span class="sxs-lookup"><span data-stu-id="588dd-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="588dd-128">U kunt:</span><span class="sxs-lookup"><span data-stu-id="588dd-128">You can:</span></span>

* <span data-ttu-id="588dd-129">Hallo verbinding doorgeven string rechtstreeks tooit of</span><span class="sxs-lookup"><span data-stu-id="588dd-129">pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="588dd-130">Gebruik Hallo **CloudConfigurationManager (CCM)** toocheck meerdere externe voor Hallo-verbindingsreeks gegevensbronnen:</span><span class="sxs-lookup"><span data-stu-id="588dd-130">use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="588dd-131">Standaard wordt geleverd met ondersteuning voor een externe bron - omgevingsvariabelen</span><span class="sxs-lookup"><span data-stu-id="588dd-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="588dd-132">u kunt nieuwe bronnen toevoegen door uit te breiden Hallo **ConnectionStringSource** klasse</span><span class="sxs-lookup"><span data-stu-id="588dd-132">you can add new sources by extending hello **ConnectionStringSource** class</span></span>

<span data-ttu-id="588dd-133">Voor Hallo voorbeelden die hier wordt beschreven, worden de verbindingsreeks Hallo rechtstreeks doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="588dd-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="588dd-134">Een tabel maken</span><span class="sxs-lookup"><span data-stu-id="588dd-134">Create a table</span></span>
<span data-ttu-id="588dd-135">Een **TableRestProxy** object kunt u een tabel maken met de Hallo **createTable** methode.</span><span class="sxs-lookup"><span data-stu-id="588dd-135">A **TableRestProxy** object lets you create a table with hello **createTable** method.</span></span> <span data-ttu-id="588dd-136">Bij het maken van een tabel, kunt u Hallo tabel service time-out kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="588dd-136">When creating a table, you can set hello Table service timeout.</span></span> <span data-ttu-id="588dd-137">(Zie voor meer informatie over Hallo tabel service time-out [time-outs instellen voor tabel servicebewerkingen][table-service-timeouts].)</span><span class="sxs-lookup"><span data-stu-id="588dd-137">(For more information about hello Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

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

<span data-ttu-id="588dd-138">Zie voor meer informatie over de beperkingen op tabelnamen [Understanding Hallo Table Service Data Model][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="588dd-138">For information about restrictions on table names, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="588dd-139">Een entiteit tooa tabel toevoegen</span><span class="sxs-lookup"><span data-stu-id="588dd-139">Add an entity tooa table</span></span>
<span data-ttu-id="588dd-140">tooadd een entiteit tooa tabel, maakt u een nieuwe **entiteit** object en geef dit door te**TableRestProxy -> insertEntity**.</span><span class="sxs-lookup"><span data-stu-id="588dd-140">tooadd an entity tooa table, create a new **Entity** object and pass it too**TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="588dd-141">Houd er rekening mee dat wanneer u een entiteit maakt, moet u een `PartitionKey` en `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="588dd-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="588dd-142">Deze Hallo unieke id's voor een entiteit zijn en zijn waarden die veel sneller dan andere entiteitseigenschappen kunnen worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="588dd-142">These are hello unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="588dd-143">gebruikt Hallo systeem `PartitionKey` tooautomatically hello tabelentiteiten distribueren via veel opslagknooppunten.</span><span class="sxs-lookup"><span data-stu-id="588dd-143">hello system uses `PartitionKey` tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="588dd-144">Entiteiten met dezelfde Hallo `PartitionKey` zijn opgeslagen op Hallo hetzelfde knooppunt.</span><span class="sxs-lookup"><span data-stu-id="588dd-144">Entities with hello same `PartitionKey` are stored on hello same node.</span></span> <span data-ttu-id="588dd-145">(Bewerkingen voor meerdere entiteiten die zijn opgeslagen op hetzelfde knooppunt uitvoeren Hallo beter dan op entiteiten die zijn opgeslagen op verschillende knooppunten.) Hallo `RowKey` Hallo unieke ID van een entiteit binnen een partitie is.</span><span class="sxs-lookup"><span data-stu-id="588dd-145">(Operations on multiple entities stored on hello same node perform better than on entities stored across different nodes.) hello `RowKey` is hello unique ID of an entity within a partition.</span></span>

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

<span data-ttu-id="588dd-146">Zie voor meer informatie over de eigenschappen van de tabel en typen [Understanding Hallo Table Service Data Model][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="588dd-146">For information about Table properties and types, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="588dd-147">Hallo **TableRestProxy** klasse biedt twee alternatieve methoden voor het invoegen van entiteiten: **insertOrMergeEntity** en **insertOrReplaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="588dd-147">hello **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="588dd-148">toouse deze methoden, maak een nieuwe **entiteit** en geven deze als een parameter tooeither-methode.</span><span class="sxs-lookup"><span data-stu-id="588dd-148">toouse these methods, create a new **Entity** and pass it as a parameter tooeither method.</span></span> <span data-ttu-id="588dd-149">Elke methode worden Hallo entiteit ingevoegd als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="588dd-149">Each method will insert hello entity if it does not exist.</span></span> <span data-ttu-id="588dd-150">Als Hallo entiteit al bestaat, **insertOrMergeEntity** eigenschapswaarden bijgewerkt als Hallo eigenschappen al bestaat en worden nieuwe eigenschappen toegevoegd als ze niet bestaan, terwijl **insertOrReplaceEntity** volledig vervangt een bestaande entiteit.</span><span class="sxs-lookup"><span data-stu-id="588dd-150">If hello entity already exists, **insertOrMergeEntity** updates property values if hello properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="588dd-151">Hallo volgende voorbeeld wordt getoond hoe toouse **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="588dd-151">hello following example shows how toouse **insertOrMergeEntity**.</span></span> <span data-ttu-id="588dd-152">Als de entiteit met de Hallo `PartitionKey` 'tasksSeattle' en `RowKey` '1' niet al bestaat, wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="588dd-152">If hello entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="588dd-153">Echter, als deze eerder is ingevoegd (zoals weergegeven in bovenstaande Hallo voorbeeld), Hallo `DueDate` eigenschap wordt bijgewerkt en Hallo `Status` eigenschap wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="588dd-153">However, if it has previously been inserted (as shown in hello example above), hello `DueDate` property will be updated, and hello `Status` property will be added.</span></span> <span data-ttu-id="588dd-154">Hallo `Description` en `Location` eigenschappen ook worden bijgewerkt, maar met waarden die effectief blijven ongewijzigd.</span><span class="sxs-lookup"><span data-stu-id="588dd-154">hello `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="588dd-155">Als deze laatste twee eigenschappen zijn niet toegevoegd, zoals in Hallo voorbeeld, maar op Hallo doelentiteit bestonden, blijft hun bestaande waarden ongewijzigd.</span><span class="sxs-lookup"><span data-stu-id="588dd-155">If these latter two properties were not added as shown in hello example, but existed on hello target entity, their existing values would remain unchanged.</span></span>

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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="588dd-156">Eén entiteit ophalen</span><span class="sxs-lookup"><span data-stu-id="588dd-156">Retrieve a single entity</span></span>
<span data-ttu-id="588dd-157">Hallo **TableRestProxy -> getEntity** methode kunt u tooretrieve één entiteit via het opvragen van de `PartitionKey` en `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="588dd-157">hello **TableRestProxy->getEntity** method allows you tooretrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="588dd-158">In onderstaande Hallo voorbeeld, Hallo partitiesleutel `tasksSeattle` en rijsleutel `1` toohello worden doorgegeven **getEntity** methode.</span><span class="sxs-lookup"><span data-stu-id="588dd-158">In hello example below, hello partition key `tasksSeattle` and row key `1` are passed toohello **getEntity** method.</span></span>

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

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="588dd-159">Alle entiteiten in een partitie ophalen</span><span class="sxs-lookup"><span data-stu-id="588dd-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="588dd-160">Entiteit-query's worden gemaakt met behulp van filters (Zie voor meer informatie [opvragen van tabellen en entiteiten][filters]).</span><span class="sxs-lookup"><span data-stu-id="588dd-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="588dd-161">tooretrieve alle entiteiten in partitie, gebruikt u Hallo filter ' PartitionKey eq *partitienaam*'.</span><span class="sxs-lookup"><span data-stu-id="588dd-161">tooretrieve all entities in partition, use hello filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="588dd-162">Hallo volgende voorbeeld wordt getoond hoe tooretrieve alle entiteiten in Hallo `tasksSeattle` partitie door een filter toohello **queryEntities** methode.</span><span class="sxs-lookup"><span data-stu-id="588dd-162">hello following example shows how tooretrieve all entities in hello `tasksSeattle` partition by passing a filter toohello **queryEntities** method.</span></span>

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

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="588dd-163">Een subset van entiteiten in een partitie ophalen</span><span class="sxs-lookup"><span data-stu-id="588dd-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="588dd-164">hetzelfde patroon dat wordt gebruikt in het vorige voorbeeld Hallo Hallo gebruikte tooretrieve een subset van entiteiten in een partitie kan worden.</span><span class="sxs-lookup"><span data-stu-id="588dd-164">hello same pattern used in hello previous example can be used tooretrieve any subset of entities in a partition.</span></span> <span data-ttu-id="588dd-165">Hallo subset van de entiteiten die u ophalen worden bepaald door Hallo filter dat u gebruikt (Zie voor meer informatie [opvragen van tabellen en entiteiten][filters]) .hello volgende voorbeeld ziet u hoe een filter tooretrieve toouse alle entiteiten met een specifieke `Location` en een `DueDate` kleiner is dan een opgegeven datum.</span><span class="sxs-lookup"><span data-stu-id="588dd-165">hello subset of entities you retrieve are determined by hello filter you use (for more information, see [Querying Tables and Entities][filters]).hello following example shows how toouse a filter tooretrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

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

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="588dd-166">Ophalen van een subset van entiteitseigenschappen</span><span class="sxs-lookup"><span data-stu-id="588dd-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="588dd-167">Een query kunt een subset van entiteitseigenschappen ophalen.</span><span class="sxs-lookup"><span data-stu-id="588dd-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="588dd-168">Deze methode, aangeroepen *projectie*, verbruikt minder bandbreedte en kan de queryprestaties verbeteren, vooral bij grote entiteiten.</span><span class="sxs-lookup"><span data-stu-id="588dd-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="588dd-169">toospecify een eigenschap toobe opgehaald, Hallo-naam van Hallo eigenschap toohello doorgeeft **Query -> addSelectField** methode.</span><span class="sxs-lookup"><span data-stu-id="588dd-169">toospecify a property toobe retrieved, pass hello name of hello property toohello **Query->addSelectField** method.</span></span> <span data-ttu-id="588dd-170">U kunt deze methode tooadd meerdere keren aanroepen meer eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="588dd-170">You can call this method multiple times tooadd more properties.</span></span> <span data-ttu-id="588dd-171">Na het uitvoeren van **TableRestProxy -> queryEntities**, Hallo geretourneerd entiteiten wordt alleen geselecteerd Hallo eigenschappen hebben.</span><span class="sxs-lookup"><span data-stu-id="588dd-171">After executing **TableRestProxy->queryEntities**, hello returned entities will only have hello selected properties.</span></span> <span data-ttu-id="588dd-172">(Als u tooreturn een subset van de tabelentiteiten wilt, gebruikt u een filter zoals weergegeven in de bovenstaande Hallo query's.)</span><span class="sxs-lookup"><span data-stu-id="588dd-172">(If you want tooreturn a subset of Table entities, use a filter as shown in hello queries above.)</span></span>

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

## <a name="update-an-entity"></a><span data-ttu-id="588dd-173">Bijwerken van een entiteit</span><span class="sxs-lookup"><span data-stu-id="588dd-173">Update an entity</span></span>
<span data-ttu-id="588dd-174">Een bestaande entiteit kan worden bijgewerkt met behulp van Hallo **entiteit -> setProperty** en **entiteit -> addProperty** methoden op Hallo entiteit en vervolgens aanroepen **TableRestProxy-updateEntity >** .</span><span class="sxs-lookup"><span data-stu-id="588dd-174">An existing entity can be updated by using hello **Entity->setProperty** and **Entity->addProperty** methods on hello entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="588dd-175">Hallo volgende voorbeeld worden opgehaald van een entiteit, één eigenschap wijzigt, verwijdert u een andere eigenschap en wordt een nieuwe eigenschap toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="588dd-175">hello following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="588dd-176">Opmerking dat u een eigenschap verwijderen kunt door de waarde ervan te**null**.</span><span class="sxs-lookup"><span data-stu-id="588dd-176">Note that you can remove a property by setting its value too**null**.</span></span>

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

## <a name="delete-an-entity"></a><span data-ttu-id="588dd-177">Een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="588dd-177">Delete an entity</span></span>
<span data-ttu-id="588dd-178">een entiteit toodelete Hallo tabelnaam en van Hallo entiteit doorgeven `PartitionKey` en `RowKey` toohello **TableRestProxy -> deleteEntity** methode.</span><span class="sxs-lookup"><span data-stu-id="588dd-178">toodelete an entity, pass hello table name, and hello entity's `PartitionKey` and `RowKey` toohello **TableRestProxy->deleteEntity** method.</span></span>

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

<span data-ttu-id="588dd-179">Houd er rekening mee dat voor controles gelijktijdigheid van taken, u Hallo Etag voor een entiteit toobe verwijderd instellen kunt met behulp van Hallo **DeleteEntityOptions -> setEtag** methode en geven Hallo **DeleteEntityOptions** object te**deleteEntity** als een vierde parameter.</span><span class="sxs-lookup"><span data-stu-id="588dd-179">Note that for concurrency checks, you can set hello Etag for an entity toobe deleted by using hello **DeleteEntityOptions->setEtag** method and passing hello **DeleteEntityOptions** object too**deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="588dd-180">Batchbewerkingen tabel</span><span class="sxs-lookup"><span data-stu-id="588dd-180">Batch table operations</span></span>
<span data-ttu-id="588dd-181">Hallo **TableRestProxy -> batch** methode kunt u tooexecute meerdere bewerkingen in een afzonderlijke aanvraag.</span><span class="sxs-lookup"><span data-stu-id="588dd-181">hello **TableRestProxy->batch** method allows you tooexecute multiple operations in a single request.</span></span> <span data-ttu-id="588dd-182">Hallo patroon hier omvat het toevoegen van bewerkingen te**BatchRequest** object en vervolgens doorgegeven Hallo **BatchRequest** object toohello **TableRestProxy -> batch** methode.</span><span class="sxs-lookup"><span data-stu-id="588dd-182">hello pattern here involves adding operations too**BatchRequest** object and then passing hello **BatchRequest** object toohello **TableRestProxy->batch** method.</span></span> <span data-ttu-id="588dd-183">een bewerking tooa tooadd **BatchRequest** object, kunt u een van de volgende methoden meerdere keren Hallo aanroepen:</span><span class="sxs-lookup"><span data-stu-id="588dd-183">tooadd an operation tooa **BatchRequest** object, you can call any of hello following methods multiple times:</span></span>

* <span data-ttu-id="588dd-184">**addInsertEntity** (toevoegen van een bewerking insertEntity)</span><span class="sxs-lookup"><span data-stu-id="588dd-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="588dd-185">**addUpdateEntity** (toevoegen van een bewerking updateEntity)</span><span class="sxs-lookup"><span data-stu-id="588dd-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="588dd-186">**addMergeEntity** (toevoegen van een bewerking mergeEntity)</span><span class="sxs-lookup"><span data-stu-id="588dd-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="588dd-187">**addInsertOrReplaceEntity** (toevoegen van een bewerking insertOrReplaceEntity)</span><span class="sxs-lookup"><span data-stu-id="588dd-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="588dd-188">**addInsertOrMergeEntity** (toevoegen van een bewerking insertOrMergeEntity)</span><span class="sxs-lookup"><span data-stu-id="588dd-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="588dd-189">**addDeleteEntity** (toevoegen van een bewerking deleteEntity)</span><span class="sxs-lookup"><span data-stu-id="588dd-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="588dd-190">Hallo volgende voorbeeld wordt getoond hoe tooexecute **insertEntity** en **deleteEntity** bewerkingen in een afzonderlijke aanvraag:</span><span class="sxs-lookup"><span data-stu-id="588dd-190">hello following example shows how tooexecute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

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

<span data-ttu-id="588dd-191">Zie voor meer informatie over batchverwerking tabelbewerkingen [uitvoeren entiteit groepstransacties][entity-group-transactions].</span><span class="sxs-lookup"><span data-stu-id="588dd-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="588dd-192">Een tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="588dd-192">Delete a table</span></span>
<span data-ttu-id="588dd-193">Ten slotte toodelete een tabel Hallo tabel naam toohello doorgeven **TableRestProxy -> deleteTable** methode.</span><span class="sxs-lookup"><span data-stu-id="588dd-193">Finally, toodelete a table, pass hello table name toohello **TableRestProxy->deleteTable** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="588dd-194">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="588dd-194">Next steps</span></span>
<span data-ttu-id="588dd-195">Nu u Hallo basisprincipes van hello Azure Table-service hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken.</span><span class="sxs-lookup"><span data-stu-id="588dd-195">Now that you've learned hello basics of hello Azure Table service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="588dd-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u toowork visueel met Azure Storage-gegevens op Windows-, Mac OS- en Linux.</span><span class="sxs-lookup"><span data-stu-id="588dd-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="588dd-197">[PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="588dd-197">[PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
