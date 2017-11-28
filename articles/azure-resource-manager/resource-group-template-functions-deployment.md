---
title: aaaAzure Resource Manager-sjabloonfuncties - implementatie | Microsoft Docs
description: Hierin wordt beschreven Hallo functies toouse in een Azure Resource Manager sjabloon tooretrieve implementatie-informatie.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="76e97-103">Implementatie-functies voor Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="76e97-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="76e97-104">Resource Manager biedt Hallo volgende fungeert voor het ophalen van waarden in de secties van de sjabloon Hallo en verwante toohello implementatie waarden:</span><span class="sxs-lookup"><span data-stu-id="76e97-104">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="76e97-105">implementatie</span><span class="sxs-lookup"><span data-stu-id="76e97-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="76e97-106">parameters</span><span class="sxs-lookup"><span data-stu-id="76e97-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="76e97-107">variabelen</span><span class="sxs-lookup"><span data-stu-id="76e97-107">variables</span></span>](#variables)

<span data-ttu-id="76e97-108">tooget waarden van resources, resourcegroepen of abonnementen, Zie [Resource functies](resource-group-template-functions-resource.md).</span><span class="sxs-lookup"><span data-stu-id="76e97-108">tooget values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="76e97-109">implementatie</span><span class="sxs-lookup"><span data-stu-id="76e97-109">deployment</span></span>
`deployment()`

<span data-ttu-id="76e97-110">Retourneert informatie over de huidige implementatiebewerking Hallo.</span><span class="sxs-lookup"><span data-stu-id="76e97-110">Returns information about hello current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="76e97-111">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="76e97-111">Return value</span></span>

<span data-ttu-id="76e97-112">Deze functie retourneert Hallo-object dat wordt doorgegeven tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="76e97-112">This function returns hello object that is passed during deployment.</span></span> <span data-ttu-id="76e97-113">Hallo-eigenschappen in object geretourneerd Hallo verschillen op basis van of hello implementatieobject is doorgegeven als een koppeling of als een in-line-object.</span><span class="sxs-lookup"><span data-stu-id="76e97-113">hello properties in hello returned object differ based on whether hello deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="76e97-114">Wanneer Hallo implementatieobject wordt doorgegeven in de regel, zoals bij gebruik van Hallo **- sjabloonbestand** parameter in Azure PowerShell toopoint tooa lokaal bestand geretourneerd Hallo-object heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="76e97-114">When hello deployment object is passed in-line, such as when using hello **-TemplateFile** parameter in Azure PowerShell toopoint tooa local file, hello returned object has hello following format:</span></span>

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

<span data-ttu-id="76e97-115">Wanneer Hallo-object doorgegeven als een koppeling, zoals wanneer met behulp van Hallo **- TemplateUri** parameter toopoint tooa extern object Hallo-object wordt geretourneerd als Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="76e97-115">When hello object is passed as a link, such as when using hello **-TemplateUri** parameter toopoint tooa remote object, hello object is returned in hello following format:</span></span> 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a><span data-ttu-id="76e97-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="76e97-116">Remarks</span></span>

<span data-ttu-id="76e97-117">U kunt deployment() toolink tooanother sjabloon op basis van het Hallo-URI van Hallo bovenliggende sjabloon gebruiken.</span><span class="sxs-lookup"><span data-stu-id="76e97-117">You can use deployment() toolink tooanother template based on hello URI of hello parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="76e97-118">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="76e97-118">Example</span></span>

<span data-ttu-id="76e97-119">Hallo wordt volgende voorbeeld Hallo implementatieobject:</span><span class="sxs-lookup"><span data-stu-id="76e97-119">hello following example returns hello deployment object:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="76e97-120">Hallo retourneert voorgaande voorbeeld Hallo na-object:</span><span class="sxs-lookup"><span data-stu-id="76e97-120">hello preceding example returns hello following object:</span></span>

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a><span data-ttu-id="76e97-121">parameters</span><span class="sxs-lookup"><span data-stu-id="76e97-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="76e97-122">Retourneert een parameterwaarde.</span><span class="sxs-lookup"><span data-stu-id="76e97-122">Returns a parameter value.</span></span> <span data-ttu-id="76e97-123">Hallo opgegeven parameternaam moet worden gedefinieerd in sectie van de parameters Hallo van Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="76e97-123">hello specified parameter name must be defined in hello parameters section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="76e97-124">Parameters</span><span class="sxs-lookup"><span data-stu-id="76e97-124">Parameters</span></span>

