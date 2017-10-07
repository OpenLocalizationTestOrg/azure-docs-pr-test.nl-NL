---
title: aaaConvert een virtuele machine van Azure tooa schaalset | Microsoft Docs
description: Maken en implementeren van een Linux Azure virtuele-machineschaalset hello Azure CLI in te stellen.
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a><span data-ttu-id="8bbeb-103">Een bestaande virtuele machine van Azure tooa scale set converteren</span><span class="sxs-lookup"><span data-stu-id="8bbeb-103">Convert an existing Azure virtual machine tooa scale set</span></span>

<span data-ttu-id="8bbeb-104">Deze zelfstudie laat zien hoe Azure CLI 2.0 toouse tooconvert een virtuele machine tooa virtuele-machineschaalset.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-104">This tutorial shows you how toouse Azure CLI 2.0 tooconvert a virtual machine tooa virtual machine scale set.</span></span> <span data-ttu-id="8bbeb-105">U leert ook hoe tooautomate Hallo configuratie van Hallo virtuele machines in Hallo scale ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-105">You also learn how tooautomate hello configuration of hello virtual machines in hello scale set.</span></span> <span data-ttu-id="8bbeb-106">Voor meer informatie over hoe tooinstall Azure CLI 2.0, Zie [aan de slag met Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8bbeb-106">For more information on how tooinstall Azure CLI 2.0, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span> <span data-ttu-id="8bbeb-107">Zie voor meer informatie over schaalsets [virtuele Machine Scale ingesteld](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8bbeb-107">For more information about scale sets, see [Virtual Machine Scale Sets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span>

## <a name="step-1---deprovision-hello-vm"></a><span data-ttu-id="8bbeb-108">Stap 1 - Deprovision Hallo VM</span><span class="sxs-lookup"><span data-stu-id="8bbeb-108">Step 1 - Deprovision hello VM</span></span>

<span data-ttu-id="8bbeb-109">Gebruik SSH tooconnect toohello VM.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-109">Use SSH tooconnect toohello VM.</span></span>

<span data-ttu-id="8bbeb-110">Identiteitsgegevens Hallo VM hello Azure VM-agent toodelete bestanden en gegevens.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-110">Deprovision hello VM using hello Azure VM agent toodelete files and data.</span></span> <span data-ttu-id="8bbeb-111">Zie voor een gedetailleerd overzicht van het opheffen van inrichting [Linux-machine vastleggen](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="8bbeb-111">For a detailed overview of deprovisioning, see [Capture a Linux virtual machine](capture-image.md).</span></span>

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a><span data-ttu-id="8bbeb-112">Stap 2: een installatiekopie van Hallo VM</span><span class="sxs-lookup"><span data-stu-id="8bbeb-112">Step 2 - Capture an image of hello VM</span></span>

<span data-ttu-id="8bbeb-113">Zie voor een gedetailleerd overzicht van het vastleggen van [Linux-machine vastleggen](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="8bbeb-113">For a detailed overview of capturing, see [Capture a Linux virtual machine](capture-image.md).</span></span>

<span data-ttu-id="8bbeb-114">Toewijzing ongedaan maken met virtuele machine Hallo [az vm ongedaan](/cli/azure/vm#deallocate):</span><span class="sxs-lookup"><span data-stu-id="8bbeb-114">Deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate):</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="8bbeb-115">Generalize Hallo VM met [az vm generalize](/cli/azure/vm#generalize):</span><span class="sxs-lookup"><span data-stu-id="8bbeb-115">Generalize hello VM with [az vm generalize](/cli/azure/vm#generalize):</span></span>

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="8bbeb-116">Een installatiekopie maken van VM-resource met Hallo [az installatiekopie maken](/cli/azure/image#create):</span><span class="sxs-lookup"><span data-stu-id="8bbeb-116">Create an image from hello VM resource with [az image create](/cli/azure/image#create):</span></span>

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a><span data-ttu-id="8bbeb-117">Stap 3: Hallo scale set maken</span><span class="sxs-lookup"><span data-stu-id="8bbeb-117">Step 3 - Create hello scale set</span></span>

<span data-ttu-id="8bbeb-118">Hallo ophalen **id** van Hallo-afbeelding.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-118">Get hello **id** of hello image.</span></span>

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

<span data-ttu-id="8bbeb-119">Een virtuele machine maken van uw Afbeeldingsbron met [az vmss maken](/cli/azure/vmss#create):</span><span class="sxs-lookup"><span data-stu-id="8bbeb-119">Create a VM from your image resource with [az vmss create](/cli/azure/vmss#create):</span></span>

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

<span data-ttu-id="8bbeb-120">Met deze opdracht wordt ook een 10gb-gegevensschijf gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-120">This command also attached a 10gb data disk.</span></span> <span data-ttu-id="8bbeb-121">Houd er rekening mee die, afhankelijk van Hallo VM gekozen grootte (we gebruikt **Standard_DS1_v2**), Hallo aantal gegevensschijven dat mag niet hetzelfde is.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-121">Keep in mind that depending on hello VM size chosen (we used **Standard_DS1_v2**), hello number of data disks allowed is different.</span></span> <span data-ttu-id="8bbeb-122">Raadpleeg voor meer informatie, Hallo [grootten van virtuele machines](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="8bbeb-122">For more information, review hello [virtual machine sizes](sizes.md).</span></span>

<span data-ttu-id="8bbeb-123">Zodra Hallo scale ingesteld is voltooid, sluit u tooit.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-123">Once hello scale set finishes, connect tooit.</span></span> <span data-ttu-id="8bbeb-124">Een lijst met IP-adressen voor Hallo exemplaren ophalen voor SSH met [az vmss lijst--verbinding-Instantiegegevens](/cli/azure/vmss#list-instance-connection-info):</span><span class="sxs-lookup"><span data-stu-id="8bbeb-124">Get a list of IP addresses for hello instances for SSH with [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info):</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

<span data-ttu-id="8bbeb-125">Nu u toohello gegevensschijf voor virtuele machine exemplaar tooinitialize Hallo verbinding kunt maken</span><span class="sxs-lookup"><span data-stu-id="8bbeb-125">Now you can connect toohello virtual machine instance tooinitialize hello data disk</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a><span data-ttu-id="8bbeb-126">Stap 4 - schijf initialiseren Hallo-gegevens</span><span class="sxs-lookup"><span data-stu-id="8bbeb-126">Step 4 - Initialize hello data disk</span></span>

<span data-ttu-id="8bbeb-127">Tijdens het verbonden toohello virtuele machine, partitie-Hallo-schijf met `fdisk`:</span><span class="sxs-lookup"><span data-stu-id="8bbeb-127">While connected toohello virtual machine, partition hello disk with `fdisk`:</span></span>

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="8bbeb-128">Schrijven van een bestand toohello systeempartitie Hello `mkfs` opdracht:</span><span class="sxs-lookup"><span data-stu-id="8bbeb-128">Write a file system toohello partition with hello `mkfs` command:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="8bbeb-129">Hallo nieuwe schijf koppelen zodat deze toegankelijk is in Hallo-besturingssysteem:</span><span class="sxs-lookup"><span data-stu-id="8bbeb-129">Mount hello new disk so that it is accessible in hello operating system:</span></span>

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="8bbeb-130">Hallo-schijf kan nu worden opent via Hallo datadrive koppelpunt, kan worden gecontroleerd met `ls /datadrive/`.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-130">hello disk can now be accesses through hello datadrive mountpoint, which can be verified with `ls /datadrive/`.</span></span>

<span data-ttu-id="8bbeb-131">Hallo SSH-sessie wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-131">End hello SSH session.</span></span>


## <a name="step-5---configure-firewall"></a><span data-ttu-id="8bbeb-132">Stap 5: de firewall configureren</span><span class="sxs-lookup"><span data-stu-id="8bbeb-132">Step 5 - Configure firewall</span></span>

<span data-ttu-id="8bbeb-133">Een gat in Hallo firewall toohello webserver gehost door Hallo schaalset perforeren.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-133">Punch a hole through hello firewall toohello webserver hosted by hello scale set.</span></span> <span data-ttu-id="8bbeb-134">Wanneer het Hallo-schaalset is gemaakt, is ook een load balancer gemaakt en u gebruikt deze **SSH** toohello afzonderlijke virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-134">When hello scale set was created, a load balancer was also created, and you used it **SSH** toohello individual virtual machines.</span></span> <span data-ttu-id="8bbeb-135">een poort tooopen, moet u twee soorten gegevens, die u kunt krijgen met Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-135">tooopen a port, you need two pieces of information, which you can get using Azure CLI.</span></span>

* <span data-ttu-id="8bbeb-136">**Frontend-IP-adresgroep**</span><span class="sxs-lookup"><span data-stu-id="8bbeb-136">**Frontend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* <span data-ttu-id="8bbeb-137">**Backend-IP-adresgroep**</span><span class="sxs-lookup"><span data-stu-id="8bbeb-137">**Backend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

<span data-ttu-id="8bbeb-138">Met deze twee namen, kunt u poort openen **80**.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-138">With those two names, you can open port **80**.</span></span>

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a><span data-ttu-id="8bbeb-139">Stap 6: configuratie automatiseren</span><span class="sxs-lookup"><span data-stu-id="8bbeb-139">Step 6 - Automate configuration</span></span>

<span data-ttu-id="8bbeb-140">Hallo gegevensschijf moet toobe geconfigureerd op elk exemplaar van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-140">hello data disk needs toobe configured on each virtual machine instance.</span></span> <span data-ttu-id="8bbeb-141">We Hallo configuratie van virtuele machine Hallo Hello kunt automatiseren **CustomScript** extensie.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-141">We can automate hello configuration of hello virtual machine with hello **CustomScript** extension.</span></span>

<span data-ttu-id="8bbeb-142">Maak eerst een *.sh* script dat Hallo schijf-indeling opdrachten bevat.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-142">First, create a *.sh* script that includes hello disk format commands.</span></span>

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

<span data-ttu-id="8bbeb-143">Vervolgens uploaden dat script bestand toowhere hello **CustomScript** extensie toegang hebt tot het.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-143">Next, upload that script file toowhere hello **CustomScript** extension can access it.</span></span> <span data-ttu-id="8bbeb-144">Een kopie beschikbaar is [hier](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span><span class="sxs-lookup"><span data-stu-id="8bbeb-144">A copy is available [here](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span></span>

<span data-ttu-id="8bbeb-145">Maken van een lokaal bestand met de naam **settings.json** en put hello volgende blok in het JSON.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-145">Create a local file named **settings.json** and put hello following JSON block in it.</span></span> <span data-ttu-id="8bbeb-146">Hallo `flieUris` eigenschap toowhere het scriptbestand is geüpload naar moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-146">hello `flieUris` property should be set toowhere your script file was uploaded to.</span></span>

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

<span data-ttu-id="8bbeb-147">Implementeren van deze opdracht tooyour schaal ingesteld met Hallo **CustomScript** extensie, die verwijzen naar Hallo **settings.json** bestand die we zojuist hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-147">Deploy this command tooyour scale set with hello **CustomScript** extension, referencing hello **settings.json** file we just created.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

<span data-ttu-id="8bbeb-148">Deze extensie wordt automatisch uitgevoerd op alle huidige exemplaren en alle exemplaren die later wordt gemaakt door te schalen.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-148">This extension automatically runs on all current instances, and any instances later created by scaling.</span></span>

## <a name="step-7---configure-autoscale-rules"></a><span data-ttu-id="8bbeb-149">Stap 7: regels voor automatisch schalen configureren</span><span class="sxs-lookup"><span data-stu-id="8bbeb-149">Step 7 - Configure autoscale rules</span></span>

<span data-ttu-id="8bbeb-150">Op dit moment kunnen kunnen niet regels voor automatisch schalen worden ingesteld in de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-150">Currently, autoscale rules cannot be set in Azure CLI.</span></span> <span data-ttu-id="8bbeb-151">Gebruik Hallo [Azure-portal](https://portal.azure.com) tooconfigure automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-151">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

## <a name="step-8---management-tasks"></a><span data-ttu-id="8bbeb-152">Stap 8 - beheertaken</span><span class="sxs-lookup"><span data-stu-id="8bbeb-152">Step 8 - Management tasks</span></span>

<span data-ttu-id="8bbeb-153">Gedurende de levenscyclus van de Hallo van Hallo scale is ingesteld, moet u mogelijk toorun een of meer beheertaken.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-153">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="8bbeb-154">Bovendien kunt u toocreate scripts die verschillende lifecycle-taken automatiseren en hello Azure CLI biedt een snelle manier toodo deze taken.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-154">Additionally, you may want toocreate scripts that automate various lifecycle-tasks, and hello Azure CLI provides a quick way toodo those tasks.</span></span> <span data-ttu-id="8bbeb-155">Hier volgen enkele algemene taken.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-155">Here are a few common tasks.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="8bbeb-156">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="8bbeb-156">Get connection info</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a><span data-ttu-id="8bbeb-157">Set-exemplaren (handmatige schaal)</span><span class="sxs-lookup"><span data-stu-id="8bbeb-157">Set instance count (manual scale)</span></span>

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a><span data-ttu-id="8bbeb-158">Verwijderen van resourcegroep</span><span class="sxs-lookup"><span data-stu-id="8bbeb-158">Delete resource group</span></span>

<span data-ttu-id="8bbeb-159">Verwijderen van een resourcegroep, worden ook alle resources binnen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8bbeb-159">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="8bbeb-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8bbeb-160">Next steps</span></span>
<span data-ttu-id="8bbeb-161">meer informatie over een aantal virtuele-machineschaalset Hallo functies geïntroduceerd in deze zelfstudie ingesteld toolearn Zie Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="8bbeb-161">toolearn more about some of hello virtual machine scale set features introduced in this tutorial, see hello following information:</span></span>

- [<span data-ttu-id="8bbeb-162">Overzicht van Azure virtuele-Machineschaalsets</span><span class="sxs-lookup"><span data-stu-id="8bbeb-162">Azure Virtual Machine Scale Sets overview</span></span>](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [<span data-ttu-id="8bbeb-163">Overzicht van Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="8bbeb-163">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="8bbeb-164">Beheren van netwerkverkeer met netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="8bbeb-164">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)