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
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="708d6-103">Azure Resource Manager-sjablonen met Linux VM-extensies</span><span class="sxs-lookup"><span data-stu-id="708d6-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="708d6-104">Uitvoeren van Azure CLI Hallo verbindingsopdracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="708d6-104">From Azure CLI, run hello following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="708d6-105">Deze opdracht retourneert Hallo publisher naam, de naam van de uitbreiding en de versie als volgt:</span><span class="sxs-lookup"><span data-stu-id="708d6-105">This command returns hello publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="708d6-106">Deze drie eigenschappen toewijzen te 'publisher', 'type' en 'typeHandlerVersion' respectievelijk in Hallo hierboven sjabloon codefragment.</span><span class="sxs-lookup"><span data-stu-id="708d6-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="708d6-107">Het is altijd aanbevolen toouse Hallo nieuwste extensie versie tooget Hallo meest bijgewerkt functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="708d6-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="708d6-108">Hallo-schema voor Hallo extensie configuratieparameters identificeren</span><span class="sxs-lookup"><span data-stu-id="708d6-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="708d6-109">Hallo volgende stap bij het ontwerpen van een sjabloon voor de uitbreiding wordt tooidentify Hallo-indeling voor het ontwikkelen van parameters voor de configuratie.</span><span class="sxs-lookup"><span data-stu-id="708d6-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="708d6-110">Elke uitbreiding ondersteunt een eigen set parameters.</span><span class="sxs-lookup"><span data-stu-id="708d6-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="708d6-111">toolook op voorbeelden van configuraties voor Linux-uitbreidingen, klikt u op het Hallo-documentatie voor Zie [voorbeelden van Linux eExtensions](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="708d6-111">toolook at sample configurations for Linux extensions, click hello documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="708d6-112">Raadpleeg toohello tooget een volledig volledige sjabloon met VM-extensies te volgen.</span><span class="sxs-lookup"><span data-stu-id="708d6-112">Please refer toohello following tooget a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="708d6-113">Extensie voor aangepaste scripts op een Linux-VM</span><span class="sxs-lookup"><span data-stu-id="708d6-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="708d6-114">Na het Hallo-sjabloon schrijft, kunt u met behulp van Azure CLI Hallo implementeren.</span><span class="sxs-lookup"><span data-stu-id="708d6-114">After authoring hello template, you can deploy it using hello Azure CLI.</span></span>

