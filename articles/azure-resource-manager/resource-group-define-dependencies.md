---
title: de implementatievolgorde aaaSet voor Azure-resources | Microsoft Docs
description: "Hierin wordt beschreven hoe tooset één resource als afhankelijk is van een andere bron tijdens implementatie tooensure resources in de juiste volgorde Hallo zijn geïmplementeerd."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a>Hallo volgorde voor het implementeren van resources in Azure Resource Manager-sjablonen definiëren
Voor een bepaalde bron, kunnen er andere resources moeten bestaan voordat Hallo resource wordt geïmplementeerd. Bijvoorbeeld, moet een SQL-server bestaan voordat u probeert toodeploy een SQL-database. U definiëren deze relatie met het markeren van een resource als afhankelijke op Hallo andere resource. U definieert een afhankelijkheid Hello **dependsOn** element, of met behulp van Hallo **verwijzing** functie. 

Resource Manager evalueert Hallo afhankelijkheden tussen resources en ze worden geïmplementeerd in de afhankelijke volgorde. Wanneer u resources zijn niet afhankelijk van elkaar, worden deze door Resource Manager parallel implementeert. U hoeft alleen toodefine afhankelijkheden voor resources die zijn geïmplementeerd in Hallo dezelfde sjabloon. 

## <a name="dependson"></a>dependsOn
Hallo dependsOn element kunt toodefine één resource als een afhankelijk zijn van een of meer resources, in uw sjabloon. De waarde kan een door komma's gescheiden lijst met resourcenamen zijn. 

Hallo volgende voorbeeld ziet u een virtuele-machineschaalset die afhankelijk zijn van een load balancer, het virtuele netwerk en een lus die meerdere opslagaccounts worden gemaakt. Deze andere resources worden niet weergegeven in het volgende voorbeeld Hallo, maar moeten ze tooexist elders in Hallo-sjabloon.

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

In de Hallo voorgaande voorbeeld, een afhankelijkheid is opgenomen op Hallo-resources die zijn gemaakt via een For-lus kopiëren met de naam **storageLoop**. Zie voor een voorbeeld [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).

Bij het definiëren van afhankelijkheden, kunt u Hallo resource provider-naamruimte en de resource type tooavoid dubbelzinnigheid kunt opnemen. Bijvoorbeeld, tooclarify een load balancer en het virtuele netwerk dat mogelijk Hallo die dezelfde namen als andere resources, gebruik Hallo volgende indeling:

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

Hoewel u mogelijk geneigd toouse dependsOn toomap relaties tussen uw resources, is het belangrijk toounderstand waarom u dit doet. DependsOn is bijvoorbeeld toodocument hoe resources onderling verbonden, niet de juiste aanpak Hallo. U kunt het welke resources zijn gedefinieerd in Hallo dependsOn element na de implementatie kan geen query uitvoeren. Met behulp van dependsOn u mogelijk gevolgen hebben voor implementatietijd omdat Resource Manager niet is geïmplementeerd in parallelle twee resources met een afhankelijkheid. Gebruik in plaats daarvan toodocument relaties tussen bronnen, [resources](/rest/api/resources/resourcelinks).

## <a name="child-resources"></a>Onderliggende resources
Hallo resources eigenschap kunt u toospecify onderliggende resources die zijn gerelateerd toohello resource wordt gedefinieerd. Onderliggende resources kunnen alleen worden gedefinieerd vijf niveaus. Het is belangrijk toonote die een impliciete afhankelijkheid niet is gemaakt tussen een onderliggende resource en Hallo bovenliggende resource. Als u moet onderliggende resource toobe geïmplementeerd na Hallo bovenliggende resource hello, moet u deze afhankelijkheid met Hallo dependsOn eigenschap expliciet vermelden. 