| <span data-ttu-id="76e97-125">Parameter</span><span class="sxs-lookup"><span data-stu-id="76e97-125">Parameter</span></span> | <span data-ttu-id="76e97-126">Vereist</span><span class="sxs-lookup"><span data-stu-id="76e97-126">Required</span></span> | <span data-ttu-id="76e97-127">Type</span><span class="sxs-lookup"><span data-stu-id="76e97-127">Type</span></span> | <span data-ttu-id="76e97-128">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="76e97-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="76e97-129">parameterName</span><span class="sxs-lookup"><span data-stu-id="76e97-129">parameterName</span></span> |<span data-ttu-id="76e97-130">Ja</span><span class="sxs-lookup"><span data-stu-id="76e97-130">Yes</span></span> |<span data-ttu-id="76e97-131">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="76e97-131">string</span></span> |<span data-ttu-id="76e97-132">Hallo-naam van Hallo parameter tooreturn.</span><span class="sxs-lookup"><span data-stu-id="76e97-132">hello name of hello parameter tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="76e97-133">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="76e97-133">Return value</span></span>

<span data-ttu-id="76e97-134">Hallo-waarde van Hallo opgegeven parameter.</span><span class="sxs-lookup"><span data-stu-id="76e97-134">hello value of hello specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="76e97-135">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="76e97-135">Remarks</span></span>

<span data-ttu-id="76e97-136">Doorgaans kunt u parameterwaarden tooset resource gebruiken.</span><span class="sxs-lookup"><span data-stu-id="76e97-136">Typically, you use parameters tooset resource values.</span></span> <span data-ttu-id="76e97-137">Hallo wordt volgende voorbeeld Hallo-naam van de website toohello doorgegeven parameterwaarde tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="76e97-137">hello following example sets hello name of web site toohello parameter value passed in during deployment.</span></span>

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="76e97-138">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="76e97-138">Example</span></span>

<span data-ttu-id="76e97-139">Hallo volgende voorbeeld ziet u een vereenvoudigde gebruik van de functie voor Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="76e97-139">hello following example shows a simplified use of hello parameters function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="76e97-140">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="76e97-140">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="76e97-141">Naam</span><span class="sxs-lookup"><span data-stu-id="76e97-141">Name</span></span> | <span data-ttu-id="76e97-142">Type</span><span class="sxs-lookup"><span data-stu-id="76e97-142">Type</span></span> | <span data-ttu-id="76e97-143">Waarde</span><span class="sxs-lookup"><span data-stu-id="76e97-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="76e97-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="76e97-144">stringOutput</span></span> | <span data-ttu-id="76e97-145">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="76e97-145">String</span></span> | <span data-ttu-id="76e97-146">Optie 1</span><span class="sxs-lookup"><span data-stu-id="76e97-146">option 1</span></span> |
| <span data-ttu-id="76e97-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="76e97-147">intOutput</span></span> | <span data-ttu-id="76e97-148">int</span><span class="sxs-lookup"><span data-stu-id="76e97-148">Int</span></span> | <span data-ttu-id="76e97-149">1</span><span class="sxs-lookup"><span data-stu-id="76e97-149">1</span></span> |
| <span data-ttu-id="76e97-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="76e97-150">objectOutput</span></span> | <span data-ttu-id="76e97-151">Object</span><span class="sxs-lookup"><span data-stu-id="76e97-151">Object</span></span> | <span data-ttu-id="76e97-152">{"een": "a", "twee": "b"}</span><span class="sxs-lookup"><span data-stu-id="76e97-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="76e97-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="76e97-153">arrayOutput</span></span> | <span data-ttu-id="76e97-154">Matrix</span><span class="sxs-lookup"><span data-stu-id="76e97-154">Array</span></span> | <span data-ttu-id="76e97-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="76e97-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="76e97-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="76e97-156">crossOutput</span></span> | <span data-ttu-id="76e97-157">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="76e97-157">String</span></span> | <span data-ttu-id="76e97-158">Optie 1</span><span class="sxs-lookup"><span data-stu-id="76e97-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="76e97-159">variabelen</span><span class="sxs-lookup"><span data-stu-id="76e97-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="76e97-160">Retourneert Hallo de waarde van variabele.</span><span class="sxs-lookup"><span data-stu-id="76e97-160">Returns hello value of variable.</span></span> <span data-ttu-id="76e97-161">Hallo opgegeven variabelenaam moet worden gedefinieerd in sectie met sjabloonvariabelen Hallo van Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="76e97-161">hello specified variable name must be defined in hello variables section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="76e97-162">Parameters</span><span class="sxs-lookup"><span data-stu-id="76e97-162">Parameters</span></span>

