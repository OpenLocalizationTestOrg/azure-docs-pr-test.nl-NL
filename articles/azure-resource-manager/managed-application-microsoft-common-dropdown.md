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
# <a name="microsoftcommondropdown-ui-element"></a>Microsoft.Common.DropDown UI-element
Een Selectiebesturingselement met een vervolgkeuzelijst. Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).

## <a name="ui-sample"></a>Voorbeeld van de gebruikersinterface
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a>Schema
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

## <a name="remarks"></a>Opmerkingen
- Hallo-label voor `constraints.allowedValues` Hallo-tekst weergeven voor een item is en de waarde is de uitvoerwaarde Hallo van Hallo element wanneer geselecteerd.
- Indien opgegeven, Hallo standaard de waarde moet een label aanwezig is in `constraints.allowedValues`. Als niet wordt opgegeven, Hallo eerste item in `constraints.allowedValues` is geselecteerd. de standaardwaarde Hallo is **null**.
- `constraints.allowedValues`moet ten minste één item bevatten.
- Dit element ondersteunt geen Hallo `constraints.required` eigenschap. tooemulate dit gedrag toevoegen van een item met een label en de waarde van `""` (een lege tekenreeks) te`constraints.allowedValues`.

## <a name="sample-output"></a>Voorbeelduitvoer
```json
"Bar"
```

## <a name="next-steps"></a>Volgende stappen
* Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).
* Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).
