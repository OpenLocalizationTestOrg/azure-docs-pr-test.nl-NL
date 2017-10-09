---
title: aaaAvailability en schalen in Azure Resource Manager-sjablonen | Microsoft Docs
description: Virtuele Machine van Azure DotNet belangrijkste zelfstudie
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 494724b5-06af-4dea-a774-ba580cf27527
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a122d8e9536ea5fc2dc9c3f84042ed5c5179d783
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="233a5-103">Beschikbaarheid en schaal in Azure Resource Manager-sjablonen voor virtuele machines van Windows</span><span class="sxs-lookup"><span data-stu-id="233a5-103">Availability and scale in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="233a5-104">Raadpleeg toouptime en Hallo mogelijkheid toomeet vraag beschikbaarheid en schaal.</span><span class="sxs-lookup"><span data-stu-id="233a5-104">Availability and scale refer toouptime and hello ability toomeet demand.</span></span> <span data-ttu-id="233a5-105">Als een toepassing van 99,9% van de tijd hello zijn moet, moet deze toohave een architectuur waarmee meerdere gelijktijdige rekenresources.</span><span class="sxs-lookup"><span data-stu-id="233a5-105">If an application must be up 99.9% of hello time, it needs toohave an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="233a5-106">In plaats van één website, bevat een configuratie met een hoger niveau van beschikbaarheid bijvoorbeeld meerdere exemplaren van dezelfde site, met de technologie voor deze balancing Hallo.</span><span class="sxs-lookup"><span data-stu-id="233a5-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of hello same site, with balancing technology in front of them.</span></span> <span data-ttu-id="233a5-107">In deze configuratie is kunt één exemplaar van de toepassing hello worden uitgeschakeld voor onderhoud, terwijl Hallo resterende toofunction blijven.</span><span class="sxs-lookup"><span data-stu-id="233a5-107">In this configuration, one instance of hello application can be taken down for maintenance, while hello remaining continue toofunction.</span></span> <span data-ttu-id="233a5-108">Schaal op Hallo verwijst daarentegen tooan toepassingen de mogelijkheid tooserve vraag.</span><span class="sxs-lookup"><span data-stu-id="233a5-108">Scale on hello other hand refers tooan applications ability tooserve demand.</span></span> <span data-ttu-id="233a5-109">Met een belasting kan taakverdeling toepassing, toevoegen of verwijderen van instanties van de groep Hallo een toepassing tooscale toomeet vraag.</span><span class="sxs-lookup"><span data-stu-id="233a5-109">With a load balanced application, adding or removing instances from hello pool allows an application tooscale toomeet demand.</span></span>

