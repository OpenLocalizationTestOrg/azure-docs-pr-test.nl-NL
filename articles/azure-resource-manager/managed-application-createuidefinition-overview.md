---
title: UI-definitie maken voor beheerde Azure-toepassingen inzicht | Microsoft Docs
description: Hierin wordt beschreven hoe u de definities van de gebruikersinterface voor beheerde Azure-toepassingen maken
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 176b891538f85c5638a2321561c3d8bd377d245b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="a0a11-103">Aan de slag met CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="a0a11-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="a0a11-104">Dit document worden de belangrijkste concepten van een CreateUiDefinition die wordt gebruikt door de Azure-portal voor het genereren van de gebruikersinterface voor het maken van een beheerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="a0a11-104">This document introduces the core concepts of a CreateUiDefinition, which is used by the Azure portal to generate the user interface for creating a managed application.</span></span>

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

<span data-ttu-id="a0a11-105">Een CreateUiDefinition bevat altijd drie eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="a0a11-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="a0a11-106">handler</span><span class="sxs-lookup"><span data-stu-id="a0a11-106">handler</span></span>
* <span data-ttu-id="a0a11-107">Versie</span><span class="sxs-lookup"><span data-stu-id="a0a11-107">version</span></span>
* <span data-ttu-id="a0a11-108">Parameters</span><span class="sxs-lookup"><span data-stu-id="a0a11-108">parameters</span></span>

