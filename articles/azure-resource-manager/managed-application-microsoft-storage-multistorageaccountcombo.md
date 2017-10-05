---
title: Azure beheerde toepassing MultiStorageAccountCombo UI-element | Microsoft Docs
description: Beschrijft het Microsoft.Storage.MultiStorageAccountCombo UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: 27843b116d949899e4eae65f342324f77ebca70b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="5419b-103">Microsoft.Storage.MultiStorageAccountCombo UI-element</span><span class="sxs-lookup"><span data-stu-id="5419b-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="5419b-104">Een groep besturingselementen voor het maken van meerdere opslagaccounts met namen die met een algemeen voorvoegsel beginnen.</span><span class="sxs-lookup"><span data-stu-id="5419b-104">A group of controls for creating multiple storage accounts, with names that start with a common prefix.</span></span> <span data-ttu-id="5419b-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="5419b-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="5419b-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="5419b-106">UI sample</span></span>
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="5419b-108">Schema</span><span class="sxs-lookup"><span data-stu-id="5419b-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="5419b-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="5419b-109">Remarks</span></span>
- <span data-ttu-id="5419b-110">De waarde voor `defaultValue.prefix` is samengevoegd met een of meer getallen voor het genereren van de volgorde van de namen van opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="5419b-110">The value for `defaultValue.prefix` is concatenated with one or more integers to generate the sequence of storage account names.</span></span> <span data-ttu-id="5419b-111">Bijvoorbeeld, als `defaultValue.prefix` is **foobar** en `count` is **2**, klikt u vervolgens opslagaccountnamen **foobar1** en **foobar2** worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="5419b-111">For example, if `defaultValue.prefix` is **foobar** and `count` is **2**, then storage account names **foobar1** and **foobar2** are generated.</span></span> <span data-ttu-id="5419b-112">Gegenereerde opslagaccountnamen worden gevalideerd voor uniekheid automatisch.</span><span class="sxs-lookup"><span data-stu-id="5419b-112">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="5419b-113">De namen van opslagaccounts zijn gegenereerd lexicographically op basis van `count`.</span><span class="sxs-lookup"><span data-stu-id="5419b-113">The storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="5419b-114">Bijvoorbeeld, als `count` 10 is, wordt de namen van opslagaccounts eindigen met gehele getallen 2 cijfers (01, 02, 03, enz.).</span><span class="sxs-lookup"><span data-stu-id="5419b-114">For example, if `count` is 10, then the storage account names end with 2-digit integers (01, 02, 03, etc.).</span></span>
- <span data-ttu-id="5419b-115">De standaardwaarde voor `defaultValue.prefix` is **null**, en voor `defaultValue.type` is **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="5419b-115">The default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="5419b-116">Een type dat niet is opgegeven in `constraints.allowedTypes` is verborgen, en een type dat niet is opgegeven in `constraints.excludedTypes` wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5419b-116">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="5419b-117">`constraints.allowedTypes`en `constraints.excludedTypes` zijn beide optioneel, maar niet gelijktijdig worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5419b-117">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="5419b-118">Naast het genereren van de namen van opslagaccounts, `count` wordt gebruikt voor het instellen van de juiste vermenigvuldiger voor het element.</span><span class="sxs-lookup"><span data-stu-id="5419b-118">In addition to generating storage account names, `count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="5419b-119">Een statische waarde, zoals ondersteunt **2**, of een dynamische waarde van een ander element, zoals `[steps('step1').storageAccountCount]`.</span><span class="sxs-lookup"><span data-stu-id="5419b-119">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="5419b-120">De standaardwaarde is **1**.</span><span class="sxs-lookup"><span data-stu-id="5419b-120">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="5419b-121">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="5419b-121">Sample output</span></span>
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="5419b-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5419b-122">Next steps</span></span>
* <span data-ttu-id="5419b-123">Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5419b-123">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="5419b-124">Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5419b-124">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="5419b-125">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="5419b-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
