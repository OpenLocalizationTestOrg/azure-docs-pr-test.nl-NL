---
title: Beheerde toepassing PasswordBox UI-element aaaAzure | Microsoft Docs
description: Beschrijft Hallo Microsoft.Common.PasswordBox UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: bcb1f54c0bee464075ed732ead9aa3f88697f49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="2dfce-103">Microsoft.Common.PasswordBox UI-element</span><span class="sxs-lookup"><span data-stu-id="2dfce-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="2dfce-104">Een besturingselement dat kan worden gebruikt tooprovide en bevestig een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="2dfce-104">A control that can be used tooprovide and confirm a password.</span></span> <span data-ttu-id="2dfce-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="2dfce-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="2dfce-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="2dfce-106">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="2dfce-108">Schema</span><span class="sxs-lookup"><span data-stu-id="2dfce-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="2dfce-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="2dfce-109">Remarks</span></span>
- <span data-ttu-id="2dfce-110">Dit element ondersteunt geen Hallo `defaultValue` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="2dfce-110">This element doesn't support hello `defaultValue` property.</span></span>
- <span data-ttu-id="2dfce-111">Implementatiedetails van de voor `constraints`, Zie [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span><span class="sxs-lookup"><span data-stu-id="2dfce-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="2dfce-112">Als `options.hideConfirmation` te is ingesteld,**true**, tweede tekstvak voor het bevestigen van het wachtwoord van gebruiker Hallo Hallo wordt verborgen.</span><span class="sxs-lookup"><span data-stu-id="2dfce-112">If `options.hideConfirmation` is set too**true**, hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="2dfce-113">de standaardwaarde Hallo is **false**.</span><span class="sxs-lookup"><span data-stu-id="2dfce-113">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="2dfce-114">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="2dfce-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="2dfce-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2dfce-115">Next steps</span></span>
* <span data-ttu-id="2dfce-116">Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2dfce-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="2dfce-117">Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2dfce-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="2dfce-118">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="2dfce-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
