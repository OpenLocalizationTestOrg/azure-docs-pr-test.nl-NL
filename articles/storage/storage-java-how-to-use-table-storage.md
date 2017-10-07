---
title: aaaHow toouse Table storage met Java | Microsoft Docs
description: Gestructureerde gegevens opslaan in Hallo cloud met Azure Table storage, een NoSQL-gegevensarchief.
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: f72cac3fc10cf0aef74780b84c515d93d715d787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-java"></a><span data-ttu-id="37ac9-103">Hoe toouse Table storage met Java</span><span class="sxs-lookup"><span data-stu-id="37ac9-103">How toouse Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="37ac9-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="37ac9-104">Overview</span></span>
<span data-ttu-id="37ac9-105">Deze handleiding leert u hoe tooperform algemene scenario's met behulp van hello Azure Table storage-service.</span><span class="sxs-lookup"><span data-stu-id="37ac9-105">This guide will show you how tooperform common scenarios using hello Azure Table storage service.</span></span> <span data-ttu-id="37ac9-106">Hallo-voorbeelden zijn geschreven in Java en gebruiken van Hallo [Azure-opslag-SDK voor Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="37ac9-106">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="37ac9-107">Hallo scenario's worden behandeld: **maken**, **aanbieding**, en **verwijderen** tabellen, evenals **invoegen**,  **uitvoeren van query's**, **wijzigen**, en **verwijderen** entiteiten in een tabel.</span><span class="sxs-lookup"><span data-stu-id="37ac9-107">hello scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="37ac9-108">Zie voor meer informatie over tabellen Hallo [Vervolgstappen](#Next-Steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="37ac9-108">For more information on tables, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="37ac9-109">Opmerking: Een SDK is beschikbaar voor ontwikkelaars die werken met Azure Storage op Android-apparaten.</span><span class="sxs-lookup"><span data-stu-id="37ac9-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="37ac9-110">Zie voor meer informatie, Hallo [Azure-opslag-SDK voor Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="37ac9-110">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="37ac9-111">Een Java-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="37ac9-111">Create a Java application</span></span>
<span data-ttu-id="37ac9-112">In deze handleiding gebruikt u opslagfuncties die kunnen worden uitgevoerd binnen een Java-toepassing lokaal of in de code die wordt uitgevoerd binnen een Webrol of worker-rol in Azure.</span><span class="sxs-lookup"><span data-stu-id="37ac9-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="37ac9-113">toodo geval is, moet u tooinstall Hallo Java Development Kit (JDK) en een Azure storage-account maken in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="37ac9-113">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="37ac9-114">Nadat u dit hebt gedaan, moet u tooverify dat uw ontwikkelsysteem voldoet aan de minimumvereisten Hallo en afhankelijkheden die worden vermeld in Hallo [Azure-opslag-SDK voor Java] [ Azure Storage SDK for Java] opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="37ac9-114">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="37ac9-115">Als uw systeem aan deze vereisten voldoet, kunt u de instructies voor het downloaden en installeren van hello Azure Storage-bibliotheken voor Java op uw systeem vanuit die opslagplaats Hallo volgen.</span><span class="sxs-lookup"><span data-stu-id="37ac9-115">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="37ac9-116">Nadat u deze taken hebt voltooid, kunt u zich kunt toocreate een Java-toepassing die gebruikmaakt van Hallo voorbeelden in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="37ac9-116">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="37ac9-117">Uw toepassing tooaccess tabelopslag configureren</span><span class="sxs-lookup"><span data-stu-id="37ac9-117">Configure your application tooaccess table storage</span></span>
<span data-ttu-id="37ac9-118">Hallo na importeren instructies toohello bovenaan Hallo Java bestand waar u toouse Microsoft Azure storage-API's tooaccess tabellen toevoegen:</span><span class="sxs-lookup"><span data-stu-id="37ac9-118">Add hello following import statements toohello top of hello Java file where you want toouse Microsoft Azure storage APIs tooaccess tables:</span></span>

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="37ac9-119">Een Azure-opslag-verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="37ac9-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="37ac9-120">Een Azure-opslag-client maakt gebruik van een storage connection string toostore eindpunten en referenties voor toegang tot gegevens beheerservices.</span><span class="sxs-lookup"><span data-stu-id="37ac9-120">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="37ac9-121">Wanneer een client-toepassing wordt uitgevoerd, moet u bieden Hallo verbindingsreeks voor opslag in Hallo indeling te volgen, met behulp van Hallo-naam van uw opslagaccount en primaire toegangssleutel voor opslagaccount Hallo die worden vermeld in Hallo Hallo [Azure-portal](https://portal.azure.com)voor Hallo *AccountName* en *AccountKey* waarden.</span><span class="sxs-lookup"><span data-stu-id="37ac9-121">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="37ac9-122">Dit voorbeeld ziet hoe u een statisch veld toohold Hallo-verbindingsreeks kunt declareren:</span><span class="sxs-lookup"><span data-stu-id="37ac9-122">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="37ac9-123">In een toepassing in een rol in Microsoft Azure wordt uitgevoerd, kan deze tekenreeks worden opgeslagen in Hallo serviceconfiguratiebestand, *ServiceConfiguration.cscfg*, en kunnen worden geopend met een aanroep van toohello  **RoleEnvironment.getConfigurationSettings** methode.</span><span class="sxs-lookup"><span data-stu-id="37ac9-123">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="37ac9-124">Hier volgt een voorbeeld van het ophalen van Hallo-verbindingsreeks uit een **instelling** element met de naam *StorageConnectionString* in Hallo serviceconfiguratiebestand:</span><span class="sxs-lookup"><span data-stu-id="37ac9-124">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="37ac9-125">Hallo volgende voorbeelden wordt ervan uitgegaan dat u een van deze twee methoden tooget Hallo-opslagverbindingsreeks hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="37ac9-125">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="37ac9-126">Procedure: een tabel maken</span><span class="sxs-lookup"><span data-stu-id="37ac9-126">How to: Create a table</span></span>
<span data-ttu-id="37ac9-127">Een **CloudTableClient** object kunt u profiteren van reference-objecten voor tabellen en entiteiten.</span><span class="sxs-lookup"><span data-stu-id="37ac9-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="37ac9-128">Hallo volgende code maakt een **CloudTableClient** object en gebruikt deze toocreate een nieuwe **CloudTable** -object met een tabel met de naam 'mensen'.</span><span class="sxs-lookup"><span data-stu-id="37ac9-128">hello following code creates a **CloudTableClient** object and uses it toocreate a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="37ac9-129">(Opmerking: Er zijn extra manieren toocreate **CloudStorageAccount** objecten; voor meer informatie Zie **CloudStorageAccount** in Hallo [Azure Storage Client SDK-naslaginformatie].)</span><span class="sxs-lookup"><span data-stu-id="37ac9-129">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create hello table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-tables"></a><span data-ttu-id="37ac9-130">Hoe: Hallo tabellen</span><span class="sxs-lookup"><span data-stu-id="37ac9-130">How to: List hello tables</span></span>
<span data-ttu-id="37ac9-131">een lijst met tabellen, aanroep Hallo tooget **CloudTableClient.listTables()** methode tooretrieve een iterable lijst met namen van tabellen.</span><span class="sxs-lookup"><span data-stu-id="37ac9-131">tooget a list of tables, call hello **CloudTableClient.listTables()** method tooretrieve an iterable list of table names.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through hello collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-tooa-table"></a><span data-ttu-id="37ac9-132">Procedure: een entiteit tooa tabel toevoegen</span><span class="sxs-lookup"><span data-stu-id="37ac9-132">How to: Add an entity tooa table</span></span>
<span data-ttu-id="37ac9-133">Entiteiten worden toegewezen tooJava objecten met behulp van de implementatie van een aangepaste klasse **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="37ac9-133">Entities map tooJava objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="37ac9-134">Voor het gemak Hallo **TableServiceEntity** klasse implementeert **TableEntity** en maakt gebruik van reflectie toomap eigenschappen toogetter en setter methoden met de naam van Hallo eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="37ac9-134">For convenience, hello **TableServiceEntity** class implements **TableEntity** and uses reflection toomap properties toogetter and setter methods named for hello properties.</span></span> <span data-ttu-id="37ac9-135">een tabel entity tooa tooadd eerst een klasse die eigenschappen Hallo van uw entiteit definieert maken.</span><span class="sxs-lookup"><span data-stu-id="37ac9-135">tooadd an entity tooa table, first create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="37ac9-136">Hallo definieert volgende code een entiteitsklasse dat gebruikmaakt van de voornaam van de klant Hallo als Hallo rijsleutel en de achternaam als partitiesleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="37ac9-136">hello following code defines an entity class which uses hello customer's first name as hello row key, and last name as hello partition key.</span></span> <span data-ttu-id="37ac9-137">Samen een entiteit partitie en rijsleutel een unieke identificatie Hallo entiteit in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="37ac9-137">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="37ac9-138">Entiteiten met dezelfde partitiesleutel kan sneller worden opgevraagd dan die met verschillende partitiesleutels Hallo.</span><span class="sxs-lookup"><span data-stu-id="37ac9-138">Entities with hello same partition key can be queried faster than those with different partition keys.</span></span>

