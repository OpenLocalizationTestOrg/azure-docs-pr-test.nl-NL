---
title: aaaMove gegevens tooand uit Azure Blob Storage met behulp van AzCopy | Microsoft Docs
description: Verplaatsen van gegevens tooand uit Azure Blob Storage met behulp van AzCopy
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c309ceb2-0e83-4a07-b16d-c997dcd62d5c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: b381ba004ac16879b6c633950d03d13ad82d5b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a>Verplaatsen van gegevens tooand uit Azure Blob Storage met behulp van AzCopy
AzCopy is een opdrachtregelprogramma dat is ontworpen voor het uploaden, downloaden en kopiëren tooand van gegevens uit Microsoft Azure blob-bestand en tabelopslag.

Zie voor instructies over het installeren van AzCopy en aanvullende informatie over het gebruik van deze Hello Azure-platform [aan de slag met het AzCopy-opdrachtregelprogramma Hallo](../storage/common/storage-use-azcopy.md).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Als u virtuele machine die is ingesteld met Hallo scripts geleverd door [gegevens wetenschappelijke virtuele machines in Azure](machine-learning-data-science-virtual-machines.md), en vervolgens AzCopy is al geïnstalleerd op Hallo VM.
> 
> [!NOTE]
> Voor een volledige inleiding tooAzure blob-opslag te verwijzen[basisbeginselen van Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) en te[Azure Blob-Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Vereisten
Dit document wordt ervan uitgegaan dat u een Azure-abonnement, een opslagaccount hebt en bijbehorende opslagsleutel voor dat account Hallo. Voordat u gaat gegevens uploaden/downloaden, moet u weten Azure naam en sleutel van uw opslagaccount.

* Zie tooset van een Azure-abonnement [gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).
* Zie voor instructies over het maken van een opslagaccount en voor het ophalen van de account en sleutelgegevens [over Azure storage-accounts](../storage/common/storage-create-storage-account.md).

## <a name="run-azcopy-commands"></a>AzCopy-opdrachten uitvoeren
toorun AzCopy opdrachten, open een opdrachtvenster en navigeer toohello AzCopy-installatiemap op uw computer, waar Hallo AzCopy.exe uitvoerbare bestand zich bevindt. 

Hallo basic syntaxis voor opdrachten van AzCopy is:

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> U kunt Hallo AzCopy locatie tooyour system installatiepad toevoegen en vervolgens Hallo opdrachten uitvoeren vanuit een andere map. AzCopy is standaard te*% ProgramFiles (x86) %\Microsoft SDKs\Azure\AzCopy* of *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.
> 
> 

## <a name="upload-files-tooan-azure-blob"></a>Uploaden van bestanden tooan Azure-blobopslag
tooupload een bestand Hallo volgende opdracht gebruiken:

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a>Bestanden downloaden van een Azure-blob
toodownload een bestand van een Azure-blob, gebruik Hallo volgende opdracht:

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a>Blobs overbrengen tussen Azure-containers
tootransfer BLOB's tussen Azure containers Hallo volgende opdracht gebruiken:

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a>Tips voor het gebruik van AzCopy
> [!TIP]
> 1. Wanneer **uploaden** bestanden, */S* recursief bestanden geüpload. Deze parameter niet opgeeft, worden bestanden in submappen niet geüpload.  
> 2. Wanneer **downloaden** bestand */S* zoekopdrachten Hallo container recursief totdat alle bestanden in de opgegeven map Hallo en de bijbehorende submappen of alle bestanden die overeenkomen met opgegeven patroon in Hallo gegeven Hallo map en alle submappen worden gedownload.  
> 3. U kunt geen opgeven een **specifieke blob-bestand** toodownload met Hallo */Source* parameter. een specifiek bestand toodownload opgeven Hallo blob bestand naam toodownload Hallo met */patroon* parameter. **/S** parameter gebruikte toohave AzCopy zoeken naar een bestand naam patroon recursief is. Hallo patroon parameter niet opgeeft downloadt AzCopy alle bestanden in die map.
> 
> 

