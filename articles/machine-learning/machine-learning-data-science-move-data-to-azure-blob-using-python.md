---
title: aaaMove gegevens tooand uit Azure Blob Storage met behulp van Python | Microsoft Docs
description: Verplaatsen van gegevens tooand uit Azure Blob Storage met behulp van Python
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 24276252-b3dd-4edf-9e5d-f6803f8ccccc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: c2be9600e0d6cb05bcf4109a8d554db522704ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a>Verplaatsen van gegevens tooand uit Azure Blob Storage met behulp van Python
Dit onderwerp wordt beschreven hoe de toolist, uploaden en downloaden van blobs met Hallo Python-API. Met de Hallo Python-API die zijn opgegeven in de Azure SDK, kunt u:

* Een container maken
* Een blob uploaden naar een container
* Blobs downloaden
* Lijst Hallo blobs in een container
* Een blob verwijderen

Zie voor meer informatie over het gebruik van Python API Hallo [hoe tooUse Blob Storage-Service met Python Hallo](../storage/blobs/storage-python-how-to-use-blob-storage.md).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Als u virtuele machine die is ingesteld met Hallo scripts geleverd door [gegevens wetenschappelijke virtuele machines in Azure](machine-learning-data-science-virtual-machines.md), en vervolgens AzCopy is al geïnstalleerd op Hallo VM.
> 
> [!NOTE]
> Voor een volledige inleiding tooAzure blob-opslag te verwijzen[basisbeginselen van Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) en te[Azure Blob-Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Vereisten
Dit document wordt ervan uitgegaan dat u een Azure-abonnement, een opslagaccount en de bijbehorende opslagsleutel Hallo voor dat account hebt. Voordat u gaat gegevens uploaden/downloaden, moet u weten Azure naam en sleutel van uw opslagaccount.

* Zie tooset van een Azure-abonnement [gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).
* Zie voor instructies over het maken van een opslagaccount en voor het ophalen van de account en sleutelgegevens [over Azure storage-accounts](../storage/common/storage-create-storage-account.md).

## <a name="upload-data-tooblob"></a>Uploaden van gegevens tooBlob
Hallo codefragment aan de bovenkant Hallo van een Python-code in die u wenst dat tooprogrammatically toegang tot Azure Storage volgende toevoegen:

    from azure.storage.blob import BlobService

Hallo **BlobService** object kunt u samenwerken met containers en blobs. Hallo volgende code maakt een BlobService-object met behulp van Hallo en -account voor de naam van de sleutel van opslagaccount. Accountnaam en accountsleutel vervangen door uw bestaande account en -sleutel.

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

Gebruik Hallo methoden tooupload gegevens tooa blob te volgen:

1. plaatsen\_blok\_blob\_van\_pad (uploads Hallo inhoud van een bestand uit het opgegeven pad Hallo)
2. plaatsen\_block_blob\_van\_bestand (uploads Hallo inhoud uit een al geopend bestandsstroom)
3. plaatsen\_blok\_blob\_van\_bytes (uploads een matrix met bytes)
4. plaatsen\_blok\_blob\_van\_tekst (uploads Hallo opgegeven tekstwaarde Hallo met de opgegeven codering)

Hallo volgende voorbeeldcode wordt een lokaal bestand tooa container geüpload:

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

Hallo uploadt volgende voorbeeldcode alle Hallo-bestanden (met uitzondering van mappen) in een lokale map tooblob opslag:

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in hello LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading hello data %s"%blob_name


## <a name="download-data-from-blob"></a>Gegevens uit Blob te downloaden
Volgende methoden toodownload gegevens uit een blob hello gebruiken:

1. ophalen van\_blob\_naar\_pad
2. ophalen van\_blob\_naar\_bestand
3. ophalen van\_blob\_naar\_bytes
4. ophalen van\_blob\_naar\_tekst

Deze methoden die Hallo nodig verdeling in segmenten uitvoeren wanneer Hallo Hallo gegevens groter zijn dan 64 MB.

Hallo downloads volgende voorbeeldcode Hallo inhoud van een blob in een container tooa lokaal bestand:

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

Hallo downloadt volgende voorbeeldcode alle blobs uit een container. Dit maakt gebruik van\_tooget Hallo lijst met beschikbare blobs in Hallo container-blobs en downloadt tooa lokale map.

    from azure.storage.blob import BlobService
    from os.path import join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)

    # List all blobs and download them one by one
    blobs = blob_service.list_blobs(CONTAINER_NAME)
    for blob in blobs:
        local_file = join(LOCAL_DIRECT, blob.name)
        try:
            blob_service.get_blob_to_path(CONTAINER_NAME, blob.name, local_file)
        except:
            print "something wrong happened when downloading hello data %s"%blob.name
