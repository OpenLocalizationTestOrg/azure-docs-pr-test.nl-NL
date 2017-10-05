---
title: Beschikbaarheidssets zelfstudie voor virtuele Linux-machines in Azure | Microsoft Docs
description: Meer informatie over de Beschikbaarheidssets voor virtuele Linux-machines in Azure.
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 63fe3f165864f06228604cac56d06cc061ab25f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-availability-sets"></a><span data-ttu-id="c93d5-103">Het gebruik van beschikbaarheidssets</span><span class="sxs-lookup"><span data-stu-id="c93d5-103">How to use availability sets</span></span>


<span data-ttu-id="c93d5-104">In deze zelfstudie leert u hoe u verhoogt de beschikbaarheid en betrouwbaarheid van uw virtuele Machine-oplossingen in Azure met een mogelijkheid Beschikbaarheidssets aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c93d5-104">In this tutorial, you will learn how to increase the availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="c93d5-105">Beschikbaarheidssets Zorg ervoor dat de virtuele machines die u implementeert in Azure worden gedistribueerd over meerdere geïsoleerde hardware-clusters.</span><span class="sxs-lookup"><span data-stu-id="c93d5-105">Availability sets ensure that the VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="c93d5-106">Dit zorgt ervoor dat als een storing hardware of software in Azure gebeurt, van invloed op een onderliggende reeks uw virtuele machines en die uw algehele oplossing blijft beschikbaar en operationele vanuit het perspectief van uw gebruik van klanten.</span><span class="sxs-lookup"><span data-stu-id="c93d5-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from the perspective of your customers using it.</span></span>

<span data-ttu-id="c93d5-107">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="c93d5-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c93d5-108">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="c93d5-108">Create an availability set</span></span>
> * <span data-ttu-id="c93d5-109">Een virtuele machine in een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="c93d5-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="c93d5-110">Controleer de beschikbare grootten voor virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c93d5-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c93d5-111">Als u wilt installeren en gebruiken van de CLI lokaal, in deze zelfstudie vereist dat u de Azure CLI versie 2.0.4 zijn uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="c93d5-111">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c93d5-112">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="c93d5-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="c93d5-113">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c93d5-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="c93d5-114">Overzicht van de beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="c93d5-114">Availability set overview</span></span>

<span data-ttu-id="c93d5-115">Een Beschikbaarheidsset is een logische groepering-functie die u in Azure gebruiken kunt om ervoor te zorgen dat de VM-resources die u in het plaatsen van elkaar geïsoleerd zijn wanneer ze zijn geïmplementeerd in een Azure-datacenter.</span><span class="sxs-lookup"><span data-stu-id="c93d5-115">An Availability Set is a logical grouping capability that you can use in Azure to ensure that the VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="c93d5-116">Azure zorgt ervoor dat de virtuele machines die u binnen een Beschikbaarheidsset uitvoeren op meerdere fysieke servers plaatst, compute rekken eenheden voor opslag en netwerkswitches.</span><span class="sxs-lookup"><span data-stu-id="c93d5-116">Azure ensures that the VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="c93d5-117">Dit zorgt ervoor dat in het geval van een hardware- of Azure software fout slechts een subset van uw virtuele machines worden beïnvloed en uw algehele toepassing blijft en blijven beschikbaar voor uw klanten.</span><span class="sxs-lookup"><span data-stu-id="c93d5-117">This ensures that in the event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue to be available to your customers.</span></span> <span data-ttu-id="c93d5-118">Met behulp van Beschikbaarheidssets is een essentiële functie gebruiken als u wilt om betrouwbare cloudoplossingen te bouwen.</span><span class="sxs-lookup"><span data-stu-id="c93d5-118">Using Availability Sets is an essential capability to leverage when you want to build reliable cloud solutions.</span></span>

