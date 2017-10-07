---
title: Beheerde toepassing OptionsGroup UI-element aaaAzure | Microsoft Docs
description: Beschrijft Hallo Microsoft.Common.OptionsGroup UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: e222468009c8db567bdde9f42836a48fb791da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="87d8b-103">Microsoft.Common.OptionsGroup UI-element</span><span class="sxs-lookup"><span data-stu-id="87d8b-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="87d8b-104">Een Selectiebesturingselement met een rij van de beschikbare opties.</span><span class="sxs-lookup"><span data-stu-id="87d8b-104">A selection control with a row of available options.</span></span> <span data-ttu-id="87d8b-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="87d8b-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="87d8b-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="87d8b-106">UI sample</span></span>
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="87d8b-108">Schema</span><span class="sxs-lookup"><span data-stu-id="87d8b-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.OptionsGroup",
  "label": "Some options group",
  "defaultValue": "Foo",
  "toolTip": "",
  "constraints": {
    "allowedValues": [
      {
        "label": "Foo",
        "value": "Bar"
      },
      {
        "label": "Baz",
        "value": "Qux"
      }
    ]
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="87d8b-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="87d8b-109">Remarks</span></span>
- <span data-ttu-id="87d8b-110">Hallo-label voor `constraints.allowedValues` Hallo-tekst weergeven voor een item is en de waarde is de uitvoerwaarde Hallo van Hallo element wanneer geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="87d8b-110">hello label for `constraints.allowedValues` is hello display text for an item, and its value is hello output value of hello element when selected.</span></span>
- <span data-ttu-id="87d8b-111">Indien opgegeven, Hallo standaard de waarde moet een label aanwezig is in `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="87d8b-111">If specified, hello default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="87d8b-112">Als niet wordt opgegeven, Hallo eerste item in `constraints.allowedValues` is standaard geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="87d8b-112">If not specified, hello first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="87d8b-113">de standaardwaarde Hallo is **null**.</span><span class="sxs-lookup"><span data-stu-id="87d8b-113">hello default value is **null**.</span></span>
- <span data-ttu-id="87d8b-114">`constraints.allowedValues`moet ten minste één item bevatten.</span><span class="sxs-lookup"><span data-stu-id="87d8b-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="87d8b-115">Dit element ondersteunt geen Hallo `constraints.required` eigenschap; een item moet geselecteerde toovalidate is.</span><span class="sxs-lookup"><span data-stu-id="87d8b-115">This element doesn't support hello `constraints.required` property; an item must be selected toovalidate successfully.</span></span>

## <a name="sample-output"></a><span data-ttu-id="87d8b-116">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="87d8b-116">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="87d8b-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="87d8b-117">Next steps</span></span>
* <span data-ttu-id="87d8b-118">Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="87d8b-118">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="87d8b-119">Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="87d8b-119">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="87d8b-120">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="87d8b-120">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
