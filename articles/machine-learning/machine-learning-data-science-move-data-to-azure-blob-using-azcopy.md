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
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a><span data-ttu-id="6cb24-103">Verplaatsen van gegevens tooand uit Azure Blob Storage met behulp van AzCopy</span><span class="sxs-lookup"><span data-stu-id="6cb24-103">Move data tooand from Azure Blob Storage using AzCopy</span></span>
<span data-ttu-id="6cb24-104">AzCopy is een opdrachtregelprogramma dat is ontworpen voor het uploaden, downloaden en kopiëren tooand van gegevens uit Microsoft Azure blob-bestand en tabelopslag.</span><span class="sxs-lookup"><span data-stu-id="6cb24-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data tooand from Microsoft Azure blob, file, and table storage.</span></span>

<span data-ttu-id="6cb24-105">Zie voor instructies over het installeren van AzCopy en aanvullende informatie over het gebruik van deze Hello Azure-platform [aan de slag met het AzCopy-opdrachtregelprogramma Hallo](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="6cb24-105">For instructions on installing AzCopy and additional information on using it with hello Azure platform, see [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="6cb24-106">Als u virtuele machine die is ingesteld met Hallo scripts geleverd door [gegevens wetenschappelijke virtuele machines in Azure](machine-learning-data-science-virtual-machines.md), en vervolgens AzCopy is al geïnstalleerd op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="6cb24-106">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="6cb24-107">Voor een volledige inleiding tooAzure blob-opslag te verwijzen[basisbeginselen van Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) en te[Azure Blob-Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="6cb24-107">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="6cb24-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6cb24-108">Prerequisites</span></span>
<span data-ttu-id="6cb24-109">Dit document wordt ervan uitgegaan dat u een Azure-abonnement, een opslagaccount hebt en bijbehorende opslagsleutel voor dat account Hallo.</span><span class="sxs-lookup"><span data-stu-id="6cb24-109">This document assumes that you have an Azure subscription, a storage account and hello corresponding storage key for that account.</span></span> <span data-ttu-id="6cb24-110">Voordat u gaat gegevens uploaden/downloaden, moet u weten Azure naam en sleutel van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="6cb24-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="6cb24-111">Zie tooset van een Azure-abonnement [gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6cb24-111">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6cb24-112">Zie voor instructies over het maken van een opslagaccount en voor het ophalen van de account en sleutelgegevens [over Azure storage-accounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="6cb24-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="run-azcopy-commands"></a><span data-ttu-id="6cb24-113">AzCopy-opdrachten uitvoeren</span><span class="sxs-lookup"><span data-stu-id="6cb24-113">Run AzCopy commands</span></span>
<span data-ttu-id="6cb24-114">toorun AzCopy opdrachten, open een opdrachtvenster en navigeer toohello AzCopy-installatiemap op uw computer, waar Hallo AzCopy.exe uitvoerbare bestand zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="6cb24-114">toorun AzCopy commands, open a command window and navigate toohello AzCopy installation directory on your computer, where hello AzCopy.exe executable is located.</span></span> 

<span data-ttu-id="6cb24-115">Hallo basic syntaxis voor opdrachten van AzCopy is:</span><span class="sxs-lookup"><span data-stu-id="6cb24-115">hello basic syntax for AzCopy commands is:</span></span>

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> <span data-ttu-id="6cb24-116">U kunt Hallo AzCopy locatie tooyour system installatiepad toevoegen en vervolgens Hallo opdrachten uitvoeren vanuit een andere map.</span><span class="sxs-lookup"><span data-stu-id="6cb24-116">You can add hello AzCopy installation location tooyour system path and then run hello commands from any directory.</span></span> <span data-ttu-id="6cb24-117">AzCopy is standaard te*% ProgramFiles (x86) %\Microsoft SDKs\Azure\AzCopy* of *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="6cb24-117">By default, AzCopy is installed too*%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span></span>
> 
> 

## <a name="upload-files-tooan-azure-blob"></a><span data-ttu-id="6cb24-118">Uploaden van bestanden tooan Azure-blobopslag</span><span class="sxs-lookup"><span data-stu-id="6cb24-118">Upload files tooan Azure blob</span></span>
<span data-ttu-id="6cb24-119">tooupload een bestand Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6cb24-119">tooupload a file, use hello following command:</span></span>

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a><span data-ttu-id="6cb24-120">Bestanden downloaden van een Azure-blob</span><span class="sxs-lookup"><span data-stu-id="6cb24-120">Download files from an Azure blob</span></span>
<span data-ttu-id="6cb24-121">toodownload een bestand van een Azure-blob, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6cb24-121">toodownload a file from an Azure blob, use hello following command:</span></span>

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a><span data-ttu-id="6cb24-122">Blobs overbrengen tussen Azure-containers</span><span class="sxs-lookup"><span data-stu-id="6cb24-122">Transfer blobs between Azure containers</span></span>
<span data-ttu-id="6cb24-123">tootransfer BLOB's tussen Azure containers Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6cb24-123">tootransfer blobs between Azure containers, use hello following command:</span></span>

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a><span data-ttu-id="6cb24-124">Tips voor het gebruik van AzCopy</span><span class="sxs-lookup"><span data-stu-id="6cb24-124">Tips for using AzCopy</span></span>
> [!TIP]
> 1. <span data-ttu-id="6cb24-125">Wanneer **uploaden** bestanden, */S* recursief bestanden geüpload.</span><span class="sxs-lookup"><span data-stu-id="6cb24-125">When **uploading** files, */S* uploads files recursively.</span></span> <span data-ttu-id="6cb24-126">Deze parameter niet opgeeft, worden bestanden in submappen niet geüpload.</span><span class="sxs-lookup"><span data-stu-id="6cb24-126">Without this parameter, files in subdirectories are not uploaded.</span></span>  
> 2. <span data-ttu-id="6cb24-127">Wanneer **downloaden** bestand */S* zoekopdrachten Hallo container recursief totdat alle bestanden in de opgegeven map Hallo en de bijbehorende submappen of alle bestanden die overeenkomen met opgegeven patroon in Hallo gegeven Hallo map en alle submappen worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="6cb24-127">When **downloading** file, */S* searches hello container recursively until all files in hello specified directory and its subdirectories, or all files that match hello specified pattern in hello given directory and its subdirectories, are downloaded.</span></span>  
> 3. <span data-ttu-id="6cb24-128">U kunt geen opgeven een **specifieke blob-bestand** toodownload met Hallo */Source* parameter.</span><span class="sxs-lookup"><span data-stu-id="6cb24-128">You cannot specify a **specific blob file** toodownload using hello */Source* parameter.</span></span> <span data-ttu-id="6cb24-129">een specifiek bestand toodownload opgeven Hallo blob bestand naam toodownload Hallo met */patroon* parameter.</span><span class="sxs-lookup"><span data-stu-id="6cb24-129">toodownload a specific file, specify hello blob file name toodownload using hello */Pattern* parameter.</span></span> <span data-ttu-id="6cb24-130">**/S** parameter gebruikte toohave AzCopy zoeken naar een bestand naam patroon recursief is.</span><span class="sxs-lookup"><span data-stu-id="6cb24-130">**/S** parameter can be used toohave AzCopy look for a file name pattern recursively.</span></span> <span data-ttu-id="6cb24-131">Hallo patroon parameter niet opgeeft downloadt AzCopy alle bestanden in die map.</span><span class="sxs-lookup"><span data-stu-id="6cb24-131">Without hello pattern parameter, AzCopy downloads all files in that directory.</span></span>
> 
> 

