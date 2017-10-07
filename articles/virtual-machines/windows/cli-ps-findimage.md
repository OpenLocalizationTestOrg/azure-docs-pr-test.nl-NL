---
title: "installatiekopieën van aaaSelect virtuele Windows-machine in Azure | Microsoft Docs"
description: "Meer informatie over hoe toouse Azure PowerSHell toodetermine Hallo uitgever, aanbieding, SKU en versie voor Marketplace-VM-installatiekopieën."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a>Hoe toofind Windows VM installatiekopieën in hello Azure Marketplace met Azure PowerShell

Dit onderwerp wordt beschreven hoe toouse Azure PowerShell toofind VM installatiekopieën in hello Azure Marketplace. Gebruik deze informatie toospecify een Marketplace-installatiekopie bij het maken van een virtuele machine van Windows.

Zorg ervoor dat u geïnstalleerd en geconfigureerd Hallo nieuwste [Azure PowerShell-module](/powershell/azure/install-azurerm-ps).



## <a name="table-of-commonly-used-windows-images"></a>Tabel met veelgebruikte Windows-installatiekopieën
| PublisherName | Aanbieding | Sku |
|:--- |:--- |:--- |:--- |
| MicrosoftWindowsServer |WindowsServer |2016 Datacenter |
| MicrosoftWindowsServer |WindowsServer |2016 Datacenter-Server Core |
| MicrosoftWindowsServer |WindowsServer |2016 Datacenter met Containers |
| MicrosoftWindowsServer |WindowsServer |2016-Nano-Server |
| MicrosoftWindowsServer |WindowsServer |2012-R2-Datacenter |
| MicrosoftWindowsServer |WindowsServer |2008 R2 SP1 |
| MicrosoftDynamicsNAV |DynamicsNAV |2017 |
| MicrosoftSharePoint |MicrosoftSharePointServer |2016 |
| MicrosoftSQLServer |SQL2016 WS2016 |Enterprise |
| MicrosoftSQLServer |SQL2014SP2 WS2012R2 |Enterprise |
| MicrosoftWindowsServerHPCPack |WindowsServerHPCPack |2012R2 |
| MicrosoftWindowsServerEssentials |WindowsServerEssentials |WindowsServerEssentials |

## <a name="find-specific-images"></a>Specifieke installatiekopieën zoeken


Wanneer u een nieuwe virtuele machine maakt met Azure Resource Manager, in sommige gevallen moet u toospecify een afbeelding met Hallo combinatie van Hallo eigenschappen van de installatiekopie te volgen:

* Uitgever
* Aanbieding
* SKU

Gebruik bijvoorbeeld deze waarden met Hallo [Set AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell-cmdlet of met een resource groep sjabloon waarin u Hallo type VM toobe gemaakt moet opgeven.

Als u deze waarden nodig toodetermine hebt, kunt u Hallo uitvoeren [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), en [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets toonavigate hello afbeeldingen. U bepalen deze waarden:

1. Lijst Hallo installatiekopie uitgevers.
2. Geef de aanbiedingen voor een bepaalde uitgever weer.
3. Geef de SKU's voor een bepaalde aanbieding weer.

Lijst eerst Hallo uitgevers Hello volgende opdrachten:

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

Vul de naam van uw gekozen publisher en Voer Hallo volgende opdrachten uit:

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Vul de aanbiedingsnaam van uw gekozen en Voer Hallo volgende opdrachten uit:

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

Uit de uitvoer Hallo Hallo `Get-AzureRMVMImageSku` uitvoert, en u alle Hallo informatie u toospecify Hallo installatiekopie voor een nieuwe virtuele machine nodig hebt.

Hallo hieronder vindt u een voorbeeld van een volledige:

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

Uitvoer:

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

Hallo 'Legitieme Microsoft Windows Server' Publisher:

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Uitvoer:

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

Voor Windows ' Server' hello bieden:

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

Uitvoer:

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

In deze lijst kopiëren Hallo gekozen SKU-naam, en hebt u alle Hallo-informatie voor Hallo `Set-AzureRMVMSourceImage` PowerShell-cmdlet of voor een resource group-sjabloon.

## <a name="next-steps"></a>Volgende stappen
Nu kunt u precies Hallo installatiekopie wilt toouse. toocreate een virtuele machine snel met behulp van de installatiekopiegegevens hello, die u zojuist hebt gevonden, Zie [virtuele Windows-machine maken met PowerShell](quick-create-powershell.md).
