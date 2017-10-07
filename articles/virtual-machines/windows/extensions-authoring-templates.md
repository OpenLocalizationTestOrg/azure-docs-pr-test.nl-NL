---
title: aaaAuthoring sjablonen met Windows VM-extensies | Microsoft Docs
description: Meer informatie over het ontwerpen van Azure Resource Manager-sjablonen met extensies voor VM's van Windows
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: c5156cb3859f7ff86bebda942150d268e57d6486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a>Azure Resource Manager-sjablonen met Windows VM-extensies
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

Voer vanuit Azure PowerShell hello Azure PowerShell-cmdlet te volgen:

      Get-AzureVMAvailableExtension


Deze cmdlet retourneert Hallo uitgeversnaam, naam en versie als volgt:

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

Deze drie eigenschappen toewijzen te 'publisher', 'type' en 'typeHandlerVersion' respectievelijk in Hallo hierboven sjabloon codefragment.

> [!NOTE]
> Het is altijd aanbevolen toouse Hallo nieuwste extensie versie tooget Hallo meest bijgewerkt functionaliteit.
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a>Hallo-schema voor Hallo extensie configuratieparameters identificeren
Hallo volgende stap bij het ontwerpen van een sjabloon voor de uitbreiding wordt tooidentify Hallo-indeling voor het ontwikkelen van parameters voor de configuratie. Elke uitbreiding ondersteunt een eigen set parameters.

Zie toolook op voorbeelden van configuraties voor Windows-uitbreidingen [voorbeelden van Windows-uitbreidingen](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Raadpleeg toohello tooget een volledig volledige sjabloon met VM-extensies te volgen.

[Extensie voor aangepaste scripts op een Windows VM](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

Na het Hallo-sjabloon schrijft, kunt u met behulp van Azure PowerShell implementeren.

