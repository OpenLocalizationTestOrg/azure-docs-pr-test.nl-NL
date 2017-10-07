---
title: aaaCreate en beheren van Windows-virtuele machines in Azure met meerdere NIC's | Microsoft Docs
description: Meer informatie over hoe toocreate en beheren van een Windows-VM met meerdere NIC's aangesloten tooit met behulp van Azure PowerShell of de Resource Manager-sjablonen.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="d72b9-103">Maken en beheren van een virtuele Windows-machine met meerdere NIC 's</span><span class="sxs-lookup"><span data-stu-id="d72b9-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="d72b9-104">Virtuele machines (VM's) in Azure, kunnen meerdere virtuele netwerk interface cards (NIC's) die zijn aangesloten toothem hebben.</span><span class="sxs-lookup"><span data-stu-id="d72b9-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached toothem.</span></span> <span data-ttu-id="d72b9-105">Een veelvoorkomend scenario toohave verschillende subnetten voor front-end en back-end-connectiviteit is of een netwerk toegewezen tooa bewaking of back-upoplossing.</span><span class="sxs-lookup"><span data-stu-id="d72b9-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="d72b9-106">Dit artikel wordt uitgelegd hoe een virtuele machine met meerdere NIC's toocreate tooit gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="d72b9-106">This article details how toocreate a VM that has multiple NICs attached tooit.</span></span> <span data-ttu-id="d72b9-107">U leert ook hoe tooadd of verwijder NIC's van een bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d72b9-107">You also learn how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="d72b9-108">Andere [VM-grootten](sizes.md) ondersteunen een verschillend aantal NIC's, dus het formaat van uw virtuele machine dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="d72b9-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="d72b9-109">Voor gedetailleerde informatie, inclusief hoe toocreate meerdere NIC's in uw eigen PowerShell-scripts, Zie [implementeren meerdere NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d72b9-109">For detailed information, including how toocreate multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d72b9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d72b9-110">Prerequisites</span></span>
<span data-ttu-id="d72b9-111">Zorg ervoor dat u Hallo hebt [meest recente versie van Azure PowerShell geïnstalleerd en geconfigureerd](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d72b9-111">Make sure that you have hello [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="d72b9-112">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="d72b9-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="d72b9-113">De namen van de voorbeeld-parameter *myResourceGroup*, *myVnet*, en *myVM*.</span><span class="sxs-lookup"><span data-stu-id="d72b9-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="d72b9-114">Een virtuele machine met meerdere NIC's maken</span><span class="sxs-lookup"><span data-stu-id="d72b9-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="d72b9-115">Maak eerst een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="d72b9-115">First, create a resource group.</span></span> <span data-ttu-id="d72b9-116">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *EastUs* locatie:</span><span class="sxs-lookup"><span data-stu-id="d72b9-116">hello following example creates a resource group named *myResourceGroup* in hello *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="d72b9-117">Virtueel netwerk en subnetten maken</span><span class="sxs-lookup"><span data-stu-id="d72b9-117">Create virtual network and subnets</span></span>
<span data-ttu-id="d72b9-118">Een gebruikelijk scenario is voor een virtueel netwerk toohave twee of meer subnetten.</span><span class="sxs-lookup"><span data-stu-id="d72b9-118">A common scenario is for a virtual network toohave two or more subnets.</span></span> <span data-ttu-id="d72b9-119">Eén subnet mogelijk voor front-verkeer, Hallo andere voor back-end-verkeer.</span><span class="sxs-lookup"><span data-stu-id="d72b9-119">One subnet may be for front-end traffic, hello other for back-end traffic.</span></span> <span data-ttu-id="d72b9-120">tooconnect tooboth subnetten wordt vervolgens gebruikt u meerdere NIC's op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d72b9-120">tooconnect tooboth subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="d72b9-121">Twee subnetten voor virtueel netwerk met definiëren [nieuw AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="d72b9-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="d72b9-122">Hallo volgende voorbeeld definieert Hallo subnetten voor *mySubnetFrontEnd* en *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="d72b9-122">hello following example defines hello subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="d72b9-123">Maken van uw virtuele netwerk en de subnetten met [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="d72b9-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="d72b9-124">Hallo volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="d72b9-124">hello following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="d72b9-125">Meerdere NIC's maken</span><span class="sxs-lookup"><span data-stu-id="d72b9-125">Create multiple NICs</span></span>
<span data-ttu-id="d72b9-126">Maak twee NIC's met [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="d72b9-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="d72b9-127">Koppel een NIC toohello front-end-subnet en één NIC toohello back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="d72b9-127">Attach one NIC toohello front-end subnet and one NIC toohello back-end subnet.</span></span> <span data-ttu-id="d72b9-128">Hallo volgende voorbeeld wordt gemaakt met de naam NIC's *myNic1* en *myNic2*:</span><span class="sxs-lookup"><span data-stu-id="d72b9-128">hello following example creates NICs named *myNic1* and *myNic2*:</span></span>

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

<span data-ttu-id="d72b9-129">Maakt u gewoonlijk ook een [netwerkbeveiligingsgroep](../../virtual-network/virtual-networks-nsg.md) of [netwerktaakverdeler](../../load-balancer/load-balancer-overview.md) toohelp beheren en distribueren van verkeer tussen uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="d72b9-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="d72b9-130">Hallo [meer gedetailleerde VM meerdere NIC](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) artikel begeleidt u bij het maken van een netwerkbeveiligingsgroep en NIC's toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d72b9-130">hello [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="d72b9-131">Hallo virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="d72b9-131">Create hello virtual machine</span></span>
<span data-ttu-id="d72b9-132">Nu starten toobuild uw VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="d72b9-132">Now start toobuild your VM configuration.</span></span> <span data-ttu-id="d72b9-133">Elk VM-grootte heeft een limiet voor Hallo kunt u het totale aantal NIC's die u tooa VM kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d72b9-133">Each VM size has a limit for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="d72b9-134">Zie voor meer informatie [Windows VM-grootten](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="d72b9-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="d72b9-135">Instellen van uw VM referenties toohello `$cred` variabele als volgt:</span><span class="sxs-lookup"><span data-stu-id="d72b9-135">Set your VM credentials toohello `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="d72b9-136">Definieer uw virtuele machine met [nieuwe AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span><span class="sxs-lookup"><span data-stu-id="d72b9-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="d72b9-137">Hallo volgende voorbeeld definieert een virtuele machine met de naam *myVM* en maakt gebruik van een VM-grootte die ondersteuning biedt voor meer dan twee NIC's (*Standard_DS3_v2*):</span><span class="sxs-lookup"><span data-stu-id="d72b9-137">hello following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="d72b9-138">Maken van de rest van de VM-configuratie met Hallo [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) en [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span><span class="sxs-lookup"><span data-stu-id="d72b9-138">Create hello rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="d72b9-139">Hallo volgende voorbeeld maakt een Windows Server 2016 VM:</span><span class="sxs-lookup"><span data-stu-id="d72b9-139">hello following example creates a Windows Server 2016 VM:</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. <span data-ttu-id="d72b9-140">Koppel Hallo twee NIC's die u eerder hebt gemaakt met [toevoegen AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="d72b9-140">Attach hello two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="d72b9-141">Maak ten slotte uw virtuele machine met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="d72b9-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a><span data-ttu-id="d72b9-142">Toevoegen van een NIC tooan bestaande VM</span><span class="sxs-lookup"><span data-stu-id="d72b9-142">Add a NIC tooan existing VM</span></span>
<span data-ttu-id="d72b9-143">toevoegen van een virtuele NIC tooan bestaande VM, dat Hallo VM ongedaan wordt gemaakt tooadd Hallo virtuele NIC en Hallo VM start.</span><span class="sxs-lookup"><span data-stu-id="d72b9-143">tooadd a virtual NIC tooan existing VM, you deallocate hello VM, add hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="d72b9-144">Toewijzing ongedaan maken met virtuele machine Hallo [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="d72b9-144">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="d72b9-145">Hallo volgende voorbeeld deallocates Hallo VM met de naam *myVM* in *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="d72b9-145">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="d72b9-146">De bestaande configuratie Hallo Hallo VM ophalen met [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="d72b9-146">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="d72b9-147">Hallo volgende voorbeeld worden gegevens opgehaald voor virtuele machine met de naam Hallo *myVM* in *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="d72b9-147">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="d72b9-148">Hallo volgende voorbeeld wordt een virtuele NIC met [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) met de naam *myNic3* die is gekoppeld te*mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="d72b9-148">hello following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached too*mySubnetBackEnd*.</span></span> <span data-ttu-id="d72b9-149">Hallo virtuele NIC is gekoppeld toohello VM met de naam *myVM* in *myResourceGroup* met [toevoegen AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="d72b9-149">hello virtual NIC is then attached toohello VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="d72b9-150">Primaire virtuele NIC 's</span><span class="sxs-lookup"><span data-stu-id="d72b9-150">Primary virtual NICs</span></span>
    <span data-ttu-id="d72b9-151">Moet één van Hallo NIC's op een VM meerdere NIC toobe primaire.</span><span class="sxs-lookup"><span data-stu-id="d72b9-151">One of hello NICs on a multi-NIC VM needs toobe primary.</span></span> <span data-ttu-id="d72b9-152">Als een van de bestaande virtuele NIC's Hallo Hallo VM is al ingesteld als primaire, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="d72b9-152">If one of hello existing virtual NICs on hello VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="d72b9-153">Hallo volgende voorbeeld wordt ervan uitgegaan dat twee virtuele NIC's nu aanwezig is op een virtuele machine zijn en u tooadd Hallo eerste NIC (`[0]`) als primaire Hallo:</span><span class="sxs-lookup"><span data-stu-id="d72b9-153">hello following example assumes that two virtual NICs are now present on a VM and you wish tooadd hello first NIC (`[0]`) as hello primary:</span></span>
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="d72b9-154">Start met virtuele machine Hallo [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="d72b9-154">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="d72b9-155">Een NIC van een bestaande virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="d72b9-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="d72b9-156">tooremove een virtuele NIC van een bestaande VM u Hallo VM ongedaan gemaakt, verwijdert u Hallo virtuele NIC en vervolgens start Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="d72b9-156">tooremove a virtual NIC from an existing VM, you deallocate hello VM, remove hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="d72b9-157">Toewijzing ongedaan maken met virtuele machine Hallo [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="d72b9-157">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="d72b9-158">Hallo volgende voorbeeld deallocates Hallo VM met de naam *myVM* in *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="d72b9-158">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="d72b9-159">De bestaande configuratie Hallo Hallo VM ophalen met [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="d72b9-159">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="d72b9-160">Hallo volgende voorbeeld worden gegevens opgehaald voor virtuele machine met de naam Hallo *myVM* in *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="d72b9-160">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="d72b9-161">Informatie ophalen over Hallo NIC verwijderen met [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="d72b9-161">Get information about hello NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="d72b9-162">Hallo volgende voorbeeld worden gegevens opgehaald over *myNic3*:</span><span class="sxs-lookup"><span data-stu-id="d72b9-162">hello following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="d72b9-163">Verwijder Hallo NIC met [verwijderen AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) en vervolgens update Hallo VM met [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="d72b9-163">Remove hello NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update hello VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="d72b9-164">Hallo volgende voorbeeld wordt verwijderd *myNic3* verkregen met `$nicId` in de voorgaande stap Hallo:</span><span class="sxs-lookup"><span data-stu-id="d72b9-164">hello following example removes *myNic3* as obtained by `$nicId` in hello preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="d72b9-165">Start met virtuele machine Hallo [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="d72b9-165">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="d72b9-166">Meerdere NIC's met behulp van sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="d72b9-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="d72b9-167">Azure Resource Manager-sjablonen bieden een manier toocreate meerdere exemplaren van een bron tijdens implementatie, zoals meerdere NIC's maken.</span><span class="sxs-lookup"><span data-stu-id="d72b9-167">Azure Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="d72b9-168">Resource Manager-sjablonen gebruiken declaratieve JSON-bestanden toodefine uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="d72b9-168">Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="d72b9-169">Zie voor meer informatie [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d72b9-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="d72b9-170">U kunt *kopie* toospecify Hallo aantal exemplaren toocreate:</span><span class="sxs-lookup"><span data-stu-id="d72b9-170">You can use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="d72b9-171">Zie voor meer informatie [maken van meerdere exemplaren met *kopie*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="d72b9-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="d72b9-172">U kunt ook `copyIndex()` tooappend de naam van een aantal tooa-resource.</span><span class="sxs-lookup"><span data-stu-id="d72b9-172">You can also use `copyIndex()` tooappend a number tooa resource name.</span></span> <span data-ttu-id="d72b9-173">Vervolgens kunt u maken *myNic1*, *MyNic2* enzovoort.</span><span class="sxs-lookup"><span data-stu-id="d72b9-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="d72b9-174">Hallo toont volgende code een voorbeeld van een indexwaarde Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="d72b9-174">hello following code shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="d72b9-175">U kunt een compleet voorbeeld van lezen [meerdere NIC's maken met Resource Manager-sjablonen](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="d72b9-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d72b9-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d72b9-176">Next steps</span></span>
<span data-ttu-id="d72b9-177">Bekijk [Windows VM-grootten](sizes.md) wanneer u probeert een virtuele machine met meerdere NIC's toocreate.</span><span class="sxs-lookup"><span data-stu-id="d72b9-177">Review [Windows VM sizes](sizes.md) when you're trying toocreate a VM that has multiple NICs.</span></span> <span data-ttu-id="d72b9-178">Betalen aandacht toohello maximum aantal NIC's die ondersteuning biedt voor elke VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="d72b9-178">Pay attention toohello maximum number of NICs that each VM size supports.</span></span> 


