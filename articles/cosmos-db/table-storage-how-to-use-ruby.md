---
title: aaaHow toouse Azure Table Storage met Ruby | Microsoft Docs
description: Gestructureerde gegevens opslaan in Hallo cloud met Azure Table storage, een NoSQL-gegevensarchief.
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
ms.openlocfilehash: 2f9eb5a9160b551d6d1d198869787070c402b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a><span data-ttu-id="7d29e-103">Hoe toouse Azure Table Storage met Ruby</span><span class="sxs-lookup"><span data-stu-id="7d29e-103">How toouse Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="7d29e-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7d29e-104">Overview</span></span>
<span data-ttu-id="7d29e-105">Deze handleiding wordt getoond hoe tooperform algemene scenario's met behulp van hello Azure Table-service.</span><span class="sxs-lookup"><span data-stu-id="7d29e-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="7d29e-106">Hallo-voorbeelden zijn geschreven met behulp van Hallo Ruby-API.</span><span class="sxs-lookup"><span data-stu-id="7d29e-106">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="7d29e-107">Hallo scenario's worden behandeld: **maken en verwijderen van een tabel, invoegen en het uitvoeren van query's entiteiten in een tabel**.</span><span class="sxs-lookup"><span data-stu-id="7d29e-107">hello scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="7d29e-108">Een Ruby-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="7d29e-108">Create a Ruby application</span></span>
<span data-ttu-id="7d29e-109">Zie voor instructies hoe toocreate een Ruby toepassing [Ruby op Rails webtoepassing op een virtuele machine van Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="7d29e-109">For instructions how toocreate a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="7d29e-110">Uw toepassing tooaccess opslag configureren</span><span class="sxs-lookup"><span data-stu-id="7d29e-110">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="7d29e-111">toouse Azure Storage, moet u toodownload en gebruik Hallo Ruby azure-pakket dat bevat een set met gemak bibliotheken die met Hallo Storage REST-services communiceren.</span><span class="sxs-lookup"><span data-stu-id="7d29e-111">toouse Azure Storage, you need toodownload and use hello Ruby azure package which includes a set of convenience libraries that communicate with hello Storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="7d29e-112">RubyGems tooobtain Hallo pakket gebruiken</span><span class="sxs-lookup"><span data-stu-id="7d29e-112">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="7d29e-113">Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="7d29e-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="7d29e-114">Type **gem installeren azure** in Hallo opdracht venster tooinstall Hallo gem en afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="7d29e-114">Type **gem install azure** in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="7d29e-115">Hallo-pakket importeren</span><span class="sxs-lookup"><span data-stu-id="7d29e-115">Import hello package</span></span>
<span data-ttu-id="7d29e-116">Uw favoriete teksteditor gebruiken, voegt Hallo toohello bovenaan Hallo Ruby bestand waarin u van plan toouse opslag bent te volgen:</span><span class="sxs-lookup"><span data-stu-id="7d29e-116">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="7d29e-117">Een Azure Storage-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="7d29e-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="7d29e-118">Hello azure-module lezen Hallo omgevingsvariabelen **AZURE\_opslag\_ACCOUNT** en **AZURE\_opslag\_toegang\_sleutel**vereist tooconnect tooyour Azure Storage-account voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7d29e-118">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required tooconnect tooyour Azure Storage account.</span></span> <span data-ttu-id="7d29e-119">Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens Hallo voordat u **Azure::TableService** Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="7d29e-119">If these environment variables are not set, you must specify hello account information before using **Azure::TableService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="7d29e-120">tooobtain deze waarden van een klassiek of Resource Manager-storage-account in hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="7d29e-120">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="7d29e-121">Meld u bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7d29e-121">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7d29e-122">Navigeer toohello gewenste toouse storage-account.</span><span class="sxs-lookup"><span data-stu-id="7d29e-122">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="7d29e-123">Klik op Hallo instellingenblade op Hallo rechts **toegangstoetsen**.</span><span class="sxs-lookup"><span data-stu-id="7d29e-123">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="7d29e-124">Hallo toegang sleutels blade die wordt weergegeven, ziet u Hallo toegangssleutel 1 en toegangssleutel 2.</span><span class="sxs-lookup"><span data-stu-id="7d29e-124">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="7d29e-125">U kunt een van beide gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7d29e-125">You can use either of these.</span></span>
5. <span data-ttu-id="7d29e-126">Klik op Hallo kopiëren pictogram toocopy Hallo sleutel toohello Klembord.</span><span class="sxs-lookup"><span data-stu-id="7d29e-126">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="7d29e-127">Een tabel maken</span><span class="sxs-lookup"><span data-stu-id="7d29e-127">Create a table</span></span>
<span data-ttu-id="7d29e-128">Hallo **Azure::TableService** object kunt u samenwerken met tabellen en entiteiten.</span><span class="sxs-lookup"><span data-stu-id="7d29e-128">hello **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="7d29e-129">een tabel toocreate gebruiken Hallo **maken\_table()** methode.</span><span class="sxs-lookup"><span data-stu-id="7d29e-129">toocreate a table, use hello **create\_table()** method.</span></span> <span data-ttu-id="7d29e-130">Hallo volgende voorbeeld wordt een tabel of afdrukken bestellen Hallo fout indien deze aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="7d29e-130">hello following example creates a table or prints hello error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="7d29e-131">Een entiteit tooa tabel toevoegen</span><span class="sxs-lookup"><span data-stu-id="7d29e-131">Add an entity tooa table</span></span>
<span data-ttu-id="7d29e-132">een entiteit tooadd eerst een hash-object dat de entiteitseigenschappen van uw definieert maken.</span><span class="sxs-lookup"><span data-stu-id="7d29e-132">tooadd an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="7d29e-133">Houd er rekening mee dat voor elke entiteit moet u een **PartitionKey** en **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="7d29e-133">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="7d29e-134">Dit Hallo unieke id's van de entiteiten en zijn waarden die veel sneller dan de andere eigenschappen kunnen worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="7d29e-134">These are hello unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="7d29e-135">Azure Storage maakt gebruik van **PartitionKey** tooautomatically hello tabelentiteiten distribueren via veel opslagknooppunten.</span><span class="sxs-lookup"><span data-stu-id="7d29e-135">Azure Storage uses **PartitionKey** tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="7d29e-136">Entiteiten met dezelfde Hallo **PartitionKey** zijn opgeslagen op Hallo hetzelfde knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7d29e-136">Entities with hello same **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="7d29e-137">Hallo **RowKey** is de unieke ID Hallo van Hallo entiteit binnen deze tot behoort Hallo-partitie.</span><span class="sxs-lookup"><span data-stu-id="7d29e-137">hello **RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="7d29e-138">Bijwerken van een entiteit</span><span class="sxs-lookup"><span data-stu-id="7d29e-138">Update an entity</span></span>
<span data-ttu-id="7d29e-139">Er zijn meerdere methoden beschikbaar tooupdate van een bestaande entiteit:</span><span class="sxs-lookup"><span data-stu-id="7d29e-139">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="7d29e-140">**bijwerken\_entity():** bijwerken van een bestaande entiteit door deze te vervangen.</span><span class="sxs-lookup"><span data-stu-id="7d29e-140">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="7d29e-141">**samenvoegen\_entity():** Updates van een bestaande entiteit door de nieuwe eigenschapswaarden samenvoegen in een bestaande Hallo-entiteit.</span><span class="sxs-lookup"><span data-stu-id="7d29e-141">**merge\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span>
* <span data-ttu-id="7d29e-142">**invoegen\_of\_samenvoegen\_entity():** Updates van een bestaande entiteit door deze te vervangen.</span><span class="sxs-lookup"><span data-stu-id="7d29e-142">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="7d29e-143">Als er is geen entiteit bestaat, wordt er een nieuwe ingevoegd:</span><span class="sxs-lookup"><span data-stu-id="7d29e-143">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="7d29e-144">**invoegen\_of\_vervangen\_entity():** Updates van een bestaande entiteit door de nieuwe eigenschapswaarden samenvoegen in een bestaande Hallo-entiteit.</span><span class="sxs-lookup"><span data-stu-id="7d29e-144">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span> <span data-ttu-id="7d29e-145">Als er is geen entiteit bestaat, wordt er een nieuwe ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="7d29e-145">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="7d29e-146">Hallo volgende voorbeeld ziet u het bijwerken van een entiteit met **bijwerken\_entity()**:</span><span class="sxs-lookup"><span data-stu-id="7d29e-146">hello following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="7d29e-147">Met **bijwerken\_entity()** en **samenvoegen\_entity()**als Hallo-entiteit die u wilt bijwerken, mislukt de updatebewerking Hallo bestaat niet.</span><span class="sxs-lookup"><span data-stu-id="7d29e-147">With **update\_entity()** and **merge\_entity()**, if hello entity that you are updating doesn't exist then hello update operation will fail.</span></span> <span data-ttu-id="7d29e-148">Dus als u wenst dat toostore een entiteit ongeacht of deze al bestaat, moet u in plaats daarvan gebruiken **invoegen\_of\_vervangen\_entity()** of **invoegen\_of \_samenvoegen\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="7d29e-148">Therefore if you wish toostore an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="7d29e-149">Werken met groepen van entiteiten</span><span class="sxs-lookup"><span data-stu-id="7d29e-149">Work with groups of entities</span></span>
<span data-ttu-id="7d29e-150">Soms is het zin toosubmit meerdere bewerkingen samen in een batch-tooensure atomic verwerken door Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="7d29e-150">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="7d29e-151">tooaccomplish dat, u eerst maakt een **Batch** object en gebruik vervolgens Hallo **uitvoeren\_batch()** methode op **TableService**.</span><span class="sxs-lookup"><span data-stu-id="7d29e-151">tooaccomplish that, you first create a **Batch** object and then use hello **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="7d29e-152">Hallo volgende voorbeeld ziet u twee entiteiten met RowKey 2 en 3 in een batch te verzenden.</span><span class="sxs-lookup"><span data-stu-id="7d29e-152">hello following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="7d29e-153">U ziet dat deze alleen werkt voor entiteiten met dezelfde PartitionKey Hallo.</span><span class="sxs-lookup"><span data-stu-id="7d29e-153">Notice that it only works for entities with hello same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="7d29e-154">Query voor een entiteit</span><span class="sxs-lookup"><span data-stu-id="7d29e-154">Query for an entity</span></span>
<span data-ttu-id="7d29e-155">een entiteit in een tabel, gebruik Hallo tooquery **ophalen\_entity()** methode door Hallo tabelnaam **PartitionKey** en **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="7d29e-155">tooquery an entity in a table, use hello **get\_entity()** method, by passing hello table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="7d29e-156">Query uitvoeren op een verzameling entiteiten</span><span class="sxs-lookup"><span data-stu-id="7d29e-156">Query a set of entities</span></span>
<span data-ttu-id="7d29e-157">tooquery een set van entiteiten in een tabel, een query-hash-object maken en gebruiken van Hallo **query\_entities()** methode.</span><span class="sxs-lookup"><span data-stu-id="7d29e-157">tooquery a set of entities in a table, create a query hash object and use hello **query\_entities()** method.</span></span> <span data-ttu-id="7d29e-158">Hallo volgende voorbeeld ziet u alle Hallo entiteiten Hello aan dezelfde **PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="7d29e-158">hello following example demonstrates getting all hello entities with hello same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="7d29e-159">Als de resultaatset Hallo is te groot voor een enkele query tooreturn, een vervolgtoken geretourneerd waarin u kunt de volgende pagina's tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="7d29e-159">If hello result set is too large for a single query tooreturn, a continuation token will be returned which you can use tooretrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="7d29e-160">Een query uitvoeren op een subset van entiteitseigenschappen</span><span class="sxs-lookup"><span data-stu-id="7d29e-160">Query a subset of entity properties</span></span>
<span data-ttu-id="7d29e-161">Een query tooa tabel ophalen slechts enkele eigenschappen van een entiteit.</span><span class="sxs-lookup"><span data-stu-id="7d29e-161">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="7d29e-162">Deze techniek, 'projectie' genoemd, verbruikt minder bandbreedte en kan de queryprestaties verbeteren, vooral bij grote entiteiten.</span><span class="sxs-lookup"><span data-stu-id="7d29e-162">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="7d29e-163">Gebruik Hallo select-component en pass Hallo namen van Hallo eigenschappen die u wilt toobring via toohello client.</span><span class="sxs-lookup"><span data-stu-id="7d29e-163">Use hello select clause and pass hello names of hello properties you would like toobring over toohello client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="7d29e-164">Een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="7d29e-164">Delete an entity</span></span>
<span data-ttu-id="7d29e-165">een entiteit toodelete gebruiken Hallo **verwijderen\_entity()** methode.</span><span class="sxs-lookup"><span data-stu-id="7d29e-165">toodelete an entity, use hello **delete\_entity()** method.</span></span> <span data-ttu-id="7d29e-166">U moet toopass in Hallo-naam van tabel Hallo Hallo entiteit, Hallo PartitionKey en RowKey van Hallo entiteit bevat.</span><span class="sxs-lookup"><span data-stu-id="7d29e-166">You need toopass in hello name of hello table which contains hello entity, hello PartitionKey and RowKey of hello entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="7d29e-167">Een tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="7d29e-167">Delete a table</span></span>
<span data-ttu-id="7d29e-168">een tabel toodelete gebruiken Hallo **verwijderen\_table()** methode en geeft u de naam Hallo van Hallo gewenste toodelete tabel.</span><span class="sxs-lookup"><span data-stu-id="7d29e-168">toodelete a table, use hello **delete\_table()** method and pass in hello name of hello table you want toodelete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="7d29e-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7d29e-169">Next steps</span></span>

* <span data-ttu-id="7d29e-170">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u toowork visueel met Azure Storage-gegevens op Windows-, Mac OS- en Linux.</span><span class="sxs-lookup"><span data-stu-id="7d29e-170">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="7d29e-171">[Azure SDK voor Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) opslagplaats op GitHub</span><span class="sxs-lookup"><span data-stu-id="7d29e-171">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

