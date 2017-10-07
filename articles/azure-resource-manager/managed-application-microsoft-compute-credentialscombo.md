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
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="5771c-103">Microsoft.Compute.CredentialsCombo UI-element</span><span class="sxs-lookup"><span data-stu-id="5771c-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="5771c-104">Een groep besturingselementen met ingebouwde validatie voor wachtwoorden voor Windows en Linux- en openbare SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="5771c-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span> <span data-ttu-id="5771c-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="5771c-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="5771c-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="5771c-106">UI sample</span></span>
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a><span data-ttu-id="5771c-108">Schema</span><span class="sxs-lookup"><span data-stu-id="5771c-108">Schema</span></span>
<span data-ttu-id="5771c-109">Als `osPlatform` is **Windows**, en vervolgens hello volgende schema wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="5771c-109">If `osPlatform` is **Windows**, then hello following schema is used:</span></span>
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

<span data-ttu-id="5771c-110">Als `osPlatform` is **Linux**, en vervolgens hello volgende schema wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="5771c-110">If `osPlatform` is **Linux**, then hello following schema is used:</span></span>
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

## <a name="remarks"></a><span data-ttu-id="5771c-111">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="5771c-111">Remarks</span></span>
- <span data-ttu-id="5771c-112">`osPlatform`moet worden opgegeven en kan **Windows** of **Linux**.</span><span class="sxs-lookup"><span data-stu-id="5771c-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="5771c-113">Als `constraints.required` te is ingesteld,**true**, vervolgens Hallo wachtwoord of SSH tekstvakken met openbare sleutel is toovalidate waarden moeten bevatten.</span><span class="sxs-lookup"><span data-stu-id="5771c-113">If `constraints.required` is set too**true**, then hello password or SSH public key text boxes must contain values toovalidate successfully.</span></span> <span data-ttu-id="5771c-114">de standaardwaarde Hallo is **true**.</span><span class="sxs-lookup"><span data-stu-id="5771c-114">hello default value is **true**.</span></span>
- <span data-ttu-id="5771c-115">Als `options.hideConfirmation` te is ingesteld,**true**, en vervolgens een tweede tekstvak voor het bevestigen van het wachtwoord van gebruiker Hallo Hallo wordt verborgen.</span><span class="sxs-lookup"><span data-stu-id="5771c-115">If `options.hideConfirmation` is set too**true**, then hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="5771c-116">de standaardwaarde Hallo is **false**.</span><span class="sxs-lookup"><span data-stu-id="5771c-116">hello default value is **false**.</span></span>
- <span data-ttu-id="5771c-117">Als `options.hidePassword` te is ingesteld,**true**, en vervolgens Hallo optie toouse wachtwoordverificatie wordt verborgen.</span><span class="sxs-lookup"><span data-stu-id="5771c-117">If `options.hidePassword` is set too**true**, then hello option toouse password authentication is hidden.</span></span> <span data-ttu-id="5771c-118">Het kan worden gebruikt alleen wanneer `osPlatform` is **Linux**.</span><span class="sxs-lookup"><span data-stu-id="5771c-118">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="5771c-119">De standaardwaarde is **false**.</span><span class="sxs-lookup"><span data-stu-id="5771c-119">The default value is **false**.</span></span>
- <span data-ttu-id="5771c-120">Aanvullende beperkingen op Hallo toegestaan wachtwoorden kunnen worden geïmplementeerd met behulp van Hallo `customPasswordRegex` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="5771c-120">Additional constraints on hello allowed passwords can be implemented by using hello `customPasswordRegex` property.</span></span> <span data-ttu-id="5771c-121">Hallo-reeks in `customValidationMessage` wordt weergegeven wanneer u een wachtwoord aangepaste validatie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="5771c-121">hello string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="5771c-122">Hallo standaardwaarde voor beide eigenschappen is **null**.</span><span class="sxs-lookup"><span data-stu-id="5771c-122">hello default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="5771c-123">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="5771c-123">Sample output</span></span>
<span data-ttu-id="5771c-124">Als `osPlatform` is **Windows**, of Hallo gebruiker een wachtwoord in plaats van een openbare SSH-sleutel opgegeven vervolgens hello volgende uitvoer wordt verwacht:</span><span class="sxs-lookup"><span data-stu-id="5771c-124">If `osPlatform` is **Windows**, or hello user provided a password instead of an SSH public key, then hello following output is expected:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="5771c-125">Als gebruiker Hallo openbare SSH-sleutel hebt opgegeven, wordt klikt u vervolgens hello volgende uitvoer verwacht.</span><span class="sxs-lookup"><span data-stu-id="5771c-125">If hello user provided an SSH public key, then hello following output is expected:</span></span>
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="5771c-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5771c-126">Next steps</span></span>
* <span data-ttu-id="5771c-127">Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5771c-127">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="5771c-128">Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5771c-128">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="5771c-129">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="5771c-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
