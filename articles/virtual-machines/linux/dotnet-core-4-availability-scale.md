---
title: aaaAvailability en schalen in Azure Resource Manager-sjablonen | Microsoft Docs
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
ms.openlocfilehash: 6f830ca0a64e6b65859312bdf31dc0af59e2b978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a>Beschikbaarheid en schaal in Azure Resource Manager-sjablonen voor virtuele Linux-machines

Raadpleeg toouptime en Hallo mogelijkheid toomeet vraag beschikbaarheid en schaal. Als een toepassing van 99,9% van de tijd hello zijn moet, moet deze toohave een architectuur waarmee meerdere gelijktijdige rekenresources. In plaats van één website, bevat een configuratie met een hoger niveau van beschikbaarheid bijvoorbeeld meerdere exemplaren van dezelfde site, met de technologie voor deze balancing Hallo. In deze configuratie is kunt één exemplaar van de toepassing hello worden uitgeschakeld voor onderhoud, terwijl Hallo resterende toofunction blijven. Schaal op Hallo verwijst daarentegen tooan toepassingen de mogelijkheid tooserve vraag. Met een belasting kan taakverdeling toepassing, toevoegen of verwijderen van instanties van de groep Hallo een toepassing tooscale toomeet vraag.

Dit document beschrijft hoe Hallo Voorbeeldimplementatie muziek Store is geconfigureerd voor de beschikbaarheid en schaal. Alle afhankelijkheden en unieke configuraties zijn gemarkeerd. Implementeer een exemplaar van Hallo oplossing tooyour Azure-abonnement en werk samen met hello Azure Resource Manager-sjabloon voor de beste ervaring Hallo. de volledige sjabloon Hallo vindt u hier: [muziek Store wilt implementeren op een virtuele Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

## <a name="availability-set"></a>Beschikbaarheidsset
Een Beschikbaarheidsset omvat Azure Virtual Machines naar andere fysieke hosts en andere infrastructurele onderdelen, zoals voedingen en fysieke netwerkhardware logisch. Beschikbaarheidssets Zorg ervoor dat tijdens onderhoud, apparaatfout of andere uitvaltijd, niet alle virtuele machines worden gedaan. Een Beschikbaarheidsset kunnen worden toegevoegd als tooan Azure Resource Manager-sjabloon met behulp van Visual Studio nieuwe Wizard Resource toevoegen Hallo of geldige JSON invoegen in een sjabloon.

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Beschikbaarheidsset](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).

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

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Beschikbaarheidsset koppeling met de virtuele Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
Hallo beschikbaarheidsset gezien vanaf hello Azure-portal. Elke virtuele machine en de gegevens over configuratie Hallo worden hier beschreven.

![Beschikbaarheidsset](./media/dotnet-core-4-availability-scale/aset.png)

Zie voor gedetailleerde informatie over Beschikbaarheidssets [beschikbaarheid van virtuele machines beheren](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

## <a name="network-load-balancer"></a>Load balancer voor netwerk
Terwijl een beschikbaarheidsset fouttolerantie van toepassing biedt, beschikbaar een load balancer veel exemplaren van de toepassing hello op één netwerkadres. Meerdere exemplaren van een toepassing kunnen worden gehost op een groot aantal virtuele machines verbonden elkaar tooa load balancer. Als de toepassing hello wordt geopend, Hallo Hallo load balancer routes inkomende aanvraag over Hallo gekoppeld leden. Een Load Balancer kan worden toegevoegd met Hallo Visual Studio nieuwe Wizard Resource toevoegen of door het invoegen van juist opgemaakte JSON-resource naar hello Azure Resource Manager-sjabloon.

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Netwerkbelastingbalancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).

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

Omdat de voorbeeldtoepassing Hallo blootgestelde toohello internet met een openbaar IP-adres, dit adres is gekoppeld aan Hallo load balancer. 

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Network Load Balancer-koppeling met openbare IP-adres](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).

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

Van hello Azure-portal toont hello network load balancer overzicht Hallo koppeling met de Hallo openbaar IP-adres.

![Load balancer voor netwerk](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a>Load Balancer-regel
Wanneer u een load balancer, zijn regels die bepalen hoe verkeer wordt verdeeld over Hallo bedoeld resources geconfigureerd. Hallo-voorbeeldtoepassing muziek Store verkeer binnenkomt op poort 80 Hallo openbare IP-adres en is verdeeld over de poort 80 van alle virtuele machines. 

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Load Balancer-regel](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).

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

Een weergave van Hallo netwerk balancer-regel uit Hallo-portal geladen.

