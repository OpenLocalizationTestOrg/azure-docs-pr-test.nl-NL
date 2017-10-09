---
title: aaaHow toouse blob storage (objectopslag) van C++ | Microsoft Docs
description: Niet-gestructureerde gegevens opslaan in Hallo cloud met Azure Blob storage (objectopslag).
services: storage
documentationcenter: .net
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 0d7e7436a109ef54fc07cc238c03cfc7cf2caac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a>Hoe toouse C++ Blob-opslag
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Overzicht
Azure Blob storage is een service die niet-gestructureerde gegevens in de cloud Hallo als objecten/blobs opslaat. In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen. BLOB-opslag is ook bedoeld tooas vorm van objectopslag.

Deze handleiding wordt gedemonstreerd hoe tooperform algemene scenario's met behulp van hello Azure Blob storage-service. Hallo-voorbeelden zijn geschreven in C++ en gebruiken van Hallo [Azure Storage-clientbibliotheek voor C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Hallo scenario's worden behandeld: **uploaden**, **aanbieding**, **downloaden**, en **verwijderen** blobs.  

> [!NOTE]
> Doel is van deze handleiding hello Azure Storage-clientbibliotheek voor C++ versie 1.0.0 en hoger. Hallo aanbevolen versie is Storage-clientbibliotheek 2.2.0, die beschikbaar is via [NuGet](http://www.nuget.org/packages/wastorage) of [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Een C++-toepassing maken
In deze handleiding gebruikt u opslagfuncties die kunnen worden uitgevoerd binnen een C++-toepassing.  

toodo geval is, moet u tooinstall hello Azure Storage-clientbibliotheek voor C++ en een Azure storage-account maken in uw Azure-abonnement.   

tooinstall hello Azure Storage-clientbibliotheek voor C++, kunt u Hallo volgende methoden:

* **Linux:** Hallo instructies gegeven in Hallo [Azure Storage-clientbibliotheek voor C++ Leesmij](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.  
* **Windows:** In Visual Studio, klikt u op **Extra > NuGet Package Manager > Package Manager Console**. Type Hallo volgende opdracht in Hallo [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) en druk op **ENTER**.  
  
     Install-Package wastorage

## <a name="configure-your-application-tooaccess-blob-storage"></a>Uw toepassing tooaccess Blob-opslag configureren
Toegevoegd Hallo volgende overzichten toohello boven in Hallo C++ bestand waar u toouse hello Azure storage-API's tooaccess blobs bevatten:  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a>Een Azure-opslag-verbindingsreeks instellen
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

Vervolgens wordt een verwijzing tooa ophalen **cloud_blob_client** klasse omdat u tooretrieve-objecten die containers en blobs die zijn opgeslagen in Blob Storage-Service Hallo vertegenwoordigen. Hallo volgende code maakt een **cloud_blob_client** -object op met de Hallo account opslagobject we hierboven opgehaald:  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a>Procedure: een container maken
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Dit voorbeeld ziet u hoe toocreate een container als deze niet al bestaat:  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create hello blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference tooa container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create hello container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

Standaard Hallo nieuwe container privé is en u uw opslag toegang tot belangrijke toodownload blobs uit deze container moet opgeven. Als u toomake Hallo-bestanden (BLOB's) binnen hello container beschikbaar tooeveryone wilt, kunt u Hallo container toobe openbare met behulp van de volgende code Hallo instellen:  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

Iedereen op Internet Hallo blobs in een openbare container kunt zien, maar u kunt wijzigen of ze alleen verwijderen als u de juiste toegangssleutel Hallo hebt.  

## <a name="how-to-upload-a-blob-into-a-container"></a>Procedure: een blob uploaden naar een container
Azure Blob Storage ondersteunt blok-blobs en pagina-blobs. In Hallo meeste gevallen is het blok-blob Hallo type toouse aanbevolen.  

een bestand tooa blok-blob tooupload een containerverwijzing ophalen en deze tooget een blok-blobverwijzing gebruiken. Zodra u een blobverwijzing hebt, kunt u elke gewenste gegevensstroom tooit gegevens uploaden door de aanroepende Hallo **upload_from_stream** methode. Deze bewerking wordt Hallo blob gemaakt als deze niet eerder bestaat of overschrijven als het bestand bestaat. Hallo volgende voorbeeld wordt getoond hoe tooupload een blob naar een container en wordt ervan uitgegaan dat Hallo-container al is gemaakt.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite hello "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite hello "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference tooa blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

U kunt ook hello gebruiken **upload_from_file** methode tooupload een bestand tooa blok-blob.

## <a name="how-to-list-hello-blobs-in-a-container"></a>Procedure: lijst Hallo blobs in een container
toolist hello blobs in een container, eerst ophalen een containerverwijzing. Vervolgens kunt u Hallo-container **list_blobs** methode tooretrieve Hallo blobs en/of mappen hierin. tooaccess Hallo uitgebreide set eigenschappen en methoden voor een geretourneerde **list_blob_item**, moet u Hallo aanroepen **list_blob_item.as_blob** methode tooget een **cloud_blob** -object of Hallo **list_blob.as_directory** methode tooget een cloud_blob_directory-object. Hallo volgende code laat zien hoe tooretrieve en uitvoer URI van elk item in Hallo Hallo **mijn-voorbeeld-container** container:

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

Zie voor meer informatie over het weergeven van bewerkingen [lijst Azure Storage-Resources in C++](storage-c-plus-plus-enumeration.md).

## <a name="how-to-download-blobs"></a>Hoe: blobs downloaden
toodownload blobs, eerst een blobverwijzing ophalen en vervolgens aanroepen Hallo **download_to_stream** methode. Hallo volgende voorbeeld wordt Hallo **download_to_stream** methode tootransfer Hallo blob inhoud tooa stroomobject dat u vervolgens blijven tooa lokaal bestand behouden kunt.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents tooa file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

U kunt ook hello gebruiken **download_to_file** methode toodownload Hallo inhoud van een blob tooa-bestand.
Bovendien kunt u ook hello gebruiken **download_text** methode toodownload Hallo inhoud van een blob als een tekenreeks.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download hello contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a>Hoe: blobs verwijderen
een blob toodelete eerst een blobverwijzing ophalen en vervolgens aanroepen Hallo **delete_blob** methode erop.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete hello blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van blob storage hebt geleerd, volgt u deze koppelingen toolearn meer over Azure Storage.  

* [Hoe toouse Queue Storage vanuit C++](storage-c-plus-plus-how-to-use-queues.md)
* [Hoe toouse Table Storage uit het C++](storage-c-plus-plus-how-to-use-tables.md)
* [Lijst met Azure Storage-Resources in C++](storage-c-plus-plus-enumeration.md)
* [Opslagclientbibliotheek voor C++-verwijzing](http://azure.github.io/azure-storage-cpp)
* [Documentatie bij Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Gegevensoverdracht met Hallo AzCopy-opdrachtregelprogramma](storage-use-azcopy.md)

