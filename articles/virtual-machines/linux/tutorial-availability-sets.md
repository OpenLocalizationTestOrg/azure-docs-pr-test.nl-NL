---
title: aaaAvailability zelfstudie stelt voor virtuele Linux-machines in Azure | Microsoft Docs
description: Meer informatie over Hallo Beschikbaarheidssets voor virtuele Linux-machines in Azure.
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
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="fc977-103">Hoe toouse beschikbaarheidssets</span><span class="sxs-lookup"><span data-stu-id="fc977-103">How toouse availability sets</span></span>


<span data-ttu-id="fc977-104">In deze zelfstudie leert u hoe tooincrease Hallo beschikbaarheid en betrouwbaarheid van uw virtuele Machine-oplossingen in Azure met een mogelijkheid Beschikbaarheidssets aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="fc977-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="fc977-105">Beschikbaarheidssets Zorg ervoor dat u implementeert op Azure VM's zijn verdeeld over meerdere geïsoleerde hardware clusters Hallo.</span><span class="sxs-lookup"><span data-stu-id="fc977-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="fc977-106">Dit zorgt ervoor dat als een storing hardware of software in Azure gebeurt, van invloed op een onderliggende reeks uw virtuele machines die uw algehele oplossing blijft beschikbaar en operationele vanuit het oogpunt van uw klanten die gebruikmaken van het Hallo van.</span><span class="sxs-lookup"><span data-stu-id="fc977-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span>

<span data-ttu-id="fc977-107">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="fc977-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fc977-108">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="fc977-108">Create an availability set</span></span>
> * <span data-ttu-id="fc977-109">Een virtuele machine in een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="fc977-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="fc977-110">Controleer de beschikbare grootten voor virtuele machine</span><span class="sxs-lookup"><span data-stu-id="fc977-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fc977-111">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="fc977-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="fc977-112">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="fc977-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fc977-113">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fc977-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="fc977-114">Overzicht van de beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="fc977-114">Availability set overview</span></span>

<span data-ttu-id="fc977-115">Een Beschikbaarheidsset, is een logische groepering-functie die u kunt gebruiken in Azure tooensure dat Hallo VM resources die u in het plaatsen van elkaar geïsoleerd zijn wanneer ze zijn geïmplementeerd in een Azure-datacenter.</span><span class="sxs-lookup"><span data-stu-id="fc977-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="fc977-116">Azure zorgt ervoor dat Hallo virtuele machines die u binnen een Beschikbaarheidsset uitvoeren op meerdere fysieke servers plaatst, compute rekken eenheden voor opslag en netwerkswitches.</span><span class="sxs-lookup"><span data-stu-id="fc977-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="fc977-117">Dit zorgt ervoor dat in geval van een softwarestoring van de Azure-of hardware Hallo slechts een subset van uw virtuele machines worden beïnvloed en uw algehele toepassing blijft en doorgaan toobe beschikbaar tooyour klanten.</span><span class="sxs-lookup"><span data-stu-id="fc977-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="fc977-118">Gebruik Beschikbaarheidssets is een tooleverage essentiële mogelijkheden als u wilt dat toobuild betrouwbare cloudoplossingen.</span><span class="sxs-lookup"><span data-stu-id="fc977-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="fc977-119">Laten we eens een typische VM-oplossing op basis van waar u mogelijk 4 front-end-webservers en 2 back-end virtuele machines die een database te hosten.</span><span class="sxs-lookup"><span data-stu-id="fc977-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="fc977-120">Met Azure, kunt u twee beschikbaarheidssets toodefine voordat u uw virtuele machines implementeren: één beschikbaarheid instellen voor Hallo 'web' laag en een beschikbaarheidsset voor Hallo 'database' laag.</span><span class="sxs-lookup"><span data-stu-id="fc977-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="fc977-121">Bij het maken van een nieuwe virtuele machine vervolgens u Hallo beschikbaarheid instellen opgeven kunt als een parameter toohello az vm-opdracht maken en Azure zorgt u dat Hallo virtuele machines die u binnen Hallo beschikbaar maken automatisch worden ingesteld op de resources van meerdere fysieke hardware geïsoleerd.</span><span class="sxs-lookup"><span data-stu-id="fc977-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="fc977-122">Dit betekent dat als Hallo fysieke hardware die een van uw webserver of VM's Database-Server wordt uitgevoerd op een probleem, u dat Hallo weet andere exemplaren van uw webserver en de Database virtuele machines blijven actief probleemloos omdat ze op andere hardware.</span><span class="sxs-lookup"><span data-stu-id="fc977-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="fc977-123">Als u wilt dat toodeploy betrouwbare VM gebaseerde oplossingen in Azure, moet u altijd Beschikbaarheidssets gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fc977-123">You should always use Availability Sets when you want toodeploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="fc977-124">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="fc977-124">Create an availability set</span></span>

