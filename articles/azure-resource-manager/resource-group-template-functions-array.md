---
title: Azure Resource Manager-sjabloon fungeert - matrices en objecten | Microsoft Docs
description: Beschrijft de functies te gebruiken in een Azure Resource Manager-sjabloon voor het werken met matrices en objecten.
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
ms.date: 06/12/2017
ms.author: tomfitz
ms.openlocfilehash: 0bd9ec41761c9ce575f3bcf4d1f8e8578b83e01c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="de51b-103">Matrix en object-functies voor Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="de51b-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="de51b-104">Resource Manager biedt een aantal functies voor het werken met matrices en objecten.</span><span class="sxs-lookup"><span data-stu-id="de51b-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="de51b-105">matrix</span><span class="sxs-lookup"><span data-stu-id="de51b-105">array</span></span>](#array)
* [<span data-ttu-id="de51b-106">coalesce</span><span class="sxs-lookup"><span data-stu-id="de51b-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="de51b-107">concat</span><span class="sxs-lookup"><span data-stu-id="de51b-107">concat</span></span>](#concat)
* [<span data-ttu-id="de51b-108">bevat</span><span class="sxs-lookup"><span data-stu-id="de51b-108">contains</span></span>](#contains)
* [<span data-ttu-id="de51b-109">createArray</span><span class="sxs-lookup"><span data-stu-id="de51b-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="de51b-110">leeg</span><span class="sxs-lookup"><span data-stu-id="de51b-110">empty</span></span>](#empty)
* [<span data-ttu-id="de51b-111">eerste</span><span class="sxs-lookup"><span data-stu-id="de51b-111">first</span></span>](#first)
* [<span data-ttu-id="de51b-112">snijpunt</span><span class="sxs-lookup"><span data-stu-id="de51b-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="de51b-113">JSON</span><span class="sxs-lookup"><span data-stu-id="de51b-113">json</span></span>](#json)
* [<span data-ttu-id="de51b-114">laatste</span><span class="sxs-lookup"><span data-stu-id="de51b-114">last</span></span>](#last)
* [<span data-ttu-id="de51b-115">lengte</span><span class="sxs-lookup"><span data-stu-id="de51b-115">length</span></span>](#length)
* [<span data-ttu-id="de51b-116">min</span><span class="sxs-lookup"><span data-stu-id="de51b-116">min</span></span>](#min)
* [<span data-ttu-id="de51b-117">maximale</span><span class="sxs-lookup"><span data-stu-id="de51b-117">max</span></span>](#max)
* [<span data-ttu-id="de51b-118">bereik</span><span class="sxs-lookup"><span data-stu-id="de51b-118">range</span></span>](#range)
* [<span data-ttu-id="de51b-119">overslaan</span><span class="sxs-lookup"><span data-stu-id="de51b-119">skip</span></span>](#skip)
* [<span data-ttu-id="de51b-120">duren</span><span class="sxs-lookup"><span data-stu-id="de51b-120">take</span></span>](#take)
* [<span data-ttu-id="de51b-121">Union</span><span class="sxs-lookup"><span data-stu-id="de51b-121">union</span></span>](#union)

<span data-ttu-id="de51b-122">Als u een matrix van tekenreekswaarden gescheiden door een waarde, Zie [splitsen](resource-group-template-functions-string.md#split).</span><span class="sxs-lookup"><span data-stu-id="de51b-122">To get an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="de51b-123">matrix</span><span class="sxs-lookup"><span data-stu-id="de51b-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="de51b-124">De waarde wordt omgezet in een matrix.</span><span class="sxs-lookup"><span data-stu-id="de51b-124">Converts the value to an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="de51b-125">Parameters</span><span class="sxs-lookup"><span data-stu-id="de51b-125">Parameters</span></span>

| <span data-ttu-id="de51b-126">Parameter</span><span class="sxs-lookup"><span data-stu-id="de51b-126">Parameter</span></span> | <span data-ttu-id="de51b-127">Vereist</span><span class="sxs-lookup"><span data-stu-id="de51b-127">Required</span></span> | <span data-ttu-id="de51b-128">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-128">Type</span></span> | <span data-ttu-id="de51b-129">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de51b-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="de51b-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="de51b-130">convertToArray</span></span> |<span data-ttu-id="de51b-131">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-131">Yes</span></span> |<span data-ttu-id="de51b-132">int, string, matrix of object</span><span class="sxs-lookup"><span data-stu-id="de51b-132">int, string, array, or object</span></span> |<span data-ttu-id="de51b-133">De waarde te converteren naar een matrix.</span><span class="sxs-lookup"><span data-stu-id="de51b-133">The value to convert to an array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="de51b-134">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="de51b-134">Return value</span></span>

<span data-ttu-id="de51b-135">Een matrix.</span><span class="sxs-lookup"><span data-stu-id="de51b-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="de51b-136">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="de51b-136">Example</span></span>

<span data-ttu-id="de51b-137">Het volgende voorbeeld ziet hoe u de functie array met verschillende typen.</span><span class="sxs-lookup"><span data-stu-id="de51b-137">The following example shows how to use the array function with different types.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "intToConvert": {
            "type": "int",
            "defaultValue": 1
        },
        "stringToConvert": {
            "type": "string",
            "defaultValue": "a"
        },
        "objectToConvert": {
            "type": "object",
            "defaultValue": {"a": "b", "c": "d"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "intOutput": {
            "type": "array",
            "value": "[array(parameters('intToConvert'))]"
        },
        "stringOutput": {
            "type": "array",
            "value": "[array(parameters('stringToConvert'))]"
        },
        "objectOutput": {
            "type": "array",
            "value": "[array(parameters('objectToConvert'))]"
        }
    }
}
```

<span data-ttu-id="de51b-138">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-138">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-139">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-139">Name</span></span> | <span data-ttu-id="de51b-140">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-140">Type</span></span> | <span data-ttu-id="de51b-141">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-142">intOutput</span></span> | <span data-ttu-id="de51b-143">matrix</span><span class="sxs-lookup"><span data-stu-id="de51b-143">Array</span></span> | <span data-ttu-id="de51b-144">[1]</span><span class="sxs-lookup"><span data-stu-id="de51b-144">[1]</span></span> |
| <span data-ttu-id="de51b-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-145">stringOutput</span></span> | <span data-ttu-id="de51b-146">matrix</span><span class="sxs-lookup"><span data-stu-id="de51b-146">Array</span></span> | <span data-ttu-id="de51b-147">["a"]</span><span class="sxs-lookup"><span data-stu-id="de51b-147">["a"]</span></span> |
| <span data-ttu-id="de51b-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-148">objectOutput</span></span> | <span data-ttu-id="de51b-149">matrix</span><span class="sxs-lookup"><span data-stu-id="de51b-149">Array</span></span> | <span data-ttu-id="de51b-150">[{"a": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="de51b-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="de51b-151">Coalesce</span><span class="sxs-lookup"><span data-stu-id="de51b-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="de51b-152">Retourneert de eerste niet-null-waarde van de parameters.</span><span class="sxs-lookup"><span data-stu-id="de51b-152">Returns first non-null value from the parameters.</span></span> <span data-ttu-id="de51b-153">Lege tekenreeksen, matrices leeg en lege objecten zijn niet null.</span><span class="sxs-lookup"><span data-stu-id="de51b-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="de51b-154">Parameters</span><span class="sxs-lookup"><span data-stu-id="de51b-154">Parameters</span></span>

| <span data-ttu-id="de51b-155">Parameter</span><span class="sxs-lookup"><span data-stu-id="de51b-155">Parameter</span></span> | <span data-ttu-id="de51b-156">Vereist</span><span class="sxs-lookup"><span data-stu-id="de51b-156">Required</span></span> | <span data-ttu-id="de51b-157">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-157">Type</span></span> | <span data-ttu-id="de51b-158">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de51b-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="de51b-159">Arg1</span><span class="sxs-lookup"><span data-stu-id="de51b-159">arg1</span></span> |<span data-ttu-id="de51b-160">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-160">Yes</span></span> |<span data-ttu-id="de51b-161">int, string, matrix of object</span><span class="sxs-lookup"><span data-stu-id="de51b-161">int, string, array, or object</span></span> |<span data-ttu-id="de51b-162">De eerste waarde om te controleren op null.</span><span class="sxs-lookup"><span data-stu-id="de51b-162">The first value to test for null.</span></span> |
| <span data-ttu-id="de51b-163">Als u meer argumenten</span><span class="sxs-lookup"><span data-stu-id="de51b-163">additional args</span></span> |<span data-ttu-id="de51b-164">Nee</span><span class="sxs-lookup"><span data-stu-id="de51b-164">No</span></span> |<span data-ttu-id="de51b-165">int, string, matrix of object</span><span class="sxs-lookup"><span data-stu-id="de51b-165">int, string, array, or object</span></span> |<span data-ttu-id="de51b-166">Aanvullende waarden testen op null.</span><span class="sxs-lookup"><span data-stu-id="de51b-166">Additional values to test for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="de51b-167">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="de51b-167">Return value</span></span>

<span data-ttu-id="de51b-168">De waarde van de eerste niet-null-parameters, dit kan een string, int, matrix of object.</span><span class="sxs-lookup"><span data-stu-id="de51b-168">The value of the first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="de51b-169">Null als alle parameters leeg zijn.</span><span class="sxs-lookup"><span data-stu-id="de51b-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="de51b-170">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="de51b-170">Example</span></span>

<span data-ttu-id="de51b-171">Het volgende voorbeeld ziet de uitvoer van verschillende coalesce worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="de51b-171">The following example shows the output from different uses of coalesce.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {
                "null1": null, 
                "null2": null,
                "string": "default",
                "int": 1,
                "object": {"first": "default"},
                "array": [1]
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').string)]"
        },
        "intOutput": {
            "type": "int",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').int)]"
        },
        "objectOutput": {
            "type": "object",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').object)]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').array)]"
        },
        "emptyOutput": {
            "type": "bool",
            "value": "[empty(coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2))]"
        }
    }
}
```

<span data-ttu-id="de51b-172">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-172">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-173">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-173">Name</span></span> | <span data-ttu-id="de51b-174">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-174">Type</span></span> | <span data-ttu-id="de51b-175">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-176">stringOutput</span></span> | <span data-ttu-id="de51b-177">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-177">String</span></span> | <span data-ttu-id="de51b-178">Standaard</span><span class="sxs-lookup"><span data-stu-id="de51b-178">default</span></span> |
| <span data-ttu-id="de51b-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-179">intOutput</span></span> | <span data-ttu-id="de51b-180">int</span><span class="sxs-lookup"><span data-stu-id="de51b-180">Int</span></span> | <span data-ttu-id="de51b-181">1</span><span class="sxs-lookup"><span data-stu-id="de51b-181">1</span></span> |
| <span data-ttu-id="de51b-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-182">objectOutput</span></span> | <span data-ttu-id="de51b-183">Object</span><span class="sxs-lookup"><span data-stu-id="de51b-183">Object</span></span> | <span data-ttu-id="de51b-184">{{'eerste': 'standaard'}</span><span class="sxs-lookup"><span data-stu-id="de51b-184">{"first": "default"}</span></span> |
| <span data-ttu-id="de51b-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-185">arrayOutput</span></span> | <span data-ttu-id="de51b-186">matrix</span><span class="sxs-lookup"><span data-stu-id="de51b-186">Array</span></span> | <span data-ttu-id="de51b-187">[1]</span><span class="sxs-lookup"><span data-stu-id="de51b-187">[1]</span></span> |
| <span data-ttu-id="de51b-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-188">emptyOutput</span></span> | <span data-ttu-id="de51b-189">BOOL</span><span class="sxs-lookup"><span data-stu-id="de51b-189">Bool</span></span> | <span data-ttu-id="de51b-190">True</span><span class="sxs-lookup"><span data-stu-id="de51b-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="de51b-191">concat</span><span class="sxs-lookup"><span data-stu-id="de51b-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="de51b-192">Combineert meerdere matrices en retourneert de aaneengeschakelde matrix of combineert meerdere tekenreekswaarden en retourneert de samengevoegde tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="de51b-192">Combines multiple arrays and returns the concatenated array, or combines multiple string values and returns the concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="de51b-193">Parameters</span><span class="sxs-lookup"><span data-stu-id="de51b-193">Parameters</span></span>

| <span data-ttu-id="de51b-194">Parameter</span><span class="sxs-lookup"><span data-stu-id="de51b-194">Parameter</span></span> | <span data-ttu-id="de51b-195">Vereist</span><span class="sxs-lookup"><span data-stu-id="de51b-195">Required</span></span> | <span data-ttu-id="de51b-196">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-196">Type</span></span> | <span data-ttu-id="de51b-197">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de51b-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="de51b-198">Arg1</span><span class="sxs-lookup"><span data-stu-id="de51b-198">arg1</span></span> |<span data-ttu-id="de51b-199">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-199">Yes</span></span> |<span data-ttu-id="de51b-200">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-200">array or string</span></span> |<span data-ttu-id="de51b-201">De eerste matrix of tekenreeks op voor de samenvoeging.</span><span class="sxs-lookup"><span data-stu-id="de51b-201">The first array or string for concatenation.</span></span> |
| <span data-ttu-id="de51b-202">Extra argumenten</span><span class="sxs-lookup"><span data-stu-id="de51b-202">additional arguments</span></span> |<span data-ttu-id="de51b-203">Nee</span><span class="sxs-lookup"><span data-stu-id="de51b-203">No</span></span> |<span data-ttu-id="de51b-204">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-204">array or string</span></span> |<span data-ttu-id="de51b-205">Aanvullende matrices of tekenreeksen in opeenvolgende volgorde voor de samenvoeging.</span><span class="sxs-lookup"><span data-stu-id="de51b-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="de51b-206">Deze functie kan duren voordat een willekeurig aantal argumenten en tekenreeksen of matrices voor de parameters kan accepteren.</span><span class="sxs-lookup"><span data-stu-id="de51b-206">This function can take any number of arguments, and can accept either strings or arrays for the parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="de51b-207">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="de51b-207">Return value</span></span>
<span data-ttu-id="de51b-208">Een tekenreeks of matrix met samengevoegde waarden.</span><span class="sxs-lookup"><span data-stu-id="de51b-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="de51b-209">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="de51b-209">Example</span></span>

<span data-ttu-id="de51b-210">Het volgende voorbeeld ziet twee matrices combineren.</span><span class="sxs-lookup"><span data-stu-id="de51b-210">The following example shows how to combine two arrays.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "firstArray": { 
            "type": "array", 
            "defaultValue": [ 
                "1-1", 
                "1-2", 
                "1-3" 
            ] 
        },
        "secondArray": {
            "type": "array", 
            "defaultValue": [ 
                "2-1", 
                "2-2",
                "2-3" 
            ] 
        }
    },
    "resources": [
    ],
    "outputs": {
        "return": {
            "type": "array",
            "value": "[concat(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="de51b-211">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-211">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-212">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-212">Name</span></span> | <span data-ttu-id="de51b-213">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-213">Type</span></span> | <span data-ttu-id="de51b-214">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-215">retourneren</span><span class="sxs-lookup"><span data-stu-id="de51b-215">return</span></span> | <span data-ttu-id="de51b-216">matrix</span><span class="sxs-lookup"><span data-stu-id="de51b-216">Array</span></span> | <span data-ttu-id="de51b-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="de51b-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="de51b-218">Het volgende voorbeeld laat zien hoe het combineren van twee tekenreekswaarden zoals en een samengevoegde tekenreeks retourneren.</span><span class="sxs-lookup"><span data-stu-id="de51b-218">The following example shows how to combine two string values and return a concatenated string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "prefix": {
            "type": "string",
            "defaultValue": "prefix"
        }
    },
    "resources": [],
    "outputs": {
        "concatOutput": {
            "value": "[concat(parameters('prefix'), '-', uniqueString(resourceGroup().id))]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="de51b-219">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-219">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-220">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-220">Name</span></span> | <span data-ttu-id="de51b-221">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-221">Type</span></span> | <span data-ttu-id="de51b-222">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-223">concatOutput</span></span> | <span data-ttu-id="de51b-224">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-224">String</span></span> | <span data-ttu-id="de51b-225">voorvoegsel 5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="de51b-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="de51b-226">Bevat</span><span class="sxs-lookup"><span data-stu-id="de51b-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="de51b-227">Controleert of een matrix een waarde bevat, een object een sleutel bevat of een tekenreeks een subtekenreeks bevat.</span><span class="sxs-lookup"><span data-stu-id="de51b-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="de51b-228">Parameters</span><span class="sxs-lookup"><span data-stu-id="de51b-228">Parameters</span></span>

| <span data-ttu-id="de51b-229">Parameter</span><span class="sxs-lookup"><span data-stu-id="de51b-229">Parameter</span></span> | <span data-ttu-id="de51b-230">Vereist</span><span class="sxs-lookup"><span data-stu-id="de51b-230">Required</span></span> | <span data-ttu-id="de51b-231">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-231">Type</span></span> | <span data-ttu-id="de51b-232">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de51b-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="de51b-233">container</span><span class="sxs-lookup"><span data-stu-id="de51b-233">container</span></span> |<span data-ttu-id="de51b-234">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-234">Yes</span></span> |<span data-ttu-id="de51b-235">Array, object of een tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-235">array, object, or string</span></span> |<span data-ttu-id="de51b-236">De waarde met de waarde om te zoeken.</span><span class="sxs-lookup"><span data-stu-id="de51b-236">The value that contains the value to find.</span></span> |
| <span data-ttu-id="de51b-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="de51b-237">itemToFind</span></span> |<span data-ttu-id="de51b-238">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-238">Yes</span></span> |<span data-ttu-id="de51b-239">String of int.</span><span class="sxs-lookup"><span data-stu-id="de51b-239">string or int</span></span> |<span data-ttu-id="de51b-240">De waarde om te zoeken.</span><span class="sxs-lookup"><span data-stu-id="de51b-240">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="de51b-241">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="de51b-241">Return value</span></span>

<span data-ttu-id="de51b-242">**De waarde True** als het item gevonden, anders wordt is **False**.</span><span class="sxs-lookup"><span data-stu-id="de51b-242">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="de51b-243">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="de51b-243">Example</span></span>

<span data-ttu-id="de51b-244">Het volgende voorbeeld ziet u hoe u bevat met verschillende typen:</span><span class="sxs-lookup"><span data-stu-id="de51b-244">The following example shows how to use contains with different types:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "OneTwoThree"
        },
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringTrue": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'e')]"
        },
        "stringFalse": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'z')]"
        },
        "objectTrue": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'one')]"
        },
        "objectFalse": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'a')]"
        },
        "arrayTrue": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'three')]"
        },
        "arrayFalse": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'four')]"
        }
    }
}
```

<span data-ttu-id="de51b-245">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-245">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-246">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-246">Name</span></span> | <span data-ttu-id="de51b-247">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-247">Type</span></span> | <span data-ttu-id="de51b-248">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="de51b-249">stringTrue</span></span> | <span data-ttu-id="de51b-250">BOOL</span><span class="sxs-lookup"><span data-stu-id="de51b-250">Bool</span></span> | <span data-ttu-id="de51b-251">True</span><span class="sxs-lookup"><span data-stu-id="de51b-251">True</span></span> |
| <span data-ttu-id="de51b-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="de51b-252">stringFalse</span></span> | <span data-ttu-id="de51b-253">BOOL</span><span class="sxs-lookup"><span data-stu-id="de51b-253">Bool</span></span> | <span data-ttu-id="de51b-254">False</span><span class="sxs-lookup"><span data-stu-id="de51b-254">False</span></span> |
| <span data-ttu-id="de51b-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="de51b-255">objectTrue</span></span> | <span data-ttu-id="de51b-256">BOOL</span><span class="sxs-lookup"><span data-stu-id="de51b-256">Bool</span></span> | <span data-ttu-id="de51b-257">True</span><span class="sxs-lookup"><span data-stu-id="de51b-257">True</span></span> |
| <span data-ttu-id="de51b-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="de51b-258">objectFalse</span></span> | <span data-ttu-id="de51b-259">BOOL</span><span class="sxs-lookup"><span data-stu-id="de51b-259">Bool</span></span> | <span data-ttu-id="de51b-260">False</span><span class="sxs-lookup"><span data-stu-id="de51b-260">False</span></span> |
| <span data-ttu-id="de51b-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="de51b-261">arrayTrue</span></span> | <span data-ttu-id="de51b-262">BOOL</span><span class="sxs-lookup"><span data-stu-id="de51b-262">Bool</span></span> | <span data-ttu-id="de51b-263">True</span><span class="sxs-lookup"><span data-stu-id="de51b-263">True</span></span> |
| <span data-ttu-id="de51b-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="de51b-264">arrayFalse</span></span> | <span data-ttu-id="de51b-265">BOOL</span><span class="sxs-lookup"><span data-stu-id="de51b-265">Bool</span></span> | <span data-ttu-id="de51b-266">False</span><span class="sxs-lookup"><span data-stu-id="de51b-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="de51b-267">createarray</span><span class="sxs-lookup"><span data-stu-id="de51b-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="de51b-268">Maakt een matrix van de parameters.</span><span class="sxs-lookup"><span data-stu-id="de51b-268">Creates an array from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="de51b-269">Parameters</span><span class="sxs-lookup"><span data-stu-id="de51b-269">Parameters</span></span>

| <span data-ttu-id="de51b-270">Parameter</span><span class="sxs-lookup"><span data-stu-id="de51b-270">Parameter</span></span> | <span data-ttu-id="de51b-271">Vereist</span><span class="sxs-lookup"><span data-stu-id="de51b-271">Required</span></span> | <span data-ttu-id="de51b-272">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-272">Type</span></span> | <span data-ttu-id="de51b-273">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de51b-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="de51b-274">Arg1</span><span class="sxs-lookup"><span data-stu-id="de51b-274">arg1</span></span> |<span data-ttu-id="de51b-275">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-275">Yes</span></span> |<span data-ttu-id="de51b-276">Tekenreeks, geheel getal, matrix of Object</span><span class="sxs-lookup"><span data-stu-id="de51b-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="de51b-277">De eerste waarde in de matrix.</span><span class="sxs-lookup"><span data-stu-id="de51b-277">The first value in the array.</span></span> |
| <span data-ttu-id="de51b-278">Extra argumenten</span><span class="sxs-lookup"><span data-stu-id="de51b-278">additional arguments</span></span> |<span data-ttu-id="de51b-279">Nee</span><span class="sxs-lookup"><span data-stu-id="de51b-279">No</span></span> |<span data-ttu-id="de51b-280">Tekenreeks, geheel getal, matrix of Object</span><span class="sxs-lookup"><span data-stu-id="de51b-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="de51b-281">Aanvullende waarden in de matrix.</span><span class="sxs-lookup"><span data-stu-id="de51b-281">Additional values in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="de51b-282">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="de51b-282">Return value</span></span>

<span data-ttu-id="de51b-283">Een matrix.</span><span class="sxs-lookup"><span data-stu-id="de51b-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="de51b-284">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="de51b-284">Example</span></span>

<span data-ttu-id="de51b-285">Het volgende voorbeeld ziet hoe u createArray met verschillende typen:</span><span class="sxs-lookup"><span data-stu-id="de51b-285">The following example shows how to use createArray with different types:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringArray": {
            "type": "array",
            "value": "[createArray('a', 'b', 'c')]"
        },
        "intArray": {
            "type": "array",
            "value": "[createArray(1, 2, 3)]"
        },
        "objectArray": {
            "type": "array",
            "value": "[createArray(parameters('objectToTest'))]"
        },
        "arrayArray": {
            "type": "array",
            "value": "[createArray(parameters('arrayToTest'))]"
        }
    }
}
```

