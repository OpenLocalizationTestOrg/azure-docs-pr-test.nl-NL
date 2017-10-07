---
title: Resource Manager aaaAzure sjabloonstructuur en syntaxis | Microsoft Docs
description: Hierin wordt beschreven Hallo structuur en eigenschappen van Azure Resource Manager-sjablonen met behulp van declaratieve JSON-syntaxis.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a>Begrijpen Hallo structuur en syntaxis van Azure Resource Manager-sjablonen
Dit onderwerp beschrijft Hallo-structuur van een Azure Resource Manager-sjabloon. Deze geeft Hallo verschillende secties van de eigenschappen van een sjabloon en Hallo die beschikbaar zijn in deze secties. Hallo sjabloon bestaat uit JSON en uitdrukkingen die u kunt tooconstruct waarden voor uw implementatie te gebruiken. Zie voor een stapsgewijze zelfstudie over het maken van een sjabloon, [maken van uw eerste Azure Resource Manager-sjabloon](resource-manager-create-first-template.md).

## <a name="template-format"></a>Sjabloon
In de meest eenvoudige structuur bevat een sjabloon Hallo volgende elementen:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| Elementnaam | Vereist | Beschrijving |
|:--- |:--- |:--- |
| $schema |Ja |Locatie van Hallo JSON-schema-bestand dat Hallo-versie van de sjabloontaal Hallo beschrijft. Hallo-URL die wordt weergegeven in het voorgaande voorbeeld hello gebruiken. |
| contentVersion |Ja |Versie van de sjabloon hello (zoals 1.0.0.0). U kunt een waarde opgeven voor dit element. Bij het implementeren van resources met behulp van Hallo-sjabloon gebruikt deze waarde kan zijn gebruikte toomake ervoor dat de juiste sjabloon hello wordt gebruikt. |
| parameters |Nee |Waarden die zijn opgegeven voor de implementatie is uitgevoerd toocustomize resources implementeren. |
| variabelen |Nee |De waarden die worden gebruikt als JSON-fragmenten in Hallo sjabloon toosimplify sjabloontaalexpressies. |
| Resources |Ja |Brontypen die worden geïmplementeerd of bijgewerkt in een resourcegroep. |
| uitvoer |Nee |De waarden die na de implementatie worden geretourneerd. |

Elk element bevat eigenschappen die u kunt instellen. Hallo volgende voorbeeld bevat de volledige syntaxis Hallo voor een sjabloon:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-hello parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

We onderzoeken Hallo secties van de sjabloon Hallo in meer detail verderop in dit onderwerp.

## <a name="expressions-and-functions"></a>Expressies en functies
Hallo basic syntaxis van de sjabloon Hallo is JSON. Expressies en functies echter uitbreiden Hallo JSON-waarden zijn beschikbaar in de sjabloon Hallo.  Expressies zijn geschreven in letterlijke JSON-tekenreeks waarvan de eerste en laatste tekens zijn Hallo haken: `[` en `]`respectievelijk. Hallo-waarde van Hallo expressie wordt geëvalueerd wanneer Hallo sjabloon wordt geïmplementeerd. Hoewel geschreven als een letterlijke tekenreeks, zijn Hallo resultaat van de evaluatie van Hallo expressie van een ander JSON-type, zoals een matrix of een geheel getal, afhankelijk van de werkelijke Hallo-expressie.  een letterlijke tekenreeks beginnen met een haakje toohave `[`, maar dit wordt geïnterpreteerd als een expressie niet, voegt u een extra haakje toostart Hallo tekenreeks met `[[`.

Normaal gesproken gebruikt u expressies met functies tooperform bewerkingen voor het configureren van Hallo-implementatie. Net zoals in JavaScript-functieaanroepen die zijn opgemaakt als `functionName(arg1,arg2,arg3)`. U verwijzen naar eigenschappen met behulp van Hallo punt en [index] operators.

Hallo volgende voorbeeld ziet u hoe toouse diverse functies tijdens het construeren van waarden:

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

Zie voor een volledige lijst met sjabloonfuncties Hallo [Azure Resource Manager-sjabloonfuncties](resource-group-template-functions.md). 

