---
title: Structuur van Azure Resource Manager-sjabloon en syntaxis | Microsoft Docs
description: Beschrijft de structuur en eigenschappen van Azure Resource Manager-sjablonen met behulp van declaratieve JSON-syntaxis.
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
ms.openlocfilehash: dc9b64062d7f68c83aa090eec96744819a5ca423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="understand-the-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="e22b7-103">Overzicht van de structuur en de syntaxis van Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="e22b7-103">Understand the structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="e22b7-104">Dit onderwerp beschrijft de structuur van een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e22b7-104">This topic describes the structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="e22b7-105">Dit geeft de verschillende secties van een sjabloon en de eigenschappen die beschikbaar in deze secties zijn.</span><span class="sxs-lookup"><span data-stu-id="e22b7-105">It presents the different sections of a template and the properties that are available in those sections.</span></span> <span data-ttu-id="e22b7-106">De sjabloon bestaat uit JSON en uitdrukkingen die u gebruiken kunt om waarden voor uw implementatie samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="e22b7-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="e22b7-107">Zie voor een stapsgewijze zelfstudie over het maken van een sjabloon, [maken van uw eerste Azure Resource Manager-sjabloon](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="e22b7-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="e22b7-108">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="e22b7-108">Template format</span></span>
<span data-ttu-id="e22b7-109">In de meest eenvoudige structuur bevat een sjabloon voor de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="e22b7-109">In its simplest structure, a template contains the following elements:</span></span>

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

| <span data-ttu-id="e22b7-110">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="e22b7-110">Element name</span></span> | <span data-ttu-id="e22b7-111">Vereist</span><span class="sxs-lookup"><span data-stu-id="e22b7-111">Required</span></span> | <span data-ttu-id="e22b7-112">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e22b7-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e22b7-113">$schema</span><span class="sxs-lookup"><span data-stu-id="e22b7-113">$schema</span></span> |<span data-ttu-id="e22b7-114">Ja</span><span class="sxs-lookup"><span data-stu-id="e22b7-114">Yes</span></span> |<span data-ttu-id="e22b7-115">Locatie van het JSON-schema-bestand dat de versie van de taal van de sjabloon beschrijft.</span><span class="sxs-lookup"><span data-stu-id="e22b7-115">Location of the JSON schema file that describes the version of the template language.</span></span> <span data-ttu-id="e22b7-116">Gebruik de URL die wordt weergegeven in het voorgaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="e22b7-116">Use the URL shown in the preceding example.</span></span> |
| <span data-ttu-id="e22b7-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="e22b7-117">contentVersion</span></span> |<span data-ttu-id="e22b7-118">Ja</span><span class="sxs-lookup"><span data-stu-id="e22b7-118">Yes</span></span> |<span data-ttu-id="e22b7-119">De versie van de sjabloon (zoals 1.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="e22b7-119">Version of the template (such as 1.0.0.0).</span></span> <span data-ttu-id="e22b7-120">U kunt een waarde opgeven voor dit element.</span><span class="sxs-lookup"><span data-stu-id="e22b7-120">You can provide any value for this element.</span></span> <span data-ttu-id="e22b7-121">Bij het implementeren van resources met behulp van de sjabloon, kan deze waarde kan worden gebruikt om ervoor te zorgen dat de juiste sjabloon wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e22b7-121">When deploying resources using the template, this value can be used to make sure that the right template is being used.</span></span> |
| <span data-ttu-id="e22b7-122">Parameters</span><span class="sxs-lookup"><span data-stu-id="e22b7-122">parameters</span></span> |<span data-ttu-id="e22b7-123">Nee</span><span class="sxs-lookup"><span data-stu-id="e22b7-123">No</span></span> |<span data-ttu-id="e22b7-124">De waarden die beschikbaar zijn wanneer de implementatie wordt uitgevoerd voor het aanpassen van de resource-implementatie.</span><span class="sxs-lookup"><span data-stu-id="e22b7-124">Values that are provided when deployment is executed to customize resource deployment.</span></span> |
| <span data-ttu-id="e22b7-125">variabelen</span><span class="sxs-lookup"><span data-stu-id="e22b7-125">variables</span></span> |<span data-ttu-id="e22b7-126">Nee</span><span class="sxs-lookup"><span data-stu-id="e22b7-126">No</span></span> |<span data-ttu-id="e22b7-127">De waarden die worden gebruikt als JSON-fragmenten in de sjabloon voor sjabloontaalexpressies vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="e22b7-127">Values that are used as JSON fragments in the template to simplify template language expressions.</span></span> |
| <span data-ttu-id="e22b7-128">Resources</span><span class="sxs-lookup"><span data-stu-id="e22b7-128">resources</span></span> |<span data-ttu-id="e22b7-129">Ja</span><span class="sxs-lookup"><span data-stu-id="e22b7-129">Yes</span></span> |<span data-ttu-id="e22b7-130">Brontypen die worden geïmplementeerd of bijgewerkt in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e22b7-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="e22b7-131">uitvoer</span><span class="sxs-lookup"><span data-stu-id="e22b7-131">outputs</span></span> |<span data-ttu-id="e22b7-132">Nee</span><span class="sxs-lookup"><span data-stu-id="e22b7-132">No</span></span> |<span data-ttu-id="e22b7-133">De waarden die na de implementatie worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="e22b7-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="e22b7-134">Elk element bevat eigenschappen die u kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="e22b7-134">Each element contains properties you can set.</span></span> <span data-ttu-id="e22b7-135">Het volgende voorbeeld bevat de volledige syntaxis van een sjabloon:</span><span class="sxs-lookup"><span data-stu-id="e22b7-135">The following example contains the full syntax for a template:</span></span>

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
                "description": "<description-of-the parameter>" 
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