<span data-ttu-id="de51b-286">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-286">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-287">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-287">Name</span></span> | <span data-ttu-id="de51b-288">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-288">Type</span></span> | <span data-ttu-id="de51b-289">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-290">stringArray</span><span class="sxs-lookup"><span data-stu-id="de51b-290">stringArray</span></span> | <span data-ttu-id="de51b-291">matrix</span><span class="sxs-lookup"><span data-stu-id="de51b-291">Array</span></span> | <span data-ttu-id="de51b-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="de51b-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="de51b-293">intArray</span><span class="sxs-lookup"><span data-stu-id="de51b-293">intArray</span></span> | <span data-ttu-id="de51b-294">matrix</span><span class="sxs-lookup"><span data-stu-id="de51b-294">Array</span></span> | <span data-ttu-id="de51b-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="de51b-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="de51b-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="de51b-296">objectArray</span></span> | <span data-ttu-id="de51b-297">matrix</span><span class="sxs-lookup"><span data-stu-id="de51b-297">Array</span></span> | <span data-ttu-id="de51b-298">[{"een": "a", "twee": "b", "drie": "c"}]</span><span class="sxs-lookup"><span data-stu-id="de51b-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="de51b-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="de51b-299">arrayArray</span></span> | <span data-ttu-id="de51b-300">matrix</span><span class="sxs-lookup"><span data-stu-id="de51b-300">Array</span></span> | <span data-ttu-id="de51b-301">[[' een', 'twee', 'drie']]</span><span class="sxs-lookup"><span data-stu-id="de51b-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="de51b-302">leeg</span><span class="sxs-lookup"><span data-stu-id="de51b-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="de51b-303">Hiermee wordt bepaald of een matrix, een object of een tekenreeks leeg is.</span><span class="sxs-lookup"><span data-stu-id="de51b-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="de51b-304">Parameters</span><span class="sxs-lookup"><span data-stu-id="de51b-304">Parameters</span></span>

