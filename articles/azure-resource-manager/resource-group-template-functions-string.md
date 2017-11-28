---
title: aaaAzure Resource Manager-sjabloonfuncties - string | Microsoft Docs
description: Hierin wordt beschreven Hallo functies toouse in een Azure Resource Manager-sjabloon toowork met tekenreeksen.
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
ms.openlocfilehash: 27f7f6a52cbe4e9915718184433e92ca92999346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="9811a-103">Tekenreeks-functies voor Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="9811a-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="9811a-104">Resource Manager biedt Hallo functies voor het werken met tekenreeksen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9811a-104">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="9811a-105">Base64</span><span class="sxs-lookup"><span data-stu-id="9811a-105">base64</span></span>](#base64)
* [<span data-ttu-id="9811a-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="9811a-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="9811a-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="9811a-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="9811a-108">concat</span><span class="sxs-lookup"><span data-stu-id="9811a-108">concat</span></span>](#concat)
* [<span data-ttu-id="9811a-109">bevat</span><span class="sxs-lookup"><span data-stu-id="9811a-109">contains</span></span>](#contains)
* [<span data-ttu-id="9811a-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="9811a-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="9811a-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="9811a-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="9811a-112">leeg</span><span class="sxs-lookup"><span data-stu-id="9811a-112">empty</span></span>](#empty)
* [<span data-ttu-id="9811a-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="9811a-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="9811a-114">eerste</span><span class="sxs-lookup"><span data-stu-id="9811a-114">first</span></span>](#first)
* [<span data-ttu-id="9811a-115">indexOf</span><span class="sxs-lookup"><span data-stu-id="9811a-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="9811a-116">laatste</span><span class="sxs-lookup"><span data-stu-id="9811a-116">last</span></span>](#last)
* [<span data-ttu-id="9811a-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="9811a-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="9811a-118">lengte</span><span class="sxs-lookup"><span data-stu-id="9811a-118">length</span></span>](#length)
* [<span data-ttu-id="9811a-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="9811a-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="9811a-120">vervangen</span><span class="sxs-lookup"><span data-stu-id="9811a-120">replace</span></span>](#replace)
* [<span data-ttu-id="9811a-121">overslaan</span><span class="sxs-lookup"><span data-stu-id="9811a-121">skip</span></span>](#skip)
* [<span data-ttu-id="9811a-122">split</span><span class="sxs-lookup"><span data-stu-id="9811a-122">split</span></span>](#split)
* [<span data-ttu-id="9811a-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="9811a-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="9811a-124">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-124">string</span></span>](#string)
* [<span data-ttu-id="9811a-125">de subtekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-125">substring</span></span>](#substring)
* [<span data-ttu-id="9811a-126">duren</span><span class="sxs-lookup"><span data-stu-id="9811a-126">take</span></span>](#take)
* [<span data-ttu-id="9811a-127">toLower</span><span class="sxs-lookup"><span data-stu-id="9811a-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="9811a-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="9811a-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="9811a-129">Trim</span><span class="sxs-lookup"><span data-stu-id="9811a-129">trim</span></span>](#trim)
* [<span data-ttu-id="9811a-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="9811a-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="9811a-131">URI</span><span class="sxs-lookup"><span data-stu-id="9811a-131">uri</span></span>](#uri)
* [<span data-ttu-id="9811a-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="9811a-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="9811a-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="9811a-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="9811a-134">Base64</span><span class="sxs-lookup"><span data-stu-id="9811a-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="9811a-135">Retourneert Hallo base64-weergave van de invoertekenreeks Hallo.</span><span class="sxs-lookup"><span data-stu-id="9811a-135">Returns hello base64 representation of hello input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-136">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-136">Parameters</span></span>

| <span data-ttu-id="9811a-137">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-137">Parameter</span></span> | <span data-ttu-id="9811a-138">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-138">Required</span></span> | <span data-ttu-id="9811a-139">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-139">Type</span></span> | <span data-ttu-id="9811a-140">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-141">inputString</span><span class="sxs-lookup"><span data-stu-id="9811a-141">inputString</span></span> |<span data-ttu-id="9811a-142">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-142">Yes</span></span> |<span data-ttu-id="9811a-143">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-143">string</span></span> |<span data-ttu-id="9811a-144">Hallo waarde tooreturn als een base64-weergave.</span><span class="sxs-lookup"><span data-stu-id="9811a-144">hello value tooreturn as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-145">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-145">Return value</span></span>

<span data-ttu-id="9811a-146">Een tekenreeks met Hallo base64-weergave.</span><span class="sxs-lookup"><span data-stu-id="9811a-146">A string containing hello base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-147">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-147">Examples</span></span>

<span data-ttu-id="9811a-148">Hallo volgende voorbeeld ziet u hoe toouse Hallo base64-functie.</span><span class="sxs-lookup"><span data-stu-id="9811a-148">hello following example shows how toouse hello base64 function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="9811a-149">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-149">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-150">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-150">Name</span></span> | <span data-ttu-id="9811a-151">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-151">Type</span></span> | <span data-ttu-id="9811a-152">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="9811a-153">base64Output</span></span> | <span data-ttu-id="9811a-154">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-154">String</span></span> | <span data-ttu-id="9811a-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="9811a-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="9811a-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-156">toStringOutput</span></span> | <span data-ttu-id="9811a-157">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-157">String</span></span> | <span data-ttu-id="9811a-158">Een twee drie</span><span class="sxs-lookup"><span data-stu-id="9811a-158">one, two, three</span></span> |
| <span data-ttu-id="9811a-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-159">toJsonOutput</span></span> | <span data-ttu-id="9811a-160">Object</span><span class="sxs-lookup"><span data-stu-id="9811a-160">Object</span></span> | <span data-ttu-id="9811a-161">{"een": "a", "twee": "b"}</span><span class="sxs-lookup"><span data-stu-id="9811a-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="9811a-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="9811a-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="9811a-163">Converteert een base64-weergave tooa JSON-object.</span><span class="sxs-lookup"><span data-stu-id="9811a-163">Converts a base64 representation tooa JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-164">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-164">Parameters</span></span>

| <span data-ttu-id="9811a-165">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-165">Parameter</span></span> | <span data-ttu-id="9811a-166">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-166">Required</span></span> | <span data-ttu-id="9811a-167">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-167">Type</span></span> | <span data-ttu-id="9811a-168">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-169">base64Value</span><span class="sxs-lookup"><span data-stu-id="9811a-169">base64Value</span></span> |<span data-ttu-id="9811a-170">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-170">Yes</span></span> |<span data-ttu-id="9811a-171">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-171">string</span></span> |<span data-ttu-id="9811a-172">Hallo base64-weergave tooconvert tooa JSON-object.</span><span class="sxs-lookup"><span data-stu-id="9811a-172">hello base64 representation tooconvert tooa JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-173">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-173">Return value</span></span>

<span data-ttu-id="9811a-174">Een JSON-object.</span><span class="sxs-lookup"><span data-stu-id="9811a-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-175">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-175">Examples</span></span>

<span data-ttu-id="9811a-176">Hallo wordt volgende voorbeeld Hallo base64ToJson functie tooconvert een base64-waarde:</span><span class="sxs-lookup"><span data-stu-id="9811a-176">hello following example uses hello base64ToJson function tooconvert a base64 value:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="9811a-177">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-177">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-178">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-178">Name</span></span> | <span data-ttu-id="9811a-179">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-179">Type</span></span> | <span data-ttu-id="9811a-180">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="9811a-181">base64Output</span></span> | <span data-ttu-id="9811a-182">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-182">String</span></span> | <span data-ttu-id="9811a-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="9811a-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="9811a-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-184">toStringOutput</span></span> | <span data-ttu-id="9811a-185">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-185">String</span></span> | <span data-ttu-id="9811a-186">Een twee drie</span><span class="sxs-lookup"><span data-stu-id="9811a-186">one, two, three</span></span> |
| <span data-ttu-id="9811a-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-187">toJsonOutput</span></span> | <span data-ttu-id="9811a-188">Object</span><span class="sxs-lookup"><span data-stu-id="9811a-188">Object</span></span> | <span data-ttu-id="9811a-189">{"een": "a", "twee": "b"}</span><span class="sxs-lookup"><span data-stu-id="9811a-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="9811a-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="9811a-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="9811a-191">Zet een tekenreeks met base64-weergave tooa.</span><span class="sxs-lookup"><span data-stu-id="9811a-191">Converts a base64 representation tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-192">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-192">Parameters</span></span>

| <span data-ttu-id="9811a-193">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-193">Parameter</span></span> | <span data-ttu-id="9811a-194">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-194">Required</span></span> | <span data-ttu-id="9811a-195">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-195">Type</span></span> | <span data-ttu-id="9811a-196">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-197">base64Value</span><span class="sxs-lookup"><span data-stu-id="9811a-197">base64Value</span></span> |<span data-ttu-id="9811a-198">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-198">Yes</span></span> |<span data-ttu-id="9811a-199">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-199">string</span></span> |<span data-ttu-id="9811a-200">Hallo base64-weergave tooconvert tooa tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-200">hello base64 representation tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-201">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-201">Return value</span></span>

<span data-ttu-id="9811a-202">Een tekenreeks van Hallo geconverteerd base64-waarde.</span><span class="sxs-lookup"><span data-stu-id="9811a-202">A string of hello converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-203">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-203">Examples</span></span>

<span data-ttu-id="9811a-204">Hallo wordt volgende voorbeeld Hallo base64ToString functie tooconvert een base64-waarde:</span><span class="sxs-lookup"><span data-stu-id="9811a-204">hello following example uses hello base64ToString function tooconvert a base64 value:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="9811a-205">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-205">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-206">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-206">Name</span></span> | <span data-ttu-id="9811a-207">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-207">Type</span></span> | <span data-ttu-id="9811a-208">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="9811a-209">base64Output</span></span> | <span data-ttu-id="9811a-210">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-210">String</span></span> | <span data-ttu-id="9811a-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="9811a-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="9811a-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-212">toStringOutput</span></span> | <span data-ttu-id="9811a-213">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-213">String</span></span> | <span data-ttu-id="9811a-214">Een twee drie</span><span class="sxs-lookup"><span data-stu-id="9811a-214">one, two, three</span></span> |
| <span data-ttu-id="9811a-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-215">toJsonOutput</span></span> | <span data-ttu-id="9811a-216">Object</span><span class="sxs-lookup"><span data-stu-id="9811a-216">Object</span></span> | <span data-ttu-id="9811a-217">{"een": "a", "twee": "b"}</span><span class="sxs-lookup"><span data-stu-id="9811a-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="9811a-218">concat</span><span class="sxs-lookup"><span data-stu-id="9811a-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="9811a-219">Combineert meerdere tekenreekswaarden en retourneert Hallo samengevoegd tekenreeks, of combineert meerdere matrices en retourneert Hallo samengevoegd matrix.</span><span class="sxs-lookup"><span data-stu-id="9811a-219">Combines multiple string values and returns hello concatenated string, or combines multiple arrays and returns hello concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-220">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-220">Parameters</span></span>

| <span data-ttu-id="9811a-221">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-221">Parameter</span></span> | <span data-ttu-id="9811a-222">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-222">Required</span></span> | <span data-ttu-id="9811a-223">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-223">Type</span></span> | <span data-ttu-id="9811a-224">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-225">Arg1</span><span class="sxs-lookup"><span data-stu-id="9811a-225">arg1</span></span> |<span data-ttu-id="9811a-226">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-226">Yes</span></span> |<span data-ttu-id="9811a-227">tekenreeks of matrix</span><span class="sxs-lookup"><span data-stu-id="9811a-227">string or array</span></span> |<span data-ttu-id="9811a-228">Hallo eerste waarde voor de samenvoeging.</span><span class="sxs-lookup"><span data-stu-id="9811a-228">hello first value for concatenation.</span></span> |
| <span data-ttu-id="9811a-229">Extra argumenten</span><span class="sxs-lookup"><span data-stu-id="9811a-229">additional arguments</span></span> |<span data-ttu-id="9811a-230">Nee</span><span class="sxs-lookup"><span data-stu-id="9811a-230">No</span></span> |<span data-ttu-id="9811a-231">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-231">string</span></span> |<span data-ttu-id="9811a-232">Aanvullende waarden in opeenvolgende volgorde voor de samenvoeging.</span><span class="sxs-lookup"><span data-stu-id="9811a-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-233">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-233">Return value</span></span>
<span data-ttu-id="9811a-234">Een tekenreeks of matrix met samengevoegde waarden.</span><span class="sxs-lookup"><span data-stu-id="9811a-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-235">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-235">Examples</span></span>

<span data-ttu-id="9811a-236">Hallo volgende voorbeeld ziet u hoe toocombine twee tekenreekswaarden en een samengevoegde tekenreeks retourneren.</span><span class="sxs-lookup"><span data-stu-id="9811a-236">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="9811a-237">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-237">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-238">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-238">Name</span></span> | <span data-ttu-id="9811a-239">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-239">Type</span></span> | <span data-ttu-id="9811a-240">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-241">concatOutput</span></span> | <span data-ttu-id="9811a-242">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-242">String</span></span> | <span data-ttu-id="9811a-243">voorvoegsel 5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="9811a-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="9811a-244">Hallo volgende voorbeeld ziet u hoe toocombine twee matrices.</span><span class="sxs-lookup"><span data-stu-id="9811a-244">hello following example shows how toocombine two arrays.</span></span>

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

<span data-ttu-id="9811a-245">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-246">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-246">Name</span></span> | <span data-ttu-id="9811a-247">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-247">Type</span></span> | <span data-ttu-id="9811a-248">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-249">retourneren</span><span class="sxs-lookup"><span data-stu-id="9811a-249">return</span></span> | <span data-ttu-id="9811a-250">Matrix</span><span class="sxs-lookup"><span data-stu-id="9811a-250">Array</span></span> | <span data-ttu-id="9811a-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="9811a-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="9811a-252">Bevat</span><span class="sxs-lookup"><span data-stu-id="9811a-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="9811a-253">Controleert of een matrix een waarde bevat, een object een sleutel bevat of een tekenreeks een subtekenreeks bevat.</span><span class="sxs-lookup"><span data-stu-id="9811a-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-254">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-254">Parameters</span></span>

| <span data-ttu-id="9811a-255">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-255">Parameter</span></span> | <span data-ttu-id="9811a-256">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-256">Required</span></span> | <span data-ttu-id="9811a-257">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-257">Type</span></span> | <span data-ttu-id="9811a-258">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-259">container</span><span class="sxs-lookup"><span data-stu-id="9811a-259">container</span></span> |<span data-ttu-id="9811a-260">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-260">Yes</span></span> |<span data-ttu-id="9811a-261">Array, object of een tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-261">array, object, or string</span></span> |<span data-ttu-id="9811a-262">Hallo-waarde die Hallo waarde toofind bevat.</span><span class="sxs-lookup"><span data-stu-id="9811a-262">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="9811a-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="9811a-263">itemToFind</span></span> |<span data-ttu-id="9811a-264">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-264">Yes</span></span> |<span data-ttu-id="9811a-265">String of int.</span><span class="sxs-lookup"><span data-stu-id="9811a-265">string or int</span></span> |<span data-ttu-id="9811a-266">Hallo waarde toofind.</span><span class="sxs-lookup"><span data-stu-id="9811a-266">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-267">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-267">Return value</span></span>

<span data-ttu-id="9811a-268">**De waarde True** als Hallo item gevonden, anders wordt is **False**.</span><span class="sxs-lookup"><span data-stu-id="9811a-268">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-269">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-269">Examples</span></span>

<span data-ttu-id="9811a-270">Hallo volgende voorbeeld laat zien hoe toouse bevat met verschillende typen:</span><span class="sxs-lookup"><span data-stu-id="9811a-270">hello following example shows how toouse contains with different types:</span></span>

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

<span data-ttu-id="9811a-271">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-271">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-272">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-272">Name</span></span> | <span data-ttu-id="9811a-273">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-273">Type</span></span> | <span data-ttu-id="9811a-274">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="9811a-275">stringTrue</span></span> | <span data-ttu-id="9811a-276">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-276">Bool</span></span> | <span data-ttu-id="9811a-277">True</span><span class="sxs-lookup"><span data-stu-id="9811a-277">True</span></span> |
| <span data-ttu-id="9811a-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="9811a-278">stringFalse</span></span> | <span data-ttu-id="9811a-279">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-279">Bool</span></span> | <span data-ttu-id="9811a-280">False</span><span class="sxs-lookup"><span data-stu-id="9811a-280">False</span></span> |
| <span data-ttu-id="9811a-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="9811a-281">objectTrue</span></span> | <span data-ttu-id="9811a-282">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-282">Bool</span></span> | <span data-ttu-id="9811a-283">True</span><span class="sxs-lookup"><span data-stu-id="9811a-283">True</span></span> |
| <span data-ttu-id="9811a-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="9811a-284">objectFalse</span></span> | <span data-ttu-id="9811a-285">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-285">Bool</span></span> | <span data-ttu-id="9811a-286">False</span><span class="sxs-lookup"><span data-stu-id="9811a-286">False</span></span> |
| <span data-ttu-id="9811a-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="9811a-287">arrayTrue</span></span> | <span data-ttu-id="9811a-288">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-288">Bool</span></span> | <span data-ttu-id="9811a-289">True</span><span class="sxs-lookup"><span data-stu-id="9811a-289">True</span></span> |
| <span data-ttu-id="9811a-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="9811a-290">arrayFalse</span></span> | <span data-ttu-id="9811a-291">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-291">Bool</span></span> | <span data-ttu-id="9811a-292">False</span><span class="sxs-lookup"><span data-stu-id="9811a-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="9811a-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="9811a-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="9811a-294">Converteert een waarde tooa gegevens URI.</span><span class="sxs-lookup"><span data-stu-id="9811a-294">Converts a value tooa data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-295">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-295">Parameters</span></span>

| <span data-ttu-id="9811a-296">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-296">Parameter</span></span> | <span data-ttu-id="9811a-297">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-297">Required</span></span> | <span data-ttu-id="9811a-298">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-298">Type</span></span> | <span data-ttu-id="9811a-299">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="9811a-300">stringToConvert</span></span> |<span data-ttu-id="9811a-301">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-301">Yes</span></span> |<span data-ttu-id="9811a-302">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-302">string</span></span> |<span data-ttu-id="9811a-303">Hallo tooconvert tooa Waardegegevens URI.</span><span class="sxs-lookup"><span data-stu-id="9811a-303">hello value tooconvert tooa data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-304">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-304">Return value</span></span>

<span data-ttu-id="9811a-305">Een tekenreeks zijn opgemaakt als een gegevens-URI.</span><span class="sxs-lookup"><span data-stu-id="9811a-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-306">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-306">Examples</span></span>

<span data-ttu-id="9811a-307">Hallo voorbeeld te volgen tooa gegevenswaarde URI converteert en zet een gegevens-URI tooa tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="9811a-307">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

<span data-ttu-id="9811a-308">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-308">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-309">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-309">Name</span></span> | <span data-ttu-id="9811a-310">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-310">Type</span></span> | <span data-ttu-id="9811a-311">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-312">dataUriOutput</span></span> | <span data-ttu-id="9811a-313">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-313">String</span></span> | <span data-ttu-id="9811a-314">gegevens: tekst / onbewerkte; charset = utf8; base64, SGVsbG8 =</span><span class="sxs-lookup"><span data-stu-id="9811a-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="9811a-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-315">toStringOutput</span></span> | <span data-ttu-id="9811a-316">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-316">String</span></span> | <span data-ttu-id="9811a-317">Hallo mensen!</span><span class="sxs-lookup"><span data-stu-id="9811a-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="9811a-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="9811a-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="9811a-319">Een gegevens-URI converteert geformatteerd tooa tekenreekswaarde.</span><span class="sxs-lookup"><span data-stu-id="9811a-319">Converts a data URI formatted value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-320">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-320">Parameters</span></span>

| <span data-ttu-id="9811a-321">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-321">Parameter</span></span> | <span data-ttu-id="9811a-322">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-322">Required</span></span> | <span data-ttu-id="9811a-323">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-323">Type</span></span> | <span data-ttu-id="9811a-324">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="9811a-325">dataUriToConvert</span></span> |<span data-ttu-id="9811a-326">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-326">Yes</span></span> |<span data-ttu-id="9811a-327">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-327">string</span></span> |<span data-ttu-id="9811a-328">Hallo gegevenswaarde URI tooconvert.</span><span class="sxs-lookup"><span data-stu-id="9811a-328">hello data URI value tooconvert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-329">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-329">Return value</span></span>

<span data-ttu-id="9811a-330">Een tekenreeks met Hallo geconverteerd waarde.</span><span class="sxs-lookup"><span data-stu-id="9811a-330">A string containing hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-331">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-331">Examples</span></span>

<span data-ttu-id="9811a-332">Hallo voorbeeld te volgen tooa gegevenswaarde URI converteert en zet een gegevens-URI tooa tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="9811a-332">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

<span data-ttu-id="9811a-333">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-333">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-334">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-334">Name</span></span> | <span data-ttu-id="9811a-335">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-335">Type</span></span> | <span data-ttu-id="9811a-336">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-337">dataUriOutput</span></span> | <span data-ttu-id="9811a-338">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-338">String</span></span> | <span data-ttu-id="9811a-339">gegevens: tekst / onbewerkte; charset = utf8; base64, SGVsbG8 =</span><span class="sxs-lookup"><span data-stu-id="9811a-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="9811a-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-340">toStringOutput</span></span> | <span data-ttu-id="9811a-341">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-341">String</span></span> | <span data-ttu-id="9811a-342">Hallo mensen!</span><span class="sxs-lookup"><span data-stu-id="9811a-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="9811a-343">leeg</span><span class="sxs-lookup"><span data-stu-id="9811a-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="9811a-344">Hiermee wordt bepaald of een matrix, een object of een tekenreeks leeg is.</span><span class="sxs-lookup"><span data-stu-id="9811a-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-345">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-345">Parameters</span></span>

| <span data-ttu-id="9811a-346">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-346">Parameter</span></span> | <span data-ttu-id="9811a-347">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-347">Required</span></span> | <span data-ttu-id="9811a-348">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-348">Type</span></span> | <span data-ttu-id="9811a-349">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="9811a-350">itemToTest</span></span> |<span data-ttu-id="9811a-351">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-351">Yes</span></span> |<span data-ttu-id="9811a-352">Array, object of een tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-352">array, object, or string</span></span> |<span data-ttu-id="9811a-353">Hallo waarde toocheck als deze leeg is.</span><span class="sxs-lookup"><span data-stu-id="9811a-353">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-354">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-354">Return value</span></span>

<span data-ttu-id="9811a-355">Retourneert **True** als Hallo-waarde leeg, anders wordt is **False**.</span><span class="sxs-lookup"><span data-stu-id="9811a-355">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-356">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-356">Examples</span></span>

<span data-ttu-id="9811a-357">Hallo volgende voorbeeld wordt gecontroleerd of een matrix, het object en de tekenreeks leeg zijn.</span><span class="sxs-lookup"><span data-stu-id="9811a-357">hello following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="9811a-358">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-358">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-359">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-359">Name</span></span> | <span data-ttu-id="9811a-360">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-360">Type</span></span> | <span data-ttu-id="9811a-361">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="9811a-362">arrayEmpty</span></span> | <span data-ttu-id="9811a-363">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-363">Bool</span></span> | <span data-ttu-id="9811a-364">True</span><span class="sxs-lookup"><span data-stu-id="9811a-364">True</span></span> |
| <span data-ttu-id="9811a-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="9811a-365">objectEmpty</span></span> | <span data-ttu-id="9811a-366">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-366">Bool</span></span> | <span data-ttu-id="9811a-367">True</span><span class="sxs-lookup"><span data-stu-id="9811a-367">True</span></span> |
| <span data-ttu-id="9811a-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="9811a-368">stringEmpty</span></span> | <span data-ttu-id="9811a-369">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-369">Bool</span></span> | <span data-ttu-id="9811a-370">True</span><span class="sxs-lookup"><span data-stu-id="9811a-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="9811a-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="9811a-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="9811a-372">Hiermee wordt bepaald of een tekenreeks met een waarde eindigt.</span><span class="sxs-lookup"><span data-stu-id="9811a-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="9811a-373">Hallo vergelijking is niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="9811a-373">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-374">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-374">Parameters</span></span>

| <span data-ttu-id="9811a-375">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-375">Parameter</span></span> | <span data-ttu-id="9811a-376">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-376">Required</span></span> | <span data-ttu-id="9811a-377">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-377">Type</span></span> | <span data-ttu-id="9811a-378">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="9811a-379">stringToSearch</span></span> |<span data-ttu-id="9811a-380">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-380">Yes</span></span> |<span data-ttu-id="9811a-381">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-381">string</span></span> |<span data-ttu-id="9811a-382">Hallo-waarde die Hallo item toofind bevat.</span><span class="sxs-lookup"><span data-stu-id="9811a-382">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="9811a-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="9811a-383">stringToFind</span></span> |<span data-ttu-id="9811a-384">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-384">Yes</span></span> |<span data-ttu-id="9811a-385">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-385">string</span></span> |<span data-ttu-id="9811a-386">Hallo waarde toofind.</span><span class="sxs-lookup"><span data-stu-id="9811a-386">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-387">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-387">Return value</span></span>

<span data-ttu-id="9811a-388">**De waarde True** als laatste teken Hallo of van Hallo tekenreeks overeenkomt met de waarde van de Hallo; anders **False**.</span><span class="sxs-lookup"><span data-stu-id="9811a-388">**True** if hello last character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-389">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-389">Examples</span></span>

<span data-ttu-id="9811a-390">Hallo volgende voorbeeld ziet u hoe toouse Hallo startsWith en endsWith-functies:</span><span class="sxs-lookup"><span data-stu-id="9811a-390">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="9811a-391">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-391">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-392">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-392">Name</span></span> | <span data-ttu-id="9811a-393">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-393">Type</span></span> | <span data-ttu-id="9811a-394">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="9811a-395">startsTrue</span></span> | <span data-ttu-id="9811a-396">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-396">Bool</span></span> | <span data-ttu-id="9811a-397">True</span><span class="sxs-lookup"><span data-stu-id="9811a-397">True</span></span> |
| <span data-ttu-id="9811a-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="9811a-398">startsCapTrue</span></span> | <span data-ttu-id="9811a-399">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-399">Bool</span></span> | <span data-ttu-id="9811a-400">True</span><span class="sxs-lookup"><span data-stu-id="9811a-400">True</span></span> |
| <span data-ttu-id="9811a-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="9811a-401">startsFalse</span></span> | <span data-ttu-id="9811a-402">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-402">Bool</span></span> | <span data-ttu-id="9811a-403">False</span><span class="sxs-lookup"><span data-stu-id="9811a-403">False</span></span> |
| <span data-ttu-id="9811a-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="9811a-404">endsTrue</span></span> | <span data-ttu-id="9811a-405">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-405">Bool</span></span> | <span data-ttu-id="9811a-406">True</span><span class="sxs-lookup"><span data-stu-id="9811a-406">True</span></span> |
| <span data-ttu-id="9811a-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="9811a-407">endsCapTrue</span></span> | <span data-ttu-id="9811a-408">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-408">Bool</span></span> | <span data-ttu-id="9811a-409">True</span><span class="sxs-lookup"><span data-stu-id="9811a-409">True</span></span> |
| <span data-ttu-id="9811a-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="9811a-410">endsFalse</span></span> | <span data-ttu-id="9811a-411">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-411">Bool</span></span> | <span data-ttu-id="9811a-412">False</span><span class="sxs-lookup"><span data-stu-id="9811a-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="9811a-413">eerste</span><span class="sxs-lookup"><span data-stu-id="9811a-413">first</span></span>
`first(arg1)`

<span data-ttu-id="9811a-414">Retourneert Hallo eerste teken van Hallo tekenreeks of het eerste element van de matrix Hallo.</span><span class="sxs-lookup"><span data-stu-id="9811a-414">Returns hello first character of hello string, or first element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-415">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-415">Parameters</span></span>

| <span data-ttu-id="9811a-416">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-416">Parameter</span></span> | <span data-ttu-id="9811a-417">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-417">Required</span></span> | <span data-ttu-id="9811a-418">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-418">Type</span></span> | <span data-ttu-id="9811a-419">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-420">Arg1</span><span class="sxs-lookup"><span data-stu-id="9811a-420">arg1</span></span> |<span data-ttu-id="9811a-421">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-421">Yes</span></span> |<span data-ttu-id="9811a-422">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-422">array or string</span></span> |<span data-ttu-id="9811a-423">Hallo waarde tooretrieve Hallo eerste element of teken.</span><span class="sxs-lookup"><span data-stu-id="9811a-423">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-424">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-424">Return value</span></span>

<span data-ttu-id="9811a-425">Een tekenreeks van het eerste teken Hallo of Hallo type (string, int, matrix of object) Hallo eerste element in een matrix.</span><span class="sxs-lookup"><span data-stu-id="9811a-425">A string of hello first character, or hello type (string, int, array, or object) of hello first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-426">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-426">Examples</span></span>

<span data-ttu-id="9811a-427">Hallo volgende voorbeeld ziet u hoe toouse Hallo eerste functie met een matrix en de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-427">hello following example shows how toouse hello first function with an array and string.</span></span>

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

<span data-ttu-id="9811a-428">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-429">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-429">Name</span></span> | <span data-ttu-id="9811a-430">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-430">Type</span></span> | <span data-ttu-id="9811a-431">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-432">arrayOutput</span></span> | <span data-ttu-id="9811a-433">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-433">String</span></span> | <span data-ttu-id="9811a-434">een</span><span class="sxs-lookup"><span data-stu-id="9811a-434">one</span></span> |
| <span data-ttu-id="9811a-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-435">stringOutput</span></span> | <span data-ttu-id="9811a-436">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-436">String</span></span> | <span data-ttu-id="9811a-437">O</span><span class="sxs-lookup"><span data-stu-id="9811a-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="9811a-438">indexOf</span><span class="sxs-lookup"><span data-stu-id="9811a-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="9811a-439">Retourneert Hallo eerste positie van een waarde in een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-439">Returns hello first position of a value within a string.</span></span> <span data-ttu-id="9811a-440">Hallo vergelijking is niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="9811a-440">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-441">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-441">Parameters</span></span>

| <span data-ttu-id="9811a-442">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-442">Parameter</span></span> | <span data-ttu-id="9811a-443">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-443">Required</span></span> | <span data-ttu-id="9811a-444">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-444">Type</span></span> | <span data-ttu-id="9811a-445">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="9811a-446">stringToSearch</span></span> |<span data-ttu-id="9811a-447">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-447">Yes</span></span> |<span data-ttu-id="9811a-448">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-448">string</span></span> |<span data-ttu-id="9811a-449">Hallo-waarde die Hallo item toofind bevat.</span><span class="sxs-lookup"><span data-stu-id="9811a-449">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="9811a-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="9811a-450">stringToFind</span></span> |<span data-ttu-id="9811a-451">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-451">Yes</span></span> |<span data-ttu-id="9811a-452">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-452">string</span></span> |<span data-ttu-id="9811a-453">Hallo waarde toofind.</span><span class="sxs-lookup"><span data-stu-id="9811a-453">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-454">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-454">Return value</span></span>

<span data-ttu-id="9811a-455">Een geheel getal dat de positie Hallo van Hallo item toofind weergeeft.</span><span class="sxs-lookup"><span data-stu-id="9811a-455">An integer that represents hello position of hello item toofind.</span></span> <span data-ttu-id="9811a-456">Hallo-waarde is gebaseerd op nul.</span><span class="sxs-lookup"><span data-stu-id="9811a-456">hello value is zero-based.</span></span> <span data-ttu-id="9811a-457">Als het Hallo-item niet is gevonden, wordt -1 geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9811a-457">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-458">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-458">Examples</span></span>

<span data-ttu-id="9811a-459">Hallo volgende voorbeeld ziet u hoe toouse Hallo indexOf en lastIndexOf functies:</span><span class="sxs-lookup"><span data-stu-id="9811a-459">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

<span data-ttu-id="9811a-460">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-460">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-461">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-461">Name</span></span> | <span data-ttu-id="9811a-462">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-462">Type</span></span> | <span data-ttu-id="9811a-463">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-464">firstT</span><span class="sxs-lookup"><span data-stu-id="9811a-464">firstT</span></span> | <span data-ttu-id="9811a-465">int</span><span class="sxs-lookup"><span data-stu-id="9811a-465">Int</span></span> | <span data-ttu-id="9811a-466">0</span><span class="sxs-lookup"><span data-stu-id="9811a-466">0</span></span> |
| <span data-ttu-id="9811a-467">lastT</span><span class="sxs-lookup"><span data-stu-id="9811a-467">lastT</span></span> | <span data-ttu-id="9811a-468">int</span><span class="sxs-lookup"><span data-stu-id="9811a-468">Int</span></span> | <span data-ttu-id="9811a-469">3</span><span class="sxs-lookup"><span data-stu-id="9811a-469">3</span></span> |
| <span data-ttu-id="9811a-470">firstString</span><span class="sxs-lookup"><span data-stu-id="9811a-470">firstString</span></span> | <span data-ttu-id="9811a-471">int</span><span class="sxs-lookup"><span data-stu-id="9811a-471">Int</span></span> | <span data-ttu-id="9811a-472">2</span><span class="sxs-lookup"><span data-stu-id="9811a-472">2</span></span> |
| <span data-ttu-id="9811a-473">lastString</span><span class="sxs-lookup"><span data-stu-id="9811a-473">lastString</span></span> | <span data-ttu-id="9811a-474">int</span><span class="sxs-lookup"><span data-stu-id="9811a-474">Int</span></span> | <span data-ttu-id="9811a-475">0</span><span class="sxs-lookup"><span data-stu-id="9811a-475">0</span></span> |
| <span data-ttu-id="9811a-476">notFound</span><span class="sxs-lookup"><span data-stu-id="9811a-476">notFound</span></span> | <span data-ttu-id="9811a-477">int</span><span class="sxs-lookup"><span data-stu-id="9811a-477">Int</span></span> | <span data-ttu-id="9811a-478">-1</span><span class="sxs-lookup"><span data-stu-id="9811a-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="9811a-479">laatste</span><span class="sxs-lookup"><span data-stu-id="9811a-479">last</span></span>
`last (arg1)`

<span data-ttu-id="9811a-480">Retourneert de laatste teken van Hallo tekenreeks of Hallo laatste element van Hallo matrix.</span><span class="sxs-lookup"><span data-stu-id="9811a-480">Returns last character of hello string, or hello last element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-481">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-481">Parameters</span></span>

| <span data-ttu-id="9811a-482">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-482">Parameter</span></span> | <span data-ttu-id="9811a-483">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-483">Required</span></span> | <span data-ttu-id="9811a-484">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-484">Type</span></span> | <span data-ttu-id="9811a-485">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-486">Arg1</span><span class="sxs-lookup"><span data-stu-id="9811a-486">arg1</span></span> |<span data-ttu-id="9811a-487">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-487">Yes</span></span> |<span data-ttu-id="9811a-488">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-488">array or string</span></span> |<span data-ttu-id="9811a-489">Hallo waarde tooretrieve Hallo laatste element of teken.</span><span class="sxs-lookup"><span data-stu-id="9811a-489">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-490">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-490">Return value</span></span>

<span data-ttu-id="9811a-491">Een tekenreeks van het Hallo-type (string, int, matrix of object) van het laatste element in een matrix Hallo of Hallo laatste teken.</span><span class="sxs-lookup"><span data-stu-id="9811a-491">A string of hello last character, or hello type (string, int, array, or object) of hello last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-492">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-492">Examples</span></span>

<span data-ttu-id="9811a-493">Hallo volgende voorbeeld ziet u hoe toouse Hallo laatste functie met een matrix en de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-493">hello following example shows how toouse hello last function with an array and string.</span></span>

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

<span data-ttu-id="9811a-494">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-494">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-495">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-495">Name</span></span> | <span data-ttu-id="9811a-496">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-496">Type</span></span> | <span data-ttu-id="9811a-497">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-498">arrayOutput</span></span> | <span data-ttu-id="9811a-499">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-499">String</span></span> | <span data-ttu-id="9811a-500">drie</span><span class="sxs-lookup"><span data-stu-id="9811a-500">three</span></span> |
| <span data-ttu-id="9811a-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-501">stringOutput</span></span> | <span data-ttu-id="9811a-502">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-502">String</span></span> | <span data-ttu-id="9811a-503">E</span><span class="sxs-lookup"><span data-stu-id="9811a-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="9811a-504">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="9811a-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="9811a-505">Retourneert Hallo laatste positie van een waarde in een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-505">Returns hello last position of a value within a string.</span></span> <span data-ttu-id="9811a-506">Hallo vergelijking is niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="9811a-506">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-507">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-507">Parameters</span></span>

| <span data-ttu-id="9811a-508">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-508">Parameter</span></span> | <span data-ttu-id="9811a-509">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-509">Required</span></span> | <span data-ttu-id="9811a-510">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-510">Type</span></span> | <span data-ttu-id="9811a-511">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="9811a-512">stringToSearch</span></span> |<span data-ttu-id="9811a-513">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-513">Yes</span></span> |<span data-ttu-id="9811a-514">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-514">string</span></span> |<span data-ttu-id="9811a-515">Hallo-waarde die Hallo item toofind bevat.</span><span class="sxs-lookup"><span data-stu-id="9811a-515">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="9811a-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="9811a-516">stringToFind</span></span> |<span data-ttu-id="9811a-517">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-517">Yes</span></span> |<span data-ttu-id="9811a-518">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-518">string</span></span> |<span data-ttu-id="9811a-519">Hallo waarde toofind.</span><span class="sxs-lookup"><span data-stu-id="9811a-519">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-520">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-520">Return value</span></span>

<span data-ttu-id="9811a-521">Een geheel getal dat de laatste positie Hallo van Hallo item toofind vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="9811a-521">An integer that represents hello last position of hello item toofind.</span></span> <span data-ttu-id="9811a-522">Hallo-waarde is gebaseerd op nul.</span><span class="sxs-lookup"><span data-stu-id="9811a-522">hello value is zero-based.</span></span> <span data-ttu-id="9811a-523">Als het Hallo-item niet is gevonden, wordt -1 geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9811a-523">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-524">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-524">Examples</span></span>

<span data-ttu-id="9811a-525">Hallo volgende voorbeeld ziet u hoe toouse Hallo indexOf en lastIndexOf functies:</span><span class="sxs-lookup"><span data-stu-id="9811a-525">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

<span data-ttu-id="9811a-526">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-526">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-527">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-527">Name</span></span> | <span data-ttu-id="9811a-528">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-528">Type</span></span> | <span data-ttu-id="9811a-529">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-530">firstT</span><span class="sxs-lookup"><span data-stu-id="9811a-530">firstT</span></span> | <span data-ttu-id="9811a-531">int</span><span class="sxs-lookup"><span data-stu-id="9811a-531">Int</span></span> | <span data-ttu-id="9811a-532">0</span><span class="sxs-lookup"><span data-stu-id="9811a-532">0</span></span> |
| <span data-ttu-id="9811a-533">lastT</span><span class="sxs-lookup"><span data-stu-id="9811a-533">lastT</span></span> | <span data-ttu-id="9811a-534">int</span><span class="sxs-lookup"><span data-stu-id="9811a-534">Int</span></span> | <span data-ttu-id="9811a-535">3</span><span class="sxs-lookup"><span data-stu-id="9811a-535">3</span></span> |
| <span data-ttu-id="9811a-536">firstString</span><span class="sxs-lookup"><span data-stu-id="9811a-536">firstString</span></span> | <span data-ttu-id="9811a-537">int</span><span class="sxs-lookup"><span data-stu-id="9811a-537">Int</span></span> | <span data-ttu-id="9811a-538">2</span><span class="sxs-lookup"><span data-stu-id="9811a-538">2</span></span> |
| <span data-ttu-id="9811a-539">lastString</span><span class="sxs-lookup"><span data-stu-id="9811a-539">lastString</span></span> | <span data-ttu-id="9811a-540">int</span><span class="sxs-lookup"><span data-stu-id="9811a-540">Int</span></span> | <span data-ttu-id="9811a-541">0</span><span class="sxs-lookup"><span data-stu-id="9811a-541">0</span></span> |
| <span data-ttu-id="9811a-542">notFound</span><span class="sxs-lookup"><span data-stu-id="9811a-542">notFound</span></span> | <span data-ttu-id="9811a-543">int</span><span class="sxs-lookup"><span data-stu-id="9811a-543">Int</span></span> | <span data-ttu-id="9811a-544">-1</span><span class="sxs-lookup"><span data-stu-id="9811a-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="9811a-545">lengte</span><span class="sxs-lookup"><span data-stu-id="9811a-545">length</span></span>
`length(string)`

<span data-ttu-id="9811a-546">Retourneert het aantal tekens Hallo in een tekenreeks of elementen in een matrix.</span><span class="sxs-lookup"><span data-stu-id="9811a-546">Returns hello number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-547">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-547">Parameters</span></span>

| <span data-ttu-id="9811a-548">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-548">Parameter</span></span> | <span data-ttu-id="9811a-549">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-549">Required</span></span> | <span data-ttu-id="9811a-550">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-550">Type</span></span> | <span data-ttu-id="9811a-551">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-552">Arg1</span><span class="sxs-lookup"><span data-stu-id="9811a-552">arg1</span></span> |<span data-ttu-id="9811a-553">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-553">Yes</span></span> |<span data-ttu-id="9811a-554">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-554">array or string</span></span> |<span data-ttu-id="9811a-555">Hallo toouse voor het ophalen van het aantal elementen Hallo matrix of tekenreeks toouse voor het ophalen van het aantal tekens Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="9811a-555">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-556">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-556">Return value</span></span>

<span data-ttu-id="9811a-557">Een int.</span><span class="sxs-lookup"><span data-stu-id="9811a-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="9811a-558">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-558">Examples</span></span>

<span data-ttu-id="9811a-559">Hallo volgende voorbeeld wordt getoond hoe toouse lengte met een matrix en de tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="9811a-559">hello following example shows how toouse length with an array and string:</span></span>

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

<span data-ttu-id="9811a-560">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-560">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-561">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-561">Name</span></span> | <span data-ttu-id="9811a-562">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-562">Type</span></span> | <span data-ttu-id="9811a-563">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="9811a-564">arrayLength</span></span> | <span data-ttu-id="9811a-565">int</span><span class="sxs-lookup"><span data-stu-id="9811a-565">Int</span></span> | <span data-ttu-id="9811a-566">3</span><span class="sxs-lookup"><span data-stu-id="9811a-566">3</span></span> |
| <span data-ttu-id="9811a-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="9811a-567">stringLength</span></span> | <span data-ttu-id="9811a-568">int</span><span class="sxs-lookup"><span data-stu-id="9811a-568">Int</span></span> | <span data-ttu-id="9811a-569">13</span><span class="sxs-lookup"><span data-stu-id="9811a-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="9811a-570">PadLeft</span><span class="sxs-lookup"><span data-stu-id="9811a-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="9811a-571">Retourneert een rechts uitgelijnde tekenreeks door toe te voegen tekens toohello links tot het bereiken van Hallo totale opgegeven lengte.</span><span class="sxs-lookup"><span data-stu-id="9811a-571">Returns a right-aligned string by adding characters toohello left until reaching hello total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-572">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-572">Parameters</span></span>

| <span data-ttu-id="9811a-573">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-573">Parameter</span></span> | <span data-ttu-id="9811a-574">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-574">Required</span></span> | <span data-ttu-id="9811a-575">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-575">Type</span></span> | <span data-ttu-id="9811a-576">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-577">valueToPad</span><span class="sxs-lookup"><span data-stu-id="9811a-577">valueToPad</span></span> |<span data-ttu-id="9811a-578">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-578">Yes</span></span> |<span data-ttu-id="9811a-579">String of int.</span><span class="sxs-lookup"><span data-stu-id="9811a-579">string or int</span></span> |<span data-ttu-id="9811a-580">waarde tooright Hallo-uitlijnen.</span><span class="sxs-lookup"><span data-stu-id="9811a-580">hello value tooright-align.</span></span> |
| <span data-ttu-id="9811a-581">totalLength</span><span class="sxs-lookup"><span data-stu-id="9811a-581">totalLength</span></span> |<span data-ttu-id="9811a-582">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-582">Yes</span></span> |<span data-ttu-id="9811a-583">int</span><span class="sxs-lookup"><span data-stu-id="9811a-583">int</span></span> |<span data-ttu-id="9811a-584">Totaal aantal tekens in Hallo Hallo tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9811a-584">hello total number of characters in hello returned string.</span></span> |
| <span data-ttu-id="9811a-585">paddingCharacter</span><span class="sxs-lookup"><span data-stu-id="9811a-585">paddingCharacter</span></span> |<span data-ttu-id="9811a-586">Nee</span><span class="sxs-lookup"><span data-stu-id="9811a-586">No</span></span> |<span data-ttu-id="9811a-587">willekeurig teken</span><span class="sxs-lookup"><span data-stu-id="9811a-587">single character</span></span> |<span data-ttu-id="9811a-588">Hallo teken toouse voor links-opvulling tot de totale lengte van Hallo is bereikt.</span><span class="sxs-lookup"><span data-stu-id="9811a-588">hello character toouse for left-padding until hello total length is reached.</span></span> <span data-ttu-id="9811a-589">Hallo-standaardwaarde is een spatie.</span><span class="sxs-lookup"><span data-stu-id="9811a-589">hello default value is a space.</span></span> |

<span data-ttu-id="9811a-590">Als de oorspronkelijke reeks Hallo langer dan het aantal tekens toopad hello is, worden geen tekens toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="9811a-590">If hello original string is longer than hello number of characters toopad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="9811a-591">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-591">Return value</span></span>

<span data-ttu-id="9811a-592">Een tekenreeks met Hallo minimaal aantal tekens opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9811a-592">A string with at least hello number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-593">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-593">Examples</span></span>

<span data-ttu-id="9811a-594">Hallo volgende voorbeeld ziet u hoe toopad Hallo waarde van de gebruiker opgegeven parameter door toe te voegen Hallo teken nul totdat het totaal aantal tekens Hallo bereikt.</span><span class="sxs-lookup"><span data-stu-id="9811a-594">hello following example shows how toopad hello user-provided parameter value by adding hello zero character until it reaches hello total number of characters.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123"
        }
    },
    "resources": [],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[padLeft(parameters('testString'),10,'0')]"
        }
    }
}
```

<span data-ttu-id="9811a-595">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-595">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-596">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-596">Name</span></span> | <span data-ttu-id="9811a-597">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-597">Type</span></span> | <span data-ttu-id="9811a-598">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-599">stringOutput</span></span> | <span data-ttu-id="9811a-600">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-600">String</span></span> | <span data-ttu-id="9811a-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="9811a-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="9811a-602">vervangen</span><span class="sxs-lookup"><span data-stu-id="9811a-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="9811a-603">Retourneert een nieuwe tekenreeks met alle exemplaren van de ene tekenreeks vervangen door een andere tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-604">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-604">Parameters</span></span>

| <span data-ttu-id="9811a-605">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-605">Parameter</span></span> | <span data-ttu-id="9811a-606">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-606">Required</span></span> | <span data-ttu-id="9811a-607">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-607">Type</span></span> | <span data-ttu-id="9811a-608">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-609">originalString</span><span class="sxs-lookup"><span data-stu-id="9811a-609">originalString</span></span> |<span data-ttu-id="9811a-610">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-610">Yes</span></span> |<span data-ttu-id="9811a-611">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-611">string</span></span> |<span data-ttu-id="9811a-612">Hallo-waarde met alle exemplaren van de ene tekenreeks vervangen door een andere tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-612">hello value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="9811a-613">oldString</span><span class="sxs-lookup"><span data-stu-id="9811a-613">oldString</span></span> |<span data-ttu-id="9811a-614">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-614">Yes</span></span> |<span data-ttu-id="9811a-615">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-615">string</span></span> |<span data-ttu-id="9811a-616">Hallo tekenreeks toobe verwijderd uit de oorspronkelijke reeks Hallo.</span><span class="sxs-lookup"><span data-stu-id="9811a-616">hello string toobe removed from hello original string.</span></span> |
| <span data-ttu-id="9811a-617">met de newString</span><span class="sxs-lookup"><span data-stu-id="9811a-617">newString</span></span> |<span data-ttu-id="9811a-618">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-618">Yes</span></span> |<span data-ttu-id="9811a-619">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-619">string</span></span> |<span data-ttu-id="9811a-620">Hallo tekenreeks tooadd in plaats van Hallo tekenreeks verwijderd.</span><span class="sxs-lookup"><span data-stu-id="9811a-620">hello string tooadd in place of hello removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-621">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-621">Return value</span></span>

<span data-ttu-id="9811a-622">Een tekenreeks met Hallo vervangen tekens.</span><span class="sxs-lookup"><span data-stu-id="9811a-622">A string with hello replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-623">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-623">Examples</span></span>

<span data-ttu-id="9811a-624">Hallo volgende voorbeeld ziet u hoe tooremove alle van de gebruiker opgegeven tekenreeks Hallo streepjes en hoe tooreplace deel uit van Hallo tekenreeks door een andere tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-624">hello following example shows how tooremove all dashes from hello user-provided string, and how tooreplace part of hello string with another string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123-123-1234"
        }
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'-', '')]"
        },
        "secodeOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'1234', 'xxxx')]"
        }
    }
}
```

<span data-ttu-id="9811a-625">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-625">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-626">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-626">Name</span></span> | <span data-ttu-id="9811a-627">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-627">Type</span></span> | <span data-ttu-id="9811a-628">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-629">firstOutput</span></span> | <span data-ttu-id="9811a-630">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-630">String</span></span> | <span data-ttu-id="9811a-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="9811a-631">1231231234</span></span> |
| <span data-ttu-id="9811a-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-632">secodeOutput</span></span> | <span data-ttu-id="9811a-633">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-633">String</span></span> | <span data-ttu-id="9811a-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="9811a-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="9811a-635">Overslaan</span><span class="sxs-lookup"><span data-stu-id="9811a-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="9811a-636">Retourneert een tekenreeks waarin alle tekens worden Hallo nadat Hallo aantal tekens of een matrix met alle Hallo elementen opgegeven nadat Hallo aantal elementen opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9811a-636">Returns a string with all hello characters after hello specified number of characters, or an array with all hello elements after hello specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-637">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-637">Parameters</span></span>

| <span data-ttu-id="9811a-638">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-638">Parameter</span></span> | <span data-ttu-id="9811a-639">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-639">Required</span></span> | <span data-ttu-id="9811a-640">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-640">Type</span></span> | <span data-ttu-id="9811a-641">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="9811a-642">originalValue</span></span> |<span data-ttu-id="9811a-643">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-643">Yes</span></span> |<span data-ttu-id="9811a-644">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-644">array or string</span></span> |<span data-ttu-id="9811a-645">Hallo toouse matrix of tekenreeks voor het overslaan.</span><span class="sxs-lookup"><span data-stu-id="9811a-645">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="9811a-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="9811a-646">numberToSkip</span></span> |<span data-ttu-id="9811a-647">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-647">Yes</span></span> |<span data-ttu-id="9811a-648">int</span><span class="sxs-lookup"><span data-stu-id="9811a-648">int</span></span> |<span data-ttu-id="9811a-649">Hallo aantal elementen of tekens tooskip.</span><span class="sxs-lookup"><span data-stu-id="9811a-649">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="9811a-650">Als deze waarde 0 of minder is, alle elementen Hallo of tekens in Hallo-waarde worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9811a-650">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="9811a-651">Als deze groter dan Hallo lengte van Hallo matrix of tekenreeks is, een lege matrix of tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9811a-651">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-652">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-652">Return value</span></span>

<span data-ttu-id="9811a-653">Een matrix of tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="9811a-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-654">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-654">Examples</span></span>

<span data-ttu-id="9811a-655">Hallo voorbeeld Slaat het Hallo na opgegeven aantal elementen in Hallo matrix en Hallo opgegeven aantal tekens in een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-655">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

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

<span data-ttu-id="9811a-656">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-656">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-657">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-657">Name</span></span> | <span data-ttu-id="9811a-658">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-658">Type</span></span> | <span data-ttu-id="9811a-659">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-660">arrayOutput</span></span> | <span data-ttu-id="9811a-661">Matrix</span><span class="sxs-lookup"><span data-stu-id="9811a-661">Array</span></span> | <span data-ttu-id="9811a-662">["drie"]</span><span class="sxs-lookup"><span data-stu-id="9811a-662">["three"]</span></span> |
| <span data-ttu-id="9811a-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-663">stringOutput</span></span> | <span data-ttu-id="9811a-664">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-664">String</span></span> | <span data-ttu-id="9811a-665">twee drie</span><span class="sxs-lookup"><span data-stu-id="9811a-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="9811a-666">split</span><span class="sxs-lookup"><span data-stu-id="9811a-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="9811a-667">Retourneert een matrix met tekenreeksen die Hallo subtekenreeksen Hallo bevat invoerreeks die worden gescheiden door Hallo opgegeven scheidingstekens.</span><span class="sxs-lookup"><span data-stu-id="9811a-667">Returns an array of strings that contains hello substrings of hello input string that are delimited by hello specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-668">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-668">Parameters</span></span>

| <span data-ttu-id="9811a-669">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-669">Parameter</span></span> | <span data-ttu-id="9811a-670">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-670">Required</span></span> | <span data-ttu-id="9811a-671">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-671">Type</span></span> | <span data-ttu-id="9811a-672">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-673">inputString</span><span class="sxs-lookup"><span data-stu-id="9811a-673">inputString</span></span> |<span data-ttu-id="9811a-674">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-674">Yes</span></span> |<span data-ttu-id="9811a-675">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-675">string</span></span> |<span data-ttu-id="9811a-676">Hallo tekenreeks toosplit.</span><span class="sxs-lookup"><span data-stu-id="9811a-676">hello string toosplit.</span></span> |
| <span data-ttu-id="9811a-677">Scheidingsteken</span><span class="sxs-lookup"><span data-stu-id="9811a-677">delimiter</span></span> |<span data-ttu-id="9811a-678">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-678">Yes</span></span> |<span data-ttu-id="9811a-679">tekenreeks of matrix met tekenreeksen</span><span class="sxs-lookup"><span data-stu-id="9811a-679">string or array of strings</span></span> |<span data-ttu-id="9811a-680">Hallo scheidingsteken toouse voor het splitsen van Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-680">hello delimiter toouse for splitting hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-681">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-681">Return value</span></span>

<span data-ttu-id="9811a-682">Een matrix met tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="9811a-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-683">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-683">Examples</span></span>

<span data-ttu-id="9811a-684">Hallo volgende voorbeeld wordt gesplitst invoerreeks Hallo met een komma en met een komma of puntkomma's.</span><span class="sxs-lookup"><span data-stu-id="9811a-684">hello following example splits hello input string with a comma, and with either a comma or a semi-colon.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstString": {
            "type": "string",
            "defaultValue": "one,two,three"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "one;two,three"
        }
    },
    "variables": {
        "delimiters": [ ",", ";" ]
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "array",
            "value": "[split(parameters('firstString'),',')]"
        },
        "secondOutput": {
            "type": "array",
            "value": "[split(parameters('secondString'),variables('delimiters'))]"
        }
    }
}
```

<span data-ttu-id="9811a-685">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-685">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-686">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-686">Name</span></span> | <span data-ttu-id="9811a-687">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-687">Type</span></span> | <span data-ttu-id="9811a-688">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-689">firstOutput</span></span> | <span data-ttu-id="9811a-690">Matrix</span><span class="sxs-lookup"><span data-stu-id="9811a-690">Array</span></span> | <span data-ttu-id="9811a-691">['een', 'twee', 'drie']</span><span class="sxs-lookup"><span data-stu-id="9811a-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="9811a-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-692">secondOutput</span></span> | <span data-ttu-id="9811a-693">Matrix</span><span class="sxs-lookup"><span data-stu-id="9811a-693">Array</span></span> | <span data-ttu-id="9811a-694">['een', 'twee', 'drie']</span><span class="sxs-lookup"><span data-stu-id="9811a-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="9811a-695">StartsWith</span><span class="sxs-lookup"><span data-stu-id="9811a-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="9811a-696">Hiermee wordt bepaald of een tekenreeks met een waarde begint.</span><span class="sxs-lookup"><span data-stu-id="9811a-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="9811a-697">Hallo vergelijking is niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="9811a-697">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-698">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-698">Parameters</span></span>

| <span data-ttu-id="9811a-699">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-699">Parameter</span></span> | <span data-ttu-id="9811a-700">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-700">Required</span></span> | <span data-ttu-id="9811a-701">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-701">Type</span></span> | <span data-ttu-id="9811a-702">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="9811a-703">stringToSearch</span></span> |<span data-ttu-id="9811a-704">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-704">Yes</span></span> |<span data-ttu-id="9811a-705">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-705">string</span></span> |<span data-ttu-id="9811a-706">Hallo-waarde die Hallo item toofind bevat.</span><span class="sxs-lookup"><span data-stu-id="9811a-706">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="9811a-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="9811a-707">stringToFind</span></span> |<span data-ttu-id="9811a-708">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-708">Yes</span></span> |<span data-ttu-id="9811a-709">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-709">string</span></span> |<span data-ttu-id="9811a-710">Hallo waarde toofind.</span><span class="sxs-lookup"><span data-stu-id="9811a-710">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-711">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-711">Return value</span></span>

<span data-ttu-id="9811a-712">**De waarde True** als eerste teken Hallo of van Hallo tekenreeks overeenkomt met de waarde van de Hallo; anders **False**.</span><span class="sxs-lookup"><span data-stu-id="9811a-712">**True** if hello first character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-713">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-713">Examples</span></span>

<span data-ttu-id="9811a-714">Hallo volgende voorbeeld ziet u hoe toouse Hallo startsWith en endsWith-functies:</span><span class="sxs-lookup"><span data-stu-id="9811a-714">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="9811a-715">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-715">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-716">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-716">Name</span></span> | <span data-ttu-id="9811a-717">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-717">Type</span></span> | <span data-ttu-id="9811a-718">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="9811a-719">startsTrue</span></span> | <span data-ttu-id="9811a-720">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-720">Bool</span></span> | <span data-ttu-id="9811a-721">True</span><span class="sxs-lookup"><span data-stu-id="9811a-721">True</span></span> |
| <span data-ttu-id="9811a-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="9811a-722">startsCapTrue</span></span> | <span data-ttu-id="9811a-723">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-723">Bool</span></span> | <span data-ttu-id="9811a-724">True</span><span class="sxs-lookup"><span data-stu-id="9811a-724">True</span></span> |
| <span data-ttu-id="9811a-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="9811a-725">startsFalse</span></span> | <span data-ttu-id="9811a-726">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-726">Bool</span></span> | <span data-ttu-id="9811a-727">False</span><span class="sxs-lookup"><span data-stu-id="9811a-727">False</span></span> |
| <span data-ttu-id="9811a-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="9811a-728">endsTrue</span></span> | <span data-ttu-id="9811a-729">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-729">Bool</span></span> | <span data-ttu-id="9811a-730">True</span><span class="sxs-lookup"><span data-stu-id="9811a-730">True</span></span> |
| <span data-ttu-id="9811a-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="9811a-731">endsCapTrue</span></span> | <span data-ttu-id="9811a-732">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-732">Bool</span></span> | <span data-ttu-id="9811a-733">True</span><span class="sxs-lookup"><span data-stu-id="9811a-733">True</span></span> |
| <span data-ttu-id="9811a-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="9811a-734">endsFalse</span></span> | <span data-ttu-id="9811a-735">BOOL</span><span class="sxs-lookup"><span data-stu-id="9811a-735">Bool</span></span> | <span data-ttu-id="9811a-736">False</span><span class="sxs-lookup"><span data-stu-id="9811a-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="9811a-737">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="9811a-738">Converteert Hallo opgegeven tooa tekenreekswaarde.</span><span class="sxs-lookup"><span data-stu-id="9811a-738">Converts hello specified value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-739">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-739">Parameters</span></span>

| <span data-ttu-id="9811a-740">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-740">Parameter</span></span> | <span data-ttu-id="9811a-741">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-741">Required</span></span> | <span data-ttu-id="9811a-742">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-742">Type</span></span> | <span data-ttu-id="9811a-743">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="9811a-744">valueToConvert</span></span> |<span data-ttu-id="9811a-745">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-745">Yes</span></span> | <span data-ttu-id="9811a-746">Alle</span><span class="sxs-lookup"><span data-stu-id="9811a-746">Any</span></span> |<span data-ttu-id="9811a-747">Hallo waarde tooconvert toostring.</span><span class="sxs-lookup"><span data-stu-id="9811a-747">hello value tooconvert toostring.</span></span> <span data-ttu-id="9811a-748">Elk type waarde kan worden geconverteerd, met inbegrip van objecten en -matrices.</span><span class="sxs-lookup"><span data-stu-id="9811a-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-749">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-749">Return value</span></span>

<span data-ttu-id="9811a-750">Een tekenreeks van Hallo geconverteerd-waarde.</span><span class="sxs-lookup"><span data-stu-id="9811a-750">A string of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-751">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-751">Examples</span></span>

<span data-ttu-id="9811a-752">Hallo volgende voorbeeld ziet u hoe verschillende typen tooconvert toostrings waarden:</span><span class="sxs-lookup"><span data-stu-id="9811a-752">hello following example shows how tooconvert different types of values toostrings:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testObject": {
            "type": "object",
            "defaultValue": {
                "valueA": 10,
                "valueB": "Example Text"
            }
        },
        "testArray": {
            "type": "array",
            "defaultValue": [
                "a",
                "b",
                "c"
            ]
        },
        "testInt": {
            "type": "int",
            "defaultValue": 5
        }
    },
    "resources": [],
    "outputs": {
        "objectOutput": {
            "type": "string",
            "value": "[string(parameters('testObject'))]"
        },
        "arrayOutput": {
            "type": "string",
            "value": "[string(parameters('testArray'))]"
        },
        "intOutput": {
            "type": "string",
            "value": "[string(parameters('testInt'))]"
        }
    }
}
```

<span data-ttu-id="9811a-753">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-753">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-754">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-754">Name</span></span> | <span data-ttu-id="9811a-755">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-755">Type</span></span> | <span data-ttu-id="9811a-756">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-757">objectOutput</span></span> | <span data-ttu-id="9811a-758">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-758">String</span></span> | <span data-ttu-id="9811a-759">{{'valueA': 10, 'valueB': "Voorbeeldtekst"}</span><span class="sxs-lookup"><span data-stu-id="9811a-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="9811a-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-760">arrayOutput</span></span> | <span data-ttu-id="9811a-761">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-761">String</span></span> | <span data-ttu-id="9811a-762">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="9811a-762">["a","b","c"]</span></span> |
| <span data-ttu-id="9811a-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-763">intOutput</span></span> | <span data-ttu-id="9811a-764">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-764">String</span></span> | <span data-ttu-id="9811a-765">5</span><span class="sxs-lookup"><span data-stu-id="9811a-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="9811a-766">de subtekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="9811a-767">Retourneert een subtekenreeks dat begint bij Hallo opgegeven tekenpositie en bevat Hallo opgegeven aantal tekens.</span><span class="sxs-lookup"><span data-stu-id="9811a-767">Returns a substring that starts at hello specified character position and contains hello specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-768">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-768">Parameters</span></span>

| <span data-ttu-id="9811a-769">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-769">Parameter</span></span> | <span data-ttu-id="9811a-770">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-770">Required</span></span> | <span data-ttu-id="9811a-771">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-771">Type</span></span> | <span data-ttu-id="9811a-772">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-773">stringToParse</span><span class="sxs-lookup"><span data-stu-id="9811a-773">stringToParse</span></span> |<span data-ttu-id="9811a-774">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-774">Yes</span></span> |<span data-ttu-id="9811a-775">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-775">string</span></span> |<span data-ttu-id="9811a-776">de oorspronkelijke reeks Hallo van welke Hallo subtekenreeks wordt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="9811a-776">hello original string from which hello substring is extracted.</span></span> |
| <span data-ttu-id="9811a-777">startIndex</span><span class="sxs-lookup"><span data-stu-id="9811a-777">startIndex</span></span> |<span data-ttu-id="9811a-778">Nee</span><span class="sxs-lookup"><span data-stu-id="9811a-778">No</span></span> |<span data-ttu-id="9811a-779">int</span><span class="sxs-lookup"><span data-stu-id="9811a-779">int</span></span> |<span data-ttu-id="9811a-780">Hallo op nul gebaseerde beginpositie voor Hallo substring.</span><span class="sxs-lookup"><span data-stu-id="9811a-780">hello zero-based starting character position for hello substring.</span></span> |
| <span data-ttu-id="9811a-781">lengte</span><span class="sxs-lookup"><span data-stu-id="9811a-781">length</span></span> |<span data-ttu-id="9811a-782">Nee</span><span class="sxs-lookup"><span data-stu-id="9811a-782">No</span></span> |<span data-ttu-id="9811a-783">int</span><span class="sxs-lookup"><span data-stu-id="9811a-783">int</span></span> |<span data-ttu-id="9811a-784">Hallo aantal tekens voor Hallo substring.</span><span class="sxs-lookup"><span data-stu-id="9811a-784">hello number of characters for hello substring.</span></span> <span data-ttu-id="9811a-785">Moet verwijzen tooa locatie binnen Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-785">Must refer tooa location within hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-786">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-786">Return value</span></span>

<span data-ttu-id="9811a-787">Hallo substring.</span><span class="sxs-lookup"><span data-stu-id="9811a-787">hello substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="9811a-788">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9811a-788">Remarks</span></span>

<span data-ttu-id="9811a-789">Hallo-functie mislukt wanneer Hallo subtekenreeks Hallo einde van de Hallo tekenreeks overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="9811a-789">hello function fails when hello substring extends beyond hello end of hello string.</span></span> <span data-ttu-id="9811a-790">Hallo volgt mislukt met de Hallo fout 'hello index en lengte parameters moeten verwijzen tooa locatie binnen Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-790">hello following example fails with hello error "hello index and length parameters must refer tooa location within hello string.</span></span> <span data-ttu-id="9811a-791">Hallo Indexparameter: '0' Hallo lengteparameter: '11' Hallo lengte van de tekenreeksparameter Hallo: "10". ".</span><span class="sxs-lookup"><span data-stu-id="9811a-791">hello index parameter: '0', hello length parameter: '11', hello length of hello string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="9811a-792">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-792">Examples</span></span>

<span data-ttu-id="9811a-793">Hallo volgt subtekenreeks een uit een parameter.</span><span class="sxs-lookup"><span data-stu-id="9811a-793">hello following example extracts a substring from a parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        }
    },
    "resources": [],
    "outputs": {
        "substringOutput": {
            "value": "[substring(parameters('testString'), 4, 3)]",
            "type": "string"
        }
    }
}
```

<span data-ttu-id="9811a-794">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-794">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-795">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-795">Name</span></span> | <span data-ttu-id="9811a-796">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-796">Type</span></span> | <span data-ttu-id="9811a-797">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-798">substringOutput</span></span> | <span data-ttu-id="9811a-799">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-799">String</span></span> | <span data-ttu-id="9811a-800">twee</span><span class="sxs-lookup"><span data-stu-id="9811a-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="9811a-801">duren</span><span class="sxs-lookup"><span data-stu-id="9811a-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="9811a-802">Retourneert een tekenreeks met Hallo aantal tekens vanaf het begin van Hallo opgegeven Hallo tekenreeks of een matrix met Hallo opgegeven aantal elementen vanaf het begin van de matrix Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="9811a-802">Returns a string with hello specified number of characters from hello start of hello string, or an array with hello specified number of elements from hello start of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-803">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-803">Parameters</span></span>

| <span data-ttu-id="9811a-804">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-804">Parameter</span></span> | <span data-ttu-id="9811a-805">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-805">Required</span></span> | <span data-ttu-id="9811a-806">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-806">Type</span></span> | <span data-ttu-id="9811a-807">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="9811a-808">originalValue</span></span> |<span data-ttu-id="9811a-809">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-809">Yes</span></span> |<span data-ttu-id="9811a-810">matrix of tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-810">array or string</span></span> |<span data-ttu-id="9811a-811">Hallo matrix of tekenreeks tootake Hallo elementen uit.</span><span class="sxs-lookup"><span data-stu-id="9811a-811">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="9811a-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="9811a-812">numberToTake</span></span> |<span data-ttu-id="9811a-813">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-813">Yes</span></span> |<span data-ttu-id="9811a-814">int</span><span class="sxs-lookup"><span data-stu-id="9811a-814">int</span></span> |<span data-ttu-id="9811a-815">Hallo aantal elementen of tekens tootake.</span><span class="sxs-lookup"><span data-stu-id="9811a-815">hello number of elements or characters tootake.</span></span> <span data-ttu-id="9811a-816">Als deze waarde 0 of minder is, wordt een lege matrix of tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9811a-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="9811a-817">Als het is groter dan de lengte Hallo Hallo gegeven matrix of tekenreeks, worden alle Hallo-elementen in het Hallo-matrix of tekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9811a-817">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-818">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-818">Return value</span></span>

<span data-ttu-id="9811a-819">Een matrix of tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="9811a-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-820">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-820">Examples</span></span>

<span data-ttu-id="9811a-821">Hallo voorbeeld vergt Hallo na een opgegeven aantal elementen van een matrix van Hallo en tekens uit een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-821">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

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

<span data-ttu-id="9811a-822">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-822">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-823">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-823">Name</span></span> | <span data-ttu-id="9811a-824">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-824">Type</span></span> | <span data-ttu-id="9811a-825">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-826">arrayOutput</span></span> | <span data-ttu-id="9811a-827">Matrix</span><span class="sxs-lookup"><span data-stu-id="9811a-827">Array</span></span> | <span data-ttu-id="9811a-828">['een', 'twee']</span><span class="sxs-lookup"><span data-stu-id="9811a-828">["one", "two"]</span></span> |
| <span data-ttu-id="9811a-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-829">stringOutput</span></span> | <span data-ttu-id="9811a-830">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-830">String</span></span> | <span data-ttu-id="9811a-831">op</span><span class="sxs-lookup"><span data-stu-id="9811a-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="9811a-832">toLower</span><span class="sxs-lookup"><span data-stu-id="9811a-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="9811a-833">Converteert Hallo opgegeven tekenreeks toolower geval.</span><span class="sxs-lookup"><span data-stu-id="9811a-833">Converts hello specified string toolower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-834">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-834">Parameters</span></span>

| <span data-ttu-id="9811a-835">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-835">Parameter</span></span> | <span data-ttu-id="9811a-836">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-836">Required</span></span> | <span data-ttu-id="9811a-837">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-837">Type</span></span> | <span data-ttu-id="9811a-838">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-839">stringToChange</span><span class="sxs-lookup"><span data-stu-id="9811a-839">stringToChange</span></span> |<span data-ttu-id="9811a-840">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-840">Yes</span></span> |<span data-ttu-id="9811a-841">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-841">string</span></span> |<span data-ttu-id="9811a-842">Hallo waarde tooconvert toolower geval.</span><span class="sxs-lookup"><span data-stu-id="9811a-842">hello value tooconvert toolower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-843">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-843">Return value</span></span>

<span data-ttu-id="9811a-844">Hallo-tekenreeks geconverteerd toolower geval.</span><span class="sxs-lookup"><span data-stu-id="9811a-844">hello string converted toolower case.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-845">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-845">Examples</span></span>

<span data-ttu-id="9811a-846">Hallo volgt converteert een parameter waarde toolower geval en tooupper geval.</span><span class="sxs-lookup"><span data-stu-id="9811a-846">hello following example converts a parameter value toolower case and tooupper case.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="9811a-847">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-847">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-848">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-848">Name</span></span> | <span data-ttu-id="9811a-849">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-849">Type</span></span> | <span data-ttu-id="9811a-850">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-851">toLowerOutput</span></span> | <span data-ttu-id="9811a-852">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-852">String</span></span> | <span data-ttu-id="9811a-853">Een twee drie</span><span class="sxs-lookup"><span data-stu-id="9811a-853">one two three</span></span> |
| <span data-ttu-id="9811a-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-854">toUpperOutput</span></span> | <span data-ttu-id="9811a-855">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-855">String</span></span> | <span data-ttu-id="9811a-856">EEN TWEE DRIE</span><span class="sxs-lookup"><span data-stu-id="9811a-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="9811a-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="9811a-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="9811a-858">Converteert Hallo opgegeven tekenreeks tooupper geval.</span><span class="sxs-lookup"><span data-stu-id="9811a-858">Converts hello specified string tooupper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-859">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-859">Parameters</span></span>

| <span data-ttu-id="9811a-860">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-860">Parameter</span></span> | <span data-ttu-id="9811a-861">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-861">Required</span></span> | <span data-ttu-id="9811a-862">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-862">Type</span></span> | <span data-ttu-id="9811a-863">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-864">stringToChange</span><span class="sxs-lookup"><span data-stu-id="9811a-864">stringToChange</span></span> |<span data-ttu-id="9811a-865">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-865">Yes</span></span> |<span data-ttu-id="9811a-866">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-866">string</span></span> |<span data-ttu-id="9811a-867">Hallo waarde tooconvert tooupper geval.</span><span class="sxs-lookup"><span data-stu-id="9811a-867">hello value tooconvert tooupper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-868">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-868">Return value</span></span>

<span data-ttu-id="9811a-869">Hallo-tekenreeks geconverteerd tooupper geval.</span><span class="sxs-lookup"><span data-stu-id="9811a-869">hello string converted tooupper case.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-870">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-870">Examples</span></span>

<span data-ttu-id="9811a-871">Hallo volgt converteert een parameter waarde toolower geval en tooupper geval.</span><span class="sxs-lookup"><span data-stu-id="9811a-871">hello following example converts a parameter value toolower case and tooupper case.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="9811a-872">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-872">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-873">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-873">Name</span></span> | <span data-ttu-id="9811a-874">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-874">Type</span></span> | <span data-ttu-id="9811a-875">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-876">toLowerOutput</span></span> | <span data-ttu-id="9811a-877">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-877">String</span></span> | <span data-ttu-id="9811a-878">Een twee drie</span><span class="sxs-lookup"><span data-stu-id="9811a-878">one two three</span></span> |
| <span data-ttu-id="9811a-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-879">toUpperOutput</span></span> | <span data-ttu-id="9811a-880">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-880">String</span></span> | <span data-ttu-id="9811a-881">EEN TWEE DRIE</span><span class="sxs-lookup"><span data-stu-id="9811a-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="9811a-882">Trim</span><span class="sxs-lookup"><span data-stu-id="9811a-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="9811a-883">Hiermee verwijdert u alle voorloopspaties en afsluitende spaties uit Hallo opgegeven tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-883">Removes all leading and trailing white-space characters from hello specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-884">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-884">Parameters</span></span>

| <span data-ttu-id="9811a-885">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-885">Parameter</span></span> | <span data-ttu-id="9811a-886">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-886">Required</span></span> | <span data-ttu-id="9811a-887">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-887">Type</span></span> | <span data-ttu-id="9811a-888">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="9811a-889">stringToTrim</span></span> |<span data-ttu-id="9811a-890">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-890">Yes</span></span> |<span data-ttu-id="9811a-891">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-891">string</span></span> |<span data-ttu-id="9811a-892">Hallo waarde tootrim.</span><span class="sxs-lookup"><span data-stu-id="9811a-892">hello value tootrim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-893">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-893">Return value</span></span>

<span data-ttu-id="9811a-894">Hallo tekenreeks zonder voorloopspaties en afsluitende spatietekens bestaan.</span><span class="sxs-lookup"><span data-stu-id="9811a-894">hello string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-895">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-895">Examples</span></span>

<span data-ttu-id="9811a-896">Hallo verwijdert volgende voorbeeld Hallo spatietekens bestaan uit Hallo-parameter.</span><span class="sxs-lookup"><span data-stu-id="9811a-896">hello following example trims hello white-space characters from hello parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "    one two three   "
        }
    },
    "resources": [],
    "outputs": {
        "return": {
            "type": "string",
            "value": "[trim(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="9811a-897">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-897">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-898">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-898">Name</span></span> | <span data-ttu-id="9811a-899">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-899">Type</span></span> | <span data-ttu-id="9811a-900">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-901">retourneren</span><span class="sxs-lookup"><span data-stu-id="9811a-901">return</span></span> | <span data-ttu-id="9811a-902">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-902">String</span></span> | <span data-ttu-id="9811a-903">Een twee drie</span><span class="sxs-lookup"><span data-stu-id="9811a-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="9811a-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="9811a-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="9811a-905">Maakt een deterministische hash-tekenreeks op basis van Hallo waarden als parameters opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9811a-905">Creates a deterministic hash string based on hello values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="9811a-906">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-906">Parameters</span></span>

| <span data-ttu-id="9811a-907">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-907">Parameter</span></span> | <span data-ttu-id="9811a-908">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-908">Required</span></span> | <span data-ttu-id="9811a-909">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-909">Type</span></span> | <span data-ttu-id="9811a-910">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-911">baseString</span><span class="sxs-lookup"><span data-stu-id="9811a-911">baseString</span></span> |<span data-ttu-id="9811a-912">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-912">Yes</span></span> |<span data-ttu-id="9811a-913">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-913">string</span></span> |<span data-ttu-id="9811a-914">Hallo-waarde die is gebruikt in Hallo hash-functie toocreate een unieke tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-914">hello value used in hello hash function toocreate a unique string.</span></span> |
| <span data-ttu-id="9811a-915">extra parameters indien nodig</span><span class="sxs-lookup"><span data-stu-id="9811a-915">additional parameters as needed</span></span> |<span data-ttu-id="9811a-916">Nee</span><span class="sxs-lookup"><span data-stu-id="9811a-916">No</span></span> |<span data-ttu-id="9811a-917">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-917">string</span></span> |<span data-ttu-id="9811a-918">U kunt zoveel tekenreeksen als benodigde toocreate Hallo waarde die Hallo niveau van uniekheid aangeeft toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9811a-918">You can add as many strings as needed toocreate hello value that specifies hello level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="9811a-919">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9811a-919">Remarks</span></span>

<span data-ttu-id="9811a-920">Deze functie is handig wanneer u een unieke naam voor een resource toocreate nodig.</span><span class="sxs-lookup"><span data-stu-id="9811a-920">This function is helpful when you need toocreate a unique name for a resource.</span></span> <span data-ttu-id="9811a-921">U opgeven parameterwaarden die Hallo uniciteitsbereik voor Hallo resultaat beperken.</span><span class="sxs-lookup"><span data-stu-id="9811a-921">You provide parameter values that limit hello scope of uniqueness for hello result.</span></span> <span data-ttu-id="9811a-922">U kunt opgeven of de naam van de Hallo unieke omlaag toosubscription, resourcegroep of implementatie.</span><span class="sxs-lookup"><span data-stu-id="9811a-922">You can specify whether hello name is unique down toosubscription, resource group, or deployment.</span></span> 

<span data-ttu-id="9811a-923">Hallo geretourneerde waarde is niet een willekeurige tekenreeks op, maar in plaats daarvan Hallo resultaat van een hash-functie.</span><span class="sxs-lookup"><span data-stu-id="9811a-923">hello returned value is not a random string, but rather hello result of a hash function.</span></span> <span data-ttu-id="9811a-924">Hallo geretourneerde waarde 13 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="9811a-924">hello returned value is 13 characters long.</span></span> <span data-ttu-id="9811a-925">Het is niet uniek.</span><span class="sxs-lookup"><span data-stu-id="9811a-925">It is not globally unique.</span></span> <span data-ttu-id="9811a-926">U kunt toocombine Hallo-waarde met een voorvoegsel van uw naming convention toocreate een beschrijvende naam.</span><span class="sxs-lookup"><span data-stu-id="9811a-926">You may want toocombine hello value with a prefix from your naming convention toocreate a name that is meaningful.</span></span> <span data-ttu-id="9811a-927">Hallo volgende voorbeeld ziet u de indeling Hallo Hallo waarde geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9811a-927">hello following example shows hello format of hello returned value.</span></span> <span data-ttu-id="9811a-928">Hallo werkelijke waarde verschilt per Hallo parameters opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9811a-928">hello actual value varies by hello provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="9811a-929">Hallo volgen voorbeelden laten zien hoe toouse uniqueString toocreate een unieke waarde voor vaak gebruikte niveaus.</span><span class="sxs-lookup"><span data-stu-id="9811a-929">hello following examples show how toouse uniqueString toocreate a unique value for commonly used levels.</span></span>

<span data-ttu-id="9811a-930">Uniek binnen het bereik toosubscription</span><span class="sxs-lookup"><span data-stu-id="9811a-930">Unique scoped toosubscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="9811a-931">Uniek binnen het bereik tooresource groep</span><span class="sxs-lookup"><span data-stu-id="9811a-931">Unique scoped tooresource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="9811a-932">Uniek binnen het bereik toodeployment voor een resourcegroep</span><span class="sxs-lookup"><span data-stu-id="9811a-932">Unique scoped toodeployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="9811a-933">Hallo volgende voorbeeld ziet u hoe toocreate een unieke naam voor een opslagaccount op basis van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="9811a-933">hello following example shows how toocreate a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="9811a-934">In de resourcegroep hello, Hallo naam is niet uniek als Hallo samengesteld dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="9811a-934">Inside hello resource group, hello name is not unique if constructed hello same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="9811a-935">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-935">Return value</span></span>

<span data-ttu-id="9811a-936">Een tekenreeks met 13 tekens.</span><span class="sxs-lookup"><span data-stu-id="9811a-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-937">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-937">Examples</span></span>

<span data-ttu-id="9811a-938">Hallo volgende voorbeeld retourneert de resultaten van uniquestring:</span><span class="sxs-lookup"><span data-stu-id="9811a-938">hello following example returns results from uniquestring:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "uniqueRG": {
            "value": "[uniqueString(resourceGroup().id)]",
            "type" : "string"
        },
        "uniqueDeploy": {
            "value": "[uniqueString(resourceGroup().id, deployment().name)]",
            "type" : "string"
        }
    }
}
```

<a id="uri" />

## <a name="uri"></a><span data-ttu-id="9811a-939">URI</span><span class="sxs-lookup"><span data-stu-id="9811a-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="9811a-940">Maakt een absolute URI door Hallo baseUri en Hallo relativeUri tekenreeks te combineren.</span><span class="sxs-lookup"><span data-stu-id="9811a-940">Creates an absolute URI by combining hello baseUri and hello relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-941">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-941">Parameters</span></span>

| <span data-ttu-id="9811a-942">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-942">Parameter</span></span> | <span data-ttu-id="9811a-943">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-943">Required</span></span> | <span data-ttu-id="9811a-944">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-944">Type</span></span> | <span data-ttu-id="9811a-945">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-946">baseUri</span><span class="sxs-lookup"><span data-stu-id="9811a-946">baseUri</span></span> |<span data-ttu-id="9811a-947">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-947">Yes</span></span> |<span data-ttu-id="9811a-948">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-948">string</span></span> |<span data-ttu-id="9811a-949">Hallo basis-uri-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-949">hello base uri string.</span></span> |
| <span data-ttu-id="9811a-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="9811a-950">relativeUri</span></span> |<span data-ttu-id="9811a-951">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-951">Yes</span></span> |<span data-ttu-id="9811a-952">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-952">string</span></span> |<span data-ttu-id="9811a-953">Hallo relatieve uri tekenreeks tooadd toohello basis-uri-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-953">hello relative uri string tooadd toohello base uri string.</span></span> |

<span data-ttu-id="9811a-954">waarde voor Hallo Hallo **baseUri** parameter kan een specifiek bestand bevatten, maar alleen het basispad hello wordt gebruikt tijdens het construeren van Hallo URI.</span><span class="sxs-lookup"><span data-stu-id="9811a-954">hello value for hello **baseUri** parameter can include a specific file, but only hello base path is used when constructing hello URI.</span></span> <span data-ttu-id="9811a-955">Bijvoorbeeld, doorgeven `http://contoso.com/resources/azuredeploy.json` als Hallo baseUri parameter resulteert in een basis-URI van `http://contoso.com/resources/`.</span><span class="sxs-lookup"><span data-stu-id="9811a-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as hello baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="9811a-956">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-956">Return value</span></span>

<span data-ttu-id="9811a-957">Een tekenreeks voor Hallo absolute URI voor Hallo basis en relatieve waarden.</span><span class="sxs-lookup"><span data-stu-id="9811a-957">A string representing hello absolute URI for hello base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-958">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-958">Examples</span></span>

<span data-ttu-id="9811a-959">Hallo volgende voorbeeld ziet u hoe tooconstruct een koppeling tooa geneste sjabloon op basis van Hallo-waarde van sjabloon voor bovenliggend Hallo.</span><span class="sxs-lookup"><span data-stu-id="9811a-959">hello following example shows how tooconstruct a link tooa nested template based on hello value of hello parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="9811a-960">Hallo volgende voorbeeld wordt getoond hoe toouse uri, uriComponent, en uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="9811a-960">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="9811a-961">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-961">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-962">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-962">Name</span></span> | <span data-ttu-id="9811a-963">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-963">Type</span></span> | <span data-ttu-id="9811a-964">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-965">uriOutput</span></span> | <span data-ttu-id="9811a-966">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-966">String</span></span> | <span data-ttu-id="9811a-967">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="9811a-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="9811a-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-968">componentOutput</span></span> | <span data-ttu-id="9811a-969">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-969">String</span></span> | <span data-ttu-id="9811a-970">HTTP%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="9811a-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="9811a-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-971">toStringOutput</span></span> | <span data-ttu-id="9811a-972">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-972">String</span></span> | <span data-ttu-id="9811a-973">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="9811a-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="9811a-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="9811a-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="9811a-975">Codeert een URI.</span><span class="sxs-lookup"><span data-stu-id="9811a-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-976">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-976">Parameters</span></span>

| <span data-ttu-id="9811a-977">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-977">Parameter</span></span> | <span data-ttu-id="9811a-978">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-978">Required</span></span> | <span data-ttu-id="9811a-979">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-979">Type</span></span> | <span data-ttu-id="9811a-980">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="9811a-981">stringToEncode</span></span> |<span data-ttu-id="9811a-982">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-982">Yes</span></span> |<span data-ttu-id="9811a-983">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-983">string</span></span> |<span data-ttu-id="9811a-984">Hallo waarde tooencode.</span><span class="sxs-lookup"><span data-stu-id="9811a-984">hello value tooencode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-985">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-985">Return value</span></span>

<span data-ttu-id="9811a-986">Een tekenreeks van Hallo URI gecodeerde waarde.</span><span class="sxs-lookup"><span data-stu-id="9811a-986">A string of hello URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-987">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-987">Examples</span></span>

<span data-ttu-id="9811a-988">Hallo volgende voorbeeld wordt getoond hoe toouse uri, uriComponent, en uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="9811a-988">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="9811a-989">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-989">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-990">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-990">Name</span></span> | <span data-ttu-id="9811a-991">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-991">Type</span></span> | <span data-ttu-id="9811a-992">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-993">uriOutput</span></span> | <span data-ttu-id="9811a-994">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-994">String</span></span> | <span data-ttu-id="9811a-995">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="9811a-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="9811a-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-996">componentOutput</span></span> | <span data-ttu-id="9811a-997">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-997">String</span></span> | <span data-ttu-id="9811a-998">HTTP%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="9811a-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="9811a-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-999">toStringOutput</span></span> | <span data-ttu-id="9811a-1000">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-1000">String</span></span> | <span data-ttu-id="9811a-1001">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="9811a-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="9811a-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="9811a-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="9811a-1003">Retourneert dat een tekenreeks van een URI-gecodeerde waarde.</span><span class="sxs-lookup"><span data-stu-id="9811a-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="9811a-1004">Parameters</span><span class="sxs-lookup"><span data-stu-id="9811a-1004">Parameters</span></span>

| <span data-ttu-id="9811a-1005">Parameter</span><span class="sxs-lookup"><span data-stu-id="9811a-1005">Parameter</span></span> | <span data-ttu-id="9811a-1006">Vereist</span><span class="sxs-lookup"><span data-stu-id="9811a-1006">Required</span></span> | <span data-ttu-id="9811a-1007">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-1007">Type</span></span> | <span data-ttu-id="9811a-1008">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9811a-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9811a-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="9811a-1009">uriEncodedString</span></span> |<span data-ttu-id="9811a-1010">Ja</span><span class="sxs-lookup"><span data-stu-id="9811a-1010">Yes</span></span> |<span data-ttu-id="9811a-1011">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-1011">string</span></span> |<span data-ttu-id="9811a-1012">Hallo URI-gecodeerde waarde tooconvert tooa tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9811a-1012">hello URI encoded value tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9811a-1013">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="9811a-1013">Return value</span></span>

<span data-ttu-id="9811a-1014">Een gecodeerde tekenreeks van URI gecodeerde waarde.</span><span class="sxs-lookup"><span data-stu-id="9811a-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="9811a-1015">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9811a-1015">Examples</span></span>

<span data-ttu-id="9811a-1016">Hallo volgende voorbeeld wordt getoond hoe toouse uri, uriComponent, en uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="9811a-1016">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="9811a-1017">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="9811a-1017">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9811a-1018">Naam</span><span class="sxs-lookup"><span data-stu-id="9811a-1018">Name</span></span> | <span data-ttu-id="9811a-1019">Type</span><span class="sxs-lookup"><span data-stu-id="9811a-1019">Type</span></span> | <span data-ttu-id="9811a-1020">Waarde</span><span class="sxs-lookup"><span data-stu-id="9811a-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9811a-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-1021">uriOutput</span></span> | <span data-ttu-id="9811a-1022">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-1022">String</span></span> | <span data-ttu-id="9811a-1023">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="9811a-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="9811a-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-1024">componentOutput</span></span> | <span data-ttu-id="9811a-1025">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-1025">String</span></span> | <span data-ttu-id="9811a-1026">HTTP%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="9811a-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="9811a-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="9811a-1027">toStringOutput</span></span> | <span data-ttu-id="9811a-1028">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9811a-1028">String</span></span> | <span data-ttu-id="9811a-1029">http://contoso.com/resources/Nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="9811a-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="9811a-1030">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9811a-1030">Next steps</span></span>
* <span data-ttu-id="9811a-1031">Zie voor een beschrijving van de secties Hallo in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9811a-1031">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="9811a-1032">toomerge meerdere sjablonen Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9811a-1032">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="9811a-1033">een opgegeven aantal keren tooiterate bij het maken van een type resource, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="9811a-1033">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="9811a-1034">toosee hoe toodeploy Hallo sjabloon die u hebt gemaakt, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="9811a-1034">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