<span data-ttu-id="233a5-110">Dit document beschrijft hoe Hallo Voorbeeldimplementatie muziek Store is geconfigureerd voor de beschikbaarheid en schaal.</span><span class="sxs-lookup"><span data-stu-id="233a5-110">This document details how hello Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="233a5-111">Alle afhankelijkheden en unieke configuraties zijn gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="233a5-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="233a5-112">Implementeer een exemplaar van Hallo oplossing tooyour Azure-abonnement en werk samen met hello Azure Resource Manager-sjabloon voor de beste ervaring Hallo.</span><span class="sxs-lookup"><span data-stu-id="233a5-112">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="233a5-113">de volledige sjabloon Hallo vindt u hier: [muziek Store wilt implementeren op Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="233a5-113">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="availability-set"></a><span data-ttu-id="233a5-114">Beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="233a5-114">Availability Set</span></span>
<span data-ttu-id="233a5-115">Een Beschikbaarheidsset omvat Azure Virtual Machines naar andere fysieke hosts en andere infrastructurele onderdelen, zoals voedingen en fysieke netwerkhardware logisch.</span><span class="sxs-lookup"><span data-stu-id="233a5-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="233a5-116">Beschikbaarheidssets Zorg ervoor dat tijdens onderhoud, apparaatfout of andere uitvaltijd, niet alle virtuele machines worden gedaan.</span><span class="sxs-lookup"><span data-stu-id="233a5-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="233a5-117">Een Beschikbaarheidsset kunnen worden toegevoegd als tooan Azure Resource Manager-sjabloon met behulp van Visual Studio nieuwe Wizard Resource toevoegen Hallo of geldige JSON invoegen in een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="233a5-117">An Availability Set can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="233a5-118">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Beschikbaarheidsset](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).</span><span class="sxs-lookup"><span data-stu-id="233a5-118">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "availability-set"
  },
  "properties": {
  }
}
```

<span data-ttu-id="233a5-119">Een Beschikbaarheidsset is gedeclareerd als een eigenschap van de bron van een virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="233a5-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="233a5-120">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Beschikbaarheidsset koppeling met de virtuele Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).</span><span class="sxs-lookup"><span data-stu-id="233a5-120">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="233a5-121">Hallo beschikbaarheidsset gezien vanaf hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="233a5-121">hello availability set as seen from hello Azure portal.</span></span> <span data-ttu-id="233a5-122">Elke virtuele machine en de gegevens over configuratie Hallo worden hier beschreven.</span><span class="sxs-lookup"><span data-stu-id="233a5-122">Each virtual machine and details about hello configuration are detailed here.</span></span>

![Beschikbaarheidsset](./media/dotnet-core-4-availability-scale/ase-win.png)

<span data-ttu-id="233a5-124">Zie voor gedetailleerde informatie over Beschikbaarheidssets [beschikbaarheid van virtuele machines beheren](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="233a5-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="233a5-125">Load balancer voor netwerk</span><span class="sxs-lookup"><span data-stu-id="233a5-125">Network Load Balancer</span></span>
<span data-ttu-id="233a5-126">Terwijl een beschikbaarheidsset fouttolerantie van toepassing biedt, beschikbaar een load balancer veel exemplaren van de toepassing hello op één netwerkadres.</span><span class="sxs-lookup"><span data-stu-id="233a5-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of hello application available on a single network address.</span></span> <span data-ttu-id="233a5-127">Meerdere exemplaren van een toepassing kunnen worden gehost op een groot aantal virtuele machines verbonden elkaar tooa load balancer.</span><span class="sxs-lookup"><span data-stu-id="233a5-127">Multiple instances of an application can be hosted on many virtual machines, each one connected tooa load balancer.</span></span> <span data-ttu-id="233a5-128">Als de toepassing hello wordt geopend, Hallo Hallo load balancer routes inkomende aanvraag over Hallo gekoppeld leden.</span><span class="sxs-lookup"><span data-stu-id="233a5-128">As hello application is accessed, hello load balancer routes hello incoming request across hello attached members.</span></span> <span data-ttu-id="233a5-129">Een Load Balancer kan worden toegevoegd met Hallo Visual Studio nieuwe Wizard Resource toevoegen of door het invoegen van juist opgemaakte JSON-resource naar hello Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="233a5-129">A Load Balancer can be added using hello Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into hello Azure Resource Manager template.</span></span>

<span data-ttu-id="233a5-130">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Netwerkbelastingbalancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).</span><span class="sxs-lookup"><span data-stu-id="233a5-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer"
  },
  ........<truncated>
}
```

<span data-ttu-id="233a5-131">Omdat de voorbeeldtoepassing Hallo blootgestelde toohello internet met een openbaar IP-adres, dit adres is gekoppeld aan Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="233a5-131">Because hello sample application is exposed toohello internet with a public IP address, this address is associated with hello load balancer.</span></span> 

