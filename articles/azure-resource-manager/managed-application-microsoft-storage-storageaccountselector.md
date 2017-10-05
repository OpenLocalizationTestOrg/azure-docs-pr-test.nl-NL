---
title: Azure beheerde toepassing StorageAccountSelector UI-element | Microsoft Docs
description: Beschrijft het Microsoft.Storage.StorageAccountSelector UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: 15e69c0deb4bce64b7413b557eb69db5165bde73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="b3d7a-103">Microsoft.Storage.StorageAccountSelector UI-element</span><span class="sxs-lookup"><span data-stu-id="b3d7a-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="b3d7a-104">Een besturingselement voor het selecteren van een nieuwe of bestaande opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="b3d7a-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="b3d7a-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="b3d7a-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="b3d7a-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="b3d7a-106">UI sample</span></span>
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="b3d7a-108">Schema</span><span class="sxs-lookup"><span data-stu-id="b3d7a-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.StorageAccountSelector",
  "label": "Storage account",
  "toolTip": "",
  "defaultValue": {
    "name": "storageaccount01",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "options": {
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="b3d7a-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="b3d7a-109">Remarks</span></span>
- <span data-ttu-id="b3d7a-110">Indien opgegeven, `defaultValue.name` automatisch wordt gevalideerd voor uniekheid.</span><span class="sxs-lookup"><span data-stu-id="b3d7a-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="b3d7a-111">Als de opslagaccountnaam is niet uniek is, moet de gebruiker Geef een andere naam of kies een bestaand opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="b3d7a-111">If the storage account name is not unique, the user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="b3d7a-112">De standaardwaarde voor `defaultValue.type` is **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="b3d7a-112">The default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="b3d7a-113">Een type dat niet is opgegeven in `constraints.allowedTypes` is verborgen, en een type dat niet is opgegeven in `constraints.excludedTypes` wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b3d7a-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="b3d7a-114">`constraints.allowedTypes`en `constraints.excludedTypes` zijn beide optioneel, maar niet gelijktijdig worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b3d7a-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="b3d7a-115">Als `options.hideExisting` is **true**, de gebruiker een bestaand opslagaccount niet kiezen.</span><span class="sxs-lookup"><span data-stu-id="b3d7a-115">If `options.hideExisting` is **true**, the user can't choose an existing storage account.</span></span> <span data-ttu-id="b3d7a-116">De standaardwaarde is **false**.</span><span class="sxs-lookup"><span data-stu-id="b3d7a-116">The default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="b3d7a-117">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="b3d7a-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="b3d7a-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b3d7a-118">Next steps</span></span>
* <span data-ttu-id="b3d7a-119">Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b3d7a-119">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="b3d7a-120">Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b3d7a-120">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="b3d7a-121">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="b3d7a-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