<span data-ttu-id="c93d5-119">Laten we eens een typische VM-oplossing op basis van waar u mogelijk 4 front-end-webservers en 2 back-end virtuele machines die een database te hosten.</span><span class="sxs-lookup"><span data-stu-id="c93d5-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="c93d5-120">Met Azure twee beschikbaarheidssets definiëren voordat u uw virtuele machines implementeert u zou willen: één beschikbaarheidsset voor de laag 'web' en een beschikbaarheidsset voor de laag 'database'.</span><span class="sxs-lookup"><span data-stu-id="c93d5-120">With Azure, you’d want to define two availability sets before you deploy your VMs: one availability set for the “web” tier and one availability set for the “database” tier.</span></span> <span data-ttu-id="c93d5-121">Bij het maken van een nieuwe virtuele machine vervolgens u kunt de beschikbaarheidsset als een parameter voor de vm az opdracht maken en Azure automatisch zorgt u dat de virtuele machines die u in de set beschikbaar maakt zijn geïsoleerd over meerdere fysieke hardware-resources.</span><span class="sxs-lookup"><span data-stu-id="c93d5-121">When you create a new VM you can then specify the availability set as a parameter to the az vm create command, and Azure will automatically ensure that the VMs you create within the available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="c93d5-122">Dit betekent dat als de fysieke hardware die een van uw webserver of VM's Database-Server wordt uitgevoerd op een probleem is, u kent dat de andere exemplaren van uw webserver en de Database virtuele machines actief probleemloos blijven wordt omdat ze op andere hardware.</span><span class="sxs-lookup"><span data-stu-id="c93d5-122">This means that if the physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that the other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="c93d5-123">U moet altijd Beschikbaarheidssets gebruiken wanneer u wilt implementeren, betrouwbare oplossingen op basis van virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="c93d5-123">You should always use Availability Sets when you want to deploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="c93d5-124">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="c93d5-124">Create an availability set</span></span>