<span data-ttu-id="fc977-125">Kunt u een beschikbaarheidsset met [az vm beschikbaarheidsset maken](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="fc977-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="fc977-126">In dit voorbeeld we beide Hallo aantal update en fouttolerantie domeinen op instellen *2* voor Hallo beschikbaarheidsset benoemde *myAvailabilitySet* in Hallo *myResourceGroupAvailability*resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="fc977-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="fc977-127">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="fc977-127">Create a resource group.</span></span>

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

<span data-ttu-id="fc977-128">Beschikbaarheidssets kunnen u resources tooisolate over 'foutdomeinen' en 'domeinen bijwerken'.</span><span class="sxs-lookup"><span data-stu-id="fc977-128">Availability Sets allow you tooisolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="fc977-129">Een **foutdomein** vertegenwoordigt een geïsoleerd verzameling server + netwerk en opslag resources.</span><span class="sxs-lookup"><span data-stu-id="fc977-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="fc977-130">Hallo voorgaande voorbeeld, geven we dat we dat onze beschikbaarheidsset toobe verdeeld over ten minste twee domeinen met fouten willen als onze virtuele machines worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="fc977-130">In hello preceding example, we indicate that we want our availability set toobe distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="fc977-131">We ook aangeven dat we onze beschikbaarheidsset gedistribueerde in twee **domeinen bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="fc977-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="fc977-132">Twee domeinen van de update ervoor te zorgen dat wanneer Azure voert de software-updates voor onze VM-netwerkbronnen geïsoleerd, waardoor alle Hallo software uitgevoerd onder de virtuele machine wordt bijgewerkt op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="fc977-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all hello software running underneath our VM from being updated at hello same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="fc977-133">Virtueel netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="fc977-133">Configure virtual network</span></span>
<span data-ttu-id="fc977-134">Voordat u een aantal virtuele machines implementeren en uw balancer kunt testen, maak Hallo ondersteunende resources van een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="fc977-134">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="fc977-135">Zie voor meer informatie over virtuele netwerken Hallo [Azure Virtual Networks beheren](tutorial-virtual-network.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="fc977-135">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="fc977-136">Maken van netwerkbronnen</span><span class="sxs-lookup"><span data-stu-id="fc977-136">Create network resources</span></span>
<span data-ttu-id="fc977-137">Maak een virtueel netwerk met [az network vnet maken](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="fc977-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="fc977-138">Hallo volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* met een subnet met de naam *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="fc977-138">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="fc977-139">Virtuele NIC's zijn gemaakt met [az netwerk nic maken](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="fc977-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="fc977-140">Hallo maakt volgende voorbeeld drie virtuele NIC's.</span><span class="sxs-lookup"><span data-stu-id="fc977-140">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="fc977-141">(Een virtuele NIC voor elke VM die u maakt voor uw app in hello te volgen stappen.)</span><span class="sxs-lookup"><span data-stu-id="fc977-141">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="fc977-142">U kunt extra virtuele NIC's en virtuele machines maken op elk gewenst moment en ze toohello load balancer toevoegen:</span><span class="sxs-lookup"><span data-stu-id="fc977-142">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

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

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="fc977-143">Virtuele machines in een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="fc977-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="fc977-144">Virtuele machines moeten worden gemaakt binnen Hallo beschikbaarheid set toomake zeker van te zijn dat ze correct zijn verdeeld over Hallo hardware.</span><span class="sxs-lookup"><span data-stu-id="fc977-144">VMs must be created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="fc977-145">U kunt een bestaande VM tooan beschikbaarheidsset nadat deze is gemaakt niet toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fc977-145">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="fc977-146">Wanneer u een virtuele machine met maakt [az vm maken](/cli/azure/vm#create) u Hallo beschikbaarheid instellen met behulp van Hallo opgeven `--availability-set` toospecify Hallo parameternaam van Hallo beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="fc977-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify hello availability set using hello `--availability-set` parameter toospecify hello name of hello availability set.</span></span>

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

<span data-ttu-id="fc977-147">Nu hebben we twee virtuele machines in onze nieuwe beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="fc977-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="fc977-148">Omdat ze zich in dezelfde Hallo beschikbaarheidsset, Azure zorgt ervoor dat Hallo VM's en alle hun bronnen (met inbegrip van gegevensschijven) worden gedistribueerd over geïsoleerde fysieke hardware.</span><span class="sxs-lookup"><span data-stu-id="fc977-148">Because they are in hello same availability set, Azure will ensure that hello VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="fc977-149">Deze verdeling kan ervoor zorgen veel hogere beschikbaarheid van de algehele oplossing voor de VM.</span><span class="sxs-lookup"><span data-stu-id="fc977-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="fc977-150">Wat die u tegenkomen kunt wanneer u virtuele machines toevoegt is een bepaalde VM-grootte is niet langer beschikbaar toouse binnen uw beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="fc977-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available toouse within your availability set.</span></span> <span data-ttu-id="fc977-151">Dit probleem kan zich voordoen als er niet langer voldoende capaciteit tooadd het is behoud van Hallo beschikbaarheidsset voor Hallo isolatie regels worden afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="fc977-151">This issue can happen if there is no longer enough capacity tooadd it while preserving hello isolation rules hello availability set enforces.</span></span> <span data-ttu-id="fc977-152">U kunt toosee controleren welke VM-grootten zijn beschikbaar toouse binnen een bestaande beschikbaarheidsset gebruiken Hallo `--availability-set list-sizes` parameter.</span><span class="sxs-lookup"><span data-stu-id="fc977-152">You can check toosee what VM sizes are available toouse within an existing availability set using hello `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="fc977-153">Controleren op beschikbare VM-grootten</span><span class="sxs-lookup"><span data-stu-id="fc977-153">Check for available VM sizes</span></span> 

<span data-ttu-id="fc977-154">U kunt meer virtuele machines toohello beschikbaarheidsset later toevoegen, maar u moet tooknow welke VM-grootten zijn beschikbaar op Hallo hardware.</span><span class="sxs-lookup"><span data-stu-id="fc977-154">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="fc977-155">Gebruik [az vm beschikbaarheidsset lijst met grootten](/cli/azure/availability-set#list-sizes) toolist alle beschikbare grootten van Hallo op Hallo hardware-cluster voor Hallo beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="fc977-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="fc977-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fc977-156">Next steps</span></span>

<span data-ttu-id="fc977-157">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="fc977-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fc977-158">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="fc977-158">Create an availability set</span></span>
> * <span data-ttu-id="fc977-159">Een virtuele machine in een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="fc977-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="fc977-160">Controleer de beschikbare grootten voor virtuele machine</span><span class="sxs-lookup"><span data-stu-id="fc977-160">Check available VM sizes</span></span>

<span data-ttu-id="fc977-161">Toohello volgende zelfstudie toolearn over virtuele-machineschaalsets gaan.</span><span class="sxs-lookup"><span data-stu-id="fc977-161">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc977-162">Een VM-schaalset maken</span><span class="sxs-lookup"><span data-stu-id="fc977-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

