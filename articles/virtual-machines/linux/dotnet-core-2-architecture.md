---
title: aaaDeploying Linux Compute Resources met Azure Resource Manager-sjablonen | Microsoft Docs
description: Virtuele Machine van Azure DotNet belangrijkste zelfstudie
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 1c4d419e-ba0e-45e4-a9dd-7ee9975a86f9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0bc26805860fed47923d46fc84f357060f68a951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-linux-vms"></a>Toepassingsarchitectuur met Azure Resource Manager-sjablonen voor virtuele Linux-machines

Bij het ontwikkelen van een Azure Resource Manager-implementatie, moeten de compute-vereisten toobe toegewezen tooAzure resources en services. Als een toepassing bestaat uit verschillende HTTP-eindpunten, een database en een gegevens in de cache van de service, hello Azure-resources die als host fungeren van elk van deze onderdelen moet toobe gerationaliseerd. Hallo-voorbeeldtoepassing muziek Store bevat bijvoorbeeld een webtoepassing die wordt gehost op een virtuele machine en een SQL-database wordt gehost in Azure SQL-database. 

Dit document beschrijft hoe Hallo muziek Store rekenresources zijn geconfigureerd in Hallo voorbeeld Azure Resource Manager-sjabloon. Alle afhankelijkheden en unieke configuraties zijn gemarkeerd. Implementeer een exemplaar van Hallo oplossing tooyour Azure-abonnement en werk samen met hello Azure Resource Manager-sjabloon voor de beste ervaring Hallo. de volledige sjabloon Hallo vindt u hier: [muziek Store wilt implementeren op een virtuele Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux). 

## <a name="virtual-machine"></a>Virtuele machine
Hallo muziek Store-toepassing bevat een webtoepassing waarin klanten kunnen bladeren en muziek. Er zijn verschillende Azure-services dat de host van webtoepassingen, in dit voorbeeld wordt een virtuele Machine wordt gebruikt. Hallo-voorbeeldsjabloon muziek Store gebruikt, een virtuele machine is geïmplementeerd, een webserver installeren en Hallo muziek Store website geïnstalleerd en geconfigureerd. Voor Hallo mogelijk te houden van dit artikel, de implementatie van virtuele machines met alleen Hallo worden beschreven. Hallo-configuratie van het Hallo-webserver en de toepassing hello is uiteengezet in een latere artikel.

Een virtuele machine kan worden toegevoegd met behulp van Visual Studio nieuwe Resource toevoegen wizard, of door een geldige JSON in Hallo implementatiesjabloon invoegen Hallo tooa-sjabloon. Wanneer u een virtuele machine implementeert, zijn ook enkele verwante resources nodig. Als Visual Studio toocreate Hallo sjabloon gebruikt, worden deze resources voor u gemaakt. Als handmatig Hallo-sjabloon maken, moeten deze resources toobe ingevoegd en geconfigureerd.

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [JSON van de virtuele Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
      ........<truncated>  
    }
```

Zodra geïmplementeerd, kunnen u de eigenschappen van de virtuele machine Hallo bekijken in hello Azure-portal.

![Virtuele machine](./media/dotnet-core-2-architecture/vm.png)

## <a name="storage-account"></a>Storage-Account
Storage-accounts hebben veel opties voor opslag en mogelijkheden. Hallo-context van Azure virtuele machines bevat een opslagaccount Hallo virtuele harde schijven van Hallo virtuele machine en eventuele extra gegevensschijven. Hallo muziek Store voorbeeld bevat één storage account toohold Hallo virtuele harde schijf van elke virtuele machine in Hallo-implementatie. 

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Opslagaccount](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

Storage-account is koppelen aan een virtuele machine in Hallo Resource Manager-sjabloondeclaratie van Hallo virtuele machine. 

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [virtuele Machine- en Storage-Account koppeling](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

Na de implementatie kan Hallo storage-account worden weergegeven in hello Azure-portal.

![Storage-Account](./media/dotnet-core-2-architecture/storacct.png)

Op te klikken in Hallo blob storage account-container, kunt Hallo virtuele harde schijf-bestand voor elke virtuele machine geïmplementeerd met Hallo sjabloon bekijken.

![Virtuele harde schijven](./media/dotnet-core-2-architecture/vhd.png)

Zie voor meer informatie over Azure Storage [documentatie bij Azure Storage](https://azure.microsoft.com/documentation/services/storage/).

## <a name="virtual-network"></a>Virtual Network
Als een virtuele machine interne netwerken zoals Hallo mogelijkheid toocommunicate met andere virtuele machines en de Azure-resources vereist, is een Azure-netwerk is vereist.  Een virtueel netwerk maakt geen Hallo virtuele machine toegankelijk zijn via internet Hallo. Openbare-connectiviteit vereist een openbaar IP-adres, verderop in deze reeks wordt beschreven.

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [virtueel netwerk en subnetten](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
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
  }
}
```

