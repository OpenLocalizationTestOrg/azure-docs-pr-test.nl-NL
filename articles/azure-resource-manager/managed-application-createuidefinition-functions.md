---
title: UI-definitie functies maken voor aaaAzure beheerde toepassingen | Microsoft Docs
description: Hierin wordt beschreven Hallo functies toouse tijdens het construeren van UI-definities voor beheerde Azure-toepassingen
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 7a311a25404ccaec8c19c3ed8cd7038f6887c013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-functions"></a><span data-ttu-id="d53b6-103">CreateUiDefinition functies</span><span class="sxs-lookup"><span data-stu-id="d53b6-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="d53b6-104">Deze sectie bevat Hallo handtekeningen voor alle ondersteunde functies van een CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="d53b6-104">This section contains hello signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="d53b6-105">toouse een functie rond Hallo declaratie vierkante haken.</span><span class="sxs-lookup"><span data-stu-id="d53b6-105">toouse a function, surround hello declaration with square brackets.</span></span> <span data-ttu-id="d53b6-106">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d53b6-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="d53b6-107">Tekenreeksen en andere functies kunnen worden verwezen als parameters voor een functie, maar tekenreeksen moeten tussen enkele aanhalingstekens worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="d53b6-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="d53b6-108">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d53b6-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="d53b6-109">Indien van toepassing, kunt u de eigenschappen van het Hallo-uitvoer van een functie met behulp van Hallo bewerkingsteken raadplegen.</span><span class="sxs-lookup"><span data-stu-id="d53b6-109">Where applicable, you can reference properties of hello output of a function by using hello dot operator.</span></span> <span data-ttu-id="d53b6-110">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d53b6-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="d53b6-111">Functies die verwijzen naar</span><span class="sxs-lookup"><span data-stu-id="d53b6-111">Referencing functions</span></span>
<span data-ttu-id="d53b6-112">Deze functies kunnen worden gebruikt tooreference uitvoer van Hallo eigenschappen of context van een CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="d53b6-112">These functions can be used tooreference outputs from hello properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="d53b6-113">basisbeginselen</span><span class="sxs-lookup"><span data-stu-id="d53b6-113">basics</span></span>
<span data-ttu-id="d53b6-114">Hallo uitvoerwaarden van een element dat is gedefinieerd in Hallo basisbeginselen stap retourneert.</span><span class="sxs-lookup"><span data-stu-id="d53b6-114">Returns hello output values of an element that is defined in hello Basics step.</span></span>

<span data-ttu-id="d53b6-115">Hallo volgende voorbeeld wordt de uitvoer Hallo van Hallo-element met de naam `foo` in Hallo basisbeginselen stap:</span><span class="sxs-lookup"><span data-stu-id="d53b6-115">hello following example returns hello output of hello element named `foo` in hello Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="d53b6-116">Stappen</span><span class="sxs-lookup"><span data-stu-id="d53b6-116">steps</span></span>
<span data-ttu-id="d53b6-117">Hallo uitvoerwaarden van een element dat is gedefinieerd in de opgegeven stap Hallo retourneert.</span><span class="sxs-lookup"><span data-stu-id="d53b6-117">Returns hello output values of an element that is defined in hello specified step.</span></span> <span data-ttu-id="d53b6-118">tooget hello uitvoerwaarden van elementen in Hallo basisbeginselen stap gebruiken `basics()` in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="d53b6-118">tooget hello output values of elements in hello Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="d53b6-119">Hallo volgende voorbeeld wordt de uitvoer Hallo van Hallo-element met de naam `bar` in Hallo stap met de naam `foo`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-119">hello following example returns hello output of hello element named `bar` in hello step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="d53b6-120">location</span><span class="sxs-lookup"><span data-stu-id="d53b6-120">location</span></span>
<span data-ttu-id="d53b6-121">Retourneert Hallo locatie in Hallo basisbeginselen stap of de huidige context Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="d53b6-121">Returns hello location selected in hello Basics step or hello current context.</span></span>

<span data-ttu-id="d53b6-122">Hallo volgende voorbeeld kan retourneren `"westus"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-122">hello following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="d53b6-123">Tekenreeks-functies</span><span class="sxs-lookup"><span data-stu-id="d53b6-123">String functions</span></span>
<span data-ttu-id="d53b6-124">Deze functies kunnen alleen worden gebruikt met een JSON-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="d53b6-125">concat</span><span class="sxs-lookup"><span data-stu-id="d53b6-125">concat</span></span>
<span data-ttu-id="d53b6-126">Een of meer reeksen aaneengeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d53b6-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="d53b6-127">Bijvoorbeeld, als Hallo uitvoer de waarde van `element1` als `"bar"`, en vervolgens in dit voorbeeld Hallo tekenreeks retourneert `"foobar!"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-127">For example, if hello output value of `element1` if `"bar"`, then this example returns hello string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="d53b6-128">de subtekenreeks</span><span class="sxs-lookup"><span data-stu-id="d53b6-128">substring</span></span>
<span data-ttu-id="d53b6-129">Retourneert de subtekenreeks Hallo Hallo opgegeven tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-129">Returns hello substring of hello specified string.</span></span> <span data-ttu-id="d53b6-130">Hallo subtekenreeks wordt gestart op de opgegeven index Hallo en heeft Hallo opgegeven lengte.</span><span class="sxs-lookup"><span data-stu-id="d53b6-130">hello substring starts at hello specified index and has hello specified length.</span></span>

