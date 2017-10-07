---
title: "aaaAbout installatiekopieën voor virtuele machines van Windows | Microsoft Docs"
description: Meer informatie over hoe afbeeldingen worden gebruikt met Windows virtuele machines in Azure.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a>Over de installatiekopieën voor virtuele machines van Windows
> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Zie voor meer informatie over het vinden en gebruiken van afbeeldingen in het Resource Manager-model Hallo [hier](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a>Werken met installatiekopieën

U kunt hello Azure PowerShell-module en hello Azure portal toomanage Hallo installatiekopieën beschikbaar tooyour Azure-abonnement gebruiken. Hello Azure PowerShell-module biedt meer opdrachtopties, zodat u precies wat kan leiden of wilt u toosee doen. Hello Azure-portal biedt een grafische gebruikersinterface voor veel van de dagelijkse beheertaken Hallo.

Hier volgen enkele voorbeelden die gebruikmaken van hello Azure PowerShell-module.

* **Ophalen van alle installatiekopieën**:`Get-AzureVMImage`retourneert een lijst met alle Hallo installatiekopieën beschikbaar zijn in uw huidige abonnement: uw afbeeldingen en die worden verstrekt door Azure of partners. de resulterende lijst Hallo kan oplopen. volgende voorbeelden kunt u zien hoe Hallo tooget een kortere lijst.
* **Opvragen van families van de afbeelding**:`Get-AzureVMImage | select ImageFamily` opgehaald van een lijst van families van de installatiekopie door te geven tekenreeksen **ImageFamily** eigenschap.
* **Ophalen van alle afbeeldingen in een specifieke productfamilie**:`Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`
* **VM-installatiekopieën vinden**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` deze cmdlet werkt met een filter Hallo DataDiskConfiguration eigenschap, die afbeeldingen tooVM is alleen van toepassing. In dit voorbeeld wordt ook Hallo tooonly Hallo label en image uitvoernaam filtert.
* **Opslaan van een algemene installatiekopie**:`Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`
* **Opslaan van de installatiekopie van een gespecialiseerde**:`Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`

  > [!TIP]
  > Hallo OSState parameter is vereist toocreate een VM-installatiekopie die omvat Hallo besturingssysteemschijf en gegevensschijven gekoppeld. Als u Hallo-parameter niet gebruikt, maakt het Hallo-cmdlet een installatiekopie van het besturingssysteem. Hallo-waarde van parameter Hallo aangeeft of Hallo-installatiekopie is gegeneraliseerd of speciale, gebaseerd op of de besturingssysteemschijf Hallo is voorbereid voor hergebruik.

* **Verwijderen van een installatiekopie van een**:`Remove-AzureVMImage –ImageName "MyOldVmImage"`

## <a name="next-steps"></a>Volgende stappen
U kunt ook [maken van een Windows-machine met behulp van Azure-portal Hallo](tutorial.md).
