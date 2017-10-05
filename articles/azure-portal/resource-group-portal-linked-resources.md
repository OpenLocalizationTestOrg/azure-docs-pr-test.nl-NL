---
title: Verwante en gekoppelde resources in de tegel-galerie
description: Meer informatie over verwante en gekoppelde resources die worden weergegeven in de tegel-galerie van Azure preview portal.
services: azure-portal
documentationcenter: 
author: adamabdelhamed
manager: wpickett
editor: 
ms.assetid: dba96d29-f518-49c8-bfd2-f14cecb44cbf
ms.service: azure-portal
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2015
ms.author: adamab
ms.openlocfilehash: efa7bce26c2c4c153b083e0e34d689a11d27dd16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="related-and-linked-resources-in-the-tile-gallery"></a><span data-ttu-id="c31ac-103">Verwante en gekoppelde resources in de tegel-galerie</span><span class="sxs-lookup"><span data-stu-id="c31ac-103">Related and linked resources in the tile gallery</span></span>
<span data-ttu-id="c31ac-104">De tegel galerie kunt u tegels vinden voor een bepaalde bron- en sleep deze naar uw huidige blade.</span><span class="sxs-lookup"><span data-stu-id="c31ac-104">The tile gallery enables you to find tiles for a particular resource and drag them onto your current blade.</span></span> <span data-ttu-id="c31ac-105">Met de tegel-galerie, kunt u beheerweergaven die resources omvatten.</span><span class="sxs-lookup"><span data-stu-id="c31ac-105">Using the tile gallery, you can create management views that span resources.</span></span> <span data-ttu-id="c31ac-106">Voor een opgegeven resource bevatten de bijbehorende resources alle resources in de resourcegroep en alle resources die een koppeling naar of van de resource.</span><span class="sxs-lookup"><span data-stu-id="c31ac-106">For any specified resource, the related resources include all the resources in its resource group, and any resources that link to or from the resource.</span></span>

## <a name="linked-resources-in-resource-manager"></a><span data-ttu-id="c31ac-107">Gekoppelde resources in het Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c31ac-107">Linked resources in Resource Manager</span></span>
<span data-ttu-id="c31ac-108">Koppelen is een functie van de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c31ac-108">Linking is a feature of the Resource Manager.</span></span>  <span data-ttu-id="c31ac-109">Hiermee kunt u relaties tussen resources declareren, zelfs als ze zich niet in dezelfde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c31ac-109">It enables you to declare relationships between resources even if they do not reside in the same resource group.</span></span> <span data-ttu-id="c31ac-110">Koppelen, heeft geen invloed op de runtime van uw resources, niet van invloed op de facturering en niet van invloed op rollen gebaseerde toegang.</span><span class="sxs-lookup"><span data-stu-id="c31ac-110">Linking has no impact on the runtime of your resources, no impact on billing, and no impact on role-based access.</span></span>  <span data-ttu-id="c31ac-111">Het is gewoon een mechanisme die kunt u vertegenwoordigen relaties, zodat de hulpprogramma's als de tegel-galerie een geavanceerde beheermogelijkheden bieden kan optreden.</span><span class="sxs-lookup"><span data-stu-id="c31ac-111">It's simply a mechanism you can use to represent relationships so that tools like the tile gallery can provide a rich management experience.</span></span>  <span data-ttu-id="c31ac-112">De hulpprogramma's kunnen de koppelingen die via de koppelingen API inspecteren en bieden aangepaste relatie management ook optreedt.</span><span class="sxs-lookup"><span data-stu-id="c31ac-112">Your tools can inspect the links using the links API and provide custom relationship management experiences as well.</span></span> 

## <a name="how-do-i-link-my-resources"></a><span data-ttu-id="c31ac-113">Hoe kan ik mijn resources koppelen?</span><span class="sxs-lookup"><span data-stu-id="c31ac-113">How do I link my resources?</span></span>
<span data-ttu-id="c31ac-114">Wanneer u resources via de portal of met het implementeren van een sjabloon via Azure PowerShell of Azure CLI maakt, worden automatisch koppelingen gemaakt voor enkele afhankelijke resources.</span><span class="sxs-lookup"><span data-stu-id="c31ac-114">When you create resources through the portal or by deploying a template through Azure PowerShell or Azure CLI, links are automatically created for some dependent resources.</span></span> <span data-ttu-id="c31ac-115">U kunt ook programmatisch resources koppelen met behulp van de [gekoppelde Resources REST-API](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="c31ac-115">You can also programmatically link resources by using the [Linked Resources REST API](/rest/api/resources/resourcelinks).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c31ac-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c31ac-116">Next steps</span></span>
* <span data-ttu-id="c31ac-117">Als u een inleiding tot het schrijven van Resource Manager-sjablonen, Zie [sjablonen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c31ac-117">If you need an introduction to writing Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c31ac-118">Zie voor meer informatie over het werken met resourcegroepen gebruiken via de portal, [met behulp van de Azure-portal voor het beheren van uw Azure-resources](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c31ac-118">To understand more about working with resource groups through the portal, see [Using the Azure portal to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>

