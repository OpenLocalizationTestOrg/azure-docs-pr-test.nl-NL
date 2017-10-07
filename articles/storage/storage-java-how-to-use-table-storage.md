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
# <a name="how-toouse-table-storage-from-java"></a>Hoe toouse Table storage met Java
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Overzicht
Deze handleiding leert u hoe tooperform algemene scenario's met behulp van hello Azure Table storage-service. Hallo-voorbeelden zijn geschreven in Java en gebruiken van Hallo [Azure-opslag-SDK voor Java][Azure Storage SDK for Java]. Hallo scenario's worden behandeld: **maken**, **aanbieding**, en **verwijderen** tabellen, evenals **invoegen**,  **uitvoeren van query's**, **wijzigen**, en **verwijderen** entiteiten in een tabel. Zie voor meer informatie over tabellen Hallo [Vervolgstappen](#Next-Steps) sectie.

Opmerking: Een SDK is beschikbaar voor ontwikkelaars die werken met Azure Storage op Android-apparaten. Zie voor meer informatie, Hallo [Azure-opslag-SDK voor Android][Azure Storage SDK for Android].

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Een Java-toepassing maken
In deze handleiding gebruikt u opslagfuncties die kunnen worden uitgevoerd binnen een Java-toepassing lokaal of in de code die wordt uitgevoerd binnen een Webrol of worker-rol in Azure.

toodo geval is, moet u tooinstall Hallo Java Development Kit (JDK) en een Azure storage-account maken in uw Azure-abonnement. Nadat u dit hebt gedaan, moet u tooverify dat uw ontwikkelsysteem voldoet aan de minimumvereisten Hallo en afhankelijkheden die worden vermeld in Hallo [Azure-opslag-SDK voor Java] [ Azure Storage SDK for Java] opslagplaats op GitHub. Als uw systeem aan deze vereisten voldoet, kunt u de instructies voor het downloaden en installeren van hello Azure Storage-bibliotheken voor Java op uw systeem vanuit die opslagplaats Hallo volgen. Nadat u deze taken hebt voltooid, kunt u zich kunt toocreate een Java-toepassing die gebruikmaakt van Hallo voorbeelden in dit artikel.