| <span data-ttu-id="76e97-163">Parameter</span><span class="sxs-lookup"><span data-stu-id="76e97-163">Parameter</span></span> | <span data-ttu-id="76e97-164">Vereist</span><span class="sxs-lookup"><span data-stu-id="76e97-164">Required</span></span> | <span data-ttu-id="76e97-165">Type</span><span class="sxs-lookup"><span data-stu-id="76e97-165">Type</span></span> | <span data-ttu-id="76e97-166">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="76e97-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="76e97-167">Variabelenaam</span><span class="sxs-lookup"><span data-stu-id="76e97-167">variableName</span></span> |<span data-ttu-id="76e97-168">Ja</span><span class="sxs-lookup"><span data-stu-id="76e97-168">Yes</span></span> |<span data-ttu-id="76e97-169">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="76e97-169">String</span></span> |<span data-ttu-id="76e97-170">Hallo-naam van de variabele tooreturn Hallo.</span><span class="sxs-lookup"><span data-stu-id="76e97-170">hello name of hello variable tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="76e97-171">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="76e97-171">Return value</span></span>

<span data-ttu-id="76e97-172">Hallo-waarde van de opgegeven Hallo-variabele.</span><span class="sxs-lookup"><span data-stu-id="76e97-172">hello value of hello specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="76e97-173">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="76e97-173">Remarks</span></span>

<span data-ttu-id="76e97-174">Normaal gesproken u variabelen toosimplify uw sjabloon door slechts één keer complexe waarden samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="76e97-174">Typically, you use variables toosimplify your template by constructing complex values only once.</span></span> <span data-ttu-id="76e97-175">Hallo wordt volgende voorbeeld een unieke naam voor een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="76e97-175">hello following example constructs a unique name for a storage account.</span></span>

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a><span data-ttu-id="76e97-176">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="76e97-176">Example</span></span>

<span data-ttu-id="76e97-177">Hallo-voorbeeldsjabloon retourneert verschillende waarden van variabelen.</span><span class="sxs-lookup"><span data-stu-id="76e97-177">hello example template returns different variable values.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="76e97-178">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="76e97-178">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="76e97-179">Naam</span><span class="sxs-lookup"><span data-stu-id="76e97-179">Name</span></span> | <span data-ttu-id="76e97-180">Type</span><span class="sxs-lookup"><span data-stu-id="76e97-180">Type</span></span> | <span data-ttu-id="76e97-181">Waarde</span><span class="sxs-lookup"><span data-stu-id="76e97-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="76e97-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="76e97-182">exampleOutput1</span></span> | <span data-ttu-id="76e97-183">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="76e97-183">String</span></span> | <span data-ttu-id="76e97-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="76e97-184">myVariable</span></span> |
| <span data-ttu-id="76e97-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="76e97-185">exampleOutput2</span></span> | <span data-ttu-id="76e97-186">Matrix</span><span class="sxs-lookup"><span data-stu-id="76e97-186">Array</span></span> | <span data-ttu-id="76e97-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="76e97-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="76e97-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="76e97-188">exampleOutput3</span></span> | <span data-ttu-id="76e97-189">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="76e97-189">String</span></span> | <span data-ttu-id="76e97-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="76e97-190">myVariable</span></span> |
| <span data-ttu-id="76e97-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="76e97-191">exampleOutput4</span></span> |  <span data-ttu-id="76e97-192">Object</span><span class="sxs-lookup"><span data-stu-id="76e97-192">Object</span></span> | <span data-ttu-id="76e97-193">{{'1': 'value1', 'eigenschap 2': 'waarde2'}</span><span class="sxs-lookup"><span data-stu-id="76e97-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="76e97-194">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="76e97-194">Next steps</span></span>
* <span data-ttu-id="76e97-195">Zie voor een beschrijving van de secties Hallo in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="76e97-195">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="76e97-196">toomerge meerdere sjablonen Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="76e97-196">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="76e97-197">een opgegeven aantal keren tooiterate bij het maken van een type resource, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="76e97-197">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="76e97-198">toosee hoe toodeploy Hallo sjabloon die u hebt gemaakt, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="76e97-198">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

