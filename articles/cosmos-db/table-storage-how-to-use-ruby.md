---
title: Hoe Azure Table Storage gebruiken met Ruby | Microsoft Docs
description: Sla gestructureerde gegevens op in de cloud met Azure Table Storage, een oplossing voor NoSQL-gegevensopslag.
services: cosmos-db
documentationcenter: ruby
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 372bc89f75ad4730f0defbf9d6f9f041ae5ce1bf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-from-ruby"></a><span data-ttu-id="3841d-103">Hoe Azure Table Storage gebruiken met Ruby</span><span class="sxs-lookup"><span data-stu-id="3841d-103">How to use Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="3841d-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="3841d-104">Overview</span></span>
<span data-ttu-id="3841d-105">Deze handleiding wordt beschreven hoe u veelvoorkomende scenario's met de service Azure Table uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3841d-105">This guide shows you how to perform common scenarios using the Azure Table service.</span></span> <span data-ttu-id="3841d-106">De voorbeelden zijn geschreven met behulp van de Ruby-API.</span><span class="sxs-lookup"><span data-stu-id="3841d-106">The samples are written using the Ruby API.</span></span> <span data-ttu-id="3841d-107">De scenario's worden behandeld: **maken en verwijderen van een tabel, invoegen en het uitvoeren van query's entiteiten in een tabel**.</span><span class="sxs-lookup"><span data-stu-id="3841d-107">The scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="3841d-108">Een Ruby-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="3841d-108">Create a Ruby application</span></span>
<span data-ttu-id="3841d-109">Voor instructies hoe een Ruby-toepassing maken, Zie [Ruby op Rails webtoepassing op een virtuele machine van Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="3841d-109">For instructions how to create a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="3841d-110">Uw toepassing configureren voor toegang tot opslag</span><span class="sxs-lookup"><span data-stu-id="3841d-110">Configure your application to access Storage</span></span>
<span data-ttu-id="3841d-111">Voor het gebruik van Azure Storage, die u wilt downloaden en gebruiken van het Ruby azure-pakket met een set van gemak bibliotheken die met de REST van de Storage-services communiceren.</span><span class="sxs-lookup"><span data-stu-id="3841d-111">To use Azure Storage, you need to download and use the Ruby azure package which includes a set of convenience libraries that communicate with the Storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="3841d-112">RubyGems gebruiken om het pakket te verkrijgen</span><span class="sxs-lookup"><span data-stu-id="3841d-112">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="3841d-113">Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="3841d-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="3841d-114">Type **gem installeren azure** in het opdrachtvenster voor het installeren van de gem en afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="3841d-114">Type **gem install azure** in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="3841d-115">Het pakket importeren</span><span class="sxs-lookup"><span data-stu-id="3841d-115">Import the package</span></span>
<span data-ttu-id="3841d-116">Uw favoriete teksteditor gebruiken, Voeg het volgende toe aan het begin van de Ruby bestand waarop u wilt opslag gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3841d-116">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="3841d-117">Een Azure Storage-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="3841d-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="3841d-118">De azure-module leest de omgevingsvariabelen **AZURE\_opslag\_ACCOUNT** en **AZURE\_opslag\_toegang\_sleutel** voor de benodigde informatie om te verbinden met uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="3841d-118">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required to connect to your Azure Storage account.</span></span> <span data-ttu-id="3841d-119">Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens voordat u **Azure::TableService** met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="3841d-119">If these environment variables are not set, you must specify the account information before using **Azure::TableService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="3841d-120">Als u deze waarden van een klassiek of Resource Manager-opslagaccount in de Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="3841d-120">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="3841d-121">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3841d-121">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3841d-122">Ga naar het opslagaccount dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3841d-122">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="3841d-123">Klik op de blade instellingen aan de rechterkant **toegangstoetsen**.</span><span class="sxs-lookup"><span data-stu-id="3841d-123">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="3841d-124">In de blade van de toegang tot sleutels die wordt weergegeven, ziet u de toegangssleutel 1 en toegangssleutel 2.</span><span class="sxs-lookup"><span data-stu-id="3841d-124">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="3841d-125">U kunt een van beide gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3841d-125">You can use either of these.</span></span>
5. <span data-ttu-id="3841d-126">Klik op het pictogram kopiëren om de sleutel naar het Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="3841d-126">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="3841d-127">Een tabel maken</span><span class="sxs-lookup"><span data-stu-id="3841d-127">Create a table</span></span>
<span data-ttu-id="3841d-128">De **Azure::TableService** object kunt u samenwerken met tabellen en entiteiten.</span><span class="sxs-lookup"><span data-stu-id="3841d-128">The **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="3841d-129">Een tabel te maken, gebruikt u de **maken\_table()** methode.</span><span class="sxs-lookup"><span data-stu-id="3841d-129">To create a table, use the **create\_table()** method.</span></span> <span data-ttu-id="3841d-130">Het volgende voorbeeld maakt een tabel of de fout wordt afgedrukt indien deze aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="3841d-130">The following example creates a table or prints the error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="3841d-131">Een entiteit toevoegen aan een tabel</span><span class="sxs-lookup"><span data-stu-id="3841d-131">Add an entity to a table</span></span>
<span data-ttu-id="3841d-132">Als u wilt een entiteit toevoegen, moet u eerst een hash-object dat de entiteitseigenschappen van uw definieert maken.</span><span class="sxs-lookup"><span data-stu-id="3841d-132">To add an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="3841d-133">Houd er rekening mee dat voor elke entiteit moet u een **PartitionKey** en **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="3841d-133">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="3841d-134">Dit zijn de unieke id's van de entiteiten en waarden die veel sneller dan de andere eigenschappen kunnen worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="3841d-134">These are the unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="3841d-135">Azure Storage maakt gebruik van **PartitionKey** automatisch over veel opslagknooppunten verdelen van de tabel entiteiten.</span><span class="sxs-lookup"><span data-stu-id="3841d-135">Azure Storage uses **PartitionKey** to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="3841d-136">Entiteiten met dezelfde **PartitionKey** op hetzelfde knooppunt worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3841d-136">Entities with the same **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="3841d-137">De **RowKey** is de unieke ID van de entiteit in de partitie hoort bij.</span><span class="sxs-lookup"><span data-stu-id="3841d-137">The **RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="3841d-138">Bijwerken van een entiteit</span><span class="sxs-lookup"><span data-stu-id="3841d-138">Update an entity</span></span>
<span data-ttu-id="3841d-139">Er zijn meerdere methoden beschikbaar voor het bijwerken van een bestaande entiteit:</span><span class="sxs-lookup"><span data-stu-id="3841d-139">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="3841d-140">**bijwerken\_entity():** bijwerken van een bestaande entiteit door deze te vervangen.</span><span class="sxs-lookup"><span data-stu-id="3841d-140">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="3841d-141">**samenvoegen\_entity():** Updates van een bestaande entiteit door nieuwe eigenschapswaarden in de bestaande entiteit samen te voegen.</span><span class="sxs-lookup"><span data-stu-id="3841d-141">**merge\_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span>
* <span data-ttu-id="3841d-142">**invoegen\_of\_samenvoegen\_entity():** Updates van een bestaande entiteit door deze te vervangen.</span><span class="sxs-lookup"><span data-stu-id="3841d-142">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="3841d-143">Als er is geen entiteit bestaat, wordt er een nieuwe ingevoegd:</span><span class="sxs-lookup"><span data-stu-id="3841d-143">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="3841d-144">**invoegen\_of\_vervangen\_entity():** Updates van een bestaande entiteit door nieuwe eigenschapswaarden in de bestaande entiteit samen te voegen.</span><span class="sxs-lookup"><span data-stu-id="3841d-144">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span> <span data-ttu-id="3841d-145">Als er is geen entiteit bestaat, wordt er een nieuwe ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="3841d-145">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="3841d-146">Het volgende voorbeeld toont het bijwerken van een entiteit met **bijwerken\_entity()**:</span><span class="sxs-lookup"><span data-stu-id="3841d-146">The following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="3841d-147">Met **bijwerken\_entity()** en **samenvoegen\_entity()**, als de entiteit die u wilt bijwerken, mislukt de update-bewerking niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="3841d-147">With **update\_entity()** and **merge\_entity()**, if the entity that you are updating doesn't exist then the update operation will fail.</span></span> <span data-ttu-id="3841d-148">Dus als u opslaan van een entiteit wilt ongeacht of deze al bestaat, moet u in plaats daarvan gebruiken **invoegen\_of\_vervangen\_entity()** of **invoegen\_of\_samenvoegen\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="3841d-148">Therefore if you wish to store an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="3841d-149">Werken met groepen van entiteiten</span><span class="sxs-lookup"><span data-stu-id="3841d-149">Work with groups of entities</span></span>
<span data-ttu-id="3841d-150">Soms is het zinvol verzenden meerdere bewerkingen samen in een batch om ervoor te zorgen atomic verwerking door de server.</span><span class="sxs-lookup"><span data-stu-id="3841d-150">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="3841d-151">Om te realiseren dat, maakt u eerst een **Batch** object en gebruik vervolgens de **uitvoeren\_batch()** methode op **TableService**.</span><span class="sxs-lookup"><span data-stu-id="3841d-151">To accomplish that, you first create a **Batch** object and then use the **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="3841d-152">Het volgende voorbeeld ziet twee entiteiten met RowKey 2 en 3 in een batch te verzenden.</span><span class="sxs-lookup"><span data-stu-id="3841d-152">The following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="3841d-153">U ziet dat deze functie alleen voor entiteiten met de dezelfde PartitionKey werkt.</span><span class="sxs-lookup"><span data-stu-id="3841d-153">Notice that it only works for entities with the same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="3841d-154">Query voor een entiteit</span><span class="sxs-lookup"><span data-stu-id="3841d-154">Query for an entity</span></span>
<span data-ttu-id="3841d-155">Om te vragen een entiteit in een tabel, gebruikt u de **ophalen\_entity()** methode door de naam van de tabel **PartitionKey** en **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="3841d-155">To query an entity in a table, use the **get\_entity()** method, by passing the table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="3841d-156">Query uitvoeren op een verzameling entiteiten</span><span class="sxs-lookup"><span data-stu-id="3841d-156">Query a set of entities</span></span>
<span data-ttu-id="3841d-157">Om te vragen een set van entiteiten in een tabel, een query-hash-object maken en gebruiken de **query\_entities()** methode.</span><span class="sxs-lookup"><span data-stu-id="3841d-157">To query a set of entities in a table, create a query hash object and use the **query\_entities()** method.</span></span> <span data-ttu-id="3841d-158">Het volgende voorbeeld toont ophalen van de entiteiten met dezelfde **PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="3841d-158">The following example demonstrates getting all the entities with the same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="3841d-159">Als het resultaat is te groot voor één query op om te retourneren, een vervolgtoken wordt geretourneerd dat u kunt gebruiken voor het ophalen van de volgende pagina's.</span><span class="sxs-lookup"><span data-stu-id="3841d-159">If the result set is too large for a single query to return, a continuation token will be returned which you can use to retrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="3841d-160">Een query uitvoeren op een subset van entiteitseigenschappen</span><span class="sxs-lookup"><span data-stu-id="3841d-160">Query a subset of entity properties</span></span>
<span data-ttu-id="3841d-161">Een query naar een tabel ophalen slechts enkele eigenschappen van een entiteit.</span><span class="sxs-lookup"><span data-stu-id="3841d-161">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="3841d-162">Deze techniek, 'projectie' genoemd, verbruikt minder bandbreedte en kan de queryprestaties verbeteren, vooral bij grote entiteiten.</span><span class="sxs-lookup"><span data-stu-id="3841d-162">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="3841d-163">Gebruik de component select en geeft de namen van de eigenschappen die u wilt worden overgebracht naar de client.</span><span class="sxs-lookup"><span data-stu-id="3841d-163">Use the select clause and pass the names of the properties you would like to bring over to the client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="3841d-164">Een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="3841d-164">Delete an entity</span></span>
<span data-ttu-id="3841d-165">U een entiteit verwijderen met de **verwijderen\_entity()** methode.</span><span class="sxs-lookup"><span data-stu-id="3841d-165">To delete an entity, use the **delete\_entity()** method.</span></span> <span data-ttu-id="3841d-166">U moet doorgeven in de naam van de tabel die de entiteit, de PartitionKey en RowKey van de entiteit bevat.</span><span class="sxs-lookup"><span data-stu-id="3841d-166">You need to pass in the name of the table which contains the entity, the PartitionKey and RowKey of the entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="3841d-167">Een tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="3841d-167">Delete a table</span></span>
<span data-ttu-id="3841d-168">Als u wilt verwijderen van een tabel, gebruikt u de **verwijderen\_table()** methode aan en geeft u op de naam van de tabel die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="3841d-168">To delete a table, use the **delete\_table()** method and pass in the name of the table you want to delete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="3841d-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3841d-169">Next steps</span></span>

* <span data-ttu-id="3841d-170">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u visueel met Azure Storage-gegevens kunt werken in Windows, macOS en Linux.</span><span class="sxs-lookup"><span data-stu-id="3841d-170">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="3841d-171">[Azure SDK voor Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) opslagplaats op GitHub</span><span class="sxs-lookup"><span data-stu-id="3841d-171">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