![Network Load Balancer-regel](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a>Load Balancer-test
Hallo load balancer moet ook toomonitor elke virtuele machine zodat aanvragen worden alleen toorunning systemen behandeld. Deze controle vindt plaats door constante zoeken van een vooraf gedefinieerde poort. Hallo muziek Store-implementatie is geconfigureerde tooprobe poort 80 op alle opgenomen virtuele machines. 

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Load Balancer-test](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).

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

Hallo load balancer-test gezien vanaf hello Azure-portal.

![Network Load Balancer-test](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a>Inkomende NAT-regels
Wanneer u een Load Balancer, regels toobe moeten worden uitgevoerd die niet load balanced toegang tooeach virtuele Machine te bieden. Bijvoorbeeld, wanneer u een SSH-verbinding met elke virtuele machine maakt, dit verkeer mag geen taakverdeling, in plaats daarvan een vooraf bepaald pad moet worden geconfigureerd. vooraf bepaald paden zijn geconfigureerd met behulp van de bron van een binnenkomende NAT-regel. Deze bron, binnenkomende communicatie, kan worden toegewezen tooindividual virtuele Machines. 

Met Hallo muziek Store-toepassing is een poort die begint bij 5000 toegewezen tooport 22 op elke virtuele Machine voor SSH-toegang. Hallo `copyindex()` functie is gebruikte tooincrement Hallo binnenkomende poort, zoals die Hallo tweede virtuele Machine een binnenkomende poort van 5001 ontvangt, derde 5002 hello, enzovoort. 

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [binnenkomende NAT-regels](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270). 

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

Voorbeeld van een binnenkomende NAT-regel als zoals weergegeven in hello Azure-portal. Een SSH-NAT-regel is gemaakt voor elke virtuele machine in Hallo-implementatie.

![Binnenkomende NAT-regel](./media/dotnet-core-4-availability-scale/natrule.png)

Zie voor gedetailleerde informatie over hello Azure Network Load Balancer [taakverdeling voor Azure-infrastructuurservices](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="deploy-multiple-vms"></a>Meerdere virtuele machines implementeren
Ten slotte zijn meerdere virtuele machines voor een functie Beschikbaarheidsset of Load Balancer tooeffectively vereist. Meerdere virtuele machines kunnen worden geïmplementeerd met behulp van de functie voor hello Azure Resource Manager-sjabloon kopiëren. Hallo kopieerfunctie gebruikt, is niet nodig toodefine een beperkt aantal virtuele Machines, in plaats daarvan deze waarde kan dynamisch worden verstrekt op Hallo moment van implementatie. Hallo kopieerfunctie verbruikt Hallo aantal exemplaren toocreated en ingangen Hallo juiste aantal virtuele machines en de bijbehorende resources implementeren.

In voorbeeldsjabloon Hallo muziek Store, een parameter waarmee het aantal instanties gedefinieerd. Dit nummer wordt gebruikt in de gehele Hallo sjabloon bij het maken van virtuele machines en gerelateerde resources.

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
}
```

Op Hallo virtuele-machinebron, Hallo kopie lus krijgt een naam en het aantal exemplaren parameter Hallo toocontrol Hallo aantal resulterende exemplaren gebruikt.

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [kopieerfunctie van het virtuele Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300). 

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

Hallo huidige herhaling van Hallo kopieerfunctie toegankelijk zijn met de Hallo `copyIndex()` functie. Hallo waarde van de index kopieerfunctie Hallo mag gebruikte tooname virtuele machines en andere bronnen. Bijvoorbeeld, als er twee exemplaren van een virtuele machine zijn geïmplementeerd, moeten ze verschillende namen. Hallo `copyIndex()` functie kan worden gebruikt als onderdeel van Hallo virtuele machine toocreate naam een unieke naam. Een voorbeeld van Hallo `copyindex()` functie gebruikt voor de naamgeving van de toepassing in Hallo virtuele-machinebron weergegeven. Hier Hallo computernaam is een samenvoeging van Hallo `vmName` parameter en Hallo `copyIndex()` functie. 

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Index kopieerfunctie](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319). 

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

Hallo `copyIndex` functie Hallo muziek Store voorbeeldsjabloon meerdere keren wordt gebruikt. Bronnen en functies met behulp van `copyIndex` bevatten alles specifieke tooa één exemplaar van Hallo virtuele machine, zoals de netwerkinterface, de regels van load balancer, en een is afhankelijk van functies. 

Zie voor meer informatie over Hallo kopieerfunctie [maken van meerdere exemplaren van resources in Azure Resource Manager](../../resource-group-create-multiple.md).

## <a name="next-step"></a>Volgende stap
<hr>

[Stap 4: implementatie van de toepassing met Azure Resource Manager-sjablonen](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

