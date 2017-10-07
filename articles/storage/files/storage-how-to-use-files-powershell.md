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
ms.openlocfilehash: 7bd84c9cfa31782aedf4a209cb15d4b8d92e2737
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a>Hoe toouse PowerShell toomanage Azure File storage
U kunt Azure PowerShell toocreate gebruiken en beheren van bestandsshares.

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a>Hallo PowerShell-cmdlets voor Azure Storage installeren
tooprepare toouse PowerShell, download en installeer hello Azure PowerShell-cmdlets. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs) installeren voor Hallo installatiepunt en de installatie-instructies.

> [!NOTE]
> Het verdient aanbeveling dat u downloaden en installeren of upgraden van de meest recente Azure PowerShell-module toohello.
> 
> 

Open een Azure PowerShell-venster door op **Start** te klikken en **Windows PowerShell** te typen. Hallo PowerShell-venster wordt hello Azure Powershell-module voor u geladen.

## <a name="create-a-context-for-your-storage-account-and-key"></a>Een context maken voor uw opslagaccount en -sleutel
Hallo storage account context maken. Hallo context ingekapseld Hallo naam en opslagaccountsleutel. Voor instructies voor het kopiëren van de accountsleutel uit Hallo [Azure-portal](https://portal.azure.com), Zie [weergeven en kopiëren opslagtoegangssleutels](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).

Vervang `storage-account-name` en `storage-account-key` opslagaccountnaam en sleutel van uw in Hallo voorbeeld te volgen.

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a>Een nieuwe bestandsshare maken
Maak nieuwe share hello, met de naam `logs`.

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

U hebt nu een bestandsshare in File Storage. Nu gaan we een map en een bestand toevoegen.

> [!IMPORTANT]
> Hallo-naam van de bestandsshare moet alleen kleine letters bevatten. Zie [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx) (Shares, mappen, bestanden en metagegevens een naam geven en hiernaar verwijzen) voor meer informatie over de naamgeving van bestandsshares en bestanden.
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a>Maak een map in Hallo-bestandsshare
Maak een map op Hallo-share. In de Hallo voorbeeld te volgen, Hallo directory heet `CustomLogs`.

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a>Uploaden van een lokale map voor toohello
Upload nu een lokaal bestand toohello-map. Hallo volgende voorbeeld wordt een bestand geüpload vanuit `C:\temp\Log1.txt`. Hallo-bestandspad bewerken zodat deze tooa geldig bestand op uw lokale machine verwijst.

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a>Lijst Hallo bestanden in de directory Hallo
toosee Hallo-bestand in map hello, kunt u alle bestanden van de directory Hallo kunt aanbieden. Met deze opdracht retourneert Hallo bestanden en submappen (wanneer aanwezig) in Hallo map customlogs.

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

Get-AzureStorageFile retourneert een lijst met bestanden en mappen voor elk mapobject dat daaraan is doorgegeven. ' Get-AzureStorageFile-Share $s "retourneert een lijst met bestanden en mappen in de hoofdmap Hallo. een lijst met bestanden in een submap tooget, hebt u toopass Hallo submap tooGet-AzureStorageFile. Dit is wat dit heeft--Hallo eerste deel van de opdracht Hallo up toohello pipe retourneert een mapexemplaar van Hallo submap CustomLogs. Vervolgens wordt dit doorgegeven via Get-azurestoragefile, die als Hallo bestanden en mappen in CustomLogs resultaat.

## <a name="copy-files"></a>Bestanden kopiëren
Vanaf versie 0.9.7 van Azure PowerShell, kunt u een bestand tooanother, een bestand tooa blob of een blob tooa-bestand kopiëren. Hieronder ziet u hoe tooperform die deze kopiëren bewerkingen met behulp van PowerShell-cmdlets.

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a>Volgende stappen
Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.

* [Veelgestelde vragen](../storage-files-faq.md)
* [Problemen oplossen in Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Problemen oplossen in Linux](storage-troubleshoot-linux-file-connection-problems.md)    