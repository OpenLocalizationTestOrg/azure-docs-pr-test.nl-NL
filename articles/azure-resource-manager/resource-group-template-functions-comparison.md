---
title: aaaAzure Resource Manager-sjabloonfuncties - vergelijking | Microsoft Docs
description: Hierin wordt beschreven Hallo functies toouse in een Azure Resource Manager sjabloon toocompare waarden.
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
ms.openlocfilehash: ebcfc9ed6c93f8b540ec4c066e9457c621800b7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="72a56-103">Vergelijking van functies voor Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="72a56-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="72a56-104">Resource Manager biedt een aantal functies voor het maken van vergelijkingen in uw sjablonen.</span><span class="sxs-lookup"><span data-stu-id="72a56-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="72a56-105">is gelijk aan</span><span class="sxs-lookup"><span data-stu-id="72a56-105">equals</span></span>](#equals)
* [<span data-ttu-id="72a56-106">groter</span><span class="sxs-lookup"><span data-stu-id="72a56-106">greater</span></span>](#greater)
* [<span data-ttu-id="72a56-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="72a56-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="72a56-108">minder</span><span class="sxs-lookup"><span data-stu-id="72a56-108">less</span></span>](#less)
* [<span data-ttu-id="72a56-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="72a56-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="72a56-110">is gelijk aan</span><span class="sxs-lookup"><span data-stu-id="72a56-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="72a56-111">Controleert of twee waarden gelijk zijn aan elkaar.</span><span class="sxs-lookup"><span data-stu-id="72a56-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="72a56-112">Parameters</span><span class="sxs-lookup"><span data-stu-id="72a56-112">Parameters</span></span>

| <span data-ttu-id="72a56-113">Parameter</span><span class="sxs-lookup"><span data-stu-id="72a56-113">Parameter</span></span> | <span data-ttu-id="72a56-114">Vereist</span><span class="sxs-lookup"><span data-stu-id="72a56-114">Required</span></span> | <span data-ttu-id="72a56-115">Type</span><span class="sxs-lookup"><span data-stu-id="72a56-115">Type</span></span> | <span data-ttu-id="72a56-116">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72a56-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="72a56-117">Arg1</span><span class="sxs-lookup"><span data-stu-id="72a56-117">arg1</span></span> |<span data-ttu-id="72a56-118">Ja</span><span class="sxs-lookup"><span data-stu-id="72a56-118">Yes</span></span> |<span data-ttu-id="72a56-119">int, string, matrix of object</span><span class="sxs-lookup"><span data-stu-id="72a56-119">int, string, array, or object</span></span> |<span data-ttu-id="72a56-120">Hallo eerste waarde toocheck op gelijkheid.</span><span class="sxs-lookup"><span data-stu-id="72a56-120">hello first value toocheck for equality.</span></span> |
| <span data-ttu-id="72a56-121">Arg2</span><span class="sxs-lookup"><span data-stu-id="72a56-121">arg2</span></span> |<span data-ttu-id="72a56-122">Ja</span><span class="sxs-lookup"><span data-stu-id="72a56-122">Yes</span></span> |<span data-ttu-id="72a56-123">int, string, matrix of object</span><span class="sxs-lookup"><span data-stu-id="72a56-123">int, string, array, or object</span></span> |<span data-ttu-id="72a56-124">Hallo tweede waarde toocheck op gelijkheid.</span><span class="sxs-lookup"><span data-stu-id="72a56-124">hello second value toocheck for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="72a56-125">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="72a56-125">Return value</span></span>

<span data-ttu-id="72a56-126">Retourneert **True** als Hallo waarden gelijk zijn, anders wordt **False**.</span><span class="sxs-lookup"><span data-stu-id="72a56-126">Returns **True** if hello values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="72a56-127">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="72a56-127">Remarks</span></span>

<span data-ttu-id="72a56-128">Hallo gelijk is aan de functie wordt vaak gebruikt met Hallo `condition` tootest element of een resource wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="72a56-128">hello equals function is often used with hello `condition` element tootest whether a resource is deployed.</span></span>

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

### <a name="example"></a><span data-ttu-id="72a56-129">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="72a56-129">Example</span></span>

<span data-ttu-id="72a56-130">Hallo-voorbeeldsjabloon verschillende soorten waarden voor gelijkheid wordt gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="72a56-130">hello example template checks different types of values for equality.</span></span> <span data-ttu-id="72a56-131">Standaardwaarden voor alle Hallo retourneren True.</span><span class="sxs-lookup"><span data-stu-id="72a56-131">All hello default values return True.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 1
        },
        "firstString": {
            "type": "string",
            "defaultValue": "a"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "firstObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[equals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[equals(parameters('firstString'), parameters('secondString'))]"
        },
        "checkArrays": {
            "type": "bool",
            "value": "[equals(parameters('firstArray'), parameters('secondArray'))]"
        },
        "checkObjects": {
            "type": "bool",
            "value": "[equals(parameters('firstObject'), parameters('secondObject'))]"
        }
    }
}
```

<span data-ttu-id="72a56-132">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="72a56-132">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="72a56-133">Naam</span><span class="sxs-lookup"><span data-stu-id="72a56-133">Name</span></span> | <span data-ttu-id="72a56-134">Type</span><span class="sxs-lookup"><span data-stu-id="72a56-134">Type</span></span> | <span data-ttu-id="72a56-135">Waarde</span><span class="sxs-lookup"><span data-stu-id="72a56-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="72a56-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="72a56-136">checkInts</span></span> | <span data-ttu-id="72a56-137">BOOL</span><span class="sxs-lookup"><span data-stu-id="72a56-137">Bool</span></span> | <span data-ttu-id="72a56-138">True</span><span class="sxs-lookup"><span data-stu-id="72a56-138">True</span></span> |
| <span data-ttu-id="72a56-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="72a56-139">checkStrings</span></span> | <span data-ttu-id="72a56-140">BOOL</span><span class="sxs-lookup"><span data-stu-id="72a56-140">Bool</span></span> | <span data-ttu-id="72a56-141">True</span><span class="sxs-lookup"><span data-stu-id="72a56-141">True</span></span> |
| <span data-ttu-id="72a56-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="72a56-142">checkArrays</span></span> | <span data-ttu-id="72a56-143">BOOL</span><span class="sxs-lookup"><span data-stu-id="72a56-143">Bool</span></span> | <span data-ttu-id="72a56-144">True</span><span class="sxs-lookup"><span data-stu-id="72a56-144">True</span></span> |
| <span data-ttu-id="72a56-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="72a56-145">checkObjects</span></span> | <span data-ttu-id="72a56-146">BOOL</span><span class="sxs-lookup"><span data-stu-id="72a56-146">Bool</span></span> | <span data-ttu-id="72a56-147">True</span><span class="sxs-lookup"><span data-stu-id="72a56-147">True</span></span> |


<span data-ttu-id="72a56-148">Hallo volgende voorbeeld wordt [niet](resource-group-template-functions-logical.md#not) met **gelijk is aan**.</span><span class="sxs-lookup"><span data-stu-id="72a56-148">hello following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="72a56-149">Hallo-uitvoer van het voorgaande voorbeeld Hallo is:</span><span class="sxs-lookup"><span data-stu-id="72a56-149">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="72a56-150">Naam</span><span class="sxs-lookup"><span data-stu-id="72a56-150">Name</span></span> | <span data-ttu-id="72a56-151">Type</span><span class="sxs-lookup"><span data-stu-id="72a56-151">Type</span></span> | <span data-ttu-id="72a56-152">Waarde</span><span class="sxs-lookup"><span data-stu-id="72a56-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="72a56-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="72a56-153">checkNotEquals</span></span> | <span data-ttu-id="72a56-154">BOOL</span><span class="sxs-lookup"><span data-stu-id="72a56-154">Bool</span></span> | <span data-ttu-id="72a56-155">True</span><span class="sxs-lookup"><span data-stu-id="72a56-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="72a56-156">groter</span><span class="sxs-lookup"><span data-stu-id="72a56-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="72a56-157">Controleert of de eerste waarde Hallo groter dan de tweede waarde Hallo is.</span><span class="sxs-lookup"><span data-stu-id="72a56-157">Checks whether hello first value is greater than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="72a56-158">Parameters</span><span class="sxs-lookup"><span data-stu-id="72a56-158">Parameters</span></span>

| <span data-ttu-id="72a56-159">Parameter</span><span class="sxs-lookup"><span data-stu-id="72a56-159">Parameter</span></span> | <span data-ttu-id="72a56-160">Vereist</span><span class="sxs-lookup"><span data-stu-id="72a56-160">Required</span></span> | <span data-ttu-id="72a56-161">Type</span><span class="sxs-lookup"><span data-stu-id="72a56-161">Type</span></span> | <span data-ttu-id="72a56-162">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72a56-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="72a56-163">Arg1</span><span class="sxs-lookup"><span data-stu-id="72a56-163">arg1</span></span> |<span data-ttu-id="72a56-164">Ja</span><span class="sxs-lookup"><span data-stu-id="72a56-164">Yes</span></span> |<span data-ttu-id="72a56-165">int of string</span><span class="sxs-lookup"><span data-stu-id="72a56-165">int or string</span></span> |<span data-ttu-id="72a56-166">de eerste waarde Hallo voor Hallo groter vergelijking.</span><span class="sxs-lookup"><span data-stu-id="72a56-166">hello first value for hello greater comparison.</span></span> |
| <span data-ttu-id="72a56-167">Arg2</span><span class="sxs-lookup"><span data-stu-id="72a56-167">arg2</span></span> |<span data-ttu-id="72a56-168">Ja</span><span class="sxs-lookup"><span data-stu-id="72a56-168">Yes</span></span> |<span data-ttu-id="72a56-169">int of string</span><span class="sxs-lookup"><span data-stu-id="72a56-169">int or string</span></span> |<span data-ttu-id="72a56-170">tweede waarde Hallo voor Hallo groter vergelijking.</span><span class="sxs-lookup"><span data-stu-id="72a56-170">hello second value for hello greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="72a56-171">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="72a56-171">Return value</span></span>

<span data-ttu-id="72a56-172">Retourneert **True** als de eerste waarde Hallo groter is dan de tweede waarde hello, anders wordt **False**.</span><span class="sxs-lookup"><span data-stu-id="72a56-172">Returns **True** if hello first value is greater than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="72a56-173">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="72a56-173">Example</span></span>

<span data-ttu-id="72a56-174">Hallo-voorbeeldsjabloon controleert of Hallo één waarde groter is dan Hallo andere.</span><span class="sxs-lookup"><span data-stu-id="72a56-174">hello example template checks whether hello one value is greater than hello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greater(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greater(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="72a56-175">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="72a56-175">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="72a56-176">Naam</span><span class="sxs-lookup"><span data-stu-id="72a56-176">Name</span></span> | <span data-ttu-id="72a56-177">Type</span><span class="sxs-lookup"><span data-stu-id="72a56-177">Type</span></span> | <span data-ttu-id="72a56-178">Waarde</span><span class="sxs-lookup"><span data-stu-id="72a56-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="72a56-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="72a56-179">checkInts</span></span> | <span data-ttu-id="72a56-180">BOOL</span><span class="sxs-lookup"><span data-stu-id="72a56-180">Bool</span></span> | <span data-ttu-id="72a56-181">False</span><span class="sxs-lookup"><span data-stu-id="72a56-181">False</span></span> |
| <span data-ttu-id="72a56-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="72a56-182">checkStrings</span></span> | <span data-ttu-id="72a56-183">BOOL</span><span class="sxs-lookup"><span data-stu-id="72a56-183">Bool</span></span> | <span data-ttu-id="72a56-184">True</span><span class="sxs-lookup"><span data-stu-id="72a56-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="72a56-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="72a56-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="72a56-186">Controleert of de eerste waarde Hallo groter dan of gelijk toohello tweede waarde.</span><span class="sxs-lookup"><span data-stu-id="72a56-186">Checks whether hello first value is greater than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="72a56-187">Parameters</span><span class="sxs-lookup"><span data-stu-id="72a56-187">Parameters</span></span>

| <span data-ttu-id="72a56-188">Parameter</span><span class="sxs-lookup"><span data-stu-id="72a56-188">Parameter</span></span> | <span data-ttu-id="72a56-189">Vereist</span><span class="sxs-lookup"><span data-stu-id="72a56-189">Required</span></span> | <span data-ttu-id="72a56-190">Type</span><span class="sxs-lookup"><span data-stu-id="72a56-190">Type</span></span> | <span data-ttu-id="72a56-191">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72a56-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="72a56-192">Arg1</span><span class="sxs-lookup"><span data-stu-id="72a56-192">arg1</span></span> |<span data-ttu-id="72a56-193">Ja</span><span class="sxs-lookup"><span data-stu-id="72a56-193">Yes</span></span> |<span data-ttu-id="72a56-194">int of string</span><span class="sxs-lookup"><span data-stu-id="72a56-194">int or string</span></span> |<span data-ttu-id="72a56-195">de eerste waarde Hallo voor vergelijking van Hallo groter of gelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="72a56-195">hello first value for hello greater or equal comparison.</span></span> |
| <span data-ttu-id="72a56-196">Arg2</span><span class="sxs-lookup"><span data-stu-id="72a56-196">arg2</span></span> |<span data-ttu-id="72a56-197">Ja</span><span class="sxs-lookup"><span data-stu-id="72a56-197">Yes</span></span> |<span data-ttu-id="72a56-198">int of string</span><span class="sxs-lookup"><span data-stu-id="72a56-198">int or string</span></span> |<span data-ttu-id="72a56-199">tweede waarde Hallo voor vergelijking van Hallo groter of gelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="72a56-199">hello second value for hello greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="72a56-200">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="72a56-200">Return value</span></span>

<span data-ttu-id="72a56-201">Retourneert **True** als de eerste waarde Hallo tweede waarde groter dan of gelijk toohello; anders **False**.</span><span class="sxs-lookup"><span data-stu-id="72a56-201">Returns **True** if hello first value is greater than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="72a56-202">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="72a56-202">Example</span></span>

<span data-ttu-id="72a56-203">Hallo-voorbeeldsjabloon controleert of Hallo één waarde groter dan of gelijk toohello andere.</span><span class="sxs-lookup"><span data-stu-id="72a56-203">hello example template checks whether hello one value is greater than or equal toohello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="72a56-204">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="72a56-204">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="72a56-205">Naam</span><span class="sxs-lookup"><span data-stu-id="72a56-205">Name</span></span> | <span data-ttu-id="72a56-206">Type</span><span class="sxs-lookup"><span data-stu-id="72a56-206">Type</span></span> | <span data-ttu-id="72a56-207">Waarde</span><span class="sxs-lookup"><span data-stu-id="72a56-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="72a56-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="72a56-208">checkInts</span></span> | <span data-ttu-id="72a56-209">BOOL</span><span class="sxs-lookup"><span data-stu-id="72a56-209">Bool</span></span> | <span data-ttu-id="72a56-210">False</span><span class="sxs-lookup"><span data-stu-id="72a56-210">False</span></span> |
| <span data-ttu-id="72a56-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="72a56-211">checkStrings</span></span> | <span data-ttu-id="72a56-212">BOOL</span><span class="sxs-lookup"><span data-stu-id="72a56-212">Bool</span></span> | <span data-ttu-id="72a56-213">True</span><span class="sxs-lookup"><span data-stu-id="72a56-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="72a56-214">minder</span><span class="sxs-lookup"><span data-stu-id="72a56-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="72a56-215">Controleert of de eerste waarde Hallo kleiner is dan Hallo tweede waarde.</span><span class="sxs-lookup"><span data-stu-id="72a56-215">Checks whether hello first value is less than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="72a56-216">Parameters</span><span class="sxs-lookup"><span data-stu-id="72a56-216">Parameters</span></span>

| <span data-ttu-id="72a56-217">Parameter</span><span class="sxs-lookup"><span data-stu-id="72a56-217">Parameter</span></span> | <span data-ttu-id="72a56-218">Vereist</span><span class="sxs-lookup"><span data-stu-id="72a56-218">Required</span></span> | <span data-ttu-id="72a56-219">Type</span><span class="sxs-lookup"><span data-stu-id="72a56-219">Type</span></span> | <span data-ttu-id="72a56-220">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72a56-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="72a56-221">Arg1</span><span class="sxs-lookup"><span data-stu-id="72a56-221">arg1</span></span> |<span data-ttu-id="72a56-222">Ja</span><span class="sxs-lookup"><span data-stu-id="72a56-222">Yes</span></span> |<span data-ttu-id="72a56-223">int of string</span><span class="sxs-lookup"><span data-stu-id="72a56-223">int or string</span></span> |<span data-ttu-id="72a56-224">de eerste waarde Hallo voor Hallo minder vergelijking.</span><span class="sxs-lookup"><span data-stu-id="72a56-224">hello first value for hello less comparison.</span></span> |
| <span data-ttu-id="72a56-225">Arg2</span><span class="sxs-lookup"><span data-stu-id="72a56-225">arg2</span></span> |<span data-ttu-id="72a56-226">Ja</span><span class="sxs-lookup"><span data-stu-id="72a56-226">Yes</span></span> |<span data-ttu-id="72a56-227">int of string</span><span class="sxs-lookup"><span data-stu-id="72a56-227">int or string</span></span> |<span data-ttu-id="72a56-228">tweede waarde Hallo voor Hallo minder vergelijking.</span><span class="sxs-lookup"><span data-stu-id="72a56-228">hello second value for hello less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="72a56-229">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="72a56-229">Return value</span></span>

<span data-ttu-id="72a56-230">Retourneert **True** als Hallo eerste waarde kleiner dan Hallo is tweede waarde; anders **False**.</span><span class="sxs-lookup"><span data-stu-id="72a56-230">Returns **True** if hello first value is less than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="72a56-231">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="72a56-231">Example</span></span>

<span data-ttu-id="72a56-232">Hallo-voorbeeldsjabloon controleert of Hallo een waarde lager is dan andere Hallo.</span><span class="sxs-lookup"><span data-stu-id="72a56-232">hello example template checks whether hello one value is less than hello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[less(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[less(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="72a56-233">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="72a56-233">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="72a56-234">Naam</span><span class="sxs-lookup"><span data-stu-id="72a56-234">Name</span></span> | <span data-ttu-id="72a56-235">Type</span><span class="sxs-lookup"><span data-stu-id="72a56-235">Type</span></span> | <span data-ttu-id="72a56-236">Waarde</span><span class="sxs-lookup"><span data-stu-id="72a56-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="72a56-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="72a56-237">checkInts</span></span> | <span data-ttu-id="72a56-238">BOOL</span><span class="sxs-lookup"><span data-stu-id="72a56-238">Bool</span></span> | <span data-ttu-id="72a56-239">True</span><span class="sxs-lookup"><span data-stu-id="72a56-239">True</span></span> |
| <span data-ttu-id="72a56-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="72a56-240">checkStrings</span></span> | <span data-ttu-id="72a56-241">BOOL</span><span class="sxs-lookup"><span data-stu-id="72a56-241">Bool</span></span> | <span data-ttu-id="72a56-242">False</span><span class="sxs-lookup"><span data-stu-id="72a56-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="72a56-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="72a56-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="72a56-244">Controleert of de eerste waarde Hallo kleiner dan of gelijk toohello tweede waarde.</span><span class="sxs-lookup"><span data-stu-id="72a56-244">Checks whether hello first value is less than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="72a56-245">Parameters</span><span class="sxs-lookup"><span data-stu-id="72a56-245">Parameters</span></span>

| <span data-ttu-id="72a56-246">Parameter</span><span class="sxs-lookup"><span data-stu-id="72a56-246">Parameter</span></span> | <span data-ttu-id="72a56-247">Vereist</span><span class="sxs-lookup"><span data-stu-id="72a56-247">Required</span></span> | <span data-ttu-id="72a56-248">Type</span><span class="sxs-lookup"><span data-stu-id="72a56-248">Type</span></span> | <span data-ttu-id="72a56-249">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="72a56-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="72a56-250">Arg1</span><span class="sxs-lookup"><span data-stu-id="72a56-250">arg1</span></span> |<span data-ttu-id="72a56-251">Ja</span><span class="sxs-lookup"><span data-stu-id="72a56-251">Yes</span></span> |<span data-ttu-id="72a56-252">int of string</span><span class="sxs-lookup"><span data-stu-id="72a56-252">int or string</span></span> |<span data-ttu-id="72a56-253">de eerste waarde Hallo voor Hallo kleiner of gelijk is aan vergelijking.</span><span class="sxs-lookup"><span data-stu-id="72a56-253">hello first value for hello less or equals comparison.</span></span> |
| <span data-ttu-id="72a56-254">Arg2</span><span class="sxs-lookup"><span data-stu-id="72a56-254">arg2</span></span> |<span data-ttu-id="72a56-255">Ja</span><span class="sxs-lookup"><span data-stu-id="72a56-255">Yes</span></span> |<span data-ttu-id="72a56-256">int of string</span><span class="sxs-lookup"><span data-stu-id="72a56-256">int or string</span></span> |<span data-ttu-id="72a56-257">tweede waarde voor Hallo minder Hallo of gelijk aan de vergelijking.</span><span class="sxs-lookup"><span data-stu-id="72a56-257">hello second value for hello less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="72a56-258">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="72a56-258">Return value</span></span>

<span data-ttu-id="72a56-259">Retourneert **True** als de eerste waarde Hallo kleiner dan of gelijk is toohello tweede waarde; anders **False**.</span><span class="sxs-lookup"><span data-stu-id="72a56-259">Returns **True** if hello first value is less than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="72a56-260">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="72a56-260">Example</span></span>

<span data-ttu-id="72a56-261">Hallo voorbeeldsjabloon controleert of Hallo één waarde kleiner dan of gelijk is toohello andere.</span><span class="sxs-lookup"><span data-stu-id="72a56-261">hello example template checks whether hello one value is less than or equal toohello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="72a56-262">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="72a56-262">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="72a56-263">Naam</span><span class="sxs-lookup"><span data-stu-id="72a56-263">Name</span></span> | <span data-ttu-id="72a56-264">Type</span><span class="sxs-lookup"><span data-stu-id="72a56-264">Type</span></span> | <span data-ttu-id="72a56-265">Waarde</span><span class="sxs-lookup"><span data-stu-id="72a56-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="72a56-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="72a56-266">checkInts</span></span> | <span data-ttu-id="72a56-267">BOOL</span><span class="sxs-lookup"><span data-stu-id="72a56-267">Bool</span></span> | <span data-ttu-id="72a56-268">True</span><span class="sxs-lookup"><span data-stu-id="72a56-268">True</span></span> |
| <span data-ttu-id="72a56-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="72a56-269">checkStrings</span></span> | <span data-ttu-id="72a56-270">BOOL</span><span class="sxs-lookup"><span data-stu-id="72a56-270">Bool</span></span> | <span data-ttu-id="72a56-271">False</span><span class="sxs-lookup"><span data-stu-id="72a56-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="72a56-272">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="72a56-272">Next steps</span></span>
* <span data-ttu-id="72a56-273">Zie voor een beschrijving van de secties Hallo in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="72a56-273">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="72a56-274">toomerge meerdere sjablonen Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="72a56-274">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="72a56-275">een opgegeven aantal keren tooiterate bij het maken van een type resource, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="72a56-275">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="72a56-276">toosee hoe toodeploy Hallo sjabloon die u hebt gemaakt, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="72a56-276">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

