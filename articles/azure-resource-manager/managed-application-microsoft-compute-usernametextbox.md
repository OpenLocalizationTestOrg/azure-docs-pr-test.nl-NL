---
title: Beheerde toepassing UserNameTextBox UI-element aaaAzure | Microsoft Docs
description: Beschrijft Hallo Microsoft.Compute.UserNameTextBox UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: 33092014e804c4aabd56ba49144d9cd4d6a5fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="1df2f-103">Microsoft.Compute.UserNameTextBox UI-element</span><span class="sxs-lookup"><span data-stu-id="1df2f-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="1df2f-104">Een tekstvak met ingebouwde validatie voor Windows en Linux-gebruikersnamen.</span><span class="sxs-lookup"><span data-stu-id="1df2f-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="1df2f-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="1df2f-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="1df2f-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="1df2f-106">UI sample</span></span>
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="1df2f-108">Schema</span><span class="sxs-lookup"><span data-stu-id="1df2f-108">Schema</span></span>
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
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="1df2f-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="1df2f-109">Remarks</span></span>
- <span data-ttu-id="1df2f-110">Als `constraints.required` te is ingesteld,**true**, Hallo tekstvak is een waarde toovalidate moet bevatten.</span><span class="sxs-lookup"><span data-stu-id="1df2f-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="1df2f-111">de standaardwaarde Hallo is **true**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-111">hello default value is **true**.</span></span>
- <span data-ttu-id="1df2f-112">`osPlatform`moet worden opgegeven en kan **Windows** of **Linux**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="1df2f-113">`constraints.regex`is een reguliere-expressiepatroon van JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1df2f-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="1df2f-114">Indien opgegeven, klikt u vervolgens Hallo van het tekstvak waarde moet overeenkomen met Hallo patroon toovalidate is.</span><span class="sxs-lookup"><span data-stu-id="1df2f-114">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="1df2f-115">De standaardwaarde is **null**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-115">The default value is **null**.</span></span>
- <span data-ttu-id="1df2f-116">`constraints.validationMessage`een tekenreeks toodisplay is wanneer de waarde van het Hallo-tekstvak is mislukt Hallo validatie is opgegeven door `constraints.regex`.</span><span class="sxs-lookup"><span data-stu-id="1df2f-116">`constraints.validationMessage` is a string toodisplay when hello text box's value fails hello validation specified by `constraints.regex`.</span></span> <span data-ttu-id="1df2f-117">Als dat niet wordt opgegeven, wordt Hallo van het tekstvak ingebouwde validatie berichten worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1df2f-117">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="1df2f-118">de standaardwaarde Hallo is **null**.</span><span class="sxs-lookup"><span data-stu-id="1df2f-118">hello default value is **null**.</span></span>
- <span data-ttu-id="1df2f-119">Dit element heeft ingebouwde validatiefouten die is gebaseerd op Hallo-waarde opgegeven voor `osPlatform`.</span><span class="sxs-lookup"><span data-stu-id="1df2f-119">This element has built-in validation that is based on hello value specified for `osPlatform`.</span></span> <span data-ttu-id="1df2f-120">Hallo ingebouwde validatie kan worden gebruikt samen met een aangepaste reguliere expressie.</span><span class="sxs-lookup"><span data-stu-id="1df2f-120">hello built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="1df2f-121">Als er een waarde voor `constraints.regex` is opgegeven, worden beide Hallo ingebouwde en aangepaste validaties worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="1df2f-121">If a value for `constraints.regex` is specified, then both hello built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="1df2f-122">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="1df2f-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="1df2f-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1df2f-123">Next steps</span></span>
* <span data-ttu-id="1df2f-124">Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1df2f-124">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="1df2f-125">Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1df2f-125">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="1df2f-126">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="1df2f-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