<span data-ttu-id="c93d5-125">Kunt u een beschikbaarheidsset met [az vm beschikbaarheidsset maken](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="c93d5-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="c93d5-126">In dit voorbeeld wordt zowel het aantal update en fouttolerantie domeinen op ingesteld *2* voor de beschikbaarheid van de set met de naam *myAvailabilitySet* in de *myResourceGroupAvailability* resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c93d5-126">In this example, we set both the number of update and fault domains at *2* for the availability set named *myAvailabilitySet* in the *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="c93d5-127">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c93d5-127">Create a resource group.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

<span data-ttu-id="c93d5-128">Beschikbaarheidssets kunnen u resources in 'foutdomeinen' en 'domeinen bijwerken' isoleren.</span><span class="sxs-lookup"><span data-stu-id="c93d5-128">Availability Sets allow you to isolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="c93d5-129">Een **foutdomein** vertegenwoordigt een geïsoleerd verzameling server + netwerk en opslag resources.</span><span class="sxs-lookup"><span data-stu-id="c93d5-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="c93d5-130">In het voorgaande voorbeeld geven we willen we onze beschikbaarheidsset verdeeld over ten minste twee domeinen met fouten als onze virtuele machines worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c93d5-130">In the preceding example, we indicate that we want our availability set to be distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="c93d5-131">We ook aangeven dat we onze beschikbaarheidsset gedistribueerde in twee **domeinen bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="c93d5-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="c93d5-132">Twee update domeinen Zorg ervoor dat wanneer Azure voert de software-updates onze VM-netwerkbronnen geïsoleerd, waardoor alle software die worden uitgevoerd onder de virtuele machine tegelijk worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c93d5-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all the software running underneath our VM from being updated at the same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="c93d5-133">Virtueel netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="c93d5-133">Configure virtual network</span></span>
<span data-ttu-id="c93d5-134">Voordat u een aantal virtuele machines implementeren en uw balancer kunt testen, moet u de resources van de ondersteunende virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="c93d5-134">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="c93d5-135">Zie voor meer informatie over virtuele netwerken van de [Azure Virtual Networks beheren](tutorial-virtual-network.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="c93d5-135">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="c93d5-136">Maken van netwerkbronnen</span><span class="sxs-lookup"><span data-stu-id="c93d5-136">Create network resources</span></span>
<span data-ttu-id="c93d5-137">Maak een virtueel netwerk met [az network vnet maken](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="c93d5-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="c93d5-138">Het volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* met een subnet met de naam *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="c93d5-138">The following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="c93d5-139">Virtuele NIC's zijn gemaakt met [az netwerk nic maken](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="c93d5-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="c93d5-140">Het volgende voorbeeld maakt drie virtuele NIC's.</span><span class="sxs-lookup"><span data-stu-id="c93d5-140">The following example creates three virtual NICs.</span></span> <span data-ttu-id="c93d5-141">(Een virtuele NIC voor elke VM die u maakt voor uw app in de volgende stappen uit).</span><span class="sxs-lookup"><span data-stu-id="c93d5-141">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="c93d5-142">U kunt extra virtuele NIC's en virtuele machines maken op elk gewenst moment en toe te voegen aan de load balancer:</span><span class="sxs-lookup"><span data-stu-id="c93d5-142">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="c93d5-143">Virtuele machines in een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="c93d5-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="c93d5-144">Virtuele machines moeten worden gemaakt binnen de beschikbaarheidsset om ervoor te zorgen dat ze correct zijn verdeeld over de hardware.</span><span class="sxs-lookup"><span data-stu-id="c93d5-144">VMs must be created within the availability set to make sure they are correctly distributed across the hardware.</span></span> <span data-ttu-id="c93d5-145">U kunt een bestaande virtuele machine toevoegen aan een beschikbaarheidsset nadat deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c93d5-145">You can't add an existing VM to an availability set after it is created.</span></span> 

<span data-ttu-id="c93d5-146">Wanneer u een virtuele machine met maakt [az vm maken](/cli/azure/vm#create) opgeven van de beschikbaarheidsset met behulp van de `--availability-set` parameter om de naam van de beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="c93d5-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify the availability set using the `--availability-set` parameter to specify the name of the availability set.</span></span>

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

<span data-ttu-id="c93d5-147">Nu hebben we twee virtuele machines in onze nieuwe beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="c93d5-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="c93d5-148">Omdat ze zich in dezelfde beschikbaarheidsset, kan Azure zorgt ervoor dat de virtuele machines en alle bijbehorende resources (inclusief gegevensschijven) worden gedistribueerd over geïsoleerde fysieke hardware.</span><span class="sxs-lookup"><span data-stu-id="c93d5-148">Because they are in the same availability set, Azure will ensure that the VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="c93d5-149">Deze verdeling kan ervoor zorgen veel hogere beschikbaarheid van de algehele oplossing voor de VM.</span><span class="sxs-lookup"><span data-stu-id="c93d5-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="c93d5-150">Wat die u tegenkomen kunt wanneer u virtuele machines toevoegt is een bepaalde VM-grootte is niet meer beschikbaar voor gebruik binnen uw beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="c93d5-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available to use within your availability set.</span></span> <span data-ttu-id="c93d5-151">Dit probleem kan zich voordoen als er niet langer voldoende capaciteit toe te voegen is behoud de isolatie van regels voor de beschikbaarheidsset worden afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="c93d5-151">This issue can happen if there is no longer enough capacity to add it while preserving the isolation rules the availability set enforces.</span></span> <span data-ttu-id="c93d5-152">U kunt controleren om te zien welke VM-grootten zijn beschikbaar voor gebruik binnen de bestaande beschikbaarheidsset ingesteld met de `--availability-set list-sizes` parameter.</span><span class="sxs-lookup"><span data-stu-id="c93d5-152">You can check to see what VM sizes are available to use within an existing availability set using the `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="c93d5-153">Controleren op beschikbare VM-grootten</span><span class="sxs-lookup"><span data-stu-id="c93d5-153">Check for available VM sizes</span></span> 

<span data-ttu-id="c93d5-154">U kunt meer virtuele machines toevoegen aan de beschikbaarheid later instellen, maar u moet weten welke VM-grootten zijn beschikbaar op de hardware.</span><span class="sxs-lookup"><span data-stu-id="c93d5-154">You can add more VMs to the availability set later, but you need to know what VM sizes are available on the hardware.</span></span> <span data-ttu-id="c93d5-155">Gebruik [az vm beschikbaarheidsset lijst met grootten](/cli/azure/availability-set#list-sizes) voor een lijst met alle van de beschikbare grootten van de hardware-cluster gebruikt voor de beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="c93d5-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) to list all the available sizes on the hardware cluster for the availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="c93d5-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c93d5-156">Next steps</span></span>

<span data-ttu-id="c93d5-157">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="c93d5-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c93d5-158">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="c93d5-158">Create an availability set</span></span>
> * <span data-ttu-id="c93d5-159">Een virtuele machine in een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="c93d5-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="c93d5-160">Controleer de beschikbare grootten voor virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c93d5-160">Check available VM sizes</span></span>

<span data-ttu-id="c93d5-161">Ga naar de volgende zelfstudie voor meer informatie over virtuele-machineschaalsets.</span><span class="sxs-lookup"><span data-stu-id="c93d5-161">Advance to the next tutorial to learn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c93d5-162">Een VM-schaalset maken</span><span class="sxs-lookup"><span data-stu-id="c93d5-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

