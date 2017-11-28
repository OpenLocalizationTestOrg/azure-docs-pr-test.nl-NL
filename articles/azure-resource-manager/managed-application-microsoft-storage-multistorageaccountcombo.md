---
title: Beheerde toepassing MultiStorageAccountCombo UI-element aaaAzure | Microsoft Docs
description: Beschrijft Hallo Microsoft.Storage.MultiStorageAccountCombo UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: 765be145b61c3dbf0a035a7a00aa18eee464a3eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="d7afa-103">Microsoft.Storage.MultiStorageAccountCombo UI-element</span><span class="sxs-lookup"><span data-stu-id="d7afa-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="d7afa-104">Een groep besturingselementen voor het maken van meerdere opslagaccounts met namen die met een algemeen voorvoegsel beginnen.</span><span class="sxs-lookup"><span data-stu-id="d7afa-104">A group of controls for creating multiple storage accounts, with names that start with a common prefix.</span></span> <span data-ttu-id="d7afa-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="d7afa-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="d7afa-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="d7afa-106">UI sample</span></span>
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="d7afa-108">Schema</span><span class="sxs-lookup"><span data-stu-id="d7afa-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="d7afa-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="d7afa-109">Remarks</span></span>
- <span data-ttu-id="d7afa-110">waarde voor Hallo `defaultValue.prefix` is samengevoegd met een of meer getallen toogenerate Hallo volgorde van de namen van opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="d7afa-110">hello value for `defaultValue.prefix` is concatenated with one or more integers toogenerate hello sequence of storage account names.</span></span> <span data-ttu-id="d7afa-111">Bijvoorbeeld, als `defaultValue.prefix` is **foobar** en `count` is **2**, klikt u vervolgens opslagaccountnamen **foobar1** en **foobar2** worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d7afa-111">For example, if `defaultValue.prefix` is **foobar** and `count` is **2**, then storage account names **foobar1** and **foobar2** are generated.</span></span> <span data-ttu-id="d7afa-112">Gegenereerde opslagaccountnamen worden gevalideerd voor uniekheid automatisch.</span><span class="sxs-lookup"><span data-stu-id="d7afa-112">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="d7afa-113">Hallo opslagaccountnamen worden gegenereerd lexicographically op basis van `count`.</span><span class="sxs-lookup"><span data-stu-id="d7afa-113">hello storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="d7afa-114">Bijvoorbeeld, als `count` 10, wordt de namen van opslagaccounts Hallo eindigen met gehele getallen 2 cijfers (01, 02, 03, enz.).</span><span class="sxs-lookup"><span data-stu-id="d7afa-114">For example, if `count` is 10, then hello storage account names end with 2-digit integers (01, 02, 03, etc.).</span></span>
- <span data-ttu-id="d7afa-115">de standaardwaarde voor Hallo `defaultValue.prefix` is **null**, en voor `defaultValue.type` is **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="d7afa-115">hello default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="d7afa-116">Een type dat niet is opgegeven in `constraints.allowedTypes` is verborgen, en een type dat niet is opgegeven in `constraints.excludedTypes` wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d7afa-116">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="d7afa-117">`constraints.allowedTypes`en `constraints.excludedTypes` zijn beide optioneel, maar niet gelijktijdig worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d7afa-117">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="d7afa-118">In aanvulling toogenerating namen van opslagaccounts, `count` gebruikte tooset is de juiste vermenigvuldiger voor Hallo-element.</span><span class="sxs-lookup"><span data-stu-id="d7afa-118">In addition toogenerating storage account names, `count` is used tooset the appropriate multiplier for hello element.</span></span> <span data-ttu-id="d7afa-119">Een statische waarde, zoals ondersteunt **2**, of een dynamische waarde van een ander element, zoals `[steps('step1').storageAccountCount]`.</span><span class="sxs-lookup"><span data-stu-id="d7afa-119">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="d7afa-120">de standaardwaarde Hallo is **1**.</span><span class="sxs-lookup"><span data-stu-id="d7afa-120">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="d7afa-121">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="d7afa-121">Sample output</span></span>
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="d7afa-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d7afa-122">Next steps</span></span>
* <span data-ttu-id="d7afa-123">Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d7afa-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="d7afa-124">Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d7afa-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="d7afa-125">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="d7afa-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
