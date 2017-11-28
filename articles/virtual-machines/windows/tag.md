---
title: Het label van een virtuele machine van Windows-resource in Azure | Microsoft Docs
description: Meer informatie over virtuele Windows-machine gemaakt in Azure met het implementatiemodel van Resource Manager-tagging
services: virtual-machines-windows
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 5f00c4265cea3db02dbb09a7f81be636a3fdd3d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-tag-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="3243b-103">Het label van een virtuele Windows-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="3243b-103">How to tag a Windows virtual machine in Azure</span></span>
<span data-ttu-id="3243b-104">In dit artikel beschrijft de verschillende manieren voor het taggen van een virtuele Windows-machine in Azure via het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="3243b-104">This article describes different ways to tag a Windows virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="3243b-105">Labels zijn de gebruiker gedefinieerde sleutel/waarde-paren die rechtstreeks op een resource of een resourcegroep kunnen worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="3243b-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="3243b-106">Azure ondersteunt momenteel maximaal 15 tags per resource en resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="3243b-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="3243b-107">Labels kunnen worden geplaatst op een bron op het moment van maken of toegevoegd aan een bestaande resource.</span><span class="sxs-lookup"><span data-stu-id="3243b-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="3243b-108">Houd er rekening mee dat de labels voor resources die zijn gemaakt via het Resource Manager-implementatiemodel alleen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="3243b-108">Please note that tags are supported for resources created via the Resource Manager deployment model only.</span></span> <span data-ttu-id="3243b-109">Als u wilt voor het taggen van een virtuele Linux-machine, Zie [hoe het labelen van een virtuele Linux-machine in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3243b-109">If you want to tag a Linux virtual machine, see [How to tag a Linux virtual machine in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a><span data-ttu-id="3243b-110">Labels met PowerShell</span><span class="sxs-lookup"><span data-stu-id="3243b-110">Tagging with PowerShell</span></span>
<span data-ttu-id="3243b-111">Als u wilt maken, toevoegen en verwijderen van de labels via PowerShell, moet u eerst voor het instellen van uw [PowerShell-omgeving met Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span><span class="sxs-lookup"><span data-stu-id="3243b-111">To create, add, and delete tags through PowerShell, you first need to set up your [PowerShell environment with Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span></span> <span data-ttu-id="3243b-112">Nadat u de installatie hebt voltooid, kunt u labels kunt plaatsen op Compute, netwerk en opslag bronnen bij het maken of nadat de resource is gemaakt via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3243b-112">Once you have completed the setup, you can place tags on Compute, Network, and Storage resources at creation or after the resource is created via PowerShell.</span></span> <span data-ttu-id="3243b-113">In dit artikel zal zich concentreren op weergeven/bewerken labels geplaatst op virtuele Machines.</span><span class="sxs-lookup"><span data-stu-id="3243b-113">This article will concentrate on viewing/editing tags placed on Virtual Machines.</span></span>

<span data-ttu-id="3243b-114">Eerst, gaat u naar een virtuele Machine via de `Get-AzureRmVM` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3243b-114">First, navigate to a Virtual Machine through the `Get-AzureRmVM` cmdlet.</span></span>

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

<span data-ttu-id="3243b-115">Als uw virtuele Machine al labels bevat, klikt u vervolgens ziet u de labels van uw resources:</span><span class="sxs-lookup"><span data-stu-id="3243b-115">If your Virtual Machine already contains tags, you will then see all the tags on your resource:</span></span>

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

<span data-ttu-id="3243b-116">Als u toevoegen labels via PowerShell wilt, kunt u de `Set-AzureRmResource` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3243b-116">If you would like to add tags through PowerShell, you can use the `Set-AzureRmResource` command.</span></span> <span data-ttu-id="3243b-117">Houd er rekening mee bij het bijwerken van labels via PowerShell, tags worden bijgewerkt als geheel.</span><span class="sxs-lookup"><span data-stu-id="3243b-117">Note when updating tags through PowerShell, tags are updated as a whole.</span></span> <span data-ttu-id="3243b-118">Dus als u één label aan een resource die al labels toevoegt is, moet u om op te nemen van de labels die u wilt worden geplaatst op de bron.</span><span class="sxs-lookup"><span data-stu-id="3243b-118">So if you are adding one tag to a resource that already has tags, you will need to include all the tags that you want to be placed on the resource.</span></span> <span data-ttu-id="3243b-119">Hieronder volgt een voorbeeld van andere labels toevoegen aan een resource via PowerShell-Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="3243b-119">Below is an example of how to add additional tags to a resource through PowerShell Cmdlets.</span></span>

<span data-ttu-id="3243b-120">Deze eerste cmdlet stelt alle labels op geplaatst *MyTestVM* naar de *$tags* variabele, met behulp van de `Get-AzureRmResource` en `Tags` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="3243b-120">This first cmdlet sets all of the tags placed on *MyTestVM* to the *$tags* variable, using the `Get-AzureRmResource` and `Tags` property.</span></span>

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

<span data-ttu-id="3243b-121">De tweede opdracht geeft de labels voor de opgegeven variabele.</span><span class="sxs-lookup"><span data-stu-id="3243b-121">The second command displays the tags for the given variable.</span></span>

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

<span data-ttu-id="3243b-122">De derde opdracht voegt een extra tag voor de *$tags* variabele.</span><span class="sxs-lookup"><span data-stu-id="3243b-122">The third command adds an additional tag to the *$tags* variable.</span></span> <span data-ttu-id="3243b-123">Let op het gebruik van de  **+=**  toe te voegen van de nieuwe sleutel-waardepaar voor de *$tags* lijst.</span><span class="sxs-lookup"><span data-stu-id="3243b-123">Note the use of the **+=** to append the new key/value pair to the *$tags* list.</span></span>

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

<span data-ttu-id="3243b-124">De vierde opdracht stelt alle labels gedefinieerd in de *$tags* variabele met de opgegeven bron.</span><span class="sxs-lookup"><span data-stu-id="3243b-124">The fourth command sets all of the tags defined in the *$tags* variable to the given resource.</span></span> <span data-ttu-id="3243b-125">In dit geval is het MyTestVM.</span><span class="sxs-lookup"><span data-stu-id="3243b-125">In this case, it is MyTestVM.</span></span>

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

<span data-ttu-id="3243b-126">De vijfde opdracht geeft alle labels op de bron.</span><span class="sxs-lookup"><span data-stu-id="3243b-126">The fifth command displays all of the tags on the resource.</span></span> <span data-ttu-id="3243b-127">Zoals u ziet, *locatie* is nu gedefinieerd als een label met *MyLocation* als de waarde.</span><span class="sxs-lookup"><span data-stu-id="3243b-127">As you can see, *Location* is now defined as a tag with *MyLocation* as the value.</span></span>

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

<span data-ttu-id="3243b-128">Bekijk voor meer informatie over labels via PowerShell, de [Azure Resource Cmdlets][Azure Resource Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="3243b-128">To learn more about tagging through PowerShell, check out the [Azure Resource Cmdlets][Azure Resource Cmdlets].</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="3243b-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3243b-129">Next steps</span></span>
* <span data-ttu-id="3243b-130">Zie voor meer informatie over uw Azure-resources te labelen, [overzicht van Azure Resource Manager] [ Azure Resource Manager Overview] en [Tags gebruiken om uw Azure-Resources te organiseren][Using Tags to organize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="3243b-130">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="3243b-131">Zie hoe labels kunnen u helpen uw gebruik van Azure-resources beheren [inzicht in uw Azure-factuur] [ Understanding your Azure Bill] en [inzicht in uw Microsoft Azure-brongebruik][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="3243b-131">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
