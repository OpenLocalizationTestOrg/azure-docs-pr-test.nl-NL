---
title: aaaHow tooload saldo Linux virtuele machines in Azure | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure balancer toocreate een maximaal beschikbare en beveiligde toepassing geladen over drie Linux VM 's
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="832af-103">Hoe tooload balans vinden tussen virtuele Linux-machines in Azure toocreate een maximaal beschikbare toepassing</span><span class="sxs-lookup"><span data-stu-id="832af-103">How tooload balance Linux virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="832af-104">Taakverdeling biedt een hoger niveau van de beschikbaarheid van binnenkomende aanvragen verspreid over meerdere virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="832af-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="832af-105">In deze zelfstudie leert u Hallo verschillende onderdelen van hello Azure load balancer die verkeer distribueren en bieden hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="832af-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="832af-106">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="832af-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="832af-107">Een Azure load balancer maken</span><span class="sxs-lookup"><span data-stu-id="832af-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="832af-108">Een load balancer health test maken</span><span class="sxs-lookup"><span data-stu-id="832af-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="832af-109">Regels voor netwerkverkeer voor de load balancer maken</span><span class="sxs-lookup"><span data-stu-id="832af-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="832af-110">Cloud-init toocreate een eenvoudige Node.js-app gebruiken</span><span class="sxs-lookup"><span data-stu-id="832af-110">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="832af-111">Virtuele machines maken en koppelen tooa load balancer</span><span class="sxs-lookup"><span data-stu-id="832af-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="832af-112">Een load balancer in actie weergeven</span><span class="sxs-lookup"><span data-stu-id="832af-112">View a load balancer in action</span></span>
> * <span data-ttu-id="832af-113">Toevoegen of virtuele machines van een load balancer verwijderen</span><span class="sxs-lookup"><span data-stu-id="832af-113">Add and remove VMs from a load balancer</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="832af-114">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="832af-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="832af-115">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="832af-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="832af-116">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="832af-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="azure-load-balancer-overview"></a><span data-ttu-id="832af-117">Overzicht van Azure load balancer</span><span class="sxs-lookup"><span data-stu-id="832af-117">Azure load balancer overview</span></span>
<span data-ttu-id="832af-118">Een Azure load balancer is een Layer-4 (TCP, UDP) load balancer die zorgt voor hoge beschikbaarheid door het distribueren van inkomend verkeer tussen orde virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="832af-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="832af-119">Een load balancer health test een bepaalde poort op elke virtuele machine bewaakt en distribueert u alleen verkeer tooan operationele VM.</span><span class="sxs-lookup"><span data-stu-id="832af-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="832af-120">U definieert een front-end-IP-configuratie met een of meer openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="832af-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="832af-121">Deze front-end-IP-configuratie kan de load balancer en toepassingen toobe toegankelijk via Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="832af-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="832af-122">Virtuele machines verbinding tooa load balancer met behulp van de virtuele netwerkinterfacekaart (NIC).</span><span class="sxs-lookup"><span data-stu-id="832af-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="832af-123">toodistribute verkeer toohello VM's, een back-end-adresgroep bevat Hallo IP-adressen van Hallo virtuele (NIC's) verbonden toohello load balancer.</span><span class="sxs-lookup"><span data-stu-id="832af-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="832af-124">toocontrol hello stroom van verkeer, kunt u definiëren load balancerregels voor specifieke poorten en protocollen die zijn toegewezen tooyour virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="832af-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>

