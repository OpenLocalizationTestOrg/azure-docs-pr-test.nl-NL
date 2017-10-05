---
title: Beschikbaarheid en schaal in Azure Resource Manager-sjablonen | Microsoft Docs
description: Virtuele Machine van Azure DotNet belangrijkste zelfstudie
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8fcfea79-f017-4658-8c51-74242fcfb7f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0c0250b8152ed31b9a5d8b42ae139c9b38da0984
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a>Beschikbaarheid en schaal in Azure Resource Manager-sjablonen voor virtuele Linux-machines

Beschikbaarheid en schaal Raadpleeg bedrijfstijd en de mogelijkheid om te voldoen aan de vraag. Als een toepassing van 99,9% van de tijd zijn moet, moet deze hebben een architectuur waarmee meerdere gelijktijdige rekenresources. In plaats van één website, bevat een configuratie met een hoger niveau van beschikbaarheid bijvoorbeeld meerdere exemplaren van dezelfde site, met de technologie voor deze netwerktaakverdeling. In deze configuratie is kan één exemplaar van de toepassing worden uitgeschakeld voor onderhoud, terwijl de resterende blijven werken. Schaal verwijst daarentegen naar een kunnen toepassingen vraag. Met een load kan balanced toepassing, het toevoegen of verwijderen van instanties van de groep een toepassing schalen om te voldoen aan de vraag.

Dit document beschrijft hoe de implementatie van de steekproef muziek Store is geconfigureerd voor de beschikbaarheid en schaal. Alle afhankelijkheden en unieke configuraties zijn gemarkeerd. Implementeer een exemplaar van de oplossing voor uw Azure-abonnement en werk samen met de Azure Resource Manager-sjabloon voor de beste ervaring. De volledige sjabloon vindt u hier: [muziek Store wilt implementeren op een virtuele Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

## <a name="availability-set"></a>Beschikbaarheidsset
Een Beschikbaarheidsset omvat Azure Virtual Machines naar andere fysieke hosts en andere infrastructurele onderdelen, zoals voedingen en fysieke netwerkhardware logisch. Beschikbaarheidssets Zorg ervoor dat tijdens onderhoud, apparaatfout of andere uitvaltijd, niet alle virtuele machines worden gedaan. Een Beschikbaarheidsset kunnen worden toegevoegd aan een Azure Resource Manager-sjabloon met behulp van de Visual Studio nieuwe Wizard Resource toevoegen of geldige JSON invoegen in een sjabloon.

Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Beschikbaarheidsset](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "avalibility-set"
  },
  "properties": {
    "platformUpdateDomainCount": 5,
    "platformFaultDomainCount": 3
  }
}
```

Een Beschikbaarheidsset is gedeclareerd als een eigenschap van de bron van een virtuele Machine. 

Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Beschikbaarheidsset koppeling met de virtuele Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
De beschikbaarheidsset gezien vanaf de Azure-portal. Elke virtuele machine en de gegevens over de configuratie worden hier beschreven.

![Beschikbaarheidsset](./media/dotnet-core-4-availability-scale/aset.png)

Zie voor gedetailleerde informatie over Beschikbaarheidssets [beschikbaarheid van virtuele machines beheren](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

## <a name="network-load-balancer"></a>Load balancer voor netwerk
Terwijl een beschikbaarheidsset fouttolerantie van toepassing biedt, beschikbaar een load balancer veel exemplaren van de toepassing op één netwerkadres. Meerdere exemplaren van een toepassing kunnen worden gehost op veel virtuele machines, elk een is verbonden met een load balancer. Als de toepassing wordt geopend, stuurt de load balancer de binnenkomende aanvraag via de gekoppelde leden. Een Load Balancer kan worden toegevoegd met de Visual Studio nieuwe Wizard Resource toevoegen of door het invoegen van juist opgemaakte JSON-resource in de Azure Resource Manager-sjabloon.

Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Netwerkbelastingbalancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-front"
  },
  ........<truncated>
}
```