<span data-ttu-id="d53b6-131">Hallo volgende voorbeeld retourneert `"ftw"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-131">hello following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="d53b6-132">vervangen</span><span class="sxs-lookup"><span data-stu-id="d53b6-132">replace</span></span>
<span data-ttu-id="d53b6-133">Retourneert een tekenreeks in welke alle instanties van Hallo tekenreeks in de huidige tekenreeks Hallo opgegeven worden vervangen door een andere tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-133">Returns a string in which all occurrences of hello specified string in hello current string are replaced with another string.</span></span>

<span data-ttu-id="d53b6-134">Hallo volgende voorbeeld retourneert `"Everything is awesome!"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-134">hello following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="d53b6-135">GUID</span><span class="sxs-lookup"><span data-stu-id="d53b6-135">guid</span></span>
<span data-ttu-id="d53b6-136">Genereert een globally unique identifier (GUID)-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="d53b6-137">Hallo volgende voorbeeld kan retourneren `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-137">hello following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="d53b6-138">toLower</span><span class="sxs-lookup"><span data-stu-id="d53b6-138">toLower</span></span>
<span data-ttu-id="d53b6-139">Retourneert een tekenreeks die is omgezet toolowercase.</span><span class="sxs-lookup"><span data-stu-id="d53b6-139">Returns a string converted toolowercase.</span></span>

<span data-ttu-id="d53b6-140">Hallo volgende voorbeeld retourneert `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-140">hello following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="d53b6-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="d53b6-141">toUpper</span></span>
<span data-ttu-id="d53b6-142">Retourneert een tekenreeks die is omgezet toouppercase.</span><span class="sxs-lookup"><span data-stu-id="d53b6-142">Returns a string converted toouppercase.</span></span>