<span data-ttu-id="233a5-132">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Network Load Balancer-koppeling met openbare IP-adres](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span><span class="sxs-lookup"><span data-stu-id="233a5-132">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

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

<span data-ttu-id="233a5-133">Van hello Azure-portal toont hello network load balancer overzicht Hallo koppeling met de Hallo openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="233a5-133">From hello Azure portal, hello network load balancer overview shows hello association with hello public IP address.</span></span>

![Load balancer voor netwerk](./media/dotnet-core-4-availability-scale/nlb-win.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="233a5-135">Load Balancer-regel</span><span class="sxs-lookup"><span data-stu-id="233a5-135">Load Balancer Rule</span></span>
<span data-ttu-id="233a5-136">Wanneer u een load balancer, zijn regels die bepalen hoe verkeer wordt verdeeld over Hallo bedoeld resources geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="233a5-136">When using a load balancer, rules are configured that control how traffic is balanced across hello intended resources.</span></span> <span data-ttu-id="233a5-137">Hallo-voorbeeldtoepassing muziek Store verkeer binnenkomt op poort 80 Hallo openbare IP-adres en is verdeeld over de poort 80 van alle virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="233a5-137">With hello sample Music Store application, traffic arrives on port 80 of hello public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="233a5-138">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Load Balancer-regel](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).</span><span class="sxs-lookup"><span data-stu-id="233a5-138">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).</span></span>

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

<span data-ttu-id="233a5-139">Een weergave van Hallo netwerk balancer-regel uit Hallo-portal geladen.</span><span class="sxs-lookup"><span data-stu-id="233a5-139">A view of hello network load balancer rule from hello portal.</span></span>

