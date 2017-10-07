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
# <a name="string-functions-for-azure-resource-manager-templates"></a>Tekenreeks-functies voor Azure Resource Manager-sjablonen

Resource Manager biedt Hallo functies voor het werken met tekenreeksen te volgen:

* [Base64](#base64)
* [base64ToJson](#base64tojson)
* [base64ToString](#base64tostring)
* [concat](#concat)
* [bevat](#contains)
* [dataUri](#datauri)
* [dataUriToString](#datauritostring)
* [leeg](#empty)
* [endsWith](#endswith)
* [eerste](#first)
* [indexOf](#indexof)
* [laatste](#last)
* [lastIndexOf](#lastindexof)
* [lengte](#length)
* [padLeft](#padleft)
* [vervangen](#replace)
* [overslaan](#skip)
* [split](#split)
* [startsWith](resource-group-template-functions-string.md#startswith)
* [tekenreeks](#string)
* [de subtekenreeks](#substring)
* [duren](#take)
* [toLower](#tolower)
* [toUpper](#toupper)
* [Trim](#trim)
* [uniqueString](#uniquestring)
* [URI](#uri)
* [uriComponent](resource-group-template-functions-string.md#uricomponent)
* [uriComponentToString](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a>Base64
`base64(inputString)`

Retourneert Hallo base64-weergave van de invoertekenreeks Hallo.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| inputString |Ja |Tekenreeks |Hallo waarde tooreturn als een base64-weergave. |

### <a name="return-value"></a>Retourwaarde

Een tekenreeks met Hallo base64-weergave.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld ziet u hoe toouse Hallo base64-functie.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| base64Output | Tekenreeks | b25lLCB0d28sIHRocmVl |
| toStringOutput | Tekenreeks | Een twee drie |
| toJsonOutput | Object | {"een": "a", "twee": "b"} |

<a id="base64tojson" />

## <a name="base64tojson"></a>base64ToJson
`base64tojson`

Converteert een base64-weergave tooa JSON-object.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| base64Value |Ja |Tekenreeks |Hallo base64-weergave tooconvert tooa JSON-object. |

### <a name="return-value"></a>Retourwaarde

Een JSON-object.

### <a name="examples"></a>Voorbeelden

Hallo wordt volgende voorbeeld Hallo base64ToJson functie tooconvert een base64-waarde:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| base64Output | Tekenreeks | b25lLCB0d28sIHRocmVl |
| toStringOutput | Tekenreeks | Een twee drie |
| toJsonOutput | Object | {"een": "a", "twee": "b"} |

<a id="base64tostring" />

## <a name="base64tostring"></a>base64ToString
`base64ToString(base64Value)`

Zet een tekenreeks met base64-weergave tooa.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| base64Value |Ja |Tekenreeks |Hallo base64-weergave tooconvert tooa tekenreeks. |

### <a name="return-value"></a>Retourwaarde

Een tekenreeks van Hallo geconverteerd base64-waarde.

### <a name="examples"></a>Voorbeelden

Hallo wordt volgende voorbeeld Hallo base64ToString functie tooconvert een base64-waarde:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| base64Output | Tekenreeks | b25lLCB0d28sIHRocmVl |
| toStringOutput | Tekenreeks | Een twee drie |
| toJsonOutput | Object | {"een": "a", "twee": "b"} |



<a id="concat" />

## <a name="concat"></a>concat
`concat (arg1, arg2, arg3, ...)`

Combineert meerdere tekenreekswaarden en retourneert Hallo samengevoegd tekenreeks, of combineert meerdere matrices en retourneert Hallo samengevoegd matrix.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |tekenreeks of matrix |Hallo eerste waarde voor de samenvoeging. |
| Extra argumenten |Nee |Tekenreeks |Aanvullende waarden in opeenvolgende volgorde voor de samenvoeging. |

### <a name="return-value"></a>Retourwaarde
Een tekenreeks of matrix met samengevoegde waarden.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld ziet u hoe toocombine twee tekenreekswaarden en een samengevoegde tekenreeks retourneren.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| concatOutput | Tekenreeks | voorvoegsel 5yj4yjf5mbg72 |

Hallo volgende voorbeeld ziet u hoe toocombine twee matrices.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| retourneren | Matrix | ["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"] |

<a id="contains" />

## <a name="contains"></a>Bevat
`contains (container, itemToFind)`

Controleert of een matrix een waarde bevat, een object een sleutel bevat of een tekenreeks een subtekenreeks bevat.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| container |Ja |Array, object of een tekenreeks |Hallo-waarde die Hallo waarde toofind bevat. |
| itemToFind |Ja |String of int. |Hallo waarde toofind. |

### <a name="return-value"></a>Retourwaarde

**De waarde True** als Hallo item gevonden, anders wordt is **False**.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld laat zien hoe toouse bevat met verschillende typen:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| stringTrue | BOOL | True |
| stringFalse | BOOL | False |
| objectTrue | BOOL | True |
| objectFalse | BOOL | False |
| arrayTrue | BOOL | True |
| arrayFalse | BOOL | False |

<a id="datauri" />

## <a name="datauri"></a>dataUri
`dataUri(stringToConvert)`

Converteert een waarde tooa gegevens URI.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| stringToConvert |Ja |Tekenreeks |Hallo tooconvert tooa Waardegegevens URI. |

### <a name="return-value"></a>Retourwaarde

Een tekenreeks zijn opgemaakt als een gegevens-URI.

### <a name="examples"></a>Voorbeelden

Hallo voorbeeld te volgen tooa gegevenswaarde URI converteert en zet een gegevens-URI tooa tekenreeks:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| dataUriOutput | Tekenreeks | gegevens: tekst / onbewerkte; charset = utf8; base64, SGVsbG8 = |
| toStringOutput | Tekenreeks | Hallo mensen! |

<a id="datauritostring" />

## <a name="datauritostring"></a>dataUriToString
`dataUriToString(dataUriToConvert)`

Een gegevens-URI converteert geformatteerd tooa tekenreekswaarde.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| dataUriToConvert |Ja |Tekenreeks |Hallo gegevenswaarde URI tooconvert. |

### <a name="return-value"></a>Retourwaarde

Een tekenreeks met Hallo geconverteerd waarde.

### <a name="examples"></a>Voorbeelden

Hallo voorbeeld te volgen tooa gegevenswaarde URI converteert en zet een gegevens-URI tooa tekenreeks:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| dataUriOutput | Tekenreeks | gegevens: tekst / onbewerkte; charset = utf8; base64, SGVsbG8 = |
| toStringOutput | Tekenreeks | Hallo mensen! |

<a id="empty" /> 

## <a name="empty"></a>leeg
`empty(itemToTest)`

Hiermee wordt bepaald of een matrix, een object of een tekenreeks leeg is.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| itemToTest |Ja |Array, object of een tekenreeks |Hallo waarde toocheck als deze leeg is. |

### <a name="return-value"></a>Retourwaarde

Retourneert **True** als Hallo-waarde leeg, anders wordt is **False**.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld wordt gecontroleerd of een matrix, het object en de tekenreeks leeg zijn.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| arrayEmpty | BOOL | True |
| objectEmpty | BOOL | True |
| stringEmpty | BOOL | True |

<a id="endswith" />

## <a name="endswith"></a>endsWith
`endsWith(stringToSearch, stringToFind)`

Hiermee wordt bepaald of een tekenreeks met een waarde eindigt. Hallo vergelijking is niet hoofdlettergevoelig.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| stringToSearch |Ja |Tekenreeks |Hallo-waarde die Hallo item toofind bevat. |
| stringToFind |Ja |Tekenreeks |Hallo waarde toofind. |

### <a name="return-value"></a>Retourwaarde

**De waarde True** als laatste teken Hallo of van Hallo tekenreeks overeenkomt met de waarde van de Hallo; anders **False**.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld ziet u hoe toouse Hallo startsWith en endsWith-functies:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| startsTrue | BOOL | True |
| startsCapTrue | BOOL | True |
| startsFalse | BOOL | False |
| endsTrue | BOOL | True |
| endsCapTrue | BOOL | True |
| endsFalse | BOOL | False |

<a id="first" />

## <a name="first"></a>eerste
`first(arg1)`

Retourneert Hallo eerste teken van Hallo tekenreeks of het eerste element van de matrix Hallo.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |matrix of tekenreeks |Hallo waarde tooretrieve Hallo eerste element of teken. |

### <a name="return-value"></a>Retourwaarde

Een tekenreeks van het eerste teken Hallo of Hallo type (string, int, matrix of object) Hallo eerste element in een matrix.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld ziet u hoe toouse Hallo eerste functie met een matrix en de tekenreeks.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| arrayOutput | Tekenreeks | een |
| stringOutput | Tekenreeks | O |

<a id="indexof" />

## <a name="indexof"></a>indexOf
`indexOf(stringToSearch, stringToFind)`

Retourneert Hallo eerste positie van een waarde in een tekenreeks. Hallo vergelijking is niet hoofdlettergevoelig.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| stringToSearch |Ja |Tekenreeks |Hallo-waarde die Hallo item toofind bevat. |
| stringToFind |Ja |Tekenreeks |Hallo waarde toofind. |

### <a name="return-value"></a>Retourwaarde

Een geheel getal dat de positie Hallo van Hallo item toofind weergeeft. Hallo-waarde is gebaseerd op nul. Als het Hallo-item niet is gevonden, wordt -1 geretourneerd.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld ziet u hoe toouse Hallo indexOf en lastIndexOf functies:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| firstT | int | 0 |
| lastT | int | 3 |
| firstString | int | 2 |
| lastString | int | 0 |
| notFound | int | -1 |

<a id="last" />

## <a name="last"></a>laatste
`last (arg1)`

Retourneert de laatste teken van Hallo tekenreeks of Hallo laatste element van Hallo matrix.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |matrix of tekenreeks |Hallo waarde tooretrieve Hallo laatste element of teken. |

### <a name="return-value"></a>Retourwaarde

Een tekenreeks van het Hallo-type (string, int, matrix of object) van het laatste element in een matrix Hallo of Hallo laatste teken.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld ziet u hoe toouse Hallo laatste functie met een matrix en de tekenreeks.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| arrayOutput | Tekenreeks | drie |
| stringOutput | Tekenreeks | E |

<a id="lastindexof" />

## <a name="lastindexof"></a>lastIndexOf
`lastIndexOf(stringToSearch, stringToFind)`

Retourneert Hallo laatste positie van een waarde in een tekenreeks. Hallo vergelijking is niet hoofdlettergevoelig.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| stringToSearch |Ja |Tekenreeks |Hallo-waarde die Hallo item toofind bevat. |
| stringToFind |Ja |Tekenreeks |Hallo waarde toofind. |

### <a name="return-value"></a>Retourwaarde

Een geheel getal dat de laatste positie Hallo van Hallo item toofind vertegenwoordigt. Hallo-waarde is gebaseerd op nul. Als het Hallo-item niet is gevonden, wordt -1 geretourneerd.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld ziet u hoe toouse Hallo indexOf en lastIndexOf functies:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| firstT | int | 0 |
| lastT | int | 3 |
| firstString | int | 2 |
| lastString | int | 0 |
| notFound | int | -1 |

<a id="length" />

## <a name="length"></a>lengte
`length(string)`

Retourneert het aantal tekens Hallo in een tekenreeks of elementen in een matrix.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |matrix of tekenreeks |Hallo toouse voor het ophalen van het aantal elementen Hallo matrix of tekenreeks toouse voor het ophalen van het aantal tekens Hallo Hallo. |

### <a name="return-value"></a>Retourwaarde

Een int. 

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld wordt getoond hoe toouse lengte met een matrix en de tekenreeks:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| arrayLength | int | 3 |
| stringLength | int | 13 |

<a id="padleft" />

## <a name="padleft"></a>PadLeft
`padLeft(valueToPad, totalLength, paddingCharacter)`

Retourneert een rechts uitgelijnde tekenreeks door toe te voegen tekens toohello links tot het bereiken van Hallo totale opgegeven lengte.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| valueToPad |Ja |String of int. |waarde tooright Hallo-uitlijnen. |
| totalLength |Ja |int |Totaal aantal tekens in Hallo Hallo tekenreeks geretourneerd. |
| paddingCharacter |Nee |willekeurig teken |Hallo teken toouse voor links-opvulling tot de totale lengte van Hallo is bereikt. Hallo-standaardwaarde is een spatie. |

Als de oorspronkelijke reeks Hallo langer dan het aantal tekens toopad hello is, worden geen tekens toegevoegd.

### <a name="return-value"></a>Retourwaarde

Een tekenreeks met Hallo minimaal aantal tekens opgegeven.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld ziet u hoe toopad Hallo waarde van de gebruiker opgegeven parameter door toe te voegen Hallo teken nul totdat het totaal aantal tekens Hallo bereikt. 

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| stringOutput | Tekenreeks | 0000000123 |

<a id="replace" />

## <a name="replace"></a>vervangen
`replace(originalString, oldString, newString)`

Retourneert een nieuwe tekenreeks met alle exemplaren van de ene tekenreeks vervangen door een andere tekenreeks.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| originalString |Ja |Tekenreeks |Hallo-waarde met alle exemplaren van de ene tekenreeks vervangen door een andere tekenreeks. |
| oldString |Ja |Tekenreeks |Hallo tekenreeks toobe verwijderd uit de oorspronkelijke reeks Hallo. |
| met de newString |Ja |Tekenreeks |Hallo tekenreeks tooadd in plaats van Hallo tekenreeks verwijderd. |

### <a name="return-value"></a>Retourwaarde

Een tekenreeks met Hallo vervangen tekens.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld ziet u hoe tooremove alle van de gebruiker opgegeven tekenreeks Hallo streepjes en hoe tooreplace deel uit van Hallo tekenreeks door een andere tekenreeks.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| firstOutput | Tekenreeks | 1231231234 |
| secodeOutput | Tekenreeks | 123-123-xxxx |

<a id="skip" />

## <a name="skip"></a>Overslaan
`skip(originalValue, numberToSkip)`

Retourneert een tekenreeks waarin alle tekens worden Hallo nadat Hallo aantal tekens of een matrix met alle Hallo elementen opgegeven nadat Hallo aantal elementen opgegeven.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| originalValue |Ja |matrix of tekenreeks |Hallo toouse matrix of tekenreeks voor het overslaan. |
| numberToSkip |Ja |int |Hallo aantal elementen of tekens tooskip. Als deze waarde 0 of minder is, alle elementen Hallo of tekens in Hallo-waarde worden geretourneerd. Als deze groter dan Hallo lengte van Hallo matrix of tekenreeks is, een lege matrix of tekenreeks geretourneerd. |

### <a name="return-value"></a>Retourwaarde

Een matrix of tekenreeks zijn.

### <a name="examples"></a>Voorbeelden

Hallo voorbeeld Slaat het Hallo na opgegeven aantal elementen in Hallo matrix en Hallo opgegeven aantal tekens in een tekenreeks.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| arrayOutput | Matrix | ["drie"] |
| stringOutput | Tekenreeks | twee drie |

<a id="split" />

## <a name="split"></a>split
`split(inputString, delimiter)`

Retourneert een matrix met tekenreeksen die Hallo subtekenreeksen Hallo bevat invoerreeks die worden gescheiden door Hallo opgegeven scheidingstekens.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| inputString |Ja |Tekenreeks |Hallo tekenreeks toosplit. |
| Scheidingsteken |Ja |tekenreeks of matrix met tekenreeksen |Hallo scheidingsteken toouse voor het splitsen van Hallo-tekenreeks. |

### <a name="return-value"></a>Retourwaarde

Een matrix met tekenreeksen.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld wordt gesplitst invoerreeks Hallo met een komma en met een komma of puntkomma's.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| firstOutput | Matrix | ['een', 'twee', 'drie'] |
| secondOutput | Matrix | ['een', 'twee', 'drie'] |

<a id="startswith" />

## <a name="startswith"></a>StartsWith
`startsWith(stringToSearch, stringToFind)`

Hiermee wordt bepaald of een tekenreeks met een waarde begint. Hallo vergelijking is niet hoofdlettergevoelig.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| stringToSearch |Ja |Tekenreeks |Hallo-waarde die Hallo item toofind bevat. |
| stringToFind |Ja |Tekenreeks |Hallo waarde toofind. |

### <a name="return-value"></a>Retourwaarde

**De waarde True** als eerste teken Hallo of van Hallo tekenreeks overeenkomt met de waarde van de Hallo; anders **False**.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld ziet u hoe toouse Hallo startsWith en endsWith-functies:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| startsTrue | BOOL | True |
| startsCapTrue | BOOL | True |
| startsFalse | BOOL | False |
| endsTrue | BOOL | True |
| endsCapTrue | BOOL | True |
| endsFalse | BOOL | False |

<a id="string" />

## <a name="string"></a>Tekenreeks
`string(valueToConvert)`

Converteert Hallo opgegeven tooa tekenreekswaarde.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| valueToConvert |Ja | Alle |Hallo waarde tooconvert toostring. Elk type waarde kan worden geconverteerd, met inbegrip van objecten en -matrices. |

### <a name="return-value"></a>Retourwaarde

Een tekenreeks van Hallo geconverteerd-waarde.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld ziet u hoe verschillende typen tooconvert toostrings waarden:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| objectOutput | Tekenreeks | {{'valueA': 10, 'valueB': "Voorbeeldtekst"} |
| arrayOutput | Tekenreeks | ["a", "b", "c"] |
| intOutput | Tekenreeks | 5 |

<a id="substring" />

## <a name="substring"></a>de subtekenreeks
`substring(stringToParse, startIndex, length)`

Retourneert een subtekenreeks dat begint bij Hallo opgegeven tekenpositie en bevat Hallo opgegeven aantal tekens.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| stringToParse |Ja |Tekenreeks |de oorspronkelijke reeks Hallo van welke Hallo subtekenreeks wordt opgehaald. |
| startIndex |Nee |int |Hallo op nul gebaseerde beginpositie voor Hallo substring. |
| lengte |Nee |int |Hallo aantal tekens voor Hallo substring. Moet verwijzen tooa locatie binnen Hallo-tekenreeks. |

### <a name="return-value"></a>Retourwaarde

Hallo substring.

### <a name="remarks"></a>Opmerkingen

Hallo-functie mislukt wanneer Hallo subtekenreeks Hallo einde van de Hallo tekenreeks overschrijdt. Hallo volgt mislukt met de Hallo fout 'hello index en lengte parameters moeten verwijzen tooa locatie binnen Hallo-tekenreeks. Hallo Indexparameter: '0' Hallo lengteparameter: '11' Hallo lengte van de tekenreeksparameter Hallo: "10". ".

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a>Voorbeelden

Hallo volgt subtekenreeks een uit een parameter.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| substringOutput | Tekenreeks | twee |


<a id="take" />

## <a name="take"></a>duren
`take(originalValue, numberToTake)`

Retourneert een tekenreeks met Hallo aantal tekens vanaf het begin van Hallo opgegeven Hallo tekenreeks of een matrix met Hallo opgegeven aantal elementen vanaf het begin van de matrix Hallo Hallo.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| originalValue |Ja |matrix of tekenreeks |Hallo matrix of tekenreeks tootake Hallo elementen uit. |
| numberToTake |Ja |int |Hallo aantal elementen of tekens tootake. Als deze waarde 0 of minder is, wordt een lege matrix of tekenreeks geretourneerd. Als het is groter dan de lengte Hallo Hallo gegeven matrix of tekenreeks, worden alle Hallo-elementen in het Hallo-matrix of tekenreeks geretourneerd. |

### <a name="return-value"></a>Retourwaarde

Een matrix of tekenreeks zijn.

### <a name="examples"></a>Voorbeelden

Hallo voorbeeld vergt Hallo na een opgegeven aantal elementen van een matrix van Hallo en tekens uit een tekenreeks.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| arrayOutput | Matrix | ['een', 'twee'] |
| stringOutput | Tekenreeks | op |

<a id="tolower" />

## <a name="tolower"></a>toLower
`toLower(stringToChange)`

Converteert Hallo opgegeven tekenreeks toolower geval.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| stringToChange |Ja |Tekenreeks |Hallo waarde tooconvert toolower geval. |

### <a name="return-value"></a>Retourwaarde

Hallo-tekenreeks geconverteerd toolower geval.

### <a name="examples"></a>Voorbeelden

Hallo volgt converteert een parameter waarde toolower geval en tooupper geval.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| toLowerOutput | Tekenreeks | Een twee drie |
| toUpperOutput | Tekenreeks | EEN TWEE DRIE |

<a id="toupper" />

## <a name="toupper"></a>toUpper
`toUpper(stringToChange)`

Converteert Hallo opgegeven tekenreeks tooupper geval.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| stringToChange |Ja |Tekenreeks |Hallo waarde tooconvert tooupper geval. |

### <a name="return-value"></a>Retourwaarde

Hallo-tekenreeks geconverteerd tooupper geval.

### <a name="examples"></a>Voorbeelden

Hallo volgt converteert een parameter waarde toolower geval en tooupper geval.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| toLowerOutput | Tekenreeks | Een twee drie |
| toUpperOutput | Tekenreeks | EEN TWEE DRIE |

<a id="trim" />

## <a name="trim"></a>Trim
`trim (stringToTrim)`

Hiermee verwijdert u alle voorloopspaties en afsluitende spaties uit Hallo opgegeven tekenreeks.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| stringToTrim |Ja |Tekenreeks |Hallo waarde tootrim. |

### <a name="return-value"></a>Retourwaarde

Hallo tekenreeks zonder voorloopspaties en afsluitende spatietekens bestaan.

### <a name="examples"></a>Voorbeelden

Hallo verwijdert volgende voorbeeld Hallo spatietekens bestaan uit Hallo-parameter.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| retourneren | Tekenreeks | Een twee drie |

<a id="uniquestring" />

## <a name="uniquestring"></a>uniqueString
`uniqueString (baseString, ...)`

Maakt een deterministische hash-tekenreeks op basis van Hallo waarden als parameters opgegeven. 

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| baseString |Ja |Tekenreeks |Hallo-waarde die is gebruikt in Hallo hash-functie toocreate een unieke tekenreeks. |
| extra parameters indien nodig |Nee |Tekenreeks |U kunt zoveel tekenreeksen als benodigde toocreate Hallo waarde die Hallo niveau van uniekheid aangeeft toevoegen. |

### <a name="remarks"></a>Opmerkingen

Deze functie is handig wanneer u een unieke naam voor een resource toocreate nodig. U opgeven parameterwaarden die Hallo uniciteitsbereik voor Hallo resultaat beperken. U kunt opgeven of de naam van de Hallo unieke omlaag toosubscription, resourcegroep of implementatie. 

Hallo geretourneerde waarde is niet een willekeurige tekenreeks op, maar in plaats daarvan Hallo resultaat van een hash-functie. Hallo geretourneerde waarde 13 tekens bevatten. Het is niet uniek. U kunt toocombine Hallo-waarde met een voorvoegsel van uw naming convention toocreate een beschrijvende naam. Hallo volgende voorbeeld ziet u de indeling Hallo Hallo waarde geretourneerd. Hallo werkelijke waarde verschilt per Hallo parameters opgegeven.

    tcvhiyu5h2o5o

Hallo volgen voorbeelden laten zien hoe toouse uniqueString toocreate een unieke waarde voor vaak gebruikte niveaus.

Uniek binnen het bereik toosubscription

```json
"[uniqueString(subscription().subscriptionId)]"
```

Uniek binnen het bereik tooresource groep

```json
"[uniqueString(resourceGroup().id)]"
```

Uniek binnen het bereik toodeployment voor een resourcegroep

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

Hallo volgende voorbeeld ziet u hoe toocreate een unieke naam voor een opslagaccount op basis van de resourcegroep. In de resourcegroep hello, Hallo naam is niet uniek als Hallo samengesteld dezelfde manier.

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a>Retourwaarde

Een tekenreeks met 13 tekens.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld retourneert de resultaten van uniquestring:

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

## <a name="uri"></a>URI
`uri (baseUri, relativeUri)`

Maakt een absolute URI door Hallo baseUri en Hallo relativeUri tekenreeks te combineren.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| baseUri |Ja |Tekenreeks |Hallo basis-uri-tekenreeks. |
| relativeUri |Ja |Tekenreeks |Hallo relatieve uri tekenreeks tooadd toohello basis-uri-tekenreeks. |

waarde voor Hallo Hallo **baseUri** parameter kan een specifiek bestand bevatten, maar alleen het basispad hello wordt gebruikt tijdens het construeren van Hallo URI. Bijvoorbeeld, doorgeven `http://contoso.com/resources/azuredeploy.json` als Hallo baseUri parameter resulteert in een basis-URI van `http://contoso.com/resources/`.

### <a name="return-value"></a>Retourwaarde

Een tekenreeks voor Hallo absolute URI voor Hallo basis en relatieve waarden.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld ziet u hoe tooconstruct een koppeling tooa geneste sjabloon op basis van Hallo-waarde van sjabloon voor bovenliggend Hallo.

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

Hallo volgende voorbeeld wordt getoond hoe toouse uri, uriComponent, en uriComponentToString:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| uriOutput | Tekenreeks | http://contoso.com/resources/Nested/azuredeploy.JSON |
| componentOutput | Tekenreeks | HTTP%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON |
| toStringOutput | Tekenreeks | http://contoso.com/resources/Nested/azuredeploy.JSON |

<a id="uricomponent" />

## <a name="uricomponent"></a>uriComponent
`uricomponent(stringToEncode)`

Codeert een URI.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| stringToEncode |Ja |Tekenreeks |Hallo waarde tooencode. |

### <a name="return-value"></a>Retourwaarde

Een tekenreeks van Hallo URI gecodeerde waarde.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld wordt getoond hoe toouse uri, uriComponent, en uriComponentToString:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| uriOutput | Tekenreeks | http://contoso.com/resources/Nested/azuredeploy.JSON |
| componentOutput | Tekenreeks | HTTP%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON |
| toStringOutput | Tekenreeks | http://contoso.com/resources/Nested/azuredeploy.JSON |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a>uriComponentToString
`uriComponentToString(uriEncodedString)`

Retourneert dat een tekenreeks van een URI-gecodeerde waarde.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| uriEncodedString |Ja |Tekenreeks |Hallo URI-gecodeerde waarde tooconvert tooa tekenreeks. |

### <a name="return-value"></a>Retourwaarde

Een gecodeerde tekenreeks van URI gecodeerde waarde.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld wordt getoond hoe toouse uri, uriComponent, en uriComponentToString:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| uriOutput | Tekenreeks | http://contoso.com/resources/Nested/azuredeploy.JSON |
| componentOutput | Tekenreeks | HTTP%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON |
| toStringOutput | Tekenreeks | http://contoso.com/resources/Nested/azuredeploy.JSON |


## <a name="next-steps"></a>Volgende stappen
* Zie voor een beschrijving van de secties Hallo in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).
* toomerge meerdere sjablonen Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).
* een opgegeven aantal keren tooiterate bij het maken van een type resource, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).
* toosee hoe toodeploy Hallo sjabloon die u hebt gemaakt, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).

