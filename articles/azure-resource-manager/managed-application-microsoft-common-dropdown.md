---
title: aaaAzure toepassing DropDown-UI beheerd element | Microsoft Docs
description: Beschrijft Hallo Microsoft.Common.DropDown UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: 1c07a48ad66b8e8b7fd8f59561776ecb1fc6224f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommondropdown-ui-element"></a><span data-ttu-id="d914b-103">Microsoft.Common.DropDown UI-element</span><span class="sxs-lookup"><span data-stu-id="d914b-103">Microsoft.Common.DropDown UI element</span></span>
<span data-ttu-id="d914b-104">Een Selectiebesturingselement met een vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="d914b-104">A selection control with a dropdown list.</span></span> <span data-ttu-id="d914b-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="d914b-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="d914b-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="d914b-106">UI sample</span></span>
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a><span data-ttu-id="d914b-108">Schema</span><span class="sxs-lookup"><span data-stu-id="d914b-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="d914b-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="d914b-109">Remarks</span></span>
- <span data-ttu-id="d914b-110">Hallo-label voor `constraints.allowedValues` Hallo-tekst weergeven voor een item is en de waarde is de uitvoerwaarde Hallo van Hallo element wanneer geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="d914b-110">hello label for `constraints.allowedValues` is hello display text for an item, and its value is hello output value of hello element when selected.</span></span>
- <span data-ttu-id="d914b-111">Indien opgegeven, Hallo standaard de waarde moet een label aanwezig is in `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="d914b-111">If specified, hello default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="d914b-112">Als niet wordt opgegeven, Hallo eerste item in `constraints.allowedValues` is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="d914b-112">If not specified, hello first item in `constraints.allowedValues` is selected.</span></span> <span data-ttu-id="d914b-113">de standaardwaarde Hallo is **null**.</span><span class="sxs-lookup"><span data-stu-id="d914b-113">hello default value is **null**.</span></span>
- <span data-ttu-id="d914b-114">`constraints.allowedValues`moet ten minste één item bevatten.</span><span class="sxs-lookup"><span data-stu-id="d914b-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="d914b-115">Dit element ondersteunt geen Hallo `constraints.required` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="d914b-115">This element doesn't support hello `constraints.required` property.</span></span> <span data-ttu-id="d914b-116">tooemulate dit gedrag toevoegen van een item met een label en de waarde van `""` (een lege tekenreeks) te`constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="d914b-116">tooemulate this behavior, add an item with a label and value of `""` (empty string) too`constraints.allowedValues`.</span></span>

## <a name="sample-output"></a><span data-ttu-id="d914b-117">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="d914b-117">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="d914b-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d914b-118">Next steps</span></span>
* <span data-ttu-id="d914b-119">Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d914b-119">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="d914b-120">Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d914b-120">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="d914b-121">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="d914b-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