| <span data-ttu-id="de51b-305">Parameter</span><span class="sxs-lookup"><span data-stu-id="de51b-305">Parameter</span></span> | <span data-ttu-id="de51b-306">Vereist</span><span class="sxs-lookup"><span data-stu-id="de51b-306">Required</span></span> | <span data-ttu-id="de51b-307">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-307">Type</span></span> | <span data-ttu-id="de51b-308">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de51b-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="de51b-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="de51b-309">itemToTest</span></span> |<span data-ttu-id="de51b-310">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-310">Yes</span></span> |<span data-ttu-id="de51b-311">Array, object of een tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-311">array, object, or string</span></span> |<span data-ttu-id="de51b-312">De waarde om te controleren als deze leeg is.</span><span class="sxs-lookup"><span data-stu-id="de51b-312">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="de51b-313">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="de51b-313">Return value</span></span>

<span data-ttu-id="de51b-314">Retourneert **True** als de waarde leeg, anders wordt is **False**.</span><span class="sxs-lookup"><span data-stu-id="de51b-314">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="de51b-315">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="de51b-315">Example</span></span>

<span data-ttu-id="de51b-316">Het volgende voorbeeld wordt gecontroleerd of een matrix, het object en de tekenreeks leeg zijn.</span><span class="sxs-lookup"><span data-stu-id="de51b-316">The following example checks whether an array, object, and string are empty.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": []
        },
        "testObject": {
            "type": "object",
            "defaultValue": {}
        },
        "testString": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testArray'))]"
        },
        "objectEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testObject'))]"
        },
        "stringEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="de51b-317">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-317">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-318">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-318">Name</span></span> | <span data-ttu-id="de51b-319">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-319">Type</span></span> | <span data-ttu-id="de51b-320">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="de51b-321">arrayEmpty</span></span> | <span data-ttu-id="de51b-322">BOOL</span><span class="sxs-lookup"><span data-stu-id="de51b-322">Bool</span></span> | <span data-ttu-id="de51b-323">True</span><span class="sxs-lookup"><span data-stu-id="de51b-323">True</span></span> |
