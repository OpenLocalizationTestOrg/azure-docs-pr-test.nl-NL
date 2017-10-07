---
title: aaaAzure Resource Manager-sjabloonfuncties - logische | Microsoft Docs
description: Hierin wordt beschreven Hallo functies toouse in een Azure Resource Manager sjabloon toodetermine logische waarden.
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
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a>Logische functies voor Azure Resource Manager-sjablonen

Resource Manager biedt een aantal functies voor het maken van vergelijkingen in uw sjablonen.

* [en](#and)
* [BOOL](#bool)
* [Als](#if)
* [niet](#not)
* [of](#or)

## <a name="and"></a>en
`and(arg1, arg2)`

Controleert of beide parameterwaarden true zijn.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |Booleaanse waarde |eerste waarde toocheck of Hallo is ingesteld op true. |
| Arg2 |Ja |Booleaanse waarde |tweede waarde toocheck of Hallo is ingesteld op true. |

### <a name="return-value"></a>Retourwaarde

Retourneert **True** als beide waarden true, anders wordt zijn **False**.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld ziet u hoe logische toouse-functies.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

Hallo-uitvoer van het voorgaande voorbeeld Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| andExampleOutput | BOOL | False |
| orExampleOutput | BOOL | True |
| notExampleOutput | BOOL | False |


## <a name="bool"></a>BOOL
`bool(arg1)`

Converteert Hallo parameter tooa Boolean-waarde.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |String of int. |Hallo waarde tooconvert tooa Boolean-waarde. |

### <a name="return-value"></a>Retourwaarde
Een Booleaanse waarde Hallo geconverteerd waarde.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld wordt getoond hoe toouse bool met een tekenreeks of een geheel getal.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| trueString | BOOL | True |
| falseString | BOOL | False |
| trueInt | BOOL | True |
| falseInt | BOOL | False |

## <a name="if"></a>Als
`if(condition, trueValue, falseValue)`

Retourneert een waarde op basis van of u een voorwaarde is true of false.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Voorwaarde |Ja |Booleaanse waarde |Hallo waarde toocheck of true is. |
| trueValue |Ja | String, int, object of matrix |Hallo waarde tooreturn wanneer Hallo voorwaarde waar is. |
| falseValue |Ja | String, int, object of matrix |Hallo waarde tooreturn wanneer Hallo voorwaarde onwaar is. |

### <a name="return-value"></a>Retourwaarde

Retourneert een tweede parameter als eerste parameter is **True**; anders retourneert de derde parameter.

### <a name="remarks"></a>Opmerkingen

U kunt deze functie tooconditionally set een broneigenschap te gebruiken. Hallo volgende voorbeeld is niet een volledige sjabloon, maar het Hallo relevante delen voor het instellen van voorwaardelijk Hallo beschikbaarheidsset bevat.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld wordt getoond hoe toouse hello `if` functie.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

Hallo-uitvoer van het voorgaande voorbeeld Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| yesOutput | Tekenreeks | Ja |
| noOutput | Tekenreeks | Er is geen |


## <a name="not"></a>niet
`not(arg1)`

Booleaanse waarde tooits converteert tegenover waarde.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |Booleaanse waarde |Hallo waarde tooconvert. |


### <a name="return-value"></a>Retourwaarde

Retourneert **True** wanneer de parameter is **False**. Retourneert **False** wanneer de parameter is **True**.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld ziet u hoe logische toouse-functies.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

Hallo-uitvoer van het voorgaande voorbeeld Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| andExampleOutput | BOOL | False |
| orExampleOutput | BOOL | True |
| notExampleOutput | BOOL | False |

Hallo volgende voorbeeld wordt **niet** met [gelijk is aan](resource-group-template-functions-comparison.md#equals).

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


## <a name="or"></a>of
`or(arg1, arg2)`

Controleert of de waarde voor de parameter ingesteld op true is.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Arg1 |Ja |Booleaanse waarde |eerste waarde toocheck of Hallo is ingesteld op true. |
| Arg2 |Ja |Booleaanse waarde |tweede waarde toocheck of Hallo is ingesteld op true. |

### <a name="return-value"></a>Retourwaarde

Retourneert **True** als de waarde true, anders wordt is **False**.

### <a name="examples"></a>Voorbeelden

Hallo volgende voorbeeld ziet u hoe logische toouse-functies.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

Hallo-uitvoer van het voorgaande voorbeeld Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| andExampleOutput | BOOL | False |
| orExampleOutput | BOOL | True |
| notExampleOutput | BOOL | False |


## <a name="next-steps"></a>Volgende stappen
* Zie voor een beschrijving van de secties Hallo in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).
* toomerge meerdere sjablonen Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).
* een opgegeven aantal keren tooiterate bij het maken van een type resource, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).
* toosee hoe toodeploy Hallo sjabloon die u hebt gemaakt, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).

