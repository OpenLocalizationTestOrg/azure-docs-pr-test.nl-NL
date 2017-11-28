---
title: Azure beheerde toepassing PasswordBox UI-element | Microsoft Docs
description: Beschrijft het Microsoft.Common.PasswordBox UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: 196a4b8f77145f83e46b4b23e148bb3a9dffc1b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="4d05d-103">Microsoft.Common.PasswordBox UI-element</span><span class="sxs-lookup"><span data-stu-id="4d05d-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="4d05d-104">Een besturingselement dat kan worden gebruikt om te bieden en bevestig een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="4d05d-104">A control that can be used to provide and confirm a password.</span></span> <span data-ttu-id="4d05d-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="4d05d-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="4d05d-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="4d05d-106">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="4d05d-108">Schema</span><span class="sxs-lookup"><span data-stu-id="4d05d-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.PasswordBox",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "",
    "validationMessage": ""
  },
  "options": {
    "hideConfirmation": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="4d05d-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="4d05d-109">Remarks</span></span>
- <span data-ttu-id="4d05d-110">Dit element biedt geen ondersteuning voor de `defaultValue` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="4d05d-110">This element doesn't support the `defaultValue` property.</span></span>
- <span data-ttu-id="4d05d-111">Implementatiedetails van de voor `constraints`, Zie [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span><span class="sxs-lookup"><span data-stu-id="4d05d-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="4d05d-112">Als `options.hideConfirmation` is ingesteld op **true**, het tweede tekstvak voor het bevestigen van het wachtwoord van de gebruiker wordt verborgen.</span><span class="sxs-lookup"><span data-stu-id="4d05d-112">If `options.hideConfirmation` is set to **true**, the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="4d05d-113">De standaardwaarde is **false**.</span><span class="sxs-lookup"><span data-stu-id="4d05d-113">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="4d05d-114">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="4d05d-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="4d05d-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4d05d-115">Next steps</span></span>
* <span data-ttu-id="4d05d-116">Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4d05d-116">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="4d05d-117">Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4d05d-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="4d05d-118">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="4d05d-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
