---
title: aaaAccess en beveiliging in Azure-sjablonen voor virtuele machines van Windows | Microsoft Docs
description: Virtuele Machine van Azure DotNet belangrijkste zelfstudie
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: e671fc45-5e4d-40fd-aac5-290892713cc0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4b8227ae745b3b0a22d136e98d18479f8b1504c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a>Toegang en beveiliging in Azure Resource Manager-sjablonen voor virtuele machines van Windows

Toepassingen die worden gehost in Azure waarschijnlijk nodig toobe toegang via Hallo internet of een VPN-/ Express Route-verbinding met Azure. Met Hallo muziek Store toepassing voorbeeld Hallo-website op beschikbaar wordt gesteld Hallo internet met een openbaar IP-adres. Met toegang tot stand gebracht, moeten verbindingen toohello toepassing en access toohello bronnen voor virtuele machines zelf worden beveiligd. Deze beveiliging wordt verstrekt met een Netwerkbeveiligingsgroep. 

In dit document worden hoe Hallo muziek Store-toepassing in Hallo-voorbeeldsjabloon voor Azure Resource Manager worden beveiligd. Alle afhankelijkheden en unieke configuraties zijn gemarkeerd. Implementeer een exemplaar van Hallo oplossing tooyour Azure-abonnement en werk samen met hello Azure Resource Manager-sjabloon voor de beste ervaring Hallo. de volledige sjabloon Hallo vindt u hier: [muziek Store wilt implementeren op Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="public-ip-address"></a>Openbare IP-adres
tooprovide openbare toegang tooan Azure-resource, een openbare IP-adres resource kan worden gebruikt. Openbaar IP-adres kan worden geconfigureerd met een statisch of dynamisch IP-adres. Als een dynamisch adres wordt gebruikt en Hallo virtuele machine wordt gestopt en de toewijzing ongedaan gemaakt, wordt Hallo adressen verwijderd. Wanneer Hallo machine opnieuw wordt gestart, is het mogelijk dat deze een andere openbare IP-adres worden toegewezen. tooprevent een IP-adres wijzigen, een gereserveerd IP-adres kan worden gebruikt. 

Een openbaar IP-adres tooan Hallo Visual Studio nieuwe Wizard Resource toevoegen, met Azure Resource Manager-sjabloon kunnen worden toegevoegd of door een geldige JSON invoegen in een sjabloon. 

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [openbaar IP-adres](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIpAddressName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "public-ip"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

Een openbaar IP-adres kunnen worden gekoppeld aan een virtuele netwerkadapter, of een Load Balancer. Omdat Hallo muziek Store website gelijkmatig verdeeld zijn over meerdere virtuele machines, is Hallo openbaar IP-adres in dit voorbeeld aangesloten toohello Load Balancer.

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [openbaar IP-adres koppeling met de Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

Hallo openbare IP-adres als gezien vanaf hello Azure-portal. U ziet dat Hallo openbaar IP-adres gekoppeld tooa load balancer en niet op een virtuele machine is. Network load balancers zijn aangegeven in het volgende document Hallo van deze reeks.

![Openbare IP-adres](./media/dotnet-core-3-access-security/pubip-win.png)

Zie voor meer informatie over Azure openbare IP-adressen [IP-adressen in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).

## <a name="network-security-group"></a>Netwerkbeveiligingsgroep
Zodra de toegang tot stand gebrachte tooAzure resources is, is deze toegang moet worden beperkt. Veilige toegang wordt gerealiseerd met behulp van een netwerkbeveiligingsgroep voor Azure virtual machines. Met Hallo muziek Store toepassing voorbeeld alle toegang toohello virtuele machine is beperkt, behalve voor via poort 80 voor HTTP-toegang en -poort 3389 voor RDP-toegang. Een Netwerkbeveiligingsgroep tooan Hallo Visual Studio nieuwe Wizard Resource toevoegen, met Azure Resource Manager-sjabloon kunnen worden toegevoegd of door een geldige JSON invoegen in een sjabloon.

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Netwerkbeveiligingsgroep](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('networkSecurityGroup')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-security-group"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
},
```

In dit voorbeeld is de netwerkbeveiligingsgroep Hallo koppelen met Hallo subnet-object is gedeclareerd in Hallo Virtual Network-resource. 

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Netwerkbeveiligingsgroep koppeling met het virtuele netwerk](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
]
```

Hier ziet u welke Hallo netwerkbeveiligingsgroep lijkt in hello Azure-portal. Merk op dat mag een NSG koppelen aan een subnet en / of de netwerk-interface. In dit geval is Hallo NSG gekoppeld tooa subnet. In deze configuratie toepassen hello binnenkomende regels tooall virtuele machines verbonden toohello subnet.

![Netwerkbeveiligingsgroep](./media/dotnet-core-3-access-security/nsg-win.png)

Zie voor gedetailleerde informatie over Netwerkbeveiligingsgroepen [wat is er een Netwerkbeveiligingsgroep](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).

## <a name="next-step"></a>Volgende stap
<hr>

[Stap 3 - beschikbaarheid en schaal in Azure Resource Manager-sjablonen](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

