---
title: aaaRead NSG stromen Logboeken | Microsoft Docs
description: Dit artikel laat zien hoe tooparse NSG stroom registreert
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: gwallace
ms.openlocfilehash: b4f0f64639c7b2a6b4db50e54d15056bfd809e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="read-nsg-flow-logs"></a><span data-ttu-id="40077-103">NSG lezen stroom Logboeken</span><span class="sxs-lookup"><span data-stu-id="40077-103">Read NSG flow logs</span></span>

<span data-ttu-id="40077-104">Meer informatie over hoe tooread NSG stroom vermeldingen registreert met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40077-104">Learn how tooread NSG flow logs entries with PowerShell.</span></span>

<span data-ttu-id="40077-105">NSG stroom logboeken worden opgeslagen in een opslagaccount in [blok-blobs](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs).</span><span class="sxs-lookup"><span data-stu-id="40077-105">NSG flow logs are stored in a storage account in [block blobs](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs).</span></span> <span data-ttu-id="40077-106">Blok-blobs bestaan uit kleinere blokken.</span><span class="sxs-lookup"><span data-stu-id="40077-106">Block blobs are made up of smaller blocks.</span></span> <span data-ttu-id="40077-107">Elk logboek is een afzonderlijke blok-blob die elk uur wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="40077-107">Each log is a separate block blob that is generated every hour.</span></span> <span data-ttu-id="40077-108">Nieuwe logboeken worden elk uur gegenereerd, Hallo logboeken worden bijgewerkt met nieuwe vermeldingen om de paar minuten met de meest recente gegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="40077-108">New logs are generated every hour, hello logs are updated with new entries every few minutes with hello latest data.</span></span> <span data-ttu-id="40077-109">In dit artikel leert u hoe tooread gedeelten van Hallo logboeken stromen.</span><span class="sxs-lookup"><span data-stu-id="40077-109">In this article you learn how tooread portions of hello flow logs.</span></span>

## <a name="scenario"></a><span data-ttu-id="40077-110">Scenario</span><span class="sxs-lookup"><span data-stu-id="40077-110">Scenario</span></span>

<span data-ttu-id="40077-111">In de Hallo scenario te volgen, hebt u een voorbeeld van de stroom logboek die is opgeslagen in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="40077-111">In hello following scenario, you have an example flow log that is stored in a storage account.</span></span> <span data-ttu-id="40077-112">we stapsgewijs hoe kunt u selectief Hallo meest recente gebeurtenissen in Logboeken van NSG-stroom lezen.</span><span class="sxs-lookup"><span data-stu-id="40077-112">we step through how you can selectively read hello latest events in NSG flow logs.</span></span> <span data-ttu-id="40077-113">In dit artikel gebruiken we PowerShell, Hallo concepten beschreven in artikel Hallo zijn echter niet beperkt toohello programmeertaal en toepasselijke tooall talen wordt ondersteund door hello Azure Storage-API 's</span><span class="sxs-lookup"><span data-stu-id="40077-113">In this article we will use PowerShell, however, hello concepts discussed in hello article are not limited toohello programming language and are applicable tooall languages supported by hello Azure Storage APIs</span></span>

## <a name="setup"></a><span data-ttu-id="40077-114">Instellen</span><span class="sxs-lookup"><span data-stu-id="40077-114">Setup</span></span>

