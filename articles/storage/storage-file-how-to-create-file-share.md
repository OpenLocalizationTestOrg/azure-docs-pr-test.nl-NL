---
title: aaaHow toocreate een Azure-bestandsshare | Microsoft Docs
description: Hoe toocreate een Azure-bestandsshare in Azure File storage met hello Azure-portal, PowerShell en hello Azure CLI.
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: c4c59966b82d743fb4ecf79f48c0c8e61295d03d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="823ef-103">Een bestandsshare maken in Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="823ef-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="823ef-104">U kunt Azure bestandsshares maken met [Azure-portal](https://portal.azure.com/), Azure PowerShell-cmdlets Storage hello, Hallo clientbibliotheken van Azure Storage of Hallo REST-API van Azure Storage. In deze zelfstudie leert u het:</span><span class="sxs-lookup"><span data-stu-id="823ef-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), hello Azure Storage PowerShell cmdlets, hello Azure Storage client libraries, or hello Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="823ef-105">Hoe toocreate een Azure-bestand delen met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="823ef-105">How toocreate an Azure File share using hello Azure portal</span></span>](#Create file share through hello Portal)
* [<span data-ttu-id="823ef-106">Hoe toocreate een Azure-bestandsshare met behulp van Powershell</span><span class="sxs-lookup"><span data-stu-id="823ef-106">How toocreate an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="823ef-107">Hoe toocreate een Azure-bestandsshare met CLI</span><span class="sxs-lookup"><span data-stu-id="823ef-107">How toocreate an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="823ef-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="823ef-108">Prerequisites</span></span>
<span data-ttu-id="823ef-109">toocreate een Azure-bestandsshare, kunt u een opslagaccount dat al bestaat, of [maken van een nieuwe Azure-opslagaccount](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="823ef-109">toocreate an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](storage-create-storage-account.md).</span></span> <span data-ttu-id="823ef-110">een bestandsshare in Azure met PowerShell toocreate, moet u Hallo accountsleutel en de naam van uw opslagaccount...</span><span class="sxs-lookup"><span data-stu-id="823ef-110">toocreate an Azure File share with PowerShell, you will need hello account key and name of your storage account..</span></span> <span data-ttu-id="823ef-111">U moet de sleutel Opslagaccount als u van plan toouse Powershell of CLI bent.</span><span class="sxs-lookup"><span data-stu-id="823ef-111">You will need Storage account key if you plan toouse Powershell or CLI.</span></span>

## <a name="create-file-share-through-hello-portal"></a><span data-ttu-id="823ef-112">Bestandsshare via Hallo Portal maken</span><span class="sxs-lookup"><span data-stu-id="823ef-112">Create file share through hello Portal</span></span>
1. <span data-ttu-id="823ef-113">**Blade-Account in Azure Portal gaat tooStorage**:</span><span class="sxs-lookup"><span data-stu-id="823ef-113">**Go tooStorage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="823ef-114">![Blade Opslagaccount](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="823ef-114">![Storage Account Blade](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="823ef-115">**Klik op de knop Bestandsshare toevoegen**:</span><span class="sxs-lookup"><span data-stu-id="823ef-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="823ef-116">![Klik op Hallo file share knop toevoegen](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="823ef-116">![Click hello add file share button](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="823ef-117">**Geef de naam en een quotum op. Het quotum heeft momenteel een maximum van 5 TB**:</span><span class="sxs-lookup"><span data-stu-id="823ef-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="823ef-118">![Geef een naam en een gewenste quotum voor de nieuwe bestandsshare Hallo](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="823ef-118">![Provide a name and a desired quota for hello new file share](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="823ef-119">**Bekijk uw nieuwe bestandsshare**: ![Bekijk uw nieuwe bestandsshare](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="823ef-119">**View your new file share**:  ![View your new file share](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="823ef-120">**Upload een bestand**: ![Upload een bestand](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="823ef-120">**Upload a file**:  ![Upload a file](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="823ef-121">**Blader naar de bestandsshare en beheer uw mappen en bestanden**: ![Blader naar de bestandsshare](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="823ef-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="823ef-122">Een bestandsshare via de PowerShell maken</span><span class="sxs-lookup"><span data-stu-id="823ef-122">Create file share through PowerShell</span></span>
<span data-ttu-id="823ef-123">tooprepare toouse PowerShell, download en installeer hello Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="823ef-123">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="823ef-124">Zie [hoe tooinstall en configureren van Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) installeren voor Hallo installatiepunt en de installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="823ef-124">See [How tooinstall and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for hello install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="823ef-125">Het verdient aanbeveling dat u downloaden en installeren of upgraden van de meest recente Azure PowerShell-module toohello.</span><span class="sxs-lookup"><span data-stu-id="823ef-125">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="823ef-126">**Een context maken voor uw opslagaccount en de sleutel** Hallo context Hallo naam en het account opslagaccountsleutel ingekapseld.</span><span class="sxs-lookup"><span data-stu-id="823ef-126">**Create a context for your storage account and key** hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="823ef-127">Voor instructies voor het kopiëren van de accountsleutel uit [Azure Portal](https://portal.azure.com/) raadpleegt u [Opslagtoegangssleutels bekijken en kopiëren](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="823ef-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="823ef-128">**Maak een nieuwe bestandsshare**:</span><span class="sxs-lookup"><span data-stu-id="823ef-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="823ef-129">Hallo-naam van de bestandsshare moet alleen kleine letters bevatten.</span><span class="sxs-lookup"><span data-stu-id="823ef-129">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="823ef-130">Zie [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx) (Shares, mappen, bestanden en metagegevens een naam geven en hiernaar verwijzen) voor meer informatie over de naamgeving van bestandsshares en bestanden.</span><span class="sxs-lookup"><span data-stu-id="823ef-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="823ef-131">Een bestandsshare via de opdrachtregelinterface (CLI) maken</span><span class="sxs-lookup"><span data-stu-id="823ef-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="823ef-132">**tooprepare toouse een opdrachtregelinterface (CLI), download en installeer hello Azure CLI.**</span><span class="sxs-lookup"><span data-stu-id="823ef-132">**tooprepare toouse a Command Line Interface (CLI), download and install hello Azure CLI.**</span></span>  
    <span data-ttu-id="823ef-133">Zie [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) (Azure CLI 2.0 installeren) en [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) (Aan de slag met Azure CLI 2.0).</span><span class="sxs-lookup"><span data-stu-id="823ef-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="823ef-134">**Maak een verbinding tekenreeks toohello opslagaccount waar u toocreate Hallo share.**</span><span class="sxs-lookup"><span data-stu-id="823ef-134">**Create a connection string toohello storage account where you want toocreate hello share.**</span></span>  
    <span data-ttu-id="823ef-135">Vervang ```<storage-account>``` en ```<resource_group>``` met uw account en de bron opslaggroep in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="823ef-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in hello following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. <span data-ttu-id="823ef-136">**Bestandsshare maken**</span><span class="sxs-lookup"><span data-stu-id="823ef-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="823ef-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="823ef-137">Next steps</span></span>
* [<span data-ttu-id="823ef-138">Bestandsshare verbinden en koppelen - Windows</span><span class="sxs-lookup"><span data-stu-id="823ef-138">Connect and Mount File Share - Windows</span></span>](storage-file-how-to-use-files-windows.md)
* [<span data-ttu-id="823ef-139">Bestandsshare verbinden en koppelen - Linux</span><span class="sxs-lookup"><span data-stu-id="823ef-139">Connect and Mount File Share - Linux</span></span>](storage-how-to-use-files-linux.md)
* [<span data-ttu-id="823ef-140">Bestandsshare verbinden en koppelen - Mac OS</span><span class="sxs-lookup"><span data-stu-id="823ef-140">Connect and Mount File Share - macOS</span></span>](storage-file-how-to-use-files-mac.md)

<span data-ttu-id="823ef-141">Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="823ef-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="823ef-142">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="823ef-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="823ef-143">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="823ef-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)