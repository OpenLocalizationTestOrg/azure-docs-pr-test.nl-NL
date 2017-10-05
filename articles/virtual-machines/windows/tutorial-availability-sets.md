---
title: Beschikbaarheidssets zelfstudie voor Windows-machines in Azure | Microsoft Docs
description: Meer informatie over de Beschikbaarheidssets voor Windows-machines in Azure.
documentationcenter: 
services: virtual-machines-windows
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: d918362106ef93cf47620e0018d363cd510884b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-availability-sets"></a><span data-ttu-id="419db-103">Het gebruik van beschikbaarheidssets</span><span class="sxs-lookup"><span data-stu-id="419db-103">How to use availability sets</span></span>

<span data-ttu-id="419db-104">In deze zelfstudie leert u hoe u verhoogt de beschikbaarheid en betrouwbaarheid van uw virtuele Machine-oplossingen in Azure met een mogelijkheid Beschikbaarheidssets aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="419db-104">In this tutorial, you will learn how to increase the availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="419db-105">Beschikbaarheidssets Zorg ervoor dat de virtuele machines die u implementeert in Azure worden gedistribueerd over meerdere geïsoleerde hardware-clusters.</span><span class="sxs-lookup"><span data-stu-id="419db-105">Availability sets ensure that the VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="419db-106">Dit zorgt ervoor dat als een storing hardware of software in Azure gebeurt, van invloed op een onderliggende reeks uw virtuele machines en die uw algehele oplossing blijft beschikbaar en operationele vanuit het perspectief van uw gebruik van klanten.</span><span class="sxs-lookup"><span data-stu-id="419db-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from the perspective of your customers using it.</span></span> 

<span data-ttu-id="419db-107">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="419db-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="419db-108">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="419db-108">Create an availability set</span></span>
> * <span data-ttu-id="419db-109">Een virtuele machine in een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="419db-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="419db-110">Controleer de beschikbare grootten voor virtuele machine</span><span class="sxs-lookup"><span data-stu-id="419db-110">Check available VM sizes</span></span>

<span data-ttu-id="419db-111">Voor deze zelfstudie is moduleversie 3,6 of hoger van Azure PowerShell vereist.</span><span class="sxs-lookup"><span data-stu-id="419db-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="419db-112">Voer ` Get-Module -ListAvailable AzureRM` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="419db-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="419db-113">Als u upgraden wilt, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="419db-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="419db-114">Overzicht van de beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="419db-114">Availability set overview</span></span>

<span data-ttu-id="419db-115">Een Beschikbaarheidsset is een logische groepering-functie die u in Azure gebruiken kunt om ervoor te zorgen dat de VM-resources die u in het plaatsen van elkaar geïsoleerd zijn wanneer ze zijn geïmplementeerd in een Azure-datacenter.</span><span class="sxs-lookup"><span data-stu-id="419db-115">An Availability Set is a logical grouping capability that you can use in Azure to ensure that the VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="419db-116">Azure zorgt ervoor dat de virtuele machines die u binnen een Beschikbaarheidsset uitvoeren op meerdere fysieke servers plaatst, compute rekken eenheden voor opslag en netwerkswitches.</span><span class="sxs-lookup"><span data-stu-id="419db-116">Azure ensures that the VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="419db-117">Dit zorgt ervoor dat in het geval van een hardware- of Azure software fout slechts een subset van uw virtuele machines worden beïnvloed en uw algehele toepassing blijft en blijven beschikbaar voor uw klanten.</span><span class="sxs-lookup"><span data-stu-id="419db-117">This ensures that in the event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue to be available to your customers.</span></span> <span data-ttu-id="419db-118">Met behulp van Beschikbaarheidssets is een essentiële functie gebruiken als u wilt om betrouwbare cloudoplossingen te bouwen.</span><span class="sxs-lookup"><span data-stu-id="419db-118">Using Availability Sets is an essential capability to leverage when you want to build reliable cloud solutions.</span></span>

<span data-ttu-id="419db-119">Laten we eens een typische VM-oplossing op basis van waar u mogelijk 4 front-end-webservers en 2 back-end virtuele machines die een database te hosten.</span><span class="sxs-lookup"><span data-stu-id="419db-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="419db-120">Met Azure twee beschikbaarheidssets definiëren voordat u uw virtuele machines implementeert u zou willen: één beschikbaarheidsset voor de laag 'web' en een beschikbaarheidsset voor de laag 'database'.</span><span class="sxs-lookup"><span data-stu-id="419db-120">With Azure, you’d want to define two availability sets before you deploy your VMs: one availability set for the “web” tier and one availability set for the “database” tier.</span></span> <span data-ttu-id="419db-121">Bij het maken van een nieuwe virtuele machine vervolgens u kunt de beschikbaarheidsset als een parameter voor de vm az opdracht maken en Azure automatisch zorgt u dat de virtuele machines die u in de set beschikbaar maakt zijn geïsoleerd over meerdere fysieke hardware-resources.</span><span class="sxs-lookup"><span data-stu-id="419db-121">When you create a new VM you can then specify the availability set as a parameter to the az vm create command, and Azure will automatically ensure that the VMs you create within the available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="419db-122">Dit betekent dat als de fysieke hardware die een van uw webserver of VM's Database-Server wordt uitgevoerd op een probleem is, u kent dat de andere exemplaren van uw webserver en de Database virtuele machines actief probleemloos blijven wordt omdat ze op andere hardware.</span><span class="sxs-lookup"><span data-stu-id="419db-122">This means that if the physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that the other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="419db-123">U moet altijd Beschikbaarheidssets gebruiken wanneer u wilt implementeren, betrouwbare op basis van VM-oplossingen in Azure.</span><span class="sxs-lookup"><span data-stu-id="419db-123">You should always use Availability Sets when you want to deploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="419db-124">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="419db-124">Create an availability set</span></span>

