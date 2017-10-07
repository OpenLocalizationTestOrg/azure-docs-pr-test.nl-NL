---
title: aaaCreate VM vanaf een beheerde VM-installatiekopie in Azure | Microsoft Docs
description: Een virtuele Windows-machine maken van een algemene beheerde VM installatiekopie met behulp van Azure PowerShell Hallo Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
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
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a><span data-ttu-id="9e963-103">Een virtuele machine maken van een begeleide afbeelding</span><span class="sxs-lookup"><span data-stu-id="9e963-103">Create a VM from a managed image</span></span>

<span data-ttu-id="9e963-104">U kunt meerdere virtuele machines maken in een beheerde VM-installatiekopie in Azure.</span><span class="sxs-lookup"><span data-stu-id="9e963-104">You can create multiple VMs from a managed VM image in Azure.</span></span> <span data-ttu-id="9e963-105">Een beheerde VM-installatiekopie bevat Hallo informatie een virtuele machine, met inbegrip van het besturingssysteem en gegevensschijven Hallo toocreate nodig.</span><span class="sxs-lookup"><span data-stu-id="9e963-105">A managed VM image contains hello information necessary toocreate a VM, including hello OS and data disks.</span></span> <span data-ttu-id="9e963-106">Hallo virtuele harde schijven die gezamenlijk Hallo afbeelding, inclusief zowel Hallo OS-schijven en eventuele gegevensschijven, als beheerde schijven zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="9e963-106">hello VHDs that make up hello image, including both hello OS disks and any data disks, are stored as managed disks.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="9e963-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9e963-107">Prerequisites</span></span>

<span data-ttu-id="9e963-108">Moet u toohave al [gemaakt van een beheerde VM-installatiekopie](capture-image-resource.md) toouse voor het maken van nieuwe virtuele machine Hallo.</span><span class="sxs-lookup"><span data-stu-id="9e963-108">You need toohave already [created a managed VM image](capture-image-resource.md) toouse for creating hello new VM.</span></span> 

<span data-ttu-id="9e963-109">Zorg ervoor dat u beschikt over de nieuwste versies Hallo Hallo AzureRM.Compute en AzureRM.Network PowerShell-modules.</span><span class="sxs-lookup"><span data-stu-id="9e963-109">Make sure that you have hello latest versions of hello AzureRM.Compute and AzureRM.Network PowerShell modules.</span></span> <span data-ttu-id="9e963-110">Open een PowerShell een opdrachtprompt als beheerder en Voer Hallo opdracht tooinstall na deze.</span><span class="sxs-lookup"><span data-stu-id="9e963-110">Open a PowerShell prompt as an Administrator and run hello following command tooinstall them.</span></span>

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
<span data-ttu-id="9e963-111">Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9e963-111">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>



## <a name="collect-information-about-hello-image"></a><span data-ttu-id="9e963-112">Informatie over de installatiekopie Hallo verzamelen</span><span class="sxs-lookup"><span data-stu-id="9e963-112">Collect information about hello image</span></span>

