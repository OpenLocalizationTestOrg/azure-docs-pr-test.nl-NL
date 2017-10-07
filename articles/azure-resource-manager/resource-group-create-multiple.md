---
title: aaaDeploy meerdere exemplaren van Azure-resources | Microsoft Docs
description: Kopieerbewerking en matrices in een Azure Resource Manager-sjabloon tooiterate meerdere keren gebruiken bij het implementeren van resources.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 94d95810-a87b-460f-8e82-c69d462ac3ca
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/26/2017
ms.author: tomfitz
ms.openlocfilehash: a3bd42f694053317c30b639c33dc4efae41a9a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a>Implementeren van meerdere exemplaren van een resource of eigenschap in Azure Resource Manager-sjablonen
Dit onderwerp leest u hoe tooiterate in uw Azure Resource Manager-sjabloon toocreate meerdere exemplaren van een resource of meerdere exemplaren van een eigenschap van een resource.

Als u moet tooadd logica tooyour sjabloon waarmee u toospecify of een resource wordt geïmplementeerd, Zie [voorwaardelijk implementeren resource](#conditionally-deploy-resource).

## <a name="resource-iteration"></a>Resource herhaling
toocreate meerdere exemplaren van een brontype toevoegen een `copy` element toohello brontype. Hallo aantal iteraties en een naam voor deze lus opgeven in Hallo kopie-element. Hallo count-waarde moet een positief geheel getal zijn en mag niet meer dan 800. Resource Manager maakt Hallo resources parallel. Hallo volgorde waarin ze zijn gemaakt kan daarom niet worden gegarandeerd. herhaald toocreate resources in de juiste volgorde, Zie [seriële kopiëren](#serial-copy). 

Hallo resource toocreate wordt meerdere keren Hallo volgende indeling:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        }
    ],
    "outputs": {}
}
```

U ziet dat Hallo naam van elke resource bevat Hallo `copyIndex()` functie de huidige herhaling Hallo in Hallo lus retourneert. `copyIndex()`is gebaseerd op nul. In dat geval Hallo voorbeeld te volgen:

```json
"name": "[concat('storage', copyIndex())]",
```

Deze namen maakt:

* storage0
* storage1
* storage2.

toooffset hello indexwaarde, kunt u een waarde in de functie copyIndex() Hallo doorgeven. Hallo aantal iteraties tooperform is nog steeds opgegeven in Hallo kopie element, maar Hallo-waarde van copyIndex wordt gecompenseerd door Hallo opgegeven waarde. In dat geval Hallo voorbeeld te volgen:

```json
"name": "[concat('storage', copyIndex(1))]",
```

Deze namen maakt:

* storage1
* storage2
* storage3

Hallo kopieerbewerking is handig bij het werken met matrices omdat u elk element in de matrix Hallo kunt doorlopen. Gebruik Hallo `length` functie op Hallo matrix toospecify Hallo aantal voor iteraties, en `copyIndex` tooretrieve Hallo huidige index in Hallo matrix. In dat geval Hallo voorbeeld te volgen:

```json
"parameters": { 
  "org": { 
     "type": "array", 
     "defaultValue": [ 
         "contoso", 
         "fabrikam", 
         "coho" 
      ] 
  }
}, 
"resources": [ 
  { 
      "name": "[concat('storage', parameters('org')[copyIndex()])]", 
      "copy": { 
         "name": "storagecopy", 
         "count": "[length(parameters('org'))]" 
      }, 
      ...
  } 
]
```

Deze namen maakt:

* storagecontoso
* storagefabrikam
* storagecoho

## <a name="serial-copy"></a>Seriële kopiëren

Wanneer u Hallo kopie element toocreate implementeert meerdere exemplaren van een resourcetype Resource Manager worden standaard de instanties parallel. U kunt echter toospecify die Hallo resources worden geïmplementeerd in de reeks. Bijvoorbeeld bij het bijwerken van een productieomgeving kunt u toostagger Hallo bijgewerkt zodat alleen bepaalde op elk gewenst moment worden bijgewerkt.

Resource Manager biedt de eigenschappen op Hallo kopie-element waarmee u tooserially implementeren meerdere exemplaren. Instellen in element kopiëren Hallo `mode` te**seriële** en `batchSize` toohello aantal exemplaren toodeploy tegelijk. Seriële modus maakt Resource Manager met een afhankelijkheid voor eerdere exemplaren in de lus hello, zodat dit niet één batch gestart totdat de vorige batch Hallo is voltooid.

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

Hallo eigenschap mode accepteert ook **parallelle**, namelijk Hallo-standaardwaarde.

tootest seriële kopiëren zonder dat er feitelijke webbronnen gebruik Hallo-sjabloon die wordt geïmplementeerd leeg geneste sjablonen te volgen:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberToDeploy": {
      "type": "int",
      "minValue": 2,
      "defaultValue": 5
    }
  },
  "resources": [
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "[concat('loop-', copyIndex())]",
      "copy": {
        "name": "iterator",
        "count": "[parameters('numberToDeploy')]",
        "mode": "serial",
        "batchSize": 1
      },
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
          }
        }
      }
    }
  ],
  "outputs": {
  }
}
```