<span data-ttu-id="a0a11-109">Voor beheerde toepassingen handler altijd moet `Microsoft.Compute.MultiVm`, en de laatste ondersteunde versie is `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="a0a11-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and the latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="a0a11-110">Het schema van de eigenschap parameters is afhankelijk van de combinatie van de opgegeven handler en versie.</span><span class="sxs-lookup"><span data-stu-id="a0a11-110">The schema of the parameters property depends on the combination of the specified handler and version.</span></span> <span data-ttu-id="a0a11-111">Voor beheerde toepassingen, de ondersteunde eigenschappen zijn `basics`, `steps`, en `outputs`.</span><span class="sxs-lookup"><span data-stu-id="a0a11-111">For managed applications, the supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="a0a11-112">De eigenschappen van de basisprincipes en stappen bevatten de _elementen_ - zoals tekstvakken en vervolgkeuzelijsten - moet worden weergegeven in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a0a11-112">The basics and steps properties contain the _elements_ - like textboxes and dropdowns - to be displayed in the Azure portal.</span></span> <span data-ttu-id="a0a11-113">De uitvoer-eigenschap wordt gebruikt om de uitvoerwaarden van de opgegeven elementen toewijzen aan de parameters van de Azure Resource Manager-implementatiesjabloon.</span><span class="sxs-lookup"><span data-stu-id="a0a11-113">The outputs property is used to map the output values of the specified elements to the parameters of the Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="a0a11-114">Inclusief `$schema` wordt aanbevolen, maar is optioneel.</span><span class="sxs-lookup"><span data-stu-id="a0a11-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="a0a11-115">Als u opgeeft, wordt de waarde voor `version` moet overeenkomen met de versie in de `$schema` URI.</span><span class="sxs-lookup"><span data-stu-id="a0a11-115">If specified, the value for `version` must match the version within the `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="a0a11-116">Basisbeginselen</span><span class="sxs-lookup"><span data-stu-id="a0a11-116">Basics</span></span>
<span data-ttu-id="a0a11-117">De grondbeginselen van stap is altijd de eerste stap van de wizard gegenereerd wanneer de Azure portal een CreateUiDefinition wordt geparseerd.</span><span class="sxs-lookup"><span data-stu-id="a0a11-117">The Basics step is always the first step of the wizard generated when the Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="a0a11-118">Naast het weergeven van de elementen die zijn opgegeven in `basics`, de portal injects-elementen voor gebruikers om te kiezen voor het abonnement, resourcegroep en locatie voor de implementatie.</span><span class="sxs-lookup"><span data-stu-id="a0a11-118">In addition to displaying the elements specified in `basics`, the portal injects elements for users to choose the subscription, resource group, and location for the deployment.</span></span> <span data-ttu-id="a0a11-119">In het algemeen moeten elementen waarmee een query voor distributie-parameters, zoals de naam van een cluster of de administrator-referenties uitvoeren, gaat u in deze stap.</span><span class="sxs-lookup"><span data-stu-id="a0a11-119">Generally, elements that query for deployment-wide parameters, like the name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="a0a11-120">Als het gedrag van een element, is afhankelijk van abonnement, resourcegroep of locatie van de gebruiker, kan niet in basisbeginselen van dat element gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a0a11-120">If an element's behavior depends on the user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="a0a11-121">Bijvoorbeeld: **Microsoft.Compute.SizeSelector** is afhankelijk van het abonnement en de locatie voor het bepalen van de lijst met beschikbare grootten van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a0a11-121">For example, **Microsoft.Compute.SizeSelector** depends on the user's subscription and location to determine the list of available sizes.</span></span> <span data-ttu-id="a0a11-122">Daarom **Microsoft.Compute.SizeSelector** kan alleen worden gebruikt in stappen.</span><span class="sxs-lookup"><span data-stu-id="a0a11-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="a0a11-123">In het algemeen alleen elementen in de **Microsoft.Common** naamruimte in basisbeginselen kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a0a11-123">Generally, only elements in the **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="a0a11-124">Hoewel bepaalde elementen in andere naamruimten (zoals **Microsoft.Compute.Credentials**) dat niet afhankelijk zijn van de context van de gebruiker, nog steeds zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="a0a11-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on the user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="a0a11-125">Stappen</span><span class="sxs-lookup"><span data-stu-id="a0a11-125">Steps</span></span>
<span data-ttu-id="a0a11-126">De eigenschap stappen kan nul of meer extra stappen om weer te geven nadat de basisbeginselen, die elk een of meer elementen bevat bevatten.</span><span class="sxs-lookup"><span data-stu-id="a0a11-126">The steps property can contain zero or more additional steps to display after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="a0a11-127">Overweeg stappen per rol of laag van de toepassing wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a0a11-127">Consider adding steps per role or tier of the application being deployed.</span></span> <span data-ttu-id="a0a11-128">Voeg bijvoorbeeld een stap voor de invoer voor de hoofdknooppunten, en een voor worker-knooppunten in een cluster.</span><span class="sxs-lookup"><span data-stu-id="a0a11-128">For example, add a step for inputs for the master nodes, and a step for the worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="a0a11-129">uitvoer</span><span class="sxs-lookup"><span data-stu-id="a0a11-129">Outputs</span></span>
<span data-ttu-id="a0a11-130">De Azure portal maakt gebruik van de `outputs` eigenschap toewijzen van elementen uit `basics` en `steps` aan de parameters van de Azure Resource Manager-implementatiesjabloon.</span><span class="sxs-lookup"><span data-stu-id="a0a11-130">The Azure portal uses the `outputs` property to map elements from `basics` and `steps` to the parameters of the Azure Resource Manager deployment template.</span></span> <span data-ttu-id="a0a11-131">De sleutels van deze woordenlijst zijn de namen van de sjabloonparameters en de waarden worden de eigenschappen van de uitvoer-objecten van de elementen waarnaar wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="a0a11-131">The keys of this dictionary are the names of the template parameters, and the values are properties of the output objects from the referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="a0a11-132">Functies</span><span class="sxs-lookup"><span data-stu-id="a0a11-132">Functions</span></span>
<span data-ttu-id="a0a11-133">Net als bij [sjabloonfuncties](resource-group-template-functions.md) in Azure Resource Manager (zowel in de syntaxis en functionaliteit), CreateUiDefinition voorziet in functies voor het werken met in- en uitgangen elementen, evenals functies zoals voorwaardelijke.</span><span class="sxs-lookup"><span data-stu-id="a0a11-133">Similar to [template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0a11-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a0a11-134">Next steps</span></span>
<span data-ttu-id="a0a11-135">CreateUiDefinition zelf is een eenvoudig schema.</span><span class="sxs-lookup"><span data-stu-id="a0a11-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="a0a11-136">De echte diepte van het afkomstig is van de ondersteunde elementen en functies, die de volgende documenten wondrous gedetailleerd beschreven:</span><span class="sxs-lookup"><span data-stu-id="a0a11-136">The real depth of it comes from all the supported elements and functions, which the following documents describe in wondrous detail:</span></span>

- [<span data-ttu-id="a0a11-137">Elementen</span><span class="sxs-lookup"><span data-stu-id="a0a11-137">Elements</span></span>](managed-application-createuidefinition-elements.md)
- [<span data-ttu-id="a0a11-138">Functies</span><span class="sxs-lookup"><span data-stu-id="a0a11-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="a0a11-139">Een huidige JSON-schema voor CreateUiDefinition is hier beschikbaar: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="a0a11-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="a0a11-140">Latere versies zijn beschikbaar op dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="a0a11-140">Later versions will be available at the same location.</span></span> <span data-ttu-id="a0a11-141">Vervang de `0.1.2-preview` deel van de URL en de `version` waarde met de versie-id die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a0a11-141">Replace the `0.1.2-preview` portion of the URL and the `version` value with the version identifier you intend to use.</span></span> <span data-ttu-id="a0a11-142">De ondersteunde versie-id's `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, en `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="a0a11-142">The currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>