## <a name="configure-your-application-tooaccess-table-storage"></a>Uw toepassing tooaccess tabelopslag configureren
Hallo na importeren instructies toohello bovenaan Hallo Java bestand waar u toouse Microsoft Azure storage-API's tooaccess tabellen toevoegen:

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Een Azure-opslag-verbindingsreeks instellen
Een Azure-opslag-client maakt gebruik van een storage connection string toostore eindpunten en referenties voor toegang tot gegevens beheerservices. Wanneer een client-toepassing wordt uitgevoerd, moet u bieden Hallo verbindingsreeks voor opslag in Hallo indeling te volgen, met behulp van Hallo-naam van uw opslagaccount en primaire toegangssleutel voor opslagaccount Hallo die worden vermeld in Hallo Hallo [Azure-portal](https://portal.azure.com)voor Hallo *AccountName* en *AccountKey* waarden. Dit voorbeeld ziet hoe u een statisch veld toohold Hallo-verbindingsreeks kunt declareren:

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

In een toepassing in een rol in Microsoft Azure wordt uitgevoerd, kan deze tekenreeks worden opgeslagen in Hallo serviceconfiguratiebestand, *ServiceConfiguration.cscfg*, en kunnen worden geopend met een aanroep van toohello  **RoleEnvironment.getConfigurationSettings** methode. Hier volgt een voorbeeld van het ophalen van Hallo-verbindingsreeks uit een **instelling** element met de naam *StorageConnectionString* in Hallo serviceconfiguratiebestand:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Hallo volgende voorbeelden wordt ervan uitgegaan dat u een van deze twee methoden tooget Hallo-opslagverbindingsreeks hebt gebruikt.

## <a name="how-to-create-a-table"></a>Procedure: een tabel maken
Een **CloudTableClient** object kunt u profiteren van reference-objecten voor tabellen en entiteiten. Hallo volgende code maakt een **CloudTableClient** object en gebruikt deze toocreate een nieuwe **CloudTable** -object met een tabel met de naam 'mensen'. (Opmerking: Er zijn extra manieren toocreate **CloudStorageAccount** objecten; voor meer informatie Zie **CloudStorageAccount** in Hallo [Azure Storage Client SDK-naslaginformatie].)

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

## <a name="how-to-list-hello-tables"></a>Hoe: Hallo tabellen
een lijst met tabellen, aanroep Hallo tooget **CloudTableClient.listTables()** methode tooretrieve een iterable lijst met namen van tabellen.

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

## <a name="how-to-add-an-entity-tooa-table"></a>Procedure: een entiteit tooa tabel toevoegen
Entiteiten worden toegewezen tooJava objecten met behulp van de implementatie van een aangepaste klasse **TableEntity**. Voor het gemak Hallo **TableServiceEntity** klasse implementeert **TableEntity** en maakt gebruik van reflectie toomap eigenschappen toogetter en setter methoden met de naam van Hallo eigenschappen. een tabel entity tooa tooadd eerst een klasse die eigenschappen Hallo van uw entiteit definieert maken. Hallo definieert volgende code een entiteitsklasse dat gebruikmaakt van de voornaam van de klant Hallo als Hallo rijsleutel en de achternaam als partitiesleutel Hallo. Samen een entiteit partitie en rijsleutel een unieke identificatie Hallo entiteit in Hallo tabel. Entiteiten met dezelfde partitiesleutel kan sneller worden opgevraagd dan die met verschillende partitiesleutels Hallo.

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

Tabelbewerkingen met betrekking tot entiteiten vereist een **TableOperation** object. Dit object definieert Hallo bewerking toobe uitgevoerd op een entiteit die kan worden uitgevoerd met een **CloudTable** object. Hallo volgende code maakt een nieuw exemplaar van Hallo **CustomerEntity** klasse met sommige klant gegevens toobe opgeslagen. de volgende aanroepen code Hallo **TableOperation.insertOrReplace** toocreate een **TableOperation** object tooinsert een entiteit in een tabel en gekoppeld Hallo nieuwe **CustomerEntity**aan. Ten slotte Hallo code roept Hallo **uitvoeren** methode op Hallo **CloudTable** -object, waarbij Hallo 'gebruikers' tabel en nieuw Hallo **TableOperation**, welke vervolgens verzendt een aanvragen van toohello opslag service tooinsert Hallo nieuwe klantentiteit in Hallo 'gebruikers' tabel of Hallo entiteit vervangen als deze al bestaat.

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

## <a name="how-to-insert-a-batch-of-entities"></a>Procedure: een batch entiteiten invoegen
U kunt een batch entiteiten toohello tabelservice invoegen in één schrijfbewerking. Hallo volgende code maakt een **TableBatchOperation** object en vervolgens voegt u drie bewerkingen tooit invoegen. Elke bewerking insert is toegevoegd door het maken van een nieuwe entiteitsobject, de waarden in te stellen en vervolgens aanroepen Hallo **invoegen** methode op Hallo **TableBatchOperation** tooassociate Hallo entiteit met een nieuw object bewerking INSERT. Vervolgens Hallo code aanroepen **uitvoeren** op Hallo **CloudTable** -object, waarbij Hallo 'gebruikers' tabel en Hallo **TableBatchOperation** -object, dat Hallo batch van tabel verzendt bewerkingen toohello storage-service in een afzonderlijke aanvraag.

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

Een aantal dingen toonote over batchbewerkingen:

* U kunt uitvoeren om too100 invoegen, verwijderen, samenvoegen, vervangen, invoegen of samenvoegen, en invoegen of vervangen door bewerkingen in een willekeurige combinatie in één batch.
* Een batchbewerking kan een bewerking ophalen hebben als het Hallo enige bewerking in Hallo batch.
* Alle entiteiten in een batchbewerking moeten Hallo hebben dezelfde partitiesleutel.
* Een batchbewerking is beperkt tooa 4MB-nettolading.

## <a name="how-to-retrieve-all-entities-in-a-partition"></a>Hoe: alle entiteiten in een partitie ophalen
een tabel voor entiteiten in een partitie tooquery, kunt u een **TableQuery**. Roep **TableQuery.from** toocreate een query op een bepaalde tabel die een resultaattype opgegeven retourneert. Hallo geeft volgende code een filter voor entiteiten waarbij 'Smith' hello partitiesleutel is. **TableQuery.generateFilterCondition** toocreate filters voor query's van een Help-methode is. Roep **waar** op Hallo verwijzing geretourneerd door Hallo **TableQuery.from** methode tooapply Hallo-filterquery toohello. Wanneer Hallo query wordt uitgevoerd met een aanroep te**uitvoeren** op Hallo **CloudTable** object, wordt een **Iterator** Hello **CustomerEntity**resultaattype opgegeven. Vervolgens kunt u Hallo **Iterator** geretourneerd in een voor elke lus tooconsume Hallo resultaten. Deze code wordt Hallo velden van elke entiteit in Hallo query resultaten toohello console afgedrukt.

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

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a>Procedure: een bereik van entiteiten in een partitie ophalen
Als u niet tooquery alle Hallo entiteiten in een partitie wilt, kunt u een bereik met behulp van vergelijkingsoperators in een filter opgeven. Hallo code combineert twee filters tooget alle entiteiten in de partitie 'Smith' waar Hallo rijsleutel (voornaam) begint met een letter up too'E na ' in hello alfabet. Vervolgens worden de queryresultaten Hallo afgedrukt. Als u Hallo entiteiten toegevoegde toohello tabel in batch Hallo invoegen van deze handleiding, worden slechts twee entiteiten geretourneerd ditmaal (Ben en Denise Smith); Jeff Smith is niet opgenomen.

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

## <a name="how-to-retrieve-a-single-entity"></a>Hoe: Eén entiteit ophalen
U kunt een query tooretrieve één specifieke entiteit schrijven. Hallo volgende code aanroepen **TableOperation.retrieve** met partitie-sleutel en rij belangrijke parameters toospecify Hallo klant 'Jeff Smith', in plaats van het maken van een **TableQuery** en filters toodo hello gebruiken hetzelfde geldt. Bij uitvoering ophalen Hallo bewerking retourneert één entiteit in plaats van een verzameling. Hallo **getResultAsType** methode cast Hallo resultaattype toohello van Hallo toewijzing target, een **CustomerEntity** object. Als u dit type is niet compatibel met het Hallo-type opgegeven voor Hallo query, wordt er een uitzondering opgetreden. Als er is geen entiteit heeft een exacte partitie en de rijsleutel overeen met een null-waarde geretourneerd. Het opgeven van de partitie-als rijsleutels in een query is Hallo snelste manier tooretrieve uit de tabelservice Hallo één entiteit.

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

## <a name="how-to-modify-an-entity"></a>Procedure: een entiteit wijzigen
toomodify een entiteit ophalen uit de tabelservice hello, wijzigingen toohello entiteitsobject, wijzigingen aanbrengen en opslaan Hallo back toohello tabel-service met een vervangings- of merge-bewerking. Hallo wijzigt volgende code het telefoonnummer van een bestaande klant. In plaats van aanroepen **TableOperation.insert** zoals we tooinsert hebt gedaan, wordt deze code roept **TableOperation.replace**. Hallo **CloudTable.execute** tabelservice Hallo-methodeaanroepen en Hallo entiteit wordt vervangen, tenzij een andere toepassing gewijzigd het Hallo tijdig sinds deze toepassing wordt opgehaald. Wanneer dit gebeurt, is een uitzondering opgetreden en Hallo entiteit moet worden opgehaald, gewijzigd en opnieuw worden opgeslagen. Dit patroon van een nieuwe poging optimistische gelijktijdigheid is gemeenschappelijk in een gedistribueerd opslagsysteem.

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

## <a name="how-to-query-a-subset-of-entity-properties"></a>Hoe: query uitvoeren op een subset van entiteitseigenschappen
Een query tooa tabel ophalen slechts enkele eigenschappen van een entiteit. Deze methode, projectie genoemd, verbruikt minder bandbreedte en kan de queryprestaties verbeteren, vooral bij grote entiteiten. Hallo query in de volgende code Hallo gebruikt Hallo **Selecteer** methode tooreturn alleen Hallo e-mailadressen van entiteiten in Hallo tabel. Hello zijn resultaten geprojecteerd in een verzameling van **tekenreeks** met behulp van Hallo een **EntityResolver**, dat typeconversie op Hallo entiteiten geretourneerd vanaf de server Hallo Hallo. U kunt meer informatie over projectie in [Azure-tabellen: blogbericht introductie tot Upsert en Query projectie][Azure Tables: Introducing Upsert and Query Projection]. Houd er rekening mee dat projectie niet wordt ondersteund op Hallo-emulator voor lokale opslag, zodat deze code wordt alleen uitgevoerd als met een account op Hallo tabel-service.

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

## <a name="how-to-insert-or-replace-an-entity"></a>Hoe: invoegen of vervangen van een entiteit
U vaak een entiteit tooa tabel tooadd zonder te weten te komen of deze al in de tabel Hallo voorkomt. Een bewerking voor invoegen of vervangen, kunt u toomake één aanvraag die Hallo entiteit wordt ingevoegd als deze bestaat niet of u een bestaande als dit wel Hallo vervangen. Voortbouwend op de eerdere voorbeelden, hello volgende code wordt ingevoegd of vervangen Hallo entiteit voor 'Walter Harp'. Na het maken van een nieuwe entiteit deze code roept Hallo **TableOperation.insertOrReplace** methode. Deze code roept vervolgens **uitvoeren** op Hallo **CloudTable** object met Hallo tabel en Hallo invoegen of vervangen als Hallo parameters van een tabel is. slechts een deel van een entiteit tooupdate hello **TableOperation.insertOrMerge** methode in plaats daarvan kan worden gebruikt. Houd er rekening mee dat invoegen of vervangen wordt niet ondersteund op Hallo-emulator voor lokale opslag, zodat deze code wordt alleen uitgevoerd als met een account op Hallo tabel-service. U kunt meer informatie over invoegen of vervangen en insert-of-samenvoegen in deze [Azure-tabellen: blogbericht introductie tot Upsert en Query projectie][Azure Tables: Introducing Upsert and Query Projection].

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

## <a name="how-to-delete-an-entity"></a>Procedure: een entiteit verwijderen
U kunt een entiteit gemakkelijk verwijderen nadat u deze hebt opgehaald. Wanneer het Hallo-entiteit wordt opgehaald, aanroepen **TableOperation.delete** met Hallo entiteit toodelete. Roep vervolgens **uitvoeren** op Hallo **CloudTable** object. Hallo na de code opgehaald en wordt een klantentiteit verwijderd.

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

## <a name="how-to-delete-a-table"></a>Procedure: een tabel verwijderen
Ten slotte verwijdert hello volgende code een tabel uit een opslagaccount. Een tabel die is verwijderd, is niet beschikbaar toobe opnieuw gemaakt voor een bepaalde tijd na verwijdering hello, meestal minder dan 40 seconden.

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

## <a name="next-steps"></a>Volgende stappen

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u toowork visueel met Azure Storage-gegevens op Windows-, Mac OS- en Linux.
* [Azure-opslag-SDK voor Java][Azure Storage SDK for Java]
* [Azure Storage Client SDK-naslaginformatie][Azure Storage Client SDK-naslaginformatie]
* [REST API van Azure Storage][Azure Storage REST API]
* [Azure Storage-teamblog][Azure Storage Team Blog]

Zie voor meer informatie, ook Hallo [Java Developer Center](/develop/java/).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure Storage Client SDK-naslaginformatie]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
