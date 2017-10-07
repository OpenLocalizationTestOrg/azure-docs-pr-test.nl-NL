---
title: Beheerde toepassing CredentialsCombo UI-element aaaAzure | Microsoft Docs
description: Beschrijft Hallo Microsoft.Compute.CredentialsCombo UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: d44a3929ebb7a5ff78b72f9eaeb6e52b098e266f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a>Microsoft.Compute.CredentialsCombo UI-element
Een groep besturingselementen met ingebouwde validatie voor wachtwoorden voor Windows en Linux- en openbare SSH-sleutels. Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).

## <a name="ui-sample"></a>Voorbeeld van de gebruikersinterface
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a>Schema
Als `osPlatform` is **Windows**, en vervolgens hello volgende schema wordt gebruikt:
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": {
    "password": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

Als `osPlatform` is **Linux**, en vervolgens hello volgende schema wordt gebruikt:
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "authenticationType": "Authentication type",
    "password": "Password",
    "confirmPassword": "Confirm password",
    "sshPublicKey": "SSH public key"
  },
  "toolTip": {
    "authenticationType": "",
    "password": "",
    "sshPublicKey": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a>Opmerkingen
- `osPlatform`moet worden opgegeven en kan **Windows** of **Linux**.
- Als `constraints.required` te is ingesteld,**true**, vervolgens Hallo wachtwoord of SSH tekstvakken met openbare sleutel is toovalidate waarden moeten bevatten. de standaardwaarde Hallo is **true**.
- Als `options.hideConfirmation` te is ingesteld,**true**, en vervolgens een tweede tekstvak voor het bevestigen van het wachtwoord van gebruiker Hallo Hallo wordt verborgen. de standaardwaarde Hallo is **false**.
- Als `options.hidePassword` te is ingesteld,**true**, en vervolgens Hallo optie toouse wachtwoordverificatie wordt verborgen. Het kan worden gebruikt alleen wanneer `osPlatform` is **Linux**. De standaardwaarde is **false**.
- Aanvullende beperkingen op Hallo toegestaan wachtwoorden kunnen worden geïmplementeerd met behulp van Hallo `customPasswordRegex` eigenschap. Hallo-reeks in `customValidationMessage` wordt weergegeven wanneer u een wachtwoord aangepaste validatie is mislukt. Hallo standaardwaarde voor beide eigenschappen is **null**.

## <a name="sample-output"></a>Voorbeelduitvoer
Als `osPlatform` is **Windows**, of Hallo gebruiker een wachtwoord in plaats van een openbare SSH-sleutel opgegeven vervolgens hello volgende uitvoer wordt verwacht:

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

Als gebruiker Hallo openbare SSH-sleutel hebt opgegeven, wordt klikt u vervolgens hello volgende uitvoer verwacht.
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a>Volgende stappen
* Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).
* Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).
