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
# <a name="access-and-security-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="8ab5e-103">Toegang en beveiliging in Azure Resource Manager-sjablonen voor virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="8ab5e-103">Access and security in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="8ab5e-104">Toepassingen die worden gehost in Azure waarschijnlijk moeten toegang via internet of via een VPN-/ Express Route-verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-104">Applications hosted in Azure likely need to be access over the internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="8ab5e-105">De website wordt met het voorbeeld van de toepassing muziek Store beschikbaar gesteld op internet met een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-105">With the Music Store application sample, the web site is made available on the internet with a public IP address.</span></span> <span data-ttu-id="8ab5e-106">Met toegang tot stand gebracht, moeten verbindingen met de toepassing en toegang tot de resources van de virtuele machine zelf worden beveiligd.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-106">With access established, connections to the application and access to the virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="8ab5e-107">Deze beveiliging wordt verstrekt met een Netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="8ab5e-108">Dit document beschrijft hoe de muziek Store-toepassing in de steekproef Azure Resource Manager-sjabloon wordt beveiligd.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-108">This document details how the Music Store application is secured in the sample Azure Resource Manager template.</span></span> <span data-ttu-id="8ab5e-109">Alle afhankelijkheden en unieke configuraties zijn gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="8ab5e-110">Implementeer een exemplaar van de oplossing voor uw Azure-abonnement en werk samen met de Azure Resource Manager-sjabloon voor de beste ervaring.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="8ab5e-111">De volledige sjabloon vindt u hier: [muziek Store wilt implementeren op een virtuele Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="8ab5e-111">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span> 

## <a name="public-ip-address"></a><span data-ttu-id="8ab5e-112">Openbare IP-adres</span><span class="sxs-lookup"><span data-stu-id="8ab5e-112">Public IP Address</span></span>
<span data-ttu-id="8ab5e-113">Als u openbare toegang tot een Azure-resource maken, kan een openbare IP-adres resource worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-113">To provide public access to an Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="8ab5e-114">Openbaar IP-adres kan worden geconfigureerd met een statisch of dynamisch IP-adres.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="8ab5e-115">Als een dynamisch adres wordt gebruikt en de virtuele machine wordt gestopt en de toewijzing ongedaan gemaakt, wordt de adressen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-115">If a dynamic address is used, and the virtual machine is stopped and deallocated, the addresses is removed.</span></span> <span data-ttu-id="8ab5e-116">Wanneer de computer opnieuw wordt gestart, is het mogelijk dat deze een andere openbare IP-adres worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-116">When the machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="8ab5e-117">Als u wilt voorkomen dat een IP-adres wijzigen, kan een gereserveerd IP-adres worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-117">To prevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="8ab5e-118">Een openbaar IP-adres kunnen worden toegevoegd aan een Azure Resource Manager-sjabloon met behulp van de Visual Studio nieuwe Wizard Resource toevoegen of door een geldige JSON invoegen in een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-118">A Public IP Address can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="8ab5e-119">Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [openbaar IP-adres](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L121).</span><span class="sxs-lookup"><span data-stu-id="8ab5e-119">Follow this link to see the JSON sample within the Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L121).</span></span>

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

<span data-ttu-id="8ab5e-120">Een openbaar IP-adres kunnen worden gekoppeld aan een virtuele netwerkadapter, of een Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="8ab5e-121">In dit voorbeeld dat omdat de website van de winkel gelijkmatig verdeeld zijn over meerdere virtuele machines, is het openbare IP-adres is gekoppeld aan de Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-121">In this example, because the Music Store website is load balanced across several virtual machines, the Public IP Address is attached to the Load Balancer.</span></span>