<span data-ttu-id="d53b6-143">Hallo volgende voorbeeld retourneert `"FOOBAR"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-143">hello following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="d53b6-144">Functies van de verzameling</span><span class="sxs-lookup"><span data-stu-id="d53b6-144">Collection functions</span></span>
<span data-ttu-id="d53b6-145">Deze functies kunnen worden gebruikt met verzamelingen, zoals JSON tekenreeksen, matrices en objecten.</span><span class="sxs-lookup"><span data-stu-id="d53b6-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="d53b6-146">Bevat</span><span class="sxs-lookup"><span data-stu-id="d53b6-146">contains</span></span>
<span data-ttu-id="d53b6-147">Retourneert `true` als een tekenreeks bevat Hallo opgegeven subtekenreeks, bevat een matrix Hallo opgegeven waarde of een object opgegeven Hallo-sleutel bevat.</span><span class="sxs-lookup"><span data-stu-id="d53b6-147">Returns `true` if a string contains hello specified substring, an array contains hello specified value, or an object contains hello specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="d53b6-148">Voorbeeld 1: tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d53b6-148">Example 1: string</span></span>
<span data-ttu-id="d53b6-149">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-149">hello following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="d53b6-150">Voorbeeld 2: matrix</span><span class="sxs-lookup"><span data-stu-id="d53b6-150">Example 2: array</span></span>
<span data-ttu-id="d53b6-151">Stel `element1` retourneert `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="d53b6-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="d53b6-152">Hallo volgende voorbeeld retourneert `false`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-152">hello following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="d53b6-153">Voorbeeld 3: object</span><span class="sxs-lookup"><span data-stu-id="d53b6-153">Example 3: object</span></span>
<span data-ttu-id="d53b6-154">Stel `element1` geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="d53b6-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="d53b6-155">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-155">hello following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="d53b6-156">lengte</span><span class="sxs-lookup"><span data-stu-id="d53b6-156">length</span></span>
<span data-ttu-id="d53b6-157">Retourneert het aantal tekens Hallo in een tekenreeks, Hallo aantal waarden in een matrix of Hallo aantal sleutels in een object.</span><span class="sxs-lookup"><span data-stu-id="d53b6-157">Returns hello number of characters in a string, hello number of values in an array, or hello number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="d53b6-158">Voorbeeld 1: tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d53b6-158">Example 1: string</span></span>
<span data-ttu-id="d53b6-159">Hallo volgende voorbeeld retourneert `6`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-159">hello following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="d53b6-160">Voorbeeld 2: matrix</span><span class="sxs-lookup"><span data-stu-id="d53b6-160">Example 2: array</span></span>
<span data-ttu-id="d53b6-161">Stel `element1` retourneert `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="d53b6-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="d53b6-162">Hallo volgende voorbeeld retourneert `3`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-162">hello following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="d53b6-163">Voorbeeld 3: object</span><span class="sxs-lookup"><span data-stu-id="d53b6-163">Example 3: object</span></span>
<span data-ttu-id="d53b6-164">Stel `element1` geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="d53b6-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="d53b6-165">Hallo volgende voorbeeld retourneert `2`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-165">hello following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="d53b6-166">leeg</span><span class="sxs-lookup"><span data-stu-id="d53b6-166">empty</span></span>
<span data-ttu-id="d53b6-167">Retourneert `true` als Hallo tekenreekswaarde, een matrix of object null of leeg is.</span><span class="sxs-lookup"><span data-stu-id="d53b6-167">Returns `true` if hello string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="d53b6-168">Voorbeeld 1: tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d53b6-168">Example 1: string</span></span>
<span data-ttu-id="d53b6-169">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-169">hello following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="d53b6-170">Voorbeeld 2: matrix</span><span class="sxs-lookup"><span data-stu-id="d53b6-170">Example 2: array</span></span>
<span data-ttu-id="d53b6-171">Stel `element1` retourneert `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="d53b6-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="d53b6-172">Hallo volgende voorbeeld retourneert `false`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-172">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="d53b6-173">Voorbeeld 3: object</span><span class="sxs-lookup"><span data-stu-id="d53b6-173">Example 3: object</span></span>
<span data-ttu-id="d53b6-174">Stel `element1` geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="d53b6-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="d53b6-175">Hallo volgende voorbeeld retourneert `false`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-175">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="d53b6-176">Voorbeeld 4: null zijn en niet-gedefinieerde</span><span class="sxs-lookup"><span data-stu-id="d53b6-176">Example 4: null and undefined</span></span>
<span data-ttu-id="d53b6-177">Stel `element1` is `null` of niet-gedefinieerde.</span><span class="sxs-lookup"><span data-stu-id="d53b6-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="d53b6-178">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-178">hello following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="d53b6-179">eerste</span><span class="sxs-lookup"><span data-stu-id="d53b6-179">first</span></span>
<span data-ttu-id="d53b6-180">Retourneert Hallo eerste teken van Hallo opgegeven tekenreeks; eerste waarde van de opgegeven matrix Hallo; of de eerste sleutel en waarde van het opgegeven object Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="d53b6-180">Returns hello first character of hello specified string; first value of hello specified array; or hello first key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="d53b6-181">Voorbeeld 1: tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d53b6-181">Example 1: string</span></span>
<span data-ttu-id="d53b6-182">Hallo volgende voorbeeld retourneert `"f"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-182">hello following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="d53b6-183">Voorbeeld 2: matrix</span><span class="sxs-lookup"><span data-stu-id="d53b6-183">Example 2: array</span></span>
<span data-ttu-id="d53b6-184">Stel `element1` retourneert `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="d53b6-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="d53b6-185">Hallo volgende voorbeeld retourneert `1`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-185">hello following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="d53b6-186">Voorbeeld 3: object</span><span class="sxs-lookup"><span data-stu-id="d53b6-186">Example 3: object</span></span>
<span data-ttu-id="d53b6-187">Stel `element1` geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="d53b6-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="d53b6-188">Hallo volgende voorbeeld retourneert `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-188">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="d53b6-189">laatste</span><span class="sxs-lookup"><span data-stu-id="d53b6-189">last</span></span>
<span data-ttu-id="d53b6-190">Retourneert Hallo laatste teken van Hallo opgegeven verbindingsreeks, Hallo laatste waarde van de opgegeven matrix hello, of laatste sleutel en waarde van het opgegeven object Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="d53b6-190">Returns hello last character of hello specified string, hello last value of hello specified array, or hello last key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="d53b6-191">Voorbeeld 1: tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d53b6-191">Example 1: string</span></span>
<span data-ttu-id="d53b6-192">Hallo volgende voorbeeld retourneert `"r"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-192">hello following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="d53b6-193">Voorbeeld 2: matrix</span><span class="sxs-lookup"><span data-stu-id="d53b6-193">Example 2: array</span></span>
<span data-ttu-id="d53b6-194">Stel `element1` retourneert `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="d53b6-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="d53b6-195">Hallo volgende voorbeeld retourneert `2`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-195">hello following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="d53b6-196">Voorbeeld 3: object</span><span class="sxs-lookup"><span data-stu-id="d53b6-196">Example 3: object</span></span>
<span data-ttu-id="d53b6-197">Stel `element1` geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="d53b6-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="d53b6-198">Hallo volgende voorbeeld retourneert `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-198">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="d53b6-199">duren</span><span class="sxs-lookup"><span data-stu-id="d53b6-199">take</span></span>
<span data-ttu-id="d53b6-200">Retourneert een opgegeven aantal aaneengesloten tekens vanaf het begin van Hallo tekenreeks hello, een opgegeven aantal opeenvolgende waarden vanaf het begin van de matrix Hallo hello of een opgegeven aantal aaneengesloten sleutels en waarden van Hallo Hallo-object is gestart.</span><span class="sxs-lookup"><span data-stu-id="d53b6-200">Returns a specified number of contiguous characters from hello start of hello string, a specified number of contiguous values from hello start of hello array, or a specified number of contiguous keys and values from hello start of hello object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="d53b6-201">Voorbeeld 1: tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d53b6-201">Example 1: string</span></span>
<span data-ttu-id="d53b6-202">Hallo volgende voorbeeld retourneert `"foo"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-202">hello following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="d53b6-203">Voorbeeld 2: matrix</span><span class="sxs-lookup"><span data-stu-id="d53b6-203">Example 2: array</span></span>
<span data-ttu-id="d53b6-204">Stel `element1` retourneert `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="d53b6-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="d53b6-205">Hallo volgende voorbeeld retourneert `[1, 2]`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-205">hello following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="d53b6-206">Voorbeeld 3: object</span><span class="sxs-lookup"><span data-stu-id="d53b6-206">Example 3: object</span></span>
<span data-ttu-id="d53b6-207">Stel `element1` geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="d53b6-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="d53b6-208">Hallo volgende voorbeeld retourneert `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-208">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="d53b6-209">Overslaan</span><span class="sxs-lookup"><span data-stu-id="d53b6-209">skip</span></span>
<span data-ttu-id="d53b6-210">Een opgegeven aantal elementen in een verzameling omzeilt en retourneert vervolgens Hallo resterende elementen.</span><span class="sxs-lookup"><span data-stu-id="d53b6-210">Bypasses a specified number of elements in a collection, and then returns hello remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="d53b6-211">Voorbeeld 1: tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d53b6-211">Example 1: string</span></span>
<span data-ttu-id="d53b6-212">Hallo volgende voorbeeld retourneert `"bar"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-212">hello following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="d53b6-213">Voorbeeld 2: matrix</span><span class="sxs-lookup"><span data-stu-id="d53b6-213">Example 2: array</span></span>
<span data-ttu-id="d53b6-214">Stel `element1` retourneert `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="d53b6-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="d53b6-215">Hallo volgende voorbeeld retourneert `[3]`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-215">hello following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="d53b6-216">Voorbeeld 3: object</span><span class="sxs-lookup"><span data-stu-id="d53b6-216">Example 3: object</span></span>
<span data-ttu-id="d53b6-217">Stel `element1` geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="d53b6-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="d53b6-218">Hallo volgende voorbeeld retourneert `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-218">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="d53b6-219">Logische functies</span><span class="sxs-lookup"><span data-stu-id="d53b6-219">Logical functions</span></span>
<span data-ttu-id="d53b6-220">Deze functies kunnen worden gebruikt in voorwaardelijke.</span><span class="sxs-lookup"><span data-stu-id="d53b6-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="d53b6-221">Sommige functies mogelijk niet alle JSON-gegevenstypen ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d53b6-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="d53b6-222">is gelijk aan</span><span class="sxs-lookup"><span data-stu-id="d53b6-222">equals</span></span>
<span data-ttu-id="d53b6-223">Retourneert `true` als beide parameters Hallo hetzelfde type en de waarde hebben.</span><span class="sxs-lookup"><span data-stu-id="d53b6-223">Returns `true` if both parameters have hello same type and value.</span></span> <span data-ttu-id="d53b6-224">Deze functie ondersteunt alle JSON-gegevenstypen.</span><span class="sxs-lookup"><span data-stu-id="d53b6-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="d53b6-225">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-225">hello following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="d53b6-226">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-226">hello following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="d53b6-227">Hallo volgende voorbeeld retourneert `false`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-227">hello following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="d53b6-228">minder</span><span class="sxs-lookup"><span data-stu-id="d53b6-228">less</span></span>
<span data-ttu-id="d53b6-229">Retourneert `true` als eerste parameter Hallo strikt kleiner is dan de tweede parameter Hallo.</span><span class="sxs-lookup"><span data-stu-id="d53b6-229">Returns `true` if hello first parameter is strictly less than hello second parameter.</span></span> <span data-ttu-id="d53b6-230">Deze functie biedt ondersteuning voor parameters alleen van het nummer van het type en de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="d53b6-231">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-231">hello following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="d53b6-232">Hallo volgende voorbeeld retourneert `false`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-232">hello following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="d53b6-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="d53b6-233">lessOrEquals</span></span>
<span data-ttu-id="d53b6-234">Retourneert `true` als eerste parameter Hallo kleiner dan of gelijk is toohello tweede parameter.</span><span class="sxs-lookup"><span data-stu-id="d53b6-234">Returns `true` if hello first parameter is less than or equal toohello second parameter.</span></span> <span data-ttu-id="d53b6-235">Deze functie biedt ondersteuning voor parameters alleen van het nummer van het type en de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="d53b6-236">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-236">hello following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="d53b6-237">groter</span><span class="sxs-lookup"><span data-stu-id="d53b6-237">greater</span></span>
<span data-ttu-id="d53b6-238">Retourneert `true` als eerste parameter Hallo strikt groter is dan de tweede parameter Hallo.</span><span class="sxs-lookup"><span data-stu-id="d53b6-238">Returns `true` if hello first parameter is strictly greater than hello second parameter.</span></span> <span data-ttu-id="d53b6-239">Deze functie biedt ondersteuning voor parameters alleen van het nummer van het type en de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="d53b6-240">Hallo volgende voorbeeld retourneert `false`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-240">hello following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="d53b6-241">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-241">hello following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="d53b6-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="d53b6-242">greaterOrEquals</span></span>
<span data-ttu-id="d53b6-243">Retourneert `true` als eerste parameter Hallo groter dan of gelijk toohello tweede parameter is.</span><span class="sxs-lookup"><span data-stu-id="d53b6-243">Returns `true` if hello first parameter is greater than or equal toohello second parameter.</span></span> <span data-ttu-id="d53b6-244">Deze functie biedt ondersteuning voor parameters alleen van het nummer van het type en de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="d53b6-245">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-245">hello following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="d53b6-246">en</span><span class="sxs-lookup"><span data-stu-id="d53b6-246">and</span></span>
<span data-ttu-id="d53b6-247">Retourneert `true` als alle Hallo parameters te evalueren`true`.</span><span class="sxs-lookup"><span data-stu-id="d53b6-247">Returns `true` if all hello parameters evaluate too`true`.</span></span> <span data-ttu-id="d53b6-248">Deze functie biedt ondersteuning voor twee of meer parameters van het type Booleaans alleen.</span><span class="sxs-lookup"><span data-stu-id="d53b6-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="d53b6-249">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-249">hello following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="d53b6-250">Hallo volgende voorbeeld retourneert `false`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-250">hello following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="d53b6-251">of</span><span class="sxs-lookup"><span data-stu-id="d53b6-251">or</span></span>
<span data-ttu-id="d53b6-252">Retourneert `true` als ten minste één Hallo parameters te evalueert`true`.</span><span class="sxs-lookup"><span data-stu-id="d53b6-252">Returns `true` if at least one of hello parameters evaluates too`true`.</span></span> <span data-ttu-id="d53b6-253">Deze functie biedt ondersteuning voor twee of meer parameters van het type Booleaans alleen.</span><span class="sxs-lookup"><span data-stu-id="d53b6-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="d53b6-254">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-254">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="d53b6-255">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-255">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="d53b6-256">niet</span><span class="sxs-lookup"><span data-stu-id="d53b6-256">not</span></span>
<span data-ttu-id="d53b6-257">Retourneert `true` als parameter Hallo te evalueert`false`.</span><span class="sxs-lookup"><span data-stu-id="d53b6-257">Returns `true` if hello parameter evaluates too`false`.</span></span> <span data-ttu-id="d53b6-258">Deze functie biedt ondersteuning voor parameters van het type Booleaans alleen.</span><span class="sxs-lookup"><span data-stu-id="d53b6-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="d53b6-259">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-259">hello following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="d53b6-260">Hallo volgende voorbeeld retourneert `false`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-260">hello following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="d53b6-261">Coalesce</span><span class="sxs-lookup"><span data-stu-id="d53b6-261">coalesce</span></span>
<span data-ttu-id="d53b6-262">Retourneert Hallo de waarde van de eerste niet-null-parameter Hallo.</span><span class="sxs-lookup"><span data-stu-id="d53b6-262">Returns hello value of hello first non-null parameter.</span></span> <span data-ttu-id="d53b6-263">Deze functie ondersteunt alle JSON-gegevenstypen.</span><span class="sxs-lookup"><span data-stu-id="d53b6-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="d53b6-264">Stel `element1` en `element2` zijn niet gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="d53b6-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="d53b6-265">Hallo volgende voorbeeld retourneert `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-265">hello following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="d53b6-266">Van conversiefuncties</span><span class="sxs-lookup"><span data-stu-id="d53b6-266">Conversion functions</span></span>
<span data-ttu-id="d53b6-267">Deze functies kunnen worden gebruikt tooconvert waarden tussen JSON-gegevenstypen en coderingen.</span><span class="sxs-lookup"><span data-stu-id="d53b6-267">These functions can be used tooconvert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="d53b6-268">int</span><span class="sxs-lookup"><span data-stu-id="d53b6-268">int</span></span>
<span data-ttu-id="d53b6-269">Converteert Hallo parameter tooan geheel getal.</span><span class="sxs-lookup"><span data-stu-id="d53b6-269">Converts hello parameter tooan integer.</span></span> <span data-ttu-id="d53b6-270">Deze functie biedt ondersteuning voor parameters van het nummer van het type en de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="d53b6-271">Hallo volgende voorbeeld retourneert `1`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-271">hello following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="d53b6-272">Hallo volgende voorbeeld retourneert `2`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-272">hello following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="d53b6-273">Float</span><span class="sxs-lookup"><span data-stu-id="d53b6-273">float</span></span>
<span data-ttu-id="d53b6-274">Converteert Hallo parameter tooa met drijvende komma.</span><span class="sxs-lookup"><span data-stu-id="d53b6-274">Converts hello parameter tooa floating-point.</span></span> <span data-ttu-id="d53b6-275">Deze functie biedt ondersteuning voor parameters van het nummer van het type en de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="d53b6-276">Hallo volgende voorbeeld retourneert `1.0`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-276">hello following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="d53b6-277">Hallo volgende voorbeeld retourneert `2.9`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-277">hello following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="d53b6-278">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d53b6-278">string</span></span>
<span data-ttu-id="d53b6-279">Converteert Hallo parameter tooa.</span><span class="sxs-lookup"><span data-stu-id="d53b6-279">Converts hello parameter tooa string.</span></span> <span data-ttu-id="d53b6-280">Deze functie biedt ondersteuning voor parameters van alle JSON-gegevenstypen.</span><span class="sxs-lookup"><span data-stu-id="d53b6-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="d53b6-281">Hallo volgende voorbeeld retourneert `"1"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-281">hello following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="d53b6-282">Hallo volgende voorbeeld retourneert `"2.9"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-282">hello following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="d53b6-283">Hallo volgende voorbeeld retourneert `"[1,2,3]"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-283">hello following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="d53b6-284">Hallo volgende voorbeeld retourneert `"{"foo":"bar"}"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-284">hello following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="d53b6-285">BOOL</span><span class="sxs-lookup"><span data-stu-id="d53b6-285">bool</span></span>
<span data-ttu-id="d53b6-286">Converteert Hallo parameter tooa Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="d53b6-286">Converts hello parameter tooa Boolean.</span></span> <span data-ttu-id="d53b6-287">Deze functie biedt ondersteuning voor parameters van het nummer van het type tekenreeks en Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="d53b6-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="d53b6-288">Vergelijkbare tooBooleans in JavaScript, een willekeurige waarde behalve `0` of `'false'` retourneert `true`.</span><span class="sxs-lookup"><span data-stu-id="d53b6-288">Similar tooBooleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="d53b6-289">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-289">hello following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="d53b6-290">Hallo volgende voorbeeld retourneert `false`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-290">hello following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="d53b6-291">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-291">hello following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="d53b6-292">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-292">hello following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="d53b6-293">parseren</span><span class="sxs-lookup"><span data-stu-id="d53b6-293">parse</span></span>
<span data-ttu-id="d53b6-294">Converteert Hallo tooa parametereigen type.</span><span class="sxs-lookup"><span data-stu-id="d53b6-294">Converts hello parameter tooa native type.</span></span> <span data-ttu-id="d53b6-295">Met andere woorden, deze functie is Hallo inverse van `string()`.</span><span class="sxs-lookup"><span data-stu-id="d53b6-295">In other words, this function is hello inverse of `string()`.</span></span> <span data-ttu-id="d53b6-296">Deze functie biedt ondersteuning voor parameters die alleen van het type tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="d53b6-297">Hallo volgende voorbeeld retourneert `1`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-297">hello following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="d53b6-298">Hallo volgende voorbeeld retourneert `true`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-298">hello following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="d53b6-299">Hallo volgende voorbeeld retourneert `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-299">hello following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="d53b6-300">Hallo volgende voorbeeld retourneert `{"foo":"bar"}`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-300">hello following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="d53b6-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="d53b6-301">encodeBase64</span></span>
<span data-ttu-id="d53b6-302">Codeert Hallo parameter tooa base-64 gecodeerde tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-302">Encodes hello parameter tooa base-64 encoded string.</span></span> <span data-ttu-id="d53b6-303">Deze functie biedt ondersteuning voor parameters die alleen van het type tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="d53b6-304">Hallo volgende voorbeeld retourneert `"Zm9vYmFy"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-304">hello following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="d53b6-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="d53b6-305">decodeBase64</span></span>
<span data-ttu-id="d53b6-306">Decodeert Hallo-parameter van een Base64-gecodeerde tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-306">Decodes hello parameter from a base-64 encoded string.</span></span> <span data-ttu-id="d53b6-307">Deze functie biedt ondersteuning voor parameters die alleen van het type tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="d53b6-308">Hallo volgende voorbeeld retourneert `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-308">hello following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="d53b6-309">encodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="d53b6-309">encodeUriComponent</span></span>
<span data-ttu-id="d53b6-310">Codeert Hallo parameter tooa URL gecodeerde tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-310">Encodes hello parameter tooa URL encoded string.</span></span> <span data-ttu-id="d53b6-311">Deze functie biedt ondersteuning voor parameters die alleen van het type tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="d53b6-312">Hallo volgende voorbeeld retourneert `"https%3A%2F%2Fportal.azure.com%2F"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-312">hello following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="d53b6-313">decodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="d53b6-313">decodeUriComponent</span></span>
<span data-ttu-id="d53b6-314">Decodeert Hallo-parameter van een URL-gecodeerde tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-314">Decodes hello parameter from a URL encoded string.</span></span> <span data-ttu-id="d53b6-315">Deze functie biedt ondersteuning voor parameters die alleen van het type tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d53b6-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="d53b6-316">Hallo volgende voorbeeld retourneert `"https://portal.azure.com/"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-316">hello following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="d53b6-317">Rekenkundige functies</span><span class="sxs-lookup"><span data-stu-id="d53b6-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="d53b6-318">toevoegen</span><span class="sxs-lookup"><span data-stu-id="d53b6-318">add</span></span>
<span data-ttu-id="d53b6-319">Telt twee getallen en retourneert Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="d53b6-319">Adds two numbers, and returns hello result.</span></span>

