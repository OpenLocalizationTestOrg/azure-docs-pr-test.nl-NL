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
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="7db93-103">Toegang en beveiliging in Azure Resource Manager-sjablonen voor virtuele machines van Windows</span><span class="sxs-lookup"><span data-stu-id="7db93-103">Access and security in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="7db93-104">Toepassingen die worden gehost in Azure waarschijnlijk nodig toobe toegang via Hallo internet of een VPN-/ Express Route-verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="7db93-104">Applications hosted in Azure likely need toobe access over hello internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="7db93-105">Met Hallo muziek Store toepassing voorbeeld Hallo-website op beschikbaar wordt gesteld Hallo internet met een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="7db93-105">With hello Music Store application sample, hello web site is made available on hello internet with a public IP address.</span></span> <span data-ttu-id="7db93-106">Met toegang tot stand gebracht, moeten verbindingen toohello toepassing en access toohello bronnen voor virtuele machines zelf worden beveiligd.</span><span class="sxs-lookup"><span data-stu-id="7db93-106">With access established, connections toohello application and access toohello virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="7db93-107">Deze beveiliging wordt verstrekt met een Netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="7db93-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="7db93-108">In dit document worden hoe Hallo muziek Store-toepassing in Hallo-voorbeeldsjabloon voor Azure Resource Manager worden beveiligd.</span><span class="sxs-lookup"><span data-stu-id="7db93-108">This document details how hello Music Store application is secured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="7db93-109">Alle afhankelijkheden en unieke configuraties zijn gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="7db93-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="7db93-110">Implementeer een exemplaar van Hallo oplossing tooyour Azure-abonnement en werk samen met hello Azure Resource Manager-sjabloon voor de beste ervaring Hallo.</span><span class="sxs-lookup"><span data-stu-id="7db93-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="7db93-111">de volledige sjabloon Hallo vindt u hier: [muziek Store wilt implementeren op Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="7db93-111">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="public-ip-address"></a><span data-ttu-id="7db93-112">Openbare IP-adres</span><span class="sxs-lookup"><span data-stu-id="7db93-112">Public IP Address</span></span>
<span data-ttu-id="7db93-113">tooprovide openbare toegang tooan Azure-resource, een openbare IP-adres resource kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7db93-113">tooprovide public access tooan Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="7db93-114">Openbaar IP-adres kan worden geconfigureerd met een statisch of dynamisch IP-adres.</span><span class="sxs-lookup"><span data-stu-id="7db93-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="7db93-115">Als een dynamisch adres wordt gebruikt en Hallo virtuele machine wordt gestopt en de toewijzing ongedaan gemaakt, wordt Hallo adressen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7db93-115">If a dynamic address is used, and hello virtual machine is stopped and deallocated, hello addresses is removed.</span></span> <span data-ttu-id="7db93-116">Wanneer Hallo machine opnieuw wordt gestart, is het mogelijk dat deze een andere openbare IP-adres worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="7db93-116">When hello machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="7db93-117">tooprevent een IP-adres wijzigen, een gereserveerd IP-adres kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7db93-117">tooprevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="7db93-118">Een openbaar IP-adres tooan Hallo Visual Studio nieuwe Wizard Resource toevoegen, met Azure Resource Manager-sjabloon kunnen worden toegevoegd of door een geldige JSON invoegen in een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="7db93-118">A Public IP Address can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="7db93-119">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [openbaar IP-adres](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span><span class="sxs-lookup"><span data-stu-id="7db93-119">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span></span>

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

<span data-ttu-id="7db93-120">Een openbaar IP-adres kunnen worden gekoppeld aan een virtuele netwerkadapter, of een Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="7db93-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="7db93-121">Omdat Hallo muziek Store website gelijkmatig verdeeld zijn over meerdere virtuele machines, is Hallo openbaar IP-adres in dit voorbeeld aangesloten toohello Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="7db93-121">In this example, because hello Music Store website is load balanced across several virtual machines, hello Public IP Address is attached toohello Load Balancer.</span></span>

<span data-ttu-id="7db93-122">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [openbaar IP-adres koppeling met de Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span><span class="sxs-lookup"><span data-stu-id="7db93-122">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

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

<span data-ttu-id="7db93-123">Hallo openbare IP-adres als gezien vanaf hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7db93-123">hello public IP Address as seen from hello Azure portal.</span></span> <span data-ttu-id="7db93-124">U ziet dat Hallo openbaar IP-adres gekoppeld tooa load balancer en niet op een virtuele machine is.</span><span class="sxs-lookup"><span data-stu-id="7db93-124">Notice that hello public IP address is associated tooa load balancer and not a virtual machine.</span></span> <span data-ttu-id="7db93-125">Network load balancers zijn aangegeven in het volgende document Hallo van deze reeks.</span><span class="sxs-lookup"><span data-stu-id="7db93-125">Network load balancers are detailed in hello next document of this series.</span></span>

![Openbare IP-adres](./media/dotnet-core-3-access-security/pubip-win.png)

<span data-ttu-id="7db93-127">Zie voor meer informatie over Azure openbare IP-adressen [IP-adressen in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="7db93-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="7db93-128">Netwerkbeveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="7db93-128">Network Security Group</span></span>
<span data-ttu-id="7db93-129">Zodra de toegang tot stand gebrachte tooAzure resources is, is deze toegang moet worden beperkt.</span><span class="sxs-lookup"><span data-stu-id="7db93-129">Once access has been established tooAzure resources, this access should be limited.</span></span> <span data-ttu-id="7db93-130">Veilige toegang wordt gerealiseerd met behulp van een netwerkbeveiligingsgroep voor Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="7db93-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="7db93-131">Met Hallo muziek Store toepassing voorbeeld alle toegang toohello virtuele machine is beperkt, behalve voor via poort 80 voor HTTP-toegang en -poort 3389 voor RDP-toegang.</span><span class="sxs-lookup"><span data-stu-id="7db93-131">With hello Music Store application sample, all access toohello virtual machine is restricted except for over port 80 for http access, and port 3389 for RDP access.</span></span> <span data-ttu-id="7db93-132">Een Netwerkbeveiligingsgroep tooan Hallo Visual Studio nieuwe Wizard Resource toevoegen, met Azure Resource Manager-sjabloon kunnen worden toegevoegd of door een geldige JSON invoegen in een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="7db93-132">A Network Security Group can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="7db93-133">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Netwerkbeveiligingsgroep](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span><span class="sxs-lookup"><span data-stu-id="7db93-133">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span></span>

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

<span data-ttu-id="7db93-134">In dit voorbeeld is de netwerkbeveiligingsgroep Hallo koppelen met Hallo subnet-object is gedeclareerd in Hallo Virtual Network-resource.</span><span class="sxs-lookup"><span data-stu-id="7db93-134">In this example, hello network security group is associate with hello subnet object declared in hello Virtual Network resource.</span></span> 

<span data-ttu-id="7db93-135">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Netwerkbeveiligingsgroep koppeling met het virtuele netwerk](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span><span class="sxs-lookup"><span data-stu-id="7db93-135">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span></span>

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

<span data-ttu-id="7db93-136">Hier ziet u welke Hallo netwerkbeveiligingsgroep lijkt in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7db93-136">Here is what hello network security group looks like from hello Azure portal.</span></span> <span data-ttu-id="7db93-137">Merk op dat mag een NSG koppelen aan een subnet en / of de netwerk-interface.</span><span class="sxs-lookup"><span data-stu-id="7db93-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="7db93-138">In dit geval is Hallo NSG gekoppeld tooa subnet.</span><span class="sxs-lookup"><span data-stu-id="7db93-138">In this case, hello NSG is associated tooa subnet.</span></span> <span data-ttu-id="7db93-139">In deze configuratie toepassen hello binnenkomende regels tooall virtuele machines verbonden toohello subnet.</span><span class="sxs-lookup"><span data-stu-id="7db93-139">In this configuration, hello inbound rules apply tooall virtual machines connected toohello subnet.</span></span>

![Netwerkbeveiligingsgroep](./media/dotnet-core-3-access-security/nsg-win.png)

<span data-ttu-id="7db93-141">Zie voor gedetailleerde informatie over Netwerkbeveiligingsgroepen [wat is er een Netwerkbeveiligingsgroep](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span><span class="sxs-lookup"><span data-stu-id="7db93-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="7db93-142">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="7db93-142">Next step</span></span>
<hr>

[<span data-ttu-id="7db93-143">Stap 3 - beschikbaarheid en schaal in Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="7db93-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

