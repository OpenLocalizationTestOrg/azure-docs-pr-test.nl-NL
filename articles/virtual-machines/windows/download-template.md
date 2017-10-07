---
title: aaaDownload hello sjabloon voor een virtuele machine in Azure | Microsoft Docs
description: Hallo templatefor een VM-toohelp om implementaties van Resource Manager-implementatiemodel Hallo automatiseren downloaden
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a>Hallo-sjabloon downloaden voor een virtuele machine
Wanneer u een virtuele machine in Azure maakt wordt via Hallo portal of PowerShell, een Resource Manager sjabloon automatisch voor u gemaakt. U kunt deze sjabloon tooquickly duplicaat een implementatie gebruiken. Hallo-sjabloon bevat informatie over alle Hallo resources in een resourcegroep. Voor een virtuele machine, betekent dit dat Hallo sjabloon bevat alles wat u ter ondersteuning van Hallo VM in die resourcegroep, met inbegrip van netwerkresources hello wordt gemaakt.

## <a name="download-hello-template-using-hello-portal"></a>Met behulp van de portal Hallo Hallo-sjabloon downloaden
1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Een Hallo hub-menu Selecteer **virtuele Machines**.
3. Selecteer Hallo virtuele machine uit de lijst Hallo.
4. Selecteer **automatiseringsscript**.
5. Selecteer **downloaden** en Hallo ZIP-bestand tooyour lokale computer op te slaan.
6. Hallo ZIP-bestand openen en Hallo bestanden tooa map halen. Hallo ZIP-bestand bevat:
   
   * Deploy.ps1
   * Deploy.sh 
   * deployer.RB
   * DeploymentHelper.cs
   * parameters.JSON
   * Template.JSON

Hallo template.json bestand is Hallo-sjabloon.

## <a name="download-hello-template-using-powershell"></a>Met behulp van PowerShell Hallo-sjabloon downloaden
U kunt ook downloaden Hallo .json-sjabloonbestand met Hallo [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet. U kunt Hallo `-path` parameter tooprovide Hallo bestandsnaam en het pad voor Hallo .json-bestand. Dit voorbeeld ziet u hoe de naam van toodownload Hallo sjabloon voor de resourcegroep Hallo **myResourceGroup** toohello **C:\users\public\downloads** map op uw lokale computer.

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a>Volgende stappen
Zie toolearn meer informatie over het implementeren van resources met behulp van sjablonen [overzicht voor Resource Manager-sjabloon](../../azure-resource-manager/resource-manager-template-walkthrough.md).