Omdat de voorbeeldtoepassing wordt blootgesteld aan internet met een openbaar IP-adres, moet dit adres is gekoppeld aan de load balancer. 

Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Network Load Balancer-koppeling met openbare IP-adres](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

Vanuit de Azure-portal ziet network load balancer overzicht u de koppeling met het openbare IP-adres.

![Load balancer voor netwerk](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a>Load Balancer-regel
Wanneer u een load balancer, zijn regels die bepalen hoe verkeer wordt verdeeld over de beoogde resources geconfigureerd. Met de voorbeeldtoepassing muziek Store verkeer binnenkomt op poort 80 van het openbare IP-adres en is verdeeld over de poort 80 van alle virtuele machines. 

Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Load Balancer-regel](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).

```json
"loadBalancingRules": [
  {
    "name": "[variables('loadBalencerRule')]",
    "properties": {
      "frontendIPConfiguration": {
        "id": "[concat(resourceId('Microsoft.Network/loadBalancers', variables('loadBalancerName')), '/frontendIPConfigurations/LoadBalancerFrontend')]"
      },
      "backendAddressPool": {
        "id": "[variables('lbPoolID')]"
      },
      "protocol": "Tcp",
      "frontendPort": 80,
      "backendPort": 80,
      "enableFloatingIP": false,
      "idleTimeoutInMinutes": 5,
      "probe": {
        "id": "[variables('lbProbeID')]"
      }
    }
  }
]
```

Een weergave van de network load balancer-regel van de portal.

![Network Load Balancer-regel](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a>Load Balancer-test
Er moet ook de load balancer voor het bewaken van elke virtuele machine zodat aanvragen alleen voor computers die worden geleverd. Deze controle vindt plaats door constante zoeken van een vooraf gedefinieerde poort. De muziek Store-implementatie is geconfigureerd om poort 80 op alle opgenomen virtuele machines test. 

Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Load Balancer-test](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).

```json
"probes": [
  {
    "properties": {
      "protocol": "Tcp",
      "port": 80,
      "intervalInSeconds": 15,
      "numberOfProbes": 2
    },
    "name": "lbprobe"
  }
]
```

De load balancer-test gezien vanaf de Azure-portal.

![Network Load Balancer-test](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a>Inkomende NAT-regels
Wanneer u een Load Balancer, moeten regels worden ingesteld die niet load balanced toegang bieden tot elke virtuele Machine. Bijvoorbeeld, wanneer u een SSH-verbinding met elke virtuele machine maakt, dit verkeer mag geen taakverdeling, in plaats daarvan een vooraf bepaald pad moet worden geconfigureerd. vooraf bepaald paden zijn geconfigureerd met behulp van de bron van een binnenkomende NAT-regel. Met deze bron, worden binnenkomende communicatie toegewezen aan afzonderlijke virtuele Machines. 

Met de toepassing muziek Store is een poort die begint bij 5000 toegewezen aan poort 22 op elke virtuele Machine voor SSH-toegang. De `copyindex()` functie wordt gebruikt om de binnenkomende poort verhogen zodat de tweede virtuele Machine ontvangt een binnenkomende poort van 5001, het derde 5002 enzovoort. 

Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [binnenkomende NAT-regels](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270). 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'SSH-VM', copyIndex())]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "lbNatLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
  ],
  "properties": {
    "frontendIPConfiguration": {
      "id": "[variables('ipConfigID')]"
    },
    "protocol": "tcp",
    "frontendPort": "[copyIndex(5000)]",
    "backendPort": 22,
    "enableFloatingIP": false
  }
}
```

Voorbeeld van een binnenkomende NAT-regel, zoals in de Azure-portal. Een SSH-NAT-regel is gemaakt voor elke virtuele machine in de implementatie.

![Binnenkomende NAT-regel](./media/dotnet-core-4-availability-scale/natrule.png)

Zie voor gedetailleerde informatie over Azure Network Load Balancer [taakverdeling voor Azure-infrastructuurservices](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="deploy-multiple-vms"></a>Meerdere virtuele machines implementeren
Ten slotte zijn meerdere virtuele machines voor een Beschikbaarheidsset of Load Balancer effectief werken, vereist. Meerdere virtuele machines kunnen worden geïmplementeerd met behulp van de kopieerfunctie van het Azure Resource Manager-sjabloon. Met behulp van de functie kopiëren, is het niet nodig voor het definiëren van een bepaald aantal virtuele Machines, in plaats daarvan deze waarde kan dynamisch worden verstrekt op het moment van implementatie. De functie kopiëren neemt het aantal exemplaren gemaakt en verwerkt het juiste aantal virtuele machines en de bijbehorende resources implementeren.

In de sjabloon muziek Store voorbeeld is een parameter waarmee het aantal instanties gedefinieerd. Dit nummer wordt gebruikt in de sjabloon bij het maken van virtuele machines en gerelateerde resources.

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances to be created behind load balancer."
  }
}
```

Op de bron van de virtuele Machine krijgt de lus kopiëren een naam en het aantal exemplaren parameter gebruikt voor het beheren van het aantal resulterende exemplaren.

Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [kopieerfunctie van het virtuele Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300). 

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Compute/virtualMachines",
"name": "[concat(variables('vmName'),copyindex())]",
"location": "[resourceGroup().location]",
"copy": {
  "name": "virtualMachineLoop",
  "count": "[parameters('numberOfInstances')]"
}
```

De huidige herhaling van de functie kopiëren is toegankelijk via de `copyIndex()` functie. De waarde van de functie voor kopiëren-index kan worden gebruikt als naam voor virtuele machines en andere bronnen. Bijvoorbeeld, als er twee exemplaren van een virtuele machine zijn geïmplementeerd, moeten ze verschillende namen. De `copyIndex()` functie kan worden gebruikt als onderdeel van de naam van de virtuele machine een unieke naam maken. Een voorbeeld van de `copyindex()` functie gebruikt voor de naamgeving van de toepassing wordt weergegeven in de bron van de virtuele Machine. Naam van de computer is hier een samenvoeging van de `vmName` parameter, en de `copyIndex()` functie. 

Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Index kopieerfunctie](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319). 

```json
"osProfile": {
  "computerName": "[concat(parameters('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "linuxConfiguration": {
    "disablePasswordAuthentication": "true",
    "ssh": {
      "publicKeys": [
        {
          "path": "[variables('sshKeyPath')]",
          "keyData": "[parameters('sshKeyData')]"
        }
      ]
    }
  }
}
```

De `copyIndex` functie meerdere keren wordt gebruikt in de winkel voorbeeldsjabloon. Bronnen en functies met behulp van `copyIndex` bevat alle specifiek zijn voor één exemplaar van de virtuele machine, zoals netwerkinterface, de regels van load balancer, en een is afhankelijk van functies. 

Zie voor meer informatie over de functie kopiëren [maken van meerdere exemplaren van resources in Azure Resource Manager](../../resource-group-create-multiple.md).

## <a name="next-step"></a>Volgende stap
<hr>

[Stap 4: implementatie van de toepassing met Azure Resource Manager-sjablonen](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

