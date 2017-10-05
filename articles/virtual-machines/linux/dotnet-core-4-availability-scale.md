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
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="f0e35-103">Beschikbaarheid en schaal in Azure Resource Manager-sjablonen voor virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="f0e35-103">Availability and scale in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="f0e35-104">Beschikbaarheid en schaal Raadpleeg bedrijfstijd en de mogelijkheid om te voldoen aan de vraag.</span><span class="sxs-lookup"><span data-stu-id="f0e35-104">Availability and scale refer to uptime and the ability to meet demand.</span></span> <span data-ttu-id="f0e35-105">Als een toepassing van 99,9% van de tijd zijn moet, moet deze hebben een architectuur waarmee meerdere gelijktijdige rekenresources.</span><span class="sxs-lookup"><span data-stu-id="f0e35-105">If an application must be up 99.9% of the time, it needs to have an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="f0e35-106">In plaats van één website, bevat een configuratie met een hoger niveau van beschikbaarheid bijvoorbeeld meerdere exemplaren van dezelfde site, met de technologie voor deze netwerktaakverdeling.</span><span class="sxs-lookup"><span data-stu-id="f0e35-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of the same site, with balancing technology in front of them.</span></span> <span data-ttu-id="f0e35-107">In deze configuratie is kan één exemplaar van de toepassing worden uitgeschakeld voor onderhoud, terwijl de resterende blijven werken.</span><span class="sxs-lookup"><span data-stu-id="f0e35-107">In this configuration, one instance of the application can be taken down for maintenance, while the remaining continue to function.</span></span> <span data-ttu-id="f0e35-108">Schaal verwijst daarentegen naar een kunnen toepassingen vraag.</span><span class="sxs-lookup"><span data-stu-id="f0e35-108">Scale on the other hand refers to an applications ability to serve demand.</span></span> <span data-ttu-id="f0e35-109">Met een load kan balanced toepassing, het toevoegen of verwijderen van instanties van de groep een toepassing schalen om te voldoen aan de vraag.</span><span class="sxs-lookup"><span data-stu-id="f0e35-109">With a load balanced application, adding or removing instances from the pool allows an application to scale to meet demand.</span></span>

<span data-ttu-id="f0e35-110">Dit document beschrijft hoe de implementatie van de steekproef muziek Store is geconfigureerd voor de beschikbaarheid en schaal.</span><span class="sxs-lookup"><span data-stu-id="f0e35-110">This document details how the Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="f0e35-111">Alle afhankelijkheden en unieke configuraties zijn gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="f0e35-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="f0e35-112">Implementeer een exemplaar van de oplossing voor uw Azure-abonnement en werk samen met de Azure Resource Manager-sjabloon voor de beste ervaring.</span><span class="sxs-lookup"><span data-stu-id="f0e35-112">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="f0e35-113">De volledige sjabloon vindt u hier: [muziek Store wilt implementeren op een virtuele Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="f0e35-113">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="availability-set"></a><span data-ttu-id="f0e35-114">Beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="f0e35-114">Availability Set</span></span>
<span data-ttu-id="f0e35-115">Een Beschikbaarheidsset omvat Azure Virtual Machines naar andere fysieke hosts en andere infrastructurele onderdelen, zoals voedingen en fysieke netwerkhardware logisch.</span><span class="sxs-lookup"><span data-stu-id="f0e35-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="f0e35-116">Beschikbaarheidssets Zorg ervoor dat tijdens onderhoud, apparaatfout of andere uitvaltijd, niet alle virtuele machines worden gedaan.</span><span class="sxs-lookup"><span data-stu-id="f0e35-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="f0e35-117">Een Beschikbaarheidsset kunnen worden toegevoegd aan een Azure Resource Manager-sjabloon met behulp van de Visual Studio nieuwe Wizard Resource toevoegen of geldige JSON invoegen in een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f0e35-117">An Availability Set can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="f0e35-118">Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Beschikbaarheidsset](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span><span class="sxs-lookup"><span data-stu-id="f0e35-118">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span></span>

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

<span data-ttu-id="f0e35-119">Een Beschikbaarheidsset is gedeclareerd als een eigenschap van de bron van een virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="f0e35-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="f0e35-120">Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Beschikbaarheidsset koppeling met de virtuele Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span><span class="sxs-lookup"><span data-stu-id="f0e35-120">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="f0e35-121">De beschikbaarheidsset gezien vanaf de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f0e35-121">The availability set as seen from the Azure portal.</span></span> <span data-ttu-id="f0e35-122">Elke virtuele machine en de gegevens over de configuratie worden hier beschreven.</span><span class="sxs-lookup"><span data-stu-id="f0e35-122">Each virtual machine and details about the configuration are detailed here.</span></span>

