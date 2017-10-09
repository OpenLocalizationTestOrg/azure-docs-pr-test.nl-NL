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
# <a name="microsoftcommontextbox-ui-element"></a>Microsoft.Common.TextBox UI-element
Een besturingselement dat gebruikt tooedit worden kan tekst zonder opmaak. Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).

## <a name="ui-sample"></a>Voorbeeld van de gebruikersinterface
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a>Schema
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

## <a name="remarks"></a>Opmerkingen
- Als `constraints.required` te is ingesteld,**true**, Hallo tekstvak is een waarde toovalidate moet bevatten. de standaardwaarde Hallo is **false**.
- `constraints.regex`is een reguliere-expressiepatroon van JavaScript. Indien opgegeven, klikt u vervolgens Hallo van het tekstvak waarde moet overeenkomen met Hallo patroon toovalidate is. De standaardwaarde is **null**.
- `constraints.validationMessage`is een tekenreeks toodisplay wanneer de waarde van het Hallo-tekstvak validatie is mislukt. Als dat niet wordt opgegeven, wordt Hallo van het tekstvak ingebouwde validatie berichten worden gebruikt. de standaardwaarde Hallo is **null**.
- De mogelijke toospecify een waarde voor `constraints.regex` wanneer `constraints.required` te is ingesteld,**false**. In dit scenario wordt is een waarde niet vereist voor Hallo tekst vak toovalidate is. Als er een is opgegeven, moet deze Hallo reguliere-expressiepatroon overeenkomen.

## <a name="sample-output"></a>Voorbeelduitvoer

```json
"foobar"
```

## <a name="next-steps"></a>Volgende stappen
* Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).
* Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).
