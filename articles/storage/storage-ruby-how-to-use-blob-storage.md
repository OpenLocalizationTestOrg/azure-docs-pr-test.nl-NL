---
title: aaaHow toouse Blob storage (objectopslag) met Ruby | Microsoft Docs
description: Niet-gestructureerde gegevens opslaan in Hallo cloud met Azure Blob storage (objectopslag).
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e2fe4c45-27b0-4d15-b3fb-e7eb574db717
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 638826777f5a7ae8330fd67cdbb51d5eee1736a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ruby"></a>Hoe toouse Blob-opslag met Ruby
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Overzicht
Azure Blob storage is een service die niet-gestructureerde gegevens in de cloud Hallo als objecten/blobs opslaat. In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen. BLOB-opslag is ook bedoeld tooas vorm van objectopslag.

Deze handleiding leert u hoe tooperform algemene scenario's met behulp van Blob-opslag. Hallo-voorbeelden zijn geschreven met behulp van Hallo Ruby-API. Hallo scenario's worden behandeld: **uploaden, aanbieding, gedownload,** en **verwijderen** blobs.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Een Ruby-toepassing maken
Maak een Ruby toepassing. Zie voor instructies [Ruby op Rails webtoepassing op een virtuele machine in Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)

## <a name="configure-your-application-tooaccess-storage"></a>Uw toepassing tooaccess opslag configureren
toouse Azure Storage, moet u toodownload en gebruik Hallo Ruby azure, dit pakket bevat een set met gemak bibliotheken die met de Hallo storage REST-services communiceren.

### <a name="use-rubygems-tooobtain-hello-package"></a>RubyGems tooobtain Hallo pakket gebruiken
1. Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Unix).
2. Typ 'gem installeren azure' hello opdracht venster tooinstall Hallo gem en afhankelijkheden.

### <a name="import-hello-package"></a>Hallo-pakket importeren
Met uw favoriete teksteditor toevoegen Hallo toohello bovenaan Hallo Ruby bestand waarin u van plan toouse opslag bent te volgen:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Een Azure Storage-verbinding instellen
Hello azure module lezen Hallo omgevingsvariabelen **AZURE\_opslag\_ACCOUNT** en **AZURE\_opslag\_ACCESS_KEY** voor informatie vereist tooconnect tooyour Azure storage-account. Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens Hallo voordat u **Azure::Blob::BlobService** Hello code te volgen:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain deze waarden van een klassiek of Resource Manager-storage-account in hello Azure-portal:

1. Meld u bij toohello [Azure-portal](https://portal.azure.com).
2. Navigeer toohello gewenste toouse storage-account.
3. Klik op Hallo instellingenblade op Hallo rechts **toegangstoetsen**.
4. Hallo toegang sleutels blade die wordt weergegeven, ziet u Hallo toegangssleutel 1 en toegangssleutel 2. U kunt een van beide gebruiken.
5. Klik op Hallo kopiëren pictogram toocopy Hallo sleutel toohello Klembord.

tooobtain deze waarden van een klassieke storage-account in de klassieke Azure portal Hallo:

1. Meld u bij toohello [klassieke Azure portal](https://manage.windowsazure.com).
2. Navigeer toohello gewenste toouse storage-account.
3. Klik op **TOEGANGSSLEUTELS beheren** Hallo Hallo navigatiedeelvenster onderaan in.
4. In het pop-upvenster hello ziet u opslagaccountnaam hello, de primaire toegangssleutel en de secundaire toegangssleutel. U kunt voor toegangssleutel, Hallo een primaire of secundaire één Hallo gebruiken.
5. Klik op Hallo kopiëren pictogram toocopy Hallo sleutel toohello Klembord.

## <a name="create-a-container"></a>Een container maken
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Hallo **Azure::Blob::BlobService** object kunt u samenwerken met containers en blobs. toocreate een container gebruiken Hallo **maken\_container()** methode.

Hallo volgende codevoorbeeld maakt een container of afdrukken Hallo fout indien deze aanwezig is.

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

Als u toomake Hallo bestanden in de container Hallo openbare wilt, kunt u Hallo-container machtigingen instellen.

U kunt alleen Hallo wijzigen <strong>maken\_container()</strong> aanroep toopass hello **: openbare\_toegang\_niveau** optie:

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

Geldige waarden voor Hallo **: openbare\_toegang\_niveau** optie zijn:

* **BLOB:** geeft openbare leestoegang voor blobs. BLOB-gegevens in deze container via anonieme aanvragen kunnen worden gelezen, maar de containergegevens is niet beschikbaar. Clients kunnen blobs in de container Hallo via anonieme aanvragen niet opsommen.
* **container:** Hiermee geeft u op volledige openbare leestoegang voor container en de blob-gegevens. Clients kunnen opsommen blobs in de container Hallo via anonieme aanvraag, maar kunnen de containers in Hallo storage-account niet inventariseren.

U kunt ook Hallo openbare toegangsniveau van een container wijzigen met behulp van **ingesteld\_container\_acl()** methode toospecify Hallo openbare toegangsniveau.

Hallo met het volgende codevoorbeeld wijzigingen Hallo openbare toegangsniveau te**container**:

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a>Een blob uploaden naar een container
tooupload inhoud tooa blob, gebruik Hallo **maken\_blok\_blob()** methode toocreate Hallo blob, gebruikt u een bestand of een tekenreekstype als Hallo inhoud van het Hallo-blob.

Hallo volgende code Hallo bestand geüpload **test.png** als een nieuwe blob met de naam 'installatiekopie-blob' in het Hallo-container.

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a>Lijst Hallo blobs in een container
Gebruik toolist Hallo containers **list_containers()** methode.
toolist hello blobs binnen een container gebruiken **lijst\_blobs()** methode.

Dit levert Hallo-URL's van alle Hallo blobs in alle Hallo containers voor Hallo-account.

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a>Blobs downloaden
toodownload blobs, gebruik Hallo **ophalen\_blob()** methode tooretrieve Hallo inhoud.

Hallo volgende voorbeeldcode laat zien met **ophalen\_blob()** toodownload inhoud van 'installatiekopie-blob' Hallo en het lokale bestand tooa schrijven.

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a>Verwijderen van een Blob
Een blob toodelete gebruik tot slot Hallo **verwijderen\_blob()** methode. Hallo volgende voorbeeldcode laat zien hoe toodelete een blob.

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a>Volgende stappen
toolearn over complexere opslagtaken, volgt u deze koppelingen:

* [Blog van het Azure Storage-team](http://blogs.msdn.com/b/windowsazurestorage/)
* [Azure SDK voor Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) opslagplaats op GitHub
* [Gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md)