<span data-ttu-id="40077-115">Voordat u begint, kunt u Network Security groep stromen-logboekregistratie is ingeschakeld op een of meer Netwerkbeveiligingsgroepen in uw account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="40077-115">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="40077-116">Voor instructies over het inschakelen van netwerkbeveiliging stromen Logboeken, raadpleeg dan toohello volgende artikel: [inleiding tooflow logboekregistratie voor Netwerkbeveiligingsgroepen](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40077-116">For instructions on enabling Network Security flow logs, refer toohello following article: [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="retrieve-hello-block-list"></a><span data-ttu-id="40077-117">Lijst met geblokkeerde websites Hallo ophalen</span><span class="sxs-lookup"><span data-stu-id="40077-117">Retrieve hello block list</span></span>

<span data-ttu-id="40077-118">Hallo PowerShell Hallo variabelen ingesteld na nodig tooquery hello NSG stroom Meld blob en lijst Hallo-blokken binnen Hallo [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) blok-blob.</span><span class="sxs-lookup"><span data-stu-id="40077-118">hello following PowerShell sets up hello variables needed tooquery hello NSG flow log blob and list hello blocks within hello [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) block blob.</span></span> <span data-ttu-id="40077-119">Hallo script toocontain geldige waarden voor uw omgeving bijwerken.</span><span class="sxs-lookup"><span data-stu-id="40077-119">Update hello script toocontain valid values for your environment.</span></span>

```powershell
# hello SubscriptionID toouse
$subscriptionId = "00000000-0000-0000-0000-000000000000"

# Resource group that contains hello Network Security Group
$resourceGroupName = "<resourceGroupName>"

# hello name of hello Network Security Group
$nsgName = "NSGName"

# hello storage account name that contains hello NSG logs
$storageAccountName = "<storageAccountName>" 

# hello date and time for hello log toobe queried, logs are stored in hour intervals.
[datetime]$logtime = "06/16/2017 20:00"

# Retrieve hello primary storage account key tooaccess hello NSG logs
$StorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName).Value[0]

# Setup a new storage context toobe used tooquery hello logs
$ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

# Container name used by NSG flow logs
$ContainerName = "insights-logs-networksecuritygroupflowevent"

# Name of hello blob that contains hello NSG flow log
$BlobName = "resourceId=/SUBSCRIPTIONS/${subscriptionId}/RESOURCEGROUPS/${resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/${nsgName}/y=$($logtime.Year)/m=$(($logtime).ToString("MM"))/d=$(($logtime).ToString("dd"))/h=$(($logtime).ToString("HH"))/m=00/PT1H.json"

# Gets hello storage blog
$Blob = Get-AzureStorageBlob -Context $ctx -Container $ContainerName -Blob $BlobName

# Gets hello block blog of type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from hello storage blob
$CloudBlockBlob = [Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob] $Blob.ICloudBlob

# Stores hello block list in a variable from hello block blob.
$blockList = $CloudBlockBlob.DownloadBlockList()
```

<span data-ttu-id="40077-120">Hallo `$blockList` variabele retourneert een lijst van Hallo blokken in Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="40077-120">hello `$blockList` variable returns a list of hello blocks in hello blob.</span></span> <span data-ttu-id="40077-121">Elk blok-blob bevat ten minste twee blokken.</span><span class="sxs-lookup"><span data-stu-id="40077-121">Each block blob contains at least two blocks.</span></span>  <span data-ttu-id="40077-122">Hallo eerste vereiste blok heeft een lengte van `21` bytes, dit blok bevat Hallo vierkante haken van Hallo json logboek openen.</span><span class="sxs-lookup"><span data-stu-id="40077-122">hello first block has a length of `21` bytes, this block contains hello opening brackets of hello json log.</span></span> <span data-ttu-id="40077-123">Hallo andere blok Hallo vierkant haakje sluiten en heeft een lengte van `9` bytes.</span><span class="sxs-lookup"><span data-stu-id="40077-123">hello other block is hello closing brackets and has a length of `9` bytes.</span></span>  <span data-ttu-id="40077-124">Zoals u ziet bevat Hallo na voorbeeld logboek zeven vermeldingen, elk een afzonderlijke vermelding wordt.</span><span class="sxs-lookup"><span data-stu-id="40077-124">As you can see hello following example log has seven entries in it, each being an individual entry.</span></span> <span data-ttu-id="40077-125">Alle nieuwe vermeldingen in logboek Hallo toohello end aan vóór het laatste blok Hallo toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="40077-125">All new entries in hello log are added toohello end right before hello final block.</span></span>

```
Name                                         Length Committed
----                                         ------ ---------
ZDk5MTk5N2FkNGE0MmY5MTk5ZWViYjA0YmZhODRhYzY=     21      True
NzQxNDA5MTRhNDUzMGI2M2Y1MDMyOWZlN2QwNDZiYzQ=   2685      True
ODdjM2UyMWY3NzFhZTU3MmVlMmU5MDNlOWEwNWE3YWY=   2586      True
ZDU2MjA3OGQ2ZDU3MjczMWQ4MTRmYWNhYjAzOGJkMTg=   2688      True
ZmM3ZWJjMGQ0ZDA1ODJlOWMyODhlOWE3MDI1MGJhMTc=   2775      True
ZGVkYTc4MzQzNjEyMzlmZWE5MmRiNjc1OWE5OTc0OTQ=   2676      True
ZmY2MjUzYTIwYWIyOGU1OTA2ZDY1OWYzNmY2NmU4ZTY=   2777      True
Mzk1YzQwM2U0ZWY1ZDRhOWFlMTNhYjQ3OGVhYmUzNjk=   2675      True
ZjAyZTliYWE3OTI1YWZmYjFmMWI0MjJhNzMxZTI4MDM=      9      True
```

## <a name="read-hello-block-blob"></a><span data-ttu-id="40077-126">Lees Hallo blok-blob</span><span class="sxs-lookup"><span data-stu-id="40077-126">Read hello block blob</span></span>

<span data-ttu-id="40077-127">Vervolgens moet tooread hello `$blocklist` variabele tooretrieve Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="40077-127">Next we need tooread hello `$blocklist` variable tooretrieve hello data.</span></span> <span data-ttu-id="40077-128">In dit voorbeeld die we Hallo blocklist doorlopen Hallo bytes lezen van elk blok en ze in een matrix van artikel.</span><span class="sxs-lookup"><span data-stu-id="40077-128">In this example we iterate through hello blocklist, read hello bytes from each block and story them in an array.</span></span> <span data-ttu-id="40077-129">We gebruiken Hallo [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) methode tooretrieve Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="40077-129">We use hello [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) method tooretrieve hello data.</span></span>

```powershell
# Set hello size of hello byte array toohello largest block
$maxvalue = ($blocklist | measure Length -Maximum).Maximum

# Create an array toostore values in
$valuearray = @()

# Define hello starting index tootrack hello current block being read
$index = 0

# Loop through each block in hello block list
for($i=0; $i -lt $blocklist.count; $i++)
{

# Create a byte array object toostory hello bytes from hello block
$downloadArray = New-Object -TypeName byte[] -ArgumentList $maxvalue

# Download hello data into hello ByteArray, starting with hello current index, for hello number of bytes in hello current block. Index is increased by 3 when reading tooremove preceding comma.
$CloudBlockBlob.DownloadRangeToByteArray($downloadArray,0,$index+3,$($blockList[$i].Length-1)) | Out-Null

# Increment hello index by adding hello current block length toohello previous index
$index = $index + $blockList[$i].Length

# Retrieve hello string from hello byte array

$value = [System.Text.Encoding]::ASCII.GetString($downloadArray)

# Add hello log entry toohello value array
$valuearray += $value
}
```

<span data-ttu-id="40077-130">Nu Hallo `$valuearray` matrix Hallo tekenreekswaarde bevat van elk blok.</span><span class="sxs-lookup"><span data-stu-id="40077-130">Now hello `$valuearray` array contains hello string value of each block.</span></span> <span data-ttu-id="40077-131">tooverify Hallo-item, get Hallo tweede toohello laatste waarde van een matrix door te voeren Hallo `$valuearray[$valuearray.Length-2]`.</span><span class="sxs-lookup"><span data-stu-id="40077-131">tooverify hello entry, get hello second toohello last value from hello array by running `$valuearray[$valuearray.Length-2]`.</span></span> <span data-ttu-id="40077-132">We wil niet de laatste waarde Hallo is zojuist Hallo vierkant haakje sluiten.</span><span class="sxs-lookup"><span data-stu-id="40077-132">We do not want hello last value is just hello closing bracket.</span></span>

<span data-ttu-id="40077-133">Hallo-resultaten van deze waarde worden weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="40077-133">hello results of this value are shown in hello following example:</span></span>

```json
        {
             "time": "2017-06-16T20:59:43.7340000Z",
             "systemId": "5f4d02d3-a7d0-4ed4-9ce8-c0ae9377951c",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/CONTOSORG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/CONTOSONSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_AllowInternetOutBound","flows":[{"mac":"000D3A18077E","flowTuples":["1497646722,10.0.0.4,168.62.32.14,44904,443,T,O,A","1497646722,10.0.0.4,52.240.48.24,45218,443,T,O,A","1497646725,10.
0.0.4,168.62.32.14,44910,443,T,O,A","1497646725,10.0.0.4,52.240.48.24,45224,443,T,O,A","1497646728,10.0.0.4,168.62.32.14,44916,443,T,O,A","1497646728,10.0.0.4,52.240.48.24,45230,443,T,O,A","1497646732,10.0.0.4,168.62.32.14,44922,443,T,O,A","14976
46732,10.0.0.4,52.240.48.24,45236,443,T,O,A","1497646735,10.0.0.4,168.62.32.14,44928,443,T,O,A","1497646735,10.0.0.4,52.240.48.24,45242,443,T,O,A","1497646738,10.0.0.4,168.62.32.14,44934,443,T,O,A","1497646738,10.0.0.4,52.240.48.24,45248,443,T,O,
A","1497646742,10.0.0.4,168.62.32.14,44942,443,T,O,A","1497646742,10.0.0.4,52.240.48.24,45256,443,T,O,A","1497646745,10.0.0.4,168.62.32.14,44948,443,T,O,A","1497646745,10.0.0.4,52.240.48.24,45262,443,T,O,A","1497646749,10.0.0.4,168.62.32.14,44954
,443,T,O,A","1497646749,10.0.0.4,52.240.48.24,45268,443,T,O,A","1497646753,10.0.0.4,168.62.32.14,44960,443,T,O,A","1497646753,10.0.0.4,52.240.48.24,45274,443,T,O,A","1497646756,10.0.0.4,168.62.32.14,44966,443,T,O,A","1497646756,10.0.0.4,52.240.48
.24,45280,443,T,O,A","1497646759,10.0.0.4,168.62.32.14,44972,443,T,O,A","1497646759,10.0.0.4,52.240.48.24,45286,443,T,O,A","1497646763,10.0.0.4,168.62.32.14,44978,443,T,O,A","1497646763,10.0.0.4,52.240.48.24,45292,443,T,O,A","1497646766,10.0.0.4,
168.62.32.14,44984,443,T,O,A","1497646766,10.0.0.4,52.240.48.24,45298,443,T,O,A","1497646769,10.0.0.4,168.62.32.14,44990,443,T,O,A","1497646769,10.0.0.4,52.240.48.24,45304,443,T,O,A","1497646773,10.0.0.4,168.62.32.14,44996,443,T,O,A","1497646773,
10.0.0.4,52.240.48.24,45310,443,T,O,A","1497646776,10.0.0.4,168.62.32.14,45002,443,T,O,A","1497646776,10.0.0.4,52.240.48.24,45316,443,T,O,A","1497646779,10.0.0.4,168.62.32.14,45008,443,T,O,A","1497646779,10.0.0.4,52.240.48.24,45322,443,T,O,A"]}]}
,{"rule":"DefaultRule_DenyAllInBound","flows":[]},{"rule":"UserRule_ssh-rule","flows":[]},{"rule":"UserRule_web-rule","flows":[{"mac":"000D3A18077E","flowTuples":["1497646738,13.82.225.93,10.0.0.4,1180,80,T,I,A","1497646750,13.82.225.93,10.0.0.4,
1184,80,T,I,A","1497646768,13.82.225.93,10.0.0.4,1181,80,T,I,A","1497646780,13.82.225.93,10.0.0.4,1336,80,T,I,A"]}]}]}
        }
```

<span data-ttu-id="40077-134">Dit scenario is een voorbeeld van hoe tooread vermeldingen in het NSG logboeken zonder tooparse Hallo hele logboek stromen.</span><span class="sxs-lookup"><span data-stu-id="40077-134">This scenario is an example of how tooread entries in NSG flow logs without having tooparse hello entire log.</span></span> <span data-ttu-id="40077-135">Als ze zijn geschreven met behulp van Hallo blok-ID of lengte van blokken die zijn opgeslagen in het blok-blob Hallo Hallo bijhouden, kunt u nieuwe vermeldingen in logboek Hallo lezen.</span><span class="sxs-lookup"><span data-stu-id="40077-135">You can read new entries in hello log as they are written by using hello block ID or by tracking hello length of blocks stored in hello block blob.</span></span> <span data-ttu-id="40077-136">Hiermee kunt u tooread alleen Hallo nieuwe vermeldingen.</span><span class="sxs-lookup"><span data-stu-id="40077-136">This allows you tooread only hello new entries.</span></span>


## <a name="next-steps"></a><span data-ttu-id="40077-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="40077-137">Next steps</span></span>

<span data-ttu-id="40077-138">Ga naar [visualiseren met open-source hulpprogramma's van Azure-netwerk-Watcher NSG stroom logboeken](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) toolearn meer informatie over andere manieren tooview NSG stromen Logboeken.</span><span class="sxs-lookup"><span data-stu-id="40077-138">Visit [visualize Azure Network Watcher NSG flow logs using open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) toolearn more about other ways tooview NSG flow logs.</span></span>

<span data-ttu-id="40077-139">meer informatie over de storage-blobs bezoeken toolearn: [bindingen van Azure Functions Blob-opslag](../azure-functions/functions-bindings-storage-blob.md)</span><span class="sxs-lookup"><span data-stu-id="40077-139">toolearn more about storage blobs visit: [Azure Functions Blob storage bindings](../azure-functions/functions-bindings-storage-blob.md)</span></span>
