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
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="1f650-103">Microsoft.Compute.UserNameTextBox UI-element</span><span class="sxs-lookup"><span data-stu-id="1f650-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="1f650-104">Een tekstvak met ingebouwde validatie voor Windows en Linux-gebruikersnamen.</span><span class="sxs-lookup"><span data-stu-id="1f650-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="1f650-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="1f650-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="1f650-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="1f650-106">UI sample</span></span>
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="1f650-108">Schema</span><span class="sxs-lookup"><span data-stu-id="1f650-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="1f650-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="1f650-109">Remarks</span></span>
- <span data-ttu-id="1f650-110">Als `constraints.required` is ingesteld op **true**, en vervolgens in het tekstvak moet een waarde kan worden gevalideerd bevatten.</span><span class="sxs-lookup"><span data-stu-id="1f650-110">If `constraints.required` is set to **true**, then the text box must contain a value to validate successfully.</span></span> <span data-ttu-id="1f650-111">De standaardwaarde is **true**.</span><span class="sxs-lookup"><span data-stu-id="1f650-111">The default value is **true**.</span></span>
- <span data-ttu-id="1f650-112">`osPlatform`moet worden opgegeven en kan **Windows** of **Linux**.</span><span class="sxs-lookup"><span data-stu-id="1f650-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="1f650-113">`constraints.regex`is een reguliere-expressiepatroon van JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1f650-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="1f650-114">Indien opgegeven, klikt u vervolgens de waarde van het tekstvak moet overeenkomen met het patroon kan worden gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="1f650-114">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="1f650-115">De standaardwaarde is **null**.</span><span class="sxs-lookup"><span data-stu-id="1f650-115">The default value is **null**.</span></span>
- <span data-ttu-id="1f650-116">`constraints.validationMessage`is een tekenreeks om weer te geven wanneer de waarde van het tekstvak, de validatie is opgegeven mislukt door `constraints.regex`.</span><span class="sxs-lookup"><span data-stu-id="1f650-116">`constraints.validationMessage` is a string to display when the text box's value fails the validation specified by `constraints.regex`.</span></span> <span data-ttu-id="1f650-117">Als niet wordt opgegeven, wordt het tekstvak ingebouwde validatieberichten gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1f650-117">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="1f650-118">De standaardwaarde is **null**.</span><span class="sxs-lookup"><span data-stu-id="1f650-118">The default value is **null**.</span></span>
- <span data-ttu-id="1f650-119">Dit element heeft ingebouwde validatiefouten die is gebaseerd op de opgegeven waarde voor `osPlatform`.</span><span class="sxs-lookup"><span data-stu-id="1f650-119">This element has built-in validation that is based on the value specified for `osPlatform`.</span></span> <span data-ttu-id="1f650-120">De ingebouwde validatie kan worden gebruikt samen met een aangepaste reguliere expressie.</span><span class="sxs-lookup"><span data-stu-id="1f650-120">The built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="1f650-121">Als er een waarde voor `constraints.regex` is opgegeven, worden de ingebouwde en aangepaste validaties worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="1f650-121">If a value for `constraints.regex` is specified, then both the built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="1f650-122">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="1f650-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="1f650-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1f650-123">Next steps</span></span>
* <span data-ttu-id="1f650-124">Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1f650-124">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="1f650-125">Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1f650-125">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="1f650-126">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="1f650-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