In Hallo implementatiegeschiedenis, merk op dat geneste implementaties Hallo verwerkt in de reeks.

![seriële implementatie](./media/resource-group-create-multiple/serial-copy.png)

Voor een meer realistische scenario implementeert Hallo voorbeeld van de volgende twee instanties op een tijdstip van een Linux-VM uit een geneste sjabloon:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for hello Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for hello Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for hello Public IP used tooaccess hello Virtual Machine."
            }
        },
        "ubuntuOSVersion": {
            "type": "string",
            "defaultValue": "16.04.0-LTS",
            "allowedValues": [
                "12.04.5-LTS",
                "14.04.5-LTS",
                "15.10",
                "16.04.0-LTS"
            ],
            "metadata": {
                "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version."
            }
        }
    },
    "variables": {
        "templatelink": "https://raw.githubusercontent.com/rjmax/Build2017/master/Act1.TemplateEnhancements/Chapter03.LinuxVM.json"
    },
    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "[concat('nestedDeployment',copyIndex())]",
            "type": "Microsoft.Resources/deployments",
            "copy": {
                "name": "myCopySet",
                "count": 4,
                "mode": "serial",
                "batchSize": 2
            },
            "properties": {
                "mode": "Incremental",
                "templateLink": {
                    "uri": "[variables('templatelink')]",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "adminUsername": {
                        "value": "[parameters('adminUsername')]"
                    },
                    "adminPassword": {
                        "value": "[parameters('adminPassword')]"
                    },
                    "dnsLabelPrefix": {
                        "value": "[parameters('dnsLabelPrefix')]"
                    },
                    "ubuntuOSVersion": {
                        "value": "[parameters('ubuntuOSVersion')]"
                    },
                    "index":{
                        "value": "[copyIndex()]"
                    }
                }
            }
        }
    ]
}
```

## <a name="property-iteration"></a>Eigenschap herhaling

toocreate meerdere waarden voor een eigenschap van een resource toevoegen een `copy` matrix in Hallo eigenschappen element. Deze matrix bevat objecten en elk object heeft Hallo volgende eigenschappen:

* naam - Hallo van Hallo eigenschap toocreate meerdere waarden voor
* het aantal waarden toocreate Hallo - tellen
* invoer - object dat Hallo waarden tooassign toohello-eigenschap bevat  

Hallo volgende voorbeeld wordt getoond hoe tooapply `copy` toohello dataDisks-eigenschap op een virtuele machine:

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "copy": [{
          "name": "dataDisks",
          "count": 3,
          "input": {
              "lun": "[copyIndex('dataDisks')]",
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

Merk op dat wanneer u `copyIndex` binnen een iteratie eigenschap u Hallo-naam van Hallo herhaling moet opgeven. U hoeft geen tooprovide Hallo naam gebruikt in combinatie met resource herhaling.

Resource Manager worden uitgevouwen Hallo `copy` matrix tijdens de implementatie. Hallo-naam van de matrix hello wordt Hallo-naam van Hallo-eigenschap. Hallo invoerwaarden worden Hallo objecteigenschappen. Hallo geïmplementeerd sjabloon als volgt uit:

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "dataDisks": [
          {
              "lun": 0,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 1,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 2,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

U kunt resource en de eigenschap iteratie samen gebruiken. Verwijzing Hallo herhaling eigenschap met de naam.

```json
{
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[concat(parameters('vnetname'), copyIndex())]",
    "apiVersion": "2016-06-01",
    "copy":{
        "count": 2,
        "name": "vnetloop"
    },
    "location": "[resourceGroup().location]",
    "properties": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "copy": [
            {
                "name": "subnets",
                "count": 2,
                "input": {
                    "name": "[concat('subnet-', copyIndex('subnets'))]",
                    "properties": {
                        "addressPrefix": "[variables('subnetAddressPrefix')[copyIndex('subnets')]]"
                    }
                }
            }
        ]
    }
}
```

U kunt alleen één exemplaar element opnemen in Hallo-eigenschappen voor elke resource. meerdere objecten toospecify een lus herhaling voor meer dan één eigenschap definiëren in Hallo kopie matrix. Elk object wordt afzonderlijk herhaald. Bijvoorbeeld: toocreate meerdere exemplaren van beide Hallo `frontendIPConfigurations` eigenschap en Hallo `loadBalancingRules` eigenschap op een load balancer beide objecten definiëren die in een element met één exemplaar: 

```json
{
    "name": "[variables('loadBalancerName')]",
    "type": "Microsoft.Network/loadBalancers",
    "properties": {
        "copy": [
          {
              "name": "frontendIPConfigurations",
              "count": 2,
              "input": {
                  "name": "[concat('loadBalancerFrontEnd', copyIndex('frontendIPConfigurations', 1))]",
                  "properties": {
                      "publicIPAddress": {
                          "id": "[variables(concat('publicIPAddressID', copyIndex('frontendIPConfigurations', 1)))]"
                      }
                  }
              }
          },
          {
              "name": "loadBalancingRules",
              "count": 2,
              "input": {
                  "name": "[concat('LBRuleForVIP', copyIndex('loadBalancingRules', 1))]",
                  "properties": {
                      "frontendIPConfiguration": {
                          "id": "[variables(concat('frontEndIPConfigID', copyIndex('loadBalancingRules', 1)))]"
                      },
                      "backendAddressPool": {
                          "id": "[variables('lbBackendPoolID')]"
                      },
                      "protocol": "tcp",
                      "frontendPort": "[variables(concat('frontEndPort' copyIndex('loadBalancingRules', 1))]",
                      "backendPort": "[variables(concat('backEndPort' copyIndex('loadBalancingRules', 1))]",
                      "probe": {
                          "id": "[variables('lbProbeID')]"
                      }
                  }
              }
          }
        ],
        ...
    }
}
```

## <a name="depend-on-resources-in-a-loop"></a>Afhankelijk zijn van bronnen in een lus
U opgeven dat een resource na een andere resource wordt geïmplementeerd met behulp van Hallo `dependsOn` element. een resource die afhankelijk zijn van de verzameling van resources in een lus Hallo toodeploy Hallo naam opgeven van Hallo kopie lus in Hallo dependsOn element. Hallo volgende voorbeeld ziet u hoe toodeploy drie storage-accounts voordat u implementeert Hallo voor virtuele Machine. Hallo volledige virtuele Machine definitie wordt niet weergegeven. U ziet dat Hallo kopie-element heeft naam ingesteld te`storagecopy` en ook Hallo dependsOn element voor Hallo virtuele Machines is ingesteld op een te`storagecopy`.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        },
        {
            "apiVersion": "2015-06-15", 
            "type": "Microsoft.Compute/virtualMachines", 
            "name": "[concat('VM', uniqueString(resourceGroup().id))]",  
            "dependsOn": ["storagecopy"],
            ...
        }
    ],
    "outputs": {}
}
```