## <a name="parameters"></a>Parameters
In Hallo gedeelte parameters van Hallo sjabloon kunt u opgeven welke waarden u invoeren kunt bij het implementeren van Hallo resources. De parameterwaarden van deze kunnen u toocustomize Hallo implementatie door het verstrekken van waarden die zijn aangepast voor een bepaalde omgeving (zoals ontwikkelen, testen en productie). U hebt geen tooprovide parameters in de sjabloon, maar zonder parameters uw sjabloon altijd Hallo zou implementeren dezelfde resources met dezelfde namen, locaties en eigenschappen Hallo.

U kunt parameters definiëren Hello structuur te volgen:

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| Elementnaam | Vereist | Beschrijving |
|:--- |:--- |:--- |
| parameterName |Ja |Naam van Hallo-parameter. Moet een geldige JavaScript-id. |
| type |Ja |Type Hallo parameterwaarde. Zie Hallo lijst met toegestane typen na deze tabel. |
| Standaardwaarde |Nee |De standaardwaarde voor parameter hello, als geen waarde is opgegeven voor parameter Hallo. |
| allowedValues |Nee |Matrix van toegestane waarden voor Hallo parameter toomake ervoor dat de juiste waarde Hallo worden verstrekt. |
| MinValue |Nee |Hallo minimale waarde voor de parameters van het type int, deze waarde is liggen. |
| MaxValue |Nee |Hallo maximale waarde voor de parameters van het type int, deze waarde is liggen. |
| minLength |Nee |minimumlengte voor string, secureString en array typeparameters Hello, deze waarde is liggen. |
| maxLength |Nee |Hallo maximale lengte voor string, secureString en array typeparameters, deze waarde is liggen. |
| description |Nee |Beschrijving van Hallo-parameter die wordt weergegeven toousers via Hallo-portal. |

Hallo toegestane typen en waarden zijn:

* **tekenreeks**
* **secureString**
* **int**
* **BOOL**
* **object** 
* **secureObject**
* **matrix**

een parameter opgegeven als een optioneel, toospecify bieden een defaultValue (kunnen geen lege tekenreeks zijn). 

