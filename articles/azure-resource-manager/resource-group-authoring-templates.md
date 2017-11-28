---
title: Resource Manager aaaAzure sjabloonstructuur en syntaxis | Microsoft Docs
description: Hierin wordt beschreven Hallo structuur en eigenschappen van Azure Resource Manager-sjablonen met behulp van declaratieve JSON-syntaxis.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="665d5-103">Begrijpen Hallo structuur en syntaxis van Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="665d5-103">Understand hello structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="665d5-104">Dit onderwerp beschrijft Hallo-structuur van een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="665d5-104">This topic describes hello structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="665d5-105">Deze geeft Hallo verschillende secties van de eigenschappen van een sjabloon en Hallo die beschikbaar zijn in deze secties.</span><span class="sxs-lookup"><span data-stu-id="665d5-105">It presents hello different sections of a template and hello properties that are available in those sections.</span></span> <span data-ttu-id="665d5-106">Hallo sjabloon bestaat uit JSON en uitdrukkingen die u kunt tooconstruct waarden voor uw implementatie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="665d5-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="665d5-107">Zie voor een stapsgewijze zelfstudie over het maken van een sjabloon, [maken van uw eerste Azure Resource Manager-sjabloon](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="665d5-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="665d5-108">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="665d5-108">Template format</span></span>
<span data-ttu-id="665d5-109">In de meest eenvoudige structuur bevat een sjabloon Hallo volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="665d5-109">In its simplest structure, a template contains hello following elements:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| <span data-ttu-id="665d5-110">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="665d5-110">Element name</span></span> | <span data-ttu-id="665d5-111">Vereist</span><span class="sxs-lookup"><span data-stu-id="665d5-111">Required</span></span> | <span data-ttu-id="665d5-112">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="665d5-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="665d5-113">$schema</span><span class="sxs-lookup"><span data-stu-id="665d5-113">$schema</span></span> |<span data-ttu-id="665d5-114">Ja</span><span class="sxs-lookup"><span data-stu-id="665d5-114">Yes</span></span> |<span data-ttu-id="665d5-115">Locatie van Hallo JSON-schema-bestand dat Hallo-versie van de sjabloontaal Hallo beschrijft.</span><span class="sxs-lookup"><span data-stu-id="665d5-115">Location of hello JSON schema file that describes hello version of hello template language.</span></span> <span data-ttu-id="665d5-116">Hallo-URL die wordt weergegeven in het voorgaande voorbeeld hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="665d5-116">Use hello URL shown in hello preceding example.</span></span> |
| <span data-ttu-id="665d5-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="665d5-117">contentVersion</span></span> |<span data-ttu-id="665d5-118">Ja</span><span class="sxs-lookup"><span data-stu-id="665d5-118">Yes</span></span> |<span data-ttu-id="665d5-119">Versie van de sjabloon hello (zoals 1.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="665d5-119">Version of hello template (such as 1.0.0.0).</span></span> <span data-ttu-id="665d5-120">U kunt een waarde opgeven voor dit element.</span><span class="sxs-lookup"><span data-stu-id="665d5-120">You can provide any value for this element.</span></span> <span data-ttu-id="665d5-121">Bij het implementeren van resources met behulp van Hallo-sjabloon gebruikt deze waarde kan zijn gebruikte toomake ervoor dat de juiste sjabloon hello wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="665d5-121">When deploying resources using hello template, this value can be used toomake sure that hello right template is being used.</span></span> |
| <span data-ttu-id="665d5-122">parameters</span><span class="sxs-lookup"><span data-stu-id="665d5-122">parameters</span></span> |<span data-ttu-id="665d5-123">Nee</span><span class="sxs-lookup"><span data-stu-id="665d5-123">No</span></span> |<span data-ttu-id="665d5-124">Waarden die zijn opgegeven voor de implementatie is uitgevoerd toocustomize resources implementeren.</span><span class="sxs-lookup"><span data-stu-id="665d5-124">Values that are provided when deployment is executed toocustomize resource deployment.</span></span> |
| <span data-ttu-id="665d5-125">variabelen</span><span class="sxs-lookup"><span data-stu-id="665d5-125">variables</span></span> |<span data-ttu-id="665d5-126">Nee</span><span class="sxs-lookup"><span data-stu-id="665d5-126">No</span></span> |<span data-ttu-id="665d5-127">De waarden die worden gebruikt als JSON-fragmenten in Hallo sjabloon toosimplify sjabloontaalexpressies.</span><span class="sxs-lookup"><span data-stu-id="665d5-127">Values that are used as JSON fragments in hello template toosimplify template language expressions.</span></span> |
| <span data-ttu-id="665d5-128">Resources</span><span class="sxs-lookup"><span data-stu-id="665d5-128">resources</span></span> |<span data-ttu-id="665d5-129">Ja</span><span class="sxs-lookup"><span data-stu-id="665d5-129">Yes</span></span> |<span data-ttu-id="665d5-130">Brontypen die worden geïmplementeerd of bijgewerkt in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="665d5-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="665d5-131">uitvoer</span><span class="sxs-lookup"><span data-stu-id="665d5-131">outputs</span></span> |<span data-ttu-id="665d5-132">Nee</span><span class="sxs-lookup"><span data-stu-id="665d5-132">No</span></span> |<span data-ttu-id="665d5-133">De waarden die na de implementatie worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="665d5-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="665d5-134">Elk element bevat eigenschappen die u kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="665d5-134">Each element contains properties you can set.</span></span> <span data-ttu-id="665d5-135">Hallo volgende voorbeeld bevat de volledige syntaxis Hallo voor een sjabloon:</span><span class="sxs-lookup"><span data-stu-id="665d5-135">hello following example contains hello full syntax for a template:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-hello parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

