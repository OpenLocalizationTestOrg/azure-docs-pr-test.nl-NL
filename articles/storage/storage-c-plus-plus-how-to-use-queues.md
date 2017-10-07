---
title: aaaHow toouse queue storage (C++) | Microsoft Docs
description: Meer informatie over hoe toouse Hallo queue storage-service in Azure. Voorbeelden zijn geschreven in C++.
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: jahogg
editor: tysonn
ms.assetid: c8a36365-29f6-404d-8fd1-858a7f33b50a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 05/11/2017
ms.author: cbrooksmsft
ms.openlocfilehash: 755380824890ad83774e14d258975915e10cfede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-c"></a>Hoe toouse Queue Storage vanuit C++
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Overzicht
Deze handleiding leert u hoe tooperform algemene scenario's met behulp van hello Azure Queue storage-service. Hallo-voorbeelden zijn geschreven in C++ en gebruiken van Hallo [Azure Storage-clientbibliotheek voor C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Hallo scenario's worden behandeld: **invoegen**, **inspecteren**, **ophalen**, en **verwijderen** wachtrij berichten, evenals  **maken en verwijderen van wachtrijen**.

> [!NOTE]
> Doel is van deze handleiding hello Azure Storage-clientbibliotheek voor C++ versie 1.0.0 en hoger. Hallo aanbevolen versie is Storage-clientbibliotheek 2.2.0, die beschikbaar is via [NuGet](http://www.nuget.org/packages/wastorage) of [GitHub](http://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Een C++-toepassing maken
In deze handleiding gebruikt u opslagfuncties die kunnen worden uitgevoerd binnen een C++-toepassing.

toodo geval is, moet u tooinstall hello Azure Storage-clientbibliotheek voor C++ en een Azure storage-account maken in uw Azure-abonnement.

tooinstall hello Azure Storage-clientbibliotheek voor C++, kunt u Hallo volgende methoden:

* **Linux:** Hallo instructies gegeven in Hallo [Azure Storage-clientbibliotheek voor C++ Leesmij](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.
* **Windows:** In Visual Studio, klikt u op **Extra > NuGet Package Manager > Package Manager Console**. Type Hallo volgende opdracht in Hallo [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) en druk op **ENTER**.

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a>Uw toepassing tooaccess Queue Storage configureren
Toegevoegd Hallo volgende overzichten toohello boven in Hallo C++ bestand waar u toouse hello Azure storage-API's tooaccess wachtrijen bevatten:  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Een Azure-opslag-verbindingsreeks instellen
Een Azure-opslag-client maakt gebruik van een storage connection string toostore eindpunten en referenties voor toegang tot gegevens beheerservices. Wanneer een client-toepassing wordt uitgevoerd, moet u opgeven Hallo verbindingsreeks voor opslag in Hallo indeling te volgen, met behulp van Hallo-naam van uw storage-account en Hallo toegangssleutel voor opslag voor Hallo storage-account die worden vermeld in Hallo [Azure Portal](https://portal.azure.com)voor Hallo *AccountName* en *AccountKey* waarden. Zie voor informatie over de storage-accounts en toegangstoetsen, [over Azure Storage-Accounts](storage-create-storage-account.md). Dit voorbeeld ziet hoe u een statisch veld toohold Hallo-verbindingsreeks kunt declareren:  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest uw toepassing in de lokale Windows-computer, kunt u Microsoft Azure Hallo [opslagemulator](storage-use-emulator.md) die is geïnstalleerd met Hallo [Azure SDK](https://azure.microsoft.com/downloads/). Hallo-opslagemulator is een hulpprogramma dat Hallo Blob, wachtrijen en tabellen services beschikbaar zijn in Azure op uw lokale ontwikkelcomputer simuleert. Hallo volgende voorbeeld ziet u hoe u een statisch veld toohold Hallo connection string tooyour lokale opslagemulator kunt declareren:  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart hello Azure-opslagemulator Selecteer Hallo **Start** of drukt u op Hallo **Windows** sleutel. Begint te typen **Azure-Opslagemulator**, en selecteer **Microsoft Azure-Opslagemulator** in Hallo lijst met toepassingen.

Hallo volgende voorbeelden wordt ervan uitgegaan dat u een van deze twee methoden tooget Hallo-opslagverbindingsreeks hebt gebruikt.

## <a name="retrieve-your-connection-string"></a>De verbindingsreeks ophalen
U kunt Hallo **cloud_storage_account** klasse toorepresent uw Storage-Account. tooretrieve uw opslag accountgegevens van de opslagverbindingsreeks hello, kunt u Hallo **parseren** methode.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a>Procedure: een wachtrij maken
Een **cloud_queue_client** object kunt u profiteren van reference-objecten voor wachtrijen. Hallo volgende code maakt een **cloud_queue_client** object.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

Gebruik Hallo **cloud_queue_client** tooget een verwijzing toohello wachtrij die u wilt dat toouse object. U kunt Hallo wachtrij maken als deze niet bestaat.

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Procedure: een bericht in een wachtrij invoegen
een bericht in een bestaande wachtrij tooinsert eerst maakt u een nieuwe **cloud_queue_message**. Daarna roept Hallo **add_message** methode. Een **cloud_queue_message** kan worden gemaakt vanuit een tekenreeks of een **byte** matrix. Hier volgt de code die een wachtrij maakt (als deze niet bestaat) en voegt het Hallo-bericht 'Hello, World':

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it toohello queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-hello-next-message"></a>Hoe: bekijken van volgende Hallo-bericht
U kunt bekijken van Hallo-bericht in Hallo begin van een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aanroepen Hallo **peek_message** methode.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at hello next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output hello message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Hoe: Hallo inhoud van een bericht in de wachtrij wijzigen
U kunt Hallo inhoud van een bericht in-place in Hallo wachtrij wijzigen. Als het Hallo-bericht een werktaak vertegenwoordigt, kunt u deze functie tooupdate Hallo status van de werktaak hello gebruiken. Hallo na code Hallo-bericht van wachtrij bijgewerkt met nieuwe inhoud en sets Hallo zichtbaarheid time-out tooextend 60 seconden. Hallo-status van de werkitems die zijn gekoppeld aan het Hallo-bericht opgeslagen, en geeft Hallo-client een andere minuut toocontinue werkt op het Hallo-bericht. U kunt deze techniek tootrack meerdere stappen bestaande werkstromen op Wachtrijberichten, zonder toostart via van Hallo begin als een verwerkingsstap vanwege problemen met toohardware of software. Doorgaans houdt u ook een aantal voor nieuwe pogingen en als het Hallo-bericht is meer dan n keren geprobeerd, verwijdert u het. Dit biedt bescherming tegen berichten die een toepassingsfout activeren telkens wanneer ze worden verwerkt.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello message from hello queue and update hello message contents.
// hello visibility timeout "0" means make it visible immediately.
// hello visibility timeout "60" means hello client can get another minute toocontinue
// working on hello message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output hello message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-hello-next-message"></a>Procedure: het volgende Hallo-bericht uit de wachtrij
Met uw code wordt een bericht in twee stappen uit de wachtrij verwijderd. Als u aanroept **get_message**, krijgt u het volgende Hallo-bericht in een wachtrij. Een bericht dat wordt geretourneerd door **get_message** wordt onzichtbaar tooany andere codes die berichten lezen uit deze wachtrij. toofinish verwijderen Hallo-bericht uit de wachtrij hello, moet u ook aanroepen **delete_message**. Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat als uw code mislukt tooprocess een bericht vanwege problemen toohardware of software, een ander exemplaar van uw code krijgt hetzelfde bericht Hallo en probeer het opnieuw. Uw code haalt **delete_message** direct nadat het Hallo-bericht is verwerkt.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete hello message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a>Hoe: gebruikmaken van aanvullende opties voor berichten in de wachtrij plaatsen
Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen. U krijgt eerst een batch met berichten (omhoog too32). Ten tweede kunt u instellen een time-out voor onzichtbaarheid langer of korter, zodat uw code meer of minder tijd toofully elk bericht niet verwerken. Hallo volgende codevoorbeeld maakt gebruik van Hallo **get_messages** methode tooget 20 berichten in één aanroep. Vervolgens wordt verwerkt elke bericht met een **voor** lus. Hallo onzichtbaarheid toofive minuten voor de time-out voor elk bericht wordt ook ingesteld. Houd er rekening mee dat Hallo 5 minuten voor alle berichten op Hallo dezelfde time begint, betekent dat als er 5 minuten zijn verstreken sinds de aanroep hello te**get_messages**, alle berichten die niet zijn verwijderd weer zichtbaar worden.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display hello contents of hello message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-hello-queue-length"></a>Hoe: Hallo wachtrijlengte ophalen
U kunt een schatting maken van het aantal berichten Hallo krijgen in een wachtrij. Hallo **download_attributes** methode vraagt Hallo wachtrij service tooretrieve Hallo wachtrij-kenmerken, zoals aantal Hallo-berichten. Hallo **approximate_message_count** methode Hallo kunt u het geschatte aantal berichten in wachtrij Hallo opgehaald.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch hello queue attributes.
queue.download_attributes();

// Retrieve hello cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a>Procedure: een wachtrij verwijderen
een wachtrij en alle Hallo-berichten die zijn opgenomen in deze aanroep Hallo toodelete **delete_queue_if_exists** methode op Hallo wachtrij-object.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If hello queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van Queue storage hebt geleerd, volgt u deze koppelingen toolearn meer over Azure Storage.

* [Hoe toouse C++ Blob-opslag](storage-c-plus-plus-how-to-use-blobs.md)
* [Hoe toouse Table Storage uit het C++](storage-c-plus-plus-how-to-use-tables.md)
* [Lijst met Azure Storage-Resources in C++](storage-c-plus-plus-enumeration.md)
* [Opslagclientbibliotheek voor C++-verwijzing](http://azure.github.io/azure-storage-cpp)
* [Documentatie bij Azure Storage](https://azure.microsoft.com/documentation/services/storage/)