---
title: Download de sjabloon voor een virtuele machine in Azure | Microsoft Docs
description: Download de templatefor een virtuele machine om te helpen bij het automatiseren van implementaties in het Resource Manager-implementatiemodel
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
ms.openlocfilehash: 9e4c0c3cf0e233447369a24b1d5fe27495abd1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="download-the-template-for-a-vm"></a><span data-ttu-id="1dbb8-103">De sjabloon voor een VM downloaden</span><span class="sxs-lookup"><span data-stu-id="1dbb8-103">Download the template for a VM</span></span>
<span data-ttu-id="1dbb8-104">Wanneer u een virtuele machine in Azure met behulp van de portal of PowerShell maakt, wordt een Resource Manager-sjabloon automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1dbb8-104">When you create a VM in Azure using the portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="1dbb8-105">Deze sjabloon kunt u snel dupliceren van een implementatie.</span><span class="sxs-lookup"><span data-stu-id="1dbb8-105">You can use this template to quickly duplicate a deployment.</span></span> <span data-ttu-id="1dbb8-106">De sjabloon bevat informatie over alle resources in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="1dbb8-106">The template contains information about all of the resources in a resource group.</span></span> <span data-ttu-id="1dbb8-107">Voor een virtuele machine, betekent dit dat de sjabloon bevat alles wat u ter ondersteuning van de virtuele machine in die resourcegroep, met inbegrip van de netwerkbronnen wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1dbb8-107">For a virtual machine, this means the template contains everything that is created in support of the VM in that resource group, including the networking resources.</span></span>

## <a name="download-the-template-using-the-portal"></a><span data-ttu-id="1dbb8-108">Download de sjabloon die via de portal</span><span class="sxs-lookup"><span data-stu-id="1dbb8-108">Download the template using the portal</span></span>
1. <span data-ttu-id="1dbb8-109">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1dbb8-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1dbb8-110">Een het hub-menu selecteren **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="1dbb8-110">One the hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="1dbb8-111">Selecteer de virtuele machine in de lijst.</span><span class="sxs-lookup"><span data-stu-id="1dbb8-111">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="1dbb8-112">Selecteer **automatiseringsscript**.</span><span class="sxs-lookup"><span data-stu-id="1dbb8-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="1dbb8-113">Selecteer **downloaden** en sla het ZIP-bestand op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="1dbb8-113">Select **Download** and save the .zip file to your local computer.</span></span>
6. <span data-ttu-id="1dbb8-114">Open het ZIP-bestand en pak de bestanden naar een map.</span><span class="sxs-lookup"><span data-stu-id="1dbb8-114">Open the .zip file and extract the files to a folder.</span></span> <span data-ttu-id="1dbb8-115">Het ZIP-bestand bevat:</span><span class="sxs-lookup"><span data-stu-id="1dbb8-115">The .zip file will contain:</span></span>
   
   * <span data-ttu-id="1dbb8-116">Deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="1dbb8-116">deploy.ps1</span></span>
   * <span data-ttu-id="1dbb8-117">Deploy.sh</span><span class="sxs-lookup"><span data-stu-id="1dbb8-117">deploy.sh</span></span> 
   * <span data-ttu-id="1dbb8-118">deployer.RB</span><span class="sxs-lookup"><span data-stu-id="1dbb8-118">deployer.rb</span></span>
   * <span data-ttu-id="1dbb8-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="1dbb8-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="1dbb8-120">parameters.JSON</span><span class="sxs-lookup"><span data-stu-id="1dbb8-120">parameters.json</span></span>
   * <span data-ttu-id="1dbb8-121">Template.JSON</span><span class="sxs-lookup"><span data-stu-id="1dbb8-121">template.json</span></span>

<span data-ttu-id="1dbb8-122">Het bestand template.json is de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="1dbb8-122">The template.json file is the template.</span></span>

## <a name="download-the-template-using-powershell"></a><span data-ttu-id="1dbb8-123">Download de sjabloon die met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="1dbb8-123">Download the template using PowerShell</span></span>
<span data-ttu-id="1dbb8-124">U kunt ook downloaden .json sjabloon bestand met de [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1dbb8-124">You can also download the .json template file using the [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="1dbb8-125">U kunt de `-path` -parameter voor de bestandsnaam en het pad opgeven voor de .json-bestand.</span><span class="sxs-lookup"><span data-stu-id="1dbb8-125">You can use the `-path` parameter to provide the filename and path for the .json file.</span></span> <span data-ttu-id="1dbb8-126">Dit voorbeeld ziet u het downloaden van de sjabloon voor de resourcegroep met de naam **myResourceGroup** naar de **C:\users\public\downloads** map op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="1dbb8-126">This example shows how to download the template for the resource group named **myResourceGroup** to the **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="1dbb8-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1dbb8-127">Next steps</span></span>
<span data-ttu-id="1dbb8-128">Zie voor meer informatie over het implementeren van resources met behulp van sjablonen, [overzicht voor Resource Manager-sjabloon](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="1dbb8-128">To learn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

