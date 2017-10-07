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
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a><span data-ttu-id="169a9-103">Azure Resource Manager-sjablonen met Windows VM-extensies</span><span class="sxs-lookup"><span data-stu-id="169a9-103">Authoring Azure Resource Manager templates with Windows VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="169a9-104">Voer vanuit Azure PowerShell hello Azure PowerShell-cmdlet te volgen:</span><span class="sxs-lookup"><span data-stu-id="169a9-104">From Azure PowerShell, run hello following Azure PowerShell cmdlet:</span></span>

      Get-AzureVMAvailableExtension


<span data-ttu-id="169a9-105">Deze cmdlet retourneert Hallo uitgeversnaam, naam en versie als volgt:</span><span class="sxs-lookup"><span data-stu-id="169a9-105">This cmdlet returns hello publisher name, extension name, and version as follows:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="169a9-106">Deze drie eigenschappen toewijzen te 'publisher', 'type' en 'typeHandlerVersion' respectievelijk in Hallo hierboven sjabloon codefragment.</span><span class="sxs-lookup"><span data-stu-id="169a9-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="169a9-107">Het is altijd aanbevolen toouse Hallo nieuwste extensie versie tooget Hallo meest bijgewerkt functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="169a9-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="169a9-108">Hallo-schema voor Hallo extensie configuratieparameters identificeren</span><span class="sxs-lookup"><span data-stu-id="169a9-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="169a9-109">Hallo volgende stap bij het ontwerpen van een sjabloon voor de uitbreiding wordt tooidentify Hallo-indeling voor het ontwikkelen van parameters voor de configuratie.</span><span class="sxs-lookup"><span data-stu-id="169a9-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="169a9-110">Elke uitbreiding ondersteunt een eigen set parameters.</span><span class="sxs-lookup"><span data-stu-id="169a9-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="169a9-111">Zie toolook op voorbeelden van configuraties voor Windows-uitbreidingen [voorbeelden van Windows-uitbreidingen](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="169a9-111">toolook at sample configurations for Windows extensions, see [Windows extensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="169a9-112">Raadpleeg toohello tooget een volledig volledige sjabloon met VM-extensies te volgen.</span><span class="sxs-lookup"><span data-stu-id="169a9-112">Please refer toohello following tooget a fully complete template with VM extensions.</span></span>

[<span data-ttu-id="169a9-113">Extensie voor aangepaste scripts op een Windows VM</span><span class="sxs-lookup"><span data-stu-id="169a9-113">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

<span data-ttu-id="169a9-114">Na het Hallo-sjabloon schrijft, kunt u met behulp van Azure PowerShell implementeren.</span><span class="sxs-lookup"><span data-stu-id="169a9-114">After authoring hello template, you can deploy it using Azure PowerShell.</span></span>

