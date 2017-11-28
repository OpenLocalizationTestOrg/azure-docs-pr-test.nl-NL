---
title: Hoe table storage gebruiken met PHP | Microsoft Docs
description: Informatie over het gebruik van de tabelservice van PHP maken en verwijderen van een tabel, invoegen, verwijderen en opvragen van de tabel.
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
ms.openlocfilehash: 15d3216ef5bb1d7ff312bd886837a3a7b0335afd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-from-php"></a><span data-ttu-id="bd989-103">Hoe table storage gebruiken met PHP</span><span class="sxs-lookup"><span data-stu-id="bd989-103">How to use table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="bd989-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="bd989-104">Overview</span></span>
<span data-ttu-id="bd989-105">Deze handleiding wordt beschreven hoe u veelvoorkomende scenario's met de service Azure Table uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bd989-105">This guide shows you how to perform common scenarios using the Azure Table service.</span></span> <span data-ttu-id="bd989-106">De voorbeelden zijn geschreven in PHP en gebruik de [Azure SDK voor PHP][download].</span><span class="sxs-lookup"><span data-stu-id="bd989-106">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="bd989-107">De scenario's worden behandeld: **maken en verwijderen van een tabel en invoegen, verwijderen en opvragen van entiteiten in een tabel**.</span><span class="sxs-lookup"><span data-stu-id="bd989-107">The scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="bd989-108">Zie voor meer informatie over de Azure Table-service de [Vervolgstappen](#next-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="bd989-108">For more information on the Azure Table service, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="bd989-109">Een PHP-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="bd989-109">Create a PHP application</span></span>
<span data-ttu-id="bd989-110">De enige vereiste voor het maken van een PHP-toepassing die toegang heeft tot de Azure Table-service is de verwijzende klassen in de Azure SDK voor PHP vanuit uw code.</span><span class="sxs-lookup"><span data-stu-id="bd989-110">The only requirement for creating a PHP application that accesses the Azure Table service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="bd989-111">Alle ontwikkelingsprogramma's kunt u uw toepassing, met inbegrip van Kladblok maken.</span><span class="sxs-lookup"><span data-stu-id="bd989-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="bd989-112">In deze handleiding gebruikt u functies van de tabel die kunnen worden aangeroepen vanuit binnen een PHP-toepassing lokaal of in de code die wordt uitgevoerd binnen een Azure-Webrol, werkrol of website.</span><span class="sxs-lookup"><span data-stu-id="bd989-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="bd989-113">De clientbibliotheken van Azure ophalen</span><span class="sxs-lookup"><span data-stu-id="bd989-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-table-service"></a><span data-ttu-id="bd989-114">Uw toepassing configureren voor toegang tot de tabel-service</span><span class="sxs-lookup"><span data-stu-id="bd989-114">Configure your application to access the Table service</span></span>
<span data-ttu-id="bd989-115">Als u wilt de service Azure Table API's gebruikt, moet u:</span><span class="sxs-lookup"><span data-stu-id="bd989-115">To use the Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="bd989-116">Verwijst naar de autoloader-bestand met de [require_once] [ require_once] -instructie en</span><span class="sxs-lookup"><span data-stu-id="bd989-116">Reference the autoloader file using the [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="bd989-117">Verwijst naar alle klassen die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bd989-117">Reference any classes you might use.</span></span>

<span data-ttu-id="bd989-118">Het volgende voorbeeld laat zien hoe de autoloader-bestand en de verwijzing naar de **ServicesBuilder** klasse.</span><span class="sxs-lookup"><span data-stu-id="bd989-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="bd989-119">De voorbeelden in dit artikel wordt ervan uitgegaan dat u de PHP-clientbibliotheken voor Azure via Composer hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="bd989-119">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="bd989-120">Als u handmatig de bibliotheken geïnstalleerd, moet u verwijzen naar de <code>WindowsAzure.php</code> autoloader-bestand.</span><span class="sxs-lookup"><span data-stu-id="bd989-120">If you installed the libraries manually, you need to reference the <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="bd989-121">In de onderstaande voorbeelden de `require_once` instructie wordt altijd weergegeven, maar alleen de klassen die nodig zijn voor het voorbeeld uit te voeren naar worden verwezen.</span><span class="sxs-lookup"><span data-stu-id="bd989-121">In the examples below, the `require_once` statement is always shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="bd989-122">Een Azure-opslag-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="bd989-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="bd989-123">U moet een geldige verbindingsreeks hebben voor het concretiseren van een client met Azure Table-service.</span><span class="sxs-lookup"><span data-stu-id="bd989-123">To instantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="bd989-124">De notatie voor de verbindingsreeks voor de tabel is:</span><span class="sxs-lookup"><span data-stu-id="bd989-124">The format for the Table service connection string is:</span></span>

<span data-ttu-id="bd989-125">Voor toegang tot een service voor live:</span><span class="sxs-lookup"><span data-stu-id="bd989-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="bd989-126">Voor toegang tot de emulator opslag:</span><span class="sxs-lookup"><span data-stu-id="bd989-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="bd989-127">Voor het maken van een Azure-service-client die u wilt gebruiken, de **ServicesBuilder** klasse.</span><span class="sxs-lookup"><span data-stu-id="bd989-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="bd989-128">U kunt:</span><span class="sxs-lookup"><span data-stu-id="bd989-128">You can:</span></span>

* <span data-ttu-id="bd989-129">de verbindingsreeks rechtstreeks aan deze doorgeven of</span><span class="sxs-lookup"><span data-stu-id="bd989-129">pass the connection string directly to it or</span></span>
* <span data-ttu-id="bd989-130">Gebruik de **CloudConfigurationManager (CCM)** om te controleren van meerdere externe bronnen voor de verbindingsreeks:</span><span class="sxs-lookup"><span data-stu-id="bd989-130">use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="bd989-131">Standaard wordt geleverd met ondersteuning voor een externe bron - omgevingsvariabelen</span><span class="sxs-lookup"><span data-stu-id="bd989-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="bd989-132">u kunt nieuwe bronnen toevoegen door het uitbreiden van de **ConnectionStringSource** klasse</span><span class="sxs-lookup"><span data-stu-id="bd989-132">you can add new sources by extending the **ConnectionStringSource** class</span></span>

<span data-ttu-id="bd989-133">Voor de voorbeelden die hier wordt beschreven, worden de verbindingsreeks rechtstreeks doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="bd989-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="bd989-134">Een tabel maken</span><span class="sxs-lookup"><span data-stu-id="bd989-134">Create a table</span></span>
<span data-ttu-id="bd989-135">Een **TableRestProxy** object kunt u bij het maken van een tabel met de **createTable** methode.</span><span class="sxs-lookup"><span data-stu-id="bd989-135">A **TableRestProxy** object lets you create a table with the **createTable** method.</span></span> <span data-ttu-id="bd989-136">Bij het maken van een tabel, kunt u de time-out voor de tabel-service instellen.</span><span class="sxs-lookup"><span data-stu-id="bd989-136">When creating a table, you can set the Table service timeout.</span></span> <span data-ttu-id="bd989-137">(Zie voor meer informatie over de time-out voor de tabel-service, [time-outs instellen voor tabel servicebewerkingen][table-service-timeouts].)</span><span class="sxs-lookup"><span data-stu-id="bd989-137">(For more information about the Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

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

<span data-ttu-id="bd989-138">Zie voor meer informatie over de beperkingen op tabelnamen [inzicht in de tabel Service Data Model][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="bd989-138">For information about restrictions on table names, see [Understanding the Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="bd989-139">Een entiteit toevoegen aan een tabel</span><span class="sxs-lookup"><span data-stu-id="bd989-139">Add an entity to a table</span></span>
<span data-ttu-id="bd989-140">Als u wilt een entiteit toevoegen aan een tabel, maakt u een nieuwe **entiteit** object en doorgegeven aan **TableRestProxy -> insertEntity**.</span><span class="sxs-lookup"><span data-stu-id="bd989-140">To add an entity to a table, create a new **Entity** object and pass it to **TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="bd989-141">Houd er rekening mee dat wanneer u een entiteit maakt, moet u een `PartitionKey` en `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="bd989-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="bd989-142">Dit zijn de unieke id's voor een entiteit en waarden die veel sneller dan andere entiteitseigenschappen kunnen worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="bd989-142">These are the unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="bd989-143">Gebruikt het systeem `PartitionKey` automatisch over veel opslagknooppunten verdelen van de tabel entiteiten.</span><span class="sxs-lookup"><span data-stu-id="bd989-143">The system uses `PartitionKey` to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="bd989-144">Entiteiten met dezelfde `PartitionKey` op hetzelfde knooppunt worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="bd989-144">Entities with the same `PartitionKey` are stored on the same node.</span></span> <span data-ttu-id="bd989-145">(Het uitvoeren van bewerkingen op meerdere entiteiten die zijn opgeslagen op hetzelfde knooppunt beter dan op entiteiten die zijn opgeslagen op verschillende knooppunten.) De `RowKey` is de unieke ID van een entiteit binnen een partitie.</span><span class="sxs-lookup"><span data-stu-id="bd989-145">(Operations on multiple entities stored on the same node perform better than on entities stored across different nodes.) The `RowKey` is the unique ID of an entity within a partition.</span></span>

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
$entity->addProperty("Description", null, "Take out the trash.");
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

<span data-ttu-id="bd989-146">Zie voor meer informatie over de eigenschappen van de tabel en typen [inzicht in de tabel Service Data Model][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="bd989-146">For information about Table properties and types, see [Understanding the Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="bd989-147">De **TableRestProxy** klasse biedt twee alternatieve methoden voor het invoegen van entiteiten: **insertOrMergeEntity** en **insertOrReplaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="bd989-147">The **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="bd989-148">Voor het gebruik van deze methoden, maak een nieuwe **entiteit** en doorgegeven als parameter aan een van de methoden.</span><span class="sxs-lookup"><span data-stu-id="bd989-148">To use these methods, create a new **Entity** and pass it as a parameter to either method.</span></span> <span data-ttu-id="bd989-149">Elke methode worden de entiteit ingevoegd als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="bd989-149">Each method will insert the entity if it does not exist.</span></span> <span data-ttu-id="bd989-150">Als de entiteit al bestaat, **insertOrMergeEntity** eigenschapswaarden bijgewerkt als de eigenschappen al bestaat en worden nieuwe eigenschappen toegevoegd als ze niet bestaan, terwijl **insertOrReplaceEntity** Hiermee vervangt u een bestaande entiteit.</span><span class="sxs-lookup"><span data-stu-id="bd989-150">If the entity already exists, **insertOrMergeEntity** updates property values if the properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="bd989-151">Het volgende voorbeeld ziet u hoe u **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="bd989-151">The following example shows how to use **insertOrMergeEntity**.</span></span> <span data-ttu-id="bd989-152">Als de entiteit met `PartitionKey` 'tasksSeattle' en `RowKey` '1' niet al bestaat, wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="bd989-152">If the entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="bd989-153">Echter, als deze eerder is ingevoegd (zoals weergegeven in het bovenstaande voorbeeld), de `DueDate` eigenschap wordt bijgewerkt, en de `Status` eigenschap wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="bd989-153">However, if it has previously been inserted (as shown in the example above), the `DueDate` property will be updated, and the `Status` property will be added.</span></span> <span data-ttu-id="bd989-154">De `Description` en `Location` eigenschappen ook worden bijgewerkt, maar met waarden die effectief blijven ongewijzigd.</span><span class="sxs-lookup"><span data-stu-id="bd989-154">The `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="bd989-155">Als deze laatste twee eigenschappen zijn niet toegevoegd, zoals in het voorbeeld, maar er waren aanwezig op de doelentiteit, blijft hun bestaande waarden ongewijzigd.</span><span class="sxs-lookup"><span data-stu-id="bd989-155">If these latter two properties were not added as shown in the example, but existed on the target entity, their existing values would remain unchanged.</span></span>

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
$entity->addProperty("Description", null, "Take out the trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified the DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace the entity with PartitionKey "tasksSeattle" and RowKey "1".
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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="bd989-156">Eén entiteit ophalen</span><span class="sxs-lookup"><span data-stu-id="bd989-156">Retrieve a single entity</span></span>
<span data-ttu-id="bd989-157">De **TableRestProxy -> getEntity** methode kunt u één entiteit ophalen door een query uitvoert voor de `PartitionKey` en `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="bd989-157">The **TableRestProxy->getEntity** method allows you to retrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="bd989-158">In het volgende voorbeeld wordt de partitiesleutel `tasksSeattle` en rijsleutel `1` worden doorgegeven aan de **getEntity** methode.</span><span class="sxs-lookup"><span data-stu-id="bd989-158">In the example below, the partition key `tasksSeattle` and row key `1` are passed to the **getEntity** method.</span></span>

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

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="bd989-159">Alle entiteiten in een partitie ophalen</span><span class="sxs-lookup"><span data-stu-id="bd989-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="bd989-160">Entiteit-query's worden gemaakt met behulp van filters (Zie voor meer informatie [opvragen van tabellen en entiteiten][filters]).</span><span class="sxs-lookup"><span data-stu-id="bd989-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="bd989-161">U haalt alle entiteiten in de partitie met het filter ' PartitionKey eq *partitienaam*'.</span><span class="sxs-lookup"><span data-stu-id="bd989-161">To retrieve all entities in partition, use the filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="bd989-162">Het volgende voorbeeld laat zien hoe voor het ophalen van alle entiteiten in de `tasksSeattle` partitie door een filter toe op de **queryEntities** methode.</span><span class="sxs-lookup"><span data-stu-id="bd989-162">The following example shows how to retrieve all entities in the `tasksSeattle` partition by passing a filter to the **queryEntities** method.</span></span>

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

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="bd989-163">Een subset van entiteiten in een partitie ophalen</span><span class="sxs-lookup"><span data-stu-id="bd989-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="bd989-164">Hetzelfde patroon gebruikt in het vorige voorbeeld kan worden gebruikt voor het ophalen van een subset van entiteiten in een partitie.</span><span class="sxs-lookup"><span data-stu-id="bd989-164">The same pattern used in the previous example can be used to retrieve any subset of entities in a partition.</span></span> <span data-ttu-id="bd989-165">De subset met u ophalen entiteiten worden bepaald door het filter dat u gebruikt (Zie voor meer informatie [opvragen van tabellen en entiteiten][filters]). Het volgende voorbeeld laat zien hoe een filter te gebruiken voor het ophalen van alle entiteiten met een specifieke `Location` en een `DueDate` kleiner is dan een opgegeven datum.</span><span class="sxs-lookup"><span data-stu-id="bd989-165">The subset of entities you retrieve are determined by the filter you use (for more information, see [Querying Tables and Entities][filters]).The following example shows how to use a filter to retrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

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

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="bd989-166">Ophalen van een subset van entiteitseigenschappen</span><span class="sxs-lookup"><span data-stu-id="bd989-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="bd989-167">Een query kunt een subset van entiteitseigenschappen ophalen.</span><span class="sxs-lookup"><span data-stu-id="bd989-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="bd989-168">Deze methode, aangeroepen *projectie*, verbruikt minder bandbreedte en kan de queryprestaties verbeteren, vooral bij grote entiteiten.</span><span class="sxs-lookup"><span data-stu-id="bd989-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="bd989-169">Als u een eigenschap worden opgehaald, geeft u de naam van de eigenschap in op de **Query -> addSelectField** methode.</span><span class="sxs-lookup"><span data-stu-id="bd989-169">To specify a property to be retrieved, pass the name of the property to the **Query->addSelectField** method.</span></span> <span data-ttu-id="bd989-170">U kunt deze methode niet meerdere keren aanroepen meer eigenschappen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="bd989-170">You can call this method multiple times to add more properties.</span></span> <span data-ttu-id="bd989-171">Na het uitvoeren van **TableRestProxy -> queryEntities**, de geretourneerde entiteiten hebben alleen de geselecteerde eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="bd989-171">After executing **TableRestProxy->queryEntities**, the returned entities will only have the selected properties.</span></span> <span data-ttu-id="bd989-172">(Als u een subset van de tabelentiteiten retourneren wilt, gebruikt u een filter zoals weergegeven in de bovenstaande query's.)</span><span class="sxs-lookup"><span data-stu-id="bd989-172">(If you want to return a subset of Table entities, use a filter as shown in the queries above.)</span></span>

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

// All entities in the table are returned, regardless of whether
// they have the Description field.
// To limit the results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a><span data-ttu-id="bd989-173">Bijwerken van een entiteit</span><span class="sxs-lookup"><span data-stu-id="bd989-173">Update an entity</span></span>
<span data-ttu-id="bd989-174">Een bestaande entiteit kan worden bijgewerkt met behulp van de **entiteit -> setProperty** en **entiteit -> addProperty** methoden op de entiteit en vervolgens aanroepen **TableRestProxy -> updateEntity**.</span><span class="sxs-lookup"><span data-stu-id="bd989-174">An existing entity can be updated by using the **Entity->setProperty** and **Entity->addProperty** methods on the entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="bd989-175">Het volgende voorbeeld worden opgehaald van een entiteit, één eigenschap wijzigt, verwijdert u een andere eigenschap en wordt een nieuwe eigenschap toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="bd989-175">The following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="bd989-176">Houd er rekening mee dat u een eigenschap verwijderen kunt door de waarde instellen op **null**.</span><span class="sxs-lookup"><span data-stu-id="bd989-176">Note that you can remove a property by setting its value to **null**.</span></span>

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

## <a name="delete-an-entity"></a><span data-ttu-id="bd989-177">Een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="bd989-177">Delete an entity</span></span>
<span data-ttu-id="bd989-178">Als u wilt een entiteit wilt verwijderen, geeft u de tabelnaam en de entiteit `PartitionKey` en `RowKey` naar de **TableRestProxy -> deleteEntity** methode.</span><span class="sxs-lookup"><span data-stu-id="bd989-178">To delete an entity, pass the table name, and the entity's `PartitionKey` and `RowKey` to the **TableRestProxy->deleteEntity** method.</span></span>

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

<span data-ttu-id="bd989-179">Houd er rekening mee dat voor controles gelijktijdigheid van taken, u de Etag voor een entiteit instellen kunt moet worden verwijderd met behulp van de **DeleteEntityOptions -> setEtag** methode en geven de **DeleteEntityOptions** object naar de **deleteEntity** als een vierde parameter.</span><span class="sxs-lookup"><span data-stu-id="bd989-179">Note that for concurrency checks, you can set the Etag for an entity to be deleted by using the **DeleteEntityOptions->setEtag** method and passing the **DeleteEntityOptions** object to **deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="bd989-180">Batchbewerkingen tabel</span><span class="sxs-lookup"><span data-stu-id="bd989-180">Batch table operations</span></span>
<span data-ttu-id="bd989-181">De **TableRestProxy -> batch** methode kunt u meerdere bewerkingen uitvoeren in een enkele aanvraag.</span><span class="sxs-lookup"><span data-stu-id="bd989-181">The **TableRestProxy->batch** method allows you to execute multiple operations in a single request.</span></span> <span data-ttu-id="bd989-182">Het patroon hier omvat het toevoegen van bewerkingen voor **BatchRequest** object en vervolgens doorgegeven de **BatchRequest** object toe aan de **TableRestProxy -> batch** methode.</span><span class="sxs-lookup"><span data-stu-id="bd989-182">The pattern here involves adding operations to **BatchRequest** object and then passing the **BatchRequest** object to the **TableRestProxy->batch** method.</span></span> <span data-ttu-id="bd989-183">Toevoegen van een bewerking voor een **BatchRequest** object, u een van de volgende methoden kunt aanroepen, kunt u meerdere keren:</span><span class="sxs-lookup"><span data-stu-id="bd989-183">To add an operation to a **BatchRequest** object, you can call any of the following methods multiple times:</span></span>

* <span data-ttu-id="bd989-184">**addInsertEntity** (toevoegen van een bewerking insertEntity)</span><span class="sxs-lookup"><span data-stu-id="bd989-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="bd989-185">**addUpdateEntity** (toevoegen van een bewerking updateEntity)</span><span class="sxs-lookup"><span data-stu-id="bd989-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="bd989-186">**addMergeEntity** (toevoegen van een bewerking mergeEntity)</span><span class="sxs-lookup"><span data-stu-id="bd989-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="bd989-187">**addInsertOrReplaceEntity** (toevoegen van een bewerking insertOrReplaceEntity)</span><span class="sxs-lookup"><span data-stu-id="bd989-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="bd989-188">**addInsertOrMergeEntity** (toevoegen van een bewerking insertOrMergeEntity)</span><span class="sxs-lookup"><span data-stu-id="bd989-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="bd989-189">**addDeleteEntity** (toevoegen van een bewerking deleteEntity)</span><span class="sxs-lookup"><span data-stu-id="bd989-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="bd989-190">Het volgende voorbeeld ziet u het uitvoeren van **insertEntity** en **deleteEntity** bewerkingen in een afzonderlijke aanvraag:</span><span class="sxs-lookup"><span data-stu-id="bd989-190">The following example shows how to execute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

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

// Add operation to list of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation to list of batch operations.
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

<span data-ttu-id="bd989-191">Zie voor meer informatie over batchverwerking tabelbewerkingen [uitvoeren entiteit groepstransacties][entity-group-transactions].</span><span class="sxs-lookup"><span data-stu-id="bd989-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="bd989-192">Een tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="bd989-192">Delete a table</span></span>
<span data-ttu-id="bd989-193">Ten slotte voor het verwijderen van een tabel, geeft de naam van de tabel aan de **TableRestProxy -> deleteTable** methode.</span><span class="sxs-lookup"><span data-stu-id="bd989-193">Finally, to delete a table, pass the table name to the **TableRestProxy->deleteTable** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bd989-194">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bd989-194">Next steps</span></span>
<span data-ttu-id="bd989-195">Nu dat u de basisprincipes van de Azure Table-service hebt geleerd, volgt u deze koppelingen voor meer informatie over complexere opslagtaken.</span><span class="sxs-lookup"><span data-stu-id="bd989-195">Now that you've learned the basics of the Azure Table service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="bd989-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u visueel met Azure Storage-gegevens kunt werken in Windows, macOS en Linux.</span><span class="sxs-lookup"><span data-stu-id="bd989-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="bd989-197">[PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="bd989-197">[PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
