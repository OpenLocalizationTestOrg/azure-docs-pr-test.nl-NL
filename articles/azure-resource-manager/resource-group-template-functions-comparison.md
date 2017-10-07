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
# <a name="comparison-functions-for-azure-resource-manager-templates"></a>Vergelijking van functies voor Azure Resource Manager-sjablonen

Resource Manager biedt een aantal functies voor het maken van vergelijkingen in uw sjablonen.

* [is gelijk aan](#equals)
* [groter](#greater)
* [greaterOrEquals](#greaterorequals)
* [minder](#less)
* [lessOrEquals](#lessorequals)

## <a name="equals"></a>is gelijk aan
`equals(arg1, arg2)`

Controleert of twee waarden gelijk zijn aan elkaar.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |int, string, matrix of object |Hallo eerste waarde toocheck op gelijkheid. |
| Arg2 |Ja |int, string, matrix of object |Hallo tweede waarde toocheck op gelijkheid. |

### <a name="return-value"></a>Retourwaarde

Retourneert **True** als Hallo waarden gelijk zijn, anders wordt **False**.

### <a name="remarks"></a>Opmerkingen

Hallo gelijk is aan de functie wordt vaak gebruikt met Hallo `condition` tootest element of een resource wordt geïmplementeerd.

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

### <a name="example"></a>Voorbeeld

Hallo-voorbeeldsjabloon verschillende soorten waarden voor gelijkheid wordt gecontroleerd. Standaardwaarden voor alle Hallo retourneren True.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| checkInts | BOOL | True |
| checkStrings | BOOL | True |
| checkArrays | BOOL | True |
| checkObjects | BOOL | True |


Hallo volgende voorbeeld wordt [niet](resource-group-template-functions-logical.md#not) met **gelijk is aan**.

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

Hallo-uitvoer van het voorgaande voorbeeld Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| checkNotEquals | BOOL | True |


## <a name="greater"></a>groter
`greater(arg1, arg2)`

Controleert of de eerste waarde Hallo groter dan de tweede waarde Hallo is.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |int of string |de eerste waarde Hallo voor Hallo groter vergelijking. |
| Arg2 |Ja |int of string |tweede waarde Hallo voor Hallo groter vergelijking. |

### <a name="return-value"></a>Retourwaarde

Retourneert **True** als de eerste waarde Hallo groter is dan de tweede waarde hello, anders wordt **False**.

### <a name="example"></a>Voorbeeld

Hallo-voorbeeldsjabloon controleert of Hallo één waarde groter is dan Hallo andere.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| checkInts | BOOL | False |
| checkStrings | BOOL | True |


## <a name="greaterorequals"></a>greaterOrEquals
`greaterOrEquals(arg1, arg2)`

Controleert of de eerste waarde Hallo groter dan of gelijk toohello tweede waarde.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |int of string |de eerste waarde Hallo voor vergelijking van Hallo groter of gelijk zijn. |
| Arg2 |Ja |int of string |tweede waarde Hallo voor vergelijking van Hallo groter of gelijk zijn. |

### <a name="return-value"></a>Retourwaarde

Retourneert **True** als de eerste waarde Hallo tweede waarde groter dan of gelijk toohello; anders **False**.

### <a name="example"></a>Voorbeeld

Hallo-voorbeeldsjabloon controleert of Hallo één waarde groter dan of gelijk toohello andere.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| checkInts | BOOL | False |
| checkStrings | BOOL | True |



## <a name="less"></a>minder
`less(arg1, arg2)`

Controleert of de eerste waarde Hallo kleiner is dan Hallo tweede waarde.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |int of string |de eerste waarde Hallo voor Hallo minder vergelijking. |
| Arg2 |Ja |int of string |tweede waarde Hallo voor Hallo minder vergelijking. |

### <a name="return-value"></a>Retourwaarde

Retourneert **True** als Hallo eerste waarde kleiner dan Hallo is tweede waarde; anders **False**.

### <a name="example"></a>Voorbeeld

Hallo-voorbeeldsjabloon controleert of Hallo een waarde lager is dan andere Hallo.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| checkInts | BOOL | True |
| checkStrings | BOOL | False |


## <a name="lessorequals"></a>lessOrEquals
`lessOrEquals(arg1, arg2)`

Controleert of de eerste waarde Hallo kleiner dan of gelijk toohello tweede waarde.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |int of string |de eerste waarde Hallo voor Hallo kleiner of gelijk is aan vergelijking. |
| Arg2 |Ja |int of string |tweede waarde voor Hallo minder Hallo of gelijk aan de vergelijking. |

### <a name="return-value"></a>Retourwaarde

Retourneert **True** als de eerste waarde Hallo kleiner dan of gelijk is toohello tweede waarde; anders **False**.

### <a name="example"></a>Voorbeeld

Hallo voorbeeldsjabloon controleert of Hallo één waarde kleiner dan of gelijk is toohello andere.

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

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| checkInts | BOOL | True |
| checkStrings | BOOL | False |



## <a name="next-steps"></a>Volgende stappen
* Zie voor een beschrijving van de secties Hallo in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).
* toomerge meerdere sjablonen Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).
* een opgegeven aantal keren tooiterate bij het maken van een type resource, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).
* toosee hoe toodeploy Hallo sjabloon die u hebt gemaakt, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).