<span data-ttu-id="832af-125">Als u de vorige zelfstudie hello te gevolgd[maken van een virtuele-machineschaalset](tutorial-create-vmss.md), een load balancer voor u is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="832af-125">If you followed hello previous tutorial too[create a virtual machine scale set](tutorial-create-vmss.md), a load balancer was created for you.</span></span> <span data-ttu-id="832af-126">Al deze onderdelen zijn geconfigureerd voor u als onderdeel van Hallo scale set.</span><span class="sxs-lookup"><span data-stu-id="832af-126">All these components were configured for you as part of hello scale set.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="832af-127">Azure load balancer maken</span><span class="sxs-lookup"><span data-stu-id="832af-127">Create Azure load balancer</span></span>
<span data-ttu-id="832af-128">In deze sectie beschrijft hoe u kunt maken en configureren van elk onderdeel Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="832af-128">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="832af-129">Voordat u de load balancer maken kunt, maakt u een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="832af-129">Before you can create your load balancer, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="832af-130">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupLoadBalancer* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="832af-130">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="832af-131">Een openbaar IP-adres maken</span><span class="sxs-lookup"><span data-stu-id="832af-131">Create a public IP address</span></span>
<span data-ttu-id="832af-132">tooaccess uw app op Hallo Internet, moet u een openbaar IP-adres voor Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="832af-132">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="832af-133">Maken van een openbaar IP-adres met [az netwerk openbare ip-maken](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="832af-133">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="832af-134">Hallo volgende voorbeeld maakt u een openbaar IP-adres met de naam *myPublicIP* in Hallo *myResourceGroupLoadBalancer* resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="832af-134">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="832af-135">Een load balancer maken</span><span class="sxs-lookup"><span data-stu-id="832af-135">Create a load balancer</span></span>
<span data-ttu-id="832af-136">Maken van een load balancer met [az network Load Balancer maken](/cli/azure/network/lb#create).</span><span class="sxs-lookup"><span data-stu-id="832af-136">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="832af-137">Hallo volgende voorbeeld maakt u een load balancer met de naam *myLoadBalancer* en wijst Hallo *myPublicIP* adres toohello front-end-IP-configuratie:</span><span class="sxs-lookup"><span data-stu-id="832af-137">hello following example creates a load balancer named *myLoadBalancer* and assigns hello *myPublicIP* address toohello front-end IP configuration:</span></span>

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="832af-138">Een health test maken</span><span class="sxs-lookup"><span data-stu-id="832af-138">Create a health probe</span></span>
<span data-ttu-id="832af-139">tooallow hello load balancer toomonitor Hallo status van uw app, dat u een health test gebruiken.</span><span class="sxs-lookup"><span data-stu-id="832af-139">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="832af-140">Hallo health test wordt dynamisch toegevoegd of verwijderd van virtuele machines van Hallo load balancer wisselen op basis van hun antwoord toohealth controles.</span><span class="sxs-lookup"><span data-stu-id="832af-140">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="832af-141">Standaard wordt een virtuele machine verwijderd uit Hallo load balancer-distributie na twee opeenvolgende fouten met intervallen van 15 seconden.</span><span class="sxs-lookup"><span data-stu-id="832af-141">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="832af-142">U maakt een health test op basis van een protocol of de pagina voor de controle van een specifieke status voor uw app.</span><span class="sxs-lookup"><span data-stu-id="832af-142">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="832af-143">Hallo volgende voorbeeld wordt een TCP-test.</span><span class="sxs-lookup"><span data-stu-id="832af-143">hello following example creates a TCP probe.</span></span> <span data-ttu-id="832af-144">U kunt ook aangepaste HTTP-tests voor meer fijnmazige statuscontroles maken.</span><span class="sxs-lookup"><span data-stu-id="832af-144">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="832af-145">Wanneer u een aangepaste HTTP-test, moet u Hallo selectievakje statuspagina, zoals *healthcheck.js*.</span><span class="sxs-lookup"><span data-stu-id="832af-145">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.js*.</span></span> <span data-ttu-id="832af-146">Hallo test moet retourneren een **HTTP 200 OK** antwoord voor Hallo load balancer tookeep Hallo host in de draaihoek.</span><span class="sxs-lookup"><span data-stu-id="832af-146">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="832af-147">toocreate een TCP health test, die u gebruikt [az network Load Balancer-test maken](/cli/azure/network/lb/probe#create).</span><span class="sxs-lookup"><span data-stu-id="832af-147">toocreate a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="832af-148">Hallo volgende voorbeeld wordt een health test met de naam *myHealthProbe*:</span><span class="sxs-lookup"><span data-stu-id="832af-148">hello following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="832af-149">Een load balancer-regel maken</span><span class="sxs-lookup"><span data-stu-id="832af-149">Create a load balancer rule</span></span>
<span data-ttu-id="832af-150">Een load balancer-regel is gebruikte toodefine hoe verkeer wordt gedistribueerde toohello virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="832af-150">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="832af-151">U definieert Hallo front-end-IP-configuratie voor Hallo binnenkomende verkeer en Hallo backend-IP-adresgroep tooreceive Hallo, samen met de vereiste bron Hallo en doelpoort.</span><span class="sxs-lookup"><span data-stu-id="832af-151">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="832af-152">toomake zorgen dat alleen orde virtuele machines verkeer ontvangt, u Hallo health test toouse ook definiëren.</span><span class="sxs-lookup"><span data-stu-id="832af-152">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="832af-153">Maken van een regel voor load balancer met [az network Load Balancer-regel maken](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="832af-153">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="832af-154">Hallo volgende voorbeeld maakt u een regel met naam *myLoadBalancerRule*, gebruikt Hallo *myHealthProbe* health test en saldo's verkeer op poort *80*:</span><span class="sxs-lookup"><span data-stu-id="832af-154">hello following example creates a rule named *myLoadBalancerRule*, uses hello *myHealthProbe* health probe, and balances traffic on port *80*:</span></span>

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a><span data-ttu-id="832af-155">Virtueel netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="832af-155">Configure virtual network</span></span>
<span data-ttu-id="832af-156">Voordat u een aantal virtuele machines implementeren en uw balancer kunt testen, maak Hallo ondersteunende resources van een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="832af-156">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="832af-157">Zie voor meer informatie over virtuele netwerken Hallo [Azure Virtual Networks beheren](tutorial-virtual-network.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="832af-157">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="832af-158">Maken van netwerkbronnen</span><span class="sxs-lookup"><span data-stu-id="832af-158">Create network resources</span></span>
<span data-ttu-id="832af-159">Maak een virtueel netwerk met [az network vnet maken](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="832af-159">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="832af-160">Hallo volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* met een subnet met de naam *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="832af-160">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

<span data-ttu-id="832af-161">een netwerkbeveiligingsgroep tooadd, die u gebruikt [az netwerk nsg maken](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="832af-161">tooadd a network security group, you use [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="832af-162">Hallo volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="832af-162">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="832af-163">Maken van een groep van de netwerkbeveiligingsregel met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="832af-163">Create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="832af-164">Hallo volgende voorbeeld wordt een groep netwerkbeveiligingsregel met de naam *myNetworkSecurityGroupRule*:</span><span class="sxs-lookup"><span data-stu-id="832af-164">hello following example creates a network security group rule named *myNetworkSecurityGroupRule*:</span></span>

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

<span data-ttu-id="832af-165">Virtuele NIC's zijn gemaakt met [az netwerk nic maken](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="832af-165">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="832af-166">Hallo maakt volgende voorbeeld drie virtuele NIC's.</span><span class="sxs-lookup"><span data-stu-id="832af-166">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="832af-167">(Een virtuele NIC voor elke VM die u maakt voor uw app in hello te volgen stappen.)</span><span class="sxs-lookup"><span data-stu-id="832af-167">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="832af-168">U kunt extra virtuele NIC's en virtuele machines maken op elk gewenst moment en ze toohello load balancer toevoegen:</span><span class="sxs-lookup"><span data-stu-id="832af-168">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a><span data-ttu-id="832af-169">Virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="832af-169">Create virtual machines</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="832af-170">Cloud-init-configuratie maken</span><span class="sxs-lookup"><span data-stu-id="832af-170">Create cloud-init config</span></span>
<span data-ttu-id="832af-171">In een vorige zelfstudie over [hoe een virtuele Linux-machine op de eerste keer opstarten toocustomize](tutorial-automate-vm-deployment.md), u leert hoe tooautomate VM aanpassing met cloud-init.</span><span class="sxs-lookup"><span data-stu-id="832af-171">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="832af-172">U kunt dezelfde cloud init configuration file tooinstall NGINX Hallo en uitvoeren van een eenvoudige 'Hallo wereld' Node.js-app.</span><span class="sxs-lookup"><span data-stu-id="832af-172">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="832af-173">Maak een bestand met de naam in uw huidige shell *cloud init.txt* en plakken Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="832af-173">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="832af-174">Bijvoorbeeld, Hallo-bestand in Hallo Cloud-Shell op uw lokale machine niet maken.</span><span class="sxs-lookup"><span data-stu-id="832af-174">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="832af-175">Voer `sensible-editor cloud-init.txt` toocreate Hallo bestand en een overzicht van beschikbare editors.</span><span class="sxs-lookup"><span data-stu-id="832af-175">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="832af-176">Zorg ervoor dat Hallo hele cloud-init-bestand correct is gekopieerd, met name Hallo eerste regel:</span><span class="sxs-lookup"><span data-stu-id="832af-176">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-virtual-machines"></a><span data-ttu-id="832af-177">Virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="832af-177">Create virtual machines</span></span>
<span data-ttu-id="832af-178">tooimprove hello hoge beschikbaarheid van uw app, uw virtuele machines in een beschikbaarheidsset plaatst.</span><span class="sxs-lookup"><span data-stu-id="832af-178">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span> <span data-ttu-id="832af-179">Zie voor meer informatie over beschikbaarheidssets Hallo vorige [hoe toocreate maximaal beschikbare virtuele machines](tutorial-availability-sets.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="832af-179">For more information about availability sets, see hello previous [How toocreate highly available virtual machines](tutorial-availability-sets.md) tutorial.</span></span>

<span data-ttu-id="832af-180">Maken van een beschikbaarheidsset met [az vm beschikbaarheidsset maken](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="832af-180">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="832af-181">Hallo volgende voorbeeld maakt u een beschikbaarheidsset benoemde *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="832af-181">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

<span data-ttu-id="832af-182">Nu kunt u virtuele machines Hallo met [az vm maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="832af-182">Now you can create hello VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="832af-183">Hallo volgende voorbeeld maakt drie virtuele machines en SSH-sleutels worden gegenereerd als deze niet al bestaan:</span><span class="sxs-lookup"><span data-stu-id="832af-183">hello following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

<span data-ttu-id="832af-184">Er zijn achtergrondtaken die toorun verder gaat nadat hello Azure CLI keert u terug toohello prompt.</span><span class="sxs-lookup"><span data-stu-id="832af-184">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="832af-185">Hallo `--no-wait` parameter wacht niet voor alle taken toocomplete Hallo.</span><span class="sxs-lookup"><span data-stu-id="832af-185">hello `--no-wait` parameter does not wait for all hello tasks toocomplete.</span></span> <span data-ttu-id="832af-186">Het is mogelijk een andere paar minuten voordat u toegang hebt tot Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="832af-186">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="832af-187">Hallo load balancer health test automatisch gedetecteerd wanneer Hallo-app wordt uitgevoerd op elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="832af-187">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="832af-188">Zodra het Hallo-app wordt uitgevoerd, begint Hallo load balancer-regel toodistribute verkeer.</span><span class="sxs-lookup"><span data-stu-id="832af-188">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>


## <a name="test-load-balancer"></a><span data-ttu-id="832af-189">Test load balancer</span><span class="sxs-lookup"><span data-stu-id="832af-189">Test load balancer</span></span>
<span data-ttu-id="832af-190">Hallo openbare IP-adres van de load balancer met verkrijgen [az netwerk openbare ip-weergeven](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="832af-190">Obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="832af-191">Hallo volgende voorbeeld Hallo IP-adres krijgt voor *myPublicIP* eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="832af-191">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="832af-192">Vervolgens kunt u in de webbrowser tooa Hallo openbaar IP-adres invoeren.</span><span class="sxs-lookup"><span data-stu-id="832af-192">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="832af-193">Houd er rekening mee - duurt een paar minuten Hallo Hallo VMs toobe gereed voordat Hallo load balancer toodistribute verkeer toothem wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="832af-193">Remember - it takes a few minutes hello hello VMs toobe ready before hello load balancer starts toodistribute traffic toothem.</span></span> <span data-ttu-id="832af-194">Hallo-app wordt weergegeven, inclusief Hallo hostnaam Hallo VM die Hallo load balancer gedistribueerde tooas verkeer in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="832af-194">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Actieve Node.js-app](./media/tutorial-load-balancer/running-nodejs-app.png)

<span data-ttu-id="832af-196">toosee hello load balancer verkeer verdelen over alle drie virtuele machines waarop uw app wordt uitgevoerd, u kunt force vernieuwen van uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="832af-196">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="832af-197">Toevoegen en verwijderen van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="832af-197">Add and remove VMs</span></span>
<span data-ttu-id="832af-198">Mogelijk moet u tooperform onderhoud op Hallo van virtuele machines waarop uw app, zoals het installeren van updates voor het besturingssysteem wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="832af-198">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="832af-199">toodeal met tooyour-app voor verkeer, moet u mogelijk tooadd extra virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="832af-199">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="832af-200">Deze sectie leest u hoe tooremove of een virtuele machine van Hallo load balancer toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="832af-200">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="832af-201">Een virtuele machine van Hallo load balancer verwijderen</span><span class="sxs-lookup"><span data-stu-id="832af-201">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="832af-202">U kunt een virtuele machine verwijderen uit Hallo back-end-adresgroep met [az nic ip-config-netwerkadresgroep verwijderen](/cli/azure/network/nic/ip-config/address-pool#remove).</span><span class="sxs-lookup"><span data-stu-id="832af-202">You can remove a VM from hello backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="832af-203">Hallo volgende voorbeeld verwijdert Hallo virtuele NIC voor **myVM2** van *myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="832af-203">hello following example removes hello virtual NIC for **myVM2** from *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="832af-204">toosee hello load balancer verkeer verdelen over Hallo overige twee virtuele machines met uw app u kunt force vernieuwen van uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="832af-204">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="832af-205">U kunt nu onderhoud uitvoeren op Hallo VM, zoals het installeren van updates voor het besturingssysteem of het uitvoeren van een VM opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="832af-205">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="832af-206">Een VM toohello load balancer toevoegen</span><span class="sxs-lookup"><span data-stu-id="832af-206">Add a VM toohello load balancer</span></span>
<span data-ttu-id="832af-207">Na het uitvoeren van onderhoud van de virtuele machine, of als u tooexpand capaciteit nodig hebt, kunt u toevoegen met een VM toohello back-end-adresgroep met [az nic ip-config-netwerkadresgroep toevoegen](/cli/azure/network/nic/ip-config/address-pool#add).</span><span class="sxs-lookup"><span data-stu-id="832af-207">After performing VM maintenance, or if you need tooexpand capacity, you can add a VM toohello backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="832af-208">Hallo volgende voorbeeld wordt toegevoegd Hallo virtuele NIC voor **myVM2** te*myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="832af-208">hello following example adds hello virtual NIC for **myVM2** too*myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="832af-209">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="832af-209">Next steps</span></span>
<span data-ttu-id="832af-210">In deze zelfstudie hebt gemaakt van een load balancer en virtuele machines tooit gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="832af-210">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="832af-211">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="832af-211">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="832af-212">Een Azure load balancer maken</span><span class="sxs-lookup"><span data-stu-id="832af-212">Create an Azure load balancer</span></span>
> * <span data-ttu-id="832af-213">Een load balancer health test maken</span><span class="sxs-lookup"><span data-stu-id="832af-213">Create a load balancer health probe</span></span>
> * <span data-ttu-id="832af-214">Regels voor netwerkverkeer voor de load balancer maken</span><span class="sxs-lookup"><span data-stu-id="832af-214">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="832af-215">Cloud-init toocreate een eenvoudige Node.js-app gebruiken</span><span class="sxs-lookup"><span data-stu-id="832af-215">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="832af-216">Virtuele machines maken en koppelen tooa load balancer</span><span class="sxs-lookup"><span data-stu-id="832af-216">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="832af-217">Een load balancer in actie weergeven</span><span class="sxs-lookup"><span data-stu-id="832af-217">View a load balancer in action</span></span>
> * <span data-ttu-id="832af-218">Toevoegen of virtuele machines van een load balancer verwijderen</span><span class="sxs-lookup"><span data-stu-id="832af-218">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="832af-219">De volgende zelfstudie toolearn toohello voor vooraf meer informatie over de onderdelen van de virtuele Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="832af-219">Advance toohello next tutorial toolearn more about Azure virtual network components.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="832af-220">Virtuele machines en virtuele netwerken beheren</span><span class="sxs-lookup"><span data-stu-id="832af-220">Manage VMs and virtual networks</span></span>](tutorial-virtual-network.md)
