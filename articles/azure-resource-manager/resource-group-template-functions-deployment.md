---
title: Azure Resource Manager-sjabloonfuncties - implementatie | Microsoft Docs
description: Beschrijft de functies te gebruiken in een Azure Resource Manager-sjabloon voor het ophalen van informatie over de implementatie.
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
ms.openlocfilehash: d7e6bcd669d40cb19de44b646505856ecd8f51a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="e3e15-103">Implementatie-functies voor Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="e3e15-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="e3e15-104">Resource Manager biedt de volgende functies voor het ophalen van waarden van de secties van de sjabloon en de waarden die betrekking hebben op de implementatie:</span><span class="sxs-lookup"><span data-stu-id="e3e15-104">Resource Manager provides the following functions for getting values from sections of the template and values related to the deployment:</span></span>

* [<span data-ttu-id="e3e15-105">implementatie</span><span class="sxs-lookup"><span data-stu-id="e3e15-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="e3e15-106">parameters</span><span class="sxs-lookup"><span data-stu-id="e3e15-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="e3e15-107">variabelen</span><span class="sxs-lookup"><span data-stu-id="e3e15-107">variables</span></span>](#variables)

<span data-ttu-id="e3e15-108">Als u de waarden van resources, resourcegroepen of abonnementen, Zie [Resource functies](resource-group-template-functions-resource.md).</span><span class="sxs-lookup"><span data-stu-id="e3e15-108">To get values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="e3e15-109">implementatie</span><span class="sxs-lookup"><span data-stu-id="e3e15-109">deployment</span></span>
`deployment()`

<span data-ttu-id="e3e15-110">Retourneert informatie over de huidige implementatiebewerking.</span><span class="sxs-lookup"><span data-stu-id="e3e15-110">Returns information about the current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="e3e15-111">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="e3e15-111">Return value</span></span>

<span data-ttu-id="e3e15-112">Deze functie retourneert het object dat wordt doorgegeven tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="e3e15-112">This function returns the object that is passed during deployment.</span></span> <span data-ttu-id="e3e15-113">De eigenschappen in het geretourneerde object verschillen op basis van of het implementatieobject wordt doorgegeven als een koppeling of als een in-line-object.</span><span class="sxs-lookup"><span data-stu-id="e3e15-113">The properties in the returned object differ based on whether the deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="e3e15-114">Wanneer het implementatieobject wordt doorgegeven in de regel, zoals wanneer u de **- sjabloonbestand** parameter in Azure PowerShell om te verwijzen naar een lokaal bestand, het geretourneerde object heeft de volgende notatie:</span><span class="sxs-lookup"><span data-stu-id="e3e15-114">When the deployment object is passed in-line, such as when using the **-TemplateFile** parameter in Azure PowerShell to point to a local file, the returned object has the following format:</span></span>

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

<span data-ttu-id="e3e15-115">Wanneer het object is doorgegeven als een koppeling, zoals wanneer u de **- TemplateUri** parameter om te verwijzen naar een extern object het object wordt geretourneerd in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="e3e15-115">When the object is passed as a link, such as when using the **-TemplateUri** parameter to point to a remote object, the object is returned in the following format:</span></span> 

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

### <a name="remarks"></a><span data-ttu-id="e3e15-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="e3e15-116">Remarks</span></span>

<span data-ttu-id="e3e15-117">U kunt deployment() gebruiken om te koppelen aan een andere sjabloon op basis van de URI van de bovenliggende sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e3e15-117">You can use deployment() to link to another template based on the URI of the parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="e3e15-118">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e3e15-118">Example</span></span>

<span data-ttu-id="e3e15-119">Het volgende voorbeeld wordt het implementatieobject:</span><span class="sxs-lookup"><span data-stu-id="e3e15-119">The following example returns the deployment object:</span></span>

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

<span data-ttu-id="e3e15-120">Het vorige voorbeeld retourneert de volgende object:</span><span class="sxs-lookup"><span data-stu-id="e3e15-120">The preceding example returns the following object:</span></span>

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

## <a name="parameters"></a><span data-ttu-id="e3e15-121">Parameters</span><span class="sxs-lookup"><span data-stu-id="e3e15-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="e3e15-122">Retourneert een parameterwaarde.</span><span class="sxs-lookup"><span data-stu-id="e3e15-122">Returns a parameter value.</span></span> <span data-ttu-id="e3e15-123">De opgegeven parameternaam moet worden gedefinieerd in het gedeelte parameters van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e3e15-123">The specified parameter name must be defined in the parameters section of the template.</span></span>

### <a name="parameters"></a><span data-ttu-id="e3e15-124">Parameters</span><span class="sxs-lookup"><span data-stu-id="e3e15-124">Parameters</span></span>

| <span data-ttu-id="e3e15-125">Parameter</span><span class="sxs-lookup"><span data-stu-id="e3e15-125">Parameter</span></span> | <span data-ttu-id="e3e15-126">Vereist</span><span class="sxs-lookup"><span data-stu-id="e3e15-126">Required</span></span> | <span data-ttu-id="e3e15-127">Type</span><span class="sxs-lookup"><span data-stu-id="e3e15-127">Type</span></span> | <span data-ttu-id="e3e15-128">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e3e15-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e3e15-129">parameterName</span><span class="sxs-lookup"><span data-stu-id="e3e15-129">parameterName</span></span> |<span data-ttu-id="e3e15-130">Ja</span><span class="sxs-lookup"><span data-stu-id="e3e15-130">Yes</span></span> |<span data-ttu-id="e3e15-131">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="e3e15-131">string</span></span> |<span data-ttu-id="e3e15-132">De naam van de parameter om terug te keren.</span><span class="sxs-lookup"><span data-stu-id="e3e15-132">The name of the parameter to return.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e3e15-133">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="e3e15-133">Return value</span></span>

<span data-ttu-id="e3e15-134">De waarde van de opgegeven parameter.</span><span class="sxs-lookup"><span data-stu-id="e3e15-134">The value of the specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="e3e15-135">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="e3e15-135">Remarks</span></span>

<span data-ttu-id="e3e15-136">Doorgaans kunt u parameters resource waarden instellen.</span><span class="sxs-lookup"><span data-stu-id="e3e15-136">Typically, you use parameters to set resource values.</span></span> <span data-ttu-id="e3e15-137">Het volgende voorbeeld wordt de naam van de website met de parameterwaarde doorgegeven tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="e3e15-137">The following example sets the name of web site to the parameter value passed in during deployment.</span></span>

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

### <a name="example"></a><span data-ttu-id="e3e15-138">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e3e15-138">Example</span></span>

<span data-ttu-id="e3e15-139">Het volgende voorbeeld ziet u een vereenvoudigde gebruik van de parameters-functie.</span><span class="sxs-lookup"><span data-stu-id="e3e15-139">The following example shows a simplified use of the parameters function.</span></span>

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

<span data-ttu-id="e3e15-140">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="e3e15-140">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e3e15-141">Naam</span><span class="sxs-lookup"><span data-stu-id="e3e15-141">Name</span></span> | <span data-ttu-id="e3e15-142">Type</span><span class="sxs-lookup"><span data-stu-id="e3e15-142">Type</span></span> | <span data-ttu-id="e3e15-143">Waarde</span><span class="sxs-lookup"><span data-stu-id="e3e15-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e3e15-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="e3e15-144">stringOutput</span></span> | <span data-ttu-id="e3e15-145">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="e3e15-145">String</span></span> | <span data-ttu-id="e3e15-146">Optie 1</span><span class="sxs-lookup"><span data-stu-id="e3e15-146">option 1</span></span> |
| <span data-ttu-id="e3e15-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="e3e15-147">intOutput</span></span> | <span data-ttu-id="e3e15-148">int</span><span class="sxs-lookup"><span data-stu-id="e3e15-148">Int</span></span> | <span data-ttu-id="e3e15-149">1</span><span class="sxs-lookup"><span data-stu-id="e3e15-149">1</span></span> |
| <span data-ttu-id="e3e15-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="e3e15-150">objectOutput</span></span> | <span data-ttu-id="e3e15-151">Object</span><span class="sxs-lookup"><span data-stu-id="e3e15-151">Object</span></span> | <span data-ttu-id="e3e15-152">{"een": "a", "twee": "b"}</span><span class="sxs-lookup"><span data-stu-id="e3e15-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="e3e15-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="e3e15-153">arrayOutput</span></span> | <span data-ttu-id="e3e15-154">matrix</span><span class="sxs-lookup"><span data-stu-id="e3e15-154">Array</span></span> | <span data-ttu-id="e3e15-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="e3e15-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="e3e15-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="e3e15-156">crossOutput</span></span> | <span data-ttu-id="e3e15-157">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="e3e15-157">String</span></span> | <span data-ttu-id="e3e15-158">Optie 1</span><span class="sxs-lookup"><span data-stu-id="e3e15-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="e3e15-159">variabelen</span><span class="sxs-lookup"><span data-stu-id="e3e15-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="e3e15-160">Retourneert de waarde van variabele.</span><span class="sxs-lookup"><span data-stu-id="e3e15-160">Returns the value of variable.</span></span> <span data-ttu-id="e3e15-161">De opgegeven naam van de variabele moet worden gedefinieerd in het gedeelte variabelen van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e3e15-161">The specified variable name must be defined in the variables section of the template.</span></span>

### <a name="parameters"></a><span data-ttu-id="e3e15-162">Parameters</span><span class="sxs-lookup"><span data-stu-id="e3e15-162">Parameters</span></span>

| <span data-ttu-id="e3e15-163">Parameter</span><span class="sxs-lookup"><span data-stu-id="e3e15-163">Parameter</span></span> | <span data-ttu-id="e3e15-164">Vereist</span><span class="sxs-lookup"><span data-stu-id="e3e15-164">Required</span></span> | <span data-ttu-id="e3e15-165">Type</span><span class="sxs-lookup"><span data-stu-id="e3e15-165">Type</span></span> | <span data-ttu-id="e3e15-166">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e3e15-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e3e15-167">Variabelenaam</span><span class="sxs-lookup"><span data-stu-id="e3e15-167">variableName</span></span> |<span data-ttu-id="e3e15-168">Ja</span><span class="sxs-lookup"><span data-stu-id="e3e15-168">Yes</span></span> |<span data-ttu-id="e3e15-169">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="e3e15-169">String</span></span> |<span data-ttu-id="e3e15-170">De naam van de variabele retourneren.</span><span class="sxs-lookup"><span data-stu-id="e3e15-170">The name of the variable to return.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e3e15-171">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="e3e15-171">Return value</span></span>

<span data-ttu-id="e3e15-172">De waarde van de opgegeven variabele.</span><span class="sxs-lookup"><span data-stu-id="e3e15-172">The value of the specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="e3e15-173">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="e3e15-173">Remarks</span></span>

<span data-ttu-id="e3e15-174">Doorgaans kunt u variabelen uw sjabloon vereenvoudigen door slechts één keer complexe waarden samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="e3e15-174">Typically, you use variables to simplify your template by constructing complex values only once.</span></span> <span data-ttu-id="e3e15-175">Het volgende voorbeeld wordt een unieke naam voor een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e3e15-175">The following example constructs a unique name for a storage account.</span></span>

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

### <a name="example"></a><span data-ttu-id="e3e15-176">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e3e15-176">Example</span></span>

<span data-ttu-id="e3e15-177">De voorbeeldsjabloon retourneert de waarden van verschillende variabelen.</span><span class="sxs-lookup"><span data-stu-id="e3e15-177">The example template returns different variable values.</span></span>

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

<span data-ttu-id="e3e15-178">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="e3e15-178">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e3e15-179">Naam</span><span class="sxs-lookup"><span data-stu-id="e3e15-179">Name</span></span> | <span data-ttu-id="e3e15-180">Type</span><span class="sxs-lookup"><span data-stu-id="e3e15-180">Type</span></span> | <span data-ttu-id="e3e15-181">Waarde</span><span class="sxs-lookup"><span data-stu-id="e3e15-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e3e15-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="e3e15-182">exampleOutput1</span></span> | <span data-ttu-id="e3e15-183">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="e3e15-183">String</span></span> | <span data-ttu-id="e3e15-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="e3e15-184">myVariable</span></span> |
| <span data-ttu-id="e3e15-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="e3e15-185">exampleOutput2</span></span> | <span data-ttu-id="e3e15-186">matrix</span><span class="sxs-lookup"><span data-stu-id="e3e15-186">Array</span></span> | <span data-ttu-id="e3e15-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="e3e15-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="e3e15-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="e3e15-188">exampleOutput3</span></span> | <span data-ttu-id="e3e15-189">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="e3e15-189">String</span></span> | <span data-ttu-id="e3e15-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="e3e15-190">myVariable</span></span> |
| <span data-ttu-id="e3e15-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="e3e15-191">exampleOutput4</span></span> |  <span data-ttu-id="e3e15-192">Object</span><span class="sxs-lookup"><span data-stu-id="e3e15-192">Object</span></span> | <span data-ttu-id="e3e15-193">{{'1': 'value1', 'eigenschap 2': 'waarde2'}</span><span class="sxs-lookup"><span data-stu-id="e3e15-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e3e15-194">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e3e15-194">Next steps</span></span>
* <span data-ttu-id="e3e15-195">Zie voor een beschrijving van de secties in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e3e15-195">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="e3e15-196">U kunt meerdere sjablonen samenvoegen, Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e3e15-196">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="e3e15-197">Voor een opgegeven aantal keer herhalen bij het maken van een type resource, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="e3e15-197">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="e3e15-198">Zie voor het implementeren van de sjabloon die u hebt gemaakt, [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e3e15-198">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