Als u een parameternaam in de sjabloon die overeenkomt met een parameter in Hallo opdracht toodeploy Hallo sjabloon opgeeft, is het mogelijke verwarring over Hallo-waarden die u opgeeft. Resource Manager lost deze verwarring door toe te voegen Hallo postfix **FromTemplate** toohello sjabloonparameter. Bijvoorbeeld, als u een parameter genaamd opnemen **ResourceGroupName** in uw sjabloon een conflict met de Hallo **ResourceGroupName** parameter in Hallo [ Nieuwe AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet. Tijdens de implementatie, u bent na vragen aan gebruiker tooprovide een waarde voor **ResourceGroupNameFromTemplate**. In het algemeen voorkomt u deze verwarring door te geven geen parameters met Hallo dezelfde naam als parameters die worden gebruikt voor implementatiebewerkingen.

> [!NOTE]
> Alle wachtwoorden, sleutels en andere geheime informatie moeten hello gebruiken **secureString** type. Als u gevoelige gegevens in een JSON-object doorgeven, gebruikt u Hallo **secureObject** type. Sjabloonparameters met secureString of secureObject typen kunnen niet worden gelezen na de implementatie van de resource. 
> 
> Hallo ziet volgende vermelding in de geschiedenis van de implementatie Hallo u bijvoorbeeld Hallo-waarde voor een tekenreeks en object, maar niet voor secureString en secureObject.
>
> ![waarden van de implementatie weergeven](./media/resource-group-authoring-templates/show-parameters.png)  
>

Hallo volgende voorbeeld wordt getoond hoe toodefine parameters:

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

Zie voor hoe tooinput Hallo parameter tijdens de implementatie waarden, [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md). 

## <a name="variables"></a>Variabelen
In de sectie met sjabloonvariabelen hello, kunt u waarden die kunnen worden gebruikt in uw sjabloon opstellen. U hoeft geen toodefine variabelen, maar ze vaak uw sjabloon vereenvoudigen doordat complexe expressies.

U kunt variabelen definiëren Hello structuur te volgen:

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

Hallo volgende voorbeeld wordt getoond hoe toodefine een variabele die is samengesteld uit twee parameterwaarden:

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

Hallo volgende voorbeeld ziet u een variabele die is complex type JSON en variabelen die zijn samengesteld uit andere variabelen:

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a>Resources
In de sectie bronnen Hallo definieert u Hallo-resources die worden geïmplementeerd of bijgewerkt. Deze sectie ophalen ingewikkeld omdat u moet begrijpen Hallo typt u implementeert tooprovide Hallo juiste waarden. Hallo resource-specifieke Zie voor waarden (apiVersion, type en eigenschappen) moet u tooset [resources in Azure Resource Manager-sjablonen definiëren](/azure/templates/). 

U kunt resources definiëren Hello structuur te volgen:

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| Elementnaam | Vereist | Beschrijving |
|:--- |:--- |:--- |
| Voorwaarde | Nee | Booleaanse waarde die aangeeft of Hallo resource wordt geïmplementeerd. |
| apiVersion |Ja |Versie van Hallo REST-API toouse voor het maken van Hallo resource. |
| type |Ja |Type Hallo resource. Deze waarde is een combinatie van Hallo-naamruimte van het Hallo-resourceprovider en Hallo resourcetype (zoals **Microsoft.Storage/storageAccounts**). |
| naam |Ja |Naam van het Hallo-resource. Hallo-naam moet voldoen aan URI onderdeel beperkingen gedefinieerd in RFC3986. Bovendien Azure-services die beschikbaar Hallo resource naam toooutside partijen Hallo naam toomake u dit niet is een poging toospoof valideren een andere identiteit. |
| location |Varieert |Ondersteunde geografische locaties Hallo opgegeven resource. U kunt kiezen uit de beschikbare locaties Hallo, maar doorgaans het zin toopick maakt een sluiten tooyour gebruikers. Meestal ook is het zinvol tooplace resources die met elkaar in Hallo dezelfde communiceren regio. De meeste brontypen die een locatie vereist, maar sommige typen (zoals een roltoewijzing) hoeven niet een locatie. Zie [Resourcelocatie instellen in Azure Resource Manager-sjablonen](resource-manager-template-location.md). |
| tags |Nee |Labels die gekoppeld aan het Hallo-resource zijn. Zie [resources in Azure Resource Manager-sjablonen taggen](resource-manager-template-tags.md). |
| Opmerkingen |Nee |De notities voor resources in uw sjabloon Hallo documenteren |
| Kopiëren |Nee |Als meer dan één exemplaar is vereist, Hallo aantal resources toocreate. Hallo-standaardmodus is parallelle. Seriële mode opgeven wanneer u niet wilt dat alle of resources toodeploy op Hallo Hallo hetzelfde moment. Zie voor meer informatie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md). |
| dependsOn |Nee |Resources die moeten worden geïmplementeerd voordat u deze bron wordt geïmplementeerd. Resource Manager Hallo afhankelijkheden tussen resources geëvalueerd en worden ze geïmplementeerd in de juiste volgorde Hallo. Wanneer u resources zijn niet afhankelijk van elkaar, worden ze geïmplementeerd parallel. Hallo-waarden zijn een door komma's gescheiden lijst van een resource namen of unieke id's voor een resource. Alleen de lijst van resources die zijn geïmplementeerd in deze sjabloon. Bronnen die niet in deze sjabloon zijn gedefinieerd, moeten al bestaan. Vermijd toe te voegen onnodige afhankelijkheden als ze kunnen uw implementatie vertragen en circulaire afhankelijkheden maken. Zie voor instructies over de afhankelijkheden van de instelling [afhankelijkheden definiëren in Azure Resource Manager-sjablonen](resource-group-define-dependencies.md). |
| properties |Nee |Resource-specifieke configuratie-instellingen. Hallo-waarden voor Hallo eigenschappen Hallo dezelfde zijn als u voorzien in de aanvraagtekst Hallo Hallo REST-API (PUT-methode) toocreate Hallo bewerkingsresource Hallo-waarden. U kunt een kopie matrix toocreate ook meerdere exemplaren van een eigenschap opgeven. Zie voor meer informatie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md). |
| Resources |Nee |Onderliggende resources die afhankelijk zijn van Hallo bron wordt gedefinieerd. Geef alleen brontypen die worden toegestaan door het Hallo-schema van Hallo bovenliggende resource. Hallo volledig gekwalificeerde type Hallo onderliggende resource bevat Hallo bovenliggende brontype, zoals **Microsoft.Web/sites/extensions**. Afhankelijkheid van Hallo bovenliggende resource niet geïmpliceerd. U moet deze afhankelijkheid expliciet definiëren. |

