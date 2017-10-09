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
# <a name="azure-resource-manager-template-functions"></a>Azure Resource Manager-sjabloonfuncties
Dit onderwerp beschrijft alle Hallo-functies die kunt u in een Azure Resource Manager-sjabloon.

U functies in uw sjablonen toevoegen door deze tekst tussen vierkante haken: `[` en `]`respectievelijk. Hallo-expressie wordt geëvalueerd tijdens de implementatie. Hoewel geschreven als een letterlijke tekenreeks, zijn Hallo resultaat van de evaluatie van Hallo expressie van een ander JSON-type, zoals een matrix, een object of een geheel getal. Net zoals in JavaScript-functieaanroepen die zijn opgemaakt als `functionName(arg1,arg2,arg3)`. U verwijzen naar eigenschappen met behulp van Hallo punt en [index] operators.

Een sjabloonexpressie kan 24.576 tekens niet overschrijden.

Sjabloonfuncties en de bijbehorende parameters zijn niet hoofdlettergevoelig. Bijvoorbeeld: Resource Manager wordt omgezet **variables('var1')** en **VARIABLES('VAR1')** zoals Hallo dezelfde. Wanneer geëvalueerd, tenzij de functie Hallo wijzigt uitdrukkelijk geval (zoals toUpper of toLower), Hallo functie behoudt Hallo hoofdlettergebruik. Bepaalde brontypen misschien case vereisten, ongeacht hoe functies worden geëvalueerd.

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

## <a name="array-and-object-functions"></a>Matrix en object-functies
Resource Manager biedt een aantal functies voor het werken met matrices en objecten.

* [matrix](resource-group-template-functions-array.md#array)
* [coalesce](resource-group-template-functions-array.md#coalesce)
* [concat](resource-group-template-functions-array.md#concat)
* [bevat](resource-group-template-functions-array.md#contains)
* [createArray](resource-group-template-functions-array.md#createarray)
* [leeg](resource-group-template-functions-array.md#empty)
* [eerste](resource-group-template-functions-array.md#first)
* [snijpunt](resource-group-template-functions-array.md#intersection)
* [JSON](resource-group-template-functions-array.md#json)
* [laatste](resource-group-template-functions-array.md#last)
* [lengte](resource-group-template-functions-array.md#length)
* [min](resource-group-template-functions-array.md#min)
* [maximale](resource-group-template-functions-array.md#max)
* [bereik](resource-group-template-functions-array.md#range)
* [overslaan](resource-group-template-functions-array.md#skip)
* [duren](resource-group-template-functions-array.md#take)
* [Union](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a>Vergelijking van functies
Resource Manager biedt een aantal functies voor het maken van vergelijkingen in uw sjablonen.

* [is gelijk aan](resource-group-template-functions-comparison.md#equals)
* [minder](resource-group-template-functions-comparison.md#less)
* [lessOrEquals](resource-group-template-functions-comparison.md#lessorequals)
* [groter](resource-group-template-functions-comparison.md#greater)
* [greaterOrEquals](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a>Waarde van de implementaties
Resource Manager biedt Hallo volgende fungeert voor het ophalen van waarden in de secties van de sjabloon Hallo en verwante toohello implementatie waarden:

* [implementatie](resource-group-template-functions-deployment.md#deployment)
* [parameters](resource-group-template-functions-deployment.md#parameters)
* [variabelen](resource-group-template-functions-deployment.md#variables)

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

## <a name="logical-functions"></a>Logische functies
Resource Manager biedt de volgende functies voor het werken met logische voorwaarden Hallo:

* [en](resource-group-template-functions-logical.md#and)
* [BOOL](resource-group-template-functions-logical.md#bool)
* [Als](resource-group-template-functions-logical.md#if)
* [niet](resource-group-template-functions-logical.md#not)
* [of](resource-group-template-functions-logical.md#or)

## <a name="numeric-functions"></a>Numerieke functies
Resource Manager biedt Hallo functies voor het werken met gehele getallen te volgen:

* [toevoegen](resource-group-template-functions-numeric.md#add)
* [copyIndex](resource-group-template-functions-numeric.md#copyindex)
* [div](resource-group-template-functions-numeric.md#div)
* [Float](resource-group-template-functions-numeric.md#float)
* [int](resource-group-template-functions-numeric.md#int)
* [min](resource-group-template-functions-numeric.md#min)
* [maximale](resource-group-template-functions-numeric.md#max)
* [Mod](resource-group-template-functions-numeric.md#mod)
* [mul](resource-group-template-functions-numeric.md#mul)
* [Sub](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a>Resource-functies
Resource Manager biedt Hallo functies voor het ophalen van waarden van de resource te volgen:

* [listKeys en de lijst {Value}](resource-group-template-functions-resource.md#listkeys)
* [providers](resource-group-template-functions-resource.md#providers)
* [verwijzing](resource-group-template-functions-resource.md#reference)
* [resourceGroup](resource-group-template-functions-resource.md#resourcegroup)
* [resourceId](resource-group-template-functions-resource.md#resourceid)
* [abonnement](resource-group-template-functions-resource.md#subscription)

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

## <a name="string-functions"></a>Tekenreeks-functies
Resource Manager biedt Hallo functies voor het werken met tekenreeksen te volgen:

* [Base64](resource-group-template-functions-string.md#base64)
* [base64ToJson](resource-group-template-functions-string.md#base64tojson)
* [base64ToString](resource-group-template-functions-string.md#base64tostring)
* [concat](resource-group-template-functions-string.md#concat)
* [bevat](resource-group-template-functions-string.md#contains)
* [dataUri](resource-group-template-functions-string.md#datauri)
* [dataUriToString](resource-group-template-functions-string.md#datauritostring)
* [leeg](resource-group-template-functions-string.md#empty)
* [endsWith](resource-group-template-functions-string.md#endswith)
* [eerste](resource-group-template-functions-string.md#first)
* [indexOf](resource-group-template-functions-string.md#indexof)
* [laatste](resource-group-template-functions-string.md#last)
* [lastIndexOf](resource-group-template-functions-string.md#lastindexof)
* [lengte](resource-group-template-functions-string.md#length)
* [padLeft](resource-group-template-functions-string.md#padleft)
* [vervangen](resource-group-template-functions-string.md#replace)
* [overslaan](resource-group-template-functions-string.md#skip)
* [split](resource-group-template-functions-string.md#split)
* [startsWith](resource-group-template-functions-string.md#startswith)
* [tekenreeks](resource-group-template-functions-string.md#string)
* [de subtekenreeks](resource-group-template-functions-string.md#substring)
* [duren](resource-group-template-functions-string.md#take)
* [toLower](resource-group-template-functions-string.md#tolower)
* [toUpper](resource-group-template-functions-string.md#toupper)
* [Trim](resource-group-template-functions-string.md#trim)
* [uniqueString](resource-group-template-functions-string.md#uniquestring)
* [URI](resource-group-template-functions-string.md#uri)
* [uriComponent](resource-group-template-functions-string.md#uricomponent)
* [uriComponentToString](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a>Volgende stappen
* Zie voor een beschrijving van de secties Hallo in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md)
* toomerge meerdere sjablonen Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md)
* een opgegeven aantal keren tooiterate bij het maken van een type resource, Zie [meerdere exemplaren van resources in Azure Resource Manager maken](resource-group-create-multiple.md)
* toosee hoe toodeploy Hallo sjabloon die u hebt gemaakt, raadpleegt [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md)

