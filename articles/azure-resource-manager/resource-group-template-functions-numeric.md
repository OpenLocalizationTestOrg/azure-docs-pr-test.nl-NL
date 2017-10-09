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
# <a name="numeric-functions-for-azure-resource-manager-templates"></a>Numerieke functies voor Azure Resource Manager-sjablonen

Resource Manager biedt Hallo functies voor het werken met gehele getallen te volgen:

* [toevoegen](#add)
* [copyIndex](#copyindex)
* [div](#div)
* [Float](#float)
* [int](#int)
* [min](#min)
* [maximale](#max)
* [Mod](#mod)
* [mul](#mul)
* [Sub](#sub)

<a id="add" />

## <a name="add"></a>toevoegen
`add(operand1, operand2)`

Retourneert Hallo de som van de twee opgegeven getallen Hallo.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- | 
|operand1 |Ja |int |Eerste nummer tooadd. |
|operand2 |Ja |int |Het tweede nummer tooadd. |

### <a name="return-value"></a>Retourwaarde

Een geheel getal dat Hallo som van Hallo parameters bevat.

### <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld voegt twee parameters.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| addResult | int | 8 |

<a id="copyindex" />

## <a name="copyindex"></a>copyIndex
`copyIndex(loopName, offset)`

Retourneert Hallo index van een lus herhaling. 

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| loopName | Nee | Tekenreeks | Hallo de naam van de lus Hallo voor het ophalen van Hallo herhaling. |
| offset |Nee |int |Hallo tooadd toohello op nul gebaseerde herhaling getalwaarde. |

### <a name="remarks"></a>Opmerkingen

Deze functie wordt altijd gebruikt met een **kopie** object. Als geen waarde is opgegeven voor **offset**, Hallo huidige herhaling waarde geretourneerd. Hallo herhaling waarde begint bij nul.

Hallo **loopName** eigenschap kunt u toospecify of copyIndex tooa resource herhaling of eigenschap iteratie verwijst. Als geen waarde is opgegeven voor **loopName**, Hallo huidige resource type herhaling wordt gebruikt. Geef een waarde voor **loopName** wanneer voor een eigenschap. 
 
Voor een volledige beschrijving van het gebruik van **copyIndex**, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).

### <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld ziet u een kopie lus Hallo indexwaarde en opgenomen in het Hallo-naam. 

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

### <a name="return-value"></a>Retourwaarde

Een geheel getal dat Hallo huidige index van Hallo herhaling.

<a id="div" />

## <a name="div"></a>div
`div(operand1, operand2)`

Retourneert Hallo gehele getal van de twee opgegeven getallen Hallo.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| operand1 |Ja |int |Hallo-nummer wordt verdeeld. |
| operand2 |Ja |int |Hallo-nummer dat is gebruikt toodivide. Mag niet 0 zijn. |

### <a name="return-value"></a>Retourwaarde

Deling van een geheel getal dat Hallo getal.

### <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld wordt één parameter door een andere parameter verdeeld.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| divResult | int | 2 |

<a id="float" />

## <a name="float"></a>Float
`float(arg1)`

Hallo waarde tooa Drijvendekommagetal converteert. U deze functie alleen gebruiken als aangepaste parameters doorgegeven tooan toepassing, zoals een logische App.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |String of int. |Hallo waarde tooconvert tooa Drijvendekommagetal. |

### <a name="return-value"></a>Retourwaarde
Een drijvende komma.

### <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld ziet u hoe toouse float toopass parameters tooa logische App:

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

## <a name="int"></a>int
`int(valueToConvert)`

Converteert Hallo opgegeven waarde tooan geheel getal.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| valueToConvert |Ja |String of int. |Hallo waarde tooconvert tooan geheel getal. |

### <a name="return-value"></a>Retourwaarde

Een geheel getal van Hallo geconverteerd-waarde.

### <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld wordt geconverteerd Hallo gebruiker opgegeven parameter waarde toointeger.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| intResult | int | 4 |


<a id="min" />

## <a name="min"></a>min.
`min (arg1)`

Retourneert Hallo minimumwaarde van een matrix van gehele getallen of een door komma's gescheiden lijst met gehele getallen zijn.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |matrix van gehele getallen of door komma's gescheiden lijst met gehele getallen |Hallo verzameling tooget Hallo minimumwaarde. |

### <a name="return-value"></a>Retourwaarde

Een geheel getal dat minimumwaarde uit Hallo-verzameling.

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
`max (arg1)`

Retourneert Hallo de maximumwaarde van een matrix van gehele getallen of een door komma's gescheiden lijst met gehele getallen.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |matrix van gehele getallen of door komma's gescheiden lijst met gehele getallen |Hallo verzameling tooget Hallo maximale waarde. |

### <a name="return-value"></a>Retourwaarde

Een geheel getal dat de maximale waarde Hallo uit Hallo-verzameling.

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

<a id="mod" />

## <a name="mod"></a>Mod
`mod(operand1, operand2)`

Hallo rest van de deling van Hallo geheel getal met behulp van twee opgegeven getallen Hallo retourneert.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| operand1 |Ja |int |Hallo-nummer wordt verdeeld. |
| operand2 |Ja |int |Hallo-nummer dat is gebruikt toodivide mag niet 0 zijn. |

### <a name="return-value"></a>Retourwaarde
Een geheel getal dat Hallo resterende hoeveelheid.

### <a name="example"></a>Voorbeeld

Hallo retourneert volgende voorbeeld Hallo restgetal één parameter door een andere parameter.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| modResult | int | 1 |

<a id="mul" />

## <a name="mul"></a>mul
`mul(operand1, operand2)`

Retourneert Hallo vermeerdering van Hallo twee opgegeven getallen.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| operand1 |Ja |int |Eerste nummer toomultiply. |
| operand2 |Ja |int |Het tweede nummer toomultiply. |

### <a name="return-value"></a>Retourwaarde

Een Hallo van geheel getal dat vermenigvuldigen.

### <a name="example"></a>Voorbeeld

Hallo volgt vermenigvuldigen één parameter door een andere parameter.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| mulResult | int | 15 |

<a id="sub" />

## <a name="sub"></a>Sub
`sub(operand1, operand2)`

Retourneert Hallo aftrekken van Hallo twee opgegeven getallen.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| operand1 |Ja |int |Hallo-nummer dat wordt afgetrokken van. |
| operand2 |Ja |int |Hallo-nummer dat wordt afgetrokken. |

### <a name="return-value"></a>Retourwaarde
Een Hallo van geheel getal dat aftrekken.

### <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld wordt één parameter van een andere parameter afgetrokken.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| subResult | int | 4 |

## <a name="next-steps"></a>Volgende stappen
* Zie voor een beschrijving van de secties Hallo in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).
* toomerge meerdere sjablonen Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).
* een opgegeven aantal keren tooiterate bij het maken van een type resource, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).
* toosee hoe toodeploy Hallo sjabloon die u hebt gemaakt, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).