<span data-ttu-id="8ab5e-122">Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [openbaar IP-adres koppeling met de Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span><span class="sxs-lookup"><span data-stu-id="8ab5e-122">Follow this link to see the JSON sample within the Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

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

<span data-ttu-id="8ab5e-123">Het openbare IP-adres zoals weergegeven in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-123">The public IP Address as seen from the Azure portal.</span></span> <span data-ttu-id="8ab5e-124">U ziet dat het openbare IP-adres gekoppeld aan een load balancer en niet een virtuele machine is.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-124">Notice that the public IP address is associated to a load balancer and not a virtual machine.</span></span> <span data-ttu-id="8ab5e-125">Network load balancers zijn aangegeven in het volgende document van deze reeks.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-125">Network load balancers are detailed in the next document of this series.</span></span>

![Openbare IP-adres](./media/dotnet-core-3-access-security/pubip.png)

<span data-ttu-id="8ab5e-127">Zie voor meer informatie over Azure openbare IP-adressen [IP-adressen in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="8ab5e-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="8ab5e-128">Netwerkbeveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="8ab5e-128">Network Security Group</span></span>
<span data-ttu-id="8ab5e-129">Zodra de toegang is ingesteld voor Azure-resources, is deze toegang moet worden beperkt.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-129">Once access has been established to Azure resources, this access should be limited.</span></span> <span data-ttu-id="8ab5e-130">Veilige toegang wordt gerealiseerd met behulp van een netwerkbeveiligingsgroep voor Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="8ab5e-131">Met het voorbeeld van de toepassing muziek Store is alle toegang tot de virtuele machine beperkt, behalve voor via poort 80 voor HTTP-toegang en -poort 22 voor SSH-toegang.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-131">With the Music Store application sample, all access to the virtual machine is restricted except for over port 80 for http access, and port 22 for SSH access.</span></span> <span data-ttu-id="8ab5e-132">Een Netwerkbeveiligingsgroep kunnen worden toegevoegd aan een Azure Resource Manager-sjabloon met behulp van de Visual Studio nieuwe Wizard Resource toevoegen of door een geldige JSON invoegen in een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-132">A Network Security Group can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="8ab5e-133">Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Netwerkbeveiligingsgroep](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L68).</span><span class="sxs-lookup"><span data-stu-id="8ab5e-133">Follow this link to see the JSON sample within the Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L68).</span></span>

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

<span data-ttu-id="8ab5e-134">In dit voorbeeld wordt de netwerkbeveiligingsgroep koppelen aan het subnetobject dat is gedeclareerd in de bron van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-134">In this example, the network security group is associate with the subnet object declared in the Virtual Network resource.</span></span> 

<span data-ttu-id="8ab5e-135">Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Netwerkbeveiligingsgroep koppeling met het virtuele netwerk](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L158).</span><span class="sxs-lookup"><span data-stu-id="8ab5e-135">Follow this link to see the JSON sample within the Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L158).</span></span>

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

<span data-ttu-id="8ab5e-136">Hier wordt de netwerkbeveiligingsgroep ziet er als vanuit de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-136">Here is what the network security group looks like from the Azure portal.</span></span> <span data-ttu-id="8ab5e-137">Merk op dat mag een NSG koppelen aan een subnet en / of de netwerk-interface.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="8ab5e-138">In dit geval wordt is het NSG gekoppeld aan een subnet.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-138">In this case, the NSG is associated to a subnet.</span></span> <span data-ttu-id="8ab5e-139">In deze configuratie worden de regels voor binnenkomende verbindingen van toepassing op alle virtuele machines die zijn verbonden met het subnet.</span><span class="sxs-lookup"><span data-stu-id="8ab5e-139">In this configuration, the inbound rules apply to all virtual machines connected to the subnet.</span></span>

![Netwerkbeveiligingsgroep](./media/dotnet-core-3-access-security/nsg.png)

<span data-ttu-id="8ab5e-141">Zie voor gedetailleerde informatie over Netwerkbeveiligingsgroepen [wat is er een Netwerkbeveiligingsgroep](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span><span class="sxs-lookup"><span data-stu-id="8ab5e-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="8ab5e-142">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="8ab5e-142">Next step</span></span>
<hr>

[<span data-ttu-id="8ab5e-143">Stap 3 - beschikbaarheid en schaal in Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="8ab5e-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