| <span data-ttu-id="de51b-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="de51b-324">objectEmpty</span></span> | <span data-ttu-id="de51b-325">BOOL</span><span class="sxs-lookup"><span data-stu-id="de51b-325">Bool</span></span> | <span data-ttu-id="de51b-326">True</span><span class="sxs-lookup"><span data-stu-id="de51b-326">True</span></span> |
| <span data-ttu-id="de51b-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="de51b-327">stringEmpty</span></span> | <span data-ttu-id="de51b-328">BOOL</span><span class="sxs-lookup"><span data-stu-id="de51b-328">Bool</span></span> | <span data-ttu-id="de51b-329">True</span><span class="sxs-lookup"><span data-stu-id="de51b-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="de51b-330">eerste</span><span class="sxs-lookup"><span data-stu-id="de51b-330">first</span></span>
`first(arg1)`

<span data-ttu-id="de51b-331">Retourneert het eerste element van de matrix of het eerste teken van de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="de51b-331">Returns the first element of the array, or first character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="de51b-332">Parameters</span><span class="sxs-lookup"><span data-stu-id="de51b-332">Parameters</span></span>

| <span data-ttu-id="de51b-333">Parameter</span><span class="sxs-lookup"><span data-stu-id="de51b-333">Parameter</span></span> | <span data-ttu-id="de51b-334">Vereist</span><span class="sxs-lookup"><span data-stu-id="de51b-334">Required</span></span> | <span data-ttu-id="de51b-335">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-335">Type</span></span> | <span data-ttu-id="de51b-336">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de51b-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="de51b-337">Arg1</span><span class="sxs-lookup"><span data-stu-id="de51b-337">arg1</span></span> |<span data-ttu-id="de51b-338">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-338">Yes</span></span> |<span data-ttu-id="de51b-339">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-339">array or string</span></span> |<span data-ttu-id="de51b-340">De waarde voor het ophalen van het eerste element of teken.</span><span class="sxs-lookup"><span data-stu-id="de51b-340">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="de51b-341">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="de51b-341">Return value</span></span>

<span data-ttu-id="de51b-342">Het type (string, int, matrix of object) van het eerste element in een matrix of het eerste teken van een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="de51b-342">The type (string, int, array, or object) of the first element in an array, or the first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="de51b-343">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="de51b-343">Example</span></span>