Van hello Azure-portal eruit Hallo virtueel netwerk Hallo installatiekopie te volgen. U ziet dat alle virtuele machines die zijn geïmplementeerd met Hallo sjabloon gekoppelde toohello virtueel netwerk.

![Virtual Network](./media/dotnet-core-2-architecture/vnet.png)

## <a name="network-interface"></a>Netwerkinterface
 Een netwerkinterface verbindt een virtuele machine tooa virtueel netwerk, een meer specifiek tooa subnet dat is gedefinieerd in het virtuele netwerk Hallo. 

 Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [netwerkinterface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceNamePrefix'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'SSH-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig1",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/SSH-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

De bron van elke virtuele machine bevat een netwerkprofiel. Hallo-netwerkinterface is gekoppeld aan virtuele machine Hallo in dit profiel.  

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [netwerkprofiel van de virtuele Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceNamePrefix'), copyindex()))]"
    }
  ]
}
```

Van hello Azure-portal eruit netwerkinterface Hallo Hallo installatiekopie te volgen. Hallo interne IP-adres en de koppeling van Hallo-virtuele machine kunnen worden weergegeven op het Hallo-netwerkbron interface.

![Netwerkinterface](./media/dotnet-core-2-architecture/nic.png)

Zie voor meer informatie over Azure Virtual Networks [Azure Virtual Network-documentatie](https://azure.microsoft.com/documentation/services/virtual-network/).

## <a name="azure-sql-database"></a>Azure SQL Database
Bovendien is tooa virtuele machine die als host fungeert voor een Azure SQL Database-website muziek Store Hallo geïmplementeerde toohost Hallo muziek Store-database. Hallo voordeel van het gebruik van Azure SQL Database hier is dat een tweede set van virtuele machines niet vereist is en schaal en beschikbaarheid is ingebouwd in Hallo-service.

Een Azure SQL database kan worden toegevoegd met behulp van Visual Studio nieuwe Resource toevoegen wizard, of door een geldige JSON in een sjabloon invoegen Hallo. Hallo SQL Server-bron bevat een gebruikersnaam en wachtwoord beheerdersrechten op Hallo SQL-exemplaar wordt verleend. Ook wordt een bron van de firewall SQL toegevoegd. Standaard zijn de toepassingen die worden gehost in Azure kunnen tooconnect met Hallo SQL-exemplaar. tooallow externe toepassing zoals een SQL Server Management studio tooconnect toohello SQL-exemplaar, Hallo firewall moet toobe geconfigureerd. Voor Hallo mogelijk te houden van Hallo muziek Store demo is de standaardconfiguratie Hallo fijn. 

Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicStoreSqlName')]",
  "location": "[resourceGroup().location]",

  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('sqlAdminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicStoreSqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

Een weergave van Hallo SQL server en database MusicStore zoals gezien in hello Azure-portal.

![SQL Server](./media/dotnet-core-2-architecture/sql.png)

Zie voor meer informatie over het implementeren van Azure SQL Database [documentatie van Azure SQL Database](https://azure.microsoft.com/documentation/services/sql-database/).

## <a name="next-step"></a>Volgende stap
<hr>

[Stap 2 - toegang en beveiliging in Azure Resource Manager-sjablonen](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

