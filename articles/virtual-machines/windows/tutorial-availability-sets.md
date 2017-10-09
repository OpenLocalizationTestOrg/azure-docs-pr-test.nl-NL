---
title: aaaAvailability zelfstudie ingesteld voor Windows-machines in Azure | Microsoft Docs
description: Meer informatie over Hallo beschikbaarheid Sets voor Windows-machines in Azure.
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
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="1a4db-103">Hoe toouse beschikbaarheidssets</span><span class="sxs-lookup"><span data-stu-id="1a4db-103">How toouse availability sets</span></span>

<span data-ttu-id="1a4db-104">In deze zelfstudie leert u hoe tooincrease Hallo beschikbaarheid en betrouwbaarheid van uw virtuele Machine-oplossingen in Azure met een mogelijkheid Beschikbaarheidssets aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1a4db-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="1a4db-105">Beschikbaarheidssets Zorg ervoor dat u implementeert op Azure VM's zijn verdeeld over meerdere geïsoleerde hardware clusters Hallo.</span><span class="sxs-lookup"><span data-stu-id="1a4db-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="1a4db-106">Dit zorgt ervoor dat als een storing hardware of software in Azure gebeurt, van invloed op een onderliggende reeks uw virtuele machines die uw algehele oplossing blijft beschikbaar en operationele vanuit het oogpunt van uw klanten die gebruikmaken van het Hallo van.</span><span class="sxs-lookup"><span data-stu-id="1a4db-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span> 

<span data-ttu-id="1a4db-107">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="1a4db-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1a4db-108">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="1a4db-108">Create an availability set</span></span>
> * <span data-ttu-id="1a4db-109">Een virtuele machine in een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="1a4db-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="1a4db-110">Controleer de beschikbare grootten voor virtuele machine</span><span class="sxs-lookup"><span data-stu-id="1a4db-110">Check available VM sizes</span></span>

<span data-ttu-id="1a4db-111">Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="1a4db-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="1a4db-112">Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="1a4db-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="1a4db-113">Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="1a4db-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="1a4db-114">Overzicht van de beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="1a4db-114">Availability set overview</span></span>

<span data-ttu-id="1a4db-115">Een Beschikbaarheidsset, is een logische groepering-functie die u kunt gebruiken in Azure tooensure dat Hallo VM resources die u in het plaatsen van elkaar geïsoleerd zijn wanneer ze zijn geïmplementeerd in een Azure-datacenter.</span><span class="sxs-lookup"><span data-stu-id="1a4db-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="1a4db-116">Azure zorgt ervoor dat Hallo virtuele machines die u binnen een Beschikbaarheidsset uitvoeren op meerdere fysieke servers plaatst, compute rekken eenheden voor opslag en netwerkswitches.</span><span class="sxs-lookup"><span data-stu-id="1a4db-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="1a4db-117">Dit zorgt ervoor dat in geval van een softwarestoring van de Azure-of hardware Hallo slechts een subset van uw virtuele machines worden beïnvloed en uw algehele toepassing blijft en doorgaan toobe beschikbaar tooyour klanten.</span><span class="sxs-lookup"><span data-stu-id="1a4db-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="1a4db-118">Gebruik Beschikbaarheidssets is een tooleverage essentiële mogelijkheden als u wilt dat toobuild betrouwbare cloudoplossingen.</span><span class="sxs-lookup"><span data-stu-id="1a4db-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="1a4db-119">Laten we eens een typische VM-oplossing op basis van waar u mogelijk 4 front-end-webservers en 2 back-end virtuele machines die een database te hosten.</span><span class="sxs-lookup"><span data-stu-id="1a4db-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="1a4db-120">Met Azure, kunt u twee beschikbaarheidssets toodefine voordat u uw virtuele machines implementeren: één beschikbaarheid instellen voor Hallo 'web' laag en een beschikbaarheidsset voor Hallo 'database' laag.</span><span class="sxs-lookup"><span data-stu-id="1a4db-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="1a4db-121">Bij het maken van een nieuwe virtuele machine vervolgens u Hallo beschikbaarheid instellen opgeven kunt als een parameter toohello az vm-opdracht maken en Azure zorgt u dat Hallo virtuele machines die u binnen Hallo beschikbaar maken automatisch worden ingesteld op de resources van meerdere fysieke hardware geïsoleerd.</span><span class="sxs-lookup"><span data-stu-id="1a4db-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="1a4db-122">Dit betekent dat als Hallo fysieke hardware die een van uw webserver of VM's Database-Server wordt uitgevoerd op een probleem, u dat Hallo weet andere exemplaren van uw webserver en de Database virtuele machines blijven actief probleemloos omdat ze op andere hardware.</span><span class="sxs-lookup"><span data-stu-id="1a4db-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="1a4db-123">Als u wilt dat toodeploy betrouwbare VM op basis van oplossingen in Azure, moet u altijd Beschikbaarheidssets gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1a4db-123">You should always use Availability Sets when you want toodeploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="1a4db-124">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="1a4db-124">Create an availability set</span></span>