<span data-ttu-id="de51b-344">Het volgende voorbeeld ziet hoe u de eerste functie met een matrix en de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="de51b-344">The following example shows how to use the first function with an array and string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[first(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[first('One Two Three')]"
        }
    }
}
```

<span data-ttu-id="de51b-345">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-345">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-346">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-346">Name</span></span> | <span data-ttu-id="de51b-347">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-347">Type</span></span> | <span data-ttu-id="de51b-348">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-349">arrayOutput</span></span> | <span data-ttu-id="de51b-350">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-350">String</span></span> | <span data-ttu-id="de51b-351">een</span><span class="sxs-lookup"><span data-stu-id="de51b-351">one</span></span> |
| <span data-ttu-id="de51b-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-352">stringOutput</span></span> | <span data-ttu-id="de51b-353">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-353">String</span></span> | <span data-ttu-id="de51b-354">O</span><span class="sxs-lookup"><span data-stu-id="de51b-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="de51b-355">snijpunt</span><span class="sxs-lookup"><span data-stu-id="de51b-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="de51b-356">Retourneert een matrix of object met de algemene elementen van de parameters.</span><span class="sxs-lookup"><span data-stu-id="de51b-356">Returns a single array or object with the common elements from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="de51b-357">Parameters</span><span class="sxs-lookup"><span data-stu-id="de51b-357">Parameters</span></span>

| <span data-ttu-id="de51b-358">Parameter</span><span class="sxs-lookup"><span data-stu-id="de51b-358">Parameter</span></span> | <span data-ttu-id="de51b-359">Vereist</span><span class="sxs-lookup"><span data-stu-id="de51b-359">Required</span></span> | <span data-ttu-id="de51b-360">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-360">Type</span></span> | <span data-ttu-id="de51b-361">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de51b-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="de51b-362">Arg1</span><span class="sxs-lookup"><span data-stu-id="de51b-362">arg1</span></span> |<span data-ttu-id="de51b-363">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-363">Yes</span></span> |<span data-ttu-id="de51b-364">matrix of object</span><span class="sxs-lookup"><span data-stu-id="de51b-364">array or object</span></span> |<span data-ttu-id="de51b-365">De eerste waarde voor het zoeken naar algemene elementen.</span><span class="sxs-lookup"><span data-stu-id="de51b-365">The first value to use for finding common elements.</span></span> |
| <span data-ttu-id="de51b-366">Arg2</span><span class="sxs-lookup"><span data-stu-id="de51b-366">arg2</span></span> |<span data-ttu-id="de51b-367">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-367">Yes</span></span> |<span data-ttu-id="de51b-368">matrix of object</span><span class="sxs-lookup"><span data-stu-id="de51b-368">array or object</span></span> |<span data-ttu-id="de51b-369">De tweede waarde voor het zoeken naar algemene elementen.</span><span class="sxs-lookup"><span data-stu-id="de51b-369">The second value to use for finding common elements.</span></span> |
| <span data-ttu-id="de51b-370">Extra argumenten</span><span class="sxs-lookup"><span data-stu-id="de51b-370">additional arguments</span></span> |<span data-ttu-id="de51b-371">Nee</span><span class="sxs-lookup"><span data-stu-id="de51b-371">No</span></span> |<span data-ttu-id="de51b-372">matrix of object</span><span class="sxs-lookup"><span data-stu-id="de51b-372">array or object</span></span> |<span data-ttu-id="de51b-373">Aanvullende waarden gebruiken voor het zoeken naar algemene elementen.</span><span class="sxs-lookup"><span data-stu-id="de51b-373">Additional values to use for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="de51b-374">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="de51b-374">Return value</span></span>

<span data-ttu-id="de51b-375">Een matrix of object met de algemene elementen.</span><span class="sxs-lookup"><span data-stu-id="de51b-375">An array or object with the common elements.</span></span>

### <a name="example"></a><span data-ttu-id="de51b-376">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="de51b-376">Example</span></span>

<span data-ttu-id="de51b-377">Het volgende voorbeeld ziet hoe u snijpunt met matrices en objecten:</span><span class="sxs-lookup"><span data-stu-id="de51b-377">The following example shows how to use intersection with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "z", "three": "c"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[intersection(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[intersection(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="de51b-378">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-378">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-379">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-379">Name</span></span> | <span data-ttu-id="de51b-380">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-380">Type</span></span> | <span data-ttu-id="de51b-381">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-382">objectOutput</span></span> | <span data-ttu-id="de51b-383">Object</span><span class="sxs-lookup"><span data-stu-id="de51b-383">Object</span></span> | <span data-ttu-id="de51b-384">{"een": "a", "3": "c"}</span><span class="sxs-lookup"><span data-stu-id="de51b-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="de51b-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-385">arrayOutput</span></span> | <span data-ttu-id="de51b-386">matrix</span><span class="sxs-lookup"><span data-stu-id="de51b-386">Array</span></span> | <span data-ttu-id="de51b-387">["twee", "drie"]</span><span class="sxs-lookup"><span data-stu-id="de51b-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="de51b-388">JSON</span><span class="sxs-lookup"><span data-stu-id="de51b-388">json</span></span>
`json(arg1)`

<span data-ttu-id="de51b-389">Retourneert een JSON-object.</span><span class="sxs-lookup"><span data-stu-id="de51b-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="de51b-390">Parameters</span><span class="sxs-lookup"><span data-stu-id="de51b-390">Parameters</span></span>

| <span data-ttu-id="de51b-391">Parameter</span><span class="sxs-lookup"><span data-stu-id="de51b-391">Parameter</span></span> | <span data-ttu-id="de51b-392">Vereist</span><span class="sxs-lookup"><span data-stu-id="de51b-392">Required</span></span> | <span data-ttu-id="de51b-393">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-393">Type</span></span> | <span data-ttu-id="de51b-394">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de51b-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="de51b-395">Arg1</span><span class="sxs-lookup"><span data-stu-id="de51b-395">arg1</span></span> |<span data-ttu-id="de51b-396">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-396">Yes</span></span> |<span data-ttu-id="de51b-397">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-397">string</span></span> |<span data-ttu-id="de51b-398">De waarde niet converteren naar JSON.</span><span class="sxs-lookup"><span data-stu-id="de51b-398">The value to convert to JSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="de51b-399">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="de51b-399">Return value</span></span>

<span data-ttu-id="de51b-400">De JSON-object van de opgegeven tekenreeks of een leeg object wanneer **null** is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="de51b-400">The JSON object from the specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="de51b-401">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="de51b-401">Example</span></span>

<span data-ttu-id="de51b-402">Het volgende voorbeeld ziet hoe u snijpunt met matrices en objecten:</span><span class="sxs-lookup"><span data-stu-id="de51b-402">The following example shows how to use intersection with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "jsonOutput": {
            "type": "object",
            "value": "[json('{\"a\": \"b\"}')]"
        },
        "nullOutput": {
            "type": "bool",
            "value": "[empty(json('null'))]"
        }
    }
}
```

<span data-ttu-id="de51b-403">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-403">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-404">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-404">Name</span></span> | <span data-ttu-id="de51b-405">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-405">Type</span></span> | <span data-ttu-id="de51b-406">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-407">jsonOutput</span></span> | <span data-ttu-id="de51b-408">Object</span><span class="sxs-lookup"><span data-stu-id="de51b-408">Object</span></span> | <span data-ttu-id="de51b-409">{"a": "b"}</span><span class="sxs-lookup"><span data-stu-id="de51b-409">{"a": "b"}</span></span> |
| <span data-ttu-id="de51b-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-410">nullOutput</span></span> | <span data-ttu-id="de51b-411">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-411">Boolean</span></span> | <span data-ttu-id="de51b-412">True</span><span class="sxs-lookup"><span data-stu-id="de51b-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="de51b-413">laatste</span><span class="sxs-lookup"><span data-stu-id="de51b-413">last</span></span>
`last (arg1)`

<span data-ttu-id="de51b-414">Retourneert het laatste element van de matrix of laatste teken van de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="de51b-414">Returns the last element of the array, or last character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="de51b-415">Parameters</span><span class="sxs-lookup"><span data-stu-id="de51b-415">Parameters</span></span>

| <span data-ttu-id="de51b-416">Parameter</span><span class="sxs-lookup"><span data-stu-id="de51b-416">Parameter</span></span> | <span data-ttu-id="de51b-417">Vereist</span><span class="sxs-lookup"><span data-stu-id="de51b-417">Required</span></span> | <span data-ttu-id="de51b-418">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-418">Type</span></span> | <span data-ttu-id="de51b-419">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de51b-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="de51b-420">Arg1</span><span class="sxs-lookup"><span data-stu-id="de51b-420">arg1</span></span> |<span data-ttu-id="de51b-421">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-421">Yes</span></span> |<span data-ttu-id="de51b-422">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-422">array or string</span></span> |<span data-ttu-id="de51b-423">De waarde voor het ophalen van het laatste element of teken.</span><span class="sxs-lookup"><span data-stu-id="de51b-423">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="de51b-424">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="de51b-424">Return value</span></span>

<span data-ttu-id="de51b-425">Het type (string, int, matrix of object) van het laatste element in een matrix of het laatste teken van een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="de51b-425">The type (string, int, array, or object) of the last element in an array, or the last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="de51b-426">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="de51b-426">Example</span></span>