<span data-ttu-id="e22b7-136">We onderzoeken in de secties van de sjabloon in meer detail verderop in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="e22b7-136">We examine the sections of the template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="e22b7-137">Expressies en functies</span><span class="sxs-lookup"><span data-stu-id="e22b7-137">Expressions and functions</span></span>
<span data-ttu-id="e22b7-138">De syntaxis van de basis van de sjabloon is JSON.</span><span class="sxs-lookup"><span data-stu-id="e22b7-138">The basic syntax of the template is JSON.</span></span> <span data-ttu-id="e22b7-139">Expressies en functies echter uitbreiden de JSON-waarden die beschikbaar zijn in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e22b7-139">However, expressions and functions extend the JSON values available within the template.</span></span>  <span data-ttu-id="e22b7-140">Expressies zijn geschreven in JSON-letterlijke waarvan de eerste en laatste tekens zijn de vierkante haken: `[` en `]`respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="e22b7-140">Expressions are written within JSON string literals whose first and last characters are the brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="e22b7-141">De waarde van de expressie wordt geëvalueerd wanneer de sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e22b7-141">The value of the expression is evaluated when the template is deployed.</span></span> <span data-ttu-id="e22b7-142">Hoewel geschreven als een letterlijke tekenreeks, zijn het resultaat van evaluatie van de expressie van een ander JSON-type, zoals een matrix of een geheel getal, afhankelijk van de werkelijke expressie.</span><span class="sxs-lookup"><span data-stu-id="e22b7-142">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array or integer, depending on the actual expression.</span></span>  <span data-ttu-id="e22b7-143">Een letterlijke tekenreeks beginnen met een haakje hebben `[`, maar dit wordt geïnterpreteerd als een expressie niet, Voeg een extra haakje voor het starten van de tekenreeks met `[[`.</span><span class="sxs-lookup"><span data-stu-id="e22b7-143">To have a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket to start the string with `[[`.</span></span>

<span data-ttu-id="e22b7-144">Normaal gesproken u expressies gebruiken met functies bewerkingen voor het configureren van de implementatie uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="e22b7-144">Typically, you use expressions with functions to perform operations for configuring the deployment.</span></span> <span data-ttu-id="e22b7-145">Net zoals in JavaScript-functieaanroepen die zijn opgemaakt als `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="e22b7-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="e22b7-146">U verwijzen naar eigenschappen met behulp van de punt en [index] operators.</span><span class="sxs-lookup"><span data-stu-id="e22b7-146">You reference properties by using the dot and [index] operators.</span></span>

<span data-ttu-id="e22b7-147">Het volgende voorbeeld ziet u hoe u verschillende functies gebruikt bij het maken van de waarden:</span><span class="sxs-lookup"><span data-stu-id="e22b7-147">The following example shows how to use several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="e22b7-148">Zie voor een volledige lijst van sjabloonfuncties [Azure Resource Manager-sjabloonfuncties](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="e22b7-148">For the full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="e22b7-149">Parameters</span><span class="sxs-lookup"><span data-stu-id="e22b7-149">Parameters</span></span>
<span data-ttu-id="e22b7-150">U opgeven welke waarden u invoeren kunt bij het implementeren van de resources in het gedeelte parameters van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e22b7-150">In the parameters section of the template, you specify which values you can input when deploying the resources.</span></span> <span data-ttu-id="e22b7-151">De parameterwaarden van deze kunnen u de implementatie aanpassen door het verstrekken van waarden die zijn aangepast voor een bepaalde omgeving (zoals ontwikkelen, testen en productie).</span><span class="sxs-lookup"><span data-stu-id="e22b7-151">These parameter values enable you to customize the deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="e22b7-152">U hoeft niet te bieden parameters in de sjabloon, maar zonder parameters uw sjabloon altijd dezelfde resources met dezelfde namen, locaties en eigenschappen zou implementeren.</span><span class="sxs-lookup"><span data-stu-id="e22b7-152">You do not have to provide parameters in your template, but without parameters your template would always deploy the same resources with the same names, locations, and properties.</span></span>

<span data-ttu-id="e22b7-153">U definieert parameters met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="e22b7-153">You define parameters with the following structure:</span></span>

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
            "description": "<description-of-the parameter>" 
        }
    }
}
```

