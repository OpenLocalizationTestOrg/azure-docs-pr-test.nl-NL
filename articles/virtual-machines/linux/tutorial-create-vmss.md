---
title: een virtuele Machine-Schaalsets Linux in Azure aaaCreate | Microsoft Docs
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
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="4a863-103">Een virtuele-Machineschaalset maken en implementeren van een maximaal beschikbare app op Linux</span><span class="sxs-lookup"><span data-stu-id="4a863-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="4a863-104">Een virtuele-machineschaalset kunt u toodeploy en beheren van een reeks identiek zijn, automatisch schalen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="4a863-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="4a863-105">U kunt Hallo aantal virtuele machines in de schaalset Hallo handmatig schalen of regels tooautoscale op basis van CPU-gebruik, geheugen-aanvraag of netwerkverkeer definiëren.</span><span class="sxs-lookup"><span data-stu-id="4a863-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="4a863-106">In deze zelfstudie maakt implementeren u een virtuele-machineschaalset instellen in Azure.</span><span class="sxs-lookup"><span data-stu-id="4a863-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="4a863-107">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="4a863-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4a863-108">Cloud-init toocreate een tooscale app gebruiken</span><span class="sxs-lookup"><span data-stu-id="4a863-108">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="4a863-109">Maken van een virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="4a863-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="4a863-110">Vergroten of verkleinen Hallo aantal exemplaren in een schaalset</span><span class="sxs-lookup"><span data-stu-id="4a863-110">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="4a863-111">Verbindingsgegevens voor scale set exemplaren weergeven</span><span class="sxs-lookup"><span data-stu-id="4a863-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="4a863-112">Gegevensschijven in een schaalset gebruiken</span><span class="sxs-lookup"><span data-stu-id="4a863-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4a863-113">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="4a863-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="4a863-114">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="4a863-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4a863-115">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4a863-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="4a863-116">Overzicht van Scale Set</span><span class="sxs-lookup"><span data-stu-id="4a863-116">Scale Set overview</span></span>
<span data-ttu-id="4a863-117">Een virtuele-machineschaalset kunt u toodeploy en beheren van een reeks identiek zijn, automatisch schalen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="4a863-117">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="4a863-118">Schaal wordt ingesteld gebruik Hallo dezelfde onderdelen die u kennisgemaakt in de vorige zelfstudie hello te[maximaal beschikbare virtuele machines maken](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="4a863-118">Scale sets use hello same components as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="4a863-119">Virtuele machines in een schaalset worden gemaakt in een beschikbaarheidsset ingesteld en verdeeld over logica probleem- en domeinen.</span><span class="sxs-lookup"><span data-stu-id="4a863-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="4a863-120">Virtuele machines worden gemaakt als nodig in een schaalset.</span><span class="sxs-lookup"><span data-stu-id="4a863-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="4a863-121">U automatisch schalen regels toocontrol definiëren hoe en wanneer virtuele machines worden toegevoegd of verwijderd uit het Hallo-schaalset.</span><span class="sxs-lookup"><span data-stu-id="4a863-121">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="4a863-122">Deze regels kunnen activeren op basis van metrische gegevens zoals CPU-belasting, geheugengebruik of netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="4a863-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="4a863-123">Schaal wordt ingesteld voor ondersteuning van too1, 000 VM's wanneer u een installatiekopie van een Azure-platform.</span><span class="sxs-lookup"><span data-stu-id="4a863-123">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="4a863-124">Voor productieworkloads, kunt u desgewenst te[maken van een aangepaste VM-installatiekopie](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="4a863-124">For production workloads, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="4a863-125">U kunt maken van too100 virtuele machines in een schaal instelt met behulp van een aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="4a863-125">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="4a863-126">Maken van een app-tooscale</span><span class="sxs-lookup"><span data-stu-id="4a863-126">Create an app tooscale</span></span>
<span data-ttu-id="4a863-127">Voor gebruik in productieomgevingen, kunt u desgewenst te[maken van een aangepaste VM-installatiekopie](tutorial-custom-images.md) waarin uw toepassing geïnstalleerd en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="4a863-127">For production use, you may wish too[Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="4a863-128">Voor deze zelfstudie kunt aanpassen Hallo die VM 's op de eerste opstarten tooquickly een schaal instelt in actie zien.</span><span class="sxs-lookup"><span data-stu-id="4a863-128">For this tutorial, lets customize hello VMs on first boot tooquickly see a scale set in action.</span></span>

<span data-ttu-id="4a863-129">In een vorige zelfstudie hebt u geleerd [hoe toocustomize virtuele Linux-machine op de eerste keer opstarten](tutorial-automate-vm-deployment.md) met cloud-init.</span><span class="sxs-lookup"><span data-stu-id="4a863-129">In a previous tutorial, you learned [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="4a863-130">U kunt dezelfde cloud init configuration file tooinstall NGINX Hallo en uitvoeren van een eenvoudige 'Hallo wereld' Node.js-app.</span><span class="sxs-lookup"><span data-stu-id="4a863-130">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="4a863-131">Maak een bestand met de naam in uw huidige shell *cloud init.txt* en plakken Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="4a863-131">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="4a863-132">Bijvoorbeeld, Hallo-bestand in Hallo Cloud-Shell op uw lokale machine niet maken.</span><span class="sxs-lookup"><span data-stu-id="4a863-132">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="4a863-133">Voer `sensible-editor cloud-init.txt` toocreate Hallo bestand en een overzicht van beschikbare editors.</span><span class="sxs-lookup"><span data-stu-id="4a863-133">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="4a863-134">Zorg ervoor dat Hallo hele cloud-init-bestand correct is gekopieerd, met name Hallo eerste regel:</span><span class="sxs-lookup"><span data-stu-id="4a863-134">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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


## <a name="create-a-scale-set"></a><span data-ttu-id="4a863-135">Maken van een schaalset</span><span class="sxs-lookup"><span data-stu-id="4a863-135">Create a scale set</span></span>
<span data-ttu-id="4a863-136">Voordat u een schaalset maken kunt, maakt u een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4a863-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="4a863-137">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupScaleSet* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="4a863-137">hello following example creates a resource group named *myResourceGroupScaleSet* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="4a863-138">Maak nu de schaal van een virtuele machine in te stellen [az vmss maken](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="4a863-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="4a863-139">Hallo volgende voorbeeld wordt een set met de naam scale *myScaleSet*Hallo cloud init bestand toocustomize Hallo VM gebruikt en SSH-sleutels worden gegenereerd als deze nog niet bestaan:</span><span class="sxs-lookup"><span data-stu-id="4a863-139">hello following example creates a scale set named *myScaleSet*, uses hello cloud-init file toocustomize hello VM, and generates SSH keys if they do not exist:</span></span>

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

<span data-ttu-id="4a863-140">Het duurt enkele minuten toocreate en configureer alle Hallo scale set resources en virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="4a863-140">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span> <span data-ttu-id="4a863-141">Er zijn achtergrondtaken die toorun verder gaat nadat hello Azure CLI keert u terug toohello prompt.</span><span class="sxs-lookup"><span data-stu-id="4a863-141">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="4a863-142">Het is mogelijk een andere paar minuten voordat u toegang hebt tot Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="4a863-142">It may be another couple of minutes before you can access hello app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="4a863-143">Webverkeer toestaan</span><span class="sxs-lookup"><span data-stu-id="4a863-143">Allow web traffic</span></span>
<span data-ttu-id="4a863-144">Een load balancer is automatisch als onderdeel van Hallo virtuele-machineschaalset gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4a863-144">A load balancer was created automatically as part of hello virtual machine scale set.</span></span> <span data-ttu-id="4a863-145">Hallo load balancer wordt verkeer over een reeks gedefinieerde virtuele machines met regels voor load balancer.</span><span class="sxs-lookup"><span data-stu-id="4a863-145">hello load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="4a863-146">U kunt meer informatie over de load balancer concepten en configuratie in de volgende zelfstudie Hallo, [hoe tooload balans vinden tussen virtuele machines in Azure](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="4a863-146">You can learn more about load balancer concepts and configuration in hello next tutorial, [How tooload balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="4a863-147">tooallow verkeer tooreach Hallo web-app, maakt u een regel met [az network Load Balancer-regel maken](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="4a863-147">tooallow traffic tooreach hello web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="4a863-148">Hallo volgende voorbeeld maakt u een regel met naam *myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="4a863-148">hello following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

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

## <a name="test-your-app"></a><span data-ttu-id="4a863-149">Uw app testen</span><span class="sxs-lookup"><span data-stu-id="4a863-149">Test your app</span></span>
<span data-ttu-id="4a863-150">toosee uw Node.js-app op Hallo web verkrijgen Hallo openbare IP-adres van de load balancer met [az netwerk openbare ip-weergeven](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="4a863-150">toosee your Node.js app on hello web, obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="4a863-151">Hallo volgende voorbeeld Hallo IP-adres krijgt voor *myScaleSetLBPublicIP* gemaakt als onderdeel van het Hallo-schaalset:</span><span class="sxs-lookup"><span data-stu-id="4a863-151">hello following example obtains hello IP address for *myScaleSetLBPublicIP* created as part of hello scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="4a863-152">Voer Hallo openbaar IP-adres in de webbrowser tooa.</span><span class="sxs-lookup"><span data-stu-id="4a863-152">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="4a863-153">Hallo-app wordt weergegeven, inclusief Hallo hostnaam Hallo VM die Hallo load balancer gedistribueerde verkeer naar:</span><span class="sxs-lookup"><span data-stu-id="4a863-153">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Actieve Node.js-app](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="4a863-155">toosee hello schaal instellen in actie, u kunt force vernieuwen uw web browser toosee Hallo load balancer verkeer verdelen over alle Hallo virtuele machines waarop uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4a863-155">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="4a863-156">Beheertaken</span><span class="sxs-lookup"><span data-stu-id="4a863-156">Management tasks</span></span>
<span data-ttu-id="4a863-157">Gedurende de levenscyclus van de Hallo van Hallo scale is ingesteld, moet u mogelijk toorun een of meer beheertaken.</span><span class="sxs-lookup"><span data-stu-id="4a863-157">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="4a863-158">U kunt bovendien toocreate scripts die verschillende lifecycle-taken automatiseren.</span><span class="sxs-lookup"><span data-stu-id="4a863-158">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="4a863-159">Hello Azure CLI 2.0 biedt een snelle manier toodo deze taken.</span><span class="sxs-lookup"><span data-stu-id="4a863-159">hello Azure CLI 2.0 provides a quick way toodo those tasks.</span></span> <span data-ttu-id="4a863-160">Hier volgen enkele algemene taken.</span><span class="sxs-lookup"><span data-stu-id="4a863-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="4a863-161">Weergave virtuele machines in een schaalset</span><span class="sxs-lookup"><span data-stu-id="4a863-161">View VMs in a scale set</span></span>
<span data-ttu-id="4a863-162">tooview een lijst met virtuele machines die worden uitgevoerd in uw scale ingesteld, gebruikt u [az vmss lijstexemplaren](/cli/azure/vmss#list-instances) als volgt:</span><span class="sxs-lookup"><span data-stu-id="4a863-162">tooview a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="4a863-163">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4a863-163">hello output is similar toohello following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="4a863-164">Vergroten of verkleinen van VM-exemplaren</span><span class="sxs-lookup"><span data-stu-id="4a863-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="4a863-165">toosee hello aantal exemplaren van u momenteel hebt in een schaal ingesteld, gebruikt u [az vmss weergeven](/cli/azure/vmss#show) en query's uitvoeren op *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="4a863-165">toosee hello number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="4a863-166">U kunt vervolgens handmatig vergroten of verkleinen Hallo aantal virtuele machines in Hallo schaal in te stellen [az vmss scale](/cli/azure/vmss#scale).</span><span class="sxs-lookup"><span data-stu-id="4a863-166">You can then manually increase or decrease hello number of virtual machines in hello scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="4a863-167">Hallo volgende voorbeeld wordt Hallo aantal virtuele machines in te stellen schaal*5*:</span><span class="sxs-lookup"><span data-stu-id="4a863-167">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="4a863-168">Regels voor automatisch schalen kunt u definiëren hoe tooscale omhoog of omlaag Hallo aantal VM's in uw scale ingesteld in antwoord toodemand zoals netwerkverkeer of CPU-gebruik.</span><span class="sxs-lookup"><span data-stu-id="4a863-168">Autoscale rules let you define how tooscale up or down hello number of VMs in your scale set in response toodemand such as network traffic or CPU usage.</span></span> <span data-ttu-id="4a863-169">Deze regels kunnen op dit moment kunnen niet worden ingesteld in de Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="4a863-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="4a863-170">Gebruik Hallo [Azure-portal](https://portal.azure.com) tooconfigure automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="4a863-170">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="4a863-171">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="4a863-171">Get connection info</span></span>
<span data-ttu-id="4a863-172">verbindingsgegevens tooobtain over VM's in uw schaalsets hello, gebruik [az vmss lijst--verbinding-Instantiegegevens](/cli/azure/vmss#list-instance-connection-info).</span><span class="sxs-lookup"><span data-stu-id="4a863-172">tooobtain connection information about hello VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="4a863-173">Met deze opdracht levert Hallo openbaar IP-adres en poort voor elke virtuele machine waarmee u tooconnect met SSH:</span><span class="sxs-lookup"><span data-stu-id="4a863-173">This command outputs hello public IP address and port for each VM that allows you tooconnect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="4a863-174">Gegevensschijven met schaalsets gebruiken</span><span class="sxs-lookup"><span data-stu-id="4a863-174">Use data disks with scale sets</span></span>
<span data-ttu-id="4a863-175">U kunt maken en gebruiken van gegevensschijven met-schaalsets.</span><span class="sxs-lookup"><span data-stu-id="4a863-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="4a863-176">In een vorige zelfstudie hebt u geleerd hoe te[Azure beheren schijven](tutorial-manage-disks.md) dat overzichten Hallo best practices en verbeterde prestaties voor het bouwen van apps op gegevensschijven in plaats van Hallo OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="4a863-176">In a previous tutorial, you learned how too[Manage Azure disks](tutorial-manage-disks.md) that outlines hello best practices and performance improvements for building apps on data disks rather than hello OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="4a863-177">Schaalset met gegevensschijven maken</span><span class="sxs-lookup"><span data-stu-id="4a863-177">Create scale set with data disks</span></span>
<span data-ttu-id="4a863-178">toocreate een schaal instellen en gegevensschijven, koppel toevoegen Hallo `--data-disk-sizes-gb` parameter toohello [az vmss maken](/cli/azure/vmss#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4a863-178">toocreate a scale set and attach data disks, add hello `--data-disk-sizes-gb` parameter toohello [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="4a863-179">Hallo volgende voorbeeld wordt een instellen met schaal *50*Gb gegevensschijven gekoppeld tooeach exemplaar:</span><span class="sxs-lookup"><span data-stu-id="4a863-179">hello following example creates a scale set with *50*Gb data disks attached tooeach instance:</span></span>

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

<span data-ttu-id="4a863-180">Wanneer instanties zijn verwijderd uit een schaalset, worden ook eventuele gekoppelde gegevensschijven verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4a863-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="4a863-181">Gegevensschijven toevoegen</span><span class="sxs-lookup"><span data-stu-id="4a863-181">Add data disks</span></span>
<span data-ttu-id="4a863-182">tooadd een tooinstances gegevens schijf in uw scale instellen, gebruikt u [az vmss schijf koppelen](/cli/azure/vmss/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="4a863-182">tooadd a data disk tooinstances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="4a863-183">Hallo volgende voorbeeld wordt een *50*Gb schijf tooeach exemplaar:</span><span class="sxs-lookup"><span data-stu-id="4a863-183">hello following example adds a *50*Gb disk tooeach instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="4a863-184">Loskoppelen van gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="4a863-184">Detach data disks</span></span>
<span data-ttu-id="4a863-185">tooremove een tooinstances gegevens schijf in uw scale instellen, gebruikt u [az vmss schijf loskoppelen](/cli/azure/vmss/disk#detach).</span><span class="sxs-lookup"><span data-stu-id="4a863-185">tooremove a data disk tooinstances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="4a863-186">Hallo volgende voorbeeld wordt verwijderd Hallo gegevensschijf met LUN *2* van elk exemplaar:</span><span class="sxs-lookup"><span data-stu-id="4a863-186">hello following example removes hello data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="4a863-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4a863-187">Next steps</span></span>
<span data-ttu-id="4a863-188">In deze zelfstudie maakt u een virtuele-machineschaalset gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4a863-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="4a863-189">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="4a863-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4a863-190">Cloud-init toocreate een tooscale app gebruiken</span><span class="sxs-lookup"><span data-stu-id="4a863-190">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="4a863-191">Maken van een virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="4a863-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="4a863-192">Vergroten of verkleinen Hallo aantal exemplaren in een schaalset</span><span class="sxs-lookup"><span data-stu-id="4a863-192">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="4a863-193">Verbindingsgegevens voor scale set exemplaren weergeven</span><span class="sxs-lookup"><span data-stu-id="4a863-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="4a863-194">Gegevensschijven in een schaalset gebruiken</span><span class="sxs-lookup"><span data-stu-id="4a863-194">Use data disks in a scale set</span></span>

<span data-ttu-id="4a863-195">De volgende zelfstudie toolearn toohello voor vooraf informatie over taakverdeling concepten voor virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="4a863-195">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4a863-196">Load balance virtuele machines</span><span class="sxs-lookup"><span data-stu-id="4a863-196">Load balance virtual machines</span></span>](tutorial-load-balancer.md)