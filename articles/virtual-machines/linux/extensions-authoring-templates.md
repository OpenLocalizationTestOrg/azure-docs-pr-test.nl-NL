---
title: aaaAuthoring sjablonen met Linux VM-extensies | Microsoft Docs
description: Meer informatie over het ontwerpen van Azure Resource Manager-sjablonen met uitbreidingen voor virtuele Linux-machines
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 322f8f0b-6697-4acb-b5f3-b3f58d28358b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: b797e442d8706956bbc06c5be611a2b0119055d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a>Azure Resource Manager-sjablonen met Linux VM-extensies
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

Uitvoeren van Azure CLI Hallo verbindingsopdracht te volgen:

      Azure VM extension list

Deze opdracht retourneert Hallo publisher naam, de naam van de uitbreiding en de versie als volgt:

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

toolook op voorbeelden van configuraties voor Linux-uitbreidingen, klikt u op het Hallo-documentatie voor Zie [voorbeelden van Linux eExtensions](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Raadpleeg toohello tooget een volledig volledige sjabloon met VM-extensies te volgen.

[Extensie voor aangepaste scripts op een Linux-VM](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

Na het Hallo-sjabloon schrijft, kunt u met behulp van Azure CLI Hallo implementeren.

