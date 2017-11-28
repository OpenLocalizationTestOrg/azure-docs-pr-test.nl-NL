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
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a><span data-ttu-id="89fd3-103">Verplaatsen van gegevens tooand uit Azure Blob Storage met behulp van Python</span><span class="sxs-lookup"><span data-stu-id="89fd3-103">Move data tooand from Azure Blob Storage using Python</span></span>
<span data-ttu-id="89fd3-104">Dit onderwerp wordt beschreven hoe de toolist, uploaden en downloaden van blobs met Hallo Python-API.</span><span class="sxs-lookup"><span data-stu-id="89fd3-104">This topic describes how toolist, upload, and download blobs using hello Python API.</span></span> <span data-ttu-id="89fd3-105">Met de Hallo Python-API die zijn opgegeven in de Azure SDK, kunt u:</span><span class="sxs-lookup"><span data-stu-id="89fd3-105">With hello Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="89fd3-106">Een container maken</span><span class="sxs-lookup"><span data-stu-id="89fd3-106">Create a container</span></span>
* <span data-ttu-id="89fd3-107">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="89fd3-107">Upload a blob into a container</span></span>
* <span data-ttu-id="89fd3-108">Blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="89fd3-108">Download blobs</span></span>
* <span data-ttu-id="89fd3-109">Lijst Hallo blobs in een container</span><span class="sxs-lookup"><span data-stu-id="89fd3-109">List hello blobs in a container</span></span>
* <span data-ttu-id="89fd3-110">Een blob verwijderen</span><span class="sxs-lookup"><span data-stu-id="89fd3-110">Delete a blob</span></span>

