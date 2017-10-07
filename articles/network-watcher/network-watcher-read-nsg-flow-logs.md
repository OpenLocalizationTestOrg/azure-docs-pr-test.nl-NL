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
# <a name="read-nsg-flow-logs"></a>NSG lezen stroom Logboeken

Meer informatie over hoe tooread NSG stroom vermeldingen registreert met PowerShell.

NSG stroom logboeken worden opgeslagen in een opslagaccount in [blok-blobs](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs). Blok-blobs bestaan uit kleinere blokken. Elk logboek is een afzonderlijke blok-blob die elk uur wordt gegenereerd. Nieuwe logboeken worden elk uur gegenereerd, Hallo logboeken worden bijgewerkt met nieuwe vermeldingen om de paar minuten met de meest recente gegevens Hallo. In dit artikel leert u hoe tooread gedeelten van Hallo logboeken stromen.

## <a name="scenario"></a>Scenario

In de Hallo scenario te volgen, hebt u een voorbeeld van de stroom logboek die is opgeslagen in een opslagaccount. we stapsgewijs hoe kunt u selectief Hallo meest recente gebeurtenissen in Logboeken van NSG-stroom lezen. In dit artikel gebruiken we PowerShell, Hallo concepten beschreven in artikel Hallo zijn echter niet beperkt toohello programmeertaal en toepasselijke tooall talen wordt ondersteund door hello Azure Storage-API 's

## <a name="setup"></a>Instellen

Voordat u begint, kunt u Network Security groep stromen-logboekregistratie is ingeschakeld op een of meer Netwerkbeveiligingsgroepen in uw account moet hebben. Voor instructies over het inschakelen van netwerkbeveiliging stromen Logboeken, raadpleeg dan toohello volgende artikel: [inleiding tooflow logboekregistratie voor Netwerkbeveiligingsgroepen](network-watcher-nsg-flow-logging-overview.md).

## <a name="retrieve-hello-block-list"></a>Lijst met geblokkeerde websites Hallo ophalen

Hallo PowerShell Hallo variabelen ingesteld na nodig tooquery hello NSG stroom Meld blob en lijst Hallo-blokken binnen Hallo [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) blok-blob. Hallo script toocontain geldige waarden voor uw omgeving bijwerken.

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

Hallo `$blockList` variabele retourneert een lijst van Hallo blokken in Hallo blob. Elk blok-blob bevat ten minste twee blokken.  Hallo eerste vereiste blok heeft een lengte van `21` bytes, dit blok bevat Hallo vierkante haken van Hallo json logboek openen. Hallo andere blok Hallo vierkant haakje sluiten en heeft een lengte van `9` bytes.  Zoals u ziet bevat Hallo na voorbeeld logboek zeven vermeldingen, elk een afzonderlijke vermelding wordt. Alle nieuwe vermeldingen in logboek Hallo toohello end aan vóór het laatste blok Hallo toegevoegd.

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

## <a name="read-hello-block-blob"></a>Lees Hallo blok-blob

Vervolgens moet tooread hello `$blocklist` variabele tooretrieve Hallo gegevens. In dit voorbeeld die we Hallo blocklist doorlopen Hallo bytes lezen van elk blok en ze in een matrix van artikel. We gebruiken Hallo [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) methode tooretrieve Hallo gegevens.

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

Nu Hallo `$valuearray` matrix Hallo tekenreekswaarde bevat van elk blok. tooverify Hallo-item, get Hallo tweede toohello laatste waarde van een matrix door te voeren Hallo `$valuearray[$valuearray.Length-2]`. We wil niet de laatste waarde Hallo is zojuist Hallo vierkant haakje sluiten.

Hallo-resultaten van deze waarde worden weergegeven in Hallo voorbeeld te volgen:

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

Dit scenario is een voorbeeld van hoe tooread vermeldingen in het NSG logboeken zonder tooparse Hallo hele logboek stromen. Als ze zijn geschreven met behulp van Hallo blok-ID of lengte van blokken die zijn opgeslagen in het blok-blob Hallo Hallo bijhouden, kunt u nieuwe vermeldingen in logboek Hallo lezen. Hiermee kunt u tooread alleen Hallo nieuwe vermeldingen.


## <a name="next-steps"></a>Volgende stappen

Ga naar [visualiseren met open-source hulpprogramma's van Azure-netwerk-Watcher NSG stroom logboeken](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) toolearn meer informatie over andere manieren tooview NSG stromen Logboeken.

meer informatie over de storage-blobs bezoeken toolearn: [bindingen van Azure Functions Blob-opslag](../azure-functions/functions-bindings-storage-blob.md)
