---
title: UI-definitie voor Azure Managed toepassingen maken aaaUnderstand | Microsoft Docs
description: Hierin wordt beschreven hoe toocreate UI definities voor beheerde Azure-toepassingen
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
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="d4ad1-103">Aan de slag met CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="d4ad1-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="d4ad1-104">Dit document bevat Hallo belangrijkste concepten van een CreateUiDefinition die wordt gebruikt door hello Azure portal toogenerate Hallo-gebruikersinterface voor het maken van een beheerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-104">This document introduces hello core concepts of a CreateUiDefinition, which is used by hello Azure portal toogenerate hello user interface for creating a managed application.</span></span>

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

<span data-ttu-id="d4ad1-105">Een CreateUiDefinition bevat altijd drie eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="d4ad1-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="d4ad1-106">handler</span><span class="sxs-lookup"><span data-stu-id="d4ad1-106">handler</span></span>
* <span data-ttu-id="d4ad1-107">Versie</span><span class="sxs-lookup"><span data-stu-id="d4ad1-107">version</span></span>
* <span data-ttu-id="d4ad1-108">parameters</span><span class="sxs-lookup"><span data-stu-id="d4ad1-108">parameters</span></span>

<span data-ttu-id="d4ad1-109">Voor beheerde toepassingen handler altijd moet `Microsoft.Compute.MultiVm`, Hallo ondersteund meest recente versie en `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and hello latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="d4ad1-110">Hallo-schema van de eigenschap parameters hello, is afhankelijk van Hallo combinatie van de opgegeven handler Hallo en versie.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-110">hello schema of hello parameters property depends on hello combination of hello specified handler and version.</span></span> <span data-ttu-id="d4ad1-111">Voor beheerde toepassingen Hallo ondersteund eigenschappen zijn `basics`, `steps`, en `outputs`.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-111">For managed applications, hello supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="d4ad1-112">Hallo basisbeginselen en stappen eigenschappen bevatten Hallo _elementen_ - zoals tekstvakken en vervolgkeuzelijsten - toobe in weergegeven hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-112">hello basics and steps properties contain hello _elements_ - like textboxes and dropdowns - toobe displayed in hello Azure portal.</span></span> <span data-ttu-id="d4ad1-113">Hallo-uitvoer eigenschap gebruikte toomap Hallo uitvoerwaarden van is Hallo opgegeven elementen toohello parameters van hello Azure Resource Manager-implementatiesjabloon.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-113">hello outputs property is used toomap hello output values of hello specified elements toohello parameters of hello Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="d4ad1-114">Inclusief `$schema` wordt aanbevolen, maar is optioneel.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="d4ad1-115">Indien opgegeven, de waarde voor Hallo `version` moet overeenkomen met de versie Hallo binnen Hallo `$schema` URI.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-115">If specified, hello value for `version` must match hello version within hello `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="d4ad1-116">Basisbeginselen</span><span class="sxs-lookup"><span data-stu-id="d4ad1-116">Basics</span></span>
<span data-ttu-id="d4ad1-117">Hallo basisbeginselen stap is altijd de eerste stap Hallo van Hallo wizard gegenereerd wanneer hello Azure-portal een CreateUiDefinition parseert.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-117">hello Basics step is always hello first step of hello wizard generated when hello Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="d4ad1-118">Bovendien toodisplaying Hallo elementen is opgegeven in `basics`, Hallo portal injects-elementen voor gebruikers toochoose Hallo abonnement, resourcegroep en locatie voor Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-118">In addition toodisplaying hello elements specified in `basics`, hello portal injects elements for users toochoose hello subscription, resource group, and location for hello deployment.</span></span> <span data-ttu-id="d4ad1-119">In het algemeen moeten elementen waarmee een query voor distributie-parameters, zoals Hallo-naam van een cluster of de administrator-referenties uitvoeren, gaat u in deze stap.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-119">Generally, elements that query for deployment-wide parameters, like hello name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="d4ad1-120">Als het gedrag van een element afhankelijk is van de gebruiker van het Hallo-abonnement, resourcegroep of locatie, worden niet dat element gebruikt in basisbeginselen.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-120">If an element's behavior depends on hello user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="d4ad1-121">Bijvoorbeeld: **Microsoft.Compute.SizeSelector** afhankelijk van de gebruiker Hallo abonnement en de locatie toodetermine Hallo lijst met beschikbare grootten.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-121">For example, **Microsoft.Compute.SizeSelector** depends on hello user's subscription and location toodetermine hello list of available sizes.</span></span> <span data-ttu-id="d4ad1-122">Daarom **Microsoft.Compute.SizeSelector** kan alleen worden gebruikt in stappen.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="d4ad1-123">In het algemeen alleen elementen in Hallo **Microsoft.Common** naamruimte in basisbeginselen kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-123">Generally, only elements in hello **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="d4ad1-124">Hoewel bepaalde elementen in andere naamruimten (zoals **Microsoft.Compute.Credentials**) dat niet afhankelijk zijn van de context van de gebruiker hello, nog steeds zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on hello user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="d4ad1-125">Stappen</span><span class="sxs-lookup"><span data-stu-id="d4ad1-125">Steps</span></span>
<span data-ttu-id="d4ad1-126">Hallo stappen eigenschap kan nul of meer extra stappen toodisplay na de basisbeginselen, die elk een of meer elementen bevat bevatten.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-126">hello steps property can contain zero or more additional steps toodisplay after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="d4ad1-127">Overweeg stappen per rol of laag van Hallo-toepassing wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-127">Consider adding steps per role or tier of hello application being deployed.</span></span> <span data-ttu-id="d4ad1-128">Bijvoorbeeld, een stap voor de invoer voor de hoofdknooppunten hello, en een voor Hallo worker-knooppunten in een cluster toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-128">For example, add a step for inputs for hello master nodes, and a step for hello worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="d4ad1-129">uitvoer</span><span class="sxs-lookup"><span data-stu-id="d4ad1-129">Outputs</span></span>
<span data-ttu-id="d4ad1-130">Hello Azure portal maakt gebruik van Hallo `outputs` toomap eigenschapselementen van `basics` en `steps` toohello parameters van hello Azure Resource Manager-implementatiesjabloon.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-130">hello Azure portal uses hello `outputs` property toomap elements from `basics` and `steps` toohello parameters of hello Azure Resource Manager deployment template.</span></span> <span data-ttu-id="d4ad1-131">Hallo-sleutels van deze woordenlijst zijn Hallo namen van de sjabloonparameters Hallo en Hallo-waarden zijn eigenschappen van Hallo uitvoer objecten van de elementen Hallo waarnaar wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-131">hello keys of this dictionary are hello names of hello template parameters, and hello values are properties of hello output objects from hello referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="d4ad1-132">Functies</span><span class="sxs-lookup"><span data-stu-id="d4ad1-132">Functions</span></span>
<span data-ttu-id="d4ad1-133">Vergelijkbare te[sjabloonfuncties](resource-group-template-functions.md) in Azure Resource Manager (zowel in de syntaxis en functionaliteit), CreateUiDefinition voorziet in functies voor het werken met in- en uitgangen elementen, evenals functies zoals voorwaardelijke.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-133">Similar too[template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4ad1-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d4ad1-134">Next steps</span></span>
<span data-ttu-id="d4ad1-135">CreateUiDefinition zelf is een eenvoudig schema.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="d4ad1-136">Hallo echte diepte van het afkomstig is van alle elementen Hallo ondersteund en functies, welke Hallo documenten te volgen in wondrous detail beschrijven:</span><span class="sxs-lookup"><span data-stu-id="d4ad1-136">hello real depth of it comes from all hello supported elements and functions, which hello following documents describe in wondrous detail:</span></span>

- [<span data-ttu-id="d4ad1-137">Elementen</span><span class="sxs-lookup"><span data-stu-id="d4ad1-137">Elements</span></span>](managed-application-createuidefinition-elements.md)
- [<span data-ttu-id="d4ad1-138">Functies</span><span class="sxs-lookup"><span data-stu-id="d4ad1-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="d4ad1-139">Een huidige JSON-schema voor CreateUiDefinition is hier beschikbaar: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="d4ad1-140">Latere versies zijn beschikbaar op Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-140">Later versions will be available at hello same location.</span></span> <span data-ttu-id="d4ad1-141">Vervang Hallo `0.1.2-preview` gedeelte van het Hallo-URL en Hallo `version` waarde met de versie-id Hallo u van plan bent toouse.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-141">Replace hello `0.1.2-preview` portion of hello URL and hello `version` value with hello version identifier you intend toouse.</span></span> <span data-ttu-id="d4ad1-142">Hallo momenteel ondersteund versie-id's zijn `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, en `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="d4ad1-142">hello currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>
