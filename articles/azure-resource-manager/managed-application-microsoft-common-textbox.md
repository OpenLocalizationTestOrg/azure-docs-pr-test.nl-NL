---
title: Beheerde toepassing TextBox UI-element aaaAzure | Microsoft Docs
description: Beschrijft Hallo Microsoft.Common.TextBox UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: 11771cd1d689b720384df98b8d1465703068af37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="5657f-103">Microsoft.Common.TextBox UI-element</span><span class="sxs-lookup"><span data-stu-id="5657f-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="5657f-104">Een besturingselement dat gebruikt tooedit worden kan tekst zonder opmaak.</span><span class="sxs-lookup"><span data-stu-id="5657f-104">A control that can be used tooedit unformatted text.</span></span> <span data-ttu-id="5657f-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="5657f-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="5657f-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="5657f-106">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="5657f-108">Schema</span><span class="sxs-lookup"><span data-stu-id="5657f-108">Schema</span></span>
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
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="5657f-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="5657f-109">Remarks</span></span>
- <span data-ttu-id="5657f-110">Als `constraints.required` te is ingesteld,**true**, Hallo tekstvak is een waarde toovalidate moet bevatten.</span><span class="sxs-lookup"><span data-stu-id="5657f-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="5657f-111">de standaardwaarde Hallo is **false**.</span><span class="sxs-lookup"><span data-stu-id="5657f-111">hello default value is **false**.</span></span>
- <span data-ttu-id="5657f-112">`constraints.regex`is een reguliere-expressiepatroon van JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5657f-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="5657f-113">Indien opgegeven, klikt u vervolgens Hallo van het tekstvak waarde moet overeenkomen met Hallo patroon toovalidate is.</span><span class="sxs-lookup"><span data-stu-id="5657f-113">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="5657f-114">De standaardwaarde is **null**.</span><span class="sxs-lookup"><span data-stu-id="5657f-114">The default value is **null**.</span></span>
- <span data-ttu-id="5657f-115">`constraints.validationMessage`is een tekenreeks toodisplay wanneer de waarde van het Hallo-tekstvak validatie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="5657f-115">`constraints.validationMessage` is a string toodisplay when hello text box's value fails validation.</span></span> <span data-ttu-id="5657f-116">Als dat niet wordt opgegeven, wordt Hallo van het tekstvak ingebouwde validatie berichten worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5657f-116">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="5657f-117">de standaardwaarde Hallo is **null**.</span><span class="sxs-lookup"><span data-stu-id="5657f-117">hello default value is **null**.</span></span>
- <span data-ttu-id="5657f-118">De mogelijke toospecify een waarde voor `constraints.regex` wanneer `constraints.required` te is ingesteld,**false**.</span><span class="sxs-lookup"><span data-stu-id="5657f-118">It's possible toospecify a value for `constraints.regex` when `constraints.required` is set too**false**.</span></span> <span data-ttu-id="5657f-119">In dit scenario wordt is een waarde niet vereist voor Hallo tekst vak toovalidate is.</span><span class="sxs-lookup"><span data-stu-id="5657f-119">In this scenario, a value is not required for hello text box toovalidate successfully.</span></span> <span data-ttu-id="5657f-120">Als er een is opgegeven, moet deze Hallo reguliere-expressiepatroon overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="5657f-120">If one is specified, it must match hello regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="5657f-121">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="5657f-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="5657f-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5657f-122">Next steps</span></span>
* <span data-ttu-id="5657f-123">Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5657f-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="5657f-124">Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5657f-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="5657f-125">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="5657f-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
