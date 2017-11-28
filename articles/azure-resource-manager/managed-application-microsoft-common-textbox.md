---
title: Azure Application TextBox-UI beheerd element | Microsoft Docs
description: Beschrijft het Microsoft.Common.TextBox UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: 5a0ac5b811812c8c03f7f63aae12b8699d248ebf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="03c8c-103">Microsoft.Common.TextBox UI-element</span><span class="sxs-lookup"><span data-stu-id="03c8c-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="03c8c-104">Een besturingselement dat kan worden gebruikt voor het bewerken van tekst zonder opmaak.</span><span class="sxs-lookup"><span data-stu-id="03c8c-104">A control that can be used to edit unformatted text.</span></span> <span data-ttu-id="03c8c-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="03c8c-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="03c8c-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="03c8c-106">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="03c8c-108">Schema</span><span class="sxs-lookup"><span data-stu-id="03c8c-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Halp!",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="03c8c-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="03c8c-109">Remarks</span></span>
- <span data-ttu-id="03c8c-110">Als `constraints.required` is ingesteld op **true**, en vervolgens in het tekstvak moet een waarde kan worden gevalideerd bevatten.</span><span class="sxs-lookup"><span data-stu-id="03c8c-110">If `constraints.required` is set to **true**, then the text box must contain a value to validate successfully.</span></span> <span data-ttu-id="03c8c-111">De standaardwaarde is **false**.</span><span class="sxs-lookup"><span data-stu-id="03c8c-111">The default value is **false**.</span></span>
- <span data-ttu-id="03c8c-112">`constraints.regex`is een reguliere-expressiepatroon van JavaScript.</span><span class="sxs-lookup"><span data-stu-id="03c8c-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="03c8c-113">Indien opgegeven, klikt u vervolgens de waarde van het tekstvak moet overeenkomen met het patroon kan worden gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="03c8c-113">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="03c8c-114">De standaardwaarde is **null**.</span><span class="sxs-lookup"><span data-stu-id="03c8c-114">The default value is **null**.</span></span>
- <span data-ttu-id="03c8c-115">`constraints.validationMessage`is een tekenreeks die moet worden weergegeven wanneer de waarde van het tekstvak validatie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="03c8c-115">`constraints.validationMessage` is a string to display when the text box's value fails validation.</span></span> <span data-ttu-id="03c8c-116">Als niet wordt opgegeven, wordt het tekstvak ingebouwde validatieberichten gebruikt.</span><span class="sxs-lookup"><span data-stu-id="03c8c-116">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="03c8c-117">De standaardwaarde is **null**.</span><span class="sxs-lookup"><span data-stu-id="03c8c-117">The default value is **null**.</span></span>
- <span data-ttu-id="03c8c-118">Het is mogelijk om op te geven van een waarde voor `constraints.regex` wanneer `constraints.required` is ingesteld op **false**.</span><span class="sxs-lookup"><span data-stu-id="03c8c-118">It's possible to specify a value for `constraints.regex` when `constraints.required` is set to **false**.</span></span> <span data-ttu-id="03c8c-119">In dit scenario wordt is een waarde niet vereist voor het tekstvak kan worden gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="03c8c-119">In this scenario, a value is not required for the text box to validate successfully.</span></span> <span data-ttu-id="03c8c-120">Als er een is opgegeven, moet overeenkomen met de reguliere-expressiepatroon.</span><span class="sxs-lookup"><span data-stu-id="03c8c-120">If one is specified, it must match the regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="03c8c-121">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="03c8c-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="03c8c-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="03c8c-122">Next steps</span></span>
* <span data-ttu-id="03c8c-123">Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="03c8c-123">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="03c8c-124">Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="03c8c-124">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="03c8c-125">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="03c8c-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
