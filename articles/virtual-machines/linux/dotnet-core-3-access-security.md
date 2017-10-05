---
title: Toegang en beveiliging in Azure-sjablonen voor virtuele Linux-machines | Microsoft Docs
description: Virtuele Machine van Azure DotNet belangrijkste zelfstudie
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 07e47189-680e-4102-a8d4-5a8eb9c00213
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4ef4fc4109d4ccf4be273608bacacce820deb281
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-linux-vms"></a>Toegang en beveiliging in Azure Resource Manager-sjablonen voor virtuele Linux-machines

Toepassingen die worden gehost in Azure waarschijnlijk moeten toegang via internet of via een VPN-/ Express Route-verbinding met Azure. De website wordt met het voorbeeld van de toepassing muziek Store beschikbaar gesteld op internet met een openbaar IP-adres. Met toegang tot stand gebracht, moeten verbindingen met de toepassing en toegang tot de resources van de virtuele machine zelf worden beveiligd. Deze beveiliging wordt verstrekt met een Netwerkbeveiligingsgroep. 

Dit document beschrijft hoe de muziek Store-toepassing in de steekproef Azure Resource Manager-sjabloon wordt beveiligd. Alle afhankelijkheden en unieke configuraties zijn gemarkeerd. Implementeer een exemplaar van de oplossing voor uw Azure-abonnement en werk samen met de Azure Resource Manager-sjabloon voor de beste ervaring. De volledige sjabloon vindt u hier: [muziek Store wilt implementeren op een virtuele Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux). 

## <a name="public-ip-address"></a>Openbare IP-adres
Als u openbare toegang tot een Azure-resource maken, kan een openbare IP-adres resource worden gebruikt. Openbaar IP-adres kan worden geconfigureerd met een statisch of dynamisch IP-adres. Als een dynamisch adres wordt gebruikt en de virtuele machine wordt gestopt en de toewijzing ongedaan gemaakt, wordt de adressen verwijderd. Wanneer de computer opnieuw wordt gestart, is het mogelijk dat deze een andere openbare IP-adres worden toegewezen. Als u wilt voorkomen dat een IP-adres wijzigen, kan een gereserveerd IP-adres worden gebruikt. 

Een openbaar IP-adres kunnen worden toegevoegd aan een Azure Resource Manager-sjabloon met behulp van de Visual Studio nieuwe Wizard Resource toevoegen of door een geldige JSON invoegen in een sjabloon. 

Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [openbaar IP-adres](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L121).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicipaddressName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "public-ip-front"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

Een openbaar IP-adres kunnen worden gekoppeld aan een virtuele netwerkadapter, of een Load Balancer. In dit voorbeeld dat omdat de website van de winkel gelijkmatig verdeeld zijn over meerdere virtuele machines, is het openbare IP-adres is gekoppeld aan de Load Balancer.

Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [openbaar IP-adres koppeling met de Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).

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

Het openbare IP-adres zoals weergegeven in de Azure portal. U ziet dat het openbare IP-adres gekoppeld aan een load balancer en niet een virtuele machine is. Network load balancers zijn aangegeven in het volgende document van deze reeks.

![Openbare IP-adres](./media/dotnet-core-3-access-security/pubip.png)

Zie voor meer informatie over Azure openbare IP-adressen [IP-adressen in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).

## <a name="network-security-group"></a>Netwerkbeveiligingsgroep
Zodra de toegang is ingesteld voor Azure-resources, is deze toegang moet worden beperkt. Veilige toegang wordt gerealiseerd met behulp van een netwerkbeveiligingsgroep voor Azure virtual machines. Met het voorbeeld van de toepassing muziek Store is alle toegang tot de virtuele machine beperkt, behalve voor via poort 80 voor HTTP-toegang en -poort 22 voor SSH-toegang. Een Netwerkbeveiligingsgroep kunnen worden toegevoegd aan een Azure Resource Manager-sjabloon met behulp van de Visual Studio nieuwe Wizard Resource toevoegen of door een geldige JSON invoegen in een sjabloon.

Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Netwerkbeveiligingsgroep](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L68).

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('nsgfront')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "nsg-front"
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
}
```

In dit voorbeeld wordt de netwerkbeveiligingsgroep koppelen aan het subnetobject dat is gedeclareerd in de bron van het virtuele netwerk. 

Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Netwerkbeveiligingsgroep koppeling met het virtuele netwerk](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L158).

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
```

Hier wordt de netwerkbeveiligingsgroep ziet er als vanuit de Azure-portal. Merk op dat mag een NSG koppelen aan een subnet en / of de netwerk-interface. In dit geval wordt is het NSG gekoppeld aan een subnet. In deze configuratie worden de regels voor binnenkomende verbindingen van toepassing op alle virtuele machines die zijn verbonden met het subnet.

![Netwerkbeveiligingsgroep](./media/dotnet-core-3-access-security/nsg.png)

Zie voor gedetailleerde informatie over Netwerkbeveiligingsgroepen [wat is er een Netwerkbeveiligingsgroep](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).

## <a name="next-step"></a>Volgende stap
<hr>

[Stap 3 - beschikbaarheid en schaal in Azure Resource Manager-sjablonen](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

