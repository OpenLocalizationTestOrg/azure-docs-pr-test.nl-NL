---
title: Beheerde toepassing sectie UI-element aaaAzure | Microsoft Docs
description: Beschrijft Hallo Microsoft.Common.Section UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: d20b365b12fab66177e1a12db2ebbeefe507212e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonsection-ui-element"></a><span data-ttu-id="58f32-103">Microsoft.Common.Section UI-element</span><span class="sxs-lookup"><span data-stu-id="58f32-103">Microsoft.Common.Section UI element</span></span>
<span data-ttu-id="58f32-104">Een besturingselement dat groepen van een of meer elementen onder de kop.</span><span class="sxs-lookup"><span data-stu-id="58f32-104">A control that groups one or more elements under a heading.</span></span> <span data-ttu-id="58f32-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="58f32-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="58f32-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="58f32-106">UI sample</span></span>
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a><span data-ttu-id="58f32-108">Schema</span><span class="sxs-lookup"><span data-stu-id="58f32-108">Schema</span></span>
```json
{
  "name": "section1",
  "type": "Microsoft.Common.Section",
  "label": "Some section",
  "elements": [
    {
      "name": "element1",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 1"
    },
    {
      "name": "element2",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 2"
    }
  ],
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="58f32-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="58f32-109">Remarks</span></span>
- <span data-ttu-id="58f32-110">`elements`moet ten minste één element bevatten en mogen alle elementtypen behalve `Microsoft.Common.Section`.</span><span class="sxs-lookup"><span data-stu-id="58f32-110">`elements` must contain at least one element, and can contain all element types except `Microsoft.Common.Section`.</span></span>
- <span data-ttu-id="58f32-111">Dit element ondersteunt geen Hallo `toolTip` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="58f32-111">This element doesn't support hello `toolTip` property.</span></span>

## <a name="sample-output"></a><span data-ttu-id="58f32-112">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="58f32-112">Sample output</span></span>
<span data-ttu-id="58f32-113">Hallo tooaccess waarden van elementen in de uitvoer `elements`, gebruik Hallo [basics()](managed-application-createuidefinition-functions.md#basics) of [steps()](managed-application-createuidefinition-functions.md#steps) functies en puntnotatie:</span><span class="sxs-lookup"><span data-stu-id="58f32-113">tooaccess hello output values of elements in `elements`, use hello [basics()](managed-application-createuidefinition-functions.md#basics) or [steps()](managed-application-createuidefinition-functions.md#steps) functions and dot notation:</span></span>

```json
basics('section1').element1
```

<span data-ttu-id="58f32-114">Elementen van het type `Microsoft.Common.Section` hebben geen uitvoerwaarden zelf.</span><span class="sxs-lookup"><span data-stu-id="58f32-114">Elements of type `Microsoft.Common.Section` have no output values themselves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58f32-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="58f32-115">Next steps</span></span>
* <span data-ttu-id="58f32-116">Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="58f32-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="58f32-117">Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="58f32-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="58f32-118">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="58f32-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
