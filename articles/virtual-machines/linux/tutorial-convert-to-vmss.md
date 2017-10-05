---
title: Een Azure VM converteren naar een schaalset | Microsoft Docs
description: Maken en implementeren van een Linux Azure virtuele-machineschaalset ingesteld met de Azure CLI.
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
ms.openlocfilehash: 8d3376d2791b1349298db618d475ce5573083702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="convert-an-existing-azure-virtual-machine-to-a-scale-set"></a><span data-ttu-id="946a9-103">Een bestaande Azure virtuele machine converteren naar een schaalset</span><span class="sxs-lookup"><span data-stu-id="946a9-103">Convert an existing Azure virtual machine to a scale set</span></span>

<span data-ttu-id="946a9-104">Deze zelfstudie laat zien hoe u Azure CLI 2.0 gebruiken een virtuele machine converteren naar een virtuele-machineschaalset.</span><span class="sxs-lookup"><span data-stu-id="946a9-104">This tutorial shows you how to use Azure CLI 2.0 to convert a virtual machine to a virtual machine scale set.</span></span> <span data-ttu-id="946a9-105">U leert ook hoe u de configuratie van de virtuele machines in de schaalset automatiseren.</span><span class="sxs-lookup"><span data-stu-id="946a9-105">You also learn how to automate the configuration of the virtual machines in the scale set.</span></span> <span data-ttu-id="946a9-106">Zie voor meer informatie over het installeren van Azure CLI 2.0 [aan de slag met Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="946a9-106">For more information on how to install Azure CLI 2.0, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span> <span data-ttu-id="946a9-107">Zie voor meer informatie over schaalsets [virtuele Machine Scale ingesteld](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="946a9-107">For more information about scale sets, see [Virtual Machine Scale Sets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span>

## <a name="step-1---deprovision-the-vm"></a><span data-ttu-id="946a9-108">Stap 1: inrichting ervan ongedaan maakt de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="946a9-108">Step 1 - Deprovision the VM</span></span>

<span data-ttu-id="946a9-109">SSH gebruiken voor verbinding met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="946a9-109">Use SSH to connect to the VM.</span></span>

<span data-ttu-id="946a9-110">Inrichting ervan ongedaan maakt de virtuele machine met behulp van de Azure VM-agent verwijderen van bestanden en gegevens.</span><span class="sxs-lookup"><span data-stu-id="946a9-110">Deprovision the VM using the Azure VM agent to delete files and data.</span></span> <span data-ttu-id="946a9-111">Zie voor een gedetailleerd overzicht van het opheffen van inrichting [Linux-machine vastleggen](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="946a9-111">For a detailed overview of deprovisioning, see [Capture a Linux virtual machine](capture-image.md).</span></span>

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-the-vm"></a><span data-ttu-id="946a9-112">Stap 2: een installatiekopie van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="946a9-112">Step 2 - Capture an image of the VM</span></span>

<span data-ttu-id="946a9-113">Zie voor een gedetailleerd overzicht van het vastleggen van [Linux-machine vastleggen](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="946a9-113">For a detailed overview of capturing, see [Capture a Linux virtual machine](capture-image.md).</span></span>

<span data-ttu-id="946a9-114">Toewijzing van de virtuele machine met [az vm ongedaan](/cli/azure/vm#deallocate):</span><span class="sxs-lookup"><span data-stu-id="946a9-114">Deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate):</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="946a9-115">De virtuele machine met generalize [az vm generalize](/cli/azure/vm#generalize):</span><span class="sxs-lookup"><span data-stu-id="946a9-115">Generalize the VM with [az vm generalize](/cli/azure/vm#generalize):</span></span>

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="946a9-116">Een installatiekopie maken van de VM-resource met [az installatiekopie maken](/cli/azure/image#create):</span><span class="sxs-lookup"><span data-stu-id="946a9-116">Create an image from the VM resource with [az image create](/cli/azure/image#create):</span></span>

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-the-scale-set"></a><span data-ttu-id="946a9-117">Stap 3: de schaalaanpassingsset maken</span><span class="sxs-lookup"><span data-stu-id="946a9-117">Step 3 - Create the scale set</span></span>

<span data-ttu-id="946a9-118">Ophalen van de **id** van de afbeelding.</span><span class="sxs-lookup"><span data-stu-id="946a9-118">Get the **id** of the image.</span></span>

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

<span data-ttu-id="946a9-119">Een virtuele machine maken van uw Afbeeldingsbron met [az vmss maken](/cli/azure/vmss#create):</span><span class="sxs-lookup"><span data-stu-id="946a9-119">Create a VM from your image resource with [az vmss create](/cli/azure/vmss#create):</span></span>

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

<span data-ttu-id="946a9-120">Met deze opdracht wordt ook een 10gb-gegevensschijf gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="946a9-120">This command also attached a 10gb data disk.</span></span> <span data-ttu-id="946a9-121">Houd er rekening mee dat, afhankelijk van de virtuele machine door u gekozen grootte (we gebruikt **Standard_DS1_v2**), het aantal gegevensschijven toegestaan verschilt.</span><span class="sxs-lookup"><span data-stu-id="946a9-121">Keep in mind that depending on the VM size chosen (we used **Standard_DS1_v2**), the number of data disks allowed is different.</span></span> <span data-ttu-id="946a9-122">Raadpleeg voor meer informatie de [grootten van virtuele machines](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="946a9-122">For more information, review the [virtual machine sizes](sizes.md).</span></span>

<span data-ttu-id="946a9-123">Zodra de schaal ingesteld is voltooid, er verbinding mee maken.</span><span class="sxs-lookup"><span data-stu-id="946a9-123">Once the scale set finishes, connect to it.</span></span> <span data-ttu-id="946a9-124">Een lijst met IP-adressen voor de exemplaren ophalen voor SSH met [az vmss lijst--verbinding-Instantiegegevens](/cli/azure/vmss#list-instance-connection-info):</span><span class="sxs-lookup"><span data-stu-id="946a9-124">Get a list of IP addresses for the instances for SSH with [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info):</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

<span data-ttu-id="946a9-125">Nu u verbinding kunt maken met het exemplaar van de virtuele machine voor het initialiseren van de gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="946a9-125">Now you can connect to the virtual machine instance to initialize the data disk</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-the-data-disk"></a><span data-ttu-id="946a9-126">Stap 4: de gegevensschijf initialiseren</span><span class="sxs-lookup"><span data-stu-id="946a9-126">Step 4 - Initialize the data disk</span></span>

<span data-ttu-id="946a9-127">Verbinding gemaakt met de virtuele machine en de schijf met partitioneren `fdisk`:</span><span class="sxs-lookup"><span data-stu-id="946a9-127">While connected to the virtual machine, partition the disk with `fdisk`:</span></span>

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="946a9-128">Een bestandssysteem schrijven naar de partitie met de `mkfs` opdracht:</span><span class="sxs-lookup"><span data-stu-id="946a9-128">Write a file system to the partition with the `mkfs` command:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="946a9-129">De nieuwe schijf koppelen zodat deze toegankelijk is in het besturingssysteem:</span><span class="sxs-lookup"><span data-stu-id="946a9-129">Mount the new disk so that it is accessible in the operating system:</span></span>

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="946a9-130">De schijf kan nu worden toegang via het koppelpunt datadrive, die kan worden gecontroleerd met `ls /datadrive/`.</span><span class="sxs-lookup"><span data-stu-id="946a9-130">The disk can now be accesses through the datadrive mountpoint, which can be verified with `ls /datadrive/`.</span></span>

<span data-ttu-id="946a9-131">De SSH-sessie te beëindigen.</span><span class="sxs-lookup"><span data-stu-id="946a9-131">End the SSH session.</span></span>


## <a name="step-5---configure-firewall"></a><span data-ttu-id="946a9-132">Stap 5: de firewall configureren</span><span class="sxs-lookup"><span data-stu-id="946a9-132">Step 5 - Configure firewall</span></span>

<span data-ttu-id="946a9-133">Een gat in de firewall op de webserver dat wordt gehost door de schaalaanpassingsset perforeren.</span><span class="sxs-lookup"><span data-stu-id="946a9-133">Punch a hole through the firewall to the webserver hosted by the scale set.</span></span> <span data-ttu-id="946a9-134">Wanneer de schaalaanpassingsset is gemaakt, ook een load balancer gemaakt is en u deze gebruikt **SSH** aan de afzonderlijke virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="946a9-134">When the scale set was created, a load balancer was also created, and you used it **SSH** to the individual virtual machines.</span></span> <span data-ttu-id="946a9-135">Als u wilt een poort opent, moet u twee soorten gegevens, die u kunt krijgen met Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="946a9-135">To open a port, you need two pieces of information, which you can get using Azure CLI.</span></span>

* <span data-ttu-id="946a9-136">**Frontend-IP-adresgroep**</span><span class="sxs-lookup"><span data-stu-id="946a9-136">**Frontend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* <span data-ttu-id="946a9-137">**Backend-IP-adresgroep**</span><span class="sxs-lookup"><span data-stu-id="946a9-137">**Backend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

<span data-ttu-id="946a9-138">Met deze twee namen, kunt u poort openen **80**.</span><span class="sxs-lookup"><span data-stu-id="946a9-138">With those two names, you can open port **80**.</span></span>

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a><span data-ttu-id="946a9-139">Stap 6: configuratie automatiseren</span><span class="sxs-lookup"><span data-stu-id="946a9-139">Step 6 - Automate configuration</span></span>

<span data-ttu-id="946a9-140">De gegevensschijf moet worden geconfigureerd op elk exemplaar van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="946a9-140">The data disk needs to be configured on each virtual machine instance.</span></span> <span data-ttu-id="946a9-141">We kunnen de configuratie van de virtuele machine met automatiseren de **CustomScript** extensie.</span><span class="sxs-lookup"><span data-stu-id="946a9-141">We can automate the configuration of the virtual machine with the **CustomScript** extension.</span></span>

<span data-ttu-id="946a9-142">Maak eerst een *.sh* script dat de opdrachten van schijf-indeling bevat.</span><span class="sxs-lookup"><span data-stu-id="946a9-142">First, create a *.sh* script that includes the disk format commands.</span></span>

```sh
#!/bin/bash

# Setup the data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

<span data-ttu-id="946a9-143">Vervolgens scriptbestand uploaden naar waar de **CustomScript** extensie toegang hebt tot het.</span><span class="sxs-lookup"><span data-stu-id="946a9-143">Next, upload that script file to where the **CustomScript** extension can access it.</span></span> <span data-ttu-id="946a9-144">Een kopie beschikbaar is [hier](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span><span class="sxs-lookup"><span data-stu-id="946a9-144">A copy is available [here](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span></span>

<span data-ttu-id="946a9-145">Maken van een lokaal bestand met de naam **settings.json** en het volgende JSON-blok in het plaatsen.</span><span class="sxs-lookup"><span data-stu-id="946a9-145">Create a local file named **settings.json** and put the following JSON block in it.</span></span> <span data-ttu-id="946a9-146">De `flieUris` eigenschap moet worden ingesteld op waar het scriptbestand is geüpload naar.</span><span class="sxs-lookup"><span data-stu-id="946a9-146">The `flieUris` property should be set to where your script file was uploaded to.</span></span>

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

<span data-ttu-id="946a9-147">Met deze opdracht implementeren voor uw scale ingesteld met de **CustomScript** extensie, die verwijzen naar de **settings.json** bestand die we zojuist hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="946a9-147">Deploy this command to your scale set with the **CustomScript** extension, referencing the **settings.json** file we just created.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

<span data-ttu-id="946a9-148">Deze extensie wordt automatisch uitgevoerd op alle huidige exemplaren en alle exemplaren die later wordt gemaakt door te schalen.</span><span class="sxs-lookup"><span data-stu-id="946a9-148">This extension automatically runs on all current instances, and any instances later created by scaling.</span></span>

## <a name="step-7---configure-autoscale-rules"></a><span data-ttu-id="946a9-149">Stap 7: regels voor automatisch schalen configureren</span><span class="sxs-lookup"><span data-stu-id="946a9-149">Step 7 - Configure autoscale rules</span></span>

<span data-ttu-id="946a9-150">Op dit moment kunnen kunnen niet regels voor automatisch schalen worden ingesteld in de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="946a9-150">Currently, autoscale rules cannot be set in Azure CLI.</span></span> <span data-ttu-id="946a9-151">Gebruik de [Azure-portal](https://portal.azure.com) automatisch schalen configureren.</span><span class="sxs-lookup"><span data-stu-id="946a9-151">Use the [Azure portal](https://portal.azure.com) to configure autoscale.</span></span>

## <a name="step-8---management-tasks"></a><span data-ttu-id="946a9-152">Stap 8 - beheertaken</span><span class="sxs-lookup"><span data-stu-id="946a9-152">Step 8 - Management tasks</span></span>

<span data-ttu-id="946a9-153">Gedurende de levenscyclus van de schaal is ingesteld, moet u wellicht een of meer beheertaken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="946a9-153">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="946a9-154">Bovendien kunt u scripts maken die verschillende lifecycle-taken automatiseren en de Azure CLI biedt een snelle manier om deze taken.</span><span class="sxs-lookup"><span data-stu-id="946a9-154">Additionally, you may want to create scripts that automate various lifecycle-tasks, and the Azure CLI provides a quick way to do those tasks.</span></span> <span data-ttu-id="946a9-155">Hier volgen enkele algemene taken.</span><span class="sxs-lookup"><span data-stu-id="946a9-155">Here are a few common tasks.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="946a9-156">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="946a9-156">Get connection info</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a><span data-ttu-id="946a9-157">Set-exemplaren (handmatige schaal)</span><span class="sxs-lookup"><span data-stu-id="946a9-157">Set instance count (manual scale)</span></span>

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a><span data-ttu-id="946a9-158">Verwijderen van resourcegroep</span><span class="sxs-lookup"><span data-stu-id="946a9-158">Delete resource group</span></span>

<span data-ttu-id="946a9-159">Verwijderen van een resourcegroep, worden ook alle resources binnen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="946a9-159">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="946a9-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="946a9-160">Next steps</span></span>
<span data-ttu-id="946a9-161">Zie voor meer informatie over enkele van de virtuele machine scale set functies geïntroduceerd in deze zelfstudie, de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="946a9-161">To learn more about some of the virtual machine scale set features introduced in this tutorial, see the following information:</span></span>

- [<span data-ttu-id="946a9-162">Overzicht van Azure virtuele-Machineschaalsets</span><span class="sxs-lookup"><span data-stu-id="946a9-162">Azure Virtual Machine Scale Sets overview</span></span>](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [<span data-ttu-id="946a9-163">Overzicht van Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="946a9-163">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="946a9-164">Beheren van netwerkverkeer met netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="946a9-164">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)