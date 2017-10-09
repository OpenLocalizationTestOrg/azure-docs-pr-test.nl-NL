---
title: aaaCreate kopie maken van een Azure beheerd schijf voor back-up | Microsoft Docs
description: Meer informatie over hoe toocreate een kopie van een Azure-schijf beheerd toouse voor reserve of probleemoplossing schijf uitgeeft.
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Maak een kopie van een VHD die is opgeslagen als een beheerde Azure-schijf met behulp van momentopnamen beheerd
Een momentopname van een schijf beheerd voor back-up of een schijf beheerd vanuit Hallo momentopname maken en deze te koppelen tooa test virtuele machine tootroubleshoot. Een momentopname van een beheerd is een volledige point-in-time-kopie van een schijf VM beheerd. Deze maakt een alleen-lezen kopie van uw VHD en standaard opgeslagen als een standaard beheerde schijf. Zie voor meer informatie over beheerde schijven [overzicht van beheerde Azure-schijven](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

Zie voor meer informatie over prijzen [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/). 

## <a name="before-you-begin"></a>Voordat u begint
Als u PowerShell gebruikt, zorg ervoor dat u de meest recente versie Hallo Hallo AzureRM.Compute PowerShell-module hebt. Voer Hallo na de opdracht tooinstall deze.

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).

## <a name="copy-hello-vhd-with-a-snapshot"></a>Hallo VHD met een momentopname kopiëren
Hello Azure-portal of PowerShell tootake een momentopname van Hallo beheerd schijf gebruiken.

### <a name="use-azure-portal-tootake-a-snapshot"></a>Azure portal tootake een momentopname gebruiken 

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Beginnen in de linkerbovenhoek hello, klikt u op **nieuw** en zoek naar **momentopname**.
3. Klik op Hallo momentopname blade **maken**.
4. Voer een **naam** voor Hallo momentopname.
5. Selecteer een bestaande [resourcegroep](../../azure-resource-manager/resource-group-overview.md#resource-groups) of Hallo typenaam voor een nieuwe resourcegroep. 
6. Selecteer een Azure-datacenter locatie.  
7. Voor **bronschijf**, selecteer Hallo toosnapshot schijf beheerd.
8. Selecteer Hallo **accounttype** toouse toostore Hallo momentopname. Het is raadzaam **Standard_LRS** tenzij u deze opgeslagen op een hoog presterende schijf nodig.
9. Klik op **Create**.

### <a name="use-powershell-tootake-a-snapshot"></a>Gebruik PowerShell tootake een momentopname
Hallo volgende stappen ziet u hoe tooget Hallo VHD schijf toobe gekopieerd, maken Hallo momentopnameconfiguraties en een momentopname van het Hallo-schijf met behulp van de cmdlet New-AzureRmSnapshot hello<!--Add link toocmdlet when available-->. 

1. Sommige parameters instellen. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  Vervang de parameterwaarden Hallo:
  -  "myResourceGroup" met de resourcegroep Hallo van de virtuele machine.
  -  'southeastasia' hello geografische locatie waar u uw beheerde momentopname opgeslagen. <!---How do you look these up? -->
  -  "ContosoMD_datadisk1" met de naam van de Hallo van Hallo VHD schijf die u toocopy wilt.
  -  'ContosoMD_datadisk1_snapshot1' Hello servernaam die u hebt toouse voor nieuwe Hallo-momentopname wilt instellen.

2. Hallo VHD schijf toobe gekopieerd ophalen.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. Hallo momentopnameconfiguraties maken. 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. Hallo momentopname.

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
Als u toouse Hallo momentopname toocreate van plan een schijf beheerd bent en koppelt u dit een virtuele machine die toobe hoge prestaties behoeften, gebruikt u Hallo parameter `-AccountType Premium_LRS` met Hallo nieuw AzureRmSnapshot-opdracht. Hallo-parameter wordt Hallo momentopname gemaakt, zodat deze wordt opgeslagen als een schijf Premium beheerd. Premium-schijven beheerd zijn duurder dan de standaard. Daarom moet u dat wat u moet Premium voordat u deze parameter.