<span data-ttu-id="d53b6-320">Hallo volgende voorbeeld retourneert `3`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-320">hello following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="d53b6-321">Sub</span><span class="sxs-lookup"><span data-stu-id="d53b6-321">sub</span></span>
<span data-ttu-id="d53b6-322">Tweede nummer van het eerste nummer Hallo Hallo aftrekken en retourneert Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="d53b6-322">Subtracts hello second number from hello first number, and returns hello result.</span></span>

<span data-ttu-id="d53b6-323">Hallo volgende voorbeeld retourneert `1`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-323">hello following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="d53b6-324">mul</span><span class="sxs-lookup"><span data-stu-id="d53b6-324">mul</span></span>
<span data-ttu-id="d53b6-325">Vermenigvuldigt twee getallen en retourneert Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="d53b6-325">Multiplies two numbers, and returns hello result.</span></span>

<span data-ttu-id="d53b6-326">Hallo volgende voorbeeld retourneert `6`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-326">hello following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="d53b6-327">div</span><span class="sxs-lookup"><span data-stu-id="d53b6-327">div</span></span>
<span data-ttu-id="d53b6-328">Deelt Hallo eerste getal door het tweede getal Hallo en Hallo resultaat retourneert.</span><span class="sxs-lookup"><span data-stu-id="d53b6-328">Divides hello first number by hello second number, and returns hello result.</span></span> <span data-ttu-id="d53b6-329">Hallo-resultaat is altijd een geheel getal.</span><span class="sxs-lookup"><span data-stu-id="d53b6-329">hello result is always an integer.</span></span>