```java
public class CustomerEntity extends TableServiceEntity {
    public CustomerEntity(String lastName, String firstName) {
        this.partitionKey = lastName;
        this.rowKey = firstName;
    }

    public CustomerEntity() { }

    String email;
    String phoneNumber;

    public String getEmail() {
        return this.email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPhoneNumber() {
        return this.phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }
}
```

<span data-ttu-id="37ac9-139">Tabelbewerkingen met betrekking tot entiteiten vereist een **TableOperation** object.</span><span class="sxs-lookup"><span data-stu-id="37ac9-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="37ac9-140">Dit object definieert Hallo bewerking toobe uitgevoerd op een entiteit die kan worden uitgevoerd met een **CloudTable** object.</span><span class="sxs-lookup"><span data-stu-id="37ac9-140">This object defines hello operation toobe performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="37ac9-141">Hallo volgende code maakt een nieuw exemplaar van Hallo **CustomerEntity** klasse met sommige klant gegevens toobe opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="37ac9-141">hello following code creates a new instance of hello **CustomerEntity** class with some customer data toobe stored.</span></span> <span data-ttu-id="37ac9-142">de volgende aanroepen code Hallo **TableOperation.insertOrReplace** toocreate een **TableOperation** object tooinsert een entiteit in een tabel en gekoppeld Hallo nieuwe **CustomerEntity**aan.</span><span class="sxs-lookup"><span data-stu-id="37ac9-142">hello code next calls **TableOperation.insertOrReplace** toocreate a **TableOperation** object tooinsert an entity into a table, and associates hello new **CustomerEntity** with it.</span></span> <span data-ttu-id="37ac9-143">Ten slotte Hallo code roept Hallo **uitvoeren** methode op Hallo **CloudTable** -object, waarbij Hallo 'gebruikers' tabel en nieuw Hallo **TableOperation**, welke vervolgens verzendt een aanvragen van toohello opslag service tooinsert Hallo nieuwe klantentiteit in Hallo 'gebruikers' tabel of Hallo entiteit vervangen als deze al bestaat.</span><span class="sxs-lookup"><span data-stu-id="37ac9-143">Finally, hello code calls hello **execute** method on hello **CloudTable** object, specifying hello "people" table and hello new **TableOperation**, which then sends a request toohello storage service tooinsert hello new customer entity into hello "people" table, or replace hello entity if it already exists.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="37ac9-144">Procedure: een batch entiteiten invoegen</span><span class="sxs-lookup"><span data-stu-id="37ac9-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="37ac9-145">U kunt een batch entiteiten toohello tabelservice invoegen in één schrijfbewerking.</span><span class="sxs-lookup"><span data-stu-id="37ac9-145">You can insert a batch of entities toohello table service in one write operation.</span></span> <span data-ttu-id="37ac9-146">Hallo volgende code maakt een **TableBatchOperation** object en vervolgens voegt u drie bewerkingen tooit invoegen.</span><span class="sxs-lookup"><span data-stu-id="37ac9-146">hello following code creates a **TableBatchOperation** object, then adds three insert operations tooit.</span></span> <span data-ttu-id="37ac9-147">Elke bewerking insert is toegevoegd door het maken van een nieuwe entiteitsobject, de waarden in te stellen en vervolgens aanroepen Hallo **invoegen** methode op Hallo **TableBatchOperation** tooassociate Hallo entiteit met een nieuw object bewerking INSERT.</span><span class="sxs-lookup"><span data-stu-id="37ac9-147">Each insert operation is added by creating a new entity object, setting its values, and then calling hello **insert** method on hello **TableBatchOperation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="37ac9-148">Vervolgens Hallo code aanroepen **uitvoeren** op Hallo **CloudTable** -object, waarbij Hallo 'gebruikers' tabel en Hallo **TableBatchOperation** -object, dat Hallo batch van tabel verzendt bewerkingen toohello storage-service in een afzonderlijke aanvraag.</span><span class="sxs-lookup"><span data-stu-id="37ac9-148">Then hello code calls **execute** on hello **CloudTable** object, specifying hello "people" table and hello **TableBatchOperation** object, which sends hello batch of table operations toohello storage service in a single request.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity tooadd toohello table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity tooadd toohello table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity tooadd toohello table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute hello batch of operations on hello "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="37ac9-149">Een aantal dingen toonote over batchbewerkingen:</span><span class="sxs-lookup"><span data-stu-id="37ac9-149">Some things toonote on batch operations:</span></span>