<span data-ttu-id="9e963-113">Eerst we moet toogather basisinformatie over de installatiekopie van het Hallo en een variabele voor de installatiekopie van het Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="9e963-113">First we need toogather basic information about hello image and create a variable for hello image.</span></span> <span data-ttu-id="9e963-114">In dit voorbeeld wordt een beheerde VM-installatiekopie met de naam **myImage** die in Hallo **myResourceGroup** resourcegroep in Hallo **West-Centraal VS** locatie.</span><span class="sxs-lookup"><span data-stu-id="9e963-114">This example uses a managed VM image named **myImage** that is in hello **myResourceGroup** resource group in hello **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="9e963-115">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="9e963-115">Create a virtual network</span></span>
<span data-ttu-id="9e963-116">Hallo vNet en subnet Hallo maken [virtueel netwerk](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e963-116">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="9e963-117">Hallo subnet maken.</span><span class="sxs-lookup"><span data-stu-id="9e963-117">Create hello subnet.</span></span> <span data-ttu-id="9e963-118">In dit voorbeeld wordt een subnet met de naam **mySubnet** met het Hallo-adresvoorvoegsel van **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="9e963-118">This example creates a subnet named **mySubnet** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="9e963-119">Hallo virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="9e963-119">Create hello virtual network.</span></span> <span data-ttu-id="9e963-120">In dit voorbeeld wordt een virtueel netwerk met de naam **myVnet** met het Hallo-adresvoorvoegsel van **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="9e963-120">This example creates a virtual network named **myVnet** with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="9e963-121">Een openbaar IP-adres en een netwerkinterface maken</span><span class="sxs-lookup"><span data-stu-id="9e963-121">Create a public IP address and network interface</span></span>

<span data-ttu-id="9e963-122">tooenable communicatie met Hallo virtuele machine in het virtuele netwerk hello, moet u een [openbaar IP-adres](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) en een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="9e963-122">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="9e963-123">Een openbaar IP-adres maken.</span><span class="sxs-lookup"><span data-stu-id="9e963-123">Create a public IP address.</span></span> <span data-ttu-id="9e963-124">In dit voorbeeld wordt een openbaar IP-adres met de naam **myPip**.</span><span class="sxs-lookup"><span data-stu-id="9e963-124">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="9e963-125">Hallo NIC. maken</span><span class="sxs-lookup"><span data-stu-id="9e963-125">Create hello NIC.</span></span> <span data-ttu-id="9e963-126">In dit voorbeeld wordt een NIC met de naam **myNic**.</span><span class="sxs-lookup"><span data-stu-id="9e963-126">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="9e963-127">Netwerkbeveiligingsgroep hello en een RDP-regel maken</span><span class="sxs-lookup"><span data-stu-id="9e963-127">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="9e963-128">toobe kunnen toolog in tooyour VM met RDP, moet u toohave een netwerkbeveiligingsregel (NSG) waarmee op poort 3389 van RDP-toegang.</span><span class="sxs-lookup"><span data-stu-id="9e963-128">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="9e963-129">In dit voorbeeld maakt u een NSG met de naam **myNsg** die een regel aangeroepen bevat **myRdpRule** waarmee RDP-verkeer via poort 3389.</span><span class="sxs-lookup"><span data-stu-id="9e963-129">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="9e963-130">Zie voor meer informatie over Nsg [openen van poorten tooa VM in Azure met behulp van PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e963-130">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="9e963-131">Een variabele voor Hallo virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="9e963-131">Create a variable for hello virtual network</span></span>

<span data-ttu-id="9e963-132">Maak een variabele voor het virtuele netwerk Hallo voltooid.</span><span class="sxs-lookup"><span data-stu-id="9e963-132">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="9e963-133">Hallo-referenties voor Hallo VM ophalen</span><span class="sxs-lookup"><span data-stu-id="9e963-133">Get hello credentials for hello VM</span></span>

<span data-ttu-id="9e963-134">Hallo wordt volgende cmdlet een venster geopend waarin u een nieuwe gebruiker-naam en het wachtwoord toouse Hallo lokale administrator-account wordt invoeren voor toegang op afstand tot Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="9e963-134">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a><span data-ttu-id="9e963-135">Set variabelen voor Hallo VM naam, computernaam en grootte van Hallo VM Hallo</span><span class="sxs-lookup"><span data-stu-id="9e963-135">Set variables for hello VM name, computer name and hello size of hello VM</span></span>

1. <span data-ttu-id="9e963-136">Variabelen voor Hallo VM-naam en de naam van computer maken.</span><span class="sxs-lookup"><span data-stu-id="9e963-136">Create variables for hello VM name and computer name.</span></span> <span data-ttu-id="9e963-137">Dit voorbeeld wordt Hallo VM-naam als **myVM** en Hallo-computernaam als **computer**.</span><span class="sxs-lookup"><span data-stu-id="9e963-137">This example sets hello VM name as **myVM** and hello computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="9e963-138">Hallo-grootte van Hallo virtuele machine instellen.</span><span class="sxs-lookup"><span data-stu-id="9e963-138">Set hello size of hello virtual machine.</span></span> <span data-ttu-id="9e963-139">In dit voorbeeld maakt **Standard_DS1_v2** grootte van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9e963-139">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="9e963-140">Zie Hallo [VM-grootten](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentatie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9e963-140">See hello [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="9e963-141">Hallo VM-naam en de grootte van toohello VM-configuratie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9e963-141">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="9e963-142">Set Hallo VM-installatiekopie als bronafbeelding voor Hallo nieuwe virtuele machine</span><span class="sxs-lookup"><span data-stu-id="9e963-142">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="9e963-143">Stel broninstallatiekopie Hallo Hallo-id van VM-installatiekopie Hallo beheerd.</span><span class="sxs-lookup"><span data-stu-id="9e963-143">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="9e963-144">Configuratie van het besturingssysteem Hallo en toevoegen van Hallo NIC.</span><span class="sxs-lookup"><span data-stu-id="9e963-144">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="9e963-145">Hallo opslagtype (PremiumLRS of StandardLRS) en het Hallo-grootte van de besturingssysteemschijf Hallo invoeren.</span><span class="sxs-lookup"><span data-stu-id="9e963-145">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="9e963-146">In dit voorbeeld wordt het accounttype hello te**PremiumLRS**, schijfgrootte te Hallo**128 GB** en schijfcache te**ReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="9e963-146">This example sets hello account type too**PremiumLRS**, hello disk size too**128 GB** and disk caching too**ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="9e963-147">Hallo VM maken</span><span class="sxs-lookup"><span data-stu-id="9e963-147">Create hello VM</span></span>

<span data-ttu-id="9e963-148">Maken van nieuwe virtuele machine met behulp van Hallo-configuratie die we hebben gemaakt en opgeslagen in Hallo Hallo **$vm** variabele.</span><span class="sxs-lookup"><span data-stu-id="9e963-148">Create hello new Vm using hello configuration that we have built and stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="9e963-149">Controleer of deze Hallo die VM is gemaakt</span><span class="sxs-lookup"><span data-stu-id="9e963-149">Verify that hello VM was created</span></span>
<span data-ttu-id="9e963-150">Wanneer voltooid, ziet u VM nieuw wordt gemaakt in Hallo Hallo [Azure-portal](https://portal.azure.com) onder **Bladeren** > **virtuele machines**, of met behulp van de volgende Hallo PowerShell-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="9e963-150">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="9e963-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9e963-151">Next steps</span></span>
<span data-ttu-id="9e963-152">toomanage uw nieuwe virtuele machine met Azure PowerShell, Zie [maken en beheren van Windows-VM's met Azure PowerShell-module Hallo](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e963-152">toomanage your new virtual machine with Azure PowerShell, see [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

