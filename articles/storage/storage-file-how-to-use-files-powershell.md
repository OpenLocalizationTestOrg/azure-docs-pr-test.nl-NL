---
title: aaaHow toouse PowerShell toomanage Azure File storage | Microsoft Docs
description: Meer informatie over toouse PowerShell toomanage Azure File storage.
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
ms.openlocfilehash: 0e30e8796cf8bbf5f9249b26179d5e0f9077c8fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a><span data-ttu-id="99c25-103">Hoe toouse PowerShell toomanage Azure File storage</span><span class="sxs-lookup"><span data-stu-id="99c25-103">How toouse PowerShell toomanage Azure File storage</span></span>
<span data-ttu-id="99c25-104">U kunt Azure PowerShell toocreate gebruiken en beheren van bestandsshares.</span><span class="sxs-lookup"><span data-stu-id="99c25-104">You can use Azure PowerShell toocreate and manage file shares.</span></span>

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="99c25-105">Hallo PowerShell-cmdlets voor Azure Storage installeren</span><span class="sxs-lookup"><span data-stu-id="99c25-105">Install hello PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="99c25-106">tooprepare toouse PowerShell, download en installeer hello Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="99c25-106">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="99c25-107">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs) installeren voor Hallo installatiepunt en de installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="99c25-107">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for hello install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="99c25-108">Het verdient aanbeveling dat u downloaden en installeren of upgraden van de meest recente Azure PowerShell-module toohello.</span><span class="sxs-lookup"><span data-stu-id="99c25-108">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="99c25-109">Open een Azure PowerShell-venster door op **Start** te klikken en **Windows PowerShell** te typen.</span><span class="sxs-lookup"><span data-stu-id="99c25-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="99c25-110">Hallo PowerShell-venster wordt hello Azure Powershell-module voor u geladen.</span><span class="sxs-lookup"><span data-stu-id="99c25-110">hello PowerShell window loads hello Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="99c25-111">Een context maken voor uw opslagaccount en -sleutel</span><span class="sxs-lookup"><span data-stu-id="99c25-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="99c25-112">Hallo storage account context maken.</span><span class="sxs-lookup"><span data-stu-id="99c25-112">Create hello storage account context.</span></span> <span data-ttu-id="99c25-113">Hallo context ingekapseld Hallo naam en opslagaccountsleutel.</span><span class="sxs-lookup"><span data-stu-id="99c25-113">hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="99c25-114">Voor instructies voor het kopiëren van de accountsleutel uit Hallo [Azure-portal](https://portal.azure.com), Zie [weergeven en kopiëren opslagtoegangssleutels](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="99c25-114">For instructions on copying your account key from hello [Azure portal](https://portal.azure.com), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="99c25-115">Vervang `storage-account-name` en `storage-account-key` opslagaccountnaam en sleutel van uw in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="99c25-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in hello following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="99c25-116">Een nieuwe bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="99c25-116">Create a new file share</span></span>
<span data-ttu-id="99c25-117">Maak nieuwe share hello, met de naam `logs`.</span><span class="sxs-lookup"><span data-stu-id="99c25-117">Create hello new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="99c25-118">U hebt nu een bestandsshare in File Storage.</span><span class="sxs-lookup"><span data-stu-id="99c25-118">You now have a file share in File storage.</span></span> <span data-ttu-id="99c25-119">Nu gaan we een map en een bestand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="99c25-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99c25-120">Hallo-naam van de bestandsshare moet alleen kleine letters bevatten.</span><span class="sxs-lookup"><span data-stu-id="99c25-120">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="99c25-121">Zie [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx) (Shares, mappen, bestanden en metagegevens een naam geven en hiernaar verwijzen) voor meer informatie over de naamgeving van bestandsshares en bestanden.</span><span class="sxs-lookup"><span data-stu-id="99c25-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a><span data-ttu-id="99c25-122">Maak een map in Hallo-bestandsshare</span><span class="sxs-lookup"><span data-stu-id="99c25-122">Create a directory in hello file share</span></span>
<span data-ttu-id="99c25-123">Maak een map op Hallo-share.</span><span class="sxs-lookup"><span data-stu-id="99c25-123">Create a directory in hello share.</span></span> <span data-ttu-id="99c25-124">In de Hallo voorbeeld te volgen, Hallo directory heet `CustomLogs`.</span><span class="sxs-lookup"><span data-stu-id="99c25-124">In hello following example, hello directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a><span data-ttu-id="99c25-125">Uploaden van een lokale map voor toohello</span><span class="sxs-lookup"><span data-stu-id="99c25-125">Upload a local file toohello directory</span></span>
<span data-ttu-id="99c25-126">Upload nu een lokaal bestand toohello-map.</span><span class="sxs-lookup"><span data-stu-id="99c25-126">Now upload a local file toohello directory.</span></span> <span data-ttu-id="99c25-127">Hallo volgende voorbeeld wordt een bestand geüpload vanuit `C:\temp\Log1.txt`.</span><span class="sxs-lookup"><span data-stu-id="99c25-127">hello following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="99c25-128">Hallo-bestandspad bewerken zodat deze tooa geldig bestand op uw lokale machine verwijst.</span><span class="sxs-lookup"><span data-stu-id="99c25-128">Edit hello file path so that it points tooa valid file on your local machine.</span></span>

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a><span data-ttu-id="99c25-129">Lijst Hallo bestanden in de directory Hallo</span><span class="sxs-lookup"><span data-stu-id="99c25-129">List hello files in hello directory</span></span>
<span data-ttu-id="99c25-130">toosee Hallo-bestand in map hello, kunt u alle bestanden van de directory Hallo kunt aanbieden.</span><span class="sxs-lookup"><span data-stu-id="99c25-130">toosee hello file in hello directory, you can list all of hello directory's files.</span></span> <span data-ttu-id="99c25-131">Met deze opdracht retourneert Hallo bestanden en submappen (wanneer aanwezig) in Hallo map customlogs.</span><span class="sxs-lookup"><span data-stu-id="99c25-131">This command returns hello files and subdirectories (if there are any) in hello CustomLogs directory.</span></span>

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="99c25-132">Get-AzureStorageFile retourneert een lijst met bestanden en mappen voor elk mapobject dat daaraan is doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="99c25-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="99c25-133">' Get-AzureStorageFile-Share $s "retourneert een lijst met bestanden en mappen in de hoofdmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="99c25-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in hello root directory.</span></span> <span data-ttu-id="99c25-134">een lijst met bestanden in een submap tooget, hebt u toopass Hallo submap tooGet-AzureStorageFile.</span><span class="sxs-lookup"><span data-stu-id="99c25-134">tooget a list of files in a subdirectory, you have toopass hello subdirectory tooGet-AzureStorageFile.</span></span> <span data-ttu-id="99c25-135">Dit is wat dit heeft--Hallo eerste deel van de opdracht Hallo up toohello pipe retourneert een mapexemplaar van Hallo submap CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="99c25-135">That's what this does -- hello first part of hello command up toohello pipe returns a directory instance of hello subdirectory CustomLogs.</span></span> <span data-ttu-id="99c25-136">Vervolgens wordt dit doorgegeven via Get-azurestoragefile, die als Hallo bestanden en mappen in CustomLogs resultaat.</span><span class="sxs-lookup"><span data-stu-id="99c25-136">Then that is passed into Get-AzureStorageFile, which returns hello files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="99c25-137">Bestanden kopiëren</span><span class="sxs-lookup"><span data-stu-id="99c25-137">Copy files</span></span>
<span data-ttu-id="99c25-138">Vanaf versie 0.9.7 van Azure PowerShell, kunt u een bestand tooanother, een bestand tooa blob of een blob tooa-bestand kopiëren.</span><span class="sxs-lookup"><span data-stu-id="99c25-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="99c25-139">Hieronder ziet u hoe tooperform die deze kopiëren bewerkingen met behulp van PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="99c25-139">Below we demonstrate how tooperform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="99c25-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="99c25-140">Next steps</span></span>
<span data-ttu-id="99c25-141">Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="99c25-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="99c25-142">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="99c25-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="99c25-143">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="99c25-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)