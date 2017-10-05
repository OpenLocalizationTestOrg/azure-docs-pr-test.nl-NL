---
title: Maak een kopie van een Azure beheerd schijf voor back up | Microsoft Docs
description: Informatie over het maken van een kopie van een Azure beheerd schijf moet worden gebruikt voor back up of het oplossen van problemen van de schijf.
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
ms.openlocfilehash: a7527b12f4f0d2b45713a0c0109d81ff51293fd8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Maak een kopie van een VHD die is opgeslagen als een beheerde Azure-schijf met behulp van momentopnamen beheerd
Een momentopname van een schijf beheerd voor back-up of een schijf beheerd vanaf de momentopname maken en koppelen aan een virtuele testmachine om op te lossen. Een momentopname van een beheerd is een volledige point-in-time-kopie van een schijf VM beheerd. Deze maakt een alleen-lezen kopie van uw VHD en standaard opgeslagen als een standaard beheerde schijf. Zie voor meer informatie over beheerde schijven [overzicht van beheerde Azure-schijven](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

Zie voor meer informatie over prijzen [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/). 

## <a name="before-you-begin"></a>Voordat u begint
Als u PowerShell gebruikt, zorg ervoor dat u de nieuwste versie van de AzureRM.Compute PowerShell-module hebt. Voer de volgende opdracht om deze te installeren.

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).

## <a name="copy-the-vhd-with-a-snapshot"></a>Kopieer de VHD met een momentopname
Azure portal of PowerShell gebruiken om een momentopname van de schijf worden beheerd.

### <a name="use-azure-portal-to-take-a-snapshot"></a>Azure portal gebruiken om een momentopname 

1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Beginnen in de linkerbovenhoek, klikt u op **nieuw** en zoek naar **momentopname**.
3. Klik op de blade momentopname **maken**.
4. Voer een **naam** voor de momentopname.
5. Selecteer een bestaande [Resourcegroep](../../azure-resource-manager/resource-group-overview.md#resource-groups) of typ de gewenste naam voor een nieuwe resourcegroep. 
6. Selecteer een Azure-datacenter locatie.  
7. Voor **bronschijf**, selecteert u de schijf worden beheerd met de momentopname.
8. Selecteer de **accounttype** moet worden gebruikt voor het opslaan van de momentopname. Het is raadzaam **Standard_LRS** tenzij u deze opgeslagen op een hoog presterende schijf nodig.
9. Klik op **Create**.

### <a name="use-powershell-to-take-a-snapshot"></a>PowerShell gebruiken om een momentopname
De volgende stappen ziet u hoe u de VHD-schijf moet worden gekopieerd, maken de momentopnameconfiguraties en een momentopname van de schijf met de cmdlet New-AzureRmSnapshot<!--Add link to cmdlet when available-->. 

1. Sommige parameters instellen. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  Vervang de parameterwaarden:
  -  "myResourceGroup" met de resourcegroep van de VM.
  -  "southeastasia" met de geografische locatie waar u uw beheerde momentopname opgeslagen. <!---How do you look these up? -->
  -  "ContosoMD_datadisk1" met de naam van de VHD-schijf die u wilt kopiëren.
  -  "ContosoMD_datadisk1_snapshot1" met de naam die u wilt gebruiken voor de nieuwe momentopname.

2. Ophalen van de VHD-schijf moet worden gekopieerd.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. Maken van de momentopnameconfiguraties. 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. De momentopname.

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
Als u van plan bent de momentopname gebruiken om te maken van een schijf beheerd en koppelt u dit een virtuele machine die moet worden hoge prestaties, gebruikt u de parameter `-AccountType Premium_LRS` met de opdracht New-AzureRmSnapshot. De parameter wordt de momentopname gemaakt zodat deze wordt opgeslagen als een schijf Premium beheerd. Premium-schijven beheerd zijn duurder dan de standaard. Daarom moet u dat wat u moet Premium voordat u deze parameter.


