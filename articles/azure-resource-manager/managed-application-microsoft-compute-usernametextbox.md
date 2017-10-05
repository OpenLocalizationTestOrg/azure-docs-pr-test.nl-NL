---
title: Azure beheerde toepassing UserNameTextBox UI-element | Microsoft Docs
description: Beschrijft het Microsoft.Compute.UserNameTextBox UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: c90be5a0ed3aadda81d7ec9b5388a96472f69af0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a>Microsoft.Compute.UserNameTextBox UI-element
Een tekstvak met ingebouwde validatie voor Windows en Linux-gebruikersnamen. Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).

## <a name="ui-sample"></a>Voorbeeld van de gebruikersinterface
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a>Schema
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.UserNameTextBox",
  "label": "User name",
  "defaultValue": "",
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a>Opmerkingen
- Als `constraints.required` is ingesteld op **true**, en vervolgens in het tekstvak moet een waarde kan worden gevalideerd bevatten. De standaardwaarde is **true**.
- `osPlatform`moet worden opgegeven en kan **Windows** of **Linux**.
- `constraints.regex`is een reguliere-expressiepatroon van JavaScript. Indien opgegeven, klikt u vervolgens de waarde van het tekstvak moet overeenkomen met het patroon kan worden gevalideerd. De standaardwaarde is **null**.
- `constraints.validationMessage`is een tekenreeks om weer te geven wanneer de waarde van het tekstvak, de validatie is opgegeven mislukt door `constraints.regex`. Als niet wordt opgegeven, wordt het tekstvak ingebouwde validatieberichten gebruikt. De standaardwaarde is **null**.
- Dit element heeft ingebouwde validatiefouten die is gebaseerd op de opgegeven waarde voor `osPlatform`. De ingebouwde validatie kan worden gebruikt samen met een aangepaste reguliere expressie.
Als er een waarde voor `constraints.regex` is opgegeven, worden de ingebouwde en aangepaste validaties worden geactiveerd.

## <a name="sample-output"></a>Voorbeelduitvoer
```json
"tabrezm"
```

## <a name="next-steps"></a>Volgende stappen
* Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).
* Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).