## <a name="create-multiple-instances-of-a-child-resource"></a>Meerdere exemplaren van een onderliggende resource maken
U kunt een lus kopie niet gebruiken voor een onderliggende resource. toocreate meerdere exemplaren van een resource die u doorgaans als definiëren in een andere resource genest, moet u in plaats daarvan maken die resource als een resource op het hoogste niveau. U definiëren Hallo relatie met de Hallo bovenliggende resource via Hallo type en de naam eigenschappen.

Stel bijvoorbeeld dat u doorgaans een gegevensset definiëren als een onderliggende bron binnen een gegevensfactory.

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
    "resources": [
    {
        "type": "datasets",
        "name": "exampleDataSet",
        "dependsOn": [
            "exampleDataFactory"
        ],
        ...
    }
}]
```

toocreate meerdere exemplaren van gegevenssets, verplaatst u het buiten Hallo data factory. Hallo gegevensset moet zich op hetzelfde niveau als Hallo gegevensfactory hello, maar nog steeds een onderliggende resource van Hallo-gegevensfactory. U behouden Hallo relatie tussen de gegevensset en data factory via de eigenschappen voor het type en de naam van Hallo. Aangezien het type kan niet meer worden afgeleid van de positie in de sjabloon hello, moet u Hallo volledig gekwalificeerd type Hallo indeling opgeven: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.

tooestablish een bovenliggende/onderliggende relatie met een exemplaar van de gegevensfactory hello, Geef een naam voor de gegevensset Hallo met Hallo bovenliggende resourcenaam. Gebruik de indeling Hallo: `{parent-resource-name}/{child-resource-name}`.  

Hallo toont volgende voorbeeld Hallo implementatie:

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
},
{
    "type": "Microsoft.DataFactory/datafactories/datasets",
    "name": "[concat('exampleDataFactory', '/', 'exampleDataSet', copyIndex())]",
    "dependsOn": [
        "exampleDataFactory"
    ],
    "copy": { 
        "name": "datasetcopy", 
        "count": "3" 
    } 
    ...
}]
```

## <a name="conditionally-deploy-resource"></a>Voorwaardelijk resource implementeren

toospecify of een resource wordt geïmplementeerd, gebruiken Hallo `condition` element. Hallo-waarde voor dit element wordt omgezet tootrue of ONWAAR. Wanneer het Hallo-waarde true is, wordt Hallo resource geïmplementeerd. Wanneer het Hallo-waarde is ingesteld op false, worden Hallo resource wordt niet geïmplementeerd. Bijvoorbeeld: toospecify of een nieuw opslagaccount wordt geïmplementeerd of een bestaand opslagaccount wordt gebruikt, gebruiken:

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

Zie voor een voorbeeld van het gebruik van een wachtwoord of SSH-sleutel toodeploy virtuele machine [gebruikersnaam of SSH voorwaarde sjabloon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).

## <a name="next-steps"></a>Volgende stappen
* Als u toolearn Hallo secties van een sjabloon wilt, Zie [Azure Resource Manager-sjablonen ontwerpen](resource-group-authoring-templates.md).
* toolearn hoe toodeploy uw sjabloon Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).