<span data-ttu-id="89fd3-111">Zie voor meer informatie over het gebruik van Python API Hallo [hoe tooUse Blob Storage-Service met Python Hallo](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="89fd3-111">For more information about using hello Python API, see [How tooUse hello Blob Storage Service from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="89fd3-112">Als u virtuele machine die is ingesteld met Hallo scripts geleverd door [gegevens wetenschappelijke virtuele machines in Azure](machine-learning-data-science-virtual-machines.md), en vervolgens AzCopy is al geïnstalleerd op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="89fd3-112">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="89fd3-113">Voor een volledige inleiding tooAzure blob-opslag te verwijzen[basisbeginselen van Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) en te[Azure Blob-Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="89fd3-113">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="89fd3-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="89fd3-114">Prerequisites</span></span>
<span data-ttu-id="89fd3-115">Dit document wordt ervan uitgegaan dat u een Azure-abonnement, een opslagaccount en de bijbehorende opslagsleutel Hallo voor dat account hebt.</span><span class="sxs-lookup"><span data-stu-id="89fd3-115">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="89fd3-116">Voordat u gaat gegevens uploaden/downloaden, moet u weten Azure naam en sleutel van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="89fd3-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="89fd3-117">Zie tooset van een Azure-abonnement [gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89fd3-117">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="89fd3-118">Zie voor instructies over het maken van een opslagaccount en voor het ophalen van de account en sleutelgegevens [over Azure storage-accounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="89fd3-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="upload-data-tooblob"></a><span data-ttu-id="89fd3-119">Uploaden van gegevens tooBlob</span><span class="sxs-lookup"><span data-stu-id="89fd3-119">Upload Data tooBlob</span></span>
<span data-ttu-id="89fd3-120">Hallo codefragment aan de bovenkant Hallo van een Python-code in die u wenst dat tooprogrammatically toegang tot Azure Storage volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="89fd3-120">Add hello following snippet near hello top of any Python code in which you wish tooprogrammatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="89fd3-121">Hallo **BlobService** object kunt u samenwerken met containers en blobs.</span><span class="sxs-lookup"><span data-stu-id="89fd3-121">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="89fd3-122">Hallo volgende code maakt een BlobService-object met behulp van Hallo en -account voor de naam van de sleutel van opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="89fd3-122">hello following code creates a BlobService object using hello storage account name and account key.</span></span> <span data-ttu-id="89fd3-123">Accountnaam en accountsleutel vervangen door uw bestaande account en -sleutel.</span><span class="sxs-lookup"><span data-stu-id="89fd3-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="89fd3-124">Gebruik Hallo methoden tooupload gegevens tooa blob te volgen:</span><span class="sxs-lookup"><span data-stu-id="89fd3-124">Use hello following methods tooupload data tooa blob:</span></span>

1. <span data-ttu-id="89fd3-125">plaatsen\_blok\_blob\_van\_pad (uploads Hallo inhoud van een bestand uit het opgegeven pad Hallo)</span><span class="sxs-lookup"><span data-stu-id="89fd3-125">put\_block\_blob\_from\_path (uploads hello contents of a file from hello specified path)</span></span>
2. <span data-ttu-id="89fd3-126">plaatsen\_block_blob\_van\_bestand (uploads Hallo inhoud uit een al geopend bestandsstroom)</span><span class="sxs-lookup"><span data-stu-id="89fd3-126">put\_block_blob\_from\_file (uploads hello contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="89fd3-127">plaatsen\_blok\_blob\_van\_bytes (uploads een matrix met bytes)</span><span class="sxs-lookup"><span data-stu-id="89fd3-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="89fd3-128">plaatsen\_blok\_blob\_van\_tekst (uploads Hallo opgegeven tekstwaarde Hallo met de opgegeven codering)</span><span class="sxs-lookup"><span data-stu-id="89fd3-128">put\_block\_blob\_from\_text (uploads hello specified text value using hello specified encoding)</span></span>

<span data-ttu-id="89fd3-129">Hallo volgende voorbeeldcode wordt een lokaal bestand tooa container geüpload:</span><span class="sxs-lookup"><span data-stu-id="89fd3-129">hello following sample code uploads a local file tooa container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="89fd3-130">Hallo uploadt volgende voorbeeldcode alle Hallo-bestanden (met uitzondering van mappen) in een lokale map tooblob opslag:</span><span class="sxs-lookup"><span data-stu-id="89fd3-130">hello following sample code uploads all hello files (excluding directories) in a local directory tooblob storage:</span></span>

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


## <a name="download-data-from-blob"></a><span data-ttu-id="89fd3-131">Gegevens uit Blob te downloaden</span><span class="sxs-lookup"><span data-stu-id="89fd3-131">Download Data from Blob</span></span>
<span data-ttu-id="89fd3-132">Volgende methoden toodownload gegevens uit een blob hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="89fd3-132">Use hello following methods toodownload data from a blob:</span></span>

1. <span data-ttu-id="89fd3-133">ophalen van\_blob\_naar\_pad</span><span class="sxs-lookup"><span data-stu-id="89fd3-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="89fd3-134">ophalen van\_blob\_naar\_bestand</span><span class="sxs-lookup"><span data-stu-id="89fd3-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="89fd3-135">ophalen van\_blob\_naar\_bytes</span><span class="sxs-lookup"><span data-stu-id="89fd3-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="89fd3-136">ophalen van\_blob\_naar\_tekst</span><span class="sxs-lookup"><span data-stu-id="89fd3-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="89fd3-137">Deze methoden die Hallo nodig verdeling in segmenten uitvoeren wanneer Hallo Hallo gegevens groter zijn dan 64 MB.</span><span class="sxs-lookup"><span data-stu-id="89fd3-137">These methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="89fd3-138">Hallo downloads volgende voorbeeldcode Hallo inhoud van een blob in een container tooa lokaal bestand:</span><span class="sxs-lookup"><span data-stu-id="89fd3-138">hello following sample code downloads hello contents of a blob in a container tooa local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="89fd3-139">Hallo downloadt volgende voorbeeldcode alle blobs uit een container.</span><span class="sxs-lookup"><span data-stu-id="89fd3-139">hello following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="89fd3-140">Dit maakt gebruik van\_tooget Hallo lijst met beschikbare blobs in Hallo container-blobs en downloadt tooa lokale map.</span><span class="sxs-lookup"><span data-stu-id="89fd3-140">It uses list\_blobs tooget hello list of available blobs in hello container and downloads them tooa local directory.</span></span>

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