<span data-ttu-id="419db-125">Kunt u een beschikbaarheidsset met [nieuw AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="419db-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="419db-126">In dit voorbeeld wordt zowel het aantal update en fouttolerantie domeinen op ingesteld *2* voor de beschikbaarheid van de set met de naam *myAvailabilitySet* in de *myResourceGroupAvailability* resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="419db-126">In this example, we set both the number of update and fault domains at *2* for the availability set named *myAvailabilitySet* in the *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="419db-127">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="419db-127">Create a resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="419db-128">Virtuele machines in een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="419db-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="419db-129">Virtuele machines moeten worden gemaakt binnen de beschikbaarheidsset om ervoor te zorgen dat ze correct zijn verdeeld over de hardware.</span><span class="sxs-lookup"><span data-stu-id="419db-129">VMs need to be created within the availability set to make sure they are correctly distributed across the hardware.</span></span> <span data-ttu-id="419db-130">U kunt een bestaande virtuele machine toevoegen aan een beschikbaarheidsset nadat deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="419db-130">You can't add an existing VM to an availability set after it is created.</span></span> 

<span data-ttu-id="419db-131">De hardware op een locatie is onderverdeeld meerdere domeinen van de update en domeinen met fouten.</span><span class="sxs-lookup"><span data-stu-id="419db-131">The hardware in a location is divided in to multiple update domains and fault domains.</span></span> <span data-ttu-id="419db-132">Een **updatedomein** is een groep VM's en de onderliggende fysieke hardware die op hetzelfde moment kan worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="419db-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="419db-133">Virtuele machines in dezelfde **foutdomein** algemene storage, evenals een gemeenschappelijk power-bron- en switch delen.</span><span class="sxs-lookup"><span data-stu-id="419db-133">VMs in the same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="419db-134">Wanneer u een virtuele machine met behulp van de configuratie maakt [nieuw AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) opgeven van de beschikbaarheidsset met behulp van de `-AvailabilitySetId` parameter om de ID van de beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="419db-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify the availability set using the `-AvailabilitySetId` parameter to specify the ID of the availability set.</span></span>

<span data-ttu-id="419db-135">Maken van 2 virtuele machines met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in de beschikbaarheid instellen.</span><span class="sxs-lookup"><span data-stu-id="419db-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in the availability set.</span></span>

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify the availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage `
        -VM $vm `
        -PublisherName MicrosoftWindowsServer `
        -Offer WindowsServer `
        -Skus 2016-Datacenter `
        -Version latest
   $vm = Set-AzureRmVMOSDisk `
        -VM $vm `
        -Name myOsDisk$i `
        -DiskSizeInGB 128 `
        -CreateOption FromImage `
        -Caching ReadWrite
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

<span data-ttu-id="419db-136">Het duurt enkele minuten maken en configureren van beide virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="419db-136">It takes a few minutes to create and configure both VMs.</span></span> <span data-ttu-id="419db-137">Wanneer u klaar bent, hebt u 2 virtuele machines die zijn verdeeld over de onderliggende hardware.</span><span class="sxs-lookup"><span data-stu-id="419db-137">When finished, you will have 2 virtual machines distributed across the underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="419db-138">Controleren op beschikbare VM-grootten</span><span class="sxs-lookup"><span data-stu-id="419db-138">Check for available VM sizes</span></span> 

<span data-ttu-id="419db-139">U kunt meer virtuele machines toevoegen aan de beschikbaarheid later instellen, maar u moet weten welke VM-grootten zijn beschikbaar op de hardware.</span><span class="sxs-lookup"><span data-stu-id="419db-139">You can add more VMs to the availability set later, but you need to know what VM sizes are available on the hardware.</span></span> <span data-ttu-id="419db-140">Gebruik [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) voor een lijst met alle van de beschikbare grootten van de hardware-cluster gebruikt voor de beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="419db-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) to list all the available sizes on the hardware cluster for the availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="419db-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="419db-141">Next steps</span></span>

<span data-ttu-id="419db-142">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="419db-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="419db-143">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="419db-143">Create an availability set</span></span>
> * <span data-ttu-id="419db-144">Een virtuele machine in een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="419db-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="419db-145">Controleer de beschikbare grootten voor virtuele machine</span><span class="sxs-lookup"><span data-stu-id="419db-145">Check available VM sizes</span></span>

<span data-ttu-id="419db-146">Ga naar de volgende zelfstudie voor meer informatie over virtuele-machineschaalsets.</span><span class="sxs-lookup"><span data-stu-id="419db-146">Advance to the next tutorial to learn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="419db-147">Een VM-schaalset maken</span><span class="sxs-lookup"><span data-stu-id="419db-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


