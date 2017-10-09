---
title: aaaDevelop voor Azure File storage met C++ | Microsoft Docs
description: Meer informatie over hoe toodevelop C++-toepassingen en services die gebruikmaken van Azure File storage toostore bestandsgegevens.
services: storage
documentationcenter: .net
author: renashahmsft
manager: aungoo
editor: tysonn
ms.assetid: a1e8c99e-47a6-43a9-9541-c9262eb00b38
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: renashahmsft
ms.openlocfilehash: 48f668cf9359f88baeaaa08ee0d44e70bd0f5f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a>Ontwikkelen voor Azure File storage met C++
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Over deze zelfstudie

In deze zelfstudie leert u hoe tooperform basisbewerkingen op Azure File storage. Door steekproeven geschreven in C++, leert u hoe toocreate deelt en mappen, uploaden, weergeven en verwijderen van bestanden. Als u nieuwe tooAzure File storage, wordt gaan via Hallo concepten Hallo die in volgende secties nuttig zijn Hallo voorbeelden begrijpen.


* Maken en verwijderen van de Azure-bestandsshares
* Maken en verwijderen van mappen
* Bestanden en mappen in een Azure-bestandsshare opsommen
* Uploaden, downloaden en een bestand verwijderen
* Hallo quotum (maximumgrootte) voor een Azure-bestandsshare instellen
* Maak een shared access signature (SAS-sleutel) voor een bestand dat gebruikmaakt van een gedeeld toegangsbeleid dat is gedefinieerd op Hallo-share.