Hallo resources sectie bevat een matrix van Hallo resources toodeploy. U kunt ook een matrix van onderliggende resources binnen elke resource definiëren. Het gedeelte van uw resources kan daarom een structuur zoals hebben:

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

Zie voor meer informatie over het definiëren van de onderliggende resources [naam en type voor onderliggende resource in het Resource Manager-sjabloon instellen](resource-manager-template-child-resource.md).

Hallo **voorwaarde** element geeft aan of Hallo resource wordt geïmplementeerd. Hallo-waarde voor dit element wordt omgezet tootrue of ONWAAR. Bijvoorbeeld: toospecify of een nieuw opslagaccount wordt geïmplementeerd, gebruiken:

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

Zie voor een voorbeeld van het gebruik van een nieuwe of bestaande resourcegroep [nieuwe of bestaande voorwaarde sjabloon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).

toospecify of een virtuele machine wordt geïmplementeerd met een wachtwoord of SSH-sleutel, definieert twee versies van Hallo virtuele machine in de sjabloon en het gebruik **voorwaarde** toodifferentiate gebruik. Een parameter die welke scenario toodeploy aangeeft doorgeven.

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

Zie voor een voorbeeld van het gebruik van een wachtwoord of SSH-sleutel toodeploy virtuele machine [gebruikersnaam of SSH voorwaarde sjabloon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).

## <a name="outputs"></a>uitvoer
In sectie Hallo uitvoer geeft u de waarden die worden geretourneerd van de implementatie. Bijvoorbeeld, u kan Hallo URI tooaccess geïmplementeerde resource geretourneerd.

Hallo toont volgende voorbeeld Hallo-structuur van de definitie van een uitvoer:

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| Elementnaam | Vereist | Beschrijving |
|:--- |:--- |:--- |
| outputName |Ja |Naam van de uitvoerwaarde Hallo. Moet een geldige JavaScript-id. |
| type |Ja |Type van de uitvoerwaarde Hallo. Uitvoerwaarden ondersteuning Hallo dezelfde als sjabloon invoerparameters typen. |
| waarde |Ja |De sjabloontaalexpressie dat wordt geëvalueerd en geretourneerd als de waarde voor uitvoer. |

Hallo volgende voorbeeld ziet u een waarde die wordt geretourneerd in Hallo uitvoer sectie.

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

Zie voor meer informatie over het werken met uitvoer [delen status in Azure Resource Manager-sjablonen](best-practices-resource-manager-state.md).

## <a name="template-limits"></a>Limieten voor sjabloon

Hallo-limiet van uw sjabloon too1 MB en elke parameter too64 KB-bestand. Hallo 1 MB limiet geldt toohello eindstatus van Hallo sjabloon nadat deze is uitgebreid met iteratieve resourcedefinities en waarden voor parameters en variabelen. 

Ook bent u beperkt tot:

* 256 parameters
* 256 variabelen
* 800 bronnen (zoals aantal kopieën)
* 64 uitvoerwaarden
* 24.576 tekens in een sjabloonexpressie

U kunt sommige limieten sjabloon met een geneste sjabloon overschrijdt. Zie voor meer informatie [gekoppelde sjablonen gebruiken bij het implementeren van Azure-resources](resource-group-linked-templates.md). tooreduce hello nummer van de parameters en variabelen en uitvoer, kunt u verschillende waarden combineren in een object. Zie voor meer informatie [objecten als parameters](resource-manager-objects-as-parameters.md).

## <a name="next-steps"></a>Volgende stappen
* tooview voltooid sjablonen voor verschillende soorten oplossingen, Zie Hallo [Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates/).
* Zie voor meer informatie over het Hallo-functies die u van binnen een sjabloon gebruiken kunt [Azure Resource Manager-sjabloonfuncties](resource-group-template-functions.md).
* toocombine meerdere sjablonen tijdens de implementatie, Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).
* Mogelijk moet u toouse resources die zijn opgeslagen in een andere resourcegroep. Dit scenario is gebruikelijk dat wanneer u werkt met opslagaccounts of virtuele netwerken die worden gedeeld door meerdere resourcegroepen. Zie voor meer informatie, Hallo [resourceId functie](resource-group-template-functions-resource.md#resourceid).