<span data-ttu-id="de51b-427">Het volgende voorbeeld ziet hoe u de laatste functie met een matrix en de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="de51b-427">The following example shows how to use the last function with an array and string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[last(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[last('One Two Three')]"
        }
    }
}
```

<span data-ttu-id="de51b-428">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-428">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-429">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-429">Name</span></span> | <span data-ttu-id="de51b-430">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-430">Type</span></span> | <span data-ttu-id="de51b-431">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-432">arrayOutput</span></span> | <span data-ttu-id="de51b-433">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-433">String</span></span> | <span data-ttu-id="de51b-434">drie</span><span class="sxs-lookup"><span data-stu-id="de51b-434">three</span></span> |
| <span data-ttu-id="de51b-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-435">stringOutput</span></span> | <span data-ttu-id="de51b-436">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-436">String</span></span> | <span data-ttu-id="de51b-437">E</span><span class="sxs-lookup"><span data-stu-id="de51b-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="de51b-438">lengte</span><span class="sxs-lookup"><span data-stu-id="de51b-438">length</span></span>
`length(arg1)`

<span data-ttu-id="de51b-439">Retourneert het aantal elementen in een matrix of de tekens in een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="de51b-439">Returns the number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="de51b-440">Parameters</span><span class="sxs-lookup"><span data-stu-id="de51b-440">Parameters</span></span>

| <span data-ttu-id="de51b-441">Parameter</span><span class="sxs-lookup"><span data-stu-id="de51b-441">Parameter</span></span> | <span data-ttu-id="de51b-442">Vereist</span><span class="sxs-lookup"><span data-stu-id="de51b-442">Required</span></span> | <span data-ttu-id="de51b-443">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-443">Type</span></span> | <span data-ttu-id="de51b-444">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de51b-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="de51b-445">Arg1</span><span class="sxs-lookup"><span data-stu-id="de51b-445">arg1</span></span> |<span data-ttu-id="de51b-446">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-446">Yes</span></span> |<span data-ttu-id="de51b-447">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-447">array or string</span></span> |<span data-ttu-id="de51b-448">De matrix te gebruiken voor het ophalen van het aantal elementen of de tekenreeks moet worden gebruikt voor het ophalen van het aantal tekens.</span><span class="sxs-lookup"><span data-stu-id="de51b-448">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="de51b-449">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="de51b-449">Return value</span></span>

<span data-ttu-id="de51b-450">Een int.</span><span class="sxs-lookup"><span data-stu-id="de51b-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="de51b-451">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="de51b-451">Example</span></span>

<span data-ttu-id="de51b-452">Het volgende voorbeeld ziet u hoe lengte gebruiken met een matrix en de tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="de51b-452">The following example shows how to use length with an array and string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "stringToTest": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "arrayLength": {
            "type": "int",
            "value": "[length(parameters('arrayToTest'))]"
        },
        "stringLength": {
            "type": "int",
            "value": "[length(parameters('stringToTest'))]"
        }
    }
}
```

<span data-ttu-id="de51b-453">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-453">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-454">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-454">Name</span></span> | <span data-ttu-id="de51b-455">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-455">Type</span></span> | <span data-ttu-id="de51b-456">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="de51b-457">arrayLength</span></span> | <span data-ttu-id="de51b-458">int</span><span class="sxs-lookup"><span data-stu-id="de51b-458">Int</span></span> | <span data-ttu-id="de51b-459">3</span><span class="sxs-lookup"><span data-stu-id="de51b-459">3</span></span> |
| <span data-ttu-id="de51b-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="de51b-460">stringLength</span></span> | <span data-ttu-id="de51b-461">int</span><span class="sxs-lookup"><span data-stu-id="de51b-461">Int</span></span> | <span data-ttu-id="de51b-462">13</span><span class="sxs-lookup"><span data-stu-id="de51b-462">13</span></span> |

<span data-ttu-id="de51b-463">U kunt deze functie gebruiken met een matrix te geven voor het aantal iteraties maken van resources.</span><span class="sxs-lookup"><span data-stu-id="de51b-463">You can use this function with an array to specify the number of iterations when creating resources.</span></span> <span data-ttu-id="de51b-464">In het volgende voorbeeld wordt de parameter **siteNames** verwijzen naar een matrix van namen te gebruiken bij het maken van websites.</span><span class="sxs-lookup"><span data-stu-id="de51b-464">In the following example, the parameter **siteNames** would refer to an array of names to use when creating the web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="de51b-465">Zie voor meer informatie over het gebruik van deze functie met een matrix [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="de51b-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="de51b-466">min.</span><span class="sxs-lookup"><span data-stu-id="de51b-466">min</span></span>
`min(arg1)`

<span data-ttu-id="de51b-467">Retourneert de minimumwaarde van een matrix van gehele getallen of een door komma's gescheiden lijst met gehele getallen zijn.</span><span class="sxs-lookup"><span data-stu-id="de51b-467">Returns the minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="de51b-468">Parameters</span><span class="sxs-lookup"><span data-stu-id="de51b-468">Parameters</span></span>

| <span data-ttu-id="de51b-469">Parameter</span><span class="sxs-lookup"><span data-stu-id="de51b-469">Parameter</span></span> | <span data-ttu-id="de51b-470">Vereist</span><span class="sxs-lookup"><span data-stu-id="de51b-470">Required</span></span> | <span data-ttu-id="de51b-471">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-471">Type</span></span> | <span data-ttu-id="de51b-472">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de51b-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="de51b-473">Arg1</span><span class="sxs-lookup"><span data-stu-id="de51b-473">arg1</span></span> |<span data-ttu-id="de51b-474">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-474">Yes</span></span> |<span data-ttu-id="de51b-475">matrix van gehele getallen of door komma's gescheiden lijst met gehele getallen</span><span class="sxs-lookup"><span data-stu-id="de51b-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="de51b-476">De verzameling voor de minimumwaarde.</span><span class="sxs-lookup"><span data-stu-id="de51b-476">The collection to get the minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="de51b-477">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="de51b-477">Return value</span></span>

<span data-ttu-id="de51b-478">Een geheel getal dat de minimale waarde vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="de51b-478">An int representing the minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="de51b-479">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="de51b-479">Example</span></span>

<span data-ttu-id="de51b-480">Het volgende voorbeeld ziet u hoe min. gebruik met een matrix en een lijst met gehele getallen zijn:</span><span class="sxs-lookup"><span data-stu-id="de51b-480">The following example shows how to use min with an array and a list of integers:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[min(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[min(0,3,2,5,4)]"
        }
    }
}
```

<span data-ttu-id="de51b-481">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-481">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-482">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-482">Name</span></span> | <span data-ttu-id="de51b-483">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-483">Type</span></span> | <span data-ttu-id="de51b-484">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-485">arrayOutput</span></span> | <span data-ttu-id="de51b-486">int</span><span class="sxs-lookup"><span data-stu-id="de51b-486">Int</span></span> | <span data-ttu-id="de51b-487">0</span><span class="sxs-lookup"><span data-stu-id="de51b-487">0</span></span> |
| <span data-ttu-id="de51b-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-488">intOutput</span></span> | <span data-ttu-id="de51b-489">int</span><span class="sxs-lookup"><span data-stu-id="de51b-489">Int</span></span> | <span data-ttu-id="de51b-490">0</span><span class="sxs-lookup"><span data-stu-id="de51b-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="de51b-491">Maximum aantal</span><span class="sxs-lookup"><span data-stu-id="de51b-491">max</span></span>
`max(arg1)`

<span data-ttu-id="de51b-492">Retourneert de maximumwaarde van een matrix van gehele getallen of een door komma's gescheiden lijst met gehele getallen zijn.</span><span class="sxs-lookup"><span data-stu-id="de51b-492">Returns the maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="de51b-493">Parameters</span><span class="sxs-lookup"><span data-stu-id="de51b-493">Parameters</span></span>

| <span data-ttu-id="de51b-494">Parameter</span><span class="sxs-lookup"><span data-stu-id="de51b-494">Parameter</span></span> | <span data-ttu-id="de51b-495">Vereist</span><span class="sxs-lookup"><span data-stu-id="de51b-495">Required</span></span> | <span data-ttu-id="de51b-496">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-496">Type</span></span> | <span data-ttu-id="de51b-497">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de51b-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="de51b-498">Arg1</span><span class="sxs-lookup"><span data-stu-id="de51b-498">arg1</span></span> |<span data-ttu-id="de51b-499">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-499">Yes</span></span> |<span data-ttu-id="de51b-500">matrix van gehele getallen of door komma's gescheiden lijst met gehele getallen</span><span class="sxs-lookup"><span data-stu-id="de51b-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="de51b-501">De verzameling die de maximale waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="de51b-501">The collection to get the maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="de51b-502">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="de51b-502">Return value</span></span>

<span data-ttu-id="de51b-503">Een geheel getal dat de maximale waarde vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="de51b-503">An int representing the maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="de51b-504">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="de51b-504">Example</span></span>

<span data-ttu-id="de51b-505">Het volgende voorbeeld ziet u hoe max gebruiken met een matrix en een lijst met gehele getallen zijn:</span><span class="sxs-lookup"><span data-stu-id="de51b-505">The following example shows how to use max with an array and a list of integers:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[max(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[max(0,3,2,5,4)]"
        }
    }
}
```