> [!Note]  
> Omdat Azure File storage zijn toegankelijk via SMB, is het mogelijk toowrite eenvoudige toepassingen die toegang hebben tot hello Azure bestandsshare met behulp van Hallo standard C++ i/o-klassen en -functies. In dit artikel wordt beschreven hoe toowrite toepassingen die gebruikmaken van Azure Storage C++ SDK, die gebruikmaakt van Hallo Hallo [Azure File storage REST-API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.

## <a name="create-a-c-application"></a>Een C++-toepassing maken
Voorbeelden van toobuild hello, moet u tooinstall hello Azure Storage-clientbibliotheek 2.4.0 voor C++. U moet hebt een Azure storage-account ook gemaakt.

tooinstall hello Azure Storage Client 2.4.0 voor C++, kunt u een van de volgende methoden hello gebruiken:

* **Linux:** Hallo instructies gegeven in Hallo [Azure Storage-clientbibliotheek voor C++ Leesmij](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.
* **Windows:** In Visual Studio, klikt u op **extra &gt; NuGet Package Manager &gt; Package Manager Console**. Type Hallo volgende opdracht in Hallo [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) en druk op **ENTER**.
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a>Instellen van uw toepassing toouse Azure File storage
Toegevoegd volgende Hallo bevatten instructies toohello bovenaan Hallo C++-bronbestand waar u toomanipulate Azure File storage:

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Een Azure-opslag-verbindingsreeks instellen
toouse opslag van bestanden, moet u tooconnect tooyour Azure storage-account. Hallo eerste stap zou zijn tooconfigure een verbindingsreeks, we gebruiken tooconnect tooyour storage-account. We gaan een statische variabele toodo definiëren die.

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a>Verbinding maken met tooan Azure storage-account
U kunt Hallo **cloud_storage_account** klasse toorepresent uw Storage-Account. tooretrieve uw opslag accountgegevens van de opslagverbindingsreeks hello, kunt u Hallo **parseren** methode.

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a>Een Azure-bestandsshare maken
Alle bestanden en mappen in Azure File storage bevinden zich in een zogenaamd een **Share**. Uw storage-account kan als veel shares als de capaciteit van uw account kunt hebben. tooobtain toegang tooa share en de inhoud ervan, moet u een Azure File storage client toouse.

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

U kunt vervolgens een verwijzing tooa share verkrijgen met behulp van hello Azure File storage client.

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

Gebruik Hallo-share Hallo toocreate **create_if_not_exists** methode Hallo **cloud_file_share** object.

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

Op dit moment **delen** bevat een verwijzing tooa share met de naam **mijn-voorbeeld-share**.

## <a name="delete-an-azure-file-share"></a>Verwijderen van een Azure-bestandsshare
Verwijderen van een share wordt uitgevoerd door de aanroepende Hallo **delete_if_exists** methode voor het object cloud_file_share. Hier volgt voorbeeldcode die dat doet.

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a>Een map maken
U kunt opslag indelen door de bestanden in submappen in plaats van ze allemaal in de hoofdmap Hallo gegevens. Azure File storage, kunt u toocreate veel mappen als uw account wordt toegestaan. Hallo-code hieronder maakt u een map met de naam **mijn-voorbeeld-directory** onder de hoofdmap hello, evenals een submap met de naam **mijn-voorbeeld-submap**.

```cpp
// Retrieve a reference tooa directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if hello share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a>Een map verwijderen
Als u een map is een eenvoudige taak, maar houd er rekening mee dat u een map met nog steeds bestanden of andere mappen niet verwijderen.

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference toohello directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference toohello subdirectory you want toodelete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete hello subdirectory and hello sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Bestanden en mappen in een Azure-bestandsshare opsommen
Eenvoudig het verkrijgen van een lijst met bestanden en mappen in een share wordt gedaan door het aanroepen van **list_files_and_directories** op een **cloud_file_directory** verwijzing. tooaccess Hallo uitgebreide set eigenschappen en methoden voor een geretourneerde **list_file_and_directory_item**, moet u Hallo aanroepen **list_file_and_directory_item.as_file** methode tooget een **cloud_ bestand** object of Hallo **list_file_and_directory_item.as_directory** methode tooget een **cloud_file_directory** object.

Hallo volgende code laat zien hoe tooretrieve en uitvoer Hallo URI van elk item in de hoofdmap Hallo Hallo-share.

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

// Output URI of each item.
azure::storage::list_file_and_diretory_result_iterator end_of_results;

for (auto it = directory.list_files_and_directories(); it != end_of_results; ++it)
{
    if(it->is_directory())
    {
        ucout << "Directory: " << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
    else if (it->is_file())
    {
        ucout << "File: " << it->as_file().uri().primary_uri().to_string() << std::endl;
    }        
}
```

## <a name="upload-a-file"></a>Bestand uploaden
Op Hallo zeer minste, bevat een Azure-bestandsshare de hoofdmap waarin de bestanden kunnen zich bevinden. In deze sectie leert u hoe een bestand van de lokale opslag op Hallo tooupload de hoofdmap van een share.

Hallo eerste stap bij het uploaden van een bestand is tooobtain een verwijzing toohello map waarin dit zich moet bevinden. Dit doet u door de aanroepende Hallo **get_root_directory_reference** methode van Hallo share-object.

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

Nu dat u de hoofdmap van een verwijzing toohello van Hallo-share hebt, kunt u een bestand op deze uploaden. In dit voorbeeld bestandsuploads uit een bestand, tekst en een stroom.

```cpp
// Upload a file from a stream.
concurrency::streams::istream input_stream = 
  concurrency::streams::file_stream<uint8_t>::open_istream(_XPLATSTR("DataFile.txt")).get();

azure::storage::cloud_file file1 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));
file1.upload_from_stream(input_stream);

// Upload some files from text.
azure::storage::cloud_file file2 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
file2.upload_text(_XPLATSTR("more text"));

// Upload a file from a file.
azure::storage::cloud_file file4 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));
file4.upload_from_file(_XPLATSTR("DataFile.txt"));    
```

## <a name="download-a-file"></a>Bestand downloaden
toodownload bestanden, eerst ophalen van een bestandsverwijzing en vervolgens aanroepen Hallo **download_to_stream** methode tootransfer Hallo bestand inhoud tooa stream-object, dat u vervolgens kunt blijven behouden tooa lokaal bestand. U kunt ook hello gebruiken **download_to_file** methode toodownload Hallo inhoud van een lokaal bestand tooa-bestand. U kunt Hallo **download_text** methode toodownload Hallo inhoud van een bestand als een tekenreeks.

Hallo volgende voorbeeld wordt Hallo **download_to_stream** en **download_text** methoden toodemonstrate Hallo-bestanden die zijn gemaakt in de vorige secties downloaden.

```cpp
// Download as text
azure::storage::cloud_file text_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
utility::string_t text = text_file.download_text();
ucout << "File Text: " << text << std::endl;

// Download as a stream.
azure::storage::cloud_file stream_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
stream_file.download_to_stream(output_stream);
std::ofstream outfile("DownloadFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();
outfile.write((char *)&data[0], buffer.size());
outfile.close();
```

## <a name="delete-a-file"></a>Een bestand verwijderen
Een andere algemene Azure File storage-bewerking wordt verwijderen van bestanden. Hallo verwijdert volgende code een bestand met de naam my-voorbeeld-bestand-3 opgeslagen onder Hallo-hoofdmap.

```cpp
// Get a reference toohello root directory for hello share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a>Hallo quotum (maximumgrootte) voor een Azure-bestandsshare instellen
U kunt Hallo quotum (of de maximale grootte) instellen voor een bestandsshare, in gigabytes. U kunt ook controleren hoeveel gegevens er momenteel zijn opgeslagen op Hallo share toosee.

Door de instelling Hallo quotum voor een share, kunt u Hallo totale grootte van bestanden op Hallo share Hallo beperken. Als Hallo totale grootte van bestanden op Hallo share overschrijdt Hallo quota ingesteld voor de share Hallo en clients worden niet kan tooincrease Hallo grootte van de bestaande bestanden of nieuwe bestanden maken, tenzij deze bestanden leeg zijn.

Hallo voorbeeld hieronder ziet u hoe toocheck huidige gebruik voor een share Hallo en hoe tooset quotum voor de share Hallo Hallo.

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets hello quota too2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Een Shared Access Signature genereren voor een bestand of bestandsshare
U kunt een shared access signature (SAS) voor een bestandsshare of voor een afzonderlijk bestand genereren. U kunt ook een gedeeld toegangsbeleid op een bestandsshare-toomanage gedeelde toegang handtekeningen maken. Maken van een gedeeld toegangsbeleid wordt aanbevolen, aangezien deze een manier om Hallo SAS intrekken biedt als deze verdacht.

Hallo volgende voorbeeld wordt een beleid voor gedeelde toegang gemaakt op een bestandsshare op en gebruikt u vervolgens dat tooprovide Hallo beleidsbeperkingen voor een SAS voor een bestand in Hallo delen.

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client and get a reference toohello share
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

if (share.exists())
{
    // Create and assign a policy
    utility::string_t policy_name = _XPLATSTR("sampleSharePolicy");

    azure::storage::file_shared_access_policy sharedPolicy = 
      azure::storage::file_shared_access_policy();

    //set permissions tooexpire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for hello share
    azure::storage::file_share_permissions permissions;    

    //retrieve hello current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add hello new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save hello updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve hello root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in hello share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Azure Storage, bekijk deze resources:

* [Opslagclientbibliotheek voor C++](https://github.com/Azure/azure-storage-cpp)
* [Azure Storage-Service bestandsvoorbeelden in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)
* [Azure-opslagverkenner](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [Documentatie bij Azure Storage](https://azure.microsoft.com/documentation/services/storage/)