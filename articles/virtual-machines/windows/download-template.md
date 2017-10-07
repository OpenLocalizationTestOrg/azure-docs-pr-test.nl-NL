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
# <a name="download-hello-template-for-a-vm"></a><span data-ttu-id="5a1f1-103">Hallo-sjabloon downloaden voor een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="5a1f1-103">Download hello template for a VM</span></span>
<span data-ttu-id="5a1f1-104">Wanneer u een virtuele machine in Azure maakt wordt via Hallo portal of PowerShell, een Resource Manager sjabloon automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5a1f1-104">When you create a VM in Azure using hello portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="5a1f1-105">U kunt deze sjabloon tooquickly duplicaat een implementatie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5a1f1-105">You can use this template tooquickly duplicate a deployment.</span></span> <span data-ttu-id="5a1f1-106">Hallo-sjabloon bevat informatie over alle Hallo resources in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="5a1f1-106">hello template contains information about all of hello resources in a resource group.</span></span> <span data-ttu-id="5a1f1-107">Voor een virtuele machine, betekent dit dat Hallo sjabloon bevat alles wat u ter ondersteuning van Hallo VM in die resourcegroep, met inbegrip van netwerkresources hello wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5a1f1-107">For a virtual machine, this means hello template contains everything that is created in support of hello VM in that resource group, including hello networking resources.</span></span>

## <a name="download-hello-template-using-hello-portal"></a><span data-ttu-id="5a1f1-108">Met behulp van de portal Hallo Hallo-sjabloon downloaden</span><span class="sxs-lookup"><span data-stu-id="5a1f1-108">Download hello template using hello portal</span></span>
1. <span data-ttu-id="5a1f1-109">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5a1f1-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5a1f1-110">Een Hallo hub-menu Selecteer **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="5a1f1-110">One hello hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="5a1f1-111">Selecteer Hallo virtuele machine uit de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a1f1-111">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="5a1f1-112">Selecteer **automatiseringsscript**.</span><span class="sxs-lookup"><span data-stu-id="5a1f1-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="5a1f1-113">Selecteer **downloaden** en Hallo ZIP-bestand tooyour lokale computer op te slaan.</span><span class="sxs-lookup"><span data-stu-id="5a1f1-113">Select **Download** and save hello .zip file tooyour local computer.</span></span>
6. <span data-ttu-id="5a1f1-114">Hallo ZIP-bestand openen en Hallo bestanden tooa map halen.</span><span class="sxs-lookup"><span data-stu-id="5a1f1-114">Open hello .zip file and extract hello files tooa folder.</span></span> <span data-ttu-id="5a1f1-115">Hallo ZIP-bestand bevat:</span><span class="sxs-lookup"><span data-stu-id="5a1f1-115">hello .zip file will contain:</span></span>
   
   * <span data-ttu-id="5a1f1-116">Deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="5a1f1-116">deploy.ps1</span></span>
   * <span data-ttu-id="5a1f1-117">Deploy.sh</span><span class="sxs-lookup"><span data-stu-id="5a1f1-117">deploy.sh</span></span> 
   * <span data-ttu-id="5a1f1-118">deployer.RB</span><span class="sxs-lookup"><span data-stu-id="5a1f1-118">deployer.rb</span></span>
   * <span data-ttu-id="5a1f1-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="5a1f1-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="5a1f1-120">parameters.JSON</span><span class="sxs-lookup"><span data-stu-id="5a1f1-120">parameters.json</span></span>
   * <span data-ttu-id="5a1f1-121">Template.JSON</span><span class="sxs-lookup"><span data-stu-id="5a1f1-121">template.json</span></span>

<span data-ttu-id="5a1f1-122">Hallo template.json bestand is Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="5a1f1-122">hello template.json file is hello template.</span></span>

## <a name="download-hello-template-using-powershell"></a><span data-ttu-id="5a1f1-123">Met behulp van PowerShell Hallo-sjabloon downloaden</span><span class="sxs-lookup"><span data-stu-id="5a1f1-123">Download hello template using PowerShell</span></span>
<span data-ttu-id="5a1f1-124">U kunt ook downloaden Hallo .json-sjabloonbestand met Hallo [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5a1f1-124">You can also download hello .json template file using hello [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="5a1f1-125">U kunt Hallo `-path` parameter tooprovide Hallo bestandsnaam en het pad voor Hallo .json-bestand.</span><span class="sxs-lookup"><span data-stu-id="5a1f1-125">You can use hello `-path` parameter tooprovide hello filename and path for hello .json file.</span></span> <span data-ttu-id="5a1f1-126">Dit voorbeeld ziet u hoe de naam van toodownload Hallo sjabloon voor de resourcegroep Hallo **myResourceGroup** toohello **C:\users\public\downloads** map op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="5a1f1-126">This example shows how toodownload hello template for hello resource group named **myResourceGroup** toohello **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="5a1f1-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5a1f1-127">Next steps</span></span>
<span data-ttu-id="5a1f1-128">Zie toolearn meer informatie over het implementeren van resources met behulp van sjablonen [overzicht voor Resource Manager-sjabloon](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="5a1f1-128">toolearn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