<span data-ttu-id="d53b6-330">Hallo volgende voorbeeld retourneert `2`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-330">hello following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="d53b6-331">Mod</span><span class="sxs-lookup"><span data-stu-id="d53b6-331">mod</span></span>
<span data-ttu-id="d53b6-332">Eerste getal door het tweede getal Hallo Hallo deelt, en retourneert Hallo rest.</span><span class="sxs-lookup"><span data-stu-id="d53b6-332">Divides hello first number by hello second number, and returns hello remainder.</span></span>

<span data-ttu-id="d53b6-333">Hallo volgende voorbeeld retourneert `0`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-333">hello following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="d53b6-334">Hallo volgende voorbeeld retourneert `2`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-334">hello following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="d53b6-335">min.</span><span class="sxs-lookup"><span data-stu-id="d53b6-335">min</span></span>
<span data-ttu-id="d53b6-336">Retourneert Hallo klein Hallo twee getallen.</span><span class="sxs-lookup"><span data-stu-id="d53b6-336">Returns hello small of hello two numbers.</span></span>

<span data-ttu-id="d53b6-337">Hallo volgende voorbeeld retourneert `1`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-337">hello following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="d53b6-338">Maximum aantal</span><span class="sxs-lookup"><span data-stu-id="d53b6-338">max</span></span>
<span data-ttu-id="d53b6-339">Retourneert hello grotere van Hallo twee getallen.</span><span class="sxs-lookup"><span data-stu-id="d53b6-339">Returns hello larger of hello two numbers.</span></span>

