---
title: aaaHow tootag een virtuele machine van Azure Linux | Microsoft Docs
description: Meer informatie over labels van een Azure Linux virtuele machine in Azure met Resource Manager-implementatiemodel Hallo gemaakt.
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
ms.openlocfilehash: 456b226af4495c3b446cb79c99cf9494dde9fca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="21443-103">Hoe tootag virtuele Linux-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="21443-103">How tootag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="21443-104">In dit artikel beschrijft de verschillende manieren tootag virtuele Linux-machine in Azure via Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="21443-104">This article describes different ways tootag a Linux virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="21443-105">Labels zijn de gebruiker gedefinieerde sleutel/waarde-paren die rechtstreeks op een resource of een resourcegroep kunnen worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="21443-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="21443-106">Azure biedt momenteel ondersteuning voor maximaal too15 labels per resource en resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="21443-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="21443-107">Labels van een resource kunnen worden geplaatst op Hallo moment gemaakt of bestaande resource tooan toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="21443-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="21443-108">Houd er rekening mee,-labels worden ondersteund voor resources die zijn gemaakt via Hallo Resource Manager-implementatiemodel alleen.</span><span class="sxs-lookup"><span data-stu-id="21443-108">Please note, tags are supported for resources created via hello Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="21443-109">Met Azure CLI-tagging</span><span class="sxs-lookup"><span data-stu-id="21443-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="21443-110">toobegin, moet u Hallo nieuwste [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="21443-110">toobegin, you need hello latest [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="21443-111">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="21443-111">You can also perform these steps with hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="21443-112">U kunt alle eigenschappen weergeven voor een bepaalde virtuele Machine, met inbegrip van Hallo labels, met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="21443-112">You can view all properties for a given Virtual Machine, including hello tags, using this command:</span></span>

        az vm show --resource-group MyResourceGroup --name MyTestVM

<span data-ttu-id="21443-113">een nieuwe VM-tag via hello Azure CLI tooadd, kunt u Hallo `azure vm update` opdracht samen met de parameter tag Hallo **--ingesteld**:</span><span class="sxs-lookup"><span data-stu-id="21443-113">tooadd a new VM tag through hello Azure CLI, you can use hello `azure vm update` command along with hello tag parameter **--set**:</span></span>

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

<span data-ttu-id="21443-114">tooremove tags, kunt u Hallo **--verwijderen** parameter in Hallo `azure vm update` opdracht.</span><span class="sxs-lookup"><span data-stu-id="21443-114">tooremove tags, you can use hello **--remove** parameter in hello `azure vm update` command.</span></span>

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


<span data-ttu-id="21443-115">Nu dat we labels tooour resources Azure CLI hebt toegepast en Hallo Portal, eens kijken Hallo gebruik details toosee Hallo labels in facturering Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="21443-115">Now that we have applied tags tooour resources Azure CLI and hello Portal, let’s take a look at hello usage details toosee hello tags in hello billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="21443-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="21443-116">Next steps</span></span>
* <span data-ttu-id="21443-117">Zie toolearn meer informatie over uw Azure-resources te labelen [overzicht van Azure Resource Manager] [ Azure Resource Manager Overview] en [tooorganize labels met behulp van uw Azure-Resources] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="21443-117">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="21443-118">toosee hoe labels kunt u uw gebruik van Azure-resources beheren raadpleegt [inzicht in uw Azure-factuur] [ Understanding your Azure Bill] en [inzicht in uw Microsoft Azure-brongebruik] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="21443-118">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
