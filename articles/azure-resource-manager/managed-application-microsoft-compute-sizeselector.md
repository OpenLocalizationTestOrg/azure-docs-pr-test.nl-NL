---
title: Azure beheerde toepassing SizeSelector UI-element | Microsoft Docs
description: Beschrijft het Microsoft.Compute.SizeSelector UI-element voor beheerde Azure-toepassingen
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: e54962f73028ada258a7faef271d66f0fbcef649
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="d5734-103">Microsoft.Compute.SizeSelector UI-element</span><span class="sxs-lookup"><span data-stu-id="d5734-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="d5734-104">Een besturingselement voor het selecteren van een grootte voor een of meer exemplaren van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d5734-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="d5734-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="d5734-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="d5734-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="d5734-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="d5734-108">Schema</span><span class="sxs-lookup"><span data-stu-id="d5734-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="d5734-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="d5734-109">Remarks</span></span>
- <span data-ttu-id="d5734-110">`recommendedSizes`moet ten minste één grootte bevatten.</span><span class="sxs-lookup"><span data-stu-id="d5734-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="d5734-111">De eerste aanbevolen grootte wordt als standaardwaarde gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d5734-111">The first recommended size is used as the default.</span></span>
- <span data-ttu-id="d5734-112">Als een aanbevolen grootte niet beschikbaar in de geselecteerde locatie is, wordt de grootte automatisch overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d5734-112">If a recommended size is not available in the selected location, the size is automatically skipped.</span></span> <span data-ttu-id="d5734-113">In plaats daarvan wordt de volgende aanbevolen grootte gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d5734-113">Instead, the next recommended size is used.</span></span>
- <span data-ttu-id="d5734-114">Elke grootte niet is opgegeven in de `constraints.allowedSizes` is verborgen, en elke grootte niet is opgegeven in `constraints.excludedSizes` wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d5734-114">Any size not specified in the `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="d5734-115">`constraints.allowedSizes`en `constraints.excludedSizes` zijn beide optioneel, maar niet gelijktijdig worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d5734-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="d5734-116">Kan de lijst met beschikbare grootten worden bepaald door het aanroepen van [lijst met beschikbare virtuele machine grootten voor een abonnement](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span><span class="sxs-lookup"><span data-stu-id="d5734-116">The list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="d5734-117">`osPlatform`moet worden opgegeven en kan **Windows** of **Linux**.</span><span class="sxs-lookup"><span data-stu-id="d5734-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="d5734-118">Wordt gebruikt om de hardwarekosten van de virtuele machines te bepalen.</span><span class="sxs-lookup"><span data-stu-id="d5734-118">It's used to determine the hardware costs of the virtual machines.</span></span>
- <span data-ttu-id="d5734-119">`imageReference`wordt weggelaten voor directe installatiekopieën, maar de opgegeven voor de installatiekopieën van derden.</span><span class="sxs-lookup"><span data-stu-id="d5734-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="d5734-120">Wordt gebruikt om de softwarekosten van de virtuele machines te bepalen.</span><span class="sxs-lookup"><span data-stu-id="d5734-120">It's used to determine the software costs of the virtual machines.</span></span>
- <span data-ttu-id="d5734-121">`count`wordt gebruikt om de juiste vermenigvuldiger voor het element.</span><span class="sxs-lookup"><span data-stu-id="d5734-121">`count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="d5734-122">Een statische waarde, zoals ondersteunt **2**, of een dynamische waarde van een ander element, zoals `[steps('step1').vmCount]`.</span><span class="sxs-lookup"><span data-stu-id="d5734-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="d5734-123">De standaardwaarde is **1**.</span><span class="sxs-lookup"><span data-stu-id="d5734-123">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="d5734-124">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="d5734-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="d5734-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d5734-125">Next steps</span></span>
* <span data-ttu-id="d5734-126">Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d5734-126">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="d5734-127">Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d5734-127">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="d5734-128">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="d5734-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
