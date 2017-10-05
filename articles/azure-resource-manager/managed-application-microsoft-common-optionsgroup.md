---
title: Azure beheerde toepassing OptionsGroup UI-element | Microsoft Docs
description: Beschrijft het Microsoft.Common.OptionsGroup UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: 6e147ed28c8248f7f17cb36fd7ae13468141dced
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="7514c-103">Microsoft.Common.OptionsGroup UI-element</span><span class="sxs-lookup"><span data-stu-id="7514c-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="7514c-104">Een Selectiebesturingselement met een rij van de beschikbare opties.</span><span class="sxs-lookup"><span data-stu-id="7514c-104">A selection control with a row of available options.</span></span> <span data-ttu-id="7514c-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="7514c-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="7514c-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="7514c-106">UI sample</span></span>
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="7514c-108">Schema</span><span class="sxs-lookup"><span data-stu-id="7514c-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="7514c-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="7514c-109">Remarks</span></span>
- <span data-ttu-id="7514c-110">Het label voor `constraints.allowedValues` is de tekst weergeven voor een item en de waarde is de uitvoerwaarde van het element als geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="7514c-110">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span></span>
- <span data-ttu-id="7514c-111">Indien opgegeven, de standaardwaarde moet een label aanwezig is in `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="7514c-111">If specified, the default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="7514c-112">Als niet wordt opgegeven, het eerste item in `constraints.allowedValues` is standaard geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="7514c-112">If not specified, the first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="7514c-113">De standaardwaarde is **null**.</span><span class="sxs-lookup"><span data-stu-id="7514c-113">The default value is **null**.</span></span>
- <span data-ttu-id="7514c-114">`constraints.allowedValues`moet ten minste één item bevatten.</span><span class="sxs-lookup"><span data-stu-id="7514c-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="7514c-115">Dit element biedt geen ondersteuning voor de `constraints.required` eigenschap; een item moet worden geselecteerd om te worden gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="7514c-115">This element doesn't support the `constraints.required` property; an item must be selected to validate successfully.</span></span>

## <a name="sample-output"></a><span data-ttu-id="7514c-116">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="7514c-116">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="7514c-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7514c-117">Next steps</span></span>
* <span data-ttu-id="7514c-118">Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7514c-118">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="7514c-119">Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7514c-119">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="7514c-120">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="7514c-120">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
