---
title: Azure beheerde toepassing sectie UI-element | Microsoft Docs
description: Beschrijft het Microsoft.Common.Section UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: 34c0f2f88e6af5a0f822ec116e7e2334e4e29e8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonsection-ui-element"></a>Microsoft.Common.Section UI-element
Een besturingselement dat groepen van een of meer elementen onder de kop. Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).

## <a name="ui-sample"></a>Voorbeeld van de gebruikersinterface
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a>Schema
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

## <a name="remarks"></a>Opmerkingen
- `elements`moet ten minste één element bevatten en mogen alle elementtypen behalve `Microsoft.Common.Section`.
- Dit element biedt geen ondersteuning voor de `toolTip` eigenschap.

## <a name="sample-output"></a>Voorbeelduitvoer
Voor toegang tot de uitvoerwaarden van elementen in `elements`, gebruiken de [basics()](managed-application-createuidefinition-functions.md#basics) of [steps()](managed-application-createuidefinition-functions.md#steps) functies en puntnotatie:

```json
basics('section1').element1
```

Elementen van het type `Microsoft.Common.Section` hebben geen uitvoerwaarden zelf.

## <a name="next-steps"></a>Volgende stappen
* Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).
* Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).
