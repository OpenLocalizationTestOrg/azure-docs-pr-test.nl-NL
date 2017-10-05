---
title: Het gebruik van Table storage (C++) | Microsoft Docs
description: Sla gestructureerde gegevens op in de cloud met Azure Table Storage, een oplossing voor NoSQL-gegevensopslag.
services: storage
documentationcenter: .net
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: d68843153921c72f6e808f62e82d3686c7e2f160
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-from-c"></a><span data-ttu-id="e8701-103">Hoe Table storage gebruiken met C++</span><span class="sxs-lookup"><span data-stu-id="e8701-103">How to use Table storage from C++</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="e8701-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="e8701-104">Overview</span></span>
<span data-ttu-id="e8701-105">Deze handleiding wordt beschreven hoe u veelvoorkomende scenario's uitvoeren met behulp van de service Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="e8701-105">This guide will show you how to perform common scenarios by using the Azure Table storage service.</span></span> <span data-ttu-id="e8701-106">De voorbeelden zijn geschreven in C++ en gebruik de [Azure Storage-clientbibliotheek voor C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="e8701-106">The samples are written in C++ and use the [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="e8701-107">De scenario's worden behandeld: **maken en het verwijderen van een tabel** en **werken met tabelentiteiten**.</span><span class="sxs-lookup"><span data-stu-id="e8701-107">The scenarios covered include **creating and deleting a table** and **working with table entities**.</span></span>