* <span data-ttu-id="37ac9-150">U kunt uitvoeren om too100 invoegen, verwijderen, samenvoegen, vervangen, invoegen of samenvoegen, en invoegen of vervangen door bewerkingen in een willekeurige combinatie in één batch.</span><span class="sxs-lookup"><span data-stu-id="37ac9-150">You can perform up too100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="37ac9-151">Een batchbewerking kan een bewerking ophalen hebben als het Hallo enige bewerking in Hallo batch.</span><span class="sxs-lookup"><span data-stu-id="37ac9-151">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>
* <span data-ttu-id="37ac9-152">Alle entiteiten in een batchbewerking moeten Hallo hebben dezelfde partitiesleutel.</span><span class="sxs-lookup"><span data-stu-id="37ac9-152">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="37ac9-153">Een batchbewerking is beperkt tooa 4MB-nettolading.</span><span class="sxs-lookup"><span data-stu-id="37ac9-153">A batch operation is limited tooa 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="37ac9-154">Hoe: alle entiteiten in een partitie ophalen</span><span class="sxs-lookup"><span data-stu-id="37ac9-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="37ac9-155">een tabel voor entiteiten in een partitie tooquery, kunt u een **TableQuery**.</span><span class="sxs-lookup"><span data-stu-id="37ac9-155">tooquery a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="37ac9-156">Roep **TableQuery.from** toocreate een query op een bepaalde tabel die een resultaattype opgegeven retourneert.</span><span class="sxs-lookup"><span data-stu-id="37ac9-156">Call **TableQuery.from** toocreate a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="37ac9-157">Hallo geeft volgende code een filter voor entiteiten waarbij 'Smith' hello partitiesleutel is.</span><span class="sxs-lookup"><span data-stu-id="37ac9-157">hello following code specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="37ac9-158">**TableQuery.generateFilterCondition** toocreate filters voor query's van een Help-methode is.</span><span class="sxs-lookup"><span data-stu-id="37ac9-158">**TableQuery.generateFilterCondition** is a helper method toocreate filters for queries.</span></span> <span data-ttu-id="37ac9-159">Roep **waar** op Hallo verwijzing geretourneerd door Hallo **TableQuery.from** methode tooapply Hallo-filterquery toohello.</span><span class="sxs-lookup"><span data-stu-id="37ac9-159">Call **where** on hello reference returned by hello **TableQuery.from** method tooapply hello filter toohello query.</span></span> <span data-ttu-id="37ac9-160">Wanneer Hallo query wordt uitgevoerd met een aanroep te**uitvoeren** op Hallo **CloudTable** object, wordt een **Iterator** Hello **CustomerEntity**resultaattype opgegeven.</span><span class="sxs-lookup"><span data-stu-id="37ac9-160">When hello query is executed with a call too**execute** on hello **CloudTable** object, it returns an **Iterator** with hello **CustomerEntity** result type specified.</span></span> <span data-ttu-id="37ac9-161">Vervolgens kunt u Hallo **Iterator** geretourneerd in een voor elke lus tooconsume Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="37ac9-161">You can then use hello **Iterator** returned in a for each loop tooconsume hello results.</span></span> <span data-ttu-id="37ac9-162">Deze code wordt Hallo velden van elke entiteit in Hallo query resultaten toohello console afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="37ac9-162">This code prints hello fields of each entity in hello query results toohello console.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as hello partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through hello results, displaying information about hello entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="37ac9-163">Procedure: een bereik van entiteiten in een partitie ophalen</span><span class="sxs-lookup"><span data-stu-id="37ac9-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="37ac9-164">Als u niet tooquery alle Hallo entiteiten in een partitie wilt, kunt u een bereik met behulp van vergelijkingsoperators in een filter opgeven.</span><span class="sxs-lookup"><span data-stu-id="37ac9-164">If you don't want tooquery all hello entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="37ac9-165">Hallo code combineert twee filters tooget alle entiteiten in de partitie 'Smith' waar Hallo rijsleutel (voornaam) begint met een letter up too'E na ' in hello alfabet.</span><span class="sxs-lookup"><span data-stu-id="37ac9-165">hello following code combines two filters tooget all entities in partition "Smith" where hello row key (first name) starts with a letter up too'E' in hello alphabet.</span></span> <span data-ttu-id="37ac9-166">Vervolgens worden de queryresultaten Hallo afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="37ac9-166">Then it prints hello query results.</span></span> <span data-ttu-id="37ac9-167">Als u Hallo entiteiten toegevoegde toohello tabel in batch Hallo invoegen van deze handleiding, worden slechts twee entiteiten geretourneerd ditmaal (Ben en Denise Smith); Jeff Smith is niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="37ac9-167">If you use hello entities added toohello table in hello batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where hello row key is less than hello letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine hello two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as hello partition key,
    // with hello row key being up toohello letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through hello results, displaying information about hello entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="37ac9-168">Hoe: Eén entiteit ophalen</span><span class="sxs-lookup"><span data-stu-id="37ac9-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="37ac9-169">U kunt een query tooretrieve één specifieke entiteit schrijven.</span><span class="sxs-lookup"><span data-stu-id="37ac9-169">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="37ac9-170">Hallo volgende code aanroepen **TableOperation.retrieve** met partitie-sleutel en rij belangrijke parameters toospecify Hallo klant 'Jeff Smith', in plaats van het maken van een **TableQuery** en filters toodo hello gebruiken hetzelfde geldt.</span><span class="sxs-lookup"><span data-stu-id="37ac9-170">hello following code calls **TableOperation.retrieve** with partition key and row key parameters toospecify hello customer "Jeff Smith", instead of creating a **TableQuery** and using filters toodo hello same thing.</span></span> <span data-ttu-id="37ac9-171">Bij uitvoering ophalen Hallo bewerking retourneert één entiteit in plaats van een verzameling.</span><span class="sxs-lookup"><span data-stu-id="37ac9-171">When executed, hello retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="37ac9-172">Hallo **getResultAsType** methode cast Hallo resultaattype toohello van Hallo toewijzing target, een **CustomerEntity** object.</span><span class="sxs-lookup"><span data-stu-id="37ac9-172">hello **getResultAsType** method casts hello result toohello type of hello assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="37ac9-173">Als u dit type is niet compatibel met het Hallo-type opgegeven voor Hallo query, wordt er een uitzondering opgetreden.</span><span class="sxs-lookup"><span data-stu-id="37ac9-173">If this type is not compatible with hello type specified for hello query, an exception will be thrown.</span></span> <span data-ttu-id="37ac9-174">Als er is geen entiteit heeft een exacte partitie en de rijsleutel overeen met een null-waarde geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="37ac9-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="37ac9-175">Het opgeven van de partitie-als rijsleutels in een query is Hallo snelste manier tooretrieve uit de tabelservice Hallo één entiteit.</span><span class="sxs-lookup"><span data-stu-id="37ac9-175">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output hello entity.
    if (specificEntity != null)
    {
        System.out.println(specificEntity.getPartitionKey() +
            " " + specificEntity.getRowKey() +
            "\t" + specificEntity.getEmail() +
            "\t" + specificEntity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="37ac9-176">Procedure: een entiteit wijzigen</span><span class="sxs-lookup"><span data-stu-id="37ac9-176">How to: Modify an entity</span></span>
<span data-ttu-id="37ac9-177">toomodify een entiteit ophalen uit de tabelservice hello, wijzigingen toohello entiteitsobject, wijzigingen aanbrengen en opslaan Hallo back toohello tabel-service met een vervangings- of merge-bewerking.</span><span class="sxs-lookup"><span data-stu-id="37ac9-177">toomodify an entity, retrieve it from hello table service, make changes toohello entity object, and save hello changes back toohello table service with a replace or merge operation.</span></span> <span data-ttu-id="37ac9-178">Hallo wijzigt volgende code het telefoonnummer van een bestaande klant.</span><span class="sxs-lookup"><span data-stu-id="37ac9-178">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="37ac9-179">In plaats van aanroepen **TableOperation.insert** zoals we tooinsert hebt gedaan, wordt deze code roept **TableOperation.replace**.</span><span class="sxs-lookup"><span data-stu-id="37ac9-179">Instead of calling **TableOperation.insert** like we did tooinsert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="37ac9-180">Hallo **CloudTable.execute** tabelservice Hallo-methodeaanroepen en Hallo entiteit wordt vervangen, tenzij een andere toepassing gewijzigd het Hallo tijdig sinds deze toepassing wordt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="37ac9-180">hello **CloudTable.execute** method calls hello table service, and hello entity is replaced, unless another application changed it in hello time since this application retrieved it.</span></span> <span data-ttu-id="37ac9-181">Wanneer dit gebeurt, is een uitzondering opgetreden en Hallo entiteit moet worden opgehaald, gewijzigd en opnieuw worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="37ac9-181">When that happens, an exception is thrown, and hello entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="37ac9-182">Dit patroon van een nieuwe poging optimistische gelijktijdigheid is gemeenschappelijk in een gedistribueerd opslagsysteem.</span><span class="sxs-lookup"><span data-stu-id="37ac9-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation tooreplace hello entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit hello operation toohello table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="37ac9-183">Hoe: query uitvoeren op een subset van entiteitseigenschappen</span><span class="sxs-lookup"><span data-stu-id="37ac9-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="37ac9-184">Een query tooa tabel ophalen slechts enkele eigenschappen van een entiteit.</span><span class="sxs-lookup"><span data-stu-id="37ac9-184">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="37ac9-185">Deze methode, projectie genoemd, verbruikt minder bandbreedte en kan de queryprestaties verbeteren, vooral bij grote entiteiten.</span><span class="sxs-lookup"><span data-stu-id="37ac9-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="37ac9-186">Hallo query in de volgende code Hallo gebruikt Hallo **Selecteer** methode tooreturn alleen Hallo e-mailadressen van entiteiten in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="37ac9-186">hello query in hello following code uses hello **select** method tooreturn only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="37ac9-187">Hello zijn resultaten geprojecteerd in een verzameling van **tekenreeks** met behulp van Hallo een **EntityResolver**, dat typeconversie op Hallo entiteiten geretourneerd vanaf de server Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="37ac9-187">hello results are projected into a collection of **String** with hello help of an **EntityResolver**, which does hello type conversion on hello entities returned from hello server.</span></span> <span data-ttu-id="37ac9-188">U kunt meer informatie over projectie in [Azure-tabellen: blogbericht introductie tot Upsert en Query projectie][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="37ac9-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="37ac9-189">Houd er rekening mee dat projectie niet wordt ondersteund op Hallo-emulator voor lokale opslag, zodat deze code wordt alleen uitgevoerd als met een account op Hallo tabel-service.</span><span class="sxs-lookup"><span data-stu-id="37ac9-189">Note that projection is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only hello Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver tooproject hello entity toohello Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through hello results, displaying hello Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="37ac9-190">Hoe: invoegen of vervangen van een entiteit</span><span class="sxs-lookup"><span data-stu-id="37ac9-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="37ac9-191">U vaak een entiteit tooa tabel tooadd zonder te weten te komen of deze al in de tabel Hallo voorkomt.</span><span class="sxs-lookup"><span data-stu-id="37ac9-191">Often you want tooadd an entity tooa table without knowing if it already exists in hello table.</span></span> <span data-ttu-id="37ac9-192">Een bewerking voor invoegen of vervangen, kunt u toomake één aanvraag die Hallo entiteit wordt ingevoegd als deze bestaat niet of u een bestaande als dit wel Hallo vervangen.</span><span class="sxs-lookup"><span data-stu-id="37ac9-192">An insert-or-replace operation allows you toomake a single request which will insert hello entity if it does not exist or replace hello existing one if it does.</span></span> <span data-ttu-id="37ac9-193">Voortbouwend op de eerdere voorbeelden, hello volgende code wordt ingevoegd of vervangen Hallo entiteit voor 'Walter Harp'.</span><span class="sxs-lookup"><span data-stu-id="37ac9-193">Building on prior examples, hello following code inserts or replaces hello entity for "Walter Harp".</span></span> <span data-ttu-id="37ac9-194">Na het maken van een nieuwe entiteit deze code roept Hallo **TableOperation.insertOrReplace** methode.</span><span class="sxs-lookup"><span data-stu-id="37ac9-194">After creating a new entity, this code calls hello **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="37ac9-195">Deze code roept vervolgens **uitvoeren** op Hallo **CloudTable** object met Hallo tabel en Hallo invoegen of vervangen als Hallo parameters van een tabel is.</span><span class="sxs-lookup"><span data-stu-id="37ac9-195">This code then calls **execute** on hello **CloudTable** object with hello table and hello insert or replace table operation as hello parameters.</span></span> <span data-ttu-id="37ac9-196">slechts een deel van een entiteit tooupdate hello **TableOperation.insertOrMerge** methode in plaats daarvan kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="37ac9-196">tooupdate only part of an entity, hello **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="37ac9-197">Houd er rekening mee dat invoegen of vervangen wordt niet ondersteund op Hallo-emulator voor lokale opslag, zodat deze code wordt alleen uitgevoerd als met een account op Hallo tabel-service.</span><span class="sxs-lookup"><span data-stu-id="37ac9-197">Note that insert-or-replace is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span> <span data-ttu-id="37ac9-198">U kunt meer informatie over invoegen of vervangen en insert-of-samenvoegen in deze [Azure-tabellen: blogbericht introductie tot Upsert en Query projectie][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="37ac9-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="37ac9-199">Procedure: een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="37ac9-199">How to: Delete an entity</span></span>
<span data-ttu-id="37ac9-200">U kunt een entiteit gemakkelijk verwijderen nadat u deze hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="37ac9-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="37ac9-201">Wanneer het Hallo-entiteit wordt opgehaald, aanroepen **TableOperation.delete** met Hallo entiteit toodelete.</span><span class="sxs-lookup"><span data-stu-id="37ac9-201">Once hello entity is retrieved, call **TableOperation.delete** with hello entity toodelete.</span></span> <span data-ttu-id="37ac9-202">Roep vervolgens **uitvoeren** op Hallo **CloudTable** object.</span><span class="sxs-lookup"><span data-stu-id="37ac9-202">Then call **execute** on hello **CloudTable** object.</span></span> <span data-ttu-id="37ac9-203">Hallo na de code opgehaald en wordt een klantentiteit verwijderd.</span><span class="sxs-lookup"><span data-stu-id="37ac9-203">hello following code retrieves and deletes a customer entity.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation toodelete hello entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit hello delete operation toohello table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a><span data-ttu-id="37ac9-204">Procedure: een tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="37ac9-204">How to: Delete a table</span></span>
<span data-ttu-id="37ac9-205">Ten slotte verwijdert hello volgende code een tabel uit een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="37ac9-205">Finally, hello following code deletes a table from a storage account.</span></span> <span data-ttu-id="37ac9-206">Een tabel die is verwijderd, is niet beschikbaar toobe opnieuw gemaakt voor een bepaalde tijd na verwijdering hello, meestal minder dan 40 seconden.</span><span class="sxs-lookup"><span data-stu-id="37ac9-206">A table which has been deleted will be unavailable toobe recreated for a period of time following hello deletion, usually less than forty seconds.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete hello table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a><span data-ttu-id="37ac9-207">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="37ac9-207">Next steps</span></span>

* <span data-ttu-id="37ac9-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u toowork visueel met Azure Storage-gegevens op Windows-, Mac OS- en Linux.</span><span class="sxs-lookup"><span data-stu-id="37ac9-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="37ac9-209">[Azure-opslag-SDK voor Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="37ac9-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="37ac9-210">[Azure Storage Client SDK-naslaginformatie][Azure Storage Client SDK-naslaginformatie]</span><span class="sxs-lookup"><span data-stu-id="37ac9-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="37ac9-211">[REST API van Azure Storage][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="37ac9-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="37ac9-212">[Azure Storage-teamblog][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="37ac9-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="37ac9-213">Zie voor meer informatie, ook Hallo [Java Developer Center](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="37ac9-213">For more information, see also hello [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure Storage Client SDK-naslaginformatie]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