<span data-ttu-id="de51b-506">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-506">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-507">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-507">Name</span></span> | <span data-ttu-id="de51b-508">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-508">Type</span></span> | <span data-ttu-id="de51b-509">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-510">arrayOutput</span></span> | <span data-ttu-id="de51b-511">int</span><span class="sxs-lookup"><span data-stu-id="de51b-511">Int</span></span> | <span data-ttu-id="de51b-512">5</span><span class="sxs-lookup"><span data-stu-id="de51b-512">5</span></span> |
| <span data-ttu-id="de51b-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-513">intOutput</span></span> | <span data-ttu-id="de51b-514">int</span><span class="sxs-lookup"><span data-stu-id="de51b-514">Int</span></span> | <span data-ttu-id="de51b-515">5</span><span class="sxs-lookup"><span data-stu-id="de51b-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="de51b-516">bereik</span><span class="sxs-lookup"><span data-stu-id="de51b-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="de51b-517">Maakt een matrix van gehele getallen van een geheel getal beginnen en met een aantal items.</span><span class="sxs-lookup"><span data-stu-id="de51b-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="de51b-518">Parameters</span><span class="sxs-lookup"><span data-stu-id="de51b-518">Parameters</span></span>

| <span data-ttu-id="de51b-519">Parameter</span><span class="sxs-lookup"><span data-stu-id="de51b-519">Parameter</span></span> | <span data-ttu-id="de51b-520">Vereist</span><span class="sxs-lookup"><span data-stu-id="de51b-520">Required</span></span> | <span data-ttu-id="de51b-521">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-521">Type</span></span> | <span data-ttu-id="de51b-522">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de51b-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="de51b-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="de51b-523">startingInteger</span></span> |<span data-ttu-id="de51b-524">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-524">Yes</span></span> |<span data-ttu-id="de51b-525">int</span><span class="sxs-lookup"><span data-stu-id="de51b-525">int</span></span> |<span data-ttu-id="de51b-526">De eerste geheel getal in de matrix.</span><span class="sxs-lookup"><span data-stu-id="de51b-526">The first integer in the array.</span></span> |
| <span data-ttu-id="de51b-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="de51b-527">numberofElements</span></span> |<span data-ttu-id="de51b-528">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-528">Yes</span></span> |<span data-ttu-id="de51b-529">int</span><span class="sxs-lookup"><span data-stu-id="de51b-529">int</span></span> |<span data-ttu-id="de51b-530">Het aantal getallen in de matrix.</span><span class="sxs-lookup"><span data-stu-id="de51b-530">The number of integers in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="de51b-531">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="de51b-531">Return value</span></span>

<span data-ttu-id="de51b-532">Een matrix van gehele getallen.</span><span class="sxs-lookup"><span data-stu-id="de51b-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="de51b-533">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="de51b-533">Example</span></span>

<span data-ttu-id="de51b-534">Het volgende voorbeeld ziet u hoe de bereikfunctie gebruiken:</span><span class="sxs-lookup"><span data-stu-id="de51b-534">The following example shows how to use the range function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "startingInt": {
            "type": "int",
            "defaultValue": 5
        },
        "numberOfElements": {
            "type": "int",
            "defaultValue": 3
        }
    },
    "resources": [],
    "outputs": {
        "rangeOutput": {
            "type": "array",
            "value": "[range(parameters('startingInt'),parameters('numberOfElements'))]"
        }
    }
}
```

<span data-ttu-id="de51b-535">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-535">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-536">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-536">Name</span></span> | <span data-ttu-id="de51b-537">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-537">Type</span></span> | <span data-ttu-id="de51b-538">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-539">rangeOutput</span></span> | <span data-ttu-id="de51b-540">matrix</span><span class="sxs-lookup"><span data-stu-id="de51b-540">Array</span></span> | <span data-ttu-id="de51b-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="de51b-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="de51b-542">Overslaan</span><span class="sxs-lookup"><span data-stu-id="de51b-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="de51b-543">Retourneert een matrix met alle elementen na het opgegeven getal in de matrix of retourneert een tekenreeks met de tekens na het opgegeven getal in de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="de51b-543">Returns an array with all the elements after the specified number in the array, or returns a string with all the characters after the specified number in the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="de51b-544">Parameters</span><span class="sxs-lookup"><span data-stu-id="de51b-544">Parameters</span></span>

| <span data-ttu-id="de51b-545">Parameter</span><span class="sxs-lookup"><span data-stu-id="de51b-545">Parameter</span></span> | <span data-ttu-id="de51b-546">Vereist</span><span class="sxs-lookup"><span data-stu-id="de51b-546">Required</span></span> | <span data-ttu-id="de51b-547">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-547">Type</span></span> | <span data-ttu-id="de51b-548">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de51b-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="de51b-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="de51b-549">originalValue</span></span> |<span data-ttu-id="de51b-550">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-550">Yes</span></span> |<span data-ttu-id="de51b-551">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-551">array or string</span></span> |<span data-ttu-id="de51b-552">De matrix of tekenreeks moet worden gebruikt voor het overslaan.</span><span class="sxs-lookup"><span data-stu-id="de51b-552">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="de51b-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="de51b-553">numberToSkip</span></span> |<span data-ttu-id="de51b-554">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-554">Yes</span></span> |<span data-ttu-id="de51b-555">int</span><span class="sxs-lookup"><span data-stu-id="de51b-555">int</span></span> |<span data-ttu-id="de51b-556">Het aantal elementen of tekens over te slaan.</span><span class="sxs-lookup"><span data-stu-id="de51b-556">The number of elements or characters to skip.</span></span> <span data-ttu-id="de51b-557">Als deze waarde 0 of minder is, worden alle elementen of tekens in de waarde geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="de51b-557">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="de51b-558">Als deze groter dan de lengte van de matrix of tekenreeks is, een lege matrix of tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="de51b-558">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="de51b-559">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="de51b-559">Return value</span></span>

<span data-ttu-id="de51b-560">Een matrix of tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="de51b-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="de51b-561">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="de51b-561">Example</span></span>

<span data-ttu-id="de51b-562">Het volgende voorbeeld wordt overgeslagen voor het opgegeven aantal elementen in de matrix en het opgegeven aantal tekens in een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="de51b-562">The following example skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToSkip": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToSkip": {
            "type": "int",
            "defaultValue": 4
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[skip(parameters('testArray'),parameters('elementsToSkip'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[skip(parameters('testString'),parameters('charactersToSkip'))]"
        }
    }
}
```

<span data-ttu-id="de51b-563">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-563">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-564">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-564">Name</span></span> | <span data-ttu-id="de51b-565">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-565">Type</span></span> | <span data-ttu-id="de51b-566">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-567">arrayOutput</span></span> | <span data-ttu-id="de51b-568">matrix</span><span class="sxs-lookup"><span data-stu-id="de51b-568">Array</span></span> | <span data-ttu-id="de51b-569">["drie"]</span><span class="sxs-lookup"><span data-stu-id="de51b-569">["three"]</span></span> |
| <span data-ttu-id="de51b-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-570">stringOutput</span></span> | <span data-ttu-id="de51b-571">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-571">String</span></span> | <span data-ttu-id="de51b-572">twee drie</span><span class="sxs-lookup"><span data-stu-id="de51b-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="de51b-573">duren</span><span class="sxs-lookup"><span data-stu-id="de51b-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="de51b-574">Retourneert een matrix met het opgegeven aantal elementen vanaf het begin van de matrix of een tekenreeks zijn met het opgegeven aantal tekens vanaf het begin van de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="de51b-574">Returns an array with the specified number of elements from the start of the array, or a string with the specified number of characters from the start of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="de51b-575">Parameters</span><span class="sxs-lookup"><span data-stu-id="de51b-575">Parameters</span></span>