> [!NOTE]
> <span data-ttu-id="e8701-108">Deze handleiding is bedoeld voor de Azure Storage-clientbibliotheek voor C++ versie 1.0.0 en hoger.</span><span class="sxs-lookup"><span data-stu-id="e8701-108">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="e8701-109">De aanbevolen versie is Storage-clientbibliotheek 2.2.0, die beschikbaar is via [NuGet](http://www.nuget.org/packages/wastorage) of [GitHub](https://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="e8701-109">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="e8701-110">Een C++-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="e8701-110">Create a C++ application</span></span>
<span data-ttu-id="e8701-111">In deze handleiding gebruikt u opslagfuncties dat kunnen worden uitgevoerd binnen een C++-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e8701-111">In this guide, you will use storage features that can be run within a C++ application.</span></span> <span data-ttu-id="e8701-112">Om dit te doen, moet u voor het installeren van de Azure Storage-clientbibliotheek voor C++ en een Azure storage-account maken in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e8701-112">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>  

<span data-ttu-id="e8701-113">Voor het installeren van de Azure Storage-clientbibliotheek voor C++, kunt u de volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="e8701-113">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="e8701-114">**Linux:** Volg de instructies op de [Azure Storage-clientbibliotheek voor C++ Leesmij](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="e8701-114">**Linux:** Follow the instructions given on the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="e8701-115">**Windows:** In Visual Studio, klikt u op **Extra > NuGet Package Manager > Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="e8701-115">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="e8701-116">Typ de volgende opdracht in de [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="e8701-116">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span></span>  
  
     <span data-ttu-id="e8701-117">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="e8701-117">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-table-storage"></a><span data-ttu-id="e8701-118">Uw toepassing configureren voor toegang tot Table storage</span><span class="sxs-lookup"><span data-stu-id="e8701-118">Configure your application to access Table storage</span></span>
<span data-ttu-id="e8701-119">Toevoegen aan dat de volgende instructies op de bovenkant van het bestand C++ is waar u de Azure storage-API's gebruiken voor toegang tot tabellen bevatten:</span><span class="sxs-lookup"><span data-stu-id="e8701-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access tables:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="e8701-120">Een Azure-opslag-verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="e8701-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="e8701-121">Een Azure-opslag-client gebruikt een verbindingsreeks voor opslag voor het opslaan van eindpunten en referenties voor toegang tot gegevens beheerservices.</span><span class="sxs-lookup"><span data-stu-id="e8701-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="e8701-122">Wanneer een client-toepassing wordt uitgevoerd, moet u de verbindingsreeks voor opslag in de volgende indeling opgeven.</span><span class="sxs-lookup"><span data-stu-id="e8701-122">When running a client application, you must provide the storage connection string in the following format.</span></span> <span data-ttu-id="e8701-123">De naam van uw opslagaccount en de toegangssleutel voor opslag gebruiken voor het opslagaccount wordt vermeld in de [Azure Portal](https://portal.azure.com) voor de *AccountName* en *AccountKey* waarden.</span><span class="sxs-lookup"><span data-stu-id="e8701-123">Use the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="e8701-124">Zie voor informatie over de storage-accounts en toegangstoetsen, [over Azure storage-accounts](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e8701-124">For information on storage accounts and access keys, see [About Azure storage accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="e8701-125">Dit voorbeeld ziet hoe u een statisch veld voor het opslaan van de verbindingsreeks kunt declareren:</span><span class="sxs-lookup"><span data-stu-id="e8701-125">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="e8701-126">Testen van uw toepassing in uw lokale Windows-computer, kunt u de Azure [opslagemulator](storage-use-emulator.md) die is geïnstalleerd met de [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e8701-126">To test your application in your local Windows-based computer, you can use the Azure [storage emulator](storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="e8701-127">De opslagemulator is een hulpprogramma dat de Azure Blob, wachtrijen en tabellen services beschikbaar zijn op uw lokale ontwikkelcomputer simuleert.</span><span class="sxs-lookup"><span data-stu-id="e8701-127">The storage emulator is a utility that simulates the Azure Blob, Queue, and Table services available on your local development machine.</span></span> <span data-ttu-id="e8701-128">Het volgende voorbeeld ziet u hoe u een statisch veld voor het opslaan van de verbindingsreeks naar uw lokale opslagemulator kunt declareren:</span><span class="sxs-lookup"><span data-stu-id="e8701-128">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="e8701-129">De Azure-opslagemulator starten, klikt u op de **Start** knop of druk op de Windows-toets.</span><span class="sxs-lookup"><span data-stu-id="e8701-129">To start the Azure storage emulator, click the **Start** button or press the Windows key.</span></span> <span data-ttu-id="e8701-130">Begint te typen **Azure-Opslagemulator**, en selecteer vervolgens **Microsoft Azure-Opslagemulator** uit de lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e8701-130">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="e8701-131">De volgende voorbeelden wordt ervan uitgegaan dat u een van deze twee methoden hebt gebruikt om op te halen van de verbindingsreeks voor opslag.</span><span class="sxs-lookup"><span data-stu-id="e8701-131">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="e8701-132">De verbindingsreeks ophalen</span><span class="sxs-lookup"><span data-stu-id="e8701-132">Retrieve your connection string</span></span>
<span data-ttu-id="e8701-133">U kunt de **cloud_storage_account** klasse vertegenwoordigt de gegevens van uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="e8701-133">You can use the **cloud_storage_account** class to represent your storage account information.</span></span> <span data-ttu-id="e8701-134">Voor het ophalen van gegevens over uw storage-account van de verbindingsreeks voor opslag, kunt u de parseermethode.</span><span class="sxs-lookup"><span data-stu-id="e8701-134">To retrieve your storage account information from the storage connection string, you can use the parse method.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="e8701-135">Vervolgens maakt geen verwijzing ophalen naar een **cloud_table_client** klasse, zoals het kunt u profiteren van reference-objecten voor tabellen en entiteiten die zijn opgeslagen in de tabel storage-service.</span><span class="sxs-lookup"><span data-stu-id="e8701-135">Next, get a reference to a **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within the Table storage service.</span></span> <span data-ttu-id="e8701-136">De volgende code maakt een **cloud_table_client** object met behulp van het opslagobject account we hierboven opgehaald:</span><span class="sxs-lookup"><span data-stu-id="e8701-136">The following code creates a **cloud_table_client** object by using the storage account object we retrieved above:</span></span>  

```cpp
// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a><span data-ttu-id="e8701-137">Een tabel maken</span><span class="sxs-lookup"><span data-stu-id="e8701-137">Create a table</span></span>
<span data-ttu-id="e8701-138">Een **cloud_table_client** object kunt u profiteren van reference-objecten voor tabellen en entiteiten.</span><span class="sxs-lookup"><span data-stu-id="e8701-138">A **cloud_table_client** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="e8701-139">De volgende code maakt een **cloud_table_client** object en gebruikt deze om een nieuwe tabel maken.</span><span class="sxs-lookup"><span data-stu-id="e8701-139">The following code creates a **cloud_table_client** object and uses it to create a new table.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference to a table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="e8701-140">Een entiteit toevoegen aan een tabel</span><span class="sxs-lookup"><span data-stu-id="e8701-140">Add an entity to a table</span></span>
<span data-ttu-id="e8701-141">Als u wilt een entiteit toevoegen aan een tabel, maakt u een nieuwe **table_entity** object en doorgegeven aan **table_operation::insert_entity**.</span><span class="sxs-lookup"><span data-stu-id="e8701-141">To add an entity to a table, create a new **table_entity** object and pass it to **table_operation::insert_entity**.</span></span> <span data-ttu-id="e8701-142">De volgende code gebruikt de voornaam van de klant als de rijsleutel en de achternaam als de partitiesleutel.</span><span class="sxs-lookup"><span data-stu-id="e8701-142">The following code uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="e8701-143">De partitie- en rijsleutel van een entiteit vormen samen de unieke id van de entiteit in de tabel.</span><span class="sxs-lookup"><span data-stu-id="e8701-143">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="e8701-144">Entiteiten met dezelfde partitiesleutel kunnen sneller worden opgevraagd dan die met verschillende partitiesleutels, maar met verschillende partitiesleutels kunt grotere schaalbaarheid van parallelle bewerking.</span><span class="sxs-lookup"><span data-stu-id="e8701-144">Entities with the same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span></span> <span data-ttu-id="e8701-145">Zie voor meer informatie [Microsoft Azure storage controlelijst voor prestaties en schaalbaarheid](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="e8701-145">For more information, see [Microsoft Azure storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<span data-ttu-id="e8701-146">De volgende code maakt een nieuw exemplaar van **table_entity** met sommige gegevens van de klant worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e8701-146">The following code creates a new instance of **table_entity** with some customer data to be stored.</span></span> <span data-ttu-id="e8701-147">De volgende code-aanroepen **table_operation::insert_entity** maken een **table_operation** object voor het invoegen van een entiteit in een tabel en de nieuwe Tabelentiteit gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="e8701-147">The code next calls **table_operation::insert_entity** to create a **table_operation** object to insert an entity into a table, and associates the new table entity with it.</span></span> <span data-ttu-id="e8701-148">Ten slotte de code de execute-methode aanroepen op de **cloud_table** object.</span><span class="sxs-lookup"><span data-stu-id="e8701-148">Finally, the code calls the execute method on the **cloud_table** object.</span></span> <span data-ttu-id="e8701-149">En de nieuwe **table_operation** verzendt een aanvraag naar de tabel-service naar de nieuwe klantentiteit in de tabel 'gebruikers' invoegen.</span><span class="sxs-lookup"><span data-stu-id="e8701-149">And the new **table_operation** sends a request to the Table service to insert the new customer entity into the "people" table.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference to a table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create the table operation that inserts the customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute the insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="e8701-150">Een batch entiteiten invoegen</span><span class="sxs-lookup"><span data-stu-id="e8701-150">Insert a batch of entities</span></span>
<span data-ttu-id="e8701-151">U kunt een batch entiteiten met de service tabel invoegen in één schrijfbewerking.</span><span class="sxs-lookup"><span data-stu-id="e8701-151">You can insert a batch of entities to the Table service in one write operation.</span></span> <span data-ttu-id="e8701-152">De volgende code maakt een **table_batch_operation** object en vervolgens voegt u drie bewerkingen voor het invoegen.</span><span class="sxs-lookup"><span data-stu-id="e8701-152">The following code creates a **table_batch_operation** object, and then adds three insert operations to it.</span></span> <span data-ttu-id="e8701-153">Elke bewerking insert is toegevoegd door het maken van een nieuwe entiteitsobject, de waarden in te stellen en vervolgens het aanroepen van de methode invoegen op het **table_batch_operation** -object op voor de entiteit koppelen aan een nieuwe insert-bewerking.</span><span class="sxs-lookup"><span data-stu-id="e8701-153">Each insert operation is added by creating a new entity object, setting its values, and then calling the insert method on the **table_batch_operation** object to associate the entity with a new insert operation.</span></span> <span data-ttu-id="e8701-154">Vervolgens **cloud_table.execute** aangeroepen om de bewerking niet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e8701-154">Then, **cloud_table.execute** is called to execute the operation.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it to the table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it to the table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity to add to the table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities to the batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute the batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

<span data-ttu-id="e8701-155">Een aantal zaken te weten over batchbewerkingen:</span><span class="sxs-lookup"><span data-stu-id="e8701-155">Some things to note on batch operations:</span></span>  

* <span data-ttu-id="e8701-156">U kunt maximaal 100 invoegen, verwijderen, samenvoegen, vervangen, invoegen of merge en invoegen of vervangen bewerkingen uitvoeren in een willekeurige combinatie in één batch.</span><span class="sxs-lookup"><span data-stu-id="e8701-156">You can perform up to 100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span></span>  
* <span data-ttu-id="e8701-157">Een batchbewerking kan een bewerking ophalen hebben als dit de enige bewerking in de batch.</span><span class="sxs-lookup"><span data-stu-id="e8701-157">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span></span>  
* <span data-ttu-id="e8701-158">Alle entiteiten in een batchbewerking moeten dezelfde partitiesleutel hebben.</span><span class="sxs-lookup"><span data-stu-id="e8701-158">All entities in a single batch operation must have the same partition key.</span></span>  
* <span data-ttu-id="e8701-159">Een batchbewerking is beperkt tot een nettolading met gegevens van 4 MB.</span><span class="sxs-lookup"><span data-stu-id="e8701-159">A batch operation is limited to a 4-MB data payload.</span></span>  

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="e8701-160">Alle entiteiten in een partitie ophalen</span><span class="sxs-lookup"><span data-stu-id="e8701-160">Retrieve all entities in a partition</span></span>
<span data-ttu-id="e8701-161">Gebruiken om te vragen een tabel voor alle entiteiten in een partitie, een **table_query** object.</span><span class="sxs-lookup"><span data-stu-id="e8701-161">To query a table for all entities in a partition, use a **table_query** object.</span></span> <span data-ttu-id="e8701-162">Het volgende codevoorbeeld geeft een filter voor entiteiten waarbij 'Smith' de partitiesleutel is.</span><span class="sxs-lookup"><span data-stu-id="e8701-162">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="e8701-163">In dit voorbeeld worden de velden van elke entiteit in de queryresultaten naar de console afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="e8701-163">This example prints the fields of each entity in the query results to the console.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct the query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print the fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

<span data-ttu-id="e8701-164">De query in dit voorbeeld wordt de entiteiten die overeenkomen met de filtercriteria.</span><span class="sxs-lookup"><span data-stu-id="e8701-164">The query in this example brings all the entities that match the filter criteria.</span></span> <span data-ttu-id="e8701-165">Als er grote tabellen en moet de tabelentiteiten downloaden vaak we raden aan dat opslaat u uw gegevens in Azure storage-blobs in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="e8701-165">If you have large tables and need to download the table entities often, we recommend that you store your data in Azure storage blobs instead.</span></span>

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="e8701-166">Een bereik van entiteiten in een partitie ophalen</span><span class="sxs-lookup"><span data-stu-id="e8701-166">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="e8701-167">Als u geen query wilt uitvoeren op alle entiteiten in een partitie, kunt u een bereik opgeven door het partitiesleutelfilter te combineren met een rijsleutelfilter.</span><span class="sxs-lookup"><span data-stu-id="e8701-167">If you don't want to query all the entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span></span> <span data-ttu-id="e8701-168">Het volgende codevoorbeeld maakt gebruik van twee filters om alle entiteiten met de partitie 'Smith' op te halen waarbij de rijsleutel (voornaam) begint met een letter die in het alfabet vóór de 'E' komt. Vervolgens worden de resultaten van de query afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="e8701-168">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter earlier than 'E' in the alphabet and then prints the query results.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through the results, displaying information about the entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="e8701-169">Eén entiteit ophalen</span><span class="sxs-lookup"><span data-stu-id="e8701-169">Retrieve a single entity</span></span>
<span data-ttu-id="e8701-170">U kunt een query schrijven om één specifieke entiteit op te halen.</span><span class="sxs-lookup"><span data-stu-id="e8701-170">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="e8701-171">De volgende code gebruikt **table_operation::retrieve_entity** om op te geven van de klant 'Jeff Smith'.</span><span class="sxs-lookup"><span data-stu-id="e8701-171">The following code uses **table_operation::retrieve_entity** to specify the customer 'Jeff Smith'.</span></span> <span data-ttu-id="e8701-172">Deze methode retourneert één entiteit in plaats van een verzameling en de geretourneerde waarde is in **table_result**.</span><span class="sxs-lookup"><span data-stu-id="e8701-172">This method returns just one entity, rather than a collection, and the returned value is in **table_result**.</span></span> <span data-ttu-id="e8701-173">Het opgeven van zowel partitie- als rijsleutels in een query is de snelste manier om één entiteit op te halen uit de Tabelservice.</span><span class="sxs-lookup"><span data-stu-id="e8701-173">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output the entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a><span data-ttu-id="e8701-174">Een entiteit vervangen</span><span class="sxs-lookup"><span data-stu-id="e8701-174">Replace an entity</span></span>
<span data-ttu-id="e8701-175">Ter vervanging van een entiteit ophalen uit de tabelservice, wijzigt het entiteitsobject en sla de wijzigingen terug naar de tabel-service.</span><span class="sxs-lookup"><span data-stu-id="e8701-175">To replace an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="e8701-176">De volgende code wijzigt het telefoonnummer en e-mailadres van een bestaande klant.</span><span class="sxs-lookup"><span data-stu-id="e8701-176">The following code changes an existing customer's phone number and email address.</span></span> <span data-ttu-id="e8701-177">In plaats van aanroepen **table_operation::insert_entity**, deze code gebruikt **table_operation::replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="e8701-177">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span></span> <span data-ttu-id="e8701-178">Met deze bewerking wordt de entiteit op de server volledig vervangen, tenzij de entiteit op de server sinds het ophalen is gewijzigd. In dat geval mislukt de bewerking.</span><span class="sxs-lookup"><span data-stu-id="e8701-178">This causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span></span> <span data-ttu-id="e8701-179">Hiermee wordt voorkomen dat de toepassing per ongeluk een wijziging overschrijft die door een ander onderdeel van uw toepassing is aangebracht tussen het moment van ophalen en het moment van bijwerken.</span><span class="sxs-lookup"><span data-stu-id="e8701-179">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span></span> <span data-ttu-id="e8701-180">De juiste verwerking van deze fout wordt de entiteit opnieuw ophalen, breng uw wijzigingen (indien nog geldig) en voert u een andere **table_operation::replace_entity** bewerking.</span><span class="sxs-lookup"><span data-stu-id="e8701-180">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span></span> <span data-ttu-id="e8701-181">In de volgende sectie wordt beschreven hoe u dit gedrag kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e8701-181">The next section will show you how to override this behavior.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation to replace the entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit the operation to the Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="e8701-182">Een entiteit invoegen of vervangen</span><span class="sxs-lookup"><span data-stu-id="e8701-182">Insert-or-replace an entity</span></span>
<span data-ttu-id="e8701-183">**table_operation::replace_entity** bewerkingen mislukken als de entiteit is gewijzigd nadat deze is opgehaald van de server.</span><span class="sxs-lookup"><span data-stu-id="e8701-183">**table_operation::replace_entity** operations will fail if the entity has been changed since it was retrieved from the server.</span></span> <span data-ttu-id="e8701-184">Bovendien moet u ophalen de entiteit van de server eerst om **table_operation::replace_entity** lukken.</span><span class="sxs-lookup"><span data-stu-id="e8701-184">Furthermore, you must retrieve the entity from the server first in order for **table_operation::replace_entity** to be successful.</span></span> <span data-ttu-id="e8701-185">Soms echter, u niet weet of de entiteit op de server bestaat en de huidige waarden die erin niet relevant zijn: de update worden deze allemaal overschreven.</span><span class="sxs-lookup"><span data-stu-id="e8701-185">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant—your update should overwrite them all.</span></span> <span data-ttu-id="e8701-186">Hiervoor gebruikt u een **table_operation::insert_or_replace_entity** bewerking.</span><span class="sxs-lookup"><span data-stu-id="e8701-186">To accomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span></span> <span data-ttu-id="e8701-187">Met deze bewerking wordt de entiteit ingevoegd als deze niet bestaat of vervangen als deze wel bestaat, ongeacht wanneer de laatste update is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e8701-187">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span></span> <span data-ttu-id="e8701-188">In het volgende codevoorbeeld wordt de klantentiteit voor Jeff Smith nog steeds opgehaald, maar deze wordt vervolgens terug naar de server via opgeslagen **table_operation::insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="e8701-188">In the following code example, the customer entity for Jeff Smith is still retrieved, but it is then saved back to the server via **table_operation::insert_or_replace_entity**.</span></span> <span data-ttu-id="e8701-189">Wijzigingen in de entiteit tussen het ophalen en de update-bewerking worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="e8701-189">Any updates made to the entity between the retrieval and update operation will be overwritten.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation to insert-or-replace the entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit the operation to the Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="e8701-190">Een query uitvoeren op een subset van entiteitseigenschappen</span><span class="sxs-lookup"><span data-stu-id="e8701-190">Query a subset of entity properties</span></span>
<span data-ttu-id="e8701-191">Een query naar een tabel ophalen slechts enkele eigenschappen van een entiteit.</span><span class="sxs-lookup"><span data-stu-id="e8701-191">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="e8701-192">De query in de volgende code gebruikt de **table_query::set_select_columns** methode om te worden alleen de e-mailadressen van entiteiten in de tabel retourneren.</span><span class="sxs-lookup"><span data-stu-id="e8701-192">The query in the following code uses the **table_query::set_select_columns** method to return only the email addresses of entities in the table.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define the query, and select only the Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display the results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> <span data-ttu-id="e8701-193">Opvragen van enkele eigenschappen van een entiteit is een efficiëntere bewerking dan bij het ophalen van alle eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="e8701-193">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span></span>
> 
> 

## <a name="delete-an-entity"></a><span data-ttu-id="e8701-194">Een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="e8701-194">Delete an entity</span></span>
<span data-ttu-id="e8701-195">U kunt een entiteit gemakkelijk verwijderen nadat u deze hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="e8701-195">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="e8701-196">Wanneer de entiteit is opgehaald, aanroepen **table_operation::delete_entity** met de entiteit wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e8701-196">Once the entity is retrieved, call **table_operation::delete_entity** with the entity to delete.</span></span> <span data-ttu-id="e8701-197">Roep vervolgens de **cloud_table.execute** methode.</span><span class="sxs-lookup"><span data-stu-id="e8701-197">Then call the **cloud_table.execute** method.</span></span> <span data-ttu-id="e8701-198">De volgende code haalt en verwijdert een entiteit met een partitiesleutel van 'Smith' en een rijsleutel van 'Jeff'.</span><span class="sxs-lookup"><span data-stu-id="e8701-198">The following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation to delete the entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit the delete operation to the Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a><span data-ttu-id="e8701-199">Een tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="e8701-199">Delete a table</span></span>
<span data-ttu-id="e8701-200">Ten slotte wordt met het volgende codevoorbeeld een tabel uit een opslagaccount verwijderd.</span><span class="sxs-lookup"><span data-stu-id="e8701-200">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="e8701-201">Een verwijderde tabel kan gedurende een bepaalde tijd na de verwijdering niet opnieuw worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e8701-201">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation to delete the entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit the delete operation to the Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a><span data-ttu-id="e8701-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e8701-202">Next steps</span></span>
<span data-ttu-id="e8701-203">Nu u de basisprincipes van table storage hebt geleerd, volgt u deze koppelingen voor meer informatie over Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="e8701-203">Now that you've learned the basics of table storage, follow these links to learn more about Azure Storage:</span></span>  

* <span data-ttu-id="e8701-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u visueel met Azure Storage-gegevens kunt werken in Windows, macOS en Linux.</span><span class="sxs-lookup"><span data-stu-id="e8701-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="e8701-205">Het Blob storage gebruiken met C++</span><span class="sxs-lookup"><span data-stu-id="e8701-205">How to use Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="e8701-206">Hoe Queue storage gebruiken met C++</span><span class="sxs-lookup"><span data-stu-id="e8701-206">How to use Queue storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="e8701-207">Lijst van Azure Storage-resources in C++</span><span class="sxs-lookup"><span data-stu-id="e8701-207">List Azure Storage resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="e8701-208">Opslagclientbibliotheek voor C++-verwijzing</span><span class="sxs-lookup"><span data-stu-id="e8701-208">Storage Client Library for C++ reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="e8701-209">Documentatie bij Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e8701-209">Azure Storage documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