![Beschikbaarheidsset](./media/dotnet-core-4-availability-scale/aset.png)

<span data-ttu-id="f0e35-124">Zie voor gedetailleerde informatie over Beschikbaarheidssets [beschikbaarheid van virtuele machines beheren](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f0e35-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="f0e35-125">Load balancer voor netwerk</span><span class="sxs-lookup"><span data-stu-id="f0e35-125">Network Load Balancer</span></span>
<span data-ttu-id="f0e35-126">Terwijl een beschikbaarheidsset fouttolerantie van toepassing biedt, beschikbaar een load balancer veel exemplaren van de toepassing op één netwerkadres.</span><span class="sxs-lookup"><span data-stu-id="f0e35-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of the application available on a single network address.</span></span> <span data-ttu-id="f0e35-127">Meerdere exemplaren van een toepassing kunnen worden gehost op veel virtuele machines, elk een is verbonden met een load balancer.</span><span class="sxs-lookup"><span data-stu-id="f0e35-127">Multiple instances of an application can be hosted on many virtual machines, each one connected to a load balancer.</span></span> <span data-ttu-id="f0e35-128">Als de toepassing wordt geopend, stuurt de load balancer de binnenkomende aanvraag via de gekoppelde leden.</span><span class="sxs-lookup"><span data-stu-id="f0e35-128">As the application is accessed, the load balancer routes the incoming request across the attached members.</span></span> <span data-ttu-id="f0e35-129">Een Load Balancer kan worden toegevoegd met de Visual Studio nieuwe Wizard Resource toevoegen of door het invoegen van juist opgemaakte JSON-resource in de Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f0e35-129">A Load Balancer can be added using the Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into the Azure Resource Manager template.</span></span>

<span data-ttu-id="f0e35-130">Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Netwerkbelastingbalancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span><span class="sxs-lookup"><span data-stu-id="f0e35-130">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

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

<span data-ttu-id="f0e35-131">Omdat de voorbeeldtoepassing wordt blootgesteld aan internet met een openbaar IP-adres, moet dit adres is gekoppeld aan de load balancer.</span><span class="sxs-lookup"><span data-stu-id="f0e35-131">Because the sample application is exposed to the internet with a public IP address, this address is associated with the load balancer.</span></span> 

<span data-ttu-id="f0e35-132">Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Network Load Balancer-koppeling met openbare IP-adres](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span><span class="sxs-lookup"><span data-stu-id="f0e35-132">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span></span>

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

<span data-ttu-id="f0e35-133">Vanuit de Azure-portal ziet network load balancer overzicht u de koppeling met het openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="f0e35-133">From the Azure portal, the network load balancer overview shows the association with the public IP address.</span></span>

![Load balancer voor netwerk](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="f0e35-135">Load Balancer-regel</span><span class="sxs-lookup"><span data-stu-id="f0e35-135">Load Balancer Rule</span></span>
<span data-ttu-id="f0e35-136">Wanneer u een load balancer, zijn regels die bepalen hoe verkeer wordt verdeeld over de beoogde resources geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="f0e35-136">When using a load balancer, rules are configured that control how traffic is balanced across the intended resources.</span></span> <span data-ttu-id="f0e35-137">Met de voorbeeldtoepassing muziek Store verkeer binnenkomt op poort 80 van het openbare IP-adres en is verdeeld over de poort 80 van alle virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f0e35-137">With the sample Music Store application, traffic arrives on port 80 of the public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="f0e35-138">Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Load Balancer-regel](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="f0e35-138">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span>

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

<span data-ttu-id="f0e35-139">Een weergave van de network load balancer-regel van de portal.</span><span class="sxs-lookup"><span data-stu-id="f0e35-139">A view of the network load balancer rule from the portal.</span></span>

![Network Load Balancer-regel](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="f0e35-141">Load Balancer-test</span><span class="sxs-lookup"><span data-stu-id="f0e35-141">Load Balancer Probe</span></span>
<span data-ttu-id="f0e35-142">Er moet ook de load balancer voor het bewaken van elke virtuele machine zodat aanvragen alleen voor computers die worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="f0e35-142">The load balancer also needs to monitor each virtual machine so that requests are served only to running systems.</span></span> <span data-ttu-id="f0e35-143">Deze controle vindt plaats door constante zoeken van een vooraf gedefinieerde poort.</span><span class="sxs-lookup"><span data-stu-id="f0e35-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="f0e35-144">De muziek Store-implementatie is geconfigureerd om poort 80 op alle opgenomen virtuele machines test.</span><span class="sxs-lookup"><span data-stu-id="f0e35-144">The Music Store deployment is configured to probe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="f0e35-145">Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Load Balancer-test](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span><span class="sxs-lookup"><span data-stu-id="f0e35-145">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span></span>

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

<span data-ttu-id="f0e35-146">De load balancer-test gezien vanaf de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f0e35-146">The load balancer probe seen from the Azure portal.</span></span>

![Network Load Balancer-test](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="f0e35-148">Inkomende NAT-regels</span><span class="sxs-lookup"><span data-stu-id="f0e35-148">Inbound NAT Rules</span></span>
<span data-ttu-id="f0e35-149">Wanneer u een Load Balancer, moeten regels worden ingesteld die niet load balanced toegang bieden tot elke virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="f0e35-149">When using a Load Balancer, rules need to be put into place that provide non-load balanced access to each Virtual Machine.</span></span> <span data-ttu-id="f0e35-150">Bijvoorbeeld, wanneer u een SSH-verbinding met elke virtuele machine maakt, dit verkeer mag geen taakverdeling, in plaats daarvan een vooraf bepaald pad moet worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="f0e35-150">For instance, when creating an SSH connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="f0e35-151">vooraf bepaald paden zijn geconfigureerd met behulp van de bron van een binnenkomende NAT-regel.</span><span class="sxs-lookup"><span data-stu-id="f0e35-151">pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="f0e35-152">Met deze bron, worden binnenkomende communicatie toegewezen aan afzonderlijke virtuele Machines.</span><span class="sxs-lookup"><span data-stu-id="f0e35-152">Using this resource, inbound communication can be mapped to individual Virtual Machines.</span></span> 

<span data-ttu-id="f0e35-153">Met de toepassing muziek Store is een poort die begint bij 5000 toegewezen aan poort 22 op elke virtuele Machine voor SSH-toegang.</span><span class="sxs-lookup"><span data-stu-id="f0e35-153">With the Music Store application, a port starting at 5000 is mapped to port 22 on each Virtual Machine for SSH access.</span></span> <span data-ttu-id="f0e35-154">De `copyindex()` functie wordt gebruikt om de binnenkomende poort verhogen zodat de tweede virtuele Machine ontvangt een binnenkomende poort van 5001, het derde 5002 enzovoort.</span><span class="sxs-lookup"><span data-stu-id="f0e35-154">The `copyindex()` function is used to increment the incoming port, such that the second Virtual Machine receives an incoming port of 5001, the third 5002, and so on.</span></span> 

<span data-ttu-id="f0e35-155">Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [binnenkomende NAT-regels](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="f0e35-155">Follow this link to see the JSON sample within the Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span> 

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

<span data-ttu-id="f0e35-156">Voorbeeld van een binnenkomende NAT-regel, zoals in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f0e35-156">One example inbound NAT rule as seen in the Azure portal.</span></span> <span data-ttu-id="f0e35-157">Een SSH-NAT-regel is gemaakt voor elke virtuele machine in de implementatie.</span><span class="sxs-lookup"><span data-stu-id="f0e35-157">An SSH NAT rule is created for each virtual machine in the deployment.</span></span>

![Binnenkomende NAT-regel](./media/dotnet-core-4-availability-scale/natrule.png)

<span data-ttu-id="f0e35-159">Zie voor gedetailleerde informatie over Azure Network Load Balancer [taakverdeling voor Azure-infrastructuurservices](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f0e35-159">For in-depth information on the Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="f0e35-160">Meerdere virtuele machines implementeren</span><span class="sxs-lookup"><span data-stu-id="f0e35-160">Deploy multiple VMs</span></span>
<span data-ttu-id="f0e35-161">Ten slotte zijn meerdere virtuele machines voor een Beschikbaarheidsset of Load Balancer effectief werken, vereist.</span><span class="sxs-lookup"><span data-stu-id="f0e35-161">Finally, for an Availability Set or Load Balancer to effectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="f0e35-162">Meerdere virtuele machines kunnen worden geïmplementeerd met behulp van de kopieerfunctie van het Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f0e35-162">Multiple VMs can be deployed using the Azure Resource Manager template copy function.</span></span> <span data-ttu-id="f0e35-163">Met behulp van de functie kopiëren, is het niet nodig voor het definiëren van een bepaald aantal virtuele Machines, in plaats daarvan deze waarde kan dynamisch worden verstrekt op het moment van implementatie.</span><span class="sxs-lookup"><span data-stu-id="f0e35-163">Using the copy function, it is not necessary to define a finite number of Virtual Machines, rather this value can be dynamically provided at the time of deployment.</span></span> <span data-ttu-id="f0e35-164">De functie kopiëren neemt het aantal exemplaren gemaakt en verwerkt het juiste aantal virtuele machines en de bijbehorende resources implementeren.</span><span class="sxs-lookup"><span data-stu-id="f0e35-164">The copy function consumes the number of instances to created and handles deploying the proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="f0e35-165">In de sjabloon muziek Store voorbeeld is een parameter waarmee het aantal instanties gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="f0e35-165">In the Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="f0e35-166">Dit nummer wordt gebruikt in de sjabloon bij het maken van virtuele machines en gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="f0e35-166">This number is used throughout the template when creating virtual machines and related resources.</span></span>

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

<span data-ttu-id="f0e35-167">Op de bron van de virtuele Machine krijgt de lus kopiëren een naam en het aantal exemplaren parameter gebruikt voor het beheren van het aantal resulterende exemplaren.</span><span class="sxs-lookup"><span data-stu-id="f0e35-167">On the Virtual Machine resource, the copy loop is given a name and the number of instances parameter used to control the number of resulting copies.</span></span>

<span data-ttu-id="f0e35-168">Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [kopieerfunctie van het virtuele Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span><span class="sxs-lookup"><span data-stu-id="f0e35-168">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span></span> 

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

<span data-ttu-id="f0e35-169">De huidige herhaling van de functie kopiëren is toegankelijk via de `copyIndex()` functie.</span><span class="sxs-lookup"><span data-stu-id="f0e35-169">The current iteration of the copy function can be accessed with the `copyIndex()` function.</span></span> <span data-ttu-id="f0e35-170">De waarde van de functie voor kopiëren-index kan worden gebruikt als naam voor virtuele machines en andere bronnen.</span><span class="sxs-lookup"><span data-stu-id="f0e35-170">The value of the copy index function can be used to name virtual machines and other resources.</span></span> <span data-ttu-id="f0e35-171">Bijvoorbeeld, als er twee exemplaren van een virtuele machine zijn geïmplementeerd, moeten ze verschillende namen.</span><span class="sxs-lookup"><span data-stu-id="f0e35-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="f0e35-172">De `copyIndex()` functie kan worden gebruikt als onderdeel van de naam van de virtuele machine een unieke naam maken.</span><span class="sxs-lookup"><span data-stu-id="f0e35-172">The `copyIndex()` function can be used as part of the virtual machine name to create a unique name.</span></span> <span data-ttu-id="f0e35-173">Een voorbeeld van de `copyindex()` functie gebruikt voor de naamgeving van de toepassing wordt weergegeven in de bron van de virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="f0e35-173">An example of the `copyindex()` function used for naming purposes can be seen in the Virtual Machine resource.</span></span> <span data-ttu-id="f0e35-174">Naam van de computer is hier een samenvoeging van de `vmName` parameter, en de `copyIndex()` functie.</span><span class="sxs-lookup"><span data-stu-id="f0e35-174">Here, the computer name is a concatenation of the `vmName` parameter, and the `copyIndex()` function.</span></span> 

<span data-ttu-id="f0e35-175">Volg deze link om te zien van de JSON-voorbeeld in de Resource Manager-sjabloon – [Index kopieerfunctie](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span><span class="sxs-lookup"><span data-stu-id="f0e35-175">Follow this link to see the JSON sample within the Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span></span> 

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

<span data-ttu-id="f0e35-176">De `copyIndex` functie meerdere keren wordt gebruikt in de winkel voorbeeldsjabloon.</span><span class="sxs-lookup"><span data-stu-id="f0e35-176">The `copyIndex` function is used several times in the Music Store sample template.</span></span> <span data-ttu-id="f0e35-177">Bronnen en functies met behulp van `copyIndex` bevat alle specifiek zijn voor één exemplaar van de virtuele machine, zoals netwerkinterface, de regels van load balancer, en een is afhankelijk van functies.</span><span class="sxs-lookup"><span data-stu-id="f0e35-177">Resources and functions utilizing `copyIndex` include anything specific to a single instance of the virtual machine such as network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="f0e35-178">Zie voor meer informatie over de functie kopiëren [maken van meerdere exemplaren van resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="f0e35-178">For more information on the copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="f0e35-179">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="f0e35-179">Next step</span></span>
<hr>

[<span data-ttu-id="f0e35-180">Stap 4: implementatie van de toepassing met Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="f0e35-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

