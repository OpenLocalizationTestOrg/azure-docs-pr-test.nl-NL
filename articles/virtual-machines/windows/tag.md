---
title: aaaHow tootag een virtuele machine van Windows-resource in Azure | Microsoft Docs
description: Meer informatie over virtuele Windows-machine gemaakt in Azure met Resource Manager-implementatiemodel Hallo-tagging
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
ms.openlocfilehash: 160416ddc35998b3c98c6e579668a6a5eb6de6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="87607-103">Hoe tootag virtuele Windows-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="87607-103">How tootag a Windows virtual machine in Azure</span></span>
<span data-ttu-id="87607-104">In dit artikel beschrijft de verschillende manieren tootag virtuele Windows-machine in Azure via Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="87607-104">This article describes different ways tootag a Windows virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="87607-105">Labels zijn de gebruiker gedefinieerde sleutel/waarde-paren die rechtstreeks op een resource of een resourcegroep kunnen worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="87607-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="87607-106">Azure biedt momenteel ondersteuning voor maximaal too15 labels per resource en resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="87607-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="87607-107">Labels van een resource kunnen worden geplaatst op Hallo moment gemaakt of bestaande resource tooan toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="87607-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="87607-108">Houd er rekening mee dat de labels voor resources die zijn gemaakt via Hallo Resource Manager-implementatiemodel alleen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="87607-108">Please note that tags are supported for resources created via hello Resource Manager deployment model only.</span></span> <span data-ttu-id="87607-109">Als u een virtuele Linux-machine tootag wilt, Zie [hoe een virtuele Linux-machine in Azure tootag](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="87607-109">If you want tootag a Linux virtual machine, see [How tootag a Linux virtual machine in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a><span data-ttu-id="87607-110">Labels met PowerShell</span><span class="sxs-lookup"><span data-stu-id="87607-110">Tagging with PowerShell</span></span>
<span data-ttu-id="87607-111">toocreate, toevoegen en verwijderen van de labels via PowerShell, moet u eerst tooset van uw [PowerShell-omgeving met Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span><span class="sxs-lookup"><span data-stu-id="87607-111">toocreate, add, and delete tags through PowerShell, you first need tooset up your [PowerShell environment with Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span></span> <span data-ttu-id="87607-112">Nadat u Hallo-installatie hebt voltooid, kunt u labels kunt plaatsen op Compute, netwerk en opslag bronnen bij het maken of nadat het Hallo-resource is gemaakt via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87607-112">Once you have completed hello setup, you can place tags on Compute, Network, and Storage resources at creation or after hello resource is created via PowerShell.</span></span> <span data-ttu-id="87607-113">In dit artikel zal zich concentreren op weergeven/bewerken labels geplaatst op virtuele Machines.</span><span class="sxs-lookup"><span data-stu-id="87607-113">This article will concentrate on viewing/editing tags placed on Virtual Machines.</span></span>

<span data-ttu-id="87607-114">Ga eerst tooa virtuele Machine via Hallo `Get-AzureRmVM` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="87607-114">First, navigate tooa Virtual Machine through hello `Get-AzureRmVM` cmdlet.</span></span>

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

<span data-ttu-id="87607-115">Als uw virtuele Machine al labels bevat, klikt u vervolgens ziet u alle Hallo-tags van uw resources:</span><span class="sxs-lookup"><span data-stu-id="87607-115">If your Virtual Machine already contains tags, you will then see all hello tags on your resource:</span></span>

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

<span data-ttu-id="87607-116">Als u de labels tooadd via PowerShell dat wilt, kunt u Hallo `Set-AzureRmResource` opdracht.</span><span class="sxs-lookup"><span data-stu-id="87607-116">If you would like tooadd tags through PowerShell, you can use hello `Set-AzureRmResource` command.</span></span> <span data-ttu-id="87607-117">Houd er rekening mee bij het bijwerken van labels via PowerShell, tags worden bijgewerkt als geheel.</span><span class="sxs-lookup"><span data-stu-id="87607-117">Note when updating tags through PowerShell, tags are updated as a whole.</span></span> <span data-ttu-id="87607-118">Dus als u een bron van de tag tooa waarvoor al labels toevoegt, moet u tooinclude alle Hallo-labels die u wilt dat toobe op Hallo resource geplaatst.</span><span class="sxs-lookup"><span data-stu-id="87607-118">So if you are adding one tag tooa resource that already has tags, you will need tooinclude all hello tags that you want toobe placed on hello resource.</span></span> <span data-ttu-id="87607-119">Hieronder volgt een voorbeeld van hoe extra tooadd tags tooa resource via PowerShell-Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="87607-119">Below is an example of how tooadd additional tags tooa resource through PowerShell Cmdlets.</span></span>

<span data-ttu-id="87607-120">Deze eerste cmdlet worden alle Hallo labels op geplaatst *MyTestVM* toohello *$tags* variabele, met behulp van Hallo `Get-AzureRmResource` en `Tags` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="87607-120">This first cmdlet sets all of hello tags placed on *MyTestVM* toohello *$tags* variable, using hello `Get-AzureRmResource` and `Tags` property.</span></span>

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

<span data-ttu-id="87607-121">Hallo tweede opdracht geeft Hallo labels voor Hallo variabele opgegeven.</span><span class="sxs-lookup"><span data-stu-id="87607-121">hello second command displays hello tags for hello given variable.</span></span>

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

<span data-ttu-id="87607-122">Hallo derde opdracht voegt een extra tag toohello *$tags* variabele.</span><span class="sxs-lookup"><span data-stu-id="87607-122">hello third command adds an additional tag toohello *$tags* variable.</span></span> <span data-ttu-id="87607-123">Houd er rekening mee Hallo gebruik van Hallo  **+=**  tooappend Hallo nieuwe sleutel/waarde-paar toohello *$tags* lijst.</span><span class="sxs-lookup"><span data-stu-id="87607-123">Note hello use of hello **+=** tooappend hello new key/value pair toohello *$tags* list.</span></span>

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

<span data-ttu-id="87607-124">Hallo vierde opdracht worden alle Hallo codes, gedefinieerd in Hallo *$tags* variabele toohello resource opgegeven.</span><span class="sxs-lookup"><span data-stu-id="87607-124">hello fourth command sets all of hello tags defined in hello *$tags* variable toohello given resource.</span></span> <span data-ttu-id="87607-125">In dit geval is het MyTestVM.</span><span class="sxs-lookup"><span data-stu-id="87607-125">In this case, it is MyTestVM.</span></span>

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

<span data-ttu-id="87607-126">Hallo vijfde opdracht geeft alle Hallo labels op Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="87607-126">hello fifth command displays all of hello tags on hello resource.</span></span> <span data-ttu-id="87607-127">Zoals u ziet, *locatie* is nu gedefinieerd als een label met *MyLocation* Hallo-waarde.</span><span class="sxs-lookup"><span data-stu-id="87607-127">As you can see, *Location* is now defined as a tag with *MyLocation* as hello value.</span></span>

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

<span data-ttu-id="87607-128">informatie over toolearn Hallo tagging via PowerShell, Bekijk [Azure Resource Cmdlets][Azure Resource Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="87607-128">toolearn more about tagging through PowerShell, check out hello [Azure Resource Cmdlets][Azure Resource Cmdlets].</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="87607-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="87607-129">Next steps</span></span>
* <span data-ttu-id="87607-130">Zie toolearn meer informatie over uw Azure-resources te labelen [overzicht van Azure Resource Manager] [ Azure Resource Manager Overview] en [tooorganize labels met behulp van uw Azure-Resources] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="87607-130">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="87607-131">toosee hoe labels kunt u uw gebruik van Azure-resources beheren raadpleegt [inzicht in uw Azure-factuur] [ Understanding your Azure Bill] en [inzicht in uw Microsoft Azure-brongebruik] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="87607-131">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
