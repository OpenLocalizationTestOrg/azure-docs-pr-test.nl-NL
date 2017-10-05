---
title: PowerShell gebruiken voor het beheer van Azure File Storage | Microsoft Docs
description: Meer informatie over het gebruik van PowerShell om Azure File Storagete beheren.
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
ms.openlocfilehash: ce62d4423ce711a6902aed7b8174ff4e827f6083
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-powershell-to-manage-azure-file-storage"></a><span data-ttu-id="16e4f-103">PowerShell gebruiken voor het beheer van Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="16e4f-103">How to use PowerShell to manage Azure File storage</span></span>
<span data-ttu-id="16e4f-104">U kunt Azure PowerShell gebruiken om bestandsshares te maken en te beheren.</span><span class="sxs-lookup"><span data-stu-id="16e4f-104">You can use Azure PowerShell to create and manage file shares.</span></span>

## <a name="install-the-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="16e4f-105">PowerShell-cmdlets voor Azure Storage installeren</span><span class="sxs-lookup"><span data-stu-id="16e4f-105">Install the PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="16e4f-106">U bereidt het gebruik van PowerShell voor door de Azure PowerShell-cmdlets te downloaden en te installeren.</span><span class="sxs-lookup"><span data-stu-id="16e4f-106">To prepare to use PowerShell, download and install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="16e4f-107">Zie [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) (Azure PowerShell installeren en configureren) voor het installatiepunt en de installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="16e4f-107">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for the install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="16e4f-108">Het wordt aanbevolen om de meest recente Azure PowerShell-module te downloaden en te installeren, of hiernaar te upgraden.</span><span class="sxs-lookup"><span data-stu-id="16e4f-108">It's recommended that you download and install or upgrade to the latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="16e4f-109">Open een Azure PowerShell-venster door op **Start** te klikken en **Windows PowerShell** te typen.</span><span class="sxs-lookup"><span data-stu-id="16e4f-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="16e4f-110">In het PowerShell-venster wordt de Azure Powershell-module voor u geladen.</span><span class="sxs-lookup"><span data-stu-id="16e4f-110">The PowerShell window loads the Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="16e4f-111">Een context maken voor uw opslagaccount en -sleutel</span><span class="sxs-lookup"><span data-stu-id="16e4f-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="16e4f-112">Maak de context van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="16e4f-112">Create the storage account context.</span></span> <span data-ttu-id="16e4f-113">De context bestaat uit de naam en accountsleutel van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="16e4f-113">The context encapsulates the storage account name and account key.</span></span> <span data-ttu-id="16e4f-114">Voor instructies voor het kopiëren van de accountsleutel uit [Azure Portal](https://portal.azure.com) raadpleegt u [Opslagtoegangssleutels bekijken en kopiëren](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="16e4f-114">For instructions on copying your account key from the [Azure portal](https://portal.azure.com), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="16e4f-115">Vervang `storage-account-name` en `storage-account-key` in het volgende voorbeeld door de naam en sleutel van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="16e4f-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in the following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="16e4f-116">Een nieuwe bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="16e4f-116">Create a new file share</span></span>
<span data-ttu-id="16e4f-117">Maak de nieuwe share met de naam `logs`.</span><span class="sxs-lookup"><span data-stu-id="16e4f-117">Create the new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="16e4f-118">U hebt nu een bestandsshare in File Storage.</span><span class="sxs-lookup"><span data-stu-id="16e4f-118">You now have a file share in File storage.</span></span> <span data-ttu-id="16e4f-119">Nu gaan we een map en een bestand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="16e4f-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16e4f-120">De naam van de bestandsshare mag alleen uit kleine letters bestaan.</span><span class="sxs-lookup"><span data-stu-id="16e4f-120">The name of your file share must be all lowercase.</span></span> <span data-ttu-id="16e4f-121">Zie [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx) (Shares, mappen, bestanden en metagegevens een naam geven en hiernaar verwijzen) voor meer informatie over de naamgeving van bestandsshares en bestanden.</span><span class="sxs-lookup"><span data-stu-id="16e4f-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-the-file-share"></a><span data-ttu-id="16e4f-122">Een map maken in de bestandsshare</span><span class="sxs-lookup"><span data-stu-id="16e4f-122">Create a directory in the file share</span></span>
<span data-ttu-id="16e4f-123">Maak een map in de share.</span><span class="sxs-lookup"><span data-stu-id="16e4f-123">Create a directory in the share.</span></span> <span data-ttu-id="16e4f-124">In het volgende voorbeeld wordt de map `CustomLogs` genoemd.</span><span class="sxs-lookup"><span data-stu-id="16e4f-124">In the following example, the directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in the share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-to-the-directory"></a><span data-ttu-id="16e4f-125">Een lokaal bestand uploaden naar de map</span><span class="sxs-lookup"><span data-stu-id="16e4f-125">Upload a local file to the directory</span></span>
<span data-ttu-id="16e4f-126">Upload nu een lokaal bestand naar de map.</span><span class="sxs-lookup"><span data-stu-id="16e4f-126">Now upload a local file to the directory.</span></span> <span data-ttu-id="16e4f-127">In het volgende voorbeeld wordt een bestand geüpload vanuit `C:\temp\Log1.txt`.</span><span class="sxs-lookup"><span data-stu-id="16e4f-127">The following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="16e4f-128">Bewerk het bestandspad zo dat het wijst naar een geldig bestand op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="16e4f-128">Edit the file path so that it points to a valid file on your local machine.</span></span>