<span data-ttu-id="1a4db-125">Kunt u een beschikbaarheidsset met [nieuw AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="1a4db-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="1a4db-126">In dit voorbeeld we beide Hallo aantal update en fouttolerantie domeinen op instellen *2* voor Hallo beschikbaarheidsset benoemde *myAvailabilitySet* in Hallo *myResourceGroupAvailability*resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="1a4db-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="1a4db-127">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="1a4db-127">Create a resource group.</span></span>

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

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="1a4db-128">Virtuele machines in een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="1a4db-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="1a4db-129">Virtuele machines moeten toobe in Hallo beschikbaarheid set toomake zeker van te zijn dat ze correct zijn verdeeld over Hallo hardware hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1a4db-129">VMs need toobe created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="1a4db-130">U kunt een bestaande VM tooan beschikbaarheidsset nadat deze is gemaakt niet toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1a4db-130">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="1a4db-131">Hallo hardware op een locatie is onderverdeeld in toomultiple update domeinen en domeinen met fouten.</span><span class="sxs-lookup"><span data-stu-id="1a4db-131">hello hardware in a location is divided in toomultiple update domains and fault domains.</span></span> <span data-ttu-id="1a4db-132">Een **updatedomein** is een groep VM's en de onderliggende fysieke hardware die kan worden opgestart op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="1a4db-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="1a4db-133">Virtuele machines in dezelfde Hallo **foutdomein** algemene storage, evenals een gemeenschappelijk power-bron- en switch delen.</span><span class="sxs-lookup"><span data-stu-id="1a4db-133">VMs in hello same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="1a4db-134">Wanneer u een virtuele machine met behulp van de configuratie maakt [nieuw AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) u Hallo beschikbaarheid instellen met behulp van Hallo opgeven `-AvailabilitySetId` toospecify Hallo-ID van weergaveparameter van Hallo beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="1a4db-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify hello availability set using hello `-AvailabilitySetId` parameter toospecify hello ID of hello availability set.</span></span>

<span data-ttu-id="1a4db-135">Maken van 2 virtuele machines met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in Hallo beschikbaarheid instellen.</span><span class="sxs-lookup"><span data-stu-id="1a4db-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in hello availability set.</span></span>

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

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

   # Here is where we specify hello availability set
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

<span data-ttu-id="1a4db-136">Het duurt enkele minuten toocreate en beide VM's configureren.</span><span class="sxs-lookup"><span data-stu-id="1a4db-136">It takes a few minutes toocreate and configure both VMs.</span></span> <span data-ttu-id="1a4db-137">Wanneer u klaar bent, hebt u 2 virtuele machines die zijn verdeeld over de onderliggende hardware Hallo.</span><span class="sxs-lookup"><span data-stu-id="1a4db-137">When finished, you will have 2 virtual machines distributed across hello underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="1a4db-138">Controleren op beschikbare VM-grootten</span><span class="sxs-lookup"><span data-stu-id="1a4db-138">Check for available VM sizes</span></span> 

<span data-ttu-id="1a4db-139">U kunt meer virtuele machines toohello beschikbaarheidsset later toevoegen, maar u moet tooknow welke VM-grootten zijn beschikbaar op Hallo hardware.</span><span class="sxs-lookup"><span data-stu-id="1a4db-139">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="1a4db-140">Gebruik [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist alle beschikbare grootten van Hallo op Hallo hardware-cluster voor Hallo beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="1a4db-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="1a4db-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1a4db-141">Next steps</span></span>

<span data-ttu-id="1a4db-142">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="1a4db-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1a4db-143">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="1a4db-143">Create an availability set</span></span>
> * <span data-ttu-id="1a4db-144">Een virtuele machine in een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="1a4db-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="1a4db-145">Controleer de beschikbare grootten voor virtuele machine</span><span class="sxs-lookup"><span data-stu-id="1a4db-145">Check available VM sizes</span></span>

<span data-ttu-id="1a4db-146">Toohello volgende zelfstudie toolearn over virtuele-machineschaalsets gaan.</span><span class="sxs-lookup"><span data-stu-id="1a4db-146">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1a4db-147">Een VM-schaalset maken</span><span class="sxs-lookup"><span data-stu-id="1a4db-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


