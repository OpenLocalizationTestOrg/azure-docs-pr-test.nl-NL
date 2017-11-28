---
title: Het label van een virtuele machine van Azure Linux | Microsoft Docs
description: Meer informatie over labels van een Azure Linux virtuele machine in Azure met behulp van het Resource Manager-implementatiemodel zijn gemaakt.
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: f643001c85e127ae39e9869ffdc689bcac232ccb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-tag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="1741c-103">Het label van een virtuele Linux-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="1741c-103">How to tag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="1741c-104">In dit artikel beschrijft de verschillende manieren voor het taggen van een virtuele Linux-machine in Azure via het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="1741c-104">This article describes different ways to tag a Linux virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="1741c-105">Labels zijn de gebruiker gedefinieerde sleutel/waarde-paren die rechtstreeks op een resource of een resourcegroep kunnen worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="1741c-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="1741c-106">Azure ondersteunt momenteel maximaal 15 tags per resource en resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="1741c-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="1741c-107">Labels kunnen worden geplaatst op een bron op het moment van maken of toegevoegd aan een bestaande resource.</span><span class="sxs-lookup"><span data-stu-id="1741c-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="1741c-108">Houd er rekening mee,-labels worden ondersteund voor bronnen met behulp van het Resource Manager-implementatiemodel alleen gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1741c-108">Please note, tags are supported for resources created via the Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="1741c-109">Met Azure CLI-tagging</span><span class="sxs-lookup"><span data-stu-id="1741c-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="1741c-110">Om te beginnen, [installeren en configureren van de Azure CLI](../../xplat-cli-azure-resource-manager.md) en zorg ervoor dat u zich in de modus Resource Manager (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="1741c-110">To begin, [install and configure the Azure CLI](../../xplat-cli-azure-resource-manager.md) and make sure you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="1741c-111">U kunt alle eigenschappen weergeven voor een bepaalde virtuele Machine, met inbegrip van de labels met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="1741c-111">You can view all properties for a given Virtual Machine, including the tags, using this command:</span></span>

        azure vm show -g MyResourceGroup -n MyTestVM

<span data-ttu-id="1741c-112">Als u wilt een nieuwe VM-code via de Azure CLI toevoegt, kunt u de `azure vm set` opdracht samen met de parameter tag **-t**:</span><span class="sxs-lookup"><span data-stu-id="1741c-112">To add a new VM tag through the Azure CLI, you can use the `azure vm set` command along with the tag parameter **-t**:</span></span>

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

<span data-ttu-id="1741c-113">Als u wilt verwijderen van alle codes, kunt u de **– T** parameter in de `azure vm set` opdracht.</span><span class="sxs-lookup"><span data-stu-id="1741c-113">To remove all tags, you can use the **–T** parameter in the `azure vm set` command.</span></span>

        azure vm set – g MyResourceGroup –n MyTestVM -T


<span data-ttu-id="1741c-114">Nu dat we labels op onze bronnen Azure CLI en de Portal hebt toegepast, gaat u nu een overzicht van de gebruiksgegevens voor een overzicht van de labels in de portal voor facturering.</span><span class="sxs-lookup"><span data-stu-id="1741c-114">Now that we have applied tags to our resources Azure CLI and the Portal, let’s take a look at the usage details to see the tags in the billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="1741c-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1741c-115">Next steps</span></span>
* <span data-ttu-id="1741c-116">Zie voor meer informatie over uw Azure-resources te labelen, [overzicht van Azure Resource Manager] [ Azure Resource Manager Overview] en [Tags gebruiken om uw Azure-Resources te organiseren][Using Tags to organize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="1741c-116">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="1741c-117">Zie hoe labels kunnen u helpen uw gebruik van Azure-resources beheren [inzicht in uw Azure-factuur] [ Understanding your Azure Bill] en [inzicht in uw Microsoft Azure-brongebruik][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="1741c-117">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
