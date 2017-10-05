---
title: Azure Resource Manager-sjabloonfuncties - numerieke | Microsoft Docs
description: Beschrijft de functies in een Azure Resource Manager-sjabloon gebruiken om te werken met getallen.
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
ms.openlocfilehash: ae0261134b8d4a934048f58d6c679a48a904950b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="c3d61-103">Numerieke functies voor Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="c3d61-103">Numeric functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="c3d61-104">Resource Manager biedt de volgende functies voor het werken met gehele getallen zijn:</span><span class="sxs-lookup"><span data-stu-id="c3d61-104">Resource Manager provides the following functions for working with integers:</span></span>

* [<span data-ttu-id="c3d61-105">toevoegen</span><span class="sxs-lookup"><span data-stu-id="c3d61-105">add</span></span>](#add)
* [<span data-ttu-id="c3d61-106">copyIndex</span><span class="sxs-lookup"><span data-stu-id="c3d61-106">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="c3d61-107">div</span><span class="sxs-lookup"><span data-stu-id="c3d61-107">div</span></span>](#div)
* [<span data-ttu-id="c3d61-108">Float</span><span class="sxs-lookup"><span data-stu-id="c3d61-108">float</span></span>](#float)
* [<span data-ttu-id="c3d61-109">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-109">int</span></span>](#int)
* [<span data-ttu-id="c3d61-110">min</span><span class="sxs-lookup"><span data-stu-id="c3d61-110">min</span></span>](#min)
* [<span data-ttu-id="c3d61-111">maximale</span><span class="sxs-lookup"><span data-stu-id="c3d61-111">max</span></span>](#max)
* [<span data-ttu-id="c3d61-112">Mod</span><span class="sxs-lookup"><span data-stu-id="c3d61-112">mod</span></span>](#mod)
* [<span data-ttu-id="c3d61-113">mul</span><span class="sxs-lookup"><span data-stu-id="c3d61-113">mul</span></span>](#mul)
* [<span data-ttu-id="c3d61-114">Sub</span><span class="sxs-lookup"><span data-stu-id="c3d61-114">sub</span></span>](#sub)

<a id="add" />

## <a name="add"></a><span data-ttu-id="c3d61-115">toevoegen</span><span class="sxs-lookup"><span data-stu-id="c3d61-115">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="c3d61-116">Retourneert de som van de twee opgegeven getallen.</span><span class="sxs-lookup"><span data-stu-id="c3d61-116">Returns the sum of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c3d61-117">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3d61-117">Parameters</span></span>

| <span data-ttu-id="c3d61-118">Parameter</span><span class="sxs-lookup"><span data-stu-id="c3d61-118">Parameter</span></span> | <span data-ttu-id="c3d61-119">Vereist</span><span class="sxs-lookup"><span data-stu-id="c3d61-119">Required</span></span> | <span data-ttu-id="c3d61-120">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-120">Type</span></span> | <span data-ttu-id="c3d61-121">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c3d61-121">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="c3d61-122">operand1</span><span class="sxs-lookup"><span data-stu-id="c3d61-122">operand1</span></span> |<span data-ttu-id="c3d61-123">Ja</span><span class="sxs-lookup"><span data-stu-id="c3d61-123">Yes</span></span> |<span data-ttu-id="c3d61-124">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-124">int</span></span> |<span data-ttu-id="c3d61-125">Eerste nummer om toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="c3d61-125">First number to add.</span></span> |
|<span data-ttu-id="c3d61-126">operand2</span><span class="sxs-lookup"><span data-stu-id="c3d61-126">operand2</span></span> |<span data-ttu-id="c3d61-127">Ja</span><span class="sxs-lookup"><span data-stu-id="c3d61-127">Yes</span></span> |<span data-ttu-id="c3d61-128">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-128">int</span></span> |<span data-ttu-id="c3d61-129">Tweede getal om toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="c3d61-129">Second number to add.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c3d61-130">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-130">Return value</span></span>

<span data-ttu-id="c3d61-131">Een geheel getal dat de som van de parameters bevat.</span><span class="sxs-lookup"><span data-stu-id="c3d61-131">An integer that contains the sum of the parameters.</span></span>

### <a name="example"></a><span data-ttu-id="c3d61-132">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c3d61-132">Example</span></span>

<span data-ttu-id="c3d61-133">Het volgende voorbeeld voegt twee parameters.</span><span class="sxs-lookup"><span data-stu-id="c3d61-133">The following example adds two parameters.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer to add"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer to add"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "addResult": {
            "type": "int",
            "value": "[add(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="c3d61-134">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="c3d61-134">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c3d61-135">Naam</span><span class="sxs-lookup"><span data-stu-id="c3d61-135">Name</span></span> | <span data-ttu-id="c3d61-136">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-136">Type</span></span> | <span data-ttu-id="c3d61-137">Waarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-137">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c3d61-138">addResult</span><span class="sxs-lookup"><span data-stu-id="c3d61-138">addResult</span></span> | <span data-ttu-id="c3d61-139">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-139">Int</span></span> | <span data-ttu-id="c3d61-140">8</span><span class="sxs-lookup"><span data-stu-id="c3d61-140">8</span></span> |

<a id="copyindex" />

## <a name="copyindex"></a><span data-ttu-id="c3d61-141">copyIndex</span><span class="sxs-lookup"><span data-stu-id="c3d61-141">copyIndex</span></span>
`copyIndex(loopName, offset)`

<span data-ttu-id="c3d61-142">Retourneert de index van een lus herhaling.</span><span class="sxs-lookup"><span data-stu-id="c3d61-142">Returns the index of an iteration loop.</span></span> 

### <a name="parameters"></a><span data-ttu-id="c3d61-143">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3d61-143">Parameters</span></span>

| <span data-ttu-id="c3d61-144">Parameter</span><span class="sxs-lookup"><span data-stu-id="c3d61-144">Parameter</span></span> | <span data-ttu-id="c3d61-145">Vereist</span><span class="sxs-lookup"><span data-stu-id="c3d61-145">Required</span></span> | <span data-ttu-id="c3d61-146">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-146">Type</span></span> | <span data-ttu-id="c3d61-147">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c3d61-147">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c3d61-148">loopName</span><span class="sxs-lookup"><span data-stu-id="c3d61-148">loopName</span></span> | <span data-ttu-id="c3d61-149">Nee</span><span class="sxs-lookup"><span data-stu-id="c3d61-149">No</span></span> | <span data-ttu-id="c3d61-150">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c3d61-150">string</span></span> | <span data-ttu-id="c3d61-151">De naam van de lus voor het ophalen van de herhaling.</span><span class="sxs-lookup"><span data-stu-id="c3d61-151">The name of the loop for getting the iteration.</span></span> |
| <span data-ttu-id="c3d61-152">offset</span><span class="sxs-lookup"><span data-stu-id="c3d61-152">offset</span></span> |<span data-ttu-id="c3d61-153">Nee</span><span class="sxs-lookup"><span data-stu-id="c3d61-153">No</span></span> |<span data-ttu-id="c3d61-154">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-154">int</span></span> |<span data-ttu-id="c3d61-155">Het aantal toevoegen aan de op nul gebaseerde herhaling-waarde.</span><span class="sxs-lookup"><span data-stu-id="c3d61-155">The number to add to the zero-based iteration value.</span></span> |

### <a name="remarks"></a><span data-ttu-id="c3d61-156">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="c3d61-156">Remarks</span></span>

<span data-ttu-id="c3d61-157">Deze functie wordt altijd gebruikt met een **kopie** object.</span><span class="sxs-lookup"><span data-stu-id="c3d61-157">This function is always used with a **copy** object.</span></span> <span data-ttu-id="c3d61-158">Als geen waarde is opgegeven voor **offset**, de huidige waarde van de herhaling wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="c3d61-158">If no value is provided for **offset**, the current iteration value is returned.</span></span> <span data-ttu-id="c3d61-159">De waarde van de herhaling start bij nul.</span><span class="sxs-lookup"><span data-stu-id="c3d61-159">The iteration value starts at zero.</span></span>

<span data-ttu-id="c3d61-160">De **loopName** eigenschap kunt u opgeven of copyIndex naar een resource herhaling of eigenschap iteratie verwijst.</span><span class="sxs-lookup"><span data-stu-id="c3d61-160">The **loopName** property enables you to specify whether copyIndex is referring to a resource iteration or property iteration.</span></span> <span data-ttu-id="c3d61-161">Als geen waarde is opgegeven voor **loopName**, de huidige herhaling van de resource-type wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c3d61-161">If no value is provided for **loopName**, the current resource type iteration is used.</span></span> <span data-ttu-id="c3d61-162">Geef een waarde voor **loopName** wanneer voor een eigenschap.</span><span class="sxs-lookup"><span data-stu-id="c3d61-162">Provide a value for **loopName** when iterating on a property.</span></span> 
 
<span data-ttu-id="c3d61-163">Voor een volledige beschrijving van het gebruik van **copyIndex**, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="c3d61-163">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

### <a name="example"></a><span data-ttu-id="c3d61-164">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c3d61-164">Example</span></span>

<span data-ttu-id="c3d61-165">Het volgende voorbeeld ziet een lus kopiëren en opgenomen in de naam van de waarde voor de index.</span><span class="sxs-lookup"><span data-stu-id="c3d61-165">The following example shows a copy loop and the index value included in the name.</span></span> 

```json
"resources": [ 
  { 
    "name": "[concat('examplecopy-', copyIndex())]", 
    "type": "Microsoft.Web/sites", 
    "copy": { 
      "name": "websitescopy", 
      "count": "[parameters('count')]" 
    }, 
    ...
  }
]
```

### <a name="return-value"></a><span data-ttu-id="c3d61-166">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-166">Return value</span></span>

<span data-ttu-id="c3d61-167">Een geheel getal dat de huidige index van de herhaling.</span><span class="sxs-lookup"><span data-stu-id="c3d61-167">An integer representing the current index of the iteration.</span></span>

<a id="div" />

## <a name="div"></a><span data-ttu-id="c3d61-168">div</span><span class="sxs-lookup"><span data-stu-id="c3d61-168">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="c3d61-169">Retourneert het gehele getal van de twee opgegeven getallen.</span><span class="sxs-lookup"><span data-stu-id="c3d61-169">Returns the integer division of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c3d61-170">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3d61-170">Parameters</span></span>

| <span data-ttu-id="c3d61-171">Parameter</span><span class="sxs-lookup"><span data-stu-id="c3d61-171">Parameter</span></span> | <span data-ttu-id="c3d61-172">Vereist</span><span class="sxs-lookup"><span data-stu-id="c3d61-172">Required</span></span> | <span data-ttu-id="c3d61-173">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-173">Type</span></span> | <span data-ttu-id="c3d61-174">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c3d61-174">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c3d61-175">operand1</span><span class="sxs-lookup"><span data-stu-id="c3d61-175">operand1</span></span> |<span data-ttu-id="c3d61-176">Ja</span><span class="sxs-lookup"><span data-stu-id="c3d61-176">Yes</span></span> |<span data-ttu-id="c3d61-177">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-177">int</span></span> |<span data-ttu-id="c3d61-178">Het getal wordt verdeeld.</span><span class="sxs-lookup"><span data-stu-id="c3d61-178">The number being divided.</span></span> |
| <span data-ttu-id="c3d61-179">operand2</span><span class="sxs-lookup"><span data-stu-id="c3d61-179">operand2</span></span> |<span data-ttu-id="c3d61-180">Ja</span><span class="sxs-lookup"><span data-stu-id="c3d61-180">Yes</span></span> |<span data-ttu-id="c3d61-181">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-181">int</span></span> |<span data-ttu-id="c3d61-182">Het nummer dat wordt gebruikt om te delen.</span><span class="sxs-lookup"><span data-stu-id="c3d61-182">The number that is used to divide.</span></span> <span data-ttu-id="c3d61-183">Mag niet 0 zijn.</span><span class="sxs-lookup"><span data-stu-id="c3d61-183">Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c3d61-184">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-184">Return value</span></span>

<span data-ttu-id="c3d61-185">Een geheel getal dat de afdeling.</span><span class="sxs-lookup"><span data-stu-id="c3d61-185">An integer representing the division.</span></span>

### <a name="example"></a><span data-ttu-id="c3d61-186">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c3d61-186">Example</span></span>

<span data-ttu-id="c3d61-187">Het volgende voorbeeld wordt één parameter door een andere parameter verdeeld.</span><span class="sxs-lookup"><span data-stu-id="c3d61-187">The following example divides one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 8,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used to divide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "divResult": {
            "type": "int",
            "value": "[div(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="c3d61-188">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="c3d61-188">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c3d61-189">Naam</span><span class="sxs-lookup"><span data-stu-id="c3d61-189">Name</span></span> | <span data-ttu-id="c3d61-190">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-190">Type</span></span> | <span data-ttu-id="c3d61-191">Waarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-191">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c3d61-192">divResult</span><span class="sxs-lookup"><span data-stu-id="c3d61-192">divResult</span></span> | <span data-ttu-id="c3d61-193">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-193">Int</span></span> | <span data-ttu-id="c3d61-194">2</span><span class="sxs-lookup"><span data-stu-id="c3d61-194">2</span></span> |

<a id="float" />

## <a name="float"></a><span data-ttu-id="c3d61-195">Float</span><span class="sxs-lookup"><span data-stu-id="c3d61-195">float</span></span>
`float(arg1)`

<span data-ttu-id="c3d61-196">De waarde omgezet in een drijvende komma.</span><span class="sxs-lookup"><span data-stu-id="c3d61-196">Converts the value to a floating point number.</span></span> <span data-ttu-id="c3d61-197">U deze functie alleen gebruiken als aangepaste parameters wordt doorgegeven aan een toepassing, zoals een logische App.</span><span class="sxs-lookup"><span data-stu-id="c3d61-197">You only use this function when passing custom parameters to an application, such as a Logic App.</span></span>

### <a name="parameters"></a><span data-ttu-id="c3d61-198">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3d61-198">Parameters</span></span>

| <span data-ttu-id="c3d61-199">Parameter</span><span class="sxs-lookup"><span data-stu-id="c3d61-199">Parameter</span></span> | <span data-ttu-id="c3d61-200">Vereist</span><span class="sxs-lookup"><span data-stu-id="c3d61-200">Required</span></span> | <span data-ttu-id="c3d61-201">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-201">Type</span></span> | <span data-ttu-id="c3d61-202">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c3d61-202">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c3d61-203">Arg1</span><span class="sxs-lookup"><span data-stu-id="c3d61-203">arg1</span></span> |<span data-ttu-id="c3d61-204">Ja</span><span class="sxs-lookup"><span data-stu-id="c3d61-204">Yes</span></span> |<span data-ttu-id="c3d61-205">String of int.</span><span class="sxs-lookup"><span data-stu-id="c3d61-205">string or int</span></span> |<span data-ttu-id="c3d61-206">De waarde converteren naar een drijvende komma.</span><span class="sxs-lookup"><span data-stu-id="c3d61-206">The value to convert to a floating point number.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c3d61-207">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-207">Return value</span></span>
<span data-ttu-id="c3d61-208">Een drijvende komma.</span><span class="sxs-lookup"><span data-stu-id="c3d61-208">A floating point number.</span></span>

### <a name="example"></a><span data-ttu-id="c3d61-209">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c3d61-209">Example</span></span>

<span data-ttu-id="c3d61-210">Het volgende voorbeeld ziet hoe u float parameters doorgeven aan een logische App:</span><span class="sxs-lookup"><span data-stu-id="c3d61-210">The following example shows how to use float to pass parameters to a Logic App:</span></span>

```json
{
    "type": "Microsoft.Logic/workflows",
    "properties": {
        ...
        "parameters": {
        "custom1": {
            "value": "[float('3.0')]"
        },
        "custom2": {
            "value": "[float(3)]"
        },
```

<a id="int" />

## <a name="int"></a><span data-ttu-id="c3d61-211">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-211">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="c3d61-212">De opgegeven waarde converteert naar een geheel getal.</span><span class="sxs-lookup"><span data-stu-id="c3d61-212">Converts the specified value to an integer.</span></span>

### <a name="parameters"></a><span data-ttu-id="c3d61-213">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3d61-213">Parameters</span></span>

| <span data-ttu-id="c3d61-214">Parameter</span><span class="sxs-lookup"><span data-stu-id="c3d61-214">Parameter</span></span> | <span data-ttu-id="c3d61-215">Vereist</span><span class="sxs-lookup"><span data-stu-id="c3d61-215">Required</span></span> | <span data-ttu-id="c3d61-216">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-216">Type</span></span> | <span data-ttu-id="c3d61-217">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c3d61-217">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c3d61-218">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="c3d61-218">valueToConvert</span></span> |<span data-ttu-id="c3d61-219">Ja</span><span class="sxs-lookup"><span data-stu-id="c3d61-219">Yes</span></span> |<span data-ttu-id="c3d61-220">String of int.</span><span class="sxs-lookup"><span data-stu-id="c3d61-220">string or int</span></span> |<span data-ttu-id="c3d61-221">De waarde te converteren naar een geheel getal.</span><span class="sxs-lookup"><span data-stu-id="c3d61-221">The value to convert to an integer.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c3d61-222">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-222">Return value</span></span>

<span data-ttu-id="c3d61-223">Een geheel getal van de geconverteerde waarde.</span><span class="sxs-lookup"><span data-stu-id="c3d61-223">An integer of the converted value.</span></span>

### <a name="example"></a><span data-ttu-id="c3d61-224">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c3d61-224">Example</span></span>

<span data-ttu-id="c3d61-225">Het volgende voorbeeld wordt de gebruiker opgegeven parameterwaarde converteert naar geheel getal.</span><span class="sxs-lookup"><span data-stu-id="c3d61-225">The following example converts the user-provided parameter value to integer.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToConvert": { 
            "type": "string",
            "defaultValue": "4"
        }
    },
    "resources": [
    ],
    "outputs": {
        "intResult": {
            "type": "int",
            "value": "[int(parameters('stringToConvert'))]"
        }
    }
}
```

<span data-ttu-id="c3d61-226">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="c3d61-226">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c3d61-227">Naam</span><span class="sxs-lookup"><span data-stu-id="c3d61-227">Name</span></span> | <span data-ttu-id="c3d61-228">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-228">Type</span></span> | <span data-ttu-id="c3d61-229">Waarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-229">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c3d61-230">intResult</span><span class="sxs-lookup"><span data-stu-id="c3d61-230">intResult</span></span> | <span data-ttu-id="c3d61-231">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-231">Int</span></span> | <span data-ttu-id="c3d61-232">4</span><span class="sxs-lookup"><span data-stu-id="c3d61-232">4</span></span> |


<a id="min" />

## <a name="min"></a><span data-ttu-id="c3d61-233">min.</span><span class="sxs-lookup"><span data-stu-id="c3d61-233">min</span></span>
`min (arg1)`

<span data-ttu-id="c3d61-234">Retourneert de minimumwaarde van een matrix van gehele getallen of een door komma's gescheiden lijst met gehele getallen zijn.</span><span class="sxs-lookup"><span data-stu-id="c3d61-234">Returns the minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c3d61-235">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3d61-235">Parameters</span></span>

| <span data-ttu-id="c3d61-236">Parameter</span><span class="sxs-lookup"><span data-stu-id="c3d61-236">Parameter</span></span> | <span data-ttu-id="c3d61-237">Vereist</span><span class="sxs-lookup"><span data-stu-id="c3d61-237">Required</span></span> | <span data-ttu-id="c3d61-238">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-238">Type</span></span> | <span data-ttu-id="c3d61-239">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c3d61-239">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c3d61-240">Arg1</span><span class="sxs-lookup"><span data-stu-id="c3d61-240">arg1</span></span> |<span data-ttu-id="c3d61-241">Ja</span><span class="sxs-lookup"><span data-stu-id="c3d61-241">Yes</span></span> |<span data-ttu-id="c3d61-242">matrix van gehele getallen of door komma's gescheiden lijst met gehele getallen</span><span class="sxs-lookup"><span data-stu-id="c3d61-242">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="c3d61-243">De verzameling voor de minimumwaarde.</span><span class="sxs-lookup"><span data-stu-id="c3d61-243">The collection to get the minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c3d61-244">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-244">Return value</span></span>

<span data-ttu-id="c3d61-245">Een geheel getal voor de minimale waarde uit de verzameling.</span><span class="sxs-lookup"><span data-stu-id="c3d61-245">An integer representing minimum value from the collection.</span></span>

### <a name="example"></a><span data-ttu-id="c3d61-246">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c3d61-246">Example</span></span>

<span data-ttu-id="c3d61-247">Het volgende voorbeeld ziet u hoe min. gebruik met een matrix en een lijst met gehele getallen zijn:</span><span class="sxs-lookup"><span data-stu-id="c3d61-247">The following example shows how to use min with an array and a list of integers:</span></span>

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

<span data-ttu-id="c3d61-248">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="c3d61-248">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c3d61-249">Naam</span><span class="sxs-lookup"><span data-stu-id="c3d61-249">Name</span></span> | <span data-ttu-id="c3d61-250">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-250">Type</span></span> | <span data-ttu-id="c3d61-251">Waarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-251">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c3d61-252">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c3d61-252">arrayOutput</span></span> | <span data-ttu-id="c3d61-253">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-253">Int</span></span> | <span data-ttu-id="c3d61-254">0</span><span class="sxs-lookup"><span data-stu-id="c3d61-254">0</span></span> |
| <span data-ttu-id="c3d61-255">intOutput</span><span class="sxs-lookup"><span data-stu-id="c3d61-255">intOutput</span></span> | <span data-ttu-id="c3d61-256">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-256">Int</span></span> | <span data-ttu-id="c3d61-257">0</span><span class="sxs-lookup"><span data-stu-id="c3d61-257">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="c3d61-258">Maximum aantal</span><span class="sxs-lookup"><span data-stu-id="c3d61-258">max</span></span>
`max (arg1)`

<span data-ttu-id="c3d61-259">Retourneert de maximumwaarde van een matrix van gehele getallen of een door komma's gescheiden lijst met gehele getallen zijn.</span><span class="sxs-lookup"><span data-stu-id="c3d61-259">Returns the maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c3d61-260">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3d61-260">Parameters</span></span>

| <span data-ttu-id="c3d61-261">Parameter</span><span class="sxs-lookup"><span data-stu-id="c3d61-261">Parameter</span></span> | <span data-ttu-id="c3d61-262">Vereist</span><span class="sxs-lookup"><span data-stu-id="c3d61-262">Required</span></span> | <span data-ttu-id="c3d61-263">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-263">Type</span></span> | <span data-ttu-id="c3d61-264">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c3d61-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c3d61-265">Arg1</span><span class="sxs-lookup"><span data-stu-id="c3d61-265">arg1</span></span> |<span data-ttu-id="c3d61-266">Ja</span><span class="sxs-lookup"><span data-stu-id="c3d61-266">Yes</span></span> |<span data-ttu-id="c3d61-267">matrix van gehele getallen of door komma's gescheiden lijst met gehele getallen</span><span class="sxs-lookup"><span data-stu-id="c3d61-267">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="c3d61-268">De verzameling die de maximale waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="c3d61-268">The collection to get the maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c3d61-269">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-269">Return value</span></span>

<span data-ttu-id="c3d61-270">Een geheel getal dat de maximale waarde uit de verzameling.</span><span class="sxs-lookup"><span data-stu-id="c3d61-270">An integer representing the maximum value from the collection.</span></span>

### <a name="example"></a><span data-ttu-id="c3d61-271">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c3d61-271">Example</span></span>

<span data-ttu-id="c3d61-272">Het volgende voorbeeld ziet u hoe max gebruiken met een matrix en een lijst met gehele getallen zijn:</span><span class="sxs-lookup"><span data-stu-id="c3d61-272">The following example shows how to use max with an array and a list of integers:</span></span>

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

<span data-ttu-id="c3d61-273">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="c3d61-273">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c3d61-274">Naam</span><span class="sxs-lookup"><span data-stu-id="c3d61-274">Name</span></span> | <span data-ttu-id="c3d61-275">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-275">Type</span></span> | <span data-ttu-id="c3d61-276">Waarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-276">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c3d61-277">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c3d61-277">arrayOutput</span></span> | <span data-ttu-id="c3d61-278">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-278">Int</span></span> | <span data-ttu-id="c3d61-279">5</span><span class="sxs-lookup"><span data-stu-id="c3d61-279">5</span></span> |
| <span data-ttu-id="c3d61-280">intOutput</span><span class="sxs-lookup"><span data-stu-id="c3d61-280">intOutput</span></span> | <span data-ttu-id="c3d61-281">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-281">Int</span></span> | <span data-ttu-id="c3d61-282">5</span><span class="sxs-lookup"><span data-stu-id="c3d61-282">5</span></span> |

<a id="mod" />

## <a name="mod"></a><span data-ttu-id="c3d61-283">Mod</span><span class="sxs-lookup"><span data-stu-id="c3d61-283">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="c3d61-284">Retourneert de rest van de deling van geheel getal met behulp van de twee opgegeven getallen.</span><span class="sxs-lookup"><span data-stu-id="c3d61-284">Returns the remainder of the integer division using the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c3d61-285">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3d61-285">Parameters</span></span>

| <span data-ttu-id="c3d61-286">Parameter</span><span class="sxs-lookup"><span data-stu-id="c3d61-286">Parameter</span></span> | <span data-ttu-id="c3d61-287">Vereist</span><span class="sxs-lookup"><span data-stu-id="c3d61-287">Required</span></span> | <span data-ttu-id="c3d61-288">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-288">Type</span></span> | <span data-ttu-id="c3d61-289">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c3d61-289">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c3d61-290">operand1</span><span class="sxs-lookup"><span data-stu-id="c3d61-290">operand1</span></span> |<span data-ttu-id="c3d61-291">Ja</span><span class="sxs-lookup"><span data-stu-id="c3d61-291">Yes</span></span> |<span data-ttu-id="c3d61-292">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-292">int</span></span> |<span data-ttu-id="c3d61-293">Het getal wordt verdeeld.</span><span class="sxs-lookup"><span data-stu-id="c3d61-293">The number being divided.</span></span> |
| <span data-ttu-id="c3d61-294">operand2</span><span class="sxs-lookup"><span data-stu-id="c3d61-294">operand2</span></span> |<span data-ttu-id="c3d61-295">Ja</span><span class="sxs-lookup"><span data-stu-id="c3d61-295">Yes</span></span> |<span data-ttu-id="c3d61-296">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-296">int</span></span> |<span data-ttu-id="c3d61-297">Het getal dat wordt gebruikt om te delen, mag niet 0 zijn.</span><span class="sxs-lookup"><span data-stu-id="c3d61-297">The number that is used to divide, Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c3d61-298">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-298">Return value</span></span>
<span data-ttu-id="c3d61-299">Een geheel getal dat de rest.</span><span class="sxs-lookup"><span data-stu-id="c3d61-299">An integer representing the remainder.</span></span>

### <a name="example"></a><span data-ttu-id="c3d61-300">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c3d61-300">Example</span></span>

<span data-ttu-id="c3d61-301">Het volgende voorbeeld retourneert het restgetal één parameter door een andere parameter.</span><span class="sxs-lookup"><span data-stu-id="c3d61-301">The following example returns the remainder of dividing one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used to divide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "modResult": {
            "type": "int",
            "value": "[mod(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="c3d61-302">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="c3d61-302">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c3d61-303">Naam</span><span class="sxs-lookup"><span data-stu-id="c3d61-303">Name</span></span> | <span data-ttu-id="c3d61-304">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-304">Type</span></span> | <span data-ttu-id="c3d61-305">Waarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-305">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c3d61-306">modResult</span><span class="sxs-lookup"><span data-stu-id="c3d61-306">modResult</span></span> | <span data-ttu-id="c3d61-307">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-307">Int</span></span> | <span data-ttu-id="c3d61-308">1</span><span class="sxs-lookup"><span data-stu-id="c3d61-308">1</span></span> |

<a id="mul" />

## <a name="mul"></a><span data-ttu-id="c3d61-309">mul</span><span class="sxs-lookup"><span data-stu-id="c3d61-309">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="c3d61-310">Retourneert de vermeerdering van de twee opgegeven getallen.</span><span class="sxs-lookup"><span data-stu-id="c3d61-310">Returns the multiplication of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c3d61-311">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3d61-311">Parameters</span></span>

| <span data-ttu-id="c3d61-312">Parameter</span><span class="sxs-lookup"><span data-stu-id="c3d61-312">Parameter</span></span> | <span data-ttu-id="c3d61-313">Vereist</span><span class="sxs-lookup"><span data-stu-id="c3d61-313">Required</span></span> | <span data-ttu-id="c3d61-314">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-314">Type</span></span> | <span data-ttu-id="c3d61-315">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c3d61-315">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c3d61-316">operand1</span><span class="sxs-lookup"><span data-stu-id="c3d61-316">operand1</span></span> |<span data-ttu-id="c3d61-317">Ja</span><span class="sxs-lookup"><span data-stu-id="c3d61-317">Yes</span></span> |<span data-ttu-id="c3d61-318">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-318">int</span></span> |<span data-ttu-id="c3d61-319">Eerste nummer wilt vermenigvuldigen.</span><span class="sxs-lookup"><span data-stu-id="c3d61-319">First number to multiply.</span></span> |
| <span data-ttu-id="c3d61-320">operand2</span><span class="sxs-lookup"><span data-stu-id="c3d61-320">operand2</span></span> |<span data-ttu-id="c3d61-321">Ja</span><span class="sxs-lookup"><span data-stu-id="c3d61-321">Yes</span></span> |<span data-ttu-id="c3d61-322">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-322">int</span></span> |<span data-ttu-id="c3d61-323">Tweede getal wilt vermenigvuldigen.</span><span class="sxs-lookup"><span data-stu-id="c3d61-323">Second number to multiply.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c3d61-324">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-324">Return value</span></span>

<span data-ttu-id="c3d61-325">Een geheel getal dat de vermenigvuldiging.</span><span class="sxs-lookup"><span data-stu-id="c3d61-325">An integer representing the multiplication.</span></span>

### <a name="example"></a><span data-ttu-id="c3d61-326">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c3d61-326">Example</span></span>

<span data-ttu-id="c3d61-327">Het volgende voorbeeld vermenigvuldigen één parameter door een andere parameter.</span><span class="sxs-lookup"><span data-stu-id="c3d61-327">The following example multiplies one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer to multiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer to multiply"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "mulResult": {
            "type": "int",
            "value": "[mul(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="c3d61-328">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="c3d61-328">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c3d61-329">Naam</span><span class="sxs-lookup"><span data-stu-id="c3d61-329">Name</span></span> | <span data-ttu-id="c3d61-330">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-330">Type</span></span> | <span data-ttu-id="c3d61-331">Waarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-331">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c3d61-332">mulResult</span><span class="sxs-lookup"><span data-stu-id="c3d61-332">mulResult</span></span> | <span data-ttu-id="c3d61-333">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-333">Int</span></span> | <span data-ttu-id="c3d61-334">15</span><span class="sxs-lookup"><span data-stu-id="c3d61-334">15</span></span> |

<a id="sub" />

## <a name="sub"></a><span data-ttu-id="c3d61-335">Sub</span><span class="sxs-lookup"><span data-stu-id="c3d61-335">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="c3d61-336">Retourneert de aftrekken van de twee opgegeven getallen.</span><span class="sxs-lookup"><span data-stu-id="c3d61-336">Returns the subtraction of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c3d61-337">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3d61-337">Parameters</span></span>

| <span data-ttu-id="c3d61-338">Parameter</span><span class="sxs-lookup"><span data-stu-id="c3d61-338">Parameter</span></span> | <span data-ttu-id="c3d61-339">Vereist</span><span class="sxs-lookup"><span data-stu-id="c3d61-339">Required</span></span> | <span data-ttu-id="c3d61-340">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-340">Type</span></span> | <span data-ttu-id="c3d61-341">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c3d61-341">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c3d61-342">operand1</span><span class="sxs-lookup"><span data-stu-id="c3d61-342">operand1</span></span> |<span data-ttu-id="c3d61-343">Ja</span><span class="sxs-lookup"><span data-stu-id="c3d61-343">Yes</span></span> |<span data-ttu-id="c3d61-344">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-344">int</span></span> |<span data-ttu-id="c3d61-345">Het nummer dat wordt afgetrokken van.</span><span class="sxs-lookup"><span data-stu-id="c3d61-345">The number that is subtracted from.</span></span> |
| <span data-ttu-id="c3d61-346">operand2</span><span class="sxs-lookup"><span data-stu-id="c3d61-346">operand2</span></span> |<span data-ttu-id="c3d61-347">Ja</span><span class="sxs-lookup"><span data-stu-id="c3d61-347">Yes</span></span> |<span data-ttu-id="c3d61-348">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-348">int</span></span> |<span data-ttu-id="c3d61-349">Het nummer dat wordt afgetrokken.</span><span class="sxs-lookup"><span data-stu-id="c3d61-349">The number that is subtracted.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c3d61-350">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-350">Return value</span></span>
<span data-ttu-id="c3d61-351">Een geheel getal dat de aftrekken.</span><span class="sxs-lookup"><span data-stu-id="c3d61-351">An integer representing the subtraction.</span></span>

### <a name="example"></a><span data-ttu-id="c3d61-352">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c3d61-352">Example</span></span>

<span data-ttu-id="c3d61-353">Het volgende voorbeeld wordt één parameter van een andere parameter afgetrokken.</span><span class="sxs-lookup"><span data-stu-id="c3d61-353">The following example subtracts one parameter from another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer subtracted from"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer to subtract"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "subResult": {
            "type": "int",
            "value": "[sub(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="c3d61-354">De uitvoer van het vorige voorbeeld met de standaardwaarde is:</span><span class="sxs-lookup"><span data-stu-id="c3d61-354">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c3d61-355">Naam</span><span class="sxs-lookup"><span data-stu-id="c3d61-355">Name</span></span> | <span data-ttu-id="c3d61-356">Type</span><span class="sxs-lookup"><span data-stu-id="c3d61-356">Type</span></span> | <span data-ttu-id="c3d61-357">Waarde</span><span class="sxs-lookup"><span data-stu-id="c3d61-357">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c3d61-358">subResult</span><span class="sxs-lookup"><span data-stu-id="c3d61-358">subResult</span></span> | <span data-ttu-id="c3d61-359">int</span><span class="sxs-lookup"><span data-stu-id="c3d61-359">Int</span></span> | <span data-ttu-id="c3d61-360">4</span><span class="sxs-lookup"><span data-stu-id="c3d61-360">4</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c3d61-361">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c3d61-361">Next steps</span></span>
* <span data-ttu-id="c3d61-362">Zie voor een beschrijving van de secties in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c3d61-362">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c3d61-363">U kunt meerdere sjablonen samenvoegen, Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c3d61-363">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="c3d61-364">Voor een opgegeven aantal keer herhalen bij het maken van een type resource, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="c3d61-364">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="c3d61-365">Zie voor het implementeren van de sjabloon die u hebt gemaakt, [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c3d61-365">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