Elke bovenliggende resource accepteert alleen bepaalde resourcetypen als onderliggende resources. Hallo geaccepteerd brontypen die zijn opgegeven in Hallo [sjabloonschema](https://github.com/Azure/azure-resource-manager-schemas) van Hallo bovenliggende resource. Hallo-naam van onderliggende brontype bevat Hallo-naam van Hallo bovenliggende brontype, zoals **Microsoft.Web/sites/config** en **Microsoft.Web/sites/extensions** zijn beide onderliggende resources van Hallo  **Microsoft.Web/sites**.

Hallo volgende voorbeeld ziet u een SQL server en SQL-database. U ziet dat er een expliciete afhankelijkheid is gedefinieerd tussen Hallo SQL-database en SQL server, hoewel Hallo-database een onderliggend element van het Hallo-server is.

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a>verwijzing naar functie
Hallo [verwijst naar functie](resource-group-template-functions-resource.md#reference) wordt een tooderive expressie de waarde van andere JSON naam / waarde-paren of runtime-bronnen. Verwijzingsexpressies declareren impliciet dat één resource afhankelijk van een andere is. Hallo algemene indeling is:

```json
reference('resourceName').propertyPath
```

In Hallo voorbeeld te volgen, een CDN-eindpunt expliciet is afhankelijk van Hallo CDN-profiel en impliciet afhankelijk is van een web-app.

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

U kunt dit element of Hallo dependsOn element toospecify afhankelijkheden, maar u hoeft geen toouse beide voor Hallo dezelfde afhankelijke bron. Gebruik indien mogelijk een impliciete verwijzing tooavoid een onnodige afhankelijkheid toevoegen.

toolearn meer, Zie [verwijst naar functie](resource-group-template-functions-resource.md#reference).

## <a name="recommendations-for-setting-dependencies"></a>Aanbevelingen voor het instellen van de afhankelijkheden

Wanneer u beslist welke tooset afhankelijkheden, gebruikt u Hallo richtlijnen te volgen:

* Afhankelijkheden van zo weinig mogelijk ingesteld.
* Stel een onderliggende resource als afhankelijk van de bovenliggende resource.
* Gebruik Hallo **verwijzing** tooset impliciete afhankelijkheden tussen resources die een eigenschap tooshare moeten werken. Voeg een expliciete afhankelijkheid niet (**dependsOn**) wanneer u een impliciete afhankelijkheid al hebt gedefinieerd. Deze benadering minder kans Hallo van onnodige afhankelijkheden. 
* Een afhankelijkheid ingesteld wanneer een resource kan niet worden **gemaakt** zonder de functionaliteit van een andere resource. Stel een afhankelijkheid niet als Hallo bronnen alleen na de implementatie werken.
* Laat afhankelijkheden cascade zonder expliciet instelt. Bijvoorbeeld, de virtuele machine is afhankelijk van de virtuele netwerkinterface en Hallo virtuele netwerkinterface is afhankelijk van een virtueel netwerk en openbare IP-adressen. Daarom Hallo virtuele machine is geïmplementeerd nadat alle drie resources, maar Hallo virtuele machine niet expliciet als afhankelijk is van alle drie resources instelt. Deze aanpak wordt uitleg gegeven over Hallo afhankelijkheid volgorde en maakt het eenvoudiger toochange Hallo sjabloon later.
* Als een waarde kan worden bepaald vóór de implementatie, kunt u proberen Hallo resource zonder een afhankelijkheid implementeren. Bijvoorbeeld, als een configuratiewaarde Hallo-naam van een andere resource moet, moet u mogelijk niet een afhankelijkheid. In deze richtlijnen werkt niet altijd omdat andere resources worden gecontroleerd Hallo bestaan Hallo sommige resources. Als u een foutbericht ontvangt, voegt u een afhankelijkheid. 

Resource Manager identificeert circulaire afhankelijkheden tijdens de validatie van de sjabloon. Als u er een foutmelding weergegeven dat er een circulaire afhankelijkheid bestaat, evalueren van uw sjabloon toosee als alle afhankelijkheden zijn niet nodig en kunnen worden verwijderd. Als afhankelijkheden verwijderen niet werkt, kunt u circulaire afhankelijkheden voorkomen door bepaalde implementatiebewerkingen naar de onderliggende resources die zijn geïmplementeerd na het Hallo-resources met circulaire afhankelijkheid Hallo een te verplaatsen. Stel bijvoorbeeld dat u twee virtuele machines implementeert, maar u moet eigenschappen instellen voor elk veld dat toohello andere verwijzen. U kunt deze implementeren in Hallo volgorde:

1. vm1
2. vm2
3. Extensie op vm1, is afhankelijk van vm1 en vm2. Hallo-extensie waarden ingesteld op vm1 die van vm2 krijgt.
4. Extensie op vm2, is afhankelijk van vm1 en vm2. Hallo-extensie waarden ingesteld op vm2 van van vm1 krijgt.

Zie voor meer informatie over de beoordeling van de implementatievolgorde hello en het oplossen van afhankelijkheidsfouten [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).

## <a name="next-steps"></a>Volgende stappen
* Zie toolearn over het oplossen van afhankelijkheden tijdens de implementatie van [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).
* toolearn over het maken van Azure Resource Manager-sjablonen, Zie [sjablonen](resource-group-authoring-templates.md). 
* Zie voor een lijst met de beschikbare functies in een sjabloon Hallo [sjabloonfuncties](resource-group-template-functions.md).

