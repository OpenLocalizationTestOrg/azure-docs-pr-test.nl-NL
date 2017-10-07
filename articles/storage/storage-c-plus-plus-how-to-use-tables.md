---
title: aaaHow toouse Table storage (C++) | Microsoft Docs
description: Gestructureerde gegevens opslaan in Hallo cloud met Azure Table storage, een NoSQL-gegevensarchief.
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
ms.openlocfilehash: 8eee0031350ab6ff3f76fb288b2f896687aa17a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a>Hoe toouse Table storage uit het C++
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Overzicht
Deze handleiding leert u hoe tooperform algemene scenario's met behulp van hello Azure Table storage-service. Hallo-voorbeelden zijn geschreven in C++ en gebruiken van Hallo [Azure Storage-clientbibliotheek voor C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md). Hallo scenario's worden behandeld: **maken en het verwijderen van een tabel** en **werken met tabelentiteiten**.

> [!NOTE]
> Doel is van deze handleiding hello Azure Storage-clientbibliotheek voor C++ versie 1.0.0 en hoger. Hallo aanbevolen versie is Storage-clientbibliotheek 2.2.0, die beschikbaar is via [NuGet](http://www.nuget.org/packages/wastorage) of [GitHub](https://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Een C++-toepassing maken
In deze handleiding gebruikt u opslagfuncties dat kunnen worden uitgevoerd binnen een C++-toepassing. toodo geval is, moet u tooinstall hello Azure Storage-clientbibliotheek voor C++ en een Azure storage-account maken in uw Azure-abonnement.  

tooinstall hello Azure Storage-clientbibliotheek voor C++, kunt u Hallo volgende methoden:

* **Linux:** Hallo instructies gegeven op Hallo [Azure Storage-clientbibliotheek voor C++ Leesmij](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.  
* **Windows:** In Visual Studio, klikt u op **Extra > NuGet Package Manager > Package Manager Console**. Type Hallo volgende opdracht in Hallo [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) en druk op Enter.  
  
     Install-Package wastorage

## <a name="configure-your-application-tooaccess-table-storage"></a>Configureren van uw toepassing tooaccess Table storage
Toegevoegd Hallo volgende overzichten toohello boven in Hallo C++ bestand waar u toouse hello Azure storage-API's tooaccess tabellen bevatten:  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Een Azure-opslag-verbindingsreeks instellen
Een Azure-opslag-client maakt gebruik van een storage connection string toostore eindpunten en referenties voor toegang tot gegevens beheerservices. Wanneer een client-toepassing wordt uitgevoerd, moet u Hallo verbindingsreeks voor opslag in de volgende indeling Hallo opgeven. Gebruik Hallo de naam van uw storage-account en Hallo toegangssleutel voor opslag voor Hallo storage-account wordt vermeld in Hallo [Azure Portal](https://portal.azure.com) voor Hallo *AccountName* en *AccountKey* waarden. Zie voor informatie over de storage-accounts en toegangstoetsen, [over Azure storage-accounts](storage-create-storage-account.md). Dit voorbeeld ziet hoe u een statisch veld toohold Hallo-verbindingsreeks kunt declareren:  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest uw toepassing in uw lokale Windows-computer, kunt u hello Azure [opslagemulator](storage-use-emulator.md) die is geïnstalleerd met Hallo [Azure SDK](https://azure.microsoft.com/downloads/). Hallo-opslagemulator is een hulpprogramma dat hello Azure Blob, wachtrijen en tabellen services beschikbaar zijn op uw lokale ontwikkelcomputer simuleert. Hallo volgende voorbeeld ziet u hoe u een statisch veld toohold Hallo connection string tooyour lokale opslagemulator kunt declareren:  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart hello Azure-opslagemulator, klikt u op Hallo **Start** of drukt u op Hallo Windows-toets. Begint te typen **Azure-Opslagemulator**, en selecteer vervolgens **Microsoft Azure-Opslagemulator** in Hallo lijst met toepassingen.  

Hallo volgende voorbeelden wordt ervan uitgegaan dat u een van deze twee methoden tooget Hallo-opslagverbindingsreeks hebt gebruikt.  

## <a name="retrieve-your-connection-string"></a>De verbindingsreeks ophalen
U kunt Hallo **cloud_storage_account** klasse toorepresent gegevens over uw storage-account. tooretrieve uw opslag accountgegevens van de opslagverbindingsreeks hello, kunt u de methode parse hello gebruiken.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

Vervolgens wordt een verwijzing tooa ophalen **cloud_table_client** klasse, zoals het kunt u profiteren van reference-objecten voor tabellen en entiteiten die zijn opgeslagen in Hallo Table storage-service. Hallo volgende code maakt een **cloud_table_client** object met behulp van Hallo account opslagobject we hierboven opgehaald:  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a>Een tabel maken
Een **cloud_table_client** object kunt u profiteren van reference-objecten voor tabellen en entiteiten. Hallo volgende code maakt een **cloud_table_client** object en gebruikt deze toocreate een nieuwe tabel.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-tooa-table"></a>Een entiteit tooa tabel toevoegen
tooadd een entiteit tooa tabel, maakt u een nieuwe **table_entity** object en geef dit door te**table_operation::insert_entity**. Hallo volgende code gebruikt de voornaam van de klant Hallo als Hallo rijsleutel en de achternaam als partitiesleutel Hallo. Samen een entiteit partitie en rijsleutel een unieke identificatie Hallo entiteit in Hallo tabel. Entiteiten met dezelfde partitiesleutel kan sneller worden opgevraagd dan die met verschillende Hallo partitie-sleutels, maar met verschillende partitiesleutels kunt grotere schaalbaarheid van parallelle bewerking. Zie voor meer informatie [Microsoft Azure storage controlelijst voor prestaties en schaalbaarheid](storage-performance-checklist.md).

Hallo volgende code maakt een nieuw exemplaar van **table_entity** met sommige klant gegevens toobe opgeslagen. de volgende aanroepen code Hallo **table_operation::insert_entity** toocreate een **table_operation** object tooinsert een entiteit in een tabel en gekoppeld Hallo nieuwe Tabelentiteit met het. Ten slotte Hallo code-aanroepen Hallo methode niet uitvoeren op Hallo **cloud_table** object. En nieuwe Hallo **table_operation** verzendt een aanvraag toohello tabel service tooinsert Hallo nieuwe klantentiteit in Hallo 'gebruikers' tabel.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create hello table operation that inserts hello customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute hello insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a>Een batch entiteiten invoegen
U kunt een batch entiteiten toohello service tabel invoegen in één schrijfbewerking. Hallo volgende code maakt een **table_batch_operation** object en vervolgens voegt u drie bewerkingen tooit invoegen. Elke bewerking insert is toegevoegd door het maken van een nieuwe entiteitsobject, de waarden in te stellen en vervolgens aanroepen Hallo Voeg de methode op Hallo **table_batch_operation** object tooassociate Hallo entiteit met een nieuwe bewerking insert. Vervolgens **cloud_table.execute** tooexecute Hallo-bewerking wordt aangeroepen.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it toohello table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it toohello table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity tooadd toohello table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities toohello batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute hello batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

Een aantal dingen toonote over batchbewerkingen:  

* U kunt uitvoeren om too100 invoegen, verwijderen, samenvoegen, vervangen, invoegen of merge en invoegen of vervangen bewerkingen in een willekeurige combinatie in één batch.  
* Een batchbewerking kan een bewerking ophalen hebben als het Hallo enige bewerking in Hallo batch.  
* Alle entiteiten in een batchbewerking moeten Hallo hebben dezelfde partitiesleutel.  
* Een batchbewerking is beperkt tooa 4 MB aan gegevens nettolading.  

## <a name="retrieve-all-entities-in-a-partition"></a>Alle entiteiten in een partitie ophalen
een tabel voor alle entiteiten in een partitie, gebruik tooquery een **table_query** object. Hallo geeft volgende codevoorbeeld een filter voor entiteiten waarbij 'Smith' hello partitiesleutel is. Dit voorbeeld wordt Hallo velden van elke entiteit in Hallo query resultaten toohello-console.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct hello query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print hello fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

Hallo-query in dit voorbeeld worden alle Hallo entiteiten die overeenkomen met de filtercriteria Hallo. Als u grote tabellen hebt en toodownload Hallo tabelentiteiten vaak, raden wij aan dat u uw gegevens in Azure storage-blobs in plaats daarvan opslaat.

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>Een bereik van entiteiten in een partitie ophalen
Als u niet tooquery alle Hallo entiteiten in een partitie wilt, kunt u een bereik opgeven door een combinatie van Hallo partitie sleutel filter met een rijsleutelfilter. Hallo volgende codevoorbeeld maakt gebruik van twee filters tooget alle entiteiten in de partitie 'Smith' waarbij Hallo rijsleutel (voornaam) begint met een letter 'E' in hello alfabet vóór en vervolgens afgedrukt Hallo queryresultaten.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through hello results, displaying information about hello entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a>Eén entiteit ophalen
U kunt een query tooretrieve één specifieke entiteit schrijven. Hallo volgende code gebruikt **table_operation::retrieve_entity** toospecify Hallo klant 'Jeff Smith'. Deze methode retourneert één entiteit in plaats van een verzameling en hello geretourneerde waarde is in **table_result**. Het opgeven van de partitie-als rijsleutels in een query is Hallo snelste manier tooretrieve uit de tabelservice Hallo één entiteit.  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output hello entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a>Een entiteit vervangen
tooreplace een entiteit ophalen uit de tabelservice hello, Hallo entiteitsobject wijzigen en vervolgens weer toohello tabelservice Hallo wijzigingen opslaan. Hallo wijzigt volgende code het telefoonnummer en e-mailadres van een bestaande klant. In plaats van aanroepen **table_operation::insert_entity**, deze code gebruikt **table_operation::replace_entity**. Hierdoor Hallo entiteit toobe volledig vervangen op Hallo van server, tenzij het Hallo-entiteit op Hallo-server is gewijzigd sinds het is opgehaald, in welk geval Hallo-bewerking mislukt. Hiermee wordt de toepassing per ongeluk een wijziging overschrijft aangebracht tussen Hallo ophalen en bijwerken door een ander onderdeel van uw toepassing tooprevent. Hallo correcte verwerking van deze fout is tooretrieve Hallo entiteit opnieuw, breng uw wijzigingen (indien nog geldig) en voert u een andere **table_operation::replace_entity** bewerking. Hallo volgende sectie wordt uitgelegd hoe u toooverride dit gedrag.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation tooreplace hello entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a>Een entiteit invoegen of vervangen
**table_operation::replace_entity** bewerkingen mislukken als Hallo entiteit is gewijzigd sinds het ophalen van Hallo-server. Bovendien moet u Hallo entiteit ophalen van server eerst in de volgorde voor Hallo **table_operation::replace_entity** toobe geslaagd. Soms echter u niet weet of het Hallo entiteit op Hallo-server bestaat en Hallo van de huidige waarden die erin niet relevant zijn: de update worden deze allemaal overschreven. tooaccomplish, gebruikt u een **table_operation::insert_or_replace_entity** bewerking. Deze bewerking wordt Hallo entiteit ingevoegd als deze niet bestaat of vervangen als het geval is, ongeacht wanneer de laatste update Hallo is uitgevoerd. In Hallo volgende codevoorbeeld, Hallo klantentiteit voor Jeff Smith wordt nog steeds opgehaald, maar deze wordt vervolgens opgeslagen back toohello server via **table_operation::insert_or_replace_entity**. Eventuele updates van toohello entiteit tussen Hallo ophalen en bijwerken bewerking worden overschreven.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation tooinsert-or-replace hello entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a>Een query uitvoeren op een subset van entiteitseigenschappen
Een query tooa tabel ophalen slechts enkele eigenschappen van een entiteit. Hallo query in de volgende code Hallo gebruikt Hallo **table_query::set_select_columns** methode tooreturn alleen Hallo e-mailadressen van entiteiten in Hallo tabel.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define hello query, and select only hello Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display hello results.
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
> Opvragen van enkele eigenschappen van een entiteit is een efficiëntere bewerking dan bij het ophalen van alle eigenschappen.
> 
> 

## <a name="delete-an-entity"></a>Een entiteit verwijderen
U kunt een entiteit gemakkelijk verwijderen nadat u deze hebt opgehaald. Wanneer het Hallo-entiteit wordt opgehaald, aanroepen **table_operation::delete_entity** met Hallo entiteit toodelete. Roep vervolgens Hallo **cloud_table.execute** methode. Hallo volgende code haalt en verwijdert een entiteit met een partitiesleutel van 'Smith' en een rijsleutel van 'Jeff'.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a>Een tabel verwijderen
Ten slotte verwijdert Hallo volgende codevoorbeeld een tabel uit een opslagaccount. Een tabel die is verwijderd is niet beschikbaar toobe opnieuw worden gemaakt voor een bepaalde tijd na Hallo verwijderen.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van table storage hebt geleerd, volgt u deze koppelingen toolearn meer over Azure Storage:  

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u toowork visueel met Azure Storage-gegevens op Windows-, Mac OS- en Linux.
* [Hoe toouse C++ Blob-opslag](storage-c-plus-plus-how-to-use-blobs.md)
* [Hoe toouse Queue storage vanuit C++](storage-c-plus-plus-how-to-use-queues.md)
* [Lijst van Azure Storage-resources in C++](storage-c-plus-plus-enumeration.md)
* [Opslagclientbibliotheek voor C++-verwijzing](http://azure.github.io/azure-storage-cpp)
* [Documentatie bij Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
