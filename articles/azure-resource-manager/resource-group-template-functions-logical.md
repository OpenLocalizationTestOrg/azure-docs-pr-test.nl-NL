---
title: aaaAzure Resource Manager-sjabloonfuncties - logische | Microsoft Docs
description: Hierin wordt beschreven Hallo functies toouse in een Azure Resource Manager sjabloon toodetermine logische waarden.
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
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="63707-103">Logische functies voor Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="63707-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="63707-104">Resource Manager biedt een aantal functies voor het maken van vergelijkingen in uw sjablonen.</span><span class="sxs-lookup"><span data-stu-id="63707-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="63707-105">en</span><span class="sxs-lookup"><span data-stu-id="63707-105">and</span></span>](#and)
* [<span data-ttu-id="63707-106">BOOL</span><span class="sxs-lookup"><span data-stu-id="63707-106">bool</span></span>](#bool)
* [<span data-ttu-id="63707-107">Als</span><span class="sxs-lookup"><span data-stu-id="63707-107">if</span></span>](#if)
* [<span data-ttu-id="63707-108">niet</span><span class="sxs-lookup"><span data-stu-id="63707-108">not</span></span>](#not)
* [<span data-ttu-id="63707-109">of</span><span class="sxs-lookup"><span data-stu-id="63707-109">or</span></span>](#or)

## <a name="and"></a><span data-ttu-id="63707-110">en</span><span class="sxs-lookup"><span data-stu-id="63707-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="63707-111">Controleert of beide parameterwaarden true zijn.</span><span class="sxs-lookup"><span data-stu-id="63707-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="63707-112">Parameters</span><span class="sxs-lookup"><span data-stu-id="63707-112">Parameters</span></span>

| <span data-ttu-id="63707-113">Parameter</span><span class="sxs-lookup"><span data-stu-id="63707-113">Parameter</span></span> | <span data-ttu-id="63707-114">Vereist</span><span class="sxs-lookup"><span data-stu-id="63707-114">Required</span></span> | <span data-ttu-id="63707-115">Type</span><span class="sxs-lookup"><span data-stu-id="63707-115">Type</span></span> | <span data-ttu-id="63707-116">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="63707-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="63707-117">Arg1</span><span class="sxs-lookup"><span data-stu-id="63707-117">arg1</span></span> |<span data-ttu-id="63707-118">Ja</span><span class="sxs-lookup"><span data-stu-id="63707-118">Yes</span></span> |<span data-ttu-id="63707-119">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="63707-119">boolean</span></span> |<span data-ttu-id="63707-120">eerste waarde toocheck of Hallo is ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="63707-120">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="63707-121">Arg2</span><span class="sxs-lookup"><span data-stu-id="63707-121">arg2</span></span> |<span data-ttu-id="63707-122">Ja</span><span class="sxs-lookup"><span data-stu-id="63707-122">Yes</span></span> |<span data-ttu-id="63707-123">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="63707-123">boolean</span></span> |<span data-ttu-id="63707-124">tweede waarde toocheck of Hallo is ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="63707-124">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="63707-125">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="63707-125">Return value</span></span>

<span data-ttu-id="63707-126">Retourneert **True** als beide waarden true, anders wordt zijn **False**.</span><span class="sxs-lookup"><span data-stu-id="63707-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="63707-127">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="63707-127">Examples</span></span>

<span data-ttu-id="63707-128">Hallo volgende voorbeeld ziet u hoe logische toouse-functies.</span><span class="sxs-lookup"><span data-stu-id="63707-128">hello following example shows how toouse logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="63707-129">Hallo-uitvoer van het voorgaande voorbeeld Hallo is:</span><span class="sxs-lookup"><span data-stu-id="63707-129">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="63707-130">Naam</span><span class="sxs-lookup"><span data-stu-id="63707-130">Name</span></span> | <span data-ttu-id="63707-131">Type</span><span class="sxs-lookup"><span data-stu-id="63707-131">Type</span></span> | <span data-ttu-id="63707-132">Waarde</span><span class="sxs-lookup"><span data-stu-id="63707-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="63707-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="63707-133">andExampleOutput</span></span> | <span data-ttu-id="63707-134">BOOL</span><span class="sxs-lookup"><span data-stu-id="63707-134">Bool</span></span> | <span data-ttu-id="63707-135">False</span><span class="sxs-lookup"><span data-stu-id="63707-135">False</span></span> |
| <span data-ttu-id="63707-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="63707-136">orExampleOutput</span></span> | <span data-ttu-id="63707-137">BOOL</span><span class="sxs-lookup"><span data-stu-id="63707-137">Bool</span></span> | <span data-ttu-id="63707-138">True</span><span class="sxs-lookup"><span data-stu-id="63707-138">True</span></span> |
| <span data-ttu-id="63707-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="63707-139">notExampleOutput</span></span> | <span data-ttu-id="63707-140">BOOL</span><span class="sxs-lookup"><span data-stu-id="63707-140">Bool</span></span> | <span data-ttu-id="63707-141">False</span><span class="sxs-lookup"><span data-stu-id="63707-141">False</span></span> |


## <a name="bool"></a><span data-ttu-id="63707-142">BOOL</span><span class="sxs-lookup"><span data-stu-id="63707-142">bool</span></span>
`bool(arg1)`

<span data-ttu-id="63707-143">Converteert Hallo parameter tooa Boolean-waarde.</span><span class="sxs-lookup"><span data-stu-id="63707-143">Converts hello parameter tooa boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="63707-144">Parameters</span><span class="sxs-lookup"><span data-stu-id="63707-144">Parameters</span></span>

| <span data-ttu-id="63707-145">Parameter</span><span class="sxs-lookup"><span data-stu-id="63707-145">Parameter</span></span> | <span data-ttu-id="63707-146">Vereist</span><span class="sxs-lookup"><span data-stu-id="63707-146">Required</span></span> | <span data-ttu-id="63707-147">Type</span><span class="sxs-lookup"><span data-stu-id="63707-147">Type</span></span> | <span data-ttu-id="63707-148">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="63707-148">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="63707-149">Arg1</span><span class="sxs-lookup"><span data-stu-id="63707-149">arg1</span></span> |<span data-ttu-id="63707-150">Ja</span><span class="sxs-lookup"><span data-stu-id="63707-150">Yes</span></span> |<span data-ttu-id="63707-151">String of int.</span><span class="sxs-lookup"><span data-stu-id="63707-151">string or int</span></span> |<span data-ttu-id="63707-152">Hallo waarde tooconvert tooa Boolean-waarde.</span><span class="sxs-lookup"><span data-stu-id="63707-152">hello value tooconvert tooa boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="63707-153">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="63707-153">Return value</span></span>
<span data-ttu-id="63707-154">Een Booleaanse waarde Hallo geconverteerd waarde.</span><span class="sxs-lookup"><span data-stu-id="63707-154">A boolean of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="63707-155">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="63707-155">Examples</span></span>

<span data-ttu-id="63707-156">Hallo volgende voorbeeld wordt getoond hoe toouse bool met een tekenreeks of een geheel getal.</span><span class="sxs-lookup"><span data-stu-id="63707-156">hello following example shows how toouse bool with a string or integer.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="63707-157">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="63707-157">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="63707-158">Naam</span><span class="sxs-lookup"><span data-stu-id="63707-158">Name</span></span> | <span data-ttu-id="63707-159">Type</span><span class="sxs-lookup"><span data-stu-id="63707-159">Type</span></span> | <span data-ttu-id="63707-160">Waarde</span><span class="sxs-lookup"><span data-stu-id="63707-160">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="63707-161">trueString</span><span class="sxs-lookup"><span data-stu-id="63707-161">trueString</span></span> | <span data-ttu-id="63707-162">BOOL</span><span class="sxs-lookup"><span data-stu-id="63707-162">Bool</span></span> | <span data-ttu-id="63707-163">True</span><span class="sxs-lookup"><span data-stu-id="63707-163">True</span></span> |
| <span data-ttu-id="63707-164">falseString</span><span class="sxs-lookup"><span data-stu-id="63707-164">falseString</span></span> | <span data-ttu-id="63707-165">BOOL</span><span class="sxs-lookup"><span data-stu-id="63707-165">Bool</span></span> | <span data-ttu-id="63707-166">False</span><span class="sxs-lookup"><span data-stu-id="63707-166">False</span></span> |
| <span data-ttu-id="63707-167">trueInt</span><span class="sxs-lookup"><span data-stu-id="63707-167">trueInt</span></span> | <span data-ttu-id="63707-168">BOOL</span><span class="sxs-lookup"><span data-stu-id="63707-168">Bool</span></span> | <span data-ttu-id="63707-169">True</span><span class="sxs-lookup"><span data-stu-id="63707-169">True</span></span> |
| <span data-ttu-id="63707-170">falseInt</span><span class="sxs-lookup"><span data-stu-id="63707-170">falseInt</span></span> | <span data-ttu-id="63707-171">BOOL</span><span class="sxs-lookup"><span data-stu-id="63707-171">Bool</span></span> | <span data-ttu-id="63707-172">False</span><span class="sxs-lookup"><span data-stu-id="63707-172">False</span></span> |

## <a name="if"></a><span data-ttu-id="63707-173">Als</span><span class="sxs-lookup"><span data-stu-id="63707-173">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="63707-174">Retourneert een waarde op basis van of u een voorwaarde is true of false.</span><span class="sxs-lookup"><span data-stu-id="63707-174">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="63707-175">Parameters</span><span class="sxs-lookup"><span data-stu-id="63707-175">Parameters</span></span>

| <span data-ttu-id="63707-176">Parameter</span><span class="sxs-lookup"><span data-stu-id="63707-176">Parameter</span></span> | <span data-ttu-id="63707-177">Vereist</span><span class="sxs-lookup"><span data-stu-id="63707-177">Required</span></span> | <span data-ttu-id="63707-178">Type</span><span class="sxs-lookup"><span data-stu-id="63707-178">Type</span></span> | <span data-ttu-id="63707-179">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="63707-179">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="63707-180">Voorwaarde</span><span class="sxs-lookup"><span data-stu-id="63707-180">condition</span></span> |<span data-ttu-id="63707-181">Ja</span><span class="sxs-lookup"><span data-stu-id="63707-181">Yes</span></span> |<span data-ttu-id="63707-182">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="63707-182">boolean</span></span> |<span data-ttu-id="63707-183">Hallo waarde toocheck of true is.</span><span class="sxs-lookup"><span data-stu-id="63707-183">hello value toocheck whether it is true.</span></span> |
| <span data-ttu-id="63707-184">trueValue</span><span class="sxs-lookup"><span data-stu-id="63707-184">trueValue</span></span> |<span data-ttu-id="63707-185">Ja</span><span class="sxs-lookup"><span data-stu-id="63707-185">Yes</span></span> | <span data-ttu-id="63707-186">String, int, object of matrix</span><span class="sxs-lookup"><span data-stu-id="63707-186">string, int, object, or array</span></span> |<span data-ttu-id="63707-187">Hallo waarde tooreturn wanneer Hallo voorwaarde waar is.</span><span class="sxs-lookup"><span data-stu-id="63707-187">hello value tooreturn when hello condition is true.</span></span> |
| <span data-ttu-id="63707-188">falseValue</span><span class="sxs-lookup"><span data-stu-id="63707-188">falseValue</span></span> |<span data-ttu-id="63707-189">Ja</span><span class="sxs-lookup"><span data-stu-id="63707-189">Yes</span></span> | <span data-ttu-id="63707-190">String, int, object of matrix</span><span class="sxs-lookup"><span data-stu-id="63707-190">string, int, object, or array</span></span> |<span data-ttu-id="63707-191">Hallo waarde tooreturn wanneer Hallo voorwaarde onwaar is.</span><span class="sxs-lookup"><span data-stu-id="63707-191">hello value tooreturn when hello condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="63707-192">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="63707-192">Return value</span></span>

<span data-ttu-id="63707-193">Retourneert een tweede parameter als eerste parameter is **True**; anders retourneert de derde parameter.</span><span class="sxs-lookup"><span data-stu-id="63707-193">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="63707-194">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="63707-194">Remarks</span></span>

<span data-ttu-id="63707-195">U kunt deze functie tooconditionally set een broneigenschap te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="63707-195">You can use this function tooconditionally set a resource property.</span></span> <span data-ttu-id="63707-196">Hallo volgende voorbeeld is niet een volledige sjabloon, maar het Hallo relevante delen voor het instellen van voorwaardelijk Hallo beschikbaarheidsset bevat.</span><span class="sxs-lookup"><span data-stu-id="63707-196">hello following example is not a full template, but it shows hello relevant portions for conditionally setting hello availability set.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a><span data-ttu-id="63707-197">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="63707-197">Examples</span></span>

<span data-ttu-id="63707-198">Hallo volgende voorbeeld wordt getoond hoe toouse hello `if` functie.</span><span class="sxs-lookup"><span data-stu-id="63707-198">hello following example shows how toouse hello `if` function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

<span data-ttu-id="63707-199">Hallo-uitvoer van het voorgaande voorbeeld Hallo is:</span><span class="sxs-lookup"><span data-stu-id="63707-199">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="63707-200">Naam</span><span class="sxs-lookup"><span data-stu-id="63707-200">Name</span></span> | <span data-ttu-id="63707-201">Type</span><span class="sxs-lookup"><span data-stu-id="63707-201">Type</span></span> | <span data-ttu-id="63707-202">Waarde</span><span class="sxs-lookup"><span data-stu-id="63707-202">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="63707-203">yesOutput</span><span class="sxs-lookup"><span data-stu-id="63707-203">yesOutput</span></span> | <span data-ttu-id="63707-204">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="63707-204">String</span></span> | <span data-ttu-id="63707-205">Ja</span><span class="sxs-lookup"><span data-stu-id="63707-205">yes</span></span> |
| <span data-ttu-id="63707-206">noOutput</span><span class="sxs-lookup"><span data-stu-id="63707-206">noOutput</span></span> | <span data-ttu-id="63707-207">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="63707-207">String</span></span> | <span data-ttu-id="63707-208">Er is geen</span><span class="sxs-lookup"><span data-stu-id="63707-208">no</span></span> |


## <a name="not"></a><span data-ttu-id="63707-209">niet</span><span class="sxs-lookup"><span data-stu-id="63707-209">not</span></span>
`not(arg1)`

<span data-ttu-id="63707-210">Booleaanse waarde tooits converteert tegenover waarde.</span><span class="sxs-lookup"><span data-stu-id="63707-210">Converts boolean value tooits opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="63707-211">Parameters</span><span class="sxs-lookup"><span data-stu-id="63707-211">Parameters</span></span>

| <span data-ttu-id="63707-212">Parameter</span><span class="sxs-lookup"><span data-stu-id="63707-212">Parameter</span></span> | <span data-ttu-id="63707-213">Vereist</span><span class="sxs-lookup"><span data-stu-id="63707-213">Required</span></span> | <span data-ttu-id="63707-214">Type</span><span class="sxs-lookup"><span data-stu-id="63707-214">Type</span></span> | <span data-ttu-id="63707-215">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="63707-215">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="63707-216">Arg1</span><span class="sxs-lookup"><span data-stu-id="63707-216">arg1</span></span> |<span data-ttu-id="63707-217">Ja</span><span class="sxs-lookup"><span data-stu-id="63707-217">Yes</span></span> |<span data-ttu-id="63707-218">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="63707-218">boolean</span></span> |<span data-ttu-id="63707-219">Hallo waarde tooconvert.</span><span class="sxs-lookup"><span data-stu-id="63707-219">hello value tooconvert.</span></span> |


### <a name="return-value"></a><span data-ttu-id="63707-220">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="63707-220">Return value</span></span>

<span data-ttu-id="63707-221">Retourneert **True** wanneer de parameter is **False**.</span><span class="sxs-lookup"><span data-stu-id="63707-221">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="63707-222">Retourneert **False** wanneer de parameter is **True**.</span><span class="sxs-lookup"><span data-stu-id="63707-222">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="63707-223">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="63707-223">Examples</span></span>

<span data-ttu-id="63707-224">Hallo volgende voorbeeld ziet u hoe logische toouse-functies.</span><span class="sxs-lookup"><span data-stu-id="63707-224">hello following example shows how toouse logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="63707-225">Hallo-uitvoer van het voorgaande voorbeeld Hallo is:</span><span class="sxs-lookup"><span data-stu-id="63707-225">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="63707-226">Naam</span><span class="sxs-lookup"><span data-stu-id="63707-226">Name</span></span> | <span data-ttu-id="63707-227">Type</span><span class="sxs-lookup"><span data-stu-id="63707-227">Type</span></span> | <span data-ttu-id="63707-228">Waarde</span><span class="sxs-lookup"><span data-stu-id="63707-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="63707-229">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="63707-229">andExampleOutput</span></span> | <span data-ttu-id="63707-230">BOOL</span><span class="sxs-lookup"><span data-stu-id="63707-230">Bool</span></span> | <span data-ttu-id="63707-231">False</span><span class="sxs-lookup"><span data-stu-id="63707-231">False</span></span> |
| <span data-ttu-id="63707-232">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="63707-232">orExampleOutput</span></span> | <span data-ttu-id="63707-233">BOOL</span><span class="sxs-lookup"><span data-stu-id="63707-233">Bool</span></span> | <span data-ttu-id="63707-234">True</span><span class="sxs-lookup"><span data-stu-id="63707-234">True</span></span> |
| <span data-ttu-id="63707-235">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="63707-235">notExampleOutput</span></span> | <span data-ttu-id="63707-236">BOOL</span><span class="sxs-lookup"><span data-stu-id="63707-236">Bool</span></span> | <span data-ttu-id="63707-237">False</span><span class="sxs-lookup"><span data-stu-id="63707-237">False</span></span> |

<span data-ttu-id="63707-238">Hallo volgende voorbeeld wordt **niet** met [gelijk is aan](resource-group-template-functions-comparison.md#equals).</span><span class="sxs-lookup"><span data-stu-id="63707-238">hello following example uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "checkNotEquals": {
            "type": "bool",
            "value": "[not(equals(1, 2))]"
        }
    }
```

<span data-ttu-id="63707-239">Hallo-uitvoer van het voorgaande voorbeeld Hallo is:</span><span class="sxs-lookup"><span data-stu-id="63707-239">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="63707-240">Naam</span><span class="sxs-lookup"><span data-stu-id="63707-240">Name</span></span> | <span data-ttu-id="63707-241">Type</span><span class="sxs-lookup"><span data-stu-id="63707-241">Type</span></span> | <span data-ttu-id="63707-242">Waarde</span><span class="sxs-lookup"><span data-stu-id="63707-242">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="63707-243">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="63707-243">checkNotEquals</span></span> | <span data-ttu-id="63707-244">BOOL</span><span class="sxs-lookup"><span data-stu-id="63707-244">Bool</span></span> | <span data-ttu-id="63707-245">True</span><span class="sxs-lookup"><span data-stu-id="63707-245">True</span></span> |


## <a name="or"></a><span data-ttu-id="63707-246">of</span><span class="sxs-lookup"><span data-stu-id="63707-246">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="63707-247">Controleert of de waarde voor de parameter ingesteld op true is.</span><span class="sxs-lookup"><span data-stu-id="63707-247">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="63707-248">Parameters</span><span class="sxs-lookup"><span data-stu-id="63707-248">Parameters</span></span>

| <span data-ttu-id="63707-249">Parameter</span><span class="sxs-lookup"><span data-stu-id="63707-249">Parameter</span></span> | <span data-ttu-id="63707-250">Vereist</span><span class="sxs-lookup"><span data-stu-id="63707-250">Required</span></span> | <span data-ttu-id="63707-251">Type</span><span class="sxs-lookup"><span data-stu-id="63707-251">Type</span></span> | <span data-ttu-id="63707-252">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="63707-252">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="63707-253">Arg1</span><span class="sxs-lookup"><span data-stu-id="63707-253">arg1</span></span> |<span data-ttu-id="63707-254">Ja</span><span class="sxs-lookup"><span data-stu-id="63707-254">Yes</span></span> |<span data-ttu-id="63707-255">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="63707-255">boolean</span></span> |<span data-ttu-id="63707-256">eerste waarde toocheck of Hallo is ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="63707-256">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="63707-257">Arg2</span><span class="sxs-lookup"><span data-stu-id="63707-257">arg2</span></span> |<span data-ttu-id="63707-258">Ja</span><span class="sxs-lookup"><span data-stu-id="63707-258">Yes</span></span> |<span data-ttu-id="63707-259">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="63707-259">boolean</span></span> |<span data-ttu-id="63707-260">tweede waarde toocheck of Hallo is ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="63707-260">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="63707-261">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="63707-261">Return value</span></span>

<span data-ttu-id="63707-262">Retourneert **True** als de waarde true, anders wordt is **False**.</span><span class="sxs-lookup"><span data-stu-id="63707-262">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="63707-263">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="63707-263">Examples</span></span>

<span data-ttu-id="63707-264">Hallo volgende voorbeeld ziet u hoe logische toouse-functies.</span><span class="sxs-lookup"><span data-stu-id="63707-264">hello following example shows how toouse logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="63707-265">Hallo-uitvoer van het voorgaande voorbeeld Hallo is:</span><span class="sxs-lookup"><span data-stu-id="63707-265">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="63707-266">Naam</span><span class="sxs-lookup"><span data-stu-id="63707-266">Name</span></span> | <span data-ttu-id="63707-267">Type</span><span class="sxs-lookup"><span data-stu-id="63707-267">Type</span></span> | <span data-ttu-id="63707-268">Waarde</span><span class="sxs-lookup"><span data-stu-id="63707-268">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="63707-269">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="63707-269">andExampleOutput</span></span> | <span data-ttu-id="63707-270">BOOL</span><span class="sxs-lookup"><span data-stu-id="63707-270">Bool</span></span> | <span data-ttu-id="63707-271">False</span><span class="sxs-lookup"><span data-stu-id="63707-271">False</span></span> |
| <span data-ttu-id="63707-272">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="63707-272">orExampleOutput</span></span> | <span data-ttu-id="63707-273">BOOL</span><span class="sxs-lookup"><span data-stu-id="63707-273">Bool</span></span> | <span data-ttu-id="63707-274">True</span><span class="sxs-lookup"><span data-stu-id="63707-274">True</span></span> |
| <span data-ttu-id="63707-275">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="63707-275">notExampleOutput</span></span> | <span data-ttu-id="63707-276">BOOL</span><span class="sxs-lookup"><span data-stu-id="63707-276">Bool</span></span> | <span data-ttu-id="63707-277">False</span><span class="sxs-lookup"><span data-stu-id="63707-277">False</span></span> |


## <a name="next-steps"></a><span data-ttu-id="63707-278">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="63707-278">Next steps</span></span>
* <span data-ttu-id="63707-279">Zie voor een beschrijving van de secties Hallo in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="63707-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="63707-280">toomerge meerdere sjablonen Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="63707-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="63707-281">een opgegeven aantal keren tooiterate bij het maken van een type resource, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="63707-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="63707-282">toosee hoe toodeploy Hallo sjabloon die u hebt gemaakt, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="63707-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

