---
title: aaaAzure Resource Manager-sjabloonfuncties - numerieke | Microsoft Docs
description: Beschrijft Hallo functies toouse in een Azure Resource Manager-sjabloon toowork met getallen.
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
ms.openlocfilehash: 855d5b354d094b9815edc160e3d72efbfd36ba77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="05f18-103">Numerieke functies voor Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="05f18-103">Numeric functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="05f18-104">Resource Manager biedt Hallo functies voor het werken met gehele getallen te volgen:</span><span class="sxs-lookup"><span data-stu-id="05f18-104">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="05f18-105">toevoegen</span><span class="sxs-lookup"><span data-stu-id="05f18-105">add</span></span>](#add)
* [<span data-ttu-id="05f18-106">copyIndex</span><span class="sxs-lookup"><span data-stu-id="05f18-106">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="05f18-107">div</span><span class="sxs-lookup"><span data-stu-id="05f18-107">div</span></span>](#div)
* [<span data-ttu-id="05f18-108">Float</span><span class="sxs-lookup"><span data-stu-id="05f18-108">float</span></span>](#float)
* [<span data-ttu-id="05f18-109">int</span><span class="sxs-lookup"><span data-stu-id="05f18-109">int</span></span>](#int)
* [<span data-ttu-id="05f18-110">min</span><span class="sxs-lookup"><span data-stu-id="05f18-110">min</span></span>](#min)
* [<span data-ttu-id="05f18-111">maximale</span><span class="sxs-lookup"><span data-stu-id="05f18-111">max</span></span>](#max)
* [<span data-ttu-id="05f18-112">Mod</span><span class="sxs-lookup"><span data-stu-id="05f18-112">mod</span></span>](#mod)
* [<span data-ttu-id="05f18-113">mul</span><span class="sxs-lookup"><span data-stu-id="05f18-113">mul</span></span>](#mul)
* [<span data-ttu-id="05f18-114">Sub</span><span class="sxs-lookup"><span data-stu-id="05f18-114">sub</span></span>](#sub)

<a id="add" />

## <a name="add"></a><span data-ttu-id="05f18-115">toevoegen</span><span class="sxs-lookup"><span data-stu-id="05f18-115">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="05f18-116">Retourneert Hallo de som van de twee opgegeven getallen Hallo.</span><span class="sxs-lookup"><span data-stu-id="05f18-116">Returns hello sum of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="05f18-117">Parameters</span><span class="sxs-lookup"><span data-stu-id="05f18-117">Parameters</span></span>

| <span data-ttu-id="05f18-118">Parameter</span><span class="sxs-lookup"><span data-stu-id="05f18-118">Parameter</span></span> | <span data-ttu-id="05f18-119">Vereist</span><span class="sxs-lookup"><span data-stu-id="05f18-119">Required</span></span> | <span data-ttu-id="05f18-120">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-120">Type</span></span> | <span data-ttu-id="05f18-121">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="05f18-121">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="05f18-122">operand1</span><span class="sxs-lookup"><span data-stu-id="05f18-122">operand1</span></span> |<span data-ttu-id="05f18-123">Ja</span><span class="sxs-lookup"><span data-stu-id="05f18-123">Yes</span></span> |<span data-ttu-id="05f18-124">int</span><span class="sxs-lookup"><span data-stu-id="05f18-124">int</span></span> |<span data-ttu-id="05f18-125">Eerste nummer tooadd.</span><span class="sxs-lookup"><span data-stu-id="05f18-125">First number tooadd.</span></span> |
|<span data-ttu-id="05f18-126">operand2</span><span class="sxs-lookup"><span data-stu-id="05f18-126">operand2</span></span> |<span data-ttu-id="05f18-127">Ja</span><span class="sxs-lookup"><span data-stu-id="05f18-127">Yes</span></span> |<span data-ttu-id="05f18-128">int</span><span class="sxs-lookup"><span data-stu-id="05f18-128">int</span></span> |<span data-ttu-id="05f18-129">Het tweede nummer tooadd.</span><span class="sxs-lookup"><span data-stu-id="05f18-129">Second number tooadd.</span></span> |

### <a name="return-value"></a><span data-ttu-id="05f18-130">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="05f18-130">Return value</span></span>

<span data-ttu-id="05f18-131">Een geheel getal dat Hallo som van Hallo parameters bevat.</span><span class="sxs-lookup"><span data-stu-id="05f18-131">An integer that contains hello sum of hello parameters.</span></span>

### <a name="example"></a><span data-ttu-id="05f18-132">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="05f18-132">Example</span></span>

<span data-ttu-id="05f18-133">Hallo volgende voorbeeld voegt twee parameters.</span><span class="sxs-lookup"><span data-stu-id="05f18-133">hello following example adds two parameters.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer tooadd"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer tooadd"
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

<span data-ttu-id="05f18-134">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="05f18-134">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="05f18-135">Naam</span><span class="sxs-lookup"><span data-stu-id="05f18-135">Name</span></span> | <span data-ttu-id="05f18-136">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-136">Type</span></span> | <span data-ttu-id="05f18-137">Waarde</span><span class="sxs-lookup"><span data-stu-id="05f18-137">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="05f18-138">addResult</span><span class="sxs-lookup"><span data-stu-id="05f18-138">addResult</span></span> | <span data-ttu-id="05f18-139">int</span><span class="sxs-lookup"><span data-stu-id="05f18-139">Int</span></span> | <span data-ttu-id="05f18-140">8</span><span class="sxs-lookup"><span data-stu-id="05f18-140">8</span></span> |

<a id="copyindex" />

## <a name="copyindex"></a><span data-ttu-id="05f18-141">copyIndex</span><span class="sxs-lookup"><span data-stu-id="05f18-141">copyIndex</span></span>
`copyIndex(loopName, offset)`

<span data-ttu-id="05f18-142">Retourneert Hallo index van een lus herhaling.</span><span class="sxs-lookup"><span data-stu-id="05f18-142">Returns hello index of an iteration loop.</span></span> 

### <a name="parameters"></a><span data-ttu-id="05f18-143">Parameters</span><span class="sxs-lookup"><span data-stu-id="05f18-143">Parameters</span></span>

| <span data-ttu-id="05f18-144">Parameter</span><span class="sxs-lookup"><span data-stu-id="05f18-144">Parameter</span></span> | <span data-ttu-id="05f18-145">Vereist</span><span class="sxs-lookup"><span data-stu-id="05f18-145">Required</span></span> | <span data-ttu-id="05f18-146">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-146">Type</span></span> | <span data-ttu-id="05f18-147">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="05f18-147">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="05f18-148">loopName</span><span class="sxs-lookup"><span data-stu-id="05f18-148">loopName</span></span> | <span data-ttu-id="05f18-149">Nee</span><span class="sxs-lookup"><span data-stu-id="05f18-149">No</span></span> | <span data-ttu-id="05f18-150">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="05f18-150">string</span></span> | <span data-ttu-id="05f18-151">Hallo de naam van de lus Hallo voor het ophalen van Hallo herhaling.</span><span class="sxs-lookup"><span data-stu-id="05f18-151">hello name of hello loop for getting hello iteration.</span></span> |
| <span data-ttu-id="05f18-152">offset</span><span class="sxs-lookup"><span data-stu-id="05f18-152">offset</span></span> |<span data-ttu-id="05f18-153">Nee</span><span class="sxs-lookup"><span data-stu-id="05f18-153">No</span></span> |<span data-ttu-id="05f18-154">int</span><span class="sxs-lookup"><span data-stu-id="05f18-154">int</span></span> |<span data-ttu-id="05f18-155">Hallo tooadd toohello op nul gebaseerde herhaling getalwaarde.</span><span class="sxs-lookup"><span data-stu-id="05f18-155">hello number tooadd toohello zero-based iteration value.</span></span> |

### <a name="remarks"></a><span data-ttu-id="05f18-156">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="05f18-156">Remarks</span></span>

<span data-ttu-id="05f18-157">Deze functie wordt altijd gebruikt met een **kopie** object.</span><span class="sxs-lookup"><span data-stu-id="05f18-157">This function is always used with a **copy** object.</span></span> <span data-ttu-id="05f18-158">Als geen waarde is opgegeven voor **offset**, Hallo huidige herhaling waarde geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="05f18-158">If no value is provided for **offset**, hello current iteration value is returned.</span></span> <span data-ttu-id="05f18-159">Hallo herhaling waarde begint bij nul.</span><span class="sxs-lookup"><span data-stu-id="05f18-159">hello iteration value starts at zero.</span></span>

<span data-ttu-id="05f18-160">Hallo **loopName** eigenschap kunt u toospecify of copyIndex tooa resource herhaling of eigenschap iteratie verwijst.</span><span class="sxs-lookup"><span data-stu-id="05f18-160">hello **loopName** property enables you toospecify whether copyIndex is referring tooa resource iteration or property iteration.</span></span> <span data-ttu-id="05f18-161">Als geen waarde is opgegeven voor **loopName**, Hallo huidige resource type herhaling wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="05f18-161">If no value is provided for **loopName**, hello current resource type iteration is used.</span></span> <span data-ttu-id="05f18-162">Geef een waarde voor **loopName** wanneer voor een eigenschap.</span><span class="sxs-lookup"><span data-stu-id="05f18-162">Provide a value for **loopName** when iterating on a property.</span></span> 
 
<span data-ttu-id="05f18-163">Voor een volledige beschrijving van het gebruik van **copyIndex**, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="05f18-163">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

### <a name="example"></a><span data-ttu-id="05f18-164">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="05f18-164">Example</span></span>

<span data-ttu-id="05f18-165">Hallo volgende voorbeeld ziet u een kopie lus Hallo indexwaarde en opgenomen in het Hallo-naam.</span><span class="sxs-lookup"><span data-stu-id="05f18-165">hello following example shows a copy loop and hello index value included in hello name.</span></span> 

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

### <a name="return-value"></a><span data-ttu-id="05f18-166">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="05f18-166">Return value</span></span>

<span data-ttu-id="05f18-167">Een geheel getal dat Hallo huidige index van Hallo herhaling.</span><span class="sxs-lookup"><span data-stu-id="05f18-167">An integer representing hello current index of hello iteration.</span></span>

<a id="div" />

## <a name="div"></a><span data-ttu-id="05f18-168">div</span><span class="sxs-lookup"><span data-stu-id="05f18-168">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="05f18-169">Retourneert Hallo gehele getal van de twee opgegeven getallen Hallo.</span><span class="sxs-lookup"><span data-stu-id="05f18-169">Returns hello integer division of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="05f18-170">Parameters</span><span class="sxs-lookup"><span data-stu-id="05f18-170">Parameters</span></span>

| <span data-ttu-id="05f18-171">Parameter</span><span class="sxs-lookup"><span data-stu-id="05f18-171">Parameter</span></span> | <span data-ttu-id="05f18-172">Vereist</span><span class="sxs-lookup"><span data-stu-id="05f18-172">Required</span></span> | <span data-ttu-id="05f18-173">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-173">Type</span></span> | <span data-ttu-id="05f18-174">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="05f18-174">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="05f18-175">operand1</span><span class="sxs-lookup"><span data-stu-id="05f18-175">operand1</span></span> |<span data-ttu-id="05f18-176">Ja</span><span class="sxs-lookup"><span data-stu-id="05f18-176">Yes</span></span> |<span data-ttu-id="05f18-177">int</span><span class="sxs-lookup"><span data-stu-id="05f18-177">int</span></span> |<span data-ttu-id="05f18-178">Hallo-nummer wordt verdeeld.</span><span class="sxs-lookup"><span data-stu-id="05f18-178">hello number being divided.</span></span> |
| <span data-ttu-id="05f18-179">operand2</span><span class="sxs-lookup"><span data-stu-id="05f18-179">operand2</span></span> |<span data-ttu-id="05f18-180">Ja</span><span class="sxs-lookup"><span data-stu-id="05f18-180">Yes</span></span> |<span data-ttu-id="05f18-181">int</span><span class="sxs-lookup"><span data-stu-id="05f18-181">int</span></span> |<span data-ttu-id="05f18-182">Hallo-nummer dat is gebruikt toodivide.</span><span class="sxs-lookup"><span data-stu-id="05f18-182">hello number that is used toodivide.</span></span> <span data-ttu-id="05f18-183">Mag niet 0 zijn.</span><span class="sxs-lookup"><span data-stu-id="05f18-183">Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="05f18-184">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="05f18-184">Return value</span></span>

<span data-ttu-id="05f18-185">Deling van een geheel getal dat Hallo getal.</span><span class="sxs-lookup"><span data-stu-id="05f18-185">An integer representing hello division.</span></span>

### <a name="example"></a><span data-ttu-id="05f18-186">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="05f18-186">Example</span></span>

<span data-ttu-id="05f18-187">Hallo volgende voorbeeld wordt één parameter door een andere parameter verdeeld.</span><span class="sxs-lookup"><span data-stu-id="05f18-187">hello following example divides one parameter by another parameter.</span></span>

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
                "description": "Integer used toodivide"
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

<span data-ttu-id="05f18-188">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="05f18-188">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="05f18-189">Naam</span><span class="sxs-lookup"><span data-stu-id="05f18-189">Name</span></span> | <span data-ttu-id="05f18-190">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-190">Type</span></span> | <span data-ttu-id="05f18-191">Waarde</span><span class="sxs-lookup"><span data-stu-id="05f18-191">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="05f18-192">divResult</span><span class="sxs-lookup"><span data-stu-id="05f18-192">divResult</span></span> | <span data-ttu-id="05f18-193">int</span><span class="sxs-lookup"><span data-stu-id="05f18-193">Int</span></span> | <span data-ttu-id="05f18-194">2</span><span class="sxs-lookup"><span data-stu-id="05f18-194">2</span></span> |

<a id="float" />

## <a name="float"></a><span data-ttu-id="05f18-195">Float</span><span class="sxs-lookup"><span data-stu-id="05f18-195">float</span></span>
`float(arg1)`

<span data-ttu-id="05f18-196">Hallo waarde tooa Drijvendekommagetal converteert.</span><span class="sxs-lookup"><span data-stu-id="05f18-196">Converts hello value tooa floating point number.</span></span> <span data-ttu-id="05f18-197">U deze functie alleen gebruiken als aangepaste parameters doorgegeven tooan toepassing, zoals een logische App.</span><span class="sxs-lookup"><span data-stu-id="05f18-197">You only use this function when passing custom parameters tooan application, such as a Logic App.</span></span>

### <a name="parameters"></a><span data-ttu-id="05f18-198">Parameters</span><span class="sxs-lookup"><span data-stu-id="05f18-198">Parameters</span></span>

| <span data-ttu-id="05f18-199">Parameter</span><span class="sxs-lookup"><span data-stu-id="05f18-199">Parameter</span></span> | <span data-ttu-id="05f18-200">Vereist</span><span class="sxs-lookup"><span data-stu-id="05f18-200">Required</span></span> | <span data-ttu-id="05f18-201">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-201">Type</span></span> | <span data-ttu-id="05f18-202">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="05f18-202">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="05f18-203">Arg1</span><span class="sxs-lookup"><span data-stu-id="05f18-203">arg1</span></span> |<span data-ttu-id="05f18-204">Ja</span><span class="sxs-lookup"><span data-stu-id="05f18-204">Yes</span></span> |<span data-ttu-id="05f18-205">String of int.</span><span class="sxs-lookup"><span data-stu-id="05f18-205">string or int</span></span> |<span data-ttu-id="05f18-206">Hallo waarde tooconvert tooa Drijvendekommagetal.</span><span class="sxs-lookup"><span data-stu-id="05f18-206">hello value tooconvert tooa floating point number.</span></span> |

### <a name="return-value"></a><span data-ttu-id="05f18-207">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="05f18-207">Return value</span></span>
<span data-ttu-id="05f18-208">Een drijvende komma.</span><span class="sxs-lookup"><span data-stu-id="05f18-208">A floating point number.</span></span>

### <a name="example"></a><span data-ttu-id="05f18-209">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="05f18-209">Example</span></span>

<span data-ttu-id="05f18-210">Hallo volgende voorbeeld ziet u hoe toouse float toopass parameters tooa logische App:</span><span class="sxs-lookup"><span data-stu-id="05f18-210">hello following example shows how toouse float toopass parameters tooa Logic App:</span></span>

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

## <a name="int"></a><span data-ttu-id="05f18-211">int</span><span class="sxs-lookup"><span data-stu-id="05f18-211">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="05f18-212">Converteert Hallo opgegeven waarde tooan geheel getal.</span><span class="sxs-lookup"><span data-stu-id="05f18-212">Converts hello specified value tooan integer.</span></span>

### <a name="parameters"></a><span data-ttu-id="05f18-213">Parameters</span><span class="sxs-lookup"><span data-stu-id="05f18-213">Parameters</span></span>

| <span data-ttu-id="05f18-214">Parameter</span><span class="sxs-lookup"><span data-stu-id="05f18-214">Parameter</span></span> | <span data-ttu-id="05f18-215">Vereist</span><span class="sxs-lookup"><span data-stu-id="05f18-215">Required</span></span> | <span data-ttu-id="05f18-216">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-216">Type</span></span> | <span data-ttu-id="05f18-217">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="05f18-217">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="05f18-218">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="05f18-218">valueToConvert</span></span> |<span data-ttu-id="05f18-219">Ja</span><span class="sxs-lookup"><span data-stu-id="05f18-219">Yes</span></span> |<span data-ttu-id="05f18-220">String of int.</span><span class="sxs-lookup"><span data-stu-id="05f18-220">string or int</span></span> |<span data-ttu-id="05f18-221">Hallo waarde tooconvert tooan geheel getal.</span><span class="sxs-lookup"><span data-stu-id="05f18-221">hello value tooconvert tooan integer.</span></span> |

### <a name="return-value"></a><span data-ttu-id="05f18-222">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="05f18-222">Return value</span></span>

<span data-ttu-id="05f18-223">Een geheel getal van Hallo geconverteerd-waarde.</span><span class="sxs-lookup"><span data-stu-id="05f18-223">An integer of hello converted value.</span></span>

### <a name="example"></a><span data-ttu-id="05f18-224">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="05f18-224">Example</span></span>

<span data-ttu-id="05f18-225">Hallo volgende voorbeeld wordt geconverteerd Hallo gebruiker opgegeven parameter waarde toointeger.</span><span class="sxs-lookup"><span data-stu-id="05f18-225">hello following example converts hello user-provided parameter value toointeger.</span></span>

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

<span data-ttu-id="05f18-226">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="05f18-226">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="05f18-227">Naam</span><span class="sxs-lookup"><span data-stu-id="05f18-227">Name</span></span> | <span data-ttu-id="05f18-228">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-228">Type</span></span> | <span data-ttu-id="05f18-229">Waarde</span><span class="sxs-lookup"><span data-stu-id="05f18-229">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="05f18-230">intResult</span><span class="sxs-lookup"><span data-stu-id="05f18-230">intResult</span></span> | <span data-ttu-id="05f18-231">int</span><span class="sxs-lookup"><span data-stu-id="05f18-231">Int</span></span> | <span data-ttu-id="05f18-232">4</span><span class="sxs-lookup"><span data-stu-id="05f18-232">4</span></span> |


<a id="min" />

## <a name="min"></a><span data-ttu-id="05f18-233">min.</span><span class="sxs-lookup"><span data-stu-id="05f18-233">min</span></span>
`min (arg1)`

<span data-ttu-id="05f18-234">Retourneert Hallo minimumwaarde van een matrix van gehele getallen of een door komma's gescheiden lijst met gehele getallen zijn.</span><span class="sxs-lookup"><span data-stu-id="05f18-234">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="05f18-235">Parameters</span><span class="sxs-lookup"><span data-stu-id="05f18-235">Parameters</span></span>

| <span data-ttu-id="05f18-236">Parameter</span><span class="sxs-lookup"><span data-stu-id="05f18-236">Parameter</span></span> | <span data-ttu-id="05f18-237">Vereist</span><span class="sxs-lookup"><span data-stu-id="05f18-237">Required</span></span> | <span data-ttu-id="05f18-238">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-238">Type</span></span> | <span data-ttu-id="05f18-239">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="05f18-239">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="05f18-240">Arg1</span><span class="sxs-lookup"><span data-stu-id="05f18-240">arg1</span></span> |<span data-ttu-id="05f18-241">Ja</span><span class="sxs-lookup"><span data-stu-id="05f18-241">Yes</span></span> |<span data-ttu-id="05f18-242">matrix van gehele getallen of door komma's gescheiden lijst met gehele getallen</span><span class="sxs-lookup"><span data-stu-id="05f18-242">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="05f18-243">Hallo verzameling tooget Hallo minimumwaarde.</span><span class="sxs-lookup"><span data-stu-id="05f18-243">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="05f18-244">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="05f18-244">Return value</span></span>

<span data-ttu-id="05f18-245">Een geheel getal dat minimumwaarde uit Hallo-verzameling.</span><span class="sxs-lookup"><span data-stu-id="05f18-245">An integer representing minimum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="05f18-246">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="05f18-246">Example</span></span>

<span data-ttu-id="05f18-247">Hallo volgende voorbeeld wordt getoond hoe toouse min met een matrix en een lijst met gehele getallen zijn:</span><span class="sxs-lookup"><span data-stu-id="05f18-247">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="05f18-248">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="05f18-248">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="05f18-249">Naam</span><span class="sxs-lookup"><span data-stu-id="05f18-249">Name</span></span> | <span data-ttu-id="05f18-250">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-250">Type</span></span> | <span data-ttu-id="05f18-251">Waarde</span><span class="sxs-lookup"><span data-stu-id="05f18-251">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="05f18-252">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="05f18-252">arrayOutput</span></span> | <span data-ttu-id="05f18-253">int</span><span class="sxs-lookup"><span data-stu-id="05f18-253">Int</span></span> | <span data-ttu-id="05f18-254">0</span><span class="sxs-lookup"><span data-stu-id="05f18-254">0</span></span> |
| <span data-ttu-id="05f18-255">intOutput</span><span class="sxs-lookup"><span data-stu-id="05f18-255">intOutput</span></span> | <span data-ttu-id="05f18-256">int</span><span class="sxs-lookup"><span data-stu-id="05f18-256">Int</span></span> | <span data-ttu-id="05f18-257">0</span><span class="sxs-lookup"><span data-stu-id="05f18-257">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="05f18-258">Maximum aantal</span><span class="sxs-lookup"><span data-stu-id="05f18-258">max</span></span>
`max (arg1)`

<span data-ttu-id="05f18-259">Retourneert Hallo de maximumwaarde van een matrix van gehele getallen of een door komma's gescheiden lijst met gehele getallen.</span><span class="sxs-lookup"><span data-stu-id="05f18-259">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="05f18-260">Parameters</span><span class="sxs-lookup"><span data-stu-id="05f18-260">Parameters</span></span>

| <span data-ttu-id="05f18-261">Parameter</span><span class="sxs-lookup"><span data-stu-id="05f18-261">Parameter</span></span> | <span data-ttu-id="05f18-262">Vereist</span><span class="sxs-lookup"><span data-stu-id="05f18-262">Required</span></span> | <span data-ttu-id="05f18-263">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-263">Type</span></span> | <span data-ttu-id="05f18-264">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="05f18-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="05f18-265">Arg1</span><span class="sxs-lookup"><span data-stu-id="05f18-265">arg1</span></span> |<span data-ttu-id="05f18-266">Ja</span><span class="sxs-lookup"><span data-stu-id="05f18-266">Yes</span></span> |<span data-ttu-id="05f18-267">matrix van gehele getallen of door komma's gescheiden lijst met gehele getallen</span><span class="sxs-lookup"><span data-stu-id="05f18-267">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="05f18-268">Hallo verzameling tooget Hallo maximale waarde.</span><span class="sxs-lookup"><span data-stu-id="05f18-268">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="05f18-269">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="05f18-269">Return value</span></span>

<span data-ttu-id="05f18-270">Een geheel getal dat de maximale waarde Hallo uit Hallo-verzameling.</span><span class="sxs-lookup"><span data-stu-id="05f18-270">An integer representing hello maximum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="05f18-271">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="05f18-271">Example</span></span>

<span data-ttu-id="05f18-272">Hallo volgende voorbeeld wordt getoond hoe toouse max met een matrix en een lijst met gehele getallen zijn:</span><span class="sxs-lookup"><span data-stu-id="05f18-272">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="05f18-273">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="05f18-273">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="05f18-274">Naam</span><span class="sxs-lookup"><span data-stu-id="05f18-274">Name</span></span> | <span data-ttu-id="05f18-275">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-275">Type</span></span> | <span data-ttu-id="05f18-276">Waarde</span><span class="sxs-lookup"><span data-stu-id="05f18-276">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="05f18-277">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="05f18-277">arrayOutput</span></span> | <span data-ttu-id="05f18-278">int</span><span class="sxs-lookup"><span data-stu-id="05f18-278">Int</span></span> | <span data-ttu-id="05f18-279">5</span><span class="sxs-lookup"><span data-stu-id="05f18-279">5</span></span> |
| <span data-ttu-id="05f18-280">intOutput</span><span class="sxs-lookup"><span data-stu-id="05f18-280">intOutput</span></span> | <span data-ttu-id="05f18-281">int</span><span class="sxs-lookup"><span data-stu-id="05f18-281">Int</span></span> | <span data-ttu-id="05f18-282">5</span><span class="sxs-lookup"><span data-stu-id="05f18-282">5</span></span> |

<a id="mod" />

## <a name="mod"></a><span data-ttu-id="05f18-283">Mod</span><span class="sxs-lookup"><span data-stu-id="05f18-283">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="05f18-284">Hallo rest van de deling van Hallo geheel getal met behulp van twee opgegeven getallen Hallo retourneert.</span><span class="sxs-lookup"><span data-stu-id="05f18-284">Returns hello remainder of hello integer division using hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="05f18-285">Parameters</span><span class="sxs-lookup"><span data-stu-id="05f18-285">Parameters</span></span>

| <span data-ttu-id="05f18-286">Parameter</span><span class="sxs-lookup"><span data-stu-id="05f18-286">Parameter</span></span> | <span data-ttu-id="05f18-287">Vereist</span><span class="sxs-lookup"><span data-stu-id="05f18-287">Required</span></span> | <span data-ttu-id="05f18-288">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-288">Type</span></span> | <span data-ttu-id="05f18-289">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="05f18-289">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="05f18-290">operand1</span><span class="sxs-lookup"><span data-stu-id="05f18-290">operand1</span></span> |<span data-ttu-id="05f18-291">Ja</span><span class="sxs-lookup"><span data-stu-id="05f18-291">Yes</span></span> |<span data-ttu-id="05f18-292">int</span><span class="sxs-lookup"><span data-stu-id="05f18-292">int</span></span> |<span data-ttu-id="05f18-293">Hallo-nummer wordt verdeeld.</span><span class="sxs-lookup"><span data-stu-id="05f18-293">hello number being divided.</span></span> |
| <span data-ttu-id="05f18-294">operand2</span><span class="sxs-lookup"><span data-stu-id="05f18-294">operand2</span></span> |<span data-ttu-id="05f18-295">Ja</span><span class="sxs-lookup"><span data-stu-id="05f18-295">Yes</span></span> |<span data-ttu-id="05f18-296">int</span><span class="sxs-lookup"><span data-stu-id="05f18-296">int</span></span> |<span data-ttu-id="05f18-297">Hallo-nummer dat is gebruikt toodivide mag niet 0 zijn.</span><span class="sxs-lookup"><span data-stu-id="05f18-297">hello number that is used toodivide, Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="05f18-298">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="05f18-298">Return value</span></span>
<span data-ttu-id="05f18-299">Een geheel getal dat Hallo resterende hoeveelheid.</span><span class="sxs-lookup"><span data-stu-id="05f18-299">An integer representing hello remainder.</span></span>

### <a name="example"></a><span data-ttu-id="05f18-300">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="05f18-300">Example</span></span>

<span data-ttu-id="05f18-301">Hallo retourneert volgende voorbeeld Hallo restgetal één parameter door een andere parameter.</span><span class="sxs-lookup"><span data-stu-id="05f18-301">hello following example returns hello remainder of dividing one parameter by another parameter.</span></span>

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
                "description": "Integer used toodivide"
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

<span data-ttu-id="05f18-302">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="05f18-302">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="05f18-303">Naam</span><span class="sxs-lookup"><span data-stu-id="05f18-303">Name</span></span> | <span data-ttu-id="05f18-304">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-304">Type</span></span> | <span data-ttu-id="05f18-305">Waarde</span><span class="sxs-lookup"><span data-stu-id="05f18-305">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="05f18-306">modResult</span><span class="sxs-lookup"><span data-stu-id="05f18-306">modResult</span></span> | <span data-ttu-id="05f18-307">int</span><span class="sxs-lookup"><span data-stu-id="05f18-307">Int</span></span> | <span data-ttu-id="05f18-308">1</span><span class="sxs-lookup"><span data-stu-id="05f18-308">1</span></span> |

<a id="mul" />

## <a name="mul"></a><span data-ttu-id="05f18-309">mul</span><span class="sxs-lookup"><span data-stu-id="05f18-309">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="05f18-310">Retourneert Hallo vermeerdering van Hallo twee opgegeven getallen.</span><span class="sxs-lookup"><span data-stu-id="05f18-310">Returns hello multiplication of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="05f18-311">Parameters</span><span class="sxs-lookup"><span data-stu-id="05f18-311">Parameters</span></span>

| <span data-ttu-id="05f18-312">Parameter</span><span class="sxs-lookup"><span data-stu-id="05f18-312">Parameter</span></span> | <span data-ttu-id="05f18-313">Vereist</span><span class="sxs-lookup"><span data-stu-id="05f18-313">Required</span></span> | <span data-ttu-id="05f18-314">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-314">Type</span></span> | <span data-ttu-id="05f18-315">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="05f18-315">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="05f18-316">operand1</span><span class="sxs-lookup"><span data-stu-id="05f18-316">operand1</span></span> |<span data-ttu-id="05f18-317">Ja</span><span class="sxs-lookup"><span data-stu-id="05f18-317">Yes</span></span> |<span data-ttu-id="05f18-318">int</span><span class="sxs-lookup"><span data-stu-id="05f18-318">int</span></span> |<span data-ttu-id="05f18-319">Eerste nummer toomultiply.</span><span class="sxs-lookup"><span data-stu-id="05f18-319">First number toomultiply.</span></span> |
| <span data-ttu-id="05f18-320">operand2</span><span class="sxs-lookup"><span data-stu-id="05f18-320">operand2</span></span> |<span data-ttu-id="05f18-321">Ja</span><span class="sxs-lookup"><span data-stu-id="05f18-321">Yes</span></span> |<span data-ttu-id="05f18-322">int</span><span class="sxs-lookup"><span data-stu-id="05f18-322">int</span></span> |<span data-ttu-id="05f18-323">Het tweede nummer toomultiply.</span><span class="sxs-lookup"><span data-stu-id="05f18-323">Second number toomultiply.</span></span> |

### <a name="return-value"></a><span data-ttu-id="05f18-324">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="05f18-324">Return value</span></span>

<span data-ttu-id="05f18-325">Een Hallo van geheel getal dat vermenigvuldigen.</span><span class="sxs-lookup"><span data-stu-id="05f18-325">An integer representing hello multiplication.</span></span>

### <a name="example"></a><span data-ttu-id="05f18-326">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="05f18-326">Example</span></span>

<span data-ttu-id="05f18-327">Hallo volgt vermenigvuldigen één parameter door een andere parameter.</span><span class="sxs-lookup"><span data-stu-id="05f18-327">hello following example multiplies one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer toomultiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer toomultiply"
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

<span data-ttu-id="05f18-328">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="05f18-328">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="05f18-329">Naam</span><span class="sxs-lookup"><span data-stu-id="05f18-329">Name</span></span> | <span data-ttu-id="05f18-330">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-330">Type</span></span> | <span data-ttu-id="05f18-331">Waarde</span><span class="sxs-lookup"><span data-stu-id="05f18-331">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="05f18-332">mulResult</span><span class="sxs-lookup"><span data-stu-id="05f18-332">mulResult</span></span> | <span data-ttu-id="05f18-333">int</span><span class="sxs-lookup"><span data-stu-id="05f18-333">Int</span></span> | <span data-ttu-id="05f18-334">15</span><span class="sxs-lookup"><span data-stu-id="05f18-334">15</span></span> |

<a id="sub" />

## <a name="sub"></a><span data-ttu-id="05f18-335">Sub</span><span class="sxs-lookup"><span data-stu-id="05f18-335">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="05f18-336">Retourneert Hallo aftrekken van Hallo twee opgegeven getallen.</span><span class="sxs-lookup"><span data-stu-id="05f18-336">Returns hello subtraction of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="05f18-337">Parameters</span><span class="sxs-lookup"><span data-stu-id="05f18-337">Parameters</span></span>

| <span data-ttu-id="05f18-338">Parameter</span><span class="sxs-lookup"><span data-stu-id="05f18-338">Parameter</span></span> | <span data-ttu-id="05f18-339">Vereist</span><span class="sxs-lookup"><span data-stu-id="05f18-339">Required</span></span> | <span data-ttu-id="05f18-340">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-340">Type</span></span> | <span data-ttu-id="05f18-341">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="05f18-341">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="05f18-342">operand1</span><span class="sxs-lookup"><span data-stu-id="05f18-342">operand1</span></span> |<span data-ttu-id="05f18-343">Ja</span><span class="sxs-lookup"><span data-stu-id="05f18-343">Yes</span></span> |<span data-ttu-id="05f18-344">int</span><span class="sxs-lookup"><span data-stu-id="05f18-344">int</span></span> |<span data-ttu-id="05f18-345">Hallo-nummer dat wordt afgetrokken van.</span><span class="sxs-lookup"><span data-stu-id="05f18-345">hello number that is subtracted from.</span></span> |
| <span data-ttu-id="05f18-346">operand2</span><span class="sxs-lookup"><span data-stu-id="05f18-346">operand2</span></span> |<span data-ttu-id="05f18-347">Ja</span><span class="sxs-lookup"><span data-stu-id="05f18-347">Yes</span></span> |<span data-ttu-id="05f18-348">int</span><span class="sxs-lookup"><span data-stu-id="05f18-348">int</span></span> |<span data-ttu-id="05f18-349">Hallo-nummer dat wordt afgetrokken.</span><span class="sxs-lookup"><span data-stu-id="05f18-349">hello number that is subtracted.</span></span> |

### <a name="return-value"></a><span data-ttu-id="05f18-350">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="05f18-350">Return value</span></span>
<span data-ttu-id="05f18-351">Een Hallo van geheel getal dat aftrekken.</span><span class="sxs-lookup"><span data-stu-id="05f18-351">An integer representing hello subtraction.</span></span>

### <a name="example"></a><span data-ttu-id="05f18-352">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="05f18-352">Example</span></span>

<span data-ttu-id="05f18-353">Hallo volgende voorbeeld wordt één parameter van een andere parameter afgetrokken.</span><span class="sxs-lookup"><span data-stu-id="05f18-353">hello following example subtracts one parameter from another parameter.</span></span>

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
                "description": "Integer toosubtract"
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

<span data-ttu-id="05f18-354">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="05f18-354">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="05f18-355">Naam</span><span class="sxs-lookup"><span data-stu-id="05f18-355">Name</span></span> | <span data-ttu-id="05f18-356">Type</span><span class="sxs-lookup"><span data-stu-id="05f18-356">Type</span></span> | <span data-ttu-id="05f18-357">Waarde</span><span class="sxs-lookup"><span data-stu-id="05f18-357">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="05f18-358">subResult</span><span class="sxs-lookup"><span data-stu-id="05f18-358">subResult</span></span> | <span data-ttu-id="05f18-359">int</span><span class="sxs-lookup"><span data-stu-id="05f18-359">Int</span></span> | <span data-ttu-id="05f18-360">4</span><span class="sxs-lookup"><span data-stu-id="05f18-360">4</span></span> |

## <a name="next-steps"></a><span data-ttu-id="05f18-361">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="05f18-361">Next steps</span></span>
* <span data-ttu-id="05f18-362">Zie voor een beschrijving van de secties Hallo in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="05f18-362">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="05f18-363">toomerge meerdere sjablonen Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="05f18-363">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="05f18-364">een opgegeven aantal keren tooiterate bij het maken van een type resource, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="05f18-364">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="05f18-365">toosee hoe toodeploy Hallo sjabloon die u hebt gemaakt, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="05f18-365">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