![Network Load Balancer-regel](./media/dotnet-core-4-availability-scale/lbrule-win.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="233a5-141">Load Balancer-test</span><span class="sxs-lookup"><span data-stu-id="233a5-141">Load Balancer Probe</span></span>
<span data-ttu-id="233a5-142">Hallo load balancer moet ook toomonitor elke virtuele machine zodat aanvragen worden alleen toorunning systemen behandeld.</span><span class="sxs-lookup"><span data-stu-id="233a5-142">hello load balancer also needs toomonitor each virtual machine so that requests are served only toorunning systems.</span></span> <span data-ttu-id="233a5-143">Deze controle vindt plaats door constante zoeken van een vooraf gedefinieerde poort.</span><span class="sxs-lookup"><span data-stu-id="233a5-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="233a5-144">Hallo muziek Store-implementatie is geconfigureerde tooprobe poort 80 op alle opgenomen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="233a5-144">hello Music Store deployment is configured tooprobe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="233a5-145">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Load Balancer-test](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).</span><span class="sxs-lookup"><span data-stu-id="233a5-145">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).</span></span>

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

<span data-ttu-id="233a5-146">Hallo load balancer-test gezien vanaf hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="233a5-146">hello load balancer probe seen from hello Azure portal.</span></span>

![Network Load Balancer-test](./media/dotnet-core-4-availability-scale/lbprobe-win.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="233a5-148">Inkomende NAT-regels</span><span class="sxs-lookup"><span data-stu-id="233a5-148">Inbound NAT Rules</span></span>
<span data-ttu-id="233a5-149">Wanneer u een Load Balancer, regels toobe moeten worden uitgevoerd die niet load balanced toegang tooeach virtuele Machine te bieden.</span><span class="sxs-lookup"><span data-stu-id="233a5-149">When using a Load Balancer, rules need toobe put into place that provide non-load balanced access tooeach Virtual Machine.</span></span> <span data-ttu-id="233a5-150">Bijvoorbeeld, wanneer u een RDP-verbinding met elke virtuele machine maakt, dit verkeer mag geen taakverdeling, in plaats daarvan een vooraf bepaald pad moet worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="233a5-150">For instance, when creating an RDP connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="233a5-151">vooraf bepaald paden zijn geconfigureerd met behulp van de bron van een binnenkomende NAT-regel.</span><span class="sxs-lookup"><span data-stu-id="233a5-151">Pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="233a5-152">Deze bron, binnenkomende communicatie, kan worden toegewezen tooindividual virtuele Machines.</span><span class="sxs-lookup"><span data-stu-id="233a5-152">Using this resource, inbound communication can be mapped tooindividual Virtual Machines.</span></span> 

<span data-ttu-id="233a5-153">Met Hallo muziek Store-toepassing is een poort die begint bij 5000 toegewezen tooport 3389 op elke virtuele Machine voor RDP-toegang.</span><span class="sxs-lookup"><span data-stu-id="233a5-153">With hello Music Store application, a port starting at 5000 is mapped tooport 3389 on each Virtual Machine for RDP access.</span></span> <span data-ttu-id="233a5-154">Hallo `copyindex()` functie is gebruikte tooincrement Hallo binnenkomende poort, zoals die Hallo tweede virtuele Machine een binnenkomende poort van 5001 ontvangt, derde 5002 hello, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="233a5-154">hello `copyindex()` function is used tooincrement hello incoming port, such that hello second Virtual Machine receives an incoming port of 5001, hello third 5002, and so on.</span></span>

<span data-ttu-id="233a5-155">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [binnenkomende NAT-regels](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260).</span><span class="sxs-lookup"><span data-stu-id="233a5-155">Follow this link toosee hello JSON sample within hello Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'RDP-VM', copyIndex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
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
    "backendPort": 3389,
    "enableFloatingIP": false
  }
}
```

<span data-ttu-id="233a5-156">Voorbeeld van een binnenkomende NAT-regel als zoals weergegeven in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="233a5-156">One example inbound NAT rule as seen in hello Azure portal.</span></span> <span data-ttu-id="233a5-157">Een RDP-NAT-regel is gemaakt voor elke virtuele machine in Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="233a5-157">An RDP NAT rule is created for each virtual machine in hello deployment.</span></span>

![Binnenkomende NAT-regel](./media/dotnet-core-4-availability-scale/natrule-win.png)

<span data-ttu-id="233a5-159">Zie voor gedetailleerde informatie over hello Azure Network Load Balancer [taakverdeling voor Azure-infrastructuurservices](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="233a5-159">For in-depth information on hello Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="233a5-160">Meerdere virtuele machines implementeren</span><span class="sxs-lookup"><span data-stu-id="233a5-160">Deploy multiple VMs</span></span>
<span data-ttu-id="233a5-161">Ten slotte zijn meerdere virtuele machines voor een functie Beschikbaarheidsset of Load Balancer tooeffectively vereist.</span><span class="sxs-lookup"><span data-stu-id="233a5-161">Finally, for an Availability Set or Load Balancer tooeffectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="233a5-162">Meerdere virtuele machines kunnen worden geïmplementeerd met behulp van de functie voor hello Azure Resource Manager-sjabloon kopiëren.</span><span class="sxs-lookup"><span data-stu-id="233a5-162">Multiple VMs can be deployed using hello Azure Resource Manager template copy function.</span></span> <span data-ttu-id="233a5-163">Hallo kopieerfunctie gebruikt, is niet nodig toodefine een beperkt aantal virtuele Machines, in plaats daarvan deze waarde kan dynamisch worden verstrekt op Hallo moment van implementatie.</span><span class="sxs-lookup"><span data-stu-id="233a5-163">Using hello copy function, it is not necessary toodefine a finite number of Virtual Machines, rather this value can be dynamically provided at hello time of deployment.</span></span> <span data-ttu-id="233a5-164">Hallo kopieerfunctie verbruikt Hallo aantal exemplaren toobe gemaakt en ingangen Hallo juiste aantal virtuele machines en de bijbehorende resources implementeren.</span><span class="sxs-lookup"><span data-stu-id="233a5-164">hello copy function consumes hello number of instances toobe created and handles deploying hello proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="233a5-165">In voorbeeldsjabloon Hallo muziek Store, een parameter waarmee het aantal instanties gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="233a5-165">In hello Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="233a5-166">Dit nummer wordt gebruikt in de gehele Hallo sjabloon bij het maken van virtuele machines en gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="233a5-166">This number is used throughout hello template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 2,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
},
```

