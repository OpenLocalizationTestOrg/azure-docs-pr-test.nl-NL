---
title: Azure beheerde toepassing CredentialsCombo UI-element | Microsoft Docs
description: Beschrijft het Microsoft.Compute.CredentialsCombo UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: 254f383ee6f7cb9f7051fa135d85319a22c3c369
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="79ddb-103">Microsoft.Compute.CredentialsCombo UI-element</span><span class="sxs-lookup"><span data-stu-id="79ddb-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="79ddb-104">Een groep besturingselementen met ingebouwde validatie voor wachtwoorden voor Windows en Linux- en openbare SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="79ddb-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span> <span data-ttu-id="79ddb-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="79ddb-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="79ddb-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="79ddb-106">UI sample</span></span>
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a><span data-ttu-id="79ddb-108">Schema</span><span class="sxs-lookup"><span data-stu-id="79ddb-108">Schema</span></span>
<span data-ttu-id="79ddb-109">Als `osPlatform` is **Windows**, wordt het volgende schema gebruikt:</span><span class="sxs-lookup"><span data-stu-id="79ddb-109">If `osPlatform` is **Windows**, then the following schema is used:</span></span>
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
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

<span data-ttu-id="79ddb-110">Als `osPlatform` is **Linux**, wordt het volgende schema gebruikt:</span><span class="sxs-lookup"><span data-stu-id="79ddb-110">If `osPlatform` is **Linux**, then the following schema is used:</span></span>
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
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="79ddb-111">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="79ddb-111">Remarks</span></span>
- <span data-ttu-id="79ddb-112">`osPlatform`moet worden opgegeven en kan **Windows** of **Linux**.</span><span class="sxs-lookup"><span data-stu-id="79ddb-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="79ddb-113">Als `constraints.required` is ingesteld op **true**, en vervolgens het wachtwoord of SSH tekstvakken met openbare sleutels moeten bevatten waarden kan worden gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="79ddb-113">If `constraints.required` is set to **true**, then the password or SSH public key text boxes must contain values to validate successfully.</span></span> <span data-ttu-id="79ddb-114">De standaardwaarde is **true**.</span><span class="sxs-lookup"><span data-stu-id="79ddb-114">The default value is **true**.</span></span>
- <span data-ttu-id="79ddb-115">Als `options.hideConfirmation` is ingesteld op **true**, en vervolgens het tweede tekstvak voor het bevestigen van het wachtwoord van de gebruiker wordt verborgen.</span><span class="sxs-lookup"><span data-stu-id="79ddb-115">If `options.hideConfirmation` is set to **true**, then the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="79ddb-116">De standaardwaarde is **false**.</span><span class="sxs-lookup"><span data-stu-id="79ddb-116">The default value is **false**.</span></span>
- <span data-ttu-id="79ddb-117">Als `options.hidePassword` is ingesteld op **true**, en vervolgens de optie wachtwoordverificatie te gebruiken, wordt verborgen.</span><span class="sxs-lookup"><span data-stu-id="79ddb-117">If `options.hidePassword` is set to **true**, then the option to use password authentication is hidden.</span></span> <span data-ttu-id="79ddb-118">Het kan worden gebruikt alleen wanneer `osPlatform` is **Linux**.</span><span class="sxs-lookup"><span data-stu-id="79ddb-118">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="79ddb-119">De standaardwaarde is **false**.</span><span class="sxs-lookup"><span data-stu-id="79ddb-119">The default value is **false**.</span></span>
- <span data-ttu-id="79ddb-120">Aanvullende beperkingen voor de toegestane wachtwoorden kunnen worden geïmplementeerd met behulp van de `customPasswordRegex` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="79ddb-120">Additional constraints on the allowed passwords can be implemented by using the `customPasswordRegex` property.</span></span> <span data-ttu-id="79ddb-121">De tekenreeks in `customValidationMessage` wordt weergegeven wanneer u een wachtwoord aangepaste validatie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="79ddb-121">The string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="79ddb-122">De standaardwaarde voor beide eigenschappen is **null**.</span><span class="sxs-lookup"><span data-stu-id="79ddb-122">The default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="79ddb-123">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="79ddb-123">Sample output</span></span>
<span data-ttu-id="79ddb-124">Als `osPlatform` is **Windows**, of de gebruiker een wachtwoord in plaats van een openbare SSH-sleutel opgegeven, wordt de volgende uitvoer wordt verwacht:</span><span class="sxs-lookup"><span data-stu-id="79ddb-124">If `osPlatform` is **Windows**, or the user provided a password instead of an SSH public key, then the following output is expected:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="79ddb-125">Als de gebruiker een openbare SSH-sleutel hebt opgegeven, wordt de volgende uitvoer verwacht:</span><span class="sxs-lookup"><span data-stu-id="79ddb-125">If the user provided an SSH public key, then the following output is expected:</span></span>
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="79ddb-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="79ddb-126">Next steps</span></span>
* <span data-ttu-id="79ddb-127">Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="79ddb-127">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="79ddb-128">Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="79ddb-128">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="79ddb-129">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="79ddb-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