<span data-ttu-id="665d5-136">We onderzoeken Hallo secties van de sjabloon Hallo in meer detail verderop in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="665d5-136">We examine hello sections of hello template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="665d5-137">Expressies en functies</span><span class="sxs-lookup"><span data-stu-id="665d5-137">Expressions and functions</span></span>
<span data-ttu-id="665d5-138">Hallo basic syntaxis van de sjabloon Hallo is JSON.</span><span class="sxs-lookup"><span data-stu-id="665d5-138">hello basic syntax of hello template is JSON.</span></span> <span data-ttu-id="665d5-139">Expressies en functies echter uitbreiden Hallo JSON-waarden zijn beschikbaar in de sjabloon Hallo.</span><span class="sxs-lookup"><span data-stu-id="665d5-139">However, expressions and functions extend hello JSON values available within hello template.</span></span>  <span data-ttu-id="665d5-140">Expressies zijn geschreven in letterlijke JSON-tekenreeks waarvan de eerste en laatste tekens zijn Hallo haken: `[` en `]`respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="665d5-140">Expressions are written within JSON string literals whose first and last characters are hello brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="665d5-141">Hallo-waarde van Hallo expressie wordt geëvalueerd wanneer Hallo sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="665d5-141">hello value of hello expression is evaluated when hello template is deployed.</span></span> <span data-ttu-id="665d5-142">Hoewel geschreven als een letterlijke tekenreeks, zijn Hallo resultaat van de evaluatie van Hallo expressie van een ander JSON-type, zoals een matrix of een geheel getal, afhankelijk van de werkelijke Hallo-expressie.</span><span class="sxs-lookup"><span data-stu-id="665d5-142">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array or integer, depending on hello actual expression.</span></span>  <span data-ttu-id="665d5-143">een letterlijke tekenreeks beginnen met een haakje toohave `[`, maar dit wordt geïnterpreteerd als een expressie niet, voegt u een extra haakje toostart Hallo tekenreeks met `[[`.</span><span class="sxs-lookup"><span data-stu-id="665d5-143">toohave a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket toostart hello string with `[[`.</span></span>

