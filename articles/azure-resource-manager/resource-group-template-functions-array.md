---
title: Resource Manager-sjabloon aaaAzure functioneert - matrices en objecten | Microsoft Docs
description: Hallo functies toouse in een Azure Resource Manager-sjabloon voor het werken met matrices en objecten beschrijft.
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
ms.openlocfilehash: e5f1a9b2a71039562eae7e48c2474a1fa59a7bea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="85a1f-103">Matrix en object-functies voor Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="85a1f-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="85a1f-104">Resource Manager biedt een aantal functies voor het werken met matrices en objecten.</span><span class="sxs-lookup"><span data-stu-id="85a1f-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="85a1f-105">matrix</span><span class="sxs-lookup"><span data-stu-id="85a1f-105">array</span></span>](#array)
* [<span data-ttu-id="85a1f-106">coalesce</span><span class="sxs-lookup"><span data-stu-id="85a1f-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="85a1f-107">concat</span><span class="sxs-lookup"><span data-stu-id="85a1f-107">concat</span></span>](#concat)
* [<span data-ttu-id="85a1f-108">bevat</span><span class="sxs-lookup"><span data-stu-id="85a1f-108">contains</span></span>](#contains)
* [<span data-ttu-id="85a1f-109">createArray</span><span class="sxs-lookup"><span data-stu-id="85a1f-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="85a1f-110">leeg</span><span class="sxs-lookup"><span data-stu-id="85a1f-110">empty</span></span>](#empty)
* [<span data-ttu-id="85a1f-111">eerste</span><span class="sxs-lookup"><span data-stu-id="85a1f-111">first</span></span>](#first)
* [<span data-ttu-id="85a1f-112">snijpunt</span><span class="sxs-lookup"><span data-stu-id="85a1f-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="85a1f-113">JSON</span><span class="sxs-lookup"><span data-stu-id="85a1f-113">json</span></span>](#json)
* [<span data-ttu-id="85a1f-114">laatste</span><span class="sxs-lookup"><span data-stu-id="85a1f-114">last</span></span>](#last)
* [<span data-ttu-id="85a1f-115">lengte</span><span class="sxs-lookup"><span data-stu-id="85a1f-115">length</span></span>](#length)
* [<span data-ttu-id="85a1f-116">min</span><span class="sxs-lookup"><span data-stu-id="85a1f-116">min</span></span>](#min)
* [<span data-ttu-id="85a1f-117">maximale</span><span class="sxs-lookup"><span data-stu-id="85a1f-117">max</span></span>](#max)
* [<span data-ttu-id="85a1f-118">bereik</span><span class="sxs-lookup"><span data-stu-id="85a1f-118">range</span></span>](#range)
* [<span data-ttu-id="85a1f-119">overslaan</span><span class="sxs-lookup"><span data-stu-id="85a1f-119">skip</span></span>](#skip)
* [<span data-ttu-id="85a1f-120">duren</span><span class="sxs-lookup"><span data-stu-id="85a1f-120">take</span></span>](#take)
* [<span data-ttu-id="85a1f-121">Union</span><span class="sxs-lookup"><span data-stu-id="85a1f-121">union</span></span>](#union)

<span data-ttu-id="85a1f-122">een matrix van tekenreekswaarden gescheiden door een waarde tooget Zie [splitsen](resource-group-template-functions-string.md#split).</span><span class="sxs-lookup"><span data-stu-id="85a1f-122">tooget an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="85a1f-123">matrix</span><span class="sxs-lookup"><span data-stu-id="85a1f-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="85a1f-124">De waardematrix tooan Hallo converteert.</span><span class="sxs-lookup"><span data-stu-id="85a1f-124">Converts hello value tooan array.</span></span>

### <a name="parameters"></a><span data-ttu-id="85a1f-125">Parameters</span><span class="sxs-lookup"><span data-stu-id="85a1f-125">Parameters</span></span>

| <span data-ttu-id="85a1f-126">Parameter</span><span class="sxs-lookup"><span data-stu-id="85a1f-126">Parameter</span></span> | <span data-ttu-id="85a1f-127">Vereist</span><span class="sxs-lookup"><span data-stu-id="85a1f-127">Required</span></span> | <span data-ttu-id="85a1f-128">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-128">Type</span></span> | <span data-ttu-id="85a1f-129">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85a1f-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="85a1f-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="85a1f-130">convertToArray</span></span> |<span data-ttu-id="85a1f-131">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-131">Yes</span></span> |<span data-ttu-id="85a1f-132">int, string, matrix of object</span><span class="sxs-lookup"><span data-stu-id="85a1f-132">int, string, array, or object</span></span> |<span data-ttu-id="85a1f-133">Hallo waarde tooconvert tooan matrix.</span><span class="sxs-lookup"><span data-stu-id="85a1f-133">hello value tooconvert tooan array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="85a1f-134">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-134">Return value</span></span>

<span data-ttu-id="85a1f-135">Een matrix.</span><span class="sxs-lookup"><span data-stu-id="85a1f-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="85a1f-136">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85a1f-136">Example</span></span>

<span data-ttu-id="85a1f-137">Hallo volgende voorbeeld ziet u hoe toouse Hallo Matrixfunctie met verschillende typen.</span><span class="sxs-lookup"><span data-stu-id="85a1f-137">hello following example shows how toouse hello array function with different types.</span></span>

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

<span data-ttu-id="85a1f-138">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-138">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-139">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-139">Name</span></span> | <span data-ttu-id="85a1f-140">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-140">Type</span></span> | <span data-ttu-id="85a1f-141">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-142">intOutput</span></span> | <span data-ttu-id="85a1f-143">Matrix</span><span class="sxs-lookup"><span data-stu-id="85a1f-143">Array</span></span> | <span data-ttu-id="85a1f-144">[1]</span><span class="sxs-lookup"><span data-stu-id="85a1f-144">[1]</span></span> |
| <span data-ttu-id="85a1f-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-145">stringOutput</span></span> | <span data-ttu-id="85a1f-146">Matrix</span><span class="sxs-lookup"><span data-stu-id="85a1f-146">Array</span></span> | <span data-ttu-id="85a1f-147">["a"]</span><span class="sxs-lookup"><span data-stu-id="85a1f-147">["a"]</span></span> |
| <span data-ttu-id="85a1f-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-148">objectOutput</span></span> | <span data-ttu-id="85a1f-149">Matrix</span><span class="sxs-lookup"><span data-stu-id="85a1f-149">Array</span></span> | <span data-ttu-id="85a1f-150">[{"a": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="85a1f-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="85a1f-151">Coalesce</span><span class="sxs-lookup"><span data-stu-id="85a1f-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="85a1f-152">Retourneert de eerste niet-null-waarde van Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="85a1f-152">Returns first non-null value from hello parameters.</span></span> <span data-ttu-id="85a1f-153">Lege tekenreeksen, matrices leeg en lege objecten zijn niet null.</span><span class="sxs-lookup"><span data-stu-id="85a1f-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="85a1f-154">Parameters</span><span class="sxs-lookup"><span data-stu-id="85a1f-154">Parameters</span></span>

| <span data-ttu-id="85a1f-155">Parameter</span><span class="sxs-lookup"><span data-stu-id="85a1f-155">Parameter</span></span> | <span data-ttu-id="85a1f-156">Vereist</span><span class="sxs-lookup"><span data-stu-id="85a1f-156">Required</span></span> | <span data-ttu-id="85a1f-157">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-157">Type</span></span> | <span data-ttu-id="85a1f-158">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85a1f-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="85a1f-159">Arg1</span><span class="sxs-lookup"><span data-stu-id="85a1f-159">arg1</span></span> |<span data-ttu-id="85a1f-160">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-160">Yes</span></span> |<span data-ttu-id="85a1f-161">int, string, matrix of object</span><span class="sxs-lookup"><span data-stu-id="85a1f-161">int, string, array, or object</span></span> |<span data-ttu-id="85a1f-162">Hallo eerste waarde tootest voor null.</span><span class="sxs-lookup"><span data-stu-id="85a1f-162">hello first value tootest for null.</span></span> |
| <span data-ttu-id="85a1f-163">Als u meer argumenten</span><span class="sxs-lookup"><span data-stu-id="85a1f-163">additional args</span></span> |<span data-ttu-id="85a1f-164">Nee</span><span class="sxs-lookup"><span data-stu-id="85a1f-164">No</span></span> |<span data-ttu-id="85a1f-165">int, string, matrix of object</span><span class="sxs-lookup"><span data-stu-id="85a1f-165">int, string, array, or object</span></span> |<span data-ttu-id="85a1f-166">Aanvullende waarden tootest voor null.</span><span class="sxs-lookup"><span data-stu-id="85a1f-166">Additional values tootest for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="85a1f-167">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-167">Return value</span></span>

<span data-ttu-id="85a1f-168">Hallo-waarde van Hallo eerste niet-null-parameters, dit kan een string, int, matrix of object.</span><span class="sxs-lookup"><span data-stu-id="85a1f-168">hello value of hello first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="85a1f-169">Null als alle parameters leeg zijn.</span><span class="sxs-lookup"><span data-stu-id="85a1f-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="85a1f-170">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85a1f-170">Example</span></span>

<span data-ttu-id="85a1f-171">Hallo ziet volgende voorbeeld Hallo-uitvoer van verschillende coalesce worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="85a1f-171">hello following example shows hello output from different uses of coalesce.</span></span>

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

<span data-ttu-id="85a1f-172">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-172">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-173">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-173">Name</span></span> | <span data-ttu-id="85a1f-174">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-174">Type</span></span> | <span data-ttu-id="85a1f-175">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-176">stringOutput</span></span> | <span data-ttu-id="85a1f-177">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-177">String</span></span> | <span data-ttu-id="85a1f-178">Standaard</span><span class="sxs-lookup"><span data-stu-id="85a1f-178">default</span></span> |
| <span data-ttu-id="85a1f-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-179">intOutput</span></span> | <span data-ttu-id="85a1f-180">int</span><span class="sxs-lookup"><span data-stu-id="85a1f-180">Int</span></span> | <span data-ttu-id="85a1f-181">1</span><span class="sxs-lookup"><span data-stu-id="85a1f-181">1</span></span> |
| <span data-ttu-id="85a1f-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-182">objectOutput</span></span> | <span data-ttu-id="85a1f-183">Object</span><span class="sxs-lookup"><span data-stu-id="85a1f-183">Object</span></span> | <span data-ttu-id="85a1f-184">{{'eerste': 'standaard'}</span><span class="sxs-lookup"><span data-stu-id="85a1f-184">{"first": "default"}</span></span> |
| <span data-ttu-id="85a1f-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-185">arrayOutput</span></span> | <span data-ttu-id="85a1f-186">Matrix</span><span class="sxs-lookup"><span data-stu-id="85a1f-186">Array</span></span> | <span data-ttu-id="85a1f-187">[1]</span><span class="sxs-lookup"><span data-stu-id="85a1f-187">[1]</span></span> |
| <span data-ttu-id="85a1f-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-188">emptyOutput</span></span> | <span data-ttu-id="85a1f-189">BOOL</span><span class="sxs-lookup"><span data-stu-id="85a1f-189">Bool</span></span> | <span data-ttu-id="85a1f-190">True</span><span class="sxs-lookup"><span data-stu-id="85a1f-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="85a1f-191">concat</span><span class="sxs-lookup"><span data-stu-id="85a1f-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="85a1f-192">Combineert meerdere matrices en retourneert Hallo samengevoegd matrix, of meerdere tekenreekswaarden combineert en retourneert Hallo samengevoegd tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="85a1f-192">Combines multiple arrays and returns hello concatenated array, or combines multiple string values and returns hello concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="85a1f-193">Parameters</span><span class="sxs-lookup"><span data-stu-id="85a1f-193">Parameters</span></span>

| <span data-ttu-id="85a1f-194">Parameter</span><span class="sxs-lookup"><span data-stu-id="85a1f-194">Parameter</span></span> | <span data-ttu-id="85a1f-195">Vereist</span><span class="sxs-lookup"><span data-stu-id="85a1f-195">Required</span></span> | <span data-ttu-id="85a1f-196">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-196">Type</span></span> | <span data-ttu-id="85a1f-197">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85a1f-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="85a1f-198">Arg1</span><span class="sxs-lookup"><span data-stu-id="85a1f-198">arg1</span></span> |<span data-ttu-id="85a1f-199">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-199">Yes</span></span> |<span data-ttu-id="85a1f-200">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-200">array or string</span></span> |<span data-ttu-id="85a1f-201">Hallo eerste matrix of tekenreeks op voor de samenvoeging.</span><span class="sxs-lookup"><span data-stu-id="85a1f-201">hello first array or string for concatenation.</span></span> |
| <span data-ttu-id="85a1f-202">Extra argumenten</span><span class="sxs-lookup"><span data-stu-id="85a1f-202">additional arguments</span></span> |<span data-ttu-id="85a1f-203">Nee</span><span class="sxs-lookup"><span data-stu-id="85a1f-203">No</span></span> |<span data-ttu-id="85a1f-204">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-204">array or string</span></span> |<span data-ttu-id="85a1f-205">Aanvullende matrices of tekenreeksen in opeenvolgende volgorde voor de samenvoeging.</span><span class="sxs-lookup"><span data-stu-id="85a1f-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="85a1f-206">Deze functie kan duren voordat een willekeurig aantal argumenten en tekenreeksen of matrices voor Hallo parameters kan accepteren.</span><span class="sxs-lookup"><span data-stu-id="85a1f-206">This function can take any number of arguments, and can accept either strings or arrays for hello parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="85a1f-207">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-207">Return value</span></span>
<span data-ttu-id="85a1f-208">Een tekenreeks of matrix met samengevoegde waarden.</span><span class="sxs-lookup"><span data-stu-id="85a1f-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="85a1f-209">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85a1f-209">Example</span></span>

<span data-ttu-id="85a1f-210">Hallo volgende voorbeeld ziet u hoe toocombine twee matrices.</span><span class="sxs-lookup"><span data-stu-id="85a1f-210">hello following example shows how toocombine two arrays.</span></span>

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

<span data-ttu-id="85a1f-211">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-211">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-212">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-212">Name</span></span> | <span data-ttu-id="85a1f-213">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-213">Type</span></span> | <span data-ttu-id="85a1f-214">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-215">retourneren</span><span class="sxs-lookup"><span data-stu-id="85a1f-215">return</span></span> | <span data-ttu-id="85a1f-216">Matrix</span><span class="sxs-lookup"><span data-stu-id="85a1f-216">Array</span></span> | <span data-ttu-id="85a1f-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="85a1f-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="85a1f-218">Hallo volgende voorbeeld ziet u hoe toocombine twee tekenreekswaarden en een samengevoegde tekenreeks retourneren.</span><span class="sxs-lookup"><span data-stu-id="85a1f-218">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="85a1f-219">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-219">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-220">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-220">Name</span></span> | <span data-ttu-id="85a1f-221">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-221">Type</span></span> | <span data-ttu-id="85a1f-222">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-223">concatOutput</span></span> | <span data-ttu-id="85a1f-224">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-224">String</span></span> | <span data-ttu-id="85a1f-225">voorvoegsel 5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="85a1f-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="85a1f-226">Bevat</span><span class="sxs-lookup"><span data-stu-id="85a1f-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="85a1f-227">Controleert of een matrix een waarde bevat, een object een sleutel bevat of een tekenreeks een subtekenreeks bevat.</span><span class="sxs-lookup"><span data-stu-id="85a1f-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="85a1f-228">Parameters</span><span class="sxs-lookup"><span data-stu-id="85a1f-228">Parameters</span></span>

| <span data-ttu-id="85a1f-229">Parameter</span><span class="sxs-lookup"><span data-stu-id="85a1f-229">Parameter</span></span> | <span data-ttu-id="85a1f-230">Vereist</span><span class="sxs-lookup"><span data-stu-id="85a1f-230">Required</span></span> | <span data-ttu-id="85a1f-231">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-231">Type</span></span> | <span data-ttu-id="85a1f-232">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85a1f-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="85a1f-233">container</span><span class="sxs-lookup"><span data-stu-id="85a1f-233">container</span></span> |<span data-ttu-id="85a1f-234">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-234">Yes</span></span> |<span data-ttu-id="85a1f-235">Array, object of een tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-235">array, object, or string</span></span> |<span data-ttu-id="85a1f-236">Hallo-waarde die Hallo waarde toofind bevat.</span><span class="sxs-lookup"><span data-stu-id="85a1f-236">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="85a1f-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="85a1f-237">itemToFind</span></span> |<span data-ttu-id="85a1f-238">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-238">Yes</span></span> |<span data-ttu-id="85a1f-239">String of int.</span><span class="sxs-lookup"><span data-stu-id="85a1f-239">string or int</span></span> |<span data-ttu-id="85a1f-240">Hallo waarde toofind.</span><span class="sxs-lookup"><span data-stu-id="85a1f-240">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="85a1f-241">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-241">Return value</span></span>

<span data-ttu-id="85a1f-242">**De waarde True** als Hallo item gevonden, anders wordt is **False**.</span><span class="sxs-lookup"><span data-stu-id="85a1f-242">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="85a1f-243">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85a1f-243">Example</span></span>

<span data-ttu-id="85a1f-244">Hallo volgende voorbeeld laat zien hoe toouse bevat met verschillende typen:</span><span class="sxs-lookup"><span data-stu-id="85a1f-244">hello following example shows how toouse contains with different types:</span></span>

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

<span data-ttu-id="85a1f-245">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-246">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-246">Name</span></span> | <span data-ttu-id="85a1f-247">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-247">Type</span></span> | <span data-ttu-id="85a1f-248">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="85a1f-249">stringTrue</span></span> | <span data-ttu-id="85a1f-250">BOOL</span><span class="sxs-lookup"><span data-stu-id="85a1f-250">Bool</span></span> | <span data-ttu-id="85a1f-251">True</span><span class="sxs-lookup"><span data-stu-id="85a1f-251">True</span></span> |
| <span data-ttu-id="85a1f-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="85a1f-252">stringFalse</span></span> | <span data-ttu-id="85a1f-253">BOOL</span><span class="sxs-lookup"><span data-stu-id="85a1f-253">Bool</span></span> | <span data-ttu-id="85a1f-254">False</span><span class="sxs-lookup"><span data-stu-id="85a1f-254">False</span></span> |
| <span data-ttu-id="85a1f-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="85a1f-255">objectTrue</span></span> | <span data-ttu-id="85a1f-256">BOOL</span><span class="sxs-lookup"><span data-stu-id="85a1f-256">Bool</span></span> | <span data-ttu-id="85a1f-257">True</span><span class="sxs-lookup"><span data-stu-id="85a1f-257">True</span></span> |
| <span data-ttu-id="85a1f-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="85a1f-258">objectFalse</span></span> | <span data-ttu-id="85a1f-259">BOOL</span><span class="sxs-lookup"><span data-stu-id="85a1f-259">Bool</span></span> | <span data-ttu-id="85a1f-260">False</span><span class="sxs-lookup"><span data-stu-id="85a1f-260">False</span></span> |
| <span data-ttu-id="85a1f-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="85a1f-261">arrayTrue</span></span> | <span data-ttu-id="85a1f-262">BOOL</span><span class="sxs-lookup"><span data-stu-id="85a1f-262">Bool</span></span> | <span data-ttu-id="85a1f-263">True</span><span class="sxs-lookup"><span data-stu-id="85a1f-263">True</span></span> |
| <span data-ttu-id="85a1f-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="85a1f-264">arrayFalse</span></span> | <span data-ttu-id="85a1f-265">BOOL</span><span class="sxs-lookup"><span data-stu-id="85a1f-265">Bool</span></span> | <span data-ttu-id="85a1f-266">False</span><span class="sxs-lookup"><span data-stu-id="85a1f-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="85a1f-267">createarray</span><span class="sxs-lookup"><span data-stu-id="85a1f-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="85a1f-268">Maakt een matrix van Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="85a1f-268">Creates an array from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="85a1f-269">Parameters</span><span class="sxs-lookup"><span data-stu-id="85a1f-269">Parameters</span></span>

| <span data-ttu-id="85a1f-270">Parameter</span><span class="sxs-lookup"><span data-stu-id="85a1f-270">Parameter</span></span> | <span data-ttu-id="85a1f-271">Vereist</span><span class="sxs-lookup"><span data-stu-id="85a1f-271">Required</span></span> | <span data-ttu-id="85a1f-272">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-272">Type</span></span> | <span data-ttu-id="85a1f-273">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85a1f-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="85a1f-274">Arg1</span><span class="sxs-lookup"><span data-stu-id="85a1f-274">arg1</span></span> |<span data-ttu-id="85a1f-275">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-275">Yes</span></span> |<span data-ttu-id="85a1f-276">Tekenreeks, geheel getal, matrix of Object</span><span class="sxs-lookup"><span data-stu-id="85a1f-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="85a1f-277">Hallo eerste waarde in Hallo matrix.</span><span class="sxs-lookup"><span data-stu-id="85a1f-277">hello first value in hello array.</span></span> |
| <span data-ttu-id="85a1f-278">Extra argumenten</span><span class="sxs-lookup"><span data-stu-id="85a1f-278">additional arguments</span></span> |<span data-ttu-id="85a1f-279">Nee</span><span class="sxs-lookup"><span data-stu-id="85a1f-279">No</span></span> |<span data-ttu-id="85a1f-280">Tekenreeks, geheel getal, matrix of Object</span><span class="sxs-lookup"><span data-stu-id="85a1f-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="85a1f-281">Aanvullende waarden in Hallo matrix.</span><span class="sxs-lookup"><span data-stu-id="85a1f-281">Additional values in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="85a1f-282">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-282">Return value</span></span>

<span data-ttu-id="85a1f-283">Een matrix.</span><span class="sxs-lookup"><span data-stu-id="85a1f-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="85a1f-284">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85a1f-284">Example</span></span>

<span data-ttu-id="85a1f-285">Hallo volgende voorbeeld wordt getoond hoe toouse createArray met verschillende typen:</span><span class="sxs-lookup"><span data-stu-id="85a1f-285">hello following example shows how toouse createArray with different types:</span></span>

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

<span data-ttu-id="85a1f-286">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-286">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-287">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-287">Name</span></span> | <span data-ttu-id="85a1f-288">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-288">Type</span></span> | <span data-ttu-id="85a1f-289">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-290">stringArray</span><span class="sxs-lookup"><span data-stu-id="85a1f-290">stringArray</span></span> | <span data-ttu-id="85a1f-291">Matrix</span><span class="sxs-lookup"><span data-stu-id="85a1f-291">Array</span></span> | <span data-ttu-id="85a1f-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="85a1f-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="85a1f-293">intArray</span><span class="sxs-lookup"><span data-stu-id="85a1f-293">intArray</span></span> | <span data-ttu-id="85a1f-294">Matrix</span><span class="sxs-lookup"><span data-stu-id="85a1f-294">Array</span></span> | <span data-ttu-id="85a1f-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="85a1f-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="85a1f-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="85a1f-296">objectArray</span></span> | <span data-ttu-id="85a1f-297">Matrix</span><span class="sxs-lookup"><span data-stu-id="85a1f-297">Array</span></span> | <span data-ttu-id="85a1f-298">[{"een": "a", "twee": "b", "drie": "c"}]</span><span class="sxs-lookup"><span data-stu-id="85a1f-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="85a1f-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="85a1f-299">arrayArray</span></span> | <span data-ttu-id="85a1f-300">Matrix</span><span class="sxs-lookup"><span data-stu-id="85a1f-300">Array</span></span> | <span data-ttu-id="85a1f-301">[[' een', 'twee', 'drie']]</span><span class="sxs-lookup"><span data-stu-id="85a1f-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="85a1f-302">leeg</span><span class="sxs-lookup"><span data-stu-id="85a1f-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="85a1f-303">Hiermee wordt bepaald of een matrix, een object of een tekenreeks leeg is.</span><span class="sxs-lookup"><span data-stu-id="85a1f-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="85a1f-304">Parameters</span><span class="sxs-lookup"><span data-stu-id="85a1f-304">Parameters</span></span>

| <span data-ttu-id="85a1f-305">Parameter</span><span class="sxs-lookup"><span data-stu-id="85a1f-305">Parameter</span></span> | <span data-ttu-id="85a1f-306">Vereist</span><span class="sxs-lookup"><span data-stu-id="85a1f-306">Required</span></span> | <span data-ttu-id="85a1f-307">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-307">Type</span></span> | <span data-ttu-id="85a1f-308">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85a1f-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="85a1f-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="85a1f-309">itemToTest</span></span> |<span data-ttu-id="85a1f-310">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-310">Yes</span></span> |<span data-ttu-id="85a1f-311">Array, object of een tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-311">array, object, or string</span></span> |<span data-ttu-id="85a1f-312">Hallo waarde toocheck als deze leeg is.</span><span class="sxs-lookup"><span data-stu-id="85a1f-312">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="85a1f-313">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-313">Return value</span></span>

<span data-ttu-id="85a1f-314">Retourneert **True** als Hallo-waarde leeg, anders wordt is **False**.</span><span class="sxs-lookup"><span data-stu-id="85a1f-314">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="85a1f-315">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85a1f-315">Example</span></span>

<span data-ttu-id="85a1f-316">Hallo volgende voorbeeld wordt gecontroleerd of een matrix, het object en de tekenreeks leeg zijn.</span><span class="sxs-lookup"><span data-stu-id="85a1f-316">hello following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="85a1f-317">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-317">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-318">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-318">Name</span></span> | <span data-ttu-id="85a1f-319">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-319">Type</span></span> | <span data-ttu-id="85a1f-320">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="85a1f-321">arrayEmpty</span></span> | <span data-ttu-id="85a1f-322">BOOL</span><span class="sxs-lookup"><span data-stu-id="85a1f-322">Bool</span></span> | <span data-ttu-id="85a1f-323">True</span><span class="sxs-lookup"><span data-stu-id="85a1f-323">True</span></span> |
| <span data-ttu-id="85a1f-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="85a1f-324">objectEmpty</span></span> | <span data-ttu-id="85a1f-325">BOOL</span><span class="sxs-lookup"><span data-stu-id="85a1f-325">Bool</span></span> | <span data-ttu-id="85a1f-326">True</span><span class="sxs-lookup"><span data-stu-id="85a1f-326">True</span></span> |
| <span data-ttu-id="85a1f-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="85a1f-327">stringEmpty</span></span> | <span data-ttu-id="85a1f-328">BOOL</span><span class="sxs-lookup"><span data-stu-id="85a1f-328">Bool</span></span> | <span data-ttu-id="85a1f-329">True</span><span class="sxs-lookup"><span data-stu-id="85a1f-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="85a1f-330">eerste</span><span class="sxs-lookup"><span data-stu-id="85a1f-330">first</span></span>
`first(arg1)`

<span data-ttu-id="85a1f-331">Retourneert Hallo eerste element van Hallo matrix of het eerste teken van Hallo tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="85a1f-331">Returns hello first element of hello array, or first character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="85a1f-332">Parameters</span><span class="sxs-lookup"><span data-stu-id="85a1f-332">Parameters</span></span>

| <span data-ttu-id="85a1f-333">Parameter</span><span class="sxs-lookup"><span data-stu-id="85a1f-333">Parameter</span></span> | <span data-ttu-id="85a1f-334">Vereist</span><span class="sxs-lookup"><span data-stu-id="85a1f-334">Required</span></span> | <span data-ttu-id="85a1f-335">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-335">Type</span></span> | <span data-ttu-id="85a1f-336">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85a1f-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="85a1f-337">Arg1</span><span class="sxs-lookup"><span data-stu-id="85a1f-337">arg1</span></span> |<span data-ttu-id="85a1f-338">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-338">Yes</span></span> |<span data-ttu-id="85a1f-339">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-339">array or string</span></span> |<span data-ttu-id="85a1f-340">Hallo waarde tooretrieve Hallo eerste element of teken.</span><span class="sxs-lookup"><span data-stu-id="85a1f-340">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="85a1f-341">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-341">Return value</span></span>

<span data-ttu-id="85a1f-342">Hallo type (string, int, matrix of object) Hallo eerste element in een matrix of Hallo eerste teken van een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="85a1f-342">hello type (string, int, array, or object) of hello first element in an array, or hello first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="85a1f-343">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85a1f-343">Example</span></span>

<span data-ttu-id="85a1f-344">Hallo volgende voorbeeld ziet u hoe toouse Hallo eerste functie met een matrix en de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="85a1f-344">hello following example shows how toouse hello first function with an array and string.</span></span>

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

<span data-ttu-id="85a1f-345">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-345">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-346">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-346">Name</span></span> | <span data-ttu-id="85a1f-347">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-347">Type</span></span> | <span data-ttu-id="85a1f-348">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-349">arrayOutput</span></span> | <span data-ttu-id="85a1f-350">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-350">String</span></span> | <span data-ttu-id="85a1f-351">een</span><span class="sxs-lookup"><span data-stu-id="85a1f-351">one</span></span> |
| <span data-ttu-id="85a1f-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-352">stringOutput</span></span> | <span data-ttu-id="85a1f-353">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-353">String</span></span> | <span data-ttu-id="85a1f-354">O</span><span class="sxs-lookup"><span data-stu-id="85a1f-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="85a1f-355">snijpunt</span><span class="sxs-lookup"><span data-stu-id="85a1f-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="85a1f-356">Retourneert een matrix of object met Hallo standaardelementen van Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="85a1f-356">Returns a single array or object with hello common elements from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="85a1f-357">Parameters</span><span class="sxs-lookup"><span data-stu-id="85a1f-357">Parameters</span></span>

| <span data-ttu-id="85a1f-358">Parameter</span><span class="sxs-lookup"><span data-stu-id="85a1f-358">Parameter</span></span> | <span data-ttu-id="85a1f-359">Vereist</span><span class="sxs-lookup"><span data-stu-id="85a1f-359">Required</span></span> | <span data-ttu-id="85a1f-360">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-360">Type</span></span> | <span data-ttu-id="85a1f-361">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85a1f-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="85a1f-362">Arg1</span><span class="sxs-lookup"><span data-stu-id="85a1f-362">arg1</span></span> |<span data-ttu-id="85a1f-363">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-363">Yes</span></span> |<span data-ttu-id="85a1f-364">matrix of object</span><span class="sxs-lookup"><span data-stu-id="85a1f-364">array or object</span></span> |<span data-ttu-id="85a1f-365">Hallo eerste waarde toouse voor het zoeken naar algemene elementen.</span><span class="sxs-lookup"><span data-stu-id="85a1f-365">hello first value toouse for finding common elements.</span></span> |
| <span data-ttu-id="85a1f-366">Arg2</span><span class="sxs-lookup"><span data-stu-id="85a1f-366">arg2</span></span> |<span data-ttu-id="85a1f-367">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-367">Yes</span></span> |<span data-ttu-id="85a1f-368">matrix of object</span><span class="sxs-lookup"><span data-stu-id="85a1f-368">array or object</span></span> |<span data-ttu-id="85a1f-369">Hallo tweede waarde toouse voor het zoeken naar algemene elementen.</span><span class="sxs-lookup"><span data-stu-id="85a1f-369">hello second value toouse for finding common elements.</span></span> |
| <span data-ttu-id="85a1f-370">Extra argumenten</span><span class="sxs-lookup"><span data-stu-id="85a1f-370">additional arguments</span></span> |<span data-ttu-id="85a1f-371">Nee</span><span class="sxs-lookup"><span data-stu-id="85a1f-371">No</span></span> |<span data-ttu-id="85a1f-372">matrix of object</span><span class="sxs-lookup"><span data-stu-id="85a1f-372">array or object</span></span> |<span data-ttu-id="85a1f-373">Aanvullende waarden toouse voor het zoeken naar algemene elementen.</span><span class="sxs-lookup"><span data-stu-id="85a1f-373">Additional values toouse for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="85a1f-374">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-374">Return value</span></span>

<span data-ttu-id="85a1f-375">Een matrix of object met Hallo algemene elementen.</span><span class="sxs-lookup"><span data-stu-id="85a1f-375">An array or object with hello common elements.</span></span>

### <a name="example"></a><span data-ttu-id="85a1f-376">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85a1f-376">Example</span></span>

<span data-ttu-id="85a1f-377">Hallo volgende voorbeeld wordt getoond hoe toouse snijpunt met matrices en objecten:</span><span class="sxs-lookup"><span data-stu-id="85a1f-377">hello following example shows how toouse intersection with arrays and objects:</span></span>

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

<span data-ttu-id="85a1f-378">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-378">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-379">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-379">Name</span></span> | <span data-ttu-id="85a1f-380">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-380">Type</span></span> | <span data-ttu-id="85a1f-381">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-382">objectOutput</span></span> | <span data-ttu-id="85a1f-383">Object</span><span class="sxs-lookup"><span data-stu-id="85a1f-383">Object</span></span> | <span data-ttu-id="85a1f-384">{"een": "a", "3": "c"}</span><span class="sxs-lookup"><span data-stu-id="85a1f-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="85a1f-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-385">arrayOutput</span></span> | <span data-ttu-id="85a1f-386">Matrix</span><span class="sxs-lookup"><span data-stu-id="85a1f-386">Array</span></span> | <span data-ttu-id="85a1f-387">["twee", "drie"]</span><span class="sxs-lookup"><span data-stu-id="85a1f-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="85a1f-388">JSON</span><span class="sxs-lookup"><span data-stu-id="85a1f-388">json</span></span>
`json(arg1)`

<span data-ttu-id="85a1f-389">Retourneert een JSON-object.</span><span class="sxs-lookup"><span data-stu-id="85a1f-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="85a1f-390">Parameters</span><span class="sxs-lookup"><span data-stu-id="85a1f-390">Parameters</span></span>

| <span data-ttu-id="85a1f-391">Parameter</span><span class="sxs-lookup"><span data-stu-id="85a1f-391">Parameter</span></span> | <span data-ttu-id="85a1f-392">Vereist</span><span class="sxs-lookup"><span data-stu-id="85a1f-392">Required</span></span> | <span data-ttu-id="85a1f-393">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-393">Type</span></span> | <span data-ttu-id="85a1f-394">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85a1f-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="85a1f-395">Arg1</span><span class="sxs-lookup"><span data-stu-id="85a1f-395">arg1</span></span> |<span data-ttu-id="85a1f-396">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-396">Yes</span></span> |<span data-ttu-id="85a1f-397">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-397">string</span></span> |<span data-ttu-id="85a1f-398">Hallo waarde tooconvert tooJSON.</span><span class="sxs-lookup"><span data-stu-id="85a1f-398">hello value tooconvert tooJSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="85a1f-399">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-399">Return value</span></span>

<span data-ttu-id="85a1f-400">Hallo JSON-object van het Hallo-opgegeven tekenreeks of een leeg object wanneer **null** is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="85a1f-400">hello JSON object from hello specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="85a1f-401">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85a1f-401">Example</span></span>

<span data-ttu-id="85a1f-402">Hallo volgende voorbeeld wordt getoond hoe toouse snijpunt met matrices en objecten:</span><span class="sxs-lookup"><span data-stu-id="85a1f-402">hello following example shows how toouse intersection with arrays and objects:</span></span>

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

<span data-ttu-id="85a1f-403">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-403">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-404">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-404">Name</span></span> | <span data-ttu-id="85a1f-405">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-405">Type</span></span> | <span data-ttu-id="85a1f-406">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-407">jsonOutput</span></span> | <span data-ttu-id="85a1f-408">Object</span><span class="sxs-lookup"><span data-stu-id="85a1f-408">Object</span></span> | <span data-ttu-id="85a1f-409">{"a": "b"}</span><span class="sxs-lookup"><span data-stu-id="85a1f-409">{"a": "b"}</span></span> |
| <span data-ttu-id="85a1f-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-410">nullOutput</span></span> | <span data-ttu-id="85a1f-411">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-411">Boolean</span></span> | <span data-ttu-id="85a1f-412">True</span><span class="sxs-lookup"><span data-stu-id="85a1f-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="85a1f-413">laatste</span><span class="sxs-lookup"><span data-stu-id="85a1f-413">last</span></span>
`last (arg1)`

<span data-ttu-id="85a1f-414">Retourneert Hallo laatste element van de matrix Hallo of laatste teken van het Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="85a1f-414">Returns hello last element of hello array, or last character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="85a1f-415">Parameters</span><span class="sxs-lookup"><span data-stu-id="85a1f-415">Parameters</span></span>

| <span data-ttu-id="85a1f-416">Parameter</span><span class="sxs-lookup"><span data-stu-id="85a1f-416">Parameter</span></span> | <span data-ttu-id="85a1f-417">Vereist</span><span class="sxs-lookup"><span data-stu-id="85a1f-417">Required</span></span> | <span data-ttu-id="85a1f-418">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-418">Type</span></span> | <span data-ttu-id="85a1f-419">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85a1f-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="85a1f-420">Arg1</span><span class="sxs-lookup"><span data-stu-id="85a1f-420">arg1</span></span> |<span data-ttu-id="85a1f-421">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-421">Yes</span></span> |<span data-ttu-id="85a1f-422">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-422">array or string</span></span> |<span data-ttu-id="85a1f-423">Hallo waarde tooretrieve Hallo laatste element of teken.</span><span class="sxs-lookup"><span data-stu-id="85a1f-423">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="85a1f-424">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-424">Return value</span></span>

<span data-ttu-id="85a1f-425">Hallo type (string, int, matrix of object) Hallo laatste element in een matrix of laatste teken Hallo van een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="85a1f-425">hello type (string, int, array, or object) of hello last element in an array, or hello last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="85a1f-426">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85a1f-426">Example</span></span>

<span data-ttu-id="85a1f-427">Hallo volgende voorbeeld ziet u hoe toouse Hallo laatste functie met een matrix en de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="85a1f-427">hello following example shows how toouse hello last function with an array and string.</span></span>

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

<span data-ttu-id="85a1f-428">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-429">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-429">Name</span></span> | <span data-ttu-id="85a1f-430">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-430">Type</span></span> | <span data-ttu-id="85a1f-431">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-432">arrayOutput</span></span> | <span data-ttu-id="85a1f-433">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-433">String</span></span> | <span data-ttu-id="85a1f-434">drie</span><span class="sxs-lookup"><span data-stu-id="85a1f-434">three</span></span> |
| <span data-ttu-id="85a1f-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-435">stringOutput</span></span> | <span data-ttu-id="85a1f-436">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-436">String</span></span> | <span data-ttu-id="85a1f-437">E</span><span class="sxs-lookup"><span data-stu-id="85a1f-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="85a1f-438">lengte</span><span class="sxs-lookup"><span data-stu-id="85a1f-438">length</span></span>
`length(arg1)`

<span data-ttu-id="85a1f-439">Retourneert het aantal elementen Hallo in een matrix of de tekens in een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="85a1f-439">Returns hello number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="85a1f-440">Parameters</span><span class="sxs-lookup"><span data-stu-id="85a1f-440">Parameters</span></span>

| <span data-ttu-id="85a1f-441">Parameter</span><span class="sxs-lookup"><span data-stu-id="85a1f-441">Parameter</span></span> | <span data-ttu-id="85a1f-442">Vereist</span><span class="sxs-lookup"><span data-stu-id="85a1f-442">Required</span></span> | <span data-ttu-id="85a1f-443">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-443">Type</span></span> | <span data-ttu-id="85a1f-444">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85a1f-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="85a1f-445">Arg1</span><span class="sxs-lookup"><span data-stu-id="85a1f-445">arg1</span></span> |<span data-ttu-id="85a1f-446">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-446">Yes</span></span> |<span data-ttu-id="85a1f-447">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-447">array or string</span></span> |<span data-ttu-id="85a1f-448">Hallo toouse voor het ophalen van het aantal elementen Hallo matrix of tekenreeks toouse voor het ophalen van het aantal tekens Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="85a1f-448">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="85a1f-449">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-449">Return value</span></span>

<span data-ttu-id="85a1f-450">Een int.</span><span class="sxs-lookup"><span data-stu-id="85a1f-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="85a1f-451">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85a1f-451">Example</span></span>

<span data-ttu-id="85a1f-452">Hallo volgende voorbeeld wordt getoond hoe toouse lengte met een matrix en de tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="85a1f-452">hello following example shows how toouse length with an array and string:</span></span>

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

<span data-ttu-id="85a1f-453">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-453">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-454">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-454">Name</span></span> | <span data-ttu-id="85a1f-455">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-455">Type</span></span> | <span data-ttu-id="85a1f-456">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="85a1f-457">arrayLength</span></span> | <span data-ttu-id="85a1f-458">int</span><span class="sxs-lookup"><span data-stu-id="85a1f-458">Int</span></span> | <span data-ttu-id="85a1f-459">3</span><span class="sxs-lookup"><span data-stu-id="85a1f-459">3</span></span> |
| <span data-ttu-id="85a1f-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="85a1f-460">stringLength</span></span> | <span data-ttu-id="85a1f-461">int</span><span class="sxs-lookup"><span data-stu-id="85a1f-461">Int</span></span> | <span data-ttu-id="85a1f-462">13</span><span class="sxs-lookup"><span data-stu-id="85a1f-462">13</span></span> |

<span data-ttu-id="85a1f-463">U kunt deze functie gebruiken met een matrix toospecify Hallo aantal iteraties bij het maken van resources.</span><span class="sxs-lookup"><span data-stu-id="85a1f-463">You can use this function with an array toospecify hello number of iterations when creating resources.</span></span> <span data-ttu-id="85a1f-464">Hallo in Hallo voorbeeld te volgen, parameter **siteNames** tooan matrix van namen toouse verwijzen bij het maken van websites Hallo.</span><span class="sxs-lookup"><span data-stu-id="85a1f-464">In hello following example, hello parameter **siteNames** would refer tooan array of names toouse when creating hello web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="85a1f-465">Zie voor meer informatie over het gebruik van deze functie met een matrix [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="85a1f-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="85a1f-466">min.</span><span class="sxs-lookup"><span data-stu-id="85a1f-466">min</span></span>
`min(arg1)`

<span data-ttu-id="85a1f-467">Retourneert Hallo minimumwaarde van een matrix van gehele getallen of een door komma's gescheiden lijst met gehele getallen zijn.</span><span class="sxs-lookup"><span data-stu-id="85a1f-467">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="85a1f-468">Parameters</span><span class="sxs-lookup"><span data-stu-id="85a1f-468">Parameters</span></span>

| <span data-ttu-id="85a1f-469">Parameter</span><span class="sxs-lookup"><span data-stu-id="85a1f-469">Parameter</span></span> | <span data-ttu-id="85a1f-470">Vereist</span><span class="sxs-lookup"><span data-stu-id="85a1f-470">Required</span></span> | <span data-ttu-id="85a1f-471">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-471">Type</span></span> | <span data-ttu-id="85a1f-472">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85a1f-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="85a1f-473">Arg1</span><span class="sxs-lookup"><span data-stu-id="85a1f-473">arg1</span></span> |<span data-ttu-id="85a1f-474">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-474">Yes</span></span> |<span data-ttu-id="85a1f-475">matrix van gehele getallen of door komma's gescheiden lijst met gehele getallen</span><span class="sxs-lookup"><span data-stu-id="85a1f-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="85a1f-476">Hallo verzameling tooget Hallo minimumwaarde.</span><span class="sxs-lookup"><span data-stu-id="85a1f-476">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="85a1f-477">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-477">Return value</span></span>

<span data-ttu-id="85a1f-478">Een int die Hallo minimale waarde vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="85a1f-478">An int representing hello minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="85a1f-479">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85a1f-479">Example</span></span>

<span data-ttu-id="85a1f-480">Hallo volgende voorbeeld wordt getoond hoe toouse min met een matrix en een lijst met gehele getallen zijn:</span><span class="sxs-lookup"><span data-stu-id="85a1f-480">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="85a1f-481">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-481">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-482">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-482">Name</span></span> | <span data-ttu-id="85a1f-483">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-483">Type</span></span> | <span data-ttu-id="85a1f-484">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-485">arrayOutput</span></span> | <span data-ttu-id="85a1f-486">int</span><span class="sxs-lookup"><span data-stu-id="85a1f-486">Int</span></span> | <span data-ttu-id="85a1f-487">0</span><span class="sxs-lookup"><span data-stu-id="85a1f-487">0</span></span> |
| <span data-ttu-id="85a1f-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-488">intOutput</span></span> | <span data-ttu-id="85a1f-489">int</span><span class="sxs-lookup"><span data-stu-id="85a1f-489">Int</span></span> | <span data-ttu-id="85a1f-490">0</span><span class="sxs-lookup"><span data-stu-id="85a1f-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="85a1f-491">Maximum aantal</span><span class="sxs-lookup"><span data-stu-id="85a1f-491">max</span></span>
`max(arg1)`

<span data-ttu-id="85a1f-492">Retourneert Hallo de maximumwaarde van een matrix van gehele getallen of een door komma's gescheiden lijst met gehele getallen.</span><span class="sxs-lookup"><span data-stu-id="85a1f-492">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="85a1f-493">Parameters</span><span class="sxs-lookup"><span data-stu-id="85a1f-493">Parameters</span></span>

| <span data-ttu-id="85a1f-494">Parameter</span><span class="sxs-lookup"><span data-stu-id="85a1f-494">Parameter</span></span> | <span data-ttu-id="85a1f-495">Vereist</span><span class="sxs-lookup"><span data-stu-id="85a1f-495">Required</span></span> | <span data-ttu-id="85a1f-496">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-496">Type</span></span> | <span data-ttu-id="85a1f-497">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85a1f-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="85a1f-498">Arg1</span><span class="sxs-lookup"><span data-stu-id="85a1f-498">arg1</span></span> |<span data-ttu-id="85a1f-499">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-499">Yes</span></span> |<span data-ttu-id="85a1f-500">matrix van gehele getallen of door komma's gescheiden lijst met gehele getallen</span><span class="sxs-lookup"><span data-stu-id="85a1f-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="85a1f-501">Hallo verzameling tooget Hallo maximale waarde.</span><span class="sxs-lookup"><span data-stu-id="85a1f-501">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="85a1f-502">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-502">Return value</span></span>

<span data-ttu-id="85a1f-503">Een int die de maximale waarde Hallo vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="85a1f-503">An int representing hello maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="85a1f-504">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85a1f-504">Example</span></span>

<span data-ttu-id="85a1f-505">Hallo volgende voorbeeld wordt getoond hoe toouse max met een matrix en een lijst met gehele getallen zijn:</span><span class="sxs-lookup"><span data-stu-id="85a1f-505">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="85a1f-506">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-506">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-507">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-507">Name</span></span> | <span data-ttu-id="85a1f-508">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-508">Type</span></span> | <span data-ttu-id="85a1f-509">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-510">arrayOutput</span></span> | <span data-ttu-id="85a1f-511">int</span><span class="sxs-lookup"><span data-stu-id="85a1f-511">Int</span></span> | <span data-ttu-id="85a1f-512">5</span><span class="sxs-lookup"><span data-stu-id="85a1f-512">5</span></span> |
| <span data-ttu-id="85a1f-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-513">intOutput</span></span> | <span data-ttu-id="85a1f-514">int</span><span class="sxs-lookup"><span data-stu-id="85a1f-514">Int</span></span> | <span data-ttu-id="85a1f-515">5</span><span class="sxs-lookup"><span data-stu-id="85a1f-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="85a1f-516">bereik</span><span class="sxs-lookup"><span data-stu-id="85a1f-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="85a1f-517">Maakt een matrix van gehele getallen van een geheel getal beginnen en met een aantal items.</span><span class="sxs-lookup"><span data-stu-id="85a1f-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="85a1f-518">Parameters</span><span class="sxs-lookup"><span data-stu-id="85a1f-518">Parameters</span></span>

| <span data-ttu-id="85a1f-519">Parameter</span><span class="sxs-lookup"><span data-stu-id="85a1f-519">Parameter</span></span> | <span data-ttu-id="85a1f-520">Vereist</span><span class="sxs-lookup"><span data-stu-id="85a1f-520">Required</span></span> | <span data-ttu-id="85a1f-521">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-521">Type</span></span> | <span data-ttu-id="85a1f-522">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85a1f-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="85a1f-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="85a1f-523">startingInteger</span></span> |<span data-ttu-id="85a1f-524">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-524">Yes</span></span> |<span data-ttu-id="85a1f-525">int</span><span class="sxs-lookup"><span data-stu-id="85a1f-525">int</span></span> |<span data-ttu-id="85a1f-526">Hallo eerste geheel getal in Hallo matrix.</span><span class="sxs-lookup"><span data-stu-id="85a1f-526">hello first integer in hello array.</span></span> |
| <span data-ttu-id="85a1f-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="85a1f-527">numberofElements</span></span> |<span data-ttu-id="85a1f-528">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-528">Yes</span></span> |<span data-ttu-id="85a1f-529">int</span><span class="sxs-lookup"><span data-stu-id="85a1f-529">int</span></span> |<span data-ttu-id="85a1f-530">Hallo-nummer van gehele getallen in de matrix Hallo.</span><span class="sxs-lookup"><span data-stu-id="85a1f-530">hello number of integers in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="85a1f-531">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-531">Return value</span></span>

<span data-ttu-id="85a1f-532">Een matrix van gehele getallen.</span><span class="sxs-lookup"><span data-stu-id="85a1f-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="85a1f-533">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85a1f-533">Example</span></span>

<span data-ttu-id="85a1f-534">Hallo volgende voorbeeld ziet u hoe toouse bereikfunctie Hallo:</span><span class="sxs-lookup"><span data-stu-id="85a1f-534">hello following example shows how toouse hello range function:</span></span>

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

<span data-ttu-id="85a1f-535">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-535">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-536">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-536">Name</span></span> | <span data-ttu-id="85a1f-537">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-537">Type</span></span> | <span data-ttu-id="85a1f-538">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-539">rangeOutput</span></span> | <span data-ttu-id="85a1f-540">Matrix</span><span class="sxs-lookup"><span data-stu-id="85a1f-540">Array</span></span> | <span data-ttu-id="85a1f-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="85a1f-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="85a1f-542">Overslaan</span><span class="sxs-lookup"><span data-stu-id="85a1f-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="85a1f-543">Retourneert een matrix met alle Hallo elementen nadat Hallo getal in Hallo-matrix opgegeven, of een tekenreeks waarin alle tekens worden Hallo retourneert nadat Hallo nummer in Hallo-tekenreeks opgegeven.</span><span class="sxs-lookup"><span data-stu-id="85a1f-543">Returns an array with all hello elements after hello specified number in hello array, or returns a string with all hello characters after hello specified number in hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="85a1f-544">Parameters</span><span class="sxs-lookup"><span data-stu-id="85a1f-544">Parameters</span></span>

| <span data-ttu-id="85a1f-545">Parameter</span><span class="sxs-lookup"><span data-stu-id="85a1f-545">Parameter</span></span> | <span data-ttu-id="85a1f-546">Vereist</span><span class="sxs-lookup"><span data-stu-id="85a1f-546">Required</span></span> | <span data-ttu-id="85a1f-547">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-547">Type</span></span> | <span data-ttu-id="85a1f-548">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85a1f-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="85a1f-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="85a1f-549">originalValue</span></span> |<span data-ttu-id="85a1f-550">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-550">Yes</span></span> |<span data-ttu-id="85a1f-551">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-551">array or string</span></span> |<span data-ttu-id="85a1f-552">Hallo toouse matrix of tekenreeks voor het overslaan.</span><span class="sxs-lookup"><span data-stu-id="85a1f-552">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="85a1f-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="85a1f-553">numberToSkip</span></span> |<span data-ttu-id="85a1f-554">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-554">Yes</span></span> |<span data-ttu-id="85a1f-555">int</span><span class="sxs-lookup"><span data-stu-id="85a1f-555">int</span></span> |<span data-ttu-id="85a1f-556">Hallo aantal elementen of tekens tooskip.</span><span class="sxs-lookup"><span data-stu-id="85a1f-556">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="85a1f-557">Als deze waarde 0 of minder is, alle elementen Hallo of tekens in Hallo-waarde worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="85a1f-557">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="85a1f-558">Als deze groter dan Hallo lengte van Hallo matrix of tekenreeks is, een lege matrix of tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="85a1f-558">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="85a1f-559">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-559">Return value</span></span>

<span data-ttu-id="85a1f-560">Een matrix of tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="85a1f-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="85a1f-561">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85a1f-561">Example</span></span>

<span data-ttu-id="85a1f-562">Hallo voorbeeld Slaat het Hallo na opgegeven aantal elementen in Hallo matrix en Hallo opgegeven aantal tekens in een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="85a1f-562">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

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

<span data-ttu-id="85a1f-563">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-563">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-564">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-564">Name</span></span> | <span data-ttu-id="85a1f-565">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-565">Type</span></span> | <span data-ttu-id="85a1f-566">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-567">arrayOutput</span></span> | <span data-ttu-id="85a1f-568">Matrix</span><span class="sxs-lookup"><span data-stu-id="85a1f-568">Array</span></span> | <span data-ttu-id="85a1f-569">["drie"]</span><span class="sxs-lookup"><span data-stu-id="85a1f-569">["three"]</span></span> |
| <span data-ttu-id="85a1f-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-570">stringOutput</span></span> | <span data-ttu-id="85a1f-571">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-571">String</span></span> | <span data-ttu-id="85a1f-572">twee drie</span><span class="sxs-lookup"><span data-stu-id="85a1f-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="85a1f-573">duren</span><span class="sxs-lookup"><span data-stu-id="85a1f-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="85a1f-574">Retourneert een matrix met Hallo aantal elementen vanaf opgegeven Hallo Hallo matrix is gestart, of een tekenreeks met Hallo opgegeven aantal tekens vanaf het begin van het Hallo-tekenreeks Hallo.</span><span class="sxs-lookup"><span data-stu-id="85a1f-574">Returns an array with hello specified number of elements from hello start of hello array, or a string with hello specified number of characters from hello start of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="85a1f-575">Parameters</span><span class="sxs-lookup"><span data-stu-id="85a1f-575">Parameters</span></span>

| <span data-ttu-id="85a1f-576">Parameter</span><span class="sxs-lookup"><span data-stu-id="85a1f-576">Parameter</span></span> | <span data-ttu-id="85a1f-577">Vereist</span><span class="sxs-lookup"><span data-stu-id="85a1f-577">Required</span></span> | <span data-ttu-id="85a1f-578">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-578">Type</span></span> | <span data-ttu-id="85a1f-579">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85a1f-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="85a1f-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="85a1f-580">originalValue</span></span> |<span data-ttu-id="85a1f-581">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-581">Yes</span></span> |<span data-ttu-id="85a1f-582">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-582">array or string</span></span> |<span data-ttu-id="85a1f-583">Hallo matrix of tekenreeks tootake Hallo elementen uit.</span><span class="sxs-lookup"><span data-stu-id="85a1f-583">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="85a1f-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="85a1f-584">numberToTake</span></span> |<span data-ttu-id="85a1f-585">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-585">Yes</span></span> |<span data-ttu-id="85a1f-586">int</span><span class="sxs-lookup"><span data-stu-id="85a1f-586">int</span></span> |<span data-ttu-id="85a1f-587">Hallo aantal elementen of tekens tootake.</span><span class="sxs-lookup"><span data-stu-id="85a1f-587">hello number of elements or characters tootake.</span></span> <span data-ttu-id="85a1f-588">Als deze waarde 0 of minder is, wordt een lege matrix of tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="85a1f-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="85a1f-589">Als het is groter dan de lengte Hallo Hallo gegeven matrix of tekenreeks, worden alle Hallo-elementen in het Hallo-matrix of tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="85a1f-589">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="85a1f-590">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-590">Return value</span></span>

<span data-ttu-id="85a1f-591">Een matrix of tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="85a1f-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="85a1f-592">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85a1f-592">Example</span></span>

<span data-ttu-id="85a1f-593">Hallo voorbeeld vergt Hallo na een opgegeven aantal elementen van een matrix van Hallo en tekens uit een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="85a1f-593">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

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

<span data-ttu-id="85a1f-594">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-594">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-595">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-595">Name</span></span> | <span data-ttu-id="85a1f-596">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-596">Type</span></span> | <span data-ttu-id="85a1f-597">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-598">arrayOutput</span></span> | <span data-ttu-id="85a1f-599">Matrix</span><span class="sxs-lookup"><span data-stu-id="85a1f-599">Array</span></span> | <span data-ttu-id="85a1f-600">['een', 'twee']</span><span class="sxs-lookup"><span data-stu-id="85a1f-600">["one", "two"]</span></span> |
| <span data-ttu-id="85a1f-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-601">stringOutput</span></span> | <span data-ttu-id="85a1f-602">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="85a1f-602">String</span></span> | <span data-ttu-id="85a1f-603">op</span><span class="sxs-lookup"><span data-stu-id="85a1f-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="85a1f-604">Union</span><span class="sxs-lookup"><span data-stu-id="85a1f-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="85a1f-605">Retourneert een matrix of object met alle elementen van Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="85a1f-605">Returns a single array or object with all elements from hello parameters.</span></span> <span data-ttu-id="85a1f-606">Dubbele waarden of sleutels zijn slechts één keer wordt opgenomen.</span><span class="sxs-lookup"><span data-stu-id="85a1f-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="85a1f-607">Parameters</span><span class="sxs-lookup"><span data-stu-id="85a1f-607">Parameters</span></span>

| <span data-ttu-id="85a1f-608">Parameter</span><span class="sxs-lookup"><span data-stu-id="85a1f-608">Parameter</span></span> | <span data-ttu-id="85a1f-609">Vereist</span><span class="sxs-lookup"><span data-stu-id="85a1f-609">Required</span></span> | <span data-ttu-id="85a1f-610">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-610">Type</span></span> | <span data-ttu-id="85a1f-611">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="85a1f-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="85a1f-612">Arg1</span><span class="sxs-lookup"><span data-stu-id="85a1f-612">arg1</span></span> |<span data-ttu-id="85a1f-613">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-613">Yes</span></span> |<span data-ttu-id="85a1f-614">matrix of object</span><span class="sxs-lookup"><span data-stu-id="85a1f-614">array or object</span></span> |<span data-ttu-id="85a1f-615">Hallo eerste waarde toouse om lid te worden elementen.</span><span class="sxs-lookup"><span data-stu-id="85a1f-615">hello first value toouse for joining elements.</span></span> |
| <span data-ttu-id="85a1f-616">Arg2</span><span class="sxs-lookup"><span data-stu-id="85a1f-616">arg2</span></span> |<span data-ttu-id="85a1f-617">Ja</span><span class="sxs-lookup"><span data-stu-id="85a1f-617">Yes</span></span> |<span data-ttu-id="85a1f-618">matrix of object</span><span class="sxs-lookup"><span data-stu-id="85a1f-618">array or object</span></span> |<span data-ttu-id="85a1f-619">Hallo tweede waarde toouse om lid te worden elementen.</span><span class="sxs-lookup"><span data-stu-id="85a1f-619">hello second value toouse for joining elements.</span></span> |
| <span data-ttu-id="85a1f-620">Extra argumenten</span><span class="sxs-lookup"><span data-stu-id="85a1f-620">additional arguments</span></span> |<span data-ttu-id="85a1f-621">Nee</span><span class="sxs-lookup"><span data-stu-id="85a1f-621">No</span></span> |<span data-ttu-id="85a1f-622">matrix of object</span><span class="sxs-lookup"><span data-stu-id="85a1f-622">array or object</span></span> |<span data-ttu-id="85a1f-623">Aanvullende waarden toouse om lid te worden elementen.</span><span class="sxs-lookup"><span data-stu-id="85a1f-623">Additional values toouse for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="85a1f-624">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-624">Return value</span></span>

<span data-ttu-id="85a1f-625">Een matrix of object.</span><span class="sxs-lookup"><span data-stu-id="85a1f-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="85a1f-626">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="85a1f-626">Example</span></span>

<span data-ttu-id="85a1f-627">Hallo volgende voorbeeld wordt getoond hoe toouse union met matrices en objecten:</span><span class="sxs-lookup"><span data-stu-id="85a1f-627">hello following example shows how toouse union with arrays and objects:</span></span>

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

<span data-ttu-id="85a1f-628">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="85a1f-628">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="85a1f-629">Naam</span><span class="sxs-lookup"><span data-stu-id="85a1f-629">Name</span></span> | <span data-ttu-id="85a1f-630">Type</span><span class="sxs-lookup"><span data-stu-id="85a1f-630">Type</span></span> | <span data-ttu-id="85a1f-631">Waarde</span><span class="sxs-lookup"><span data-stu-id="85a1f-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="85a1f-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-632">objectOutput</span></span> | <span data-ttu-id="85a1f-633">Object</span><span class="sxs-lookup"><span data-stu-id="85a1f-633">Object</span></span> | <span data-ttu-id="85a1f-634">{"een": "a", "twee": "b", "drie": "c", "4": "d", "vijf": "e"}</span><span class="sxs-lookup"><span data-stu-id="85a1f-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="85a1f-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="85a1f-635">arrayOutput</span></span> | <span data-ttu-id="85a1f-636">Matrix</span><span class="sxs-lookup"><span data-stu-id="85a1f-636">Array</span></span> | <span data-ttu-id="85a1f-637">['een', 'twee', 'drie', "vier"]</span><span class="sxs-lookup"><span data-stu-id="85a1f-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="85a1f-638">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="85a1f-638">Next steps</span></span>
* <span data-ttu-id="85a1f-639">Zie voor een beschrijving van de secties Hallo in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="85a1f-639">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="85a1f-640">toomerge meerdere sjablonen Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="85a1f-640">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="85a1f-641">een opgegeven aantal keren tooiterate bij het maken van een type resource, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="85a1f-641">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="85a1f-642">toosee hoe toodeploy Hallo sjabloon die u hebt gemaakt, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="85a1f-642">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

