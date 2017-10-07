---
title: Beheerde toepassing StorageAccountSelector UI-element aaaAzure | Microsoft Docs
description: Beschrijft Hallo Microsoft.Storage.StorageAccountSelector UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: a2c9545feed4c4afb3c64b30b42c94d5382a108d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="eac42-103">Microsoft.Storage.StorageAccountSelector UI-element</span><span class="sxs-lookup"><span data-stu-id="eac42-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="eac42-104">Een besturingselement voor het selecteren van een nieuwe of bestaande opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="eac42-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="eac42-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="eac42-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="eac42-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="eac42-106">UI sample</span></span>
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="eac42-108">Schema</span><span class="sxs-lookup"><span data-stu-id="eac42-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="eac42-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="eac42-109">Remarks</span></span>
- <span data-ttu-id="eac42-110">Indien opgegeven, `defaultValue.name` automatisch wordt gevalideerd voor uniekheid.</span><span class="sxs-lookup"><span data-stu-id="eac42-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="eac42-111">Als Hallo opslagaccountnaam niet uniek is, moet de Hallo gebruiker Geef een andere naam of kies een bestaand opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="eac42-111">If hello storage account name is not unique, hello user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="eac42-112">de standaardwaarde voor Hallo `defaultValue.type` is **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="eac42-112">hello default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="eac42-113">Een type dat niet is opgegeven in `constraints.allowedTypes` is verborgen, en een type dat niet is opgegeven in `constraints.excludedTypes` wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="eac42-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="eac42-114">`constraints.allowedTypes`en `constraints.excludedTypes` zijn beide optioneel, maar niet gelijktijdig worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="eac42-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="eac42-115">Als `options.hideExisting` is **true**, Hallo gebruiker een bestaand opslagaccount niet kiezen.</span><span class="sxs-lookup"><span data-stu-id="eac42-115">If `options.hideExisting` is **true**, hello user can't choose an existing storage account.</span></span> <span data-ttu-id="eac42-116">de standaardwaarde Hallo is **false**.</span><span class="sxs-lookup"><span data-stu-id="eac42-116">hello default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="eac42-117">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="eac42-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="eac42-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eac42-118">Next steps</span></span>
* <span data-ttu-id="eac42-119">Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eac42-119">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="eac42-120">Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eac42-120">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="eac42-121">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="eac42-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
