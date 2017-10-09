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
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a>Matrix en object-functies voor Azure Resource Manager-sjablonen 

Resource Manager biedt een aantal functies voor het werken met matrices en objecten.

* [matrix](#array)
* [coalesce](#coalesce)
* [concat](#concat)
* [bevat](#contains)
* [createArray](#createarray)
* [leeg](#empty)
* [eerste](#first)
* [snijpunt](#intersection)
* [JSON](#json)
* [laatste](#last)
* [lengte](#length)
* [min](#min)
* [maximale](#max)
* [bereik](#range)
* [overslaan](#skip)
* [duren](#take)
* [Union](#union)

een matrix van tekenreekswaarden gescheiden door een waarde tooget Zie [splitsen](resource-group-template-functions-string.md#split).

<a id="array" />

## <a name="array"></a>matrix
`array(convertToArray)`

De waardematrix tooan Hallo converteert.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| convertToArray |Ja |int, string, matrix of object |Hallo waarde tooconvert tooan matrix. |

### <a name="return-value"></a>Retourwaarde

Een matrix.

### <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld ziet u hoe toouse Hallo Matrixfunctie met verschillende typen.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| intOutput | Matrix | [1] |
| stringOutput | Matrix | ["a"] |
| objectOutput | Matrix | [{"a": "b", "c": "d"}] |

<a id="coalesce" />

## <a name="coalesce"></a>Coalesce
`coalesce(arg1, arg2, arg3, ...)`

Retourneert de eerste niet-null-waarde van Hallo-parameters. Lege tekenreeksen, matrices leeg en lege objecten zijn niet null.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |int, string, matrix of object |Hallo eerste waarde tootest voor null. |
| Als u meer argumenten |Nee |int, string, matrix of object |Aanvullende waarden tootest voor null. |

### <a name="return-value"></a>Retourwaarde

Hallo-waarde van Hallo eerste niet-null-parameters, dit kan een string, int, matrix of object. Null als alle parameters leeg zijn. 

### <a name="example"></a>Voorbeeld

Hallo ziet volgende voorbeeld Hallo-uitvoer van verschillende coalesce worden gebruikt.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| stringOutput | Tekenreeks | Standaard |
| intOutput | int | 1 |
| objectOutput | Object | {{'eerste': 'standaard'} |
| arrayOutput | Matrix | [1] |
| emptyOutput | BOOL | True |

<a id="concat" />

## <a name="concat"></a>concat
`concat(arg1, arg2, arg3, ...)`

Combineert meerdere matrices en retourneert Hallo samengevoegd matrix, of meerdere tekenreekswaarden combineert en retourneert Hallo samengevoegd tekenreeks. 

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |matrix of tekenreeks |Hallo eerste matrix of tekenreeks op voor de samenvoeging. |
| Extra argumenten |Nee |matrix of tekenreeks |Aanvullende matrices of tekenreeksen in opeenvolgende volgorde voor de samenvoeging. |

Deze functie kan duren voordat een willekeurig aantal argumenten en tekenreeksen of matrices voor Hallo parameters kan accepteren.

### <a name="return-value"></a>Retourwaarde
Een tekenreeks of matrix met samengevoegde waarden.

### <a name="example"></a>Voorbeeld

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

<a id="contains" />

## <a name="contains"></a>Bevat
`contains(container, itemToFind)`

Controleert of een matrix een waarde bevat, een object een sleutel bevat of een tekenreeks een subtekenreeks bevat.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| container |Ja |Array, object of een tekenreeks |Hallo-waarde die Hallo waarde toofind bevat. |
| itemToFind |Ja |String of int. |Hallo waarde toofind. |

### <a name="return-value"></a>Retourwaarde

**De waarde True** als Hallo item gevonden, anders wordt is **False**.

### <a name="example"></a>Voorbeeld

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

<a id="createarray" />

## <a name="createarray"></a>createarray
`createArray (arg1, arg2, arg3, ...)`

Maakt een matrix van Hallo-parameters.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |Tekenreeks, geheel getal, matrix of Object |Hallo eerste waarde in Hallo matrix. |
| Extra argumenten |Nee |Tekenreeks, geheel getal, matrix of Object |Aanvullende waarden in Hallo matrix. |

### <a name="return-value"></a>Retourwaarde

Een matrix.

### <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld wordt getoond hoe toouse createArray met verschillende typen:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| stringArray | Matrix | ["a", "b", "c"] |
| intArray | Matrix | [1, 2, 3] |
| objectArray | Matrix | [{"een": "a", "twee": "b", "drie": "c"}] |
| arrayArray | Matrix | [[' een', 'twee', 'drie']] |

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

### <a name="example"></a>Voorbeeld

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

<a id="first" />

## <a name="first"></a>eerste
`first(arg1)`

Retourneert Hallo eerste element van Hallo matrix of het eerste teken van Hallo tekenreeks.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |matrix of tekenreeks |Hallo waarde tooretrieve Hallo eerste element of teken. |

### <a name="return-value"></a>Retourwaarde

Hallo type (string, int, matrix of object) Hallo eerste element in een matrix of Hallo eerste teken van een tekenreeks.

### <a name="example"></a>Voorbeeld

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

<a id="intersection" />

## <a name="intersection"></a>snijpunt
`intersection(arg1, arg2, arg3, ...)`

Retourneert een matrix of object met Hallo standaardelementen van Hallo-parameters.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |matrix of object |Hallo eerste waarde toouse voor het zoeken naar algemene elementen. |
| Arg2 |Ja |matrix of object |Hallo tweede waarde toouse voor het zoeken naar algemene elementen. |
| Extra argumenten |Nee |matrix of object |Aanvullende waarden toouse voor het zoeken naar algemene elementen. |

### <a name="return-value"></a>Retourwaarde

Een matrix of object met Hallo algemene elementen.

### <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld wordt getoond hoe toouse snijpunt met matrices en objecten:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| objectOutput | Object | {"een": "a", "3": "c"} |
| arrayOutput | Matrix | ["twee", "drie"] |


## <a name="json"></a>JSON
`json(arg1)`

Retourneert een JSON-object.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |Tekenreeks |Hallo waarde tooconvert tooJSON. |


### <a name="return-value"></a>Retourwaarde

Hallo JSON-object van het Hallo-opgegeven tekenreeks of een leeg object wanneer **null** is opgegeven.

### <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld wordt getoond hoe toouse snijpunt met matrices en objecten:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| jsonOutput | Object | {"a": "b"} |
| nullOutput | Booleaanse waarde | True |

<a id="last" />

## <a name="last"></a>laatste
`last (arg1)`

Retourneert Hallo laatste element van de matrix Hallo of laatste teken van het Hallo-tekenreeks.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |matrix of tekenreeks |Hallo waarde tooretrieve Hallo laatste element of teken. |

### <a name="return-value"></a>Retourwaarde

Hallo type (string, int, matrix of object) Hallo laatste element in een matrix of laatste teken Hallo van een tekenreeks.

### <a name="example"></a>Voorbeeld

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

<a id="length" />

## <a name="length"></a>lengte
`length(arg1)`

Retourneert het aantal elementen Hallo in een matrix of de tekens in een tekenreeks.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |matrix of tekenreeks |Hallo toouse voor het ophalen van het aantal elementen Hallo matrix of tekenreeks toouse voor het ophalen van het aantal tekens Hallo Hallo. |

### <a name="return-value"></a>Retourwaarde

Een int. 

### <a name="example"></a>Voorbeeld

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

U kunt deze functie gebruiken met een matrix toospecify Hallo aantal iteraties bij het maken van resources. Hallo in Hallo voorbeeld te volgen, parameter **siteNames** tooan matrix van namen toouse verwijzen bij het maken van websites Hallo.

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

Zie voor meer informatie over het gebruik van deze functie met een matrix [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).

<a id="min" />

## <a name="min"></a>min.
`min(arg1)`

Retourneert Hallo minimumwaarde van een matrix van gehele getallen of een door komma's gescheiden lijst met gehele getallen zijn.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |matrix van gehele getallen of door komma's gescheiden lijst met gehele getallen |Hallo verzameling tooget Hallo minimumwaarde. |

### <a name="return-value"></a>Retourwaarde

Een int die Hallo minimale waarde vertegenwoordigt.

### <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld wordt getoond hoe toouse min met een matrix en een lijst met gehele getallen zijn:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| arrayOutput | int | 0 |
| intOutput | int | 0 |

<a id="max" />

## <a name="max"></a>Maximum aantal
`max(arg1)`

Retourneert Hallo de maximumwaarde van een matrix van gehele getallen of een door komma's gescheiden lijst met gehele getallen.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |matrix van gehele getallen of door komma's gescheiden lijst met gehele getallen |Hallo verzameling tooget Hallo maximale waarde. |

### <a name="return-value"></a>Retourwaarde

Een int die de maximale waarde Hallo vertegenwoordigt.

### <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld wordt getoond hoe toouse max met een matrix en een lijst met gehele getallen zijn:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| arrayOutput | int | 5 |
| intOutput | int | 5 |

<a id="range" />

## <a name="range"></a>bereik
`range(startingInteger, numberOfElements)`

Maakt een matrix van gehele getallen van een geheel getal beginnen en met een aantal items.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| startingInteger |Ja |int |Hallo eerste geheel getal in Hallo matrix. |
| numberofElements |Ja |int |Hallo-nummer van gehele getallen in de matrix Hallo. |

### <a name="return-value"></a>Retourwaarde

Een matrix van gehele getallen.

### <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld ziet u hoe toouse bereikfunctie Hallo:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| rangeOutput | Matrix | [5, 6, 7] |

<a id="skip" />

## <a name="skip"></a>Overslaan
`skip(originalValue, numberToSkip)`

Retourneert een matrix met alle Hallo elementen nadat Hallo getal in Hallo-matrix opgegeven, of een tekenreeks waarin alle tekens worden Hallo retourneert nadat Hallo nummer in Hallo-tekenreeks opgegeven.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| originalValue |Ja |matrix of tekenreeks |Hallo toouse matrix of tekenreeks voor het overslaan. |
| numberToSkip |Ja |int |Hallo aantal elementen of tekens tooskip. Als deze waarde 0 of minder is, alle elementen Hallo of tekens in Hallo-waarde worden geretourneerd. Als deze groter dan Hallo lengte van Hallo matrix of tekenreeks is, een lege matrix of tekenreeks geretourneerd. |

### <a name="return-value"></a>Retourwaarde

Een matrix of tekenreeks zijn.

### <a name="example"></a>Voorbeeld

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

<a id="take" />

## <a name="take"></a>duren
`take(originalValue, numberToTake)`

Retourneert een matrix met Hallo aantal elementen vanaf opgegeven Hallo Hallo matrix is gestart, of een tekenreeks met Hallo opgegeven aantal tekens vanaf het begin van het Hallo-tekenreeks Hallo.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| originalValue |Ja |matrix of tekenreeks |Hallo matrix of tekenreeks tootake Hallo elementen uit. |
| numberToTake |Ja |int |Hallo aantal elementen of tekens tootake. Als deze waarde 0 of minder is, wordt een lege matrix of tekenreeks geretourneerd. Als het is groter dan de lengte Hallo Hallo gegeven matrix of tekenreeks, worden alle Hallo-elementen in het Hallo-matrix of tekenreeks geretourneerd. |

### <a name="return-value"></a>Retourwaarde

Een matrix of tekenreeks zijn.

### <a name="example"></a>Voorbeeld

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

<a id="union" />

## <a name="union"></a>Union
`union(arg1, arg2, arg3, ...)`

Retourneert een matrix of object met alle elementen van Hallo-parameters. Dubbele waarden of sleutels zijn slechts één keer wordt opgenomen.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |matrix of object |Hallo eerste waarde toouse om lid te worden elementen. |
| Arg2 |Ja |matrix of object |Hallo tweede waarde toouse om lid te worden elementen. |
| Extra argumenten |Nee |matrix of object |Aanvullende waarden toouse om lid te worden elementen. |

### <a name="return-value"></a>Retourwaarde

Een matrix of object.

### <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld wordt getoond hoe toouse union met matrices en objecten:

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| objectOutput | Object | {"een": "a", "twee": "b", "drie": "c", "4": "d", "vijf": "e"} |
| arrayOutput | Matrix | ['een', 'twee', 'drie', "vier"] |

## <a name="next-steps"></a>Volgende stappen
* Zie voor een beschrijving van de secties Hallo in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).
* toomerge meerdere sjablonen Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).
* een opgegeven aantal keren tooiterate bij het maken van een type resource, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).
* toosee hoe toodeploy Hallo sjabloon die u hebt gemaakt, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).

