---
title: aaaResource Manager-sjabloonfuncties | Microsoft Docs
description: Hallo functies toouse beschrijft een Azure Resource Manager sjabloon tooretrieve waarden, werken met tekenreeksen en cijfers en ophalen van informatie over de implementatie.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0644abe1-abaa-443d-820d-1966d7d26bfd
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: d1b2e68a33d75058f83d6972dadb33a6390d49b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-functions"></a><span data-ttu-id="2325a-103">Azure Resource Manager-sjabloonfuncties</span><span class="sxs-lookup"><span data-stu-id="2325a-103">Azure Resource Manager template functions</span></span>
<span data-ttu-id="2325a-104">Dit onderwerp beschrijft alle Hallo-functies die kunt u in een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2325a-104">This topic describes all hello functions you can use in an Azure Resource Manager template.</span></span>

<span data-ttu-id="2325a-105">U functies in uw sjablonen toevoegen door deze tekst tussen vierkante haken: `[` en `]`respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="2325a-105">You add functions in your templates by enclosing them within brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="2325a-106">Hallo-expressie wordt geëvalueerd tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="2325a-106">hello expression is evaluated during deployment.</span></span> <span data-ttu-id="2325a-107">Hoewel geschreven als een letterlijke tekenreeks, zijn Hallo resultaat van de evaluatie van Hallo expressie van een ander JSON-type, zoals een matrix, een object of een geheel getal.</span><span class="sxs-lookup"><span data-stu-id="2325a-107">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array, object, or integer.</span></span> <span data-ttu-id="2325a-108">Net zoals in JavaScript-functieaanroepen die zijn opgemaakt als `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="2325a-108">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="2325a-109">U verwijzen naar eigenschappen met behulp van Hallo punt en [index] operators.</span><span class="sxs-lookup"><span data-stu-id="2325a-109">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="2325a-110">Een sjabloonexpressie kan 24.576 tekens niet overschrijden.</span><span class="sxs-lookup"><span data-stu-id="2325a-110">A template expression cannot exceed 24,576 characters.</span></span>

<span data-ttu-id="2325a-111">Sjabloonfuncties en de bijbehorende parameters zijn niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="2325a-111">Template functions and their parameters are case-insensitive.</span></span> <span data-ttu-id="2325a-112">Bijvoorbeeld: Resource Manager wordt omgezet **variables('var1')** en **VARIABLES('VAR1')** zoals Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="2325a-112">For example, Resource Manager resolves **variables('var1')** and **VARIABLES('VAR1')** as hello same.</span></span> <span data-ttu-id="2325a-113">Wanneer geëvalueerd, tenzij de functie Hallo wijzigt uitdrukkelijk geval (zoals toUpper of toLower), Hallo functie behoudt Hallo hoofdlettergebruik.</span><span class="sxs-lookup"><span data-stu-id="2325a-113">When evaluated, unless hello function expressly modifies case (such as toUpper or toLower), hello function preserves hello case.</span></span> <span data-ttu-id="2325a-114">Bepaalde brontypen misschien case vereisten, ongeacht hoe functies worden geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="2325a-114">Certain resource types may have case requirements irrespective of how functions are evaluated.</span></span>

<a id="array" />
<a id="coalesce" />
<a id="concatarray" />
<a id="contains" />
<a id="createarray" />
<a id="empty" />
<a id="first" />
<a id="intersection" />
<a id="last" />
<a id="length" />
<a id="min" />
<a id="max" />
<a id="range" />
<a id="skip" />
<a id="take" />
<a id="union" />

## <a name="array-and-object-functions"></a><span data-ttu-id="2325a-115">Matrix en object-functies</span><span class="sxs-lookup"><span data-stu-id="2325a-115">Array and object functions</span></span>
<span data-ttu-id="2325a-116">Resource Manager biedt een aantal functies voor het werken met matrices en objecten.</span><span class="sxs-lookup"><span data-stu-id="2325a-116">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="2325a-117">matrix</span><span class="sxs-lookup"><span data-stu-id="2325a-117">array</span></span>](resource-group-template-functions-array.md#array)
* [<span data-ttu-id="2325a-118">coalesce</span><span class="sxs-lookup"><span data-stu-id="2325a-118">coalesce</span></span>](resource-group-template-functions-array.md#coalesce)
* [<span data-ttu-id="2325a-119">concat</span><span class="sxs-lookup"><span data-stu-id="2325a-119">concat</span></span>](resource-group-template-functions-array.md#concat)
* [<span data-ttu-id="2325a-120">bevat</span><span class="sxs-lookup"><span data-stu-id="2325a-120">contains</span></span>](resource-group-template-functions-array.md#contains)
* [<span data-ttu-id="2325a-121">createArray</span><span class="sxs-lookup"><span data-stu-id="2325a-121">createArray</span></span>](resource-group-template-functions-array.md#createarray)
* [<span data-ttu-id="2325a-122">leeg</span><span class="sxs-lookup"><span data-stu-id="2325a-122">empty</span></span>](resource-group-template-functions-array.md#empty)
* [<span data-ttu-id="2325a-123">eerste</span><span class="sxs-lookup"><span data-stu-id="2325a-123">first</span></span>](resource-group-template-functions-array.md#first)
* [<span data-ttu-id="2325a-124">snijpunt</span><span class="sxs-lookup"><span data-stu-id="2325a-124">intersection</span></span>](resource-group-template-functions-array.md#intersection)
* [<span data-ttu-id="2325a-125">JSON</span><span class="sxs-lookup"><span data-stu-id="2325a-125">json</span></span>](resource-group-template-functions-array.md#json)
* [<span data-ttu-id="2325a-126">laatste</span><span class="sxs-lookup"><span data-stu-id="2325a-126">last</span></span>](resource-group-template-functions-array.md#last)
* [<span data-ttu-id="2325a-127">lengte</span><span class="sxs-lookup"><span data-stu-id="2325a-127">length</span></span>](resource-group-template-functions-array.md#length)
* [<span data-ttu-id="2325a-128">min</span><span class="sxs-lookup"><span data-stu-id="2325a-128">min</span></span>](resource-group-template-functions-array.md#min)
* [<span data-ttu-id="2325a-129">maximale</span><span class="sxs-lookup"><span data-stu-id="2325a-129">max</span></span>](resource-group-template-functions-array.md#max)
* [<span data-ttu-id="2325a-130">bereik</span><span class="sxs-lookup"><span data-stu-id="2325a-130">range</span></span>](resource-group-template-functions-array.md#range)
* [<span data-ttu-id="2325a-131">overslaan</span><span class="sxs-lookup"><span data-stu-id="2325a-131">skip</span></span>](resource-group-template-functions-array.md#skip)
* [<span data-ttu-id="2325a-132">duren</span><span class="sxs-lookup"><span data-stu-id="2325a-132">take</span></span>](resource-group-template-functions-array.md#take)
* [<span data-ttu-id="2325a-133">Union</span><span class="sxs-lookup"><span data-stu-id="2325a-133">union</span></span>](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a><span data-ttu-id="2325a-134">Vergelijking van functies</span><span class="sxs-lookup"><span data-stu-id="2325a-134">Comparison functions</span></span>
<span data-ttu-id="2325a-135">Resource Manager biedt een aantal functies voor het maken van vergelijkingen in uw sjablonen.</span><span class="sxs-lookup"><span data-stu-id="2325a-135">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="2325a-136">is gelijk aan</span><span class="sxs-lookup"><span data-stu-id="2325a-136">equals</span></span>](resource-group-template-functions-comparison.md#equals)
* [<span data-ttu-id="2325a-137">minder</span><span class="sxs-lookup"><span data-stu-id="2325a-137">less</span></span>](resource-group-template-functions-comparison.md#less)
* [<span data-ttu-id="2325a-138">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="2325a-138">lessOrEquals</span></span>](resource-group-template-functions-comparison.md#lessorequals)
* [<span data-ttu-id="2325a-139">groter</span><span class="sxs-lookup"><span data-stu-id="2325a-139">greater</span></span>](resource-group-template-functions-comparison.md#greater)
* [<span data-ttu-id="2325a-140">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="2325a-140">greaterOrEquals</span></span>](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a><span data-ttu-id="2325a-141">Waarde van de implementaties</span><span class="sxs-lookup"><span data-stu-id="2325a-141">Deployment value functions</span></span>
<span data-ttu-id="2325a-142">Resource Manager biedt Hallo volgende fungeert voor het ophalen van waarden in de secties van de sjabloon Hallo en verwante toohello implementatie waarden:</span><span class="sxs-lookup"><span data-stu-id="2325a-142">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="2325a-143">implementatie</span><span class="sxs-lookup"><span data-stu-id="2325a-143">deployment</span></span>](resource-group-template-functions-deployment.md#deployment)
* [<span data-ttu-id="2325a-144">parameters</span><span class="sxs-lookup"><span data-stu-id="2325a-144">parameters</span></span>](resource-group-template-functions-deployment.md#parameters)
* [<span data-ttu-id="2325a-145">variabelen</span><span class="sxs-lookup"><span data-stu-id="2325a-145">variables</span></span>](resource-group-template-functions-deployment.md#variables)

<a id="add" />
<a id="copyindex" />
<a id="div" />
<a id="float" />
<a id="int" />
<a id="minint" />
<a id="maxint" />
<a id="mod" />
<a id="mul" />
<a id="sub" />

## <a name="logical-functions"></a><span data-ttu-id="2325a-146">Logische functies</span><span class="sxs-lookup"><span data-stu-id="2325a-146">Logical functions</span></span>
<span data-ttu-id="2325a-147">Resource Manager biedt de volgende functies voor het werken met logische voorwaarden Hallo:</span><span class="sxs-lookup"><span data-stu-id="2325a-147">Resource Manager provides hello following functions for working with logical conditions:</span></span>

* [<span data-ttu-id="2325a-148">en</span><span class="sxs-lookup"><span data-stu-id="2325a-148">and</span></span>](resource-group-template-functions-logical.md#and)
* [<span data-ttu-id="2325a-149">BOOL</span><span class="sxs-lookup"><span data-stu-id="2325a-149">bool</span></span>](resource-group-template-functions-logical.md#bool)
* [<span data-ttu-id="2325a-150">Als</span><span class="sxs-lookup"><span data-stu-id="2325a-150">if</span></span>](resource-group-template-functions-logical.md#if)
* [<span data-ttu-id="2325a-151">niet</span><span class="sxs-lookup"><span data-stu-id="2325a-151">not</span></span>](resource-group-template-functions-logical.md#not)
* [<span data-ttu-id="2325a-152">of</span><span class="sxs-lookup"><span data-stu-id="2325a-152">or</span></span>](resource-group-template-functions-logical.md#or)

## <a name="numeric-functions"></a><span data-ttu-id="2325a-153">Numerieke functies</span><span class="sxs-lookup"><span data-stu-id="2325a-153">Numeric functions</span></span>
<span data-ttu-id="2325a-154">Resource Manager biedt Hallo functies voor het werken met gehele getallen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2325a-154">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="2325a-155">toevoegen</span><span class="sxs-lookup"><span data-stu-id="2325a-155">add</span></span>](resource-group-template-functions-numeric.md#add)
* [<span data-ttu-id="2325a-156">copyIndex</span><span class="sxs-lookup"><span data-stu-id="2325a-156">copyIndex</span></span>](resource-group-template-functions-numeric.md#copyindex)
* [<span data-ttu-id="2325a-157">div</span><span class="sxs-lookup"><span data-stu-id="2325a-157">div</span></span>](resource-group-template-functions-numeric.md#div)
* [<span data-ttu-id="2325a-158">Float</span><span class="sxs-lookup"><span data-stu-id="2325a-158">float</span></span>](resource-group-template-functions-numeric.md#float)
* [<span data-ttu-id="2325a-159">int</span><span class="sxs-lookup"><span data-stu-id="2325a-159">int</span></span>](resource-group-template-functions-numeric.md#int)
* [<span data-ttu-id="2325a-160">min</span><span class="sxs-lookup"><span data-stu-id="2325a-160">min</span></span>](resource-group-template-functions-numeric.md#min)
* [<span data-ttu-id="2325a-161">maximale</span><span class="sxs-lookup"><span data-stu-id="2325a-161">max</span></span>](resource-group-template-functions-numeric.md#max)
* [<span data-ttu-id="2325a-162">Mod</span><span class="sxs-lookup"><span data-stu-id="2325a-162">mod</span></span>](resource-group-template-functions-numeric.md#mod)
* [<span data-ttu-id="2325a-163">mul</span><span class="sxs-lookup"><span data-stu-id="2325a-163">mul</span></span>](resource-group-template-functions-numeric.md#mul)
* [<span data-ttu-id="2325a-164">Sub</span><span class="sxs-lookup"><span data-stu-id="2325a-164">sub</span></span>](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a><span data-ttu-id="2325a-165">Resource-functies</span><span class="sxs-lookup"><span data-stu-id="2325a-165">Resource functions</span></span>
<span data-ttu-id="2325a-166">Resource Manager biedt Hallo functies voor het ophalen van waarden van de resource te volgen:</span><span class="sxs-lookup"><span data-stu-id="2325a-166">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="2325a-167">listKeys en de lijst {Value}</span><span class="sxs-lookup"><span data-stu-id="2325a-167">listKeys and list{Value}</span></span>](resource-group-template-functions-resource.md#listkeys)
* [<span data-ttu-id="2325a-168">providers</span><span class="sxs-lookup"><span data-stu-id="2325a-168">providers</span></span>](resource-group-template-functions-resource.md#providers)
* [<span data-ttu-id="2325a-169">verwijzing</span><span class="sxs-lookup"><span data-stu-id="2325a-169">reference</span></span>](resource-group-template-functions-resource.md#reference)
* [<span data-ttu-id="2325a-170">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="2325a-170">resourceGroup</span></span>](resource-group-template-functions-resource.md#resourcegroup)
* [<span data-ttu-id="2325a-171">resourceId</span><span class="sxs-lookup"><span data-stu-id="2325a-171">resourceId</span></span>](resource-group-template-functions-resource.md#resourceid)
* [<span data-ttu-id="2325a-172">abonnement</span><span class="sxs-lookup"><span data-stu-id="2325a-172">subscription</span></span>](resource-group-template-functions-resource.md#subscription)

<a id="base64" />
<a id="base64tojson" />
<a id="base64tostring" />
<a id="concat" />
<a id="containsstring" />
<a id="datauri" />
<a id="datauritostring" />
<a id="emptystring" />
<a id="endswith" />
<a id="firststring" />
<a id="indexof" />
<a id="laststring" />
<a id="lastindexof" />
<a id="lengthstring" />
<a id="padleft" />
<a id="replace" />
<a id="skipstring" />
<a id="split" />
<a id="startswith" />
<a id="string" />
<a id="substring" />
<a id="takestring" />
<a id="tolower" />
<a id="toupper" />
<a id="trim" />
<a id="uniquestring" />
<a id="uri" />
<a id="uricomponent" />
<a id="uricomponenttostring" />

## <a name="string-functions"></a><span data-ttu-id="2325a-173">Tekenreeks-functies</span><span class="sxs-lookup"><span data-stu-id="2325a-173">String functions</span></span>
<span data-ttu-id="2325a-174">Resource Manager biedt Hallo functies voor het werken met tekenreeksen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2325a-174">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="2325a-175">Base64</span><span class="sxs-lookup"><span data-stu-id="2325a-175">base64</span></span>](resource-group-template-functions-string.md#base64)
* [<span data-ttu-id="2325a-176">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="2325a-176">base64ToJson</span></span>](resource-group-template-functions-string.md#base64tojson)
* [<span data-ttu-id="2325a-177">base64ToString</span><span class="sxs-lookup"><span data-stu-id="2325a-177">base64ToString</span></span>](resource-group-template-functions-string.md#base64tostring)
* [<span data-ttu-id="2325a-178">concat</span><span class="sxs-lookup"><span data-stu-id="2325a-178">concat</span></span>](resource-group-template-functions-string.md#concat)
* [<span data-ttu-id="2325a-179">bevat</span><span class="sxs-lookup"><span data-stu-id="2325a-179">contains</span></span>](resource-group-template-functions-string.md#contains)
* [<span data-ttu-id="2325a-180">dataUri</span><span class="sxs-lookup"><span data-stu-id="2325a-180">dataUri</span></span>](resource-group-template-functions-string.md#datauri)
* [<span data-ttu-id="2325a-181">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="2325a-181">dataUriToString</span></span>](resource-group-template-functions-string.md#datauritostring)
* [<span data-ttu-id="2325a-182">leeg</span><span class="sxs-lookup"><span data-stu-id="2325a-182">empty</span></span>](resource-group-template-functions-string.md#empty)
* [<span data-ttu-id="2325a-183">endsWith</span><span class="sxs-lookup"><span data-stu-id="2325a-183">endsWith</span></span>](resource-group-template-functions-string.md#endswith)
* [<span data-ttu-id="2325a-184">eerste</span><span class="sxs-lookup"><span data-stu-id="2325a-184">first</span></span>](resource-group-template-functions-string.md#first)
* [<span data-ttu-id="2325a-185">indexOf</span><span class="sxs-lookup"><span data-stu-id="2325a-185">indexOf</span></span>](resource-group-template-functions-string.md#indexof)
* [<span data-ttu-id="2325a-186">laatste</span><span class="sxs-lookup"><span data-stu-id="2325a-186">last</span></span>](resource-group-template-functions-string.md#last)
* [<span data-ttu-id="2325a-187">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="2325a-187">lastIndexOf</span></span>](resource-group-template-functions-string.md#lastindexof)
* [<span data-ttu-id="2325a-188">lengte</span><span class="sxs-lookup"><span data-stu-id="2325a-188">length</span></span>](resource-group-template-functions-string.md#length)
* [<span data-ttu-id="2325a-189">padLeft</span><span class="sxs-lookup"><span data-stu-id="2325a-189">padLeft</span></span>](resource-group-template-functions-string.md#padleft)
* [<span data-ttu-id="2325a-190">vervangen</span><span class="sxs-lookup"><span data-stu-id="2325a-190">replace</span></span>](resource-group-template-functions-string.md#replace)
* [<span data-ttu-id="2325a-191">overslaan</span><span class="sxs-lookup"><span data-stu-id="2325a-191">skip</span></span>](resource-group-template-functions-string.md#skip)
* [<span data-ttu-id="2325a-192">split</span><span class="sxs-lookup"><span data-stu-id="2325a-192">split</span></span>](resource-group-template-functions-string.md#split)
* [<span data-ttu-id="2325a-193">startsWith</span><span class="sxs-lookup"><span data-stu-id="2325a-193">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="2325a-194">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="2325a-194">string</span></span>](resource-group-template-functions-string.md#string)
* [<span data-ttu-id="2325a-195">de subtekenreeks</span><span class="sxs-lookup"><span data-stu-id="2325a-195">substring</span></span>](resource-group-template-functions-string.md#substring)
* [<span data-ttu-id="2325a-196">duren</span><span class="sxs-lookup"><span data-stu-id="2325a-196">take</span></span>](resource-group-template-functions-string.md#take)
* [<span data-ttu-id="2325a-197">toLower</span><span class="sxs-lookup"><span data-stu-id="2325a-197">toLower</span></span>](resource-group-template-functions-string.md#tolower)
* [<span data-ttu-id="2325a-198">toUpper</span><span class="sxs-lookup"><span data-stu-id="2325a-198">toUpper</span></span>](resource-group-template-functions-string.md#toupper)
* [<span data-ttu-id="2325a-199">Trim</span><span class="sxs-lookup"><span data-stu-id="2325a-199">trim</span></span>](resource-group-template-functions-string.md#trim)
* [<span data-ttu-id="2325a-200">uniqueString</span><span class="sxs-lookup"><span data-stu-id="2325a-200">uniqueString</span></span>](resource-group-template-functions-string.md#uniquestring)
* [<span data-ttu-id="2325a-201">URI</span><span class="sxs-lookup"><span data-stu-id="2325a-201">uri</span></span>](resource-group-template-functions-string.md#uri)
* [<span data-ttu-id="2325a-202">uriComponent</span><span class="sxs-lookup"><span data-stu-id="2325a-202">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="2325a-203">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="2325a-203">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a><span data-ttu-id="2325a-204">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2325a-204">Next steps</span></span>
* <span data-ttu-id="2325a-205">Zie voor een beschrijving van de secties Hallo in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="2325a-205">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="2325a-206">toomerge meerdere sjablonen Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md)</span><span class="sxs-lookup"><span data-stu-id="2325a-206">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md)</span></span>
* <span data-ttu-id="2325a-207">een opgegeven aantal keren tooiterate bij het maken van een type resource, Zie [meerdere exemplaren van resources in Azure Resource Manager maken](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="2325a-207">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>
* <span data-ttu-id="2325a-208">toosee hoe toodeploy Hallo sjabloon die u hebt gemaakt, raadpleegt [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="2325a-208">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)</span></span>