| <span data-ttu-id="de51b-576">Parameter</span><span class="sxs-lookup"><span data-stu-id="de51b-576">Parameter</span></span> | <span data-ttu-id="de51b-577">Vereist</span><span class="sxs-lookup"><span data-stu-id="de51b-577">Required</span></span> | <span data-ttu-id="de51b-578">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-578">Type</span></span> | <span data-ttu-id="de51b-579">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de51b-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="de51b-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="de51b-580">originalValue</span></span> |<span data-ttu-id="de51b-581">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-581">Yes</span></span> |<span data-ttu-id="de51b-582">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-582">array or string</span></span> |<span data-ttu-id="de51b-583">De matrix of tekenreeks op voor het nemen van elementen uit.</span><span class="sxs-lookup"><span data-stu-id="de51b-583">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="de51b-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="de51b-584">numberToTake</span></span> |<span data-ttu-id="de51b-585">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-585">Yes</span></span> |<span data-ttu-id="de51b-586">int</span><span class="sxs-lookup"><span data-stu-id="de51b-586">int</span></span> |<span data-ttu-id="de51b-587">Het aantal elementen of tekens te laten worden.</span><span class="sxs-lookup"><span data-stu-id="de51b-587">The number of elements or characters to take.</span></span> <span data-ttu-id="de51b-588">Als deze waarde 0 of minder is, wordt een lege matrix of tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="de51b-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="de51b-589">Als deze groter is dan de lengte van de opgegeven matrix of tekenreeks is, worden alle elementen in de matrix of tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="de51b-589">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="de51b-590">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="de51b-590">Return value</span></span>

<span data-ttu-id="de51b-591">Een matrix of tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="de51b-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="de51b-592">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="de51b-592">Example</span></span>

<span data-ttu-id="de51b-593">Het volgende voorbeeld wordt het opgegeven aantal elementen van de matrix en de tekens uit een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="de51b-593">The following example takes the specified number of elements from the array, and characters from a string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToTake": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToTake": {
            "type": "int",
            "defaultValue": 2
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[take(parameters('testArray'),parameters('elementsToTake'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[take(parameters('testString'),parameters('charactersToTake'))]"
        }
    }
}
```

<span data-ttu-id="de51b-594">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-594">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-595">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-595">Name</span></span> | <span data-ttu-id="de51b-596">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-596">Type</span></span> | <span data-ttu-id="de51b-597">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-598">arrayOutput</span></span> | <span data-ttu-id="de51b-599">matrix</span><span class="sxs-lookup"><span data-stu-id="de51b-599">Array</span></span> | <span data-ttu-id="de51b-600">['een', 'twee']</span><span class="sxs-lookup"><span data-stu-id="de51b-600">["one", "two"]</span></span> |
| <span data-ttu-id="de51b-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-601">stringOutput</span></span> | <span data-ttu-id="de51b-602">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de51b-602">String</span></span> | <span data-ttu-id="de51b-603">op</span><span class="sxs-lookup"><span data-stu-id="de51b-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="de51b-604">Union</span><span class="sxs-lookup"><span data-stu-id="de51b-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="de51b-605">Retourneert een matrix of object met alle elementen van de parameters.</span><span class="sxs-lookup"><span data-stu-id="de51b-605">Returns a single array or object with all elements from the parameters.</span></span> <span data-ttu-id="de51b-606">Dubbele waarden of sleutels zijn slechts één keer wordt opgenomen.</span><span class="sxs-lookup"><span data-stu-id="de51b-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="de51b-607">Parameters</span><span class="sxs-lookup"><span data-stu-id="de51b-607">Parameters</span></span>

| <span data-ttu-id="de51b-608">Parameter</span><span class="sxs-lookup"><span data-stu-id="de51b-608">Parameter</span></span> | <span data-ttu-id="de51b-609">Vereist</span><span class="sxs-lookup"><span data-stu-id="de51b-609">Required</span></span> | <span data-ttu-id="de51b-610">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-610">Type</span></span> | <span data-ttu-id="de51b-611">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de51b-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="de51b-612">Arg1</span><span class="sxs-lookup"><span data-stu-id="de51b-612">arg1</span></span> |<span data-ttu-id="de51b-613">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-613">Yes</span></span> |<span data-ttu-id="de51b-614">matrix of object</span><span class="sxs-lookup"><span data-stu-id="de51b-614">array or object</span></span> |<span data-ttu-id="de51b-615">De eerste waarde moet worden gebruikt om lid te worden elementen.</span><span class="sxs-lookup"><span data-stu-id="de51b-615">The first value to use for joining elements.</span></span> |
| <span data-ttu-id="de51b-616">Arg2</span><span class="sxs-lookup"><span data-stu-id="de51b-616">arg2</span></span> |<span data-ttu-id="de51b-617">Ja</span><span class="sxs-lookup"><span data-stu-id="de51b-617">Yes</span></span> |<span data-ttu-id="de51b-618">matrix of object</span><span class="sxs-lookup"><span data-stu-id="de51b-618">array or object</span></span> |<span data-ttu-id="de51b-619">De tweede waarde moet worden gebruikt om lid te worden elementen.</span><span class="sxs-lookup"><span data-stu-id="de51b-619">The second value to use for joining elements.</span></span> |
| <span data-ttu-id="de51b-620">Extra argumenten</span><span class="sxs-lookup"><span data-stu-id="de51b-620">additional arguments</span></span> |<span data-ttu-id="de51b-621">Nee</span><span class="sxs-lookup"><span data-stu-id="de51b-621">No</span></span> |<span data-ttu-id="de51b-622">matrix of object</span><span class="sxs-lookup"><span data-stu-id="de51b-622">array or object</span></span> |<span data-ttu-id="de51b-623">Aanvullende waarden worden gebruikt om lid te worden elementen.</span><span class="sxs-lookup"><span data-stu-id="de51b-623">Additional values to use for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="de51b-624">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="de51b-624">Return value</span></span>

<span data-ttu-id="de51b-625">Een matrix of object.</span><span class="sxs-lookup"><span data-stu-id="de51b-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="de51b-626">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="de51b-626">Example</span></span>

<span data-ttu-id="de51b-627">Het volgende voorbeeld ziet hoe u union met matrices en objecten:</span><span class="sxs-lookup"><span data-stu-id="de51b-627">The following example shows how to use union with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"three": "c", "four": "d", "five": "e"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["three", "four"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[union(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[union(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="de51b-628">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="de51b-628">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="de51b-629">Naam</span><span class="sxs-lookup"><span data-stu-id="de51b-629">Name</span></span> | <span data-ttu-id="de51b-630">Type</span><span class="sxs-lookup"><span data-stu-id="de51b-630">Type</span></span> | <span data-ttu-id="de51b-631">Waarde</span><span class="sxs-lookup"><span data-stu-id="de51b-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="de51b-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-632">objectOutput</span></span> | <span data-ttu-id="de51b-633">Object</span><span class="sxs-lookup"><span data-stu-id="de51b-633">Object</span></span> | <span data-ttu-id="de51b-634">{"een": "a", "twee": "b", "drie": "c", "4": "d", "vijf": "e"}</span><span class="sxs-lookup"><span data-stu-id="de51b-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="de51b-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="de51b-635">arrayOutput</span></span> | <span data-ttu-id="de51b-636">matrix</span><span class="sxs-lookup"><span data-stu-id="de51b-636">Array</span></span> | <span data-ttu-id="de51b-637">['een', 'twee', 'drie', "vier"]</span><span class="sxs-lookup"><span data-stu-id="de51b-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="de51b-638">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="de51b-638">Next steps</span></span>
* <span data-ttu-id="de51b-639">Zie voor een beschrijving van de secties in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="de51b-639">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="de51b-640">U kunt meerdere sjablonen samenvoegen, Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="de51b-640">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="de51b-641">Voor een opgegeven aantal keer herhalen bij het maken van een type resource, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="de51b-641">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="de51b-642">Zie voor het implementeren van de sjabloon die u hebt gemaakt, [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="de51b-642">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

