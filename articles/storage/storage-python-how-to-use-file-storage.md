---
title: aaaDevelop voor Azure File storage met behulp van Python | Microsoft Docs
description: Meer informatie over hoe toodevelop Python toepassingen en services die gebruikmaken van Azure File storage toostore bestandsgegevens.
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 45623e6dbec6f140cedc4e58e56a93fb4af9054e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a>Ontwikkelen voor Azure File storage met behulp van Python
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Over deze zelfstudie
Deze zelfstudie wordt gedemonstreerd Hallo grondbeginselen van het gebruik van Python toodevelop toepassingen of services die gebruikmaken van Azure File storage toostore bestandsgegevens. In deze zelfstudie wordt een eenvoudige consoletoepassing maken en weergeven hoe tooperform basisbewerkingen uitvoeren met Python en Azure File storage:

* Azure-bestandsshares maken
* Mappen maken
* Bestanden en mappen in een Azure-bestandsshare opsommen
* Uploaden, downloaden en een bestand verwijderen

> [!Note]  
> Omdat Azure File storage zijn toegankelijk via SMB, is het mogelijk toowrite eenvoudige toepassingen die toegang hebben tot hello Azure bestandsshare met behulp van Hallo standaard Python i/o-klassen en -functies. In dit artikel wordt beschreven hoe toowrite toepassingen die gebruikmaken van Azure Storage Python SDK, die gebruikmaakt van Hallo Hallo [Azure File storage REST-API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.

### <a name="set-up-your-application-toouse-azure-file-storage"></a>Instellen van uw toepassing toouse Azure File storage
De volgende Hallo aan de bovenkant Hallo van een Python-bronbestand waarin u tooprogrammatically toegang tot Azure Storage wilt toevoegen.

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a>Instellen van een verbinding tooAzure File storage 
Hallo `FileService` object kunt u samenwerken met shares, mappen en bestanden. Hallo volgende code maakt een `FileService` object met behulp van Hallo naam en opslagaccountsleutel. Vervang `<myaccount>` en `<mykey>` met uw accountnaam en de sleutel.

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a>Een Azure-bestandsshare maken
In de Hallo volgende codevoorbeeld, kunt u een `FileService` object toocreate Hallo share als deze niet bestaat.

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a>Een map maken
U kunt ook opslag door de gegevens van de bestanden in submappen in plaats van ze allemaal in de hoofdmap Hallo indelen. Azure File storage, kunt u toocreate veel mappen als uw account wordt toegestaan. Hallo-code hieronder maakt u een onderliggende map met de naam **sampledir** onder Hallo-hoofdmap.

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Bestanden en mappen in een Azure-bestandsshare opsommen
toolist hello bestanden en mappen in een share gebruiken Hallo **lijst\_mappen\_en\_bestanden** methode. Deze methode retourneert een generator. Hallo volgende code levert Hallo **naam** van elk bestand en de map in een share toohello-console.

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a>Bestand uploaden 
Azure File share op Hallo zeer minste bevat, een hoofdmap waarin de bestanden kunnen zich bevinden. In deze sectie leert u hoe een bestand van de lokale opslag op Hallo tooupload de hoofdmap van een share.

toocreate een bestand en het van uploadgegevens, gebruikt u Hallo `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` of `create_file_from_text` methoden. Op hoog niveau van de methoden die Hallo nodig verdeling in segmenten uitvoeren wanneer Hallo Hallo gegevens groter zijn dan 64 MB zijn.

`create_file_from_path`uploads Hallo inhoud van een bestand uit Hallo opgegeven pad en `create_file_from_stream` uploads Hallo inhoud uit een al geopend bestandsstroom. `create_file_from_bytes`een matrix met bytes, uploadt en `create_file_from_text` uploads Hallo opgegeven tekstwaarde met Hallo opgegeven codering (standaardwaarden tooUTF-8).

Hallo volgende voorbeeld wordt geüpload Hallo inhoud Hallo **sunset.png** -bestand in Hallo **mijnbestand** bestand.

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a>Bestand downloaden
gegevens uit een bestand toodownload gebruiken `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, of `get_file_to_text`. Op hoog niveau van de methoden die Hallo nodig verdeling in segmenten uitvoeren wanneer Hallo Hallo gegevens groter zijn dan 64 MB zijn.

Hallo volgende voorbeeld worden `get_file_to_path` toodownload Hallo inhoud Hallo **mijnbestand** -bestand en sla het toohello **out sunset.png** bestand.

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a>Een bestand verwijderen
Tenslotte toodelete een bestand, roept `delete_file`.

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a>Volgende stappen
Nu dat u hebt geleerd hoe toomanipulate Azure File storage met behulp van Python, volgt u deze koppelingen toolearn meer.

* [Python Developer Center](/develop/python/)
* [REST-API voor Azure Storage-services](http://msdn.microsoft.com/library/azure/dd179355)
* [Microsoft Azure-opslag-SDK voor Python](https://github.com/Azure/azure-storage-python)