<span data-ttu-id="233a5-167">Op Hallo virtuele-machinebron, Hallo kopie lus krijgt een naam en het aantal exemplaren parameter Hallo toocontrol Hallo aantal resulterende exemplaren gebruikt.</span><span class="sxs-lookup"><span data-stu-id="233a5-167">On hello Virtual Machine resource, hello copy loop is given a name and hello number of instances parameter used toocontrol hello number of resulting copies.</span></span>

<span data-ttu-id="233a5-168">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [kopieerfunctie van het virtuele Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290).</span><span class="sxs-lookup"><span data-stu-id="233a5-168">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  }
```

<span data-ttu-id="233a5-169">Hallo huidige herhaling van Hallo kopieerfunctie toegankelijk zijn met de Hallo `copyIndex()` functie.</span><span class="sxs-lookup"><span data-stu-id="233a5-169">hello current iteration of hello copy function can be accessed with hello `copyIndex()` function.</span></span> <span data-ttu-id="233a5-170">Hallo waarde van de index kopieerfunctie Hallo mag gebruikte tooname virtuele machines en andere bronnen.</span><span class="sxs-lookup"><span data-stu-id="233a5-170">hello value of hello copy index function can be used tooname virtual machines and other resources.</span></span> <span data-ttu-id="233a5-171">Bijvoorbeeld, als er twee exemplaren van een virtuele machine zijn geïmplementeerd, moeten ze verschillende namen.</span><span class="sxs-lookup"><span data-stu-id="233a5-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="233a5-172">Hallo `copyIndex()` functie kan worden gebruikt als onderdeel van Hallo virtuele machine toocreate naam een unieke naam.</span><span class="sxs-lookup"><span data-stu-id="233a5-172">hello `copyIndex()` function can be used as part of hello virtual machine name toocreate a unique name.</span></span> <span data-ttu-id="233a5-173">Een voorbeeld van Hallo `copyindex()` functie gebruikt voor de naamgeving van de toepassing in Hallo virtuele-machinebron weergegeven.</span><span class="sxs-lookup"><span data-stu-id="233a5-173">An example of hello `copyindex()` function used for naming purposes can be seen in hello Virtual Machine resource.</span></span> <span data-ttu-id="233a5-174">Hier Hallo computernaam is een samenvoeging van Hallo `vmName` parameter en Hallo `copyIndex()` functie.</span><span class="sxs-lookup"><span data-stu-id="233a5-174">Here, hello computer name is a concatenation of hello `vmName` parameter, and hello `copyIndex()` function.</span></span> 

<span data-ttu-id="233a5-175">Volg deze link toosee Hallo JSON-voorbeeld binnen Hallo Resource Manager-sjabloon – [Index kopieerfunctie](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309).</span><span class="sxs-lookup"><span data-stu-id="233a5-175">Follow this link toosee hello JSON sample within hello Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309).</span></span> 

```json
"osProfile": {
  "computerName": "[concat(variables('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "adminPassword": "[parameters('adminPassword')]"
}
```

<span data-ttu-id="233a5-176">Hallo `copyIndex` functie Hallo muziek Store voorbeeldsjabloon meerdere keren wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="233a5-176">hello `copyIndex` function is used several times in hello Music Store sample template.</span></span> <span data-ttu-id="233a5-177">Bronnen en functies met behulp van `copyIndex` alles specifieke tooa één exemplaar van Hallo virtuele machine dergelijke en netwerkinterface, de regels van load balancer, en een is afhankelijk van functies.</span><span class="sxs-lookup"><span data-stu-id="233a5-177">Resources and functions utilizing `copyIndex` include anything specific tooa single instance of hello virtual machine such and network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="233a5-178">Zie voor meer informatie over Hallo kopieerfunctie [maken van meerdere exemplaren van resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="233a5-178">For more information on hello copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="233a5-179">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="233a5-179">Next step</span></span>
<hr>

[<span data-ttu-id="233a5-180">Stap 4: implementatie van de toepassing met Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="233a5-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