<span data-ttu-id="d53b6-340">Hallo volgende voorbeeld retourneert `2`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-340">hello following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="d53b6-341">bereik</span><span class="sxs-lookup"><span data-stu-id="d53b6-341">range</span></span>
<span data-ttu-id="d53b6-342">Genereert een reeks integraal getallen in Hallo opgegeven bereik.</span><span class="sxs-lookup"><span data-stu-id="d53b6-342">Generates a sequence of integral numbers within hello specified range.</span></span>

<span data-ttu-id="d53b6-343">Hallo volgende voorbeeld retourneert `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-343">hello following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="d53b6-344">rand</span><span class="sxs-lookup"><span data-stu-id="d53b6-344">rand</span></span>
<span data-ttu-id="d53b6-345">Retourneert een willekeurig geheel getal in Hallo opgegeven bereik.</span><span class="sxs-lookup"><span data-stu-id="d53b6-345">Returns a random integral number within hello specified range.</span></span> <span data-ttu-id="d53b6-346">Deze functie geen cryptografisch beveiligde willekeurige getallen gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d53b6-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="d53b6-347">Hallo volgende voorbeeld kan retourneren `42`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-347">hello following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="d53b6-348">Floor</span><span class="sxs-lookup"><span data-stu-id="d53b6-348">floor</span></span>
<span data-ttu-id="d53b6-349">Retourneert de grootste integer Hallo kleiner dan of gelijk toohello opgegeven getal.</span><span class="sxs-lookup"><span data-stu-id="d53b6-349">Returns hello largest integer less than or equal toohello specified number.</span></span>

<span data-ttu-id="d53b6-350">Hallo volgende voorbeeld retourneert `3`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-350">hello following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="d53b6-351">ceil</span><span class="sxs-lookup"><span data-stu-id="d53b6-351">ceil</span></span>
<span data-ttu-id="d53b6-352">Retourneert Hallo grootste gehele getal groter dan of gelijk zijn toohello opgegeven getal.</span><span class="sxs-lookup"><span data-stu-id="d53b6-352">Returns hello largest integer greater than or equal toohello specified number.</span></span>

<span data-ttu-id="d53b6-353">Hallo volgende voorbeeld retourneert `4`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-353">hello following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="d53b6-354">Datumfuncties</span><span class="sxs-lookup"><span data-stu-id="d53b6-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="d53b6-355">utcNow</span><span class="sxs-lookup"><span data-stu-id="d53b6-355">utcNow</span></span>
<span data-ttu-id="d53b6-356">Retourneert een tekenreeks in de ISO 8601-notatie Hallo huidige datum en tijd op de lokale computer Hallo.</span><span class="sxs-lookup"><span data-stu-id="d53b6-356">Returns a string in ISO 8601 format of hello current date and time on hello local computer.</span></span>

<span data-ttu-id="d53b6-357">Hallo volgende voorbeeld kan retourneren `"1990-12-31T23:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-357">hello following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="d53b6-358">addSeconds</span><span class="sxs-lookup"><span data-stu-id="d53b6-358">addSeconds</span></span>
<span data-ttu-id="d53b6-359">Voegt een geheel getal van seconden toohello opgegeven timestamp.</span><span class="sxs-lookup"><span data-stu-id="d53b6-359">Adds an integral number of seconds toohello specified timestamp.</span></span>

