---
title: aaaLearn over virtuele-machineschaalset sjablonen instellen | Microsoft Docs
description: Meer informatie over een minimale levensvatbaar schaal toocreate ingesteld sjabloon voor virtuele-machineschaalsets
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a>Meer informatie over de sjablonen voor virtuele machines scale set
[Azure Resource Manager-sjablonen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) zijn een goede manier toodeploy groepen verwante resources. Deze zelfstudie reeks ziet u hoe u een minimale levensvatbaar schaal toocreate sjabloon ingesteld en hoe toomodify deze sjabloon toosuit verschillende scenario's. Alle voorbeelden afkomstig zijn van dit [GitHub-opslagplaats](https://github.com/gatneil/mvss). 

Deze sjabloon is bedoeld toobe eenvoudig. Voor gedetailleerde voorbeelden van de schaal sjablonen, raadpleegt u Hallo [Azure Quick Start-sjablonen GitHub-opslagplaats](https://github.com/Azure/azure-quickstart-templates) en zoek naar de mappen met Hallo tekenreeks `vmss`.

Als u al bekend bent met sjablonen maken, kunt u hoe toohello 'Volgende stappen' sectie toosee overslaan toomodify deze sjabloon.

## <a name="review-hello-template"></a>Hallo-template bekijken

Gebruik van GitHub tooreview onze minimale levensvatbaar schaalset sjabloon [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).

In deze zelfstudie we naar de Hallo diff (`git diff master minimum-viable-scale-set`) toocreate Hallo minimale levensvatbaar schaalset sjabloon stuk door stuk.

## <a name="define-schema-and-contentversion"></a>$Schema en contentVersion definiëren
Eerst definiëren we `$schema` en `contentVersion` in Hallo-sjabloon. Hallo `$schema` element Hallo-versie van de sjabloontaal Hallo definieert en wordt gebruikt voor syntaxismarkering Visual Studio en vergelijkbare functies voor validatie. Hallo `contentVersion` element wordt niet gebruikt door Azure. In plaats daarvan kunt u Hallo sjabloonversie.

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a>parameters definiëren
Vervolgens geeft u twee parameters `adminUsername` en `adminPassword`. Parameters zijn waarden die u op Hallo moment van implementatie opgeeft. Hallo `adminUsername` parameter is gewoon een `string` type, maar omdat `adminPassword` geheim, geven wij type `securestring`. Later, worden deze parameters doorgegeven in Hallo scale set configuratie.

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a>Variabelen definiëren
Resource Manager-sjablonen kunnen u variabelen toobe verderop in de sjabloon Hallo gebruikt definiëren. Het voorbeeld gebruikt niet alle variabelen zodat we hebt leeg wordt gelaten Hallo JSON-object.

```json
  "variables": {},
```

## <a name="define-resources"></a>Resources definiëren
Naast is Hallo bronnensectie van Hallo sjabloon. Hier kunt u definiëren wat daadwerkelijk toodeploy. In tegenstelling tot `parameters` en `variables` (die zijn JSON-objecten), `resources` is een JSON-lijst van JSON-objecten.

```json
   "resources": [
```

Alle resources vereisen `type`, `name`, `apiVersion`, en `location` eigenschappen. De eerste resource in dit voorbeeld heeft een type `Microsft.Network/virtualNetwork`, naam `myVnet`, en apiVersion `2016-03-30`. (toofind Hallo nieuwste API-versie voor een brontype Zie Hallo [Azure REST API-documentatie](https://docs.microsoft.com/rest/api/).)

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a>Geef de locatie
toospecify hello locatie voor het virtuele netwerk hello, gebruiken we een [Resource Manager sjabloonfunctie](../azure-resource-manager/resource-group-template-functions.md). Deze functie moet tussen aanhalingstekens en vierkante haken als volgt: `"[<template-function>]"`. In dit geval gebruiken we Hallo `resourceGroup` functie. Dit heeft geen argumenten en retourneert een JSON-object met metagegevens over Hallo resourcegroep die deze implementatie wordt geïmplementeerd. Hallo-resourcegroep is ingesteld door de gebruiker Hallo op Hallo moment van implementatie. We vervolgens index in dit JSON-object met `.location` tooget Hallo locatie Hallo JSON-object.

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a>Eigenschappen van virtueel netwerk opgeven
Elke Resource Manager-bron heeft zijn eigen `properties` sectie voor configuraties specifieke toohello resource. In dit geval we dit virtuele netwerk Hallo moet één subnet met Hallo persoonlijk IP-adresbereik opgeven `10.0.0.0/16`. Een schaalset zich altijd in één subnet. Dit kan geen subnetten omvatten.

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a>DependsOn lijst toevoegen
Bovendien toohello vereist `type`, `name`, `apiVersion`, en `location` eigenschappen van elke bron kunnen een optionele hebben `dependsOn` lijst met tekenreeksen. Deze lijst aangeeft welke andere bronnen van deze implementatie moeten worden voltooid voordat de implementatie van deze resource.

In dit geval is slechts één element in virtueel netwerk van het vorige voorbeeld Hallo HALLO hallo lijst. We opgeven deze afhankelijkheid omdat Hallo behoeften Hallo netwerk tooexist schaalset voordat u alle virtuele machines maakt. Op deze manier Hallo scale set kan deze persoonlijke IP-adressen voor virtuele machines uit Hallo IP-adresbereik eerder opgegeven in hello netwerkgegevens geven. Hallo-indeling van elke tekenreeks in Hallo dependsOn lijst is `<type>/<name>`. Gebruik dezelfde Hallo `type` en `name` eerder gebruikt in de resourcedefinitie voor Hallo virtueel netwerk.

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a>Scale seteigenschappen opgeven
-Schaalsets hebben veel eigenschappen voor het Hallo-virtuele machines in de schaalset Hallo aanpassen. Zie voor een volledige lijst van deze eigenschappen Hallo [REST API-documentatie-schaalset](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set). Er wordt slechts enkele veelgebruikte eigenschappen ingesteld voor deze zelfstudie.
### <a name="supply-vm-size-and-capacity"></a>VM-grootte en capaciteit op te geven
Hallo-schaalset behoeften tooknow welke grootte van de VM toocreate ('sku-naam') en hoeveel dergelijke virtuele machines toocreate ('sku-capaciteit'). toosee welke VM-grootten beschikbaar zijn, Zie Hallo [VM-grootten documentatie](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a>Type van de updates kiezen
Hallo scale set moet ook tooknow hoe toohandle updates op Hallo schaalset. Er zijn momenteel twee opties `Manual` en `Automatic`. Zie voor meer informatie over de verschillen tussen twee Hallo HALLO hallo-documentatie op [hoe tooupgrade een schaalset](./virtual-machine-scale-sets-upgrade-scale-set.md).

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a>Kies VM-besturingssysteem
Hallo-schaalset behoeften tooknow welke tooput besturingssysteem op Hallo virtuele machines. Hier maken we Hallo virtuele machines met een volledig patches Ubuntu 16.04 TNS-installatiekopie.

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a>Geef de waarde voor computerNamePrefix
Hallo-schaalset implementeert meerdere virtuele machines. In plaats van elke VM-naam geven, geven we `computerNamePrefix`. Hallo schaalset voegt het voorvoegsel van een index toohello voor elke VM zodat VM-namen Hallo vorm hebben `<computerNamePrefix>_<auto-generated-index>`.

In Hallo codefragment te volgen, gebruiken we Hallo parameters uit voordat tooset Hallo beheerder gebruikersnaam en wachtwoord voor alle virtuele machines in de schaalset Hallo. We doen dit met Hallo `parameters` sjabloonfunctie. Deze functie omvat een tekenreeks die opgeeft welke parameter toorefer tooand levert Hallo-waarde voor deze parameter.

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a>VM-netwerkconfiguratie opgeven
Tot slot moeten we toospecify Hallo netwerkconfiguratie voor Hallo virtuele machines in de schaalset Hallo. In dit geval hoeft er alleen toospecify Hallo-ID van Hallo subnet eerder hebt gemaakt. Dit vertelt Hallo schaalset tooput Hallo netwerkinterfaces in dit subnet.

U kunt Hallo-ID van het virtuele netwerk van Hallo Hallo subnet met met behulp van Hallo ophalen `resourceId` sjabloonfunctie. Deze functie omvat Hallo type en de naam van een resource en retourneert Hallo volledig gekwalificeerde id van de bron. Deze ID heeft Hallo vorm:`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`

Hallo-id van het virtuele netwerk Hallo is echter niet voldoende. U moet specifieke Hallo-subnet dat Hallo scale set die virtuele machines moet opgeven. toodo dit samenvoegen `/subnets/mySubnet` toohello-ID van het virtuele netwerk Hallo. Hallo resultaat is volledig gekwalificeerd Hallo-ID van Hallo subnet. Deze samenvoeging Hello doen `concat` functie, die duurt in een reeks tekenreeksen en retourneert de samenvoeging.

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