<span data-ttu-id="665d5-144">Normaal gesproken gebruikt u expressies met functies tooperform bewerkingen voor het configureren van Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="665d5-144">Typically, you use expressions with functions tooperform operations for configuring hello deployment.</span></span> <span data-ttu-id="665d5-145">Net zoals in JavaScript-functieaanroepen die zijn opgemaakt als `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="665d5-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="665d5-146">U verwijzen naar eigenschappen met behulp van Hallo punt en [index] operators.</span><span class="sxs-lookup"><span data-stu-id="665d5-146">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="665d5-147">Hallo volgende voorbeeld ziet u hoe toouse diverse functies tijdens het construeren van waarden:</span><span class="sxs-lookup"><span data-stu-id="665d5-147">hello following example shows how toouse several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="665d5-148">Zie voor een volledige lijst met sjabloonfuncties Hallo [Azure Resource Manager-sjabloonfuncties](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="665d5-148">For hello full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="665d5-149">Parameters</span><span class="sxs-lookup"><span data-stu-id="665d5-149">Parameters</span></span>
<span data-ttu-id="665d5-150">In Hallo gedeelte parameters van Hallo sjabloon kunt u opgeven welke waarden u invoeren kunt bij het implementeren van Hallo resources.</span><span class="sxs-lookup"><span data-stu-id="665d5-150">In hello parameters section of hello template, you specify which values you can input when deploying hello resources.</span></span> <span data-ttu-id="665d5-151">De parameterwaarden van deze kunnen u toocustomize Hallo implementatie door het verstrekken van waarden die zijn aangepast voor een bepaalde omgeving (zoals ontwikkelen, testen en productie).</span><span class="sxs-lookup"><span data-stu-id="665d5-151">These parameter values enable you toocustomize hello deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="665d5-152">U hebt geen tooprovide parameters in de sjabloon, maar zonder parameters uw sjabloon altijd Hallo zou implementeren dezelfde resources met dezelfde namen, locaties en eigenschappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="665d5-152">You do not have tooprovide parameters in your template, but without parameters your template would always deploy hello same resources with hello same names, locations, and properties.</span></span>

<span data-ttu-id="665d5-153">U kunt parameters definiëren Hello structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="665d5-153">You define parameters with hello following structure:</span></span>

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| <span data-ttu-id="665d5-154">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="665d5-154">Element name</span></span> | <span data-ttu-id="665d5-155">Vereist</span><span class="sxs-lookup"><span data-stu-id="665d5-155">Required</span></span> | <span data-ttu-id="665d5-156">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="665d5-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="665d5-157">parameterName</span><span class="sxs-lookup"><span data-stu-id="665d5-157">parameterName</span></span> |<span data-ttu-id="665d5-158">Ja</span><span class="sxs-lookup"><span data-stu-id="665d5-158">Yes</span></span> |<span data-ttu-id="665d5-159">Naam van Hallo-parameter.</span><span class="sxs-lookup"><span data-stu-id="665d5-159">Name of hello parameter.</span></span> <span data-ttu-id="665d5-160">Moet een geldige JavaScript-id.</span><span class="sxs-lookup"><span data-stu-id="665d5-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="665d5-161">type</span><span class="sxs-lookup"><span data-stu-id="665d5-161">type</span></span> |<span data-ttu-id="665d5-162">Ja</span><span class="sxs-lookup"><span data-stu-id="665d5-162">Yes</span></span> |<span data-ttu-id="665d5-163">Type Hallo parameterwaarde.</span><span class="sxs-lookup"><span data-stu-id="665d5-163">Type of hello parameter value.</span></span> <span data-ttu-id="665d5-164">Zie Hallo lijst met toegestane typen na deze tabel.</span><span class="sxs-lookup"><span data-stu-id="665d5-164">See hello list of allowed types after this table.</span></span> |
| <span data-ttu-id="665d5-165">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="665d5-165">defaultValue</span></span> |<span data-ttu-id="665d5-166">Nee</span><span class="sxs-lookup"><span data-stu-id="665d5-166">No</span></span> |<span data-ttu-id="665d5-167">De standaardwaarde voor parameter hello, als geen waarde is opgegeven voor parameter Hallo.</span><span class="sxs-lookup"><span data-stu-id="665d5-167">Default value for hello parameter, if no value is provided for hello parameter.</span></span> |
| <span data-ttu-id="665d5-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="665d5-168">allowedValues</span></span> |<span data-ttu-id="665d5-169">Nee</span><span class="sxs-lookup"><span data-stu-id="665d5-169">No</span></span> |<span data-ttu-id="665d5-170">Matrix van toegestane waarden voor Hallo parameter toomake ervoor dat de juiste waarde Hallo worden verstrekt.</span><span class="sxs-lookup"><span data-stu-id="665d5-170">Array of allowed values for hello parameter toomake sure that hello right value is provided.</span></span> |
| <span data-ttu-id="665d5-171">MinValue</span><span class="sxs-lookup"><span data-stu-id="665d5-171">minValue</span></span> |<span data-ttu-id="665d5-172">Nee</span><span class="sxs-lookup"><span data-stu-id="665d5-172">No</span></span> |<span data-ttu-id="665d5-173">Hallo minimale waarde voor de parameters van het type int, deze waarde is liggen.</span><span class="sxs-lookup"><span data-stu-id="665d5-173">hello minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="665d5-174">MaxValue</span><span class="sxs-lookup"><span data-stu-id="665d5-174">maxValue</span></span> |<span data-ttu-id="665d5-175">Nee</span><span class="sxs-lookup"><span data-stu-id="665d5-175">No</span></span> |<span data-ttu-id="665d5-176">Hallo maximale waarde voor de parameters van het type int, deze waarde is liggen.</span><span class="sxs-lookup"><span data-stu-id="665d5-176">hello maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="665d5-177">minLength</span><span class="sxs-lookup"><span data-stu-id="665d5-177">minLength</span></span> |<span data-ttu-id="665d5-178">Nee</span><span class="sxs-lookup"><span data-stu-id="665d5-178">No</span></span> |<span data-ttu-id="665d5-179">minimumlengte voor string, secureString en array typeparameters Hello, deze waarde is liggen.</span><span class="sxs-lookup"><span data-stu-id="665d5-179">hello minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="665d5-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="665d5-180">maxLength</span></span> |<span data-ttu-id="665d5-181">Nee</span><span class="sxs-lookup"><span data-stu-id="665d5-181">No</span></span> |<span data-ttu-id="665d5-182">Hallo maximale lengte voor string, secureString en array typeparameters, deze waarde is liggen.</span><span class="sxs-lookup"><span data-stu-id="665d5-182">hello maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="665d5-183">description</span><span class="sxs-lookup"><span data-stu-id="665d5-183">description</span></span> |<span data-ttu-id="665d5-184">Nee</span><span class="sxs-lookup"><span data-stu-id="665d5-184">No</span></span> |<span data-ttu-id="665d5-185">Beschrijving van Hallo-parameter die wordt weergegeven toousers via Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="665d5-185">Description of hello parameter that is displayed toousers through hello portal.</span></span> |

<span data-ttu-id="665d5-186">Hallo toegestane typen en waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="665d5-186">hello allowed types and values are:</span></span>

* <span data-ttu-id="665d5-187">**tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="665d5-187">**string**</span></span>
* <span data-ttu-id="665d5-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="665d5-188">**secureString**</span></span>
* <span data-ttu-id="665d5-189">**int**</span><span class="sxs-lookup"><span data-stu-id="665d5-189">**int**</span></span>
* <span data-ttu-id="665d5-190">**BOOL**</span><span class="sxs-lookup"><span data-stu-id="665d5-190">**bool**</span></span>
* <span data-ttu-id="665d5-191">**object**</span><span class="sxs-lookup"><span data-stu-id="665d5-191">**object**</span></span> 
* <span data-ttu-id="665d5-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="665d5-192">**secureObject**</span></span>
* <span data-ttu-id="665d5-193">**matrix**</span><span class="sxs-lookup"><span data-stu-id="665d5-193">**array**</span></span>

<span data-ttu-id="665d5-194">een parameter opgegeven als een optioneel, toospecify bieden een defaultValue (kunnen geen lege tekenreeks zijn).</span><span class="sxs-lookup"><span data-stu-id="665d5-194">toospecify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="665d5-195">Als u een parameternaam in de sjabloon die overeenkomt met een parameter in Hallo opdracht toodeploy Hallo sjabloon opgeeft, is het mogelijke verwarring over Hallo-waarden die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="665d5-195">If you specify a parameter name in your template that matches a parameter in hello command toodeploy hello template, there is potential ambiguity about hello values you provide.</span></span> <span data-ttu-id="665d5-196">Resource Manager lost deze verwarring door toe te voegen Hallo postfix **FromTemplate** toohello sjabloonparameter.</span><span class="sxs-lookup"><span data-stu-id="665d5-196">Resource Manager resolves this confusion by adding hello postfix **FromTemplate** toohello template parameter.</span></span> <span data-ttu-id="665d5-197">Bijvoorbeeld, als u een parameter genaamd opnemen **ResourceGroupName** in uw sjabloon een conflict met de Hallo **ResourceGroupName** parameter in Hallo [ Nieuwe AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="665d5-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="665d5-198">Tijdens de implementatie, u bent na vragen aan gebruiker tooprovide een waarde voor **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="665d5-198">During deployment, you are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="665d5-199">In het algemeen voorkomt u deze verwarring door te geven geen parameters met Hallo dezelfde naam als parameters die worden gebruikt voor implementatiebewerkingen.</span><span class="sxs-lookup"><span data-stu-id="665d5-199">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="665d5-200">Alle wachtwoorden, sleutels en andere geheime informatie moeten hello gebruiken **secureString** type.</span><span class="sxs-lookup"><span data-stu-id="665d5-200">All passwords, keys, and other secrets should use hello **secureString** type.</span></span> <span data-ttu-id="665d5-201">Als u gevoelige gegevens in een JSON-object doorgeven, gebruikt u Hallo **secureObject** type.</span><span class="sxs-lookup"><span data-stu-id="665d5-201">If you pass sensitive data in a JSON object, use hello **secureObject** type.</span></span> <span data-ttu-id="665d5-202">Sjabloonparameters met secureString of secureObject typen kunnen niet worden gelezen na de implementatie van de resource.</span><span class="sxs-lookup"><span data-stu-id="665d5-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="665d5-203">Hallo ziet volgende vermelding in de geschiedenis van de implementatie Hallo u bijvoorbeeld Hallo-waarde voor een tekenreeks en object, maar niet voor secureString en secureObject.</span><span class="sxs-lookup"><span data-stu-id="665d5-203">For example, hello following entry in hello deployment history shows hello value for a string and object but not for secureString and secureObject.</span></span>
>
> ![waarden van de implementatie weergeven](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="665d5-205">Hallo volgende voorbeeld wordt getoond hoe toodefine parameters:</span><span class="sxs-lookup"><span data-stu-id="665d5-205">hello following example shows how toodefine parameters:</span></span>

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

<span data-ttu-id="665d5-206">Zie voor hoe tooinput Hallo parameter tijdens de implementatie waarden, [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="665d5-206">For how tooinput hello parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="665d5-207">Variabelen</span><span class="sxs-lookup"><span data-stu-id="665d5-207">Variables</span></span>
<span data-ttu-id="665d5-208">In de sectie met sjabloonvariabelen hello, kunt u waarden die kunnen worden gebruikt in uw sjabloon opstellen.</span><span class="sxs-lookup"><span data-stu-id="665d5-208">In hello variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="665d5-209">U hoeft geen toodefine variabelen, maar ze vaak uw sjabloon vereenvoudigen doordat complexe expressies.</span><span class="sxs-lookup"><span data-stu-id="665d5-209">You do not need toodefine variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="665d5-210">U kunt variabelen definiëren Hello structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="665d5-210">You define variables with hello following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="665d5-211">Hallo volgende voorbeeld wordt getoond hoe toodefine een variabele die is samengesteld uit twee parameterwaarden:</span><span class="sxs-lookup"><span data-stu-id="665d5-211">hello following example shows how toodefine a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="665d5-212">Hallo volgende voorbeeld ziet u een variabele die is complex type JSON en variabelen die zijn samengesteld uit andere variabelen:</span><span class="sxs-lookup"><span data-stu-id="665d5-212">hello next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a><span data-ttu-id="665d5-213">Resources</span><span class="sxs-lookup"><span data-stu-id="665d5-213">Resources</span></span>
<span data-ttu-id="665d5-214">In de sectie bronnen Hallo definieert u Hallo-resources die worden geïmplementeerd of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="665d5-214">In hello resources section, you define hello resources that are deployed or updated.</span></span> <span data-ttu-id="665d5-215">Deze sectie ophalen ingewikkeld omdat u moet begrijpen Hallo typt u implementeert tooprovide Hallo juiste waarden.</span><span class="sxs-lookup"><span data-stu-id="665d5-215">This section can get complicated because you must understand hello types you are deploying tooprovide hello right values.</span></span> <span data-ttu-id="665d5-216">Hallo resource-specifieke Zie voor waarden (apiVersion, type en eigenschappen) moet u tooset [resources in Azure Resource Manager-sjablonen definiëren](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="665d5-216">For hello resource-specific values (apiVersion, type, and properties) that you need tooset, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="665d5-217">U kunt resources definiëren Hello structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="665d5-217">You define resources with hello following structure:</span></span>

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| <span data-ttu-id="665d5-218">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="665d5-218">Element name</span></span> | <span data-ttu-id="665d5-219">Vereist</span><span class="sxs-lookup"><span data-stu-id="665d5-219">Required</span></span> | <span data-ttu-id="665d5-220">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="665d5-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="665d5-221">Voorwaarde</span><span class="sxs-lookup"><span data-stu-id="665d5-221">condition</span></span> | <span data-ttu-id="665d5-222">Nee</span><span class="sxs-lookup"><span data-stu-id="665d5-222">No</span></span> | <span data-ttu-id="665d5-223">Booleaanse waarde die aangeeft of Hallo resource wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="665d5-223">Boolean value that indicates whether hello resource is deployed.</span></span> |
| <span data-ttu-id="665d5-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="665d5-224">apiVersion</span></span> |<span data-ttu-id="665d5-225">Ja</span><span class="sxs-lookup"><span data-stu-id="665d5-225">Yes</span></span> |<span data-ttu-id="665d5-226">Versie van Hallo REST-API toouse voor het maken van Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="665d5-226">Version of hello REST API toouse for creating hello resource.</span></span> |
| <span data-ttu-id="665d5-227">type</span><span class="sxs-lookup"><span data-stu-id="665d5-227">type</span></span> |<span data-ttu-id="665d5-228">Ja</span><span class="sxs-lookup"><span data-stu-id="665d5-228">Yes</span></span> |<span data-ttu-id="665d5-229">Type Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="665d5-229">Type of hello resource.</span></span> <span data-ttu-id="665d5-230">Deze waarde is een combinatie van Hallo-naamruimte van het Hallo-resourceprovider en Hallo resourcetype (zoals **Microsoft.Storage/storageAccounts**).</span><span class="sxs-lookup"><span data-stu-id="665d5-230">This value is a combination of hello namespace of hello resource provider and hello resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="665d5-231">naam</span><span class="sxs-lookup"><span data-stu-id="665d5-231">name</span></span> |<span data-ttu-id="665d5-232">Ja</span><span class="sxs-lookup"><span data-stu-id="665d5-232">Yes</span></span> |<span data-ttu-id="665d5-233">Naam van het Hallo-resource.</span><span class="sxs-lookup"><span data-stu-id="665d5-233">Name of hello resource.</span></span> <span data-ttu-id="665d5-234">Hallo-naam moet voldoen aan URI onderdeel beperkingen gedefinieerd in RFC3986.</span><span class="sxs-lookup"><span data-stu-id="665d5-234">hello name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="665d5-235">Bovendien Azure-services die beschikbaar Hallo resource naam toooutside partijen Hallo naam toomake u dit niet is een poging toospoof valideren een andere identiteit.</span><span class="sxs-lookup"><span data-stu-id="665d5-235">In addition, Azure services that expose hello resource name toooutside parties validate hello name toomake sure it is not an attempt toospoof another identity.</span></span> |
| <span data-ttu-id="665d5-236">location</span><span class="sxs-lookup"><span data-stu-id="665d5-236">location</span></span> |<span data-ttu-id="665d5-237">Varieert</span><span class="sxs-lookup"><span data-stu-id="665d5-237">Varies</span></span> |<span data-ttu-id="665d5-238">Ondersteunde geografische locaties Hallo opgegeven resource.</span><span class="sxs-lookup"><span data-stu-id="665d5-238">Supported geo-locations of hello provided resource.</span></span> <span data-ttu-id="665d5-239">U kunt kiezen uit de beschikbare locaties Hallo, maar doorgaans het zin toopick maakt een sluiten tooyour gebruikers.</span><span class="sxs-lookup"><span data-stu-id="665d5-239">You can select any of hello available locations, but typically it makes sense toopick one that is close tooyour users.</span></span> <span data-ttu-id="665d5-240">Meestal ook is het zinvol tooplace resources die met elkaar in Hallo dezelfde communiceren regio.</span><span class="sxs-lookup"><span data-stu-id="665d5-240">Usually, it also makes sense tooplace resources that interact with each other in hello same region.</span></span> <span data-ttu-id="665d5-241">De meeste brontypen die een locatie vereist, maar sommige typen (zoals een roltoewijzing) hoeven niet een locatie.</span><span class="sxs-lookup"><span data-stu-id="665d5-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="665d5-242">Zie [Resourcelocatie instellen in Azure Resource Manager-sjablonen](resource-manager-template-location.md).</span><span class="sxs-lookup"><span data-stu-id="665d5-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="665d5-243">tags</span><span class="sxs-lookup"><span data-stu-id="665d5-243">tags</span></span> |<span data-ttu-id="665d5-244">Nee</span><span class="sxs-lookup"><span data-stu-id="665d5-244">No</span></span> |<span data-ttu-id="665d5-245">Labels die gekoppeld aan het Hallo-resource zijn.</span><span class="sxs-lookup"><span data-stu-id="665d5-245">Tags that are associated with hello resource.</span></span> <span data-ttu-id="665d5-246">Zie [resources in Azure Resource Manager-sjablonen taggen](resource-manager-template-tags.md).</span><span class="sxs-lookup"><span data-stu-id="665d5-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="665d5-247">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="665d5-247">comments</span></span> |<span data-ttu-id="665d5-248">Nee</span><span class="sxs-lookup"><span data-stu-id="665d5-248">No</span></span> |<span data-ttu-id="665d5-249">De notities voor resources in uw sjabloon Hallo documenteren</span><span class="sxs-lookup"><span data-stu-id="665d5-249">Your notes for documenting hello resources in your template</span></span> |
| <span data-ttu-id="665d5-250">Kopiëren</span><span class="sxs-lookup"><span data-stu-id="665d5-250">copy</span></span> |<span data-ttu-id="665d5-251">Nee</span><span class="sxs-lookup"><span data-stu-id="665d5-251">No</span></span> |<span data-ttu-id="665d5-252">Als meer dan één exemplaar is vereist, Hallo aantal resources toocreate.</span><span class="sxs-lookup"><span data-stu-id="665d5-252">If more than one instance is needed, hello number of resources toocreate.</span></span> <span data-ttu-id="665d5-253">Hallo-standaardmodus is parallelle.</span><span class="sxs-lookup"><span data-stu-id="665d5-253">hello default mode is parallel.</span></span> <span data-ttu-id="665d5-254">Seriële mode opgeven wanneer u niet wilt dat alle of resources toodeploy op Hallo Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="665d5-254">Specify serial mode when you do not want all or hello resources toodeploy at hello same time.</span></span> <span data-ttu-id="665d5-255">Zie voor meer informatie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="665d5-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="665d5-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="665d5-256">dependsOn</span></span> |<span data-ttu-id="665d5-257">Nee</span><span class="sxs-lookup"><span data-stu-id="665d5-257">No</span></span> |<span data-ttu-id="665d5-258">Resources die moeten worden geïmplementeerd voordat u deze bron wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="665d5-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="665d5-259">Resource Manager Hallo afhankelijkheden tussen resources geëvalueerd en worden ze geïmplementeerd in de juiste volgorde Hallo.</span><span class="sxs-lookup"><span data-stu-id="665d5-259">Resource Manager evaluates hello dependencies between resources and deploys them in hello correct order.</span></span> <span data-ttu-id="665d5-260">Wanneer u resources zijn niet afhankelijk van elkaar, worden ze geïmplementeerd parallel.</span><span class="sxs-lookup"><span data-stu-id="665d5-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="665d5-261">Hallo-waarden zijn een door komma's gescheiden lijst van een resource namen of unieke id's voor een resource.</span><span class="sxs-lookup"><span data-stu-id="665d5-261">hello value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="665d5-262">Alleen de lijst van resources die zijn geïmplementeerd in deze sjabloon.</span><span class="sxs-lookup"><span data-stu-id="665d5-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="665d5-263">Bronnen die niet in deze sjabloon zijn gedefinieerd, moeten al bestaan.</span><span class="sxs-lookup"><span data-stu-id="665d5-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="665d5-264">Vermijd toe te voegen onnodige afhankelijkheden als ze kunnen uw implementatie vertragen en circulaire afhankelijkheden maken.</span><span class="sxs-lookup"><span data-stu-id="665d5-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="665d5-265">Zie voor instructies over de afhankelijkheden van de instelling [afhankelijkheden definiëren in Azure Resource Manager-sjablonen](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="665d5-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="665d5-266">properties</span><span class="sxs-lookup"><span data-stu-id="665d5-266">properties</span></span> |<span data-ttu-id="665d5-267">Nee</span><span class="sxs-lookup"><span data-stu-id="665d5-267">No</span></span> |<span data-ttu-id="665d5-268">Resource-specifieke configuratie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="665d5-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="665d5-269">Hallo-waarden voor Hallo eigenschappen Hallo dezelfde zijn als u voorzien in de aanvraagtekst Hallo Hallo REST-API (PUT-methode) toocreate Hallo bewerkingsresource Hallo-waarden.</span><span class="sxs-lookup"><span data-stu-id="665d5-269">hello values for hello properties are hello same as hello values you provide in hello request body for hello REST API operation (PUT method) toocreate hello resource.</span></span> <span data-ttu-id="665d5-270">U kunt een kopie matrix toocreate ook meerdere exemplaren van een eigenschap opgeven.</span><span class="sxs-lookup"><span data-stu-id="665d5-270">You can also specify a copy array toocreate multiple instances of a property.</span></span> <span data-ttu-id="665d5-271">Zie voor meer informatie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="665d5-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="665d5-272">Resources</span><span class="sxs-lookup"><span data-stu-id="665d5-272">resources</span></span> |<span data-ttu-id="665d5-273">Nee</span><span class="sxs-lookup"><span data-stu-id="665d5-273">No</span></span> |<span data-ttu-id="665d5-274">Onderliggende resources die afhankelijk zijn van Hallo bron wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="665d5-274">Child resources that depend on hello resource being defined.</span></span> <span data-ttu-id="665d5-275">Geef alleen brontypen die worden toegestaan door het Hallo-schema van Hallo bovenliggende resource.</span><span class="sxs-lookup"><span data-stu-id="665d5-275">Only provide resource types that are permitted by hello schema of hello parent resource.</span></span> <span data-ttu-id="665d5-276">Hallo volledig gekwalificeerde type Hallo onderliggende resource bevat Hallo bovenliggende brontype, zoals **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="665d5-276">hello fully qualified type of hello child resource includes hello parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="665d5-277">Afhankelijkheid van Hallo bovenliggende resource niet geïmpliceerd.</span><span class="sxs-lookup"><span data-stu-id="665d5-277">Dependency on hello parent resource is not implied.</span></span> <span data-ttu-id="665d5-278">U moet deze afhankelijkheid expliciet definiëren.</span><span class="sxs-lookup"><span data-stu-id="665d5-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="665d5-279">Hallo resources sectie bevat een matrix van Hallo resources toodeploy.</span><span class="sxs-lookup"><span data-stu-id="665d5-279">hello resources section contains an array of hello resources toodeploy.</span></span> <span data-ttu-id="665d5-280">U kunt ook een matrix van onderliggende resources binnen elke resource definiëren.</span><span class="sxs-lookup"><span data-stu-id="665d5-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="665d5-281">Het gedeelte van uw resources kan daarom een structuur zoals hebben:</span><span class="sxs-lookup"><span data-stu-id="665d5-281">Therefore, your resources section could have a structure like:</span></span>

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

<span data-ttu-id="665d5-282">Zie voor meer informatie over het definiëren van de onderliggende resources [naam en type voor onderliggende resource in het Resource Manager-sjabloon instellen](resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="665d5-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="665d5-283">Hallo **voorwaarde** element geeft aan of Hallo resource wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="665d5-283">hello **condition** element specifies whether hello resource is deployed.</span></span> <span data-ttu-id="665d5-284">Hallo-waarde voor dit element wordt omgezet tootrue of ONWAAR.</span><span class="sxs-lookup"><span data-stu-id="665d5-284">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="665d5-285">Bijvoorbeeld: toospecify of een nieuw opslagaccount wordt geïmplementeerd, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="665d5-285">For example, toospecify whether a new storage account is deployed, use:</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="665d5-286">Zie voor een voorbeeld van het gebruik van een nieuwe of bestaande resourcegroep [nieuwe of bestaande voorwaarde sjabloon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="665d5-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="665d5-287">toospecify of een virtuele machine wordt geïmplementeerd met een wachtwoord of SSH-sleutel, definieert twee versies van Hallo virtuele machine in de sjabloon en het gebruik **voorwaarde** toodifferentiate gebruik.</span><span class="sxs-lookup"><span data-stu-id="665d5-287">toospecify whether a virtual machine is deployed with a password or SSH key, define two versions of hello virtual machine in your template and use **condition** toodifferentiate usage.</span></span> <span data-ttu-id="665d5-288">Een parameter die welke scenario toodeploy aangeeft doorgeven.</span><span class="sxs-lookup"><span data-stu-id="665d5-288">Pass a parameter that specifies which scenario toodeploy.</span></span>

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

<span data-ttu-id="665d5-289">Zie voor een voorbeeld van het gebruik van een wachtwoord of SSH-sleutel toodeploy virtuele machine [gebruikersnaam of SSH voorwaarde sjabloon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="665d5-289">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="665d5-290">uitvoer</span><span class="sxs-lookup"><span data-stu-id="665d5-290">Outputs</span></span>
<span data-ttu-id="665d5-291">In sectie Hallo uitvoer geeft u de waarden die worden geretourneerd van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="665d5-291">In hello Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="665d5-292">Bijvoorbeeld, u kan Hallo URI tooaccess geïmplementeerde resource geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="665d5-292">For example, you could return hello URI tooaccess a deployed resource.</span></span>

<span data-ttu-id="665d5-293">Hallo toont volgende voorbeeld Hallo-structuur van de definitie van een uitvoer:</span><span class="sxs-lookup"><span data-stu-id="665d5-293">hello following example shows hello structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="665d5-294">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="665d5-294">Element name</span></span> | <span data-ttu-id="665d5-295">Vereist</span><span class="sxs-lookup"><span data-stu-id="665d5-295">Required</span></span> | <span data-ttu-id="665d5-296">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="665d5-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="665d5-297">outputName</span><span class="sxs-lookup"><span data-stu-id="665d5-297">outputName</span></span> |<span data-ttu-id="665d5-298">Ja</span><span class="sxs-lookup"><span data-stu-id="665d5-298">Yes</span></span> |<span data-ttu-id="665d5-299">Naam van de uitvoerwaarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="665d5-299">Name of hello output value.</span></span> <span data-ttu-id="665d5-300">Moet een geldige JavaScript-id.</span><span class="sxs-lookup"><span data-stu-id="665d5-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="665d5-301">type</span><span class="sxs-lookup"><span data-stu-id="665d5-301">type</span></span> |<span data-ttu-id="665d5-302">Ja</span><span class="sxs-lookup"><span data-stu-id="665d5-302">Yes</span></span> |<span data-ttu-id="665d5-303">Type van de uitvoerwaarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="665d5-303">Type of hello output value.</span></span> <span data-ttu-id="665d5-304">Uitvoerwaarden ondersteuning Hallo dezelfde als sjabloon invoerparameters typen.</span><span class="sxs-lookup"><span data-stu-id="665d5-304">Output values support hello same types as template input parameters.</span></span> |
| <span data-ttu-id="665d5-305">waarde</span><span class="sxs-lookup"><span data-stu-id="665d5-305">value</span></span> |<span data-ttu-id="665d5-306">Ja</span><span class="sxs-lookup"><span data-stu-id="665d5-306">Yes</span></span> |<span data-ttu-id="665d5-307">De sjabloontaalexpressie dat wordt geëvalueerd en geretourneerd als de waarde voor uitvoer.</span><span class="sxs-lookup"><span data-stu-id="665d5-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="665d5-308">Hallo volgende voorbeeld ziet u een waarde die wordt geretourneerd in Hallo uitvoer sectie.</span><span class="sxs-lookup"><span data-stu-id="665d5-308">hello following example shows a value that is returned in hello Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="665d5-309">Zie voor meer informatie over het werken met uitvoer [delen status in Azure Resource Manager-sjablonen](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="665d5-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="665d5-310">Limieten voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="665d5-310">Template limits</span></span>

<span data-ttu-id="665d5-311">Hallo-limiet van uw sjabloon too1 MB en elke parameter too64 KB-bestand.</span><span class="sxs-lookup"><span data-stu-id="665d5-311">Limit hello size of your template too1 MB, and each parameter file too64 KB.</span></span> <span data-ttu-id="665d5-312">Hallo 1 MB limiet geldt toohello eindstatus van Hallo sjabloon nadat deze is uitgebreid met iteratieve resourcedefinities en waarden voor parameters en variabelen.</span><span class="sxs-lookup"><span data-stu-id="665d5-312">hello 1-MB limit applies toohello final state of hello template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="665d5-313">Ook bent u beperkt tot:</span><span class="sxs-lookup"><span data-stu-id="665d5-313">You are also limited to:</span></span>

* <span data-ttu-id="665d5-314">256 parameters</span><span class="sxs-lookup"><span data-stu-id="665d5-314">256 parameters</span></span>
* <span data-ttu-id="665d5-315">256 variabelen</span><span class="sxs-lookup"><span data-stu-id="665d5-315">256 variables</span></span>
* <span data-ttu-id="665d5-316">800 bronnen (zoals aantal kopieën)</span><span class="sxs-lookup"><span data-stu-id="665d5-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="665d5-317">64 uitvoerwaarden</span><span class="sxs-lookup"><span data-stu-id="665d5-317">64 output values</span></span>
* <span data-ttu-id="665d5-318">24.576 tekens in een sjabloonexpressie</span><span class="sxs-lookup"><span data-stu-id="665d5-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="665d5-319">U kunt sommige limieten sjabloon met een geneste sjabloon overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="665d5-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="665d5-320">Zie voor meer informatie [gekoppelde sjablonen gebruiken bij het implementeren van Azure-resources](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="665d5-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="665d5-321">tooreduce hello nummer van de parameters en variabelen en uitvoer, kunt u verschillende waarden combineren in een object.</span><span class="sxs-lookup"><span data-stu-id="665d5-321">tooreduce hello number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="665d5-322">Zie voor meer informatie [objecten als parameters](resource-manager-objects-as-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="665d5-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="665d5-323">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="665d5-323">Next steps</span></span>
* <span data-ttu-id="665d5-324">tooview voltooid sjablonen voor verschillende soorten oplossingen, Zie Hallo [Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="665d5-324">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="665d5-325">Zie voor meer informatie over het Hallo-functies die u van binnen een sjabloon gebruiken kunt [Azure Resource Manager-sjabloonfuncties](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="665d5-325">For details about hello functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="665d5-326">toocombine meerdere sjablonen tijdens de implementatie, Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="665d5-326">toocombine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="665d5-327">Mogelijk moet u toouse resources die zijn opgeslagen in een andere resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="665d5-327">You may need toouse resources that exist within a different resource group.</span></span> <span data-ttu-id="665d5-328">Dit scenario is gebruikelijk dat wanneer u werkt met opslagaccounts of virtuele netwerken die worden gedeeld door meerdere resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="665d5-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="665d5-329">Zie voor meer informatie, Hallo [resourceId functie](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="665d5-329">For more information, see hello [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
