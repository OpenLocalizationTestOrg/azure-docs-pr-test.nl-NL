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
- Het label voor `constraints.allowedValues` is de tekst weergeven voor een item en de waarde is de uitvoerwaarde van het element als geselecteerd.
- Indien opgegeven, de standaardwaarde moet een label aanwezig is in `constraints.allowedValues`. Als niet wordt opgegeven, het eerste item in `constraints.allowedValues` is geselecteerd. De standaardwaarde is **null**.
- `constraints.allowedValues`moet ten minste één item bevatten.
- Dit element biedt geen ondersteuning voor de `constraints.required` eigenschap. Om te emuleren, Voeg een item met een label en de waarde van `""` (lege tekenreeks) om te `constraints.allowedValues`.

## <a name="sample-output"></a>Voorbeelduitvoer
```json
"Bar"
```

## <a name="next-steps"></a>Volgende stappen
* Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).
* Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).
