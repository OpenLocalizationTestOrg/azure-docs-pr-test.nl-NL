---
title: aaaAzure Resource Manager-sjabloonfuncties - implementatie | Microsoft Docs
description: Hierin wordt beschreven Hallo functies toouse in een Azure Resource Manager sjabloon tooretrieve implementatie-informatie.
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
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a>Implementatie-functies voor Azure Resource Manager-sjablonen 

Resource Manager biedt Hallo volgende fungeert voor het ophalen van waarden in de secties van de sjabloon Hallo en verwante toohello implementatie waarden:

* [implementatie](#deployment)
* [parameters](#parameters)
* [variabelen](#variables)

tooget waarden van resources, resourcegroepen of abonnementen, Zie [Resource functies](resource-group-template-functions-resource.md).

<a id="deployment" />

## <a name="deployment"></a>implementatie
`deployment()`

Retourneert informatie over de huidige implementatiebewerking Hallo.

### <a name="return-value"></a>Retourwaarde

Deze functie retourneert Hallo-object dat wordt doorgegeven tijdens de implementatie. Hallo-eigenschappen in object geretourneerd Hallo verschillen op basis van of hello implementatieobject is doorgegeven als een koppeling of als een in-line-object. Wanneer Hallo implementatieobject wordt doorgegeven in de regel, zoals bij gebruik van Hallo **- sjabloonbestand** parameter in Azure PowerShell toopoint tooa lokaal bestand geretourneerd Hallo-object heeft Hallo volgende indeling:

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

Wanneer Hallo-object doorgegeven als een koppeling, zoals wanneer met behulp van Hallo **- TemplateUri** parameter toopoint tooa extern object Hallo-object wordt geretourneerd als Hallo volgende indeling: 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a>Opmerkingen

U kunt deployment() toolink tooanother sjabloon op basis van het Hallo-URI van Hallo bovenliggende sjabloon gebruiken.

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a>Voorbeeld

Hallo wordt volgende voorbeeld Hallo implementatieobject:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

Hallo retourneert voorgaande voorbeeld Hallo na-object:

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a>parameters
`parameters(parameterName)`

Retourneert een parameterwaarde. Hallo opgegeven parameternaam moet worden gedefinieerd in sectie van de parameters Hallo van Hallo-sjabloon.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| parameterName |Ja |Tekenreeks |Hallo-naam van Hallo parameter tooreturn. |

### <a name="return-value"></a>Retourwaarde

Hallo-waarde van Hallo opgegeven parameter.

### <a name="remarks"></a>Opmerkingen

Doorgaans kunt u parameterwaarden tooset resource gebruiken. Hallo wordt volgende voorbeeld Hallo-naam van de website toohello doorgegeven parameterwaarde tijdens de implementatie.

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld ziet u een vereenvoudigde gebruik van de functie voor Hallo-parameters.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| stringOutput | Tekenreeks | Optie 1 |
| intOutput | int | 1 |
| objectOutput | Object | {"een": "a", "twee": "b"} |
| arrayOutput | Matrix | [1, 2, 3] |
| crossOutput | Tekenreeks | Optie 1 |

<a id="variables" />

## <a name="variables"></a>variabelen
`variables(variableName)`

Retourneert Hallo de waarde van variabele. Hallo opgegeven variabelenaam moet worden gedefinieerd in sectie met sjabloonvariabelen Hallo van Hallo-sjabloon.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Variabelenaam |Ja |Tekenreeks |Hallo-naam van de variabele tooreturn Hallo. |

### <a name="return-value"></a>Retourwaarde

Hallo-waarde van de opgegeven Hallo-variabele.

### <a name="remarks"></a>Opmerkingen

Normaal gesproken u variabelen toosimplify uw sjabloon door slechts één keer complexe waarden samen te stellen. Hallo wordt volgende voorbeeld een unieke naam voor een opslagaccount.

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a>Voorbeeld

Hallo-voorbeeldsjabloon retourneert verschillende waarden van variabelen.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| exampleOutput1 | Tekenreeks | myVariable |
| exampleOutput2 | Matrix | [1, 2, 3, 4] |
| exampleOutput3 | Tekenreeks | myVariable |
| exampleOutput4 |  Object | {{'1': 'value1', 'eigenschap 2': 'waarde2'} |

## <a name="next-steps"></a>Volgende stappen
* Zie voor een beschrijving van de secties Hallo in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).
* toomerge meerdere sjablonen Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).
* een opgegeven aantal keren tooiterate bij het maken van een type resource, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).
* toosee hoe toodeploy Hallo sjabloon die u hebt gemaakt, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).

