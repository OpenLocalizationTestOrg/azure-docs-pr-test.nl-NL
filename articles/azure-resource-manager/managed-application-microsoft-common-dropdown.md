---
title: Azure Application DropDown-UI beheerd element | Microsoft Docs
description: Beschrijft het Microsoft.Common.DropDown UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: a769e14efbae928b811fa1f1b1c2d4fba3c7692b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommondropdown-ui-element"></a><span data-ttu-id="6806a-103">Microsoft.Common.DropDown UI-element</span><span class="sxs-lookup"><span data-stu-id="6806a-103">Microsoft.Common.DropDown UI element</span></span>
<span data-ttu-id="6806a-104">Een Selectiebesturingselement met een vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="6806a-104">A selection control with a dropdown list.</span></span> <span data-ttu-id="6806a-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="6806a-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="6806a-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="6806a-106">UI sample</span></span>
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a><span data-ttu-id="6806a-108">Schema</span><span class="sxs-lookup"><span data-stu-id="6806a-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.DropDown",
  "label": "Some drop down",
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

## <a name="remarks"></a><span data-ttu-id="6806a-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="6806a-109">Remarks</span></span>
- <span data-ttu-id="6806a-110">Het label voor `constraints.allowedValues` is de tekst weergeven voor een item en de waarde is de uitvoerwaarde van het element als geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="6806a-110">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span></span>
- <span data-ttu-id="6806a-111">Indien opgegeven, de standaardwaarde moet een label aanwezig is in `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="6806a-111">If specified, the default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="6806a-112">Als niet wordt opgegeven, het eerste item in `constraints.allowedValues` is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="6806a-112">If not specified, the first item in `constraints.allowedValues` is selected.</span></span> <span data-ttu-id="6806a-113">De standaardwaarde is **null**.</span><span class="sxs-lookup"><span data-stu-id="6806a-113">The default value is **null**.</span></span>
- <span data-ttu-id="6806a-114">`constraints.allowedValues`moet ten minste één item bevatten.</span><span class="sxs-lookup"><span data-stu-id="6806a-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="6806a-115">Dit element biedt geen ondersteuning voor de `constraints.required` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="6806a-115">This element doesn't support the `constraints.required` property.</span></span> <span data-ttu-id="6806a-116">Om te emuleren, Voeg een item met een label en de waarde van `""` (lege tekenreeks) om te `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="6806a-116">To emulate this behavior, add an item with a label and value of `""` (empty string) to `constraints.allowedValues`.</span></span>

## <a name="sample-output"></a><span data-ttu-id="6806a-117">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="6806a-117">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="6806a-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6806a-118">Next steps</span></span>
* <span data-ttu-id="6806a-119">Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6806a-119">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="6806a-120">Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6806a-120">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="6806a-121">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="6806a-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