<span data-ttu-id="d53b6-360">Hallo volgende voorbeeld retourneert `"1991-01-01T00:00:00.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-360">hello following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="d53b6-361">addMinutes</span><span class="sxs-lookup"><span data-stu-id="d53b6-361">addMinutes</span></span>
<span data-ttu-id="d53b6-362">Voegt een geheel getal van minuten toohello opgegeven timestamp.</span><span class="sxs-lookup"><span data-stu-id="d53b6-362">Adds an integral number of minutes toohello specified timestamp.</span></span>

<span data-ttu-id="d53b6-363">Hallo volgende voorbeeld retourneert `"1991-01-01T00:00:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-363">hello following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="d53b6-364">addHours</span><span class="sxs-lookup"><span data-stu-id="d53b6-364">addHours</span></span>
<span data-ttu-id="d53b6-365">Voegt een geheel getal van uren toohello opgegeven timestamp.</span><span class="sxs-lookup"><span data-stu-id="d53b6-365">Adds an integral number of hours toohello specified timestamp.</span></span>

<span data-ttu-id="d53b6-366">Hallo volgende voorbeeld retourneert `"1991-01-01T00:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="d53b6-366">hello following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="d53b6-367">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d53b6-367">Next steps</span></span>
* <span data-ttu-id="d53b6-368">Zie voor een inleiding tooAzure Resource Manager, [overzicht van Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d53b6-368">For an introduction tooAzure Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

