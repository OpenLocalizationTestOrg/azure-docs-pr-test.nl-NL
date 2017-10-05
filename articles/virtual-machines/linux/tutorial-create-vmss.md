---
title: Maken van een virtuele-Machineschaalsets voor Linux in Azure | Microsoft Docs
description: Maken en implementeren van een maximaal beschikbare toepassing op virtuele Linux-machines met behulp van een virtuele-machineschaalset
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 2b8d519e11f70eda164bd8f6e131a3989f242ab0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="04a86-103">Een virtuele-Machineschaalset maken en implementeren van een maximaal beschikbare app op Linux</span><span class="sxs-lookup"><span data-stu-id="04a86-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="04a86-104">Een virtuele-machineschaalset kunt u om te implementeren en beheren van een reeks identiek zijn, automatisch schalen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="04a86-104">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="04a86-105">U kunt het aantal virtuele machines in de schaalset handmatig schalen of regels automatisch te schalen op basis van CPU-gebruik, geheugen-aanvraag of netwerkverkeer definiëren.</span><span class="sxs-lookup"><span data-stu-id="04a86-105">You can scale the number of VMs in the scale set manually, or define rules to autoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="04a86-106">In deze zelfstudie maakt implementeren u een virtuele-machineschaalset instellen in Azure.</span><span class="sxs-lookup"><span data-stu-id="04a86-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="04a86-107">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="04a86-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="04a86-108">Cloud-init gebruiken voor het maken van een app schalen</span><span class="sxs-lookup"><span data-stu-id="04a86-108">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="04a86-109">Maken van een virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="04a86-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="04a86-110">Vergroten of verkleinen het aantal exemplaren in een schaalset</span><span class="sxs-lookup"><span data-stu-id="04a86-110">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="04a86-111">Verbindingsgegevens voor scale set exemplaren weergeven</span><span class="sxs-lookup"><span data-stu-id="04a86-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="04a86-112">Gegevensschijven in een schaalset gebruiken</span><span class="sxs-lookup"><span data-stu-id="04a86-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="04a86-113">Als u wilt installeren en gebruiken van de CLI lokaal, in deze zelfstudie vereist dat u de Azure CLI versie 2.0.4 zijn uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="04a86-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="04a86-114">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="04a86-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="04a86-115">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="04a86-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="04a86-116">Overzicht van Scale Set</span><span class="sxs-lookup"><span data-stu-id="04a86-116">Scale Set overview</span></span>
<span data-ttu-id="04a86-117">Een virtuele-machineschaalset kunt u om te implementeren en beheren van een reeks identiek zijn, automatisch schalen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="04a86-117">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="04a86-118">Schaalsets dezelfde onderdelen gebruiken zoals u hebt geleerd over in de vorige zelfstudie naar [maximaal beschikbare virtuele machines maken](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="04a86-118">Scale sets use the same components as you learned about in the previous tutorial to [Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="04a86-119">Virtuele machines in een schaalset worden gemaakt in een beschikbaarheidsset ingesteld en verdeeld over logica probleem- en domeinen.</span><span class="sxs-lookup"><span data-stu-id="04a86-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="04a86-120">Virtuele machines worden gemaakt als nodig in een schaalset.</span><span class="sxs-lookup"><span data-stu-id="04a86-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="04a86-121">Definieert u de regels voor automatisch schalen om te bepalen hoe en wanneer virtuele machines worden toegevoegd of verwijderd uit de schaalaanpassingsset.</span><span class="sxs-lookup"><span data-stu-id="04a86-121">You define autoscale rules to control how and when VMs are added or removed from the scale set.</span></span> <span data-ttu-id="04a86-122">Deze regels kunnen activeren op basis van metrische gegevens zoals CPU-belasting, geheugengebruik of netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="04a86-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="04a86-123">Schaal wordt ondersteuning voor maximaal 1000 VMs ingesteld wanneer u een installatiekopie van een Azure-platform.</span><span class="sxs-lookup"><span data-stu-id="04a86-123">Scale sets support up to 1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="04a86-124">Voor productieworkloads, u kunt desgewenst [maken van een aangepaste VM-installatiekopie](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="04a86-124">For production workloads, you may wish to [Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="04a86-125">U kunt maximaal 100 virtuele machines in een schaal instelt met behulp van een aangepaste installatiekopie maken.</span><span class="sxs-lookup"><span data-stu-id="04a86-125">You can create up to 100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-to-scale"></a><span data-ttu-id="04a86-126">Maak een app schalen</span><span class="sxs-lookup"><span data-stu-id="04a86-126">Create an app to scale</span></span>
<span data-ttu-id="04a86-127">Voor gebruik in productieomgevingen, u kunt desgewenst [maken van een aangepaste VM-installatiekopie](tutorial-custom-images.md) waarin uw toepassing geïnstalleerd en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="04a86-127">For production use, you may wish to [Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="04a86-128">Voor deze zelfstudie kunt aanpassen van de virtuele machines op de eerste keer wordt opgestart om snel een schaal instelt in actie zien.</span><span class="sxs-lookup"><span data-stu-id="04a86-128">For this tutorial, lets customize the VMs on first boot to quickly see a scale set in action.</span></span>

<span data-ttu-id="04a86-129">In een vorige zelfstudie hebt u geleerd [het aanpassen van een virtuele Linux-machine op de eerste keer opstarten](tutorial-automate-vm-deployment.md) met cloud-init.</span><span class="sxs-lookup"><span data-stu-id="04a86-129">In a previous tutorial, you learned [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="04a86-130">U kunt het bestand met dezelfde configuratie cloud init NGINX installeren en uitvoeren van een eenvoudige 'Hallo wereld' Node.js-app.</span><span class="sxs-lookup"><span data-stu-id="04a86-130">You can use the same cloud-init configuration file to install NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="04a86-131">Maak een bestand met de naam in uw huidige shell *cloud init.txt* en plak de volgende configuratie.</span><span class="sxs-lookup"><span data-stu-id="04a86-131">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="04a86-132">Maak bijvoorbeeld het bestand in de Cloud-Shell niet op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="04a86-132">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="04a86-133">Voer `sensible-editor cloud-init.txt` voor het maken van het bestand en een overzicht van beschikbare editors.</span><span class="sxs-lookup"><span data-stu-id="04a86-133">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="04a86-134">Controleer of het hele cloud-init-bestand correct is gekopieerd met name de eerste regel:</span><span class="sxs-lookup"><span data-stu-id="04a86-134">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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


## <a name="create-a-scale-set"></a><span data-ttu-id="04a86-135">Maken van een schaalset</span><span class="sxs-lookup"><span data-stu-id="04a86-135">Create a scale set</span></span>
<span data-ttu-id="04a86-136">Voordat u een schaalset maken kunt, maakt u een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="04a86-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="04a86-137">Het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroupScaleSet* in de *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="04a86-137">The following example creates a resource group named *myResourceGroupScaleSet* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="04a86-138">Maak nu de schaal van een virtuele machine in te stellen [az vmss maken](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="04a86-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="04a86-139">Het volgende voorbeeld wordt een set met de naam scale *myScaleSet*, gebruikt u het cloud-init-bestand voor het aanpassen van de virtuele machine en SSH-sleutels worden gegenereerd als deze nog niet bestaan:</span><span class="sxs-lookup"><span data-stu-id="04a86-139">The following example creates a scale set named *myScaleSet*, uses the cloud-init file to customize the VM, and generates SSH keys if they do not exist:</span></span>

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

<span data-ttu-id="04a86-140">Het duurt enkele minuten voor het maken en configureren van de schaal set resources en virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="04a86-140">It takes a few minutes to create and configure all the scale set resources and VMs.</span></span> <span data-ttu-id="04a86-141">Er zijn achtergrondtaken die uitvoeren blijven nadat de Azure CLI keert u terug naar de prompt.</span><span class="sxs-lookup"><span data-stu-id="04a86-141">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="04a86-142">Het is mogelijk een andere paar minuten voordat u toegang hebt tot de app.</span><span class="sxs-lookup"><span data-stu-id="04a86-142">It may be another couple of minutes before you can access the app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="04a86-143">Webverkeer toestaan</span><span class="sxs-lookup"><span data-stu-id="04a86-143">Allow web traffic</span></span>
<span data-ttu-id="04a86-144">Een load balancer is automatisch als onderdeel van de virtuele-machineschaalset gemaakt.</span><span class="sxs-lookup"><span data-stu-id="04a86-144">A load balancer was created automatically as part of the virtual machine scale set.</span></span> <span data-ttu-id="04a86-145">De load balancer wordt verkeer over een reeks gedefinieerde virtuele machines met regels voor load balancer.</span><span class="sxs-lookup"><span data-stu-id="04a86-145">The load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="04a86-146">U kunt meer informatie over de load balancer concepten en configuratie in de volgende zelfstudie [het laden van virtuele machines in Azure](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="04a86-146">You can learn more about load balancer concepts and configuration in the next tutorial, [How to load balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="04a86-147">Om verkeer te staan om te bereiken van de web-app, maakt u een regel met [az network Load Balancer-regel maken](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="04a86-147">To allow traffic to reach the web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="04a86-148">Het volgende voorbeeld wordt een regel met naam *myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="04a86-148">The following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a><span data-ttu-id="04a86-149">Uw app testen</span><span class="sxs-lookup"><span data-stu-id="04a86-149">Test your app</span></span>
<span data-ttu-id="04a86-150">Uw Node.js-app op het web vindt verkrijgen van het openbare IP-adres van de load balancer met [az netwerk openbare ip-weergeven](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="04a86-150">To see your Node.js app on the web, obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="04a86-151">Het volgende voorbeeld verkrijgt het IP-adres voor *myScaleSetLBPublicIP* gemaakt als onderdeel van de schaal is ingesteld:</span><span class="sxs-lookup"><span data-stu-id="04a86-151">The following example obtains the IP address for *myScaleSetLBPublicIP* created as part of the scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="04a86-152">Geef het openbare IP-adres in naar een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="04a86-152">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="04a86-153">De app wordt weergegeven, inclusief de hostnaam van de virtuele machine die de load balancer verkeer naar gedistribueerde:</span><span class="sxs-lookup"><span data-stu-id="04a86-153">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span></span>

![Actieve Node.js-app](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="04a86-155">Overzicht van de schaal instelt in actie, u kunt force vernieuwen uw webbrowser als u wilt zien van de load balancer verkeer verdelen over alle virtuele machines waarop uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="04a86-155">To see the scale set in action, you can force-refresh your web browser to see the load balancer distribute traffic across all the VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="04a86-156">Beheertaken</span><span class="sxs-lookup"><span data-stu-id="04a86-156">Management tasks</span></span>
<span data-ttu-id="04a86-157">Gedurende de levenscyclus van de schaal is ingesteld, moet u wellicht een of meer beheertaken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="04a86-157">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="04a86-158">Bovendien wilt u scripts maken die verschillende lifecycle-taken automatiseren.</span><span class="sxs-lookup"><span data-stu-id="04a86-158">Additionally, you may want to create scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="04a86-159">De Azure CLI 2.0 biedt een snelle manier om deze taken.</span><span class="sxs-lookup"><span data-stu-id="04a86-159">The Azure CLI 2.0 provides a quick way to do those tasks.</span></span> <span data-ttu-id="04a86-160">Hier volgen enkele algemene taken.</span><span class="sxs-lookup"><span data-stu-id="04a86-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="04a86-161">Weergave virtuele machines in een schaalset</span><span class="sxs-lookup"><span data-stu-id="04a86-161">View VMs in a scale set</span></span>
<span data-ttu-id="04a86-162">Een lijst van virtuele machines die worden uitgevoerd in de schaalset wilt weergeven, gebruikt u [az vmss lijstexemplaren](/cli/azure/vmss#list-instances) als volgt:</span><span class="sxs-lookup"><span data-stu-id="04a86-162">To view a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="04a86-163">De uitvoer lijkt op die in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="04a86-163">The output is similar to the following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="04a86-164">Vergroten of verkleinen van VM-exemplaren</span><span class="sxs-lookup"><span data-stu-id="04a86-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="04a86-165">Als het aantal exemplaren dat u momenteel in een schaalset hebt wilt weergeven, gebruikt [az vmss weergeven](/cli/azure/vmss#show) en query's uitvoeren op *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="04a86-165">To see the number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="04a86-166">U kunt vervolgens handmatig vergroten of verkleinen het aantal virtuele machines in de schaal in te stellen [az vmss scale](/cli/azure/vmss#scale).</span><span class="sxs-lookup"><span data-stu-id="04a86-166">You can then manually increase or decrease the number of virtual machines in the scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="04a86-167">Het volgende voorbeeld wordt het aantal VM's in uw ingesteld op schaal *5*:</span><span class="sxs-lookup"><span data-stu-id="04a86-167">The following example sets the number of VMs in your scale set to *5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="04a86-168">Regels voor automatisch schalen kunt u definiëren hoe schaal omhoog of omlaag het aantal VM's in uw scale instellen als reactie op de vraag zoals netwerkverkeer of CPU-gebruik.</span><span class="sxs-lookup"><span data-stu-id="04a86-168">Autoscale rules let you define how to scale up or down the number of VMs in your scale set in response to demand such as network traffic or CPU usage.</span></span> <span data-ttu-id="04a86-169">Deze regels kunnen op dit moment kunnen niet worden ingesteld in de Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="04a86-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="04a86-170">Gebruik de [Azure-portal](https://portal.azure.com) automatisch schalen configureren.</span><span class="sxs-lookup"><span data-stu-id="04a86-170">Use the [Azure portal](https://portal.azure.com) to configure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="04a86-171">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="04a86-171">Get connection info</span></span>
<span data-ttu-id="04a86-172">Gebruik om verbindingsinformatie over de VM's in uw schaalsets [az vmss lijst--verbinding-Instantiegegevens](/cli/azure/vmss#list-instance-connection-info).</span><span class="sxs-lookup"><span data-stu-id="04a86-172">To obtain connection information about the VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="04a86-173">Met deze opdracht levert de openbare IP-adres en poort voor elke virtuele machine waarmee u verbinding maken met SSH:</span><span class="sxs-lookup"><span data-stu-id="04a86-173">This command outputs the public IP address and port for each VM that allows you to connect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="04a86-174">Gegevensschijven met schaalsets gebruiken</span><span class="sxs-lookup"><span data-stu-id="04a86-174">Use data disks with scale sets</span></span>
<span data-ttu-id="04a86-175">U kunt maken en gebruiken van gegevensschijven met-schaalsets.</span><span class="sxs-lookup"><span data-stu-id="04a86-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="04a86-176">In een vorige zelfstudie hebt u geleerd hoe u [Azure beheren schijven](tutorial-manage-disks.md) die licht de aanbevolen procedures en verbeterde prestaties voor het bouwen van apps op gegevensschijven in plaats van de besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="04a86-176">In a previous tutorial, you learned how to [Manage Azure disks](tutorial-manage-disks.md) that outlines the best practices and performance improvements for building apps on data disks rather than the OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="04a86-177">Schaalset met gegevensschijven maken</span><span class="sxs-lookup"><span data-stu-id="04a86-177">Create scale set with data disks</span></span>
<span data-ttu-id="04a86-178">Voor het maken van een schaalset en gegevensschijven koppelen, voeg de `--data-disk-sizes-gb` -parameter voor de [az vmss maken](/cli/azure/vmss#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="04a86-178">To create a scale set and attach data disks, add the `--data-disk-sizes-gb` parameter to the [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="04a86-179">Het volgende voorbeeld wordt een instellen met schaal *50*Gb gegevensschijven gekoppeld aan elk exemplaar:</span><span class="sxs-lookup"><span data-stu-id="04a86-179">The following example creates a scale set with *50*Gb data disks attached to each instance:</span></span>

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

<span data-ttu-id="04a86-180">Wanneer instanties zijn verwijderd uit een schaalset, worden ook eventuele gekoppelde gegevensschijven verwijderd.</span><span class="sxs-lookup"><span data-stu-id="04a86-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="04a86-181">Gegevensschijven toevoegen</span><span class="sxs-lookup"><span data-stu-id="04a86-181">Add data disks</span></span>
<span data-ttu-id="04a86-182">U kunt een gegevensschijf toevoegen aan exemplaren in de schaalset met [az vmss schijf koppelen](/cli/azure/vmss/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="04a86-182">To add a data disk to instances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="04a86-183">Het volgende voorbeeld wordt een *50*Gb schijfruimte op elk exemplaar:</span><span class="sxs-lookup"><span data-stu-id="04a86-183">The following example adds a *50*Gb disk to each instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="04a86-184">Loskoppelen van gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="04a86-184">Detach data disks</span></span>
<span data-ttu-id="04a86-185">U kunt een gegevensschijf aan exemplaren in de schaalset verwijderen [az vmss schijf loskoppelen](/cli/azure/vmss/disk#detach).</span><span class="sxs-lookup"><span data-stu-id="04a86-185">To remove a data disk to instances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="04a86-186">Het volgende voorbeeld verwijdert u de gegevensschijf met LUN *2* van elk exemplaar:</span><span class="sxs-lookup"><span data-stu-id="04a86-186">The following example removes the data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="04a86-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="04a86-187">Next steps</span></span>
<span data-ttu-id="04a86-188">In deze zelfstudie maakt u een virtuele-machineschaalset gemaakt.</span><span class="sxs-lookup"><span data-stu-id="04a86-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="04a86-189">U leert hoe naar:</span><span class="sxs-lookup"><span data-stu-id="04a86-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="04a86-190">Cloud-init gebruiken voor het maken van een app schalen</span><span class="sxs-lookup"><span data-stu-id="04a86-190">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="04a86-191">Maken van een virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="04a86-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="04a86-192">Vergroten of verkleinen het aantal exemplaren in een schaalset</span><span class="sxs-lookup"><span data-stu-id="04a86-192">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="04a86-193">Verbindingsgegevens voor scale set exemplaren weergeven</span><span class="sxs-lookup"><span data-stu-id="04a86-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="04a86-194">Gegevensschijven in een schaalset gebruiken</span><span class="sxs-lookup"><span data-stu-id="04a86-194">Use data disks in a scale set</span></span>

<span data-ttu-id="04a86-195">Ga naar de volgende zelfstudie voor meer informatie over taakverdeling concepten voor virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="04a86-195">Advance to the next tutorial to learn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="04a86-196">Load balance virtuele machines</span><span class="sxs-lookup"><span data-stu-id="04a86-196">Load balance virtual machines</span></span>](tutorial-load-balancer.md)