```powershell
# upload a local file to the new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-the-files-in-the-directory"></a><span data-ttu-id="16e4f-129">De bestanden in de map weergeven</span><span class="sxs-lookup"><span data-stu-id="16e4f-129">List the files in the directory</span></span>
<span data-ttu-id="16e4f-130">Als u het bestand in de map wilt zien, kunt u alle bestanden in de map weergeven.</span><span class="sxs-lookup"><span data-stu-id="16e4f-130">To see the file in the directory, you can list all of the directory's files.</span></span> <span data-ttu-id="16e4f-131">Deze opdracht retourneert de bestanden en eventuele submappen in de map CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="16e4f-131">This command returns the files and subdirectories (if there are any) in the CustomLogs directory.</span></span>

```powershell
# list files in the new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="16e4f-132">Get-AzureStorageFile retourneert een lijst met bestanden en mappen voor elk mapobject dat daaraan is doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="16e4f-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="16e4f-133">"Get-AzureStorageFile -Share $s" retourneert een lijst met bestanden en mappen in de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="16e4f-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in the root directory.</span></span> <span data-ttu-id="16e4f-134">Voor een lijst met bestanden in een submap moet u de submap doorgeven aan Get-AzureStorageFile.</span><span class="sxs-lookup"><span data-stu-id="16e4f-134">To get a list of files in a subdirectory, you have to pass the subdirectory to Get-AzureStorageFile.</span></span> <span data-ttu-id="16e4f-135">Het volgende gebeurt: het eerste deel van de opdracht, tot aan de pipe, retourneert een mapexemplaar van de submap CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="16e4f-135">That's what this does -- the first part of the command up to the pipe returns a directory instance of the subdirectory CustomLogs.</span></span> <span data-ttu-id="16e4f-136">Daarna wordt dit doorgegeven via Get-AzureStorageFile, en worden de bestanden en mappen in CustomLogs geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="16e4f-136">Then that is passed into Get-AzureStorageFile, which returns the files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="16e4f-137">Bestanden kopiëren</span><span class="sxs-lookup"><span data-stu-id="16e4f-137">Copy files</span></span>
<span data-ttu-id="16e4f-138">Vanaf versie 0.9.7 van Azure PowerShell kunt u een bestand kopiëren naar een ander bestand, een bestand naar een blob of een blob naar een bestand.</span><span class="sxs-lookup"><span data-stu-id="16e4f-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="16e4f-139">Hieronder ziet u hoe u deze kopieerbewerkingen uitvoert met PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="16e4f-139">Below we demonstrate how to perform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file to the new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob to a file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="16e4f-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="16e4f-140">Next steps</span></span>
<span data-ttu-id="16e4f-141">Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="16e4f-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="16e4f-142">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="16e4f-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="16e4f-143">Problemen oplossen in Windows</span><span class="sxs-lookup"><span data-stu-id="16e4f-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="16e4f-144">Problemen oplossen in Linux</span><span class="sxs-lookup"><span data-stu-id="16e4f-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    