| <span data-ttu-id="e22b7-154">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="e22b7-154">Element name</span></span> | <span data-ttu-id="e22b7-155">Vereist</span><span class="sxs-lookup"><span data-stu-id="e22b7-155">Required</span></span> | <span data-ttu-id="e22b7-156">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e22b7-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e22b7-157">parameterName</span><span class="sxs-lookup"><span data-stu-id="e22b7-157">parameterName</span></span> |<span data-ttu-id="e22b7-158">Ja</span><span class="sxs-lookup"><span data-stu-id="e22b7-158">Yes</span></span> |<span data-ttu-id="e22b7-159">De naam van de parameter.</span><span class="sxs-lookup"><span data-stu-id="e22b7-159">Name of the parameter.</span></span> <span data-ttu-id="e22b7-160">Moet een geldige JavaScript-id.</span><span class="sxs-lookup"><span data-stu-id="e22b7-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="e22b7-161">type</span><span class="sxs-lookup"><span data-stu-id="e22b7-161">type</span></span> |<span data-ttu-id="e22b7-162">Ja</span><span class="sxs-lookup"><span data-stu-id="e22b7-162">Yes</span></span> |<span data-ttu-id="e22b7-163">Type van de waarde van parameter.</span><span class="sxs-lookup"><span data-stu-id="e22b7-163">Type of the parameter value.</span></span> <span data-ttu-id="e22b7-164">Zie de lijst met toegestane typen na deze tabel.</span><span class="sxs-lookup"><span data-stu-id="e22b7-164">See the list of allowed types after this table.</span></span> |
| <span data-ttu-id="e22b7-165">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="e22b7-165">defaultValue</span></span> |<span data-ttu-id="e22b7-166">Nee</span><span class="sxs-lookup"><span data-stu-id="e22b7-166">No</span></span> |<span data-ttu-id="e22b7-167">De standaardwaarde voor de parameter als u geen waarde is opgegeven voor de parameter.</span><span class="sxs-lookup"><span data-stu-id="e22b7-167">Default value for the parameter, if no value is provided for the parameter.</span></span> |
| <span data-ttu-id="e22b7-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="e22b7-168">allowedValues</span></span> |<span data-ttu-id="e22b7-169">Nee</span><span class="sxs-lookup"><span data-stu-id="e22b7-169">No</span></span> |<span data-ttu-id="e22b7-170">Matrix van toegestane waarden voor de parameter om ervoor te zorgen dat de juiste waarde is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e22b7-170">Array of allowed values for the parameter to make sure that the right value is provided.</span></span> |
| <span data-ttu-id="e22b7-171">MinValue</span><span class="sxs-lookup"><span data-stu-id="e22b7-171">minValue</span></span> |<span data-ttu-id="e22b7-172">Nee</span><span class="sxs-lookup"><span data-stu-id="e22b7-172">No</span></span> |<span data-ttu-id="e22b7-173">De minimumwaarde voor de parameters van het type int, deze waarde is liggen.</span><span class="sxs-lookup"><span data-stu-id="e22b7-173">The minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="e22b7-174">MaxValue</span><span class="sxs-lookup"><span data-stu-id="e22b7-174">maxValue</span></span> |<span data-ttu-id="e22b7-175">Nee</span><span class="sxs-lookup"><span data-stu-id="e22b7-175">No</span></span> |<span data-ttu-id="e22b7-176">De maximale waarde voor de parameters van het type int, deze waarde is liggen.</span><span class="sxs-lookup"><span data-stu-id="e22b7-176">The maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="e22b7-177">minLength</span><span class="sxs-lookup"><span data-stu-id="e22b7-177">minLength</span></span> |<span data-ttu-id="e22b7-178">Nee</span><span class="sxs-lookup"><span data-stu-id="e22b7-178">No</span></span> |<span data-ttu-id="e22b7-179">De minimale lengte voor string, secureString en array typeparameters deze waarde is liggen.</span><span class="sxs-lookup"><span data-stu-id="e22b7-179">The minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="e22b7-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="e22b7-180">maxLength</span></span> |<span data-ttu-id="e22b7-181">Nee</span><span class="sxs-lookup"><span data-stu-id="e22b7-181">No</span></span> |<span data-ttu-id="e22b7-182">De maximale lengte voor string, secureString en array typeparameters deze waarde is liggen.</span><span class="sxs-lookup"><span data-stu-id="e22b7-182">The maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="e22b7-183">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e22b7-183">description</span></span> |<span data-ttu-id="e22b7-184">Nee</span><span class="sxs-lookup"><span data-stu-id="e22b7-184">No</span></span> |<span data-ttu-id="e22b7-185">Beschrijving van de parameter die wordt weergegeven voor gebruikers via de portal.</span><span class="sxs-lookup"><span data-stu-id="e22b7-185">Description of the parameter that is displayed to users through the portal.</span></span> |

<span data-ttu-id="e22b7-186">De toegestane typen en waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="e22b7-186">The allowed types and values are:</span></span>

* <span data-ttu-id="e22b7-187">**tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="e22b7-187">**string**</span></span>
* <span data-ttu-id="e22b7-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="e22b7-188">**secureString**</span></span>
* <span data-ttu-id="e22b7-189">**int**</span><span class="sxs-lookup"><span data-stu-id="e22b7-189">**int**</span></span>
* <span data-ttu-id="e22b7-190">**BOOL**</span><span class="sxs-lookup"><span data-stu-id="e22b7-190">**bool**</span></span>
* <span data-ttu-id="e22b7-191">**object**</span><span class="sxs-lookup"><span data-stu-id="e22b7-191">**object**</span></span> 
* <span data-ttu-id="e22b7-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="e22b7-192">**secureObject**</span></span>
* <span data-ttu-id="e22b7-193">**matrix**</span><span class="sxs-lookup"><span data-stu-id="e22b7-193">**array**</span></span>

<span data-ttu-id="e22b7-194">Als u een parameter als een optionele, bieden een defaultValue (kunnen geen lege tekenreeks zijn).</span><span class="sxs-lookup"><span data-stu-id="e22b7-194">To specify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="e22b7-195">Als u een parameternaam in de sjabloon die overeenkomt met een parameter in de opdracht om de sjabloon te implementeren opgeeft, is het mogelijke verwarring over de waarden die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="e22b7-195">If you specify a parameter name in your template that matches a parameter in the command to deploy the template, there is potential ambiguity about the values you provide.</span></span> <span data-ttu-id="e22b7-196">Resource Manager wordt deze verwarring opgelost doordat de postfix **FromTemplate** voor de sjabloonparameter.</span><span class="sxs-lookup"><span data-stu-id="e22b7-196">Resource Manager resolves this confusion by adding the postfix **FromTemplate** to the template parameter.</span></span> <span data-ttu-id="e22b7-197">Bijvoorbeeld, als u een parameter genaamd opnemen **ResourceGroupName** in uw sjabloon een conflict met de **ResourceGroupName** parameter in de [New-AzureRmResourceGroupDeployment ](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e22b7-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="e22b7-198">Tijdens de implementatie, moet u een waarde opgeven voor **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="e22b7-198">During deployment, you are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="e22b7-199">In het algemeen moet u deze verwarring niet door de naam geen parameters met dezelfde naam als parameters die worden gebruikt voor implementatiebewerkingen.</span><span class="sxs-lookup"><span data-stu-id="e22b7-199">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="e22b7-200">Alle wachtwoorden, sleutels en andere geheime informatie moeten gebruiken de **secureString** type.</span><span class="sxs-lookup"><span data-stu-id="e22b7-200">All passwords, keys, and other secrets should use the **secureString** type.</span></span> <span data-ttu-id="e22b7-201">Als u gevoelige gegevens in een JSON-object doorgeven, gebruikt u de **secureObject** type.</span><span class="sxs-lookup"><span data-stu-id="e22b7-201">If you pass sensitive data in a JSON object, use the **secureObject** type.</span></span> <span data-ttu-id="e22b7-202">Sjabloonparameters met secureString of secureObject typen kunnen niet worden gelezen na de implementatie van de resource.</span><span class="sxs-lookup"><span data-stu-id="e22b7-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="e22b7-203">De volgende vermelding in de implementatiegeschiedenis van de ziet u bijvoorbeeld de waarde voor een tekenreeks en object maar niet voor secureString en secureObject.</span><span class="sxs-lookup"><span data-stu-id="e22b7-203">For example, the following entry in the deployment history shows the value for a string and object but not for secureString and secureObject.</span></span>
>
> ![waarden van de implementatie weergeven](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="e22b7-205">Het volgende voorbeeld ziet u hoe parameters definiëren:</span><span class="sxs-lookup"><span data-stu-id="e22b7-205">The following example shows how to define parameters:</span></span>

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

<span data-ttu-id="e22b7-206">Voor het invoeren van de parameterwaarden die tijdens de implementatie, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e22b7-206">For how to input the parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="e22b7-207">Variabelen</span><span class="sxs-lookup"><span data-stu-id="e22b7-207">Variables</span></span>
<span data-ttu-id="e22b7-208">In het gedeelte variabelen kunt u waarden die kunnen worden gebruikt in uw sjabloon opstellen.</span><span class="sxs-lookup"><span data-stu-id="e22b7-208">In the variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="e22b7-209">U hoeft geen variabelen definiëren, maar ze vaak uw sjabloon vereenvoudigen doordat complexe expressies.</span><span class="sxs-lookup"><span data-stu-id="e22b7-209">You do not need to define variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="e22b7-210">U definieert variabelen met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="e22b7-210">You define variables with the following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="e22b7-211">Het volgende voorbeeld ziet u hoe een variabele die is samengesteld uit twee parameterwaarden definiëren:</span><span class="sxs-lookup"><span data-stu-id="e22b7-211">The following example shows how to define a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="e22b7-212">Het volgende voorbeeld ziet u een variabele die is complex type JSON en variabelen die zijn samengesteld uit andere variabelen:</span><span class="sxs-lookup"><span data-stu-id="e22b7-212">The next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

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

## <a name="resources"></a><span data-ttu-id="e22b7-213">Resources</span><span class="sxs-lookup"><span data-stu-id="e22b7-213">Resources</span></span>
<span data-ttu-id="e22b7-214">In de bronnensectie definieert u de resources die worden geïmplementeerd of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e22b7-214">In the resources section, you define the resources that are deployed or updated.</span></span> <span data-ttu-id="e22b7-215">Deze sectie kunt krijgen ingewikkeld omdat de typen die u implementeert de juiste waarden opgeven dat u begrijpt.</span><span class="sxs-lookup"><span data-stu-id="e22b7-215">This section can get complicated because you must understand the types you are deploying to provide the right values.</span></span> <span data-ttu-id="e22b7-216">Zie voor de resource-specifieke waarden (apiVersion, type en eigenschappen) die u nodig hebt om in te stellen [resources in Azure Resource Manager-sjablonen definiëren](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="e22b7-216">For the resource-specific values (apiVersion, type, and properties) that you need to set, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="e22b7-217">U definieert resources met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="e22b7-217">You define resources with the following structure:</span></span>

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

| <span data-ttu-id="e22b7-218">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="e22b7-218">Element name</span></span> | <span data-ttu-id="e22b7-219">Vereist</span><span class="sxs-lookup"><span data-stu-id="e22b7-219">Required</span></span> | <span data-ttu-id="e22b7-220">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e22b7-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e22b7-221">Voorwaarde</span><span class="sxs-lookup"><span data-stu-id="e22b7-221">condition</span></span> | <span data-ttu-id="e22b7-222">Nee</span><span class="sxs-lookup"><span data-stu-id="e22b7-222">No</span></span> | <span data-ttu-id="e22b7-223">Booleaanse waarde die aangeeft of de resource is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e22b7-223">Boolean value that indicates whether the resource is deployed.</span></span> |
| <span data-ttu-id="e22b7-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e22b7-224">apiVersion</span></span> |<span data-ttu-id="e22b7-225">Ja</span><span class="sxs-lookup"><span data-stu-id="e22b7-225">Yes</span></span> |<span data-ttu-id="e22b7-226">De versie van de REST-API gebruiken voor het maken van de resource.</span><span class="sxs-lookup"><span data-stu-id="e22b7-226">Version of the REST API to use for creating the resource.</span></span> |
| <span data-ttu-id="e22b7-227">type</span><span class="sxs-lookup"><span data-stu-id="e22b7-227">type</span></span> |<span data-ttu-id="e22b7-228">Ja</span><span class="sxs-lookup"><span data-stu-id="e22b7-228">Yes</span></span> |<span data-ttu-id="e22b7-229">Type van de resource.</span><span class="sxs-lookup"><span data-stu-id="e22b7-229">Type of the resource.</span></span> <span data-ttu-id="e22b7-230">Deze waarde is een combinatie van de naamruimte van de resourceprovider en het resourcetype (zoals **Microsoft.Storage/storageAccounts**).</span><span class="sxs-lookup"><span data-stu-id="e22b7-230">This value is a combination of the namespace of the resource provider and the resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="e22b7-231">naam</span><span class="sxs-lookup"><span data-stu-id="e22b7-231">name</span></span> |<span data-ttu-id="e22b7-232">Ja</span><span class="sxs-lookup"><span data-stu-id="e22b7-232">Yes</span></span> |<span data-ttu-id="e22b7-233">De naam van de resource.</span><span class="sxs-lookup"><span data-stu-id="e22b7-233">Name of the resource.</span></span> <span data-ttu-id="e22b7-234">De naam moet URI onderdeel beperkingen gedefinieerd in RFC3986 volgen.</span><span class="sxs-lookup"><span data-stu-id="e22b7-234">The name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="e22b7-235">Bovendien Azure-services die beschikbaar om te valideren buiten partijen de naam om te controleren of deze de naam van de resource is niet een poging tot een andere identiteit vervalsen.</span><span class="sxs-lookup"><span data-stu-id="e22b7-235">In addition, Azure services that expose the resource name to outside parties validate the name to make sure it is not an attempt to spoof another identity.</span></span> |
| <span data-ttu-id="e22b7-236">location</span><span class="sxs-lookup"><span data-stu-id="e22b7-236">location</span></span> |<span data-ttu-id="e22b7-237">Varieert</span><span class="sxs-lookup"><span data-stu-id="e22b7-237">Varies</span></span> |<span data-ttu-id="e22b7-238">Ondersteunde geografische locaties van de opgegeven bron.</span><span class="sxs-lookup"><span data-stu-id="e22b7-238">Supported geo-locations of the provided resource.</span></span> <span data-ttu-id="e22b7-239">U kunt een van de beschikbare locaties selecteren, maar meestal is het verstandig om te selecteren die dicht bij uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e22b7-239">You can select any of the available locations, but typically it makes sense to pick one that is close to your users.</span></span> <span data-ttu-id="e22b7-240">Meestal is het ook handig om resources die in dezelfde regio met elkaar communiceren.</span><span class="sxs-lookup"><span data-stu-id="e22b7-240">Usually, it also makes sense to place resources that interact with each other in the same region.</span></span> <span data-ttu-id="e22b7-241">De meeste brontypen die een locatie vereist, maar sommige typen (zoals een roltoewijzing) hoeven niet een locatie.</span><span class="sxs-lookup"><span data-stu-id="e22b7-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="e22b7-242">Zie [Resourcelocatie instellen in Azure Resource Manager-sjablonen](resource-manager-template-location.md).</span><span class="sxs-lookup"><span data-stu-id="e22b7-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="e22b7-243">tags</span><span class="sxs-lookup"><span data-stu-id="e22b7-243">tags</span></span> |<span data-ttu-id="e22b7-244">Nee</span><span class="sxs-lookup"><span data-stu-id="e22b7-244">No</span></span> |<span data-ttu-id="e22b7-245">Labels die gekoppeld aan de resource zijn.</span><span class="sxs-lookup"><span data-stu-id="e22b7-245">Tags that are associated with the resource.</span></span> <span data-ttu-id="e22b7-246">Zie [resources in Azure Resource Manager-sjablonen taggen](resource-manager-template-tags.md).</span><span class="sxs-lookup"><span data-stu-id="e22b7-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="e22b7-247">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="e22b7-247">comments</span></span> |<span data-ttu-id="e22b7-248">Nee</span><span class="sxs-lookup"><span data-stu-id="e22b7-248">No</span></span> |<span data-ttu-id="e22b7-249">De notities voor de resources in uw sjabloon documenteren</span><span class="sxs-lookup"><span data-stu-id="e22b7-249">Your notes for documenting the resources in your template</span></span> |
| <span data-ttu-id="e22b7-250">Kopiëren</span><span class="sxs-lookup"><span data-stu-id="e22b7-250">copy</span></span> |<span data-ttu-id="e22b7-251">Nee</span><span class="sxs-lookup"><span data-stu-id="e22b7-251">No</span></span> |<span data-ttu-id="e22b7-252">Als meer dan één exemplaar is vereist, het aantal resources om te maken.</span><span class="sxs-lookup"><span data-stu-id="e22b7-252">If more than one instance is needed, the number of resources to create.</span></span> <span data-ttu-id="e22b7-253">Er is de standaardmodus voor parallelle.</span><span class="sxs-lookup"><span data-stu-id="e22b7-253">The default mode is parallel.</span></span> <span data-ttu-id="e22b7-254">Seriële modus wanneer u niet dat alle wilt of de resources te implementeren op hetzelfde moment opgeven.</span><span class="sxs-lookup"><span data-stu-id="e22b7-254">Specify serial mode when you do not want all or the resources to deploy at the same time.</span></span> <span data-ttu-id="e22b7-255">Zie voor meer informatie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="e22b7-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="e22b7-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="e22b7-256">dependsOn</span></span> |<span data-ttu-id="e22b7-257">Nee</span><span class="sxs-lookup"><span data-stu-id="e22b7-257">No</span></span> |<span data-ttu-id="e22b7-258">Resources die moeten worden geïmplementeerd voordat u deze bron wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e22b7-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="e22b7-259">Resource Manager evalueert de afhankelijkheden tussen resources en ze worden geïmplementeerd in de juiste volgorde.</span><span class="sxs-lookup"><span data-stu-id="e22b7-259">Resource Manager evaluates the dependencies between resources and deploys them in the correct order.</span></span> <span data-ttu-id="e22b7-260">Wanneer u resources zijn niet afhankelijk van elkaar, worden ze geïmplementeerd parallel.</span><span class="sxs-lookup"><span data-stu-id="e22b7-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="e22b7-261">De waarde kan een door komma's gescheiden lijst van een resource zijn namen of unieke id's voor een resource.</span><span class="sxs-lookup"><span data-stu-id="e22b7-261">The value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="e22b7-262">Alleen de lijst van resources die zijn geïmplementeerd in deze sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e22b7-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="e22b7-263">Bronnen die niet in deze sjabloon zijn gedefinieerd, moeten al bestaan.</span><span class="sxs-lookup"><span data-stu-id="e22b7-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="e22b7-264">Vermijd toe te voegen onnodige afhankelijkheden als ze kunnen uw implementatie vertragen en circulaire afhankelijkheden maken.</span><span class="sxs-lookup"><span data-stu-id="e22b7-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="e22b7-265">Zie voor instructies over de afhankelijkheden van de instelling [afhankelijkheden definiëren in Azure Resource Manager-sjablonen](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="e22b7-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="e22b7-266">properties</span><span class="sxs-lookup"><span data-stu-id="e22b7-266">properties</span></span> |<span data-ttu-id="e22b7-267">Nee</span><span class="sxs-lookup"><span data-stu-id="e22b7-267">No</span></span> |<span data-ttu-id="e22b7-268">Resource-specifieke configuratie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="e22b7-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="e22b7-269">De waarden voor de eigenschappen zijn hetzelfde als de waarden die u in de aanvraagtekst voor de REST-API-bewerking (PUT-methode opgeeft) om de resource te maken.</span><span class="sxs-lookup"><span data-stu-id="e22b7-269">The values for the properties are the same as the values you provide in the request body for the REST API operation (PUT method) to create the resource.</span></span> <span data-ttu-id="e22b7-270">U kunt ook een matrix kopiëren voor het maken van meerdere exemplaren van een eigenschap opgeven.</span><span class="sxs-lookup"><span data-stu-id="e22b7-270">You can also specify a copy array to create multiple instances of a property.</span></span> <span data-ttu-id="e22b7-271">Zie voor meer informatie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="e22b7-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="e22b7-272">Resources</span><span class="sxs-lookup"><span data-stu-id="e22b7-272">resources</span></span> |<span data-ttu-id="e22b7-273">Nee</span><span class="sxs-lookup"><span data-stu-id="e22b7-273">No</span></span> |<span data-ttu-id="e22b7-274">Onderliggende resources die afhankelijk zijn van de bron wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="e22b7-274">Child resources that depend on the resource being defined.</span></span> <span data-ttu-id="e22b7-275">Geef alleen brontypen die worden toegestaan door het schema van de bovenliggende resource.</span><span class="sxs-lookup"><span data-stu-id="e22b7-275">Only provide resource types that are permitted by the schema of the parent resource.</span></span> <span data-ttu-id="e22b7-276">Het volledig gekwalificeerde type van de onderliggende resource bevat het type van de bovenliggende resource, zoals **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="e22b7-276">The fully qualified type of the child resource includes the parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="e22b7-277">Afhankelijkheid van de bovenliggende resource niet geïmpliceerd.</span><span class="sxs-lookup"><span data-stu-id="e22b7-277">Dependency on the parent resource is not implied.</span></span> <span data-ttu-id="e22b7-278">U moet deze afhankelijkheid expliciet definiëren.</span><span class="sxs-lookup"><span data-stu-id="e22b7-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="e22b7-279">De sectie resources bevat een matrix van de resources te implementeren.</span><span class="sxs-lookup"><span data-stu-id="e22b7-279">The resources section contains an array of the resources to deploy.</span></span> <span data-ttu-id="e22b7-280">U kunt ook een matrix van onderliggende resources binnen elke resource definiëren.</span><span class="sxs-lookup"><span data-stu-id="e22b7-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="e22b7-281">Het gedeelte van uw resources kan daarom een structuur zoals hebben:</span><span class="sxs-lookup"><span data-stu-id="e22b7-281">Therefore, your resources section could have a structure like:</span></span>

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

<span data-ttu-id="e22b7-282">Zie voor meer informatie over het definiëren van de onderliggende resources [naam en type voor onderliggende resource in het Resource Manager-sjabloon instellen](resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="e22b7-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="e22b7-283">De **voorwaarde** element geeft aan of de resource is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e22b7-283">The **condition** element specifies whether the resource is deployed.</span></span> <span data-ttu-id="e22b7-284">De waarde voor dit element wordt omgezet in true of false.</span><span class="sxs-lookup"><span data-stu-id="e22b7-284">The value for this element resolves to true or false.</span></span> <span data-ttu-id="e22b7-285">Bijvoorbeeld: als u wilt opgeven of een nieuw opslagaccount wordt geïmplementeerd, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e22b7-285">For example, to specify whether a new storage account is deployed, use:</span></span>

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

<span data-ttu-id="e22b7-286">Zie voor een voorbeeld van het gebruik van een nieuwe of bestaande resourcegroep [nieuwe of bestaande voorwaarde sjabloon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="e22b7-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="e22b7-287">Als u wilt opgeven of een virtuele machine wordt geïmplementeerd met een wachtwoord of SSH-sleutel, definieert u twee versies van de virtuele machine in de sjabloon en het gebruik **voorwaarde** te onderscheiden van informatie over het gebruik.</span><span class="sxs-lookup"><span data-stu-id="e22b7-287">To specify whether a virtual machine is deployed with a password or SSH key, define two versions of the virtual machine in your template and use **condition** to differentiate usage.</span></span> <span data-ttu-id="e22b7-288">Hiermee geeft u een parameter die welke scenario aangeeft te implementeren.</span><span class="sxs-lookup"><span data-stu-id="e22b7-288">Pass a parameter that specifies which scenario to deploy.</span></span>

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

<span data-ttu-id="e22b7-289">Zie voor een voorbeeld van het gebruik van een wachtwoord of SSH-sleutel voor het implementeren van virtuele machine [gebruikersnaam of SSH voorwaarde sjabloon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="e22b7-289">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="e22b7-290">uitvoer</span><span class="sxs-lookup"><span data-stu-id="e22b7-290">Outputs</span></span>
<span data-ttu-id="e22b7-291">In de sectie uitvoer geeft u de waarden die worden geretourneerd van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="e22b7-291">In the Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="e22b7-292">U kan bijvoorbeeld de URI voor toegang tot een geïmplementeerde resource geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="e22b7-292">For example, you could return the URI to access a deployed resource.</span></span>

<span data-ttu-id="e22b7-293">Het volgende voorbeeld ziet u de structuur van de definitie van een uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e22b7-293">The following example shows the structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="e22b7-294">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="e22b7-294">Element name</span></span> | <span data-ttu-id="e22b7-295">Vereist</span><span class="sxs-lookup"><span data-stu-id="e22b7-295">Required</span></span> | <span data-ttu-id="e22b7-296">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e22b7-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e22b7-297">outputName</span><span class="sxs-lookup"><span data-stu-id="e22b7-297">outputName</span></span> |<span data-ttu-id="e22b7-298">Ja</span><span class="sxs-lookup"><span data-stu-id="e22b7-298">Yes</span></span> |<span data-ttu-id="e22b7-299">De naam van de uitvoerwaarde.</span><span class="sxs-lookup"><span data-stu-id="e22b7-299">Name of the output value.</span></span> <span data-ttu-id="e22b7-300">Moet een geldige JavaScript-id.</span><span class="sxs-lookup"><span data-stu-id="e22b7-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="e22b7-301">type</span><span class="sxs-lookup"><span data-stu-id="e22b7-301">type</span></span> |<span data-ttu-id="e22b7-302">Ja</span><span class="sxs-lookup"><span data-stu-id="e22b7-302">Yes</span></span> |<span data-ttu-id="e22b7-303">Type van de uitvoerwaarde.</span><span class="sxs-lookup"><span data-stu-id="e22b7-303">Type of the output value.</span></span> <span data-ttu-id="e22b7-304">Uitvoerwaarden ondersteuning voor dezelfde typen als sjabloon invoerparameters.</span><span class="sxs-lookup"><span data-stu-id="e22b7-304">Output values support the same types as template input parameters.</span></span> |
| <span data-ttu-id="e22b7-305">waarde</span><span class="sxs-lookup"><span data-stu-id="e22b7-305">value</span></span> |<span data-ttu-id="e22b7-306">Ja</span><span class="sxs-lookup"><span data-stu-id="e22b7-306">Yes</span></span> |<span data-ttu-id="e22b7-307">De sjabloontaalexpressie dat wordt geëvalueerd en geretourneerd als de waarde voor uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e22b7-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="e22b7-308">Het volgende voorbeeld ziet een waarde die wordt geretourneerd in de sectie uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e22b7-308">The following example shows a value that is returned in the Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="e22b7-309">Zie voor meer informatie over het werken met uitvoer [delen status in Azure Resource Manager-sjablonen](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="e22b7-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="e22b7-310">Limieten voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="e22b7-310">Template limits</span></span>

<span data-ttu-id="e22b7-311">Beperkt de omvang van uw sjabloon 1 MB en elk parameterbestand 64 kB.</span><span class="sxs-lookup"><span data-stu-id="e22b7-311">Limit the size of your template to 1 MB, and each parameter file to 64 KB.</span></span> <span data-ttu-id="e22b7-312">De limiet van 1 MB geldt voor de definitieve status van de sjabloon nadat deze is uitgebreid met iteratieve resourcedefinities en waarden voor parameters en variabelen.</span><span class="sxs-lookup"><span data-stu-id="e22b7-312">The 1-MB limit applies to the final state of the template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="e22b7-313">Ook bent u beperkt tot:</span><span class="sxs-lookup"><span data-stu-id="e22b7-313">You are also limited to:</span></span>

* <span data-ttu-id="e22b7-314">256 parameters</span><span class="sxs-lookup"><span data-stu-id="e22b7-314">256 parameters</span></span>
* <span data-ttu-id="e22b7-315">256 variabelen</span><span class="sxs-lookup"><span data-stu-id="e22b7-315">256 variables</span></span>
* <span data-ttu-id="e22b7-316">800 bronnen (zoals aantal kopieën)</span><span class="sxs-lookup"><span data-stu-id="e22b7-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="e22b7-317">64 uitvoerwaarden</span><span class="sxs-lookup"><span data-stu-id="e22b7-317">64 output values</span></span>
* <span data-ttu-id="e22b7-318">24.576 tekens in een sjabloonexpressie</span><span class="sxs-lookup"><span data-stu-id="e22b7-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="e22b7-319">U kunt sommige limieten sjabloon met een geneste sjabloon overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="e22b7-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="e22b7-320">Zie voor meer informatie [gekoppelde sjablonen gebruiken bij het implementeren van Azure-resources](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e22b7-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="e22b7-321">Als u het aantal parameters en variabelen en uitvoer, kunt u verschillende waarden combineren in een object.</span><span class="sxs-lookup"><span data-stu-id="e22b7-321">To reduce the number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="e22b7-322">Zie voor meer informatie [objecten als parameters](resource-manager-objects-as-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="e22b7-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e22b7-323">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e22b7-323">Next steps</span></span>
* <span data-ttu-id="e22b7-324">Zie de [Azure-snelstartsjablonen](https://azure.microsoft.com/documentation/templates/) voor volledige sjablonen voor verschillende soorten oplossingen.</span><span class="sxs-lookup"><span data-stu-id="e22b7-324">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="e22b7-325">Zie voor meer informatie over de functies die u van binnen een sjabloon gebruiken kunt [Azure Resource Manager-sjabloonfuncties](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="e22b7-325">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="e22b7-326">Als u wilt combineren meerdere sjablonen tijdens de implementatie, Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e22b7-326">To combine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="e22b7-327">Wellicht moet u bronnen gebruiken die zijn opgeslagen in een andere resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e22b7-327">You may need to use resources that exist within a different resource group.</span></span> <span data-ttu-id="e22b7-328">Dit scenario is gebruikelijk dat wanneer u werkt met opslagaccounts of virtuele netwerken die worden gedeeld door meerdere resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="e22b7-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="e22b7-329">Zie voor meer informatie de [resourceId functie](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="e22b7-329">For more information, see the [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
