---
title: aaaCreate en Windows virtuele machines beheren met Azure PowerShell-module Hallo | Microsoft Docs
description: Zelfstudie - maken en beheren van Windows virtuele machines met hello Azure PowerShell-module
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a><span data-ttu-id="1686d-103">Maken en beheren van Windows virtuele machines met hello Azure PowerShell-module</span><span class="sxs-lookup"><span data-stu-id="1686d-103">Create and Manage Windows VMs with hello Azure PowerShell module</span></span>

<span data-ttu-id="1686d-104">Virtuele machines van Azure bieden een volledig worden geconfigureerd en flexibele computeromgeving.</span><span class="sxs-lookup"><span data-stu-id="1686d-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="1686d-105">Deze zelfstudie bevat informatie over basic virtuele machine van Azure-implementatie items zoals het selecteren van een VM-grootte, een VM-installatiekopie te selecteren en implementeren van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1686d-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="1686d-106">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="1686d-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1686d-107">Maken en koppelen tooa VM</span><span class="sxs-lookup"><span data-stu-id="1686d-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="1686d-108">Selecteer en gebruik van VM-installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="1686d-108">Select and use VM images</span></span>
> * <span data-ttu-id="1686d-109">Weergeven en gebruiken van specifieke VM-grootten</span><span class="sxs-lookup"><span data-stu-id="1686d-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="1686d-110">De grootte van een virtuele machine wijzigen</span><span class="sxs-lookup"><span data-stu-id="1686d-110">Resize a VM</span></span>
> * <span data-ttu-id="1686d-111">Bekijken en te begrijpen status virtuele machine</span><span class="sxs-lookup"><span data-stu-id="1686d-111">View and understand VM state</span></span>

<span data-ttu-id="1686d-112">Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="1686d-112">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="1686d-113">Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="1686d-113">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="1686d-114">Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="1686d-114">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="1686d-115">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="1686d-115">Create resource group</span></span>

<span data-ttu-id="1686d-116">Een resourcegroep maken met de Hallo [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1686d-116">Create a resource group with hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> 

<span data-ttu-id="1686d-117">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="1686d-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="1686d-118">Een resourcegroep moet worden gemaakt voordat een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1686d-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="1686d-119">In dit voorbeeld wordt een resourcegroep met de naam *myResourceGroupVM* wordt gemaakt in Hallo *EastUS* regio.</span><span class="sxs-lookup"><span data-stu-id="1686d-119">In this example, a resource group named *myResourceGroupVM* is created in hello *EastUS* region.</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

<span data-ttu-id="1686d-120">Hallo-resourcegroep is opgegeven bij het maken of wijzigen van een virtuele machine die in deze zelfstudie kan worden gezien.</span><span class="sxs-lookup"><span data-stu-id="1686d-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="1686d-121">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="1686d-121">Create virtual machine</span></span>

<span data-ttu-id="1686d-122">Een virtuele machine moet worden verbonden tooa virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="1686d-122">A virtual machine must be connected tooa virtual network.</span></span> <span data-ttu-id="1686d-123">U communiceren met de Hallo virtuele machine via een openbaar IP-adres via een netwerkinterfacekaart.</span><span class="sxs-lookup"><span data-stu-id="1686d-123">You communicate with hello virtual machine using a public IP address through a network interface card.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="1686d-124">Virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="1686d-124">Create virtual network</span></span>

<span data-ttu-id="1686d-125">Maak een subnet met [nieuw AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="1686d-125">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="1686d-126">Maak een virtueel netwerk met [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="1686d-126">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a><span data-ttu-id="1686d-127">Openbare IP-adres maken</span><span class="sxs-lookup"><span data-stu-id="1686d-127">Create public IP address</span></span>

<span data-ttu-id="1686d-128">Maken van een openbaar IP-adres met [nieuw AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="1686d-128">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a><span data-ttu-id="1686d-129">Maken van netwerkinterfacekaart</span><span class="sxs-lookup"><span data-stu-id="1686d-129">Create network interface card</span></span>

<span data-ttu-id="1686d-130">Maken van een netwerkkaart met [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="1686d-130">Create a network interface card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a><span data-ttu-id="1686d-131">Netwerkbeveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="1686d-131">Create network security group</span></span>

<span data-ttu-id="1686d-132">Een Azure [netwerkbeveiligingsgroep](../../virtual-network/virtual-networks-nsg.md) (NSG) Hiermee wordt bepaald binnenkomend en uitgaand verkeer voor een of meer virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1686d-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="1686d-133">Netwerkbeveiligingsgroepen toestaan of weigeren van netwerkverkeer op een specifieke poort of een poortbereik.</span><span class="sxs-lookup"><span data-stu-id="1686d-133">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="1686d-134">Deze regels kunnen ook een voorvoegsel voor bronadres bevatten, zodat alleen verkeer dat afkomstig is op een vooraf gedefinieerde bron met een virtuele machine communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="1686d-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span> <span data-ttu-id="1686d-135">tooaccess hello IIS webserver die u installeert, moet u een inkomende NSG-regel toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1686d-135">tooaccess hello IIS webserver that you are installing, you must add an inbound NSG rule.</span></span>

<span data-ttu-id="1686d-136">gebruik van een inkomende regel voor het NSG toocreate [toevoegen AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="1686d-136">toocreate an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="1686d-137">Hallo volgende voorbeeld maakt u een NSG regel voor licentiecontrole *myNSGRule* opent die poort *3389* voor Hallo virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="1686d-137">hello following example creates an NSG rule named *myNSGRule* that opens port *3389* for hello virtual machine:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

<span data-ttu-id="1686d-138">Maak Hallo NSG met *myNSGRule* met [nieuw AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="1686d-138">Create hello NSG using *myNSGRule* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

<span data-ttu-id="1686d-139">Hallo NSG toohello subnet toevoegen in virtueel netwerk met Hallo [Set AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="1686d-139">Add hello NSG toohello subnet in hello virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="1686d-140">Update Hallo virtueel netwerk met [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="1686d-140">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a><span data-ttu-id="1686d-141">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="1686d-141">Create virtual machine</span></span>

<span data-ttu-id="1686d-142">Wanneer u een virtuele machine maakt, er zijn diverse opties beschikbaar zoals besturingssysteemkopie schijf sizing en administratieve referenties.</span><span class="sxs-lookup"><span data-stu-id="1686d-142">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="1686d-143">In dit voorbeeld wordt een virtuele machine gemaakt met de naam *myVM* Hallo meest recente versie van Windows Server 2016 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="1686d-143">In this example, a virtual machine is created with a name of *myVM* running hello latest version of Windows Server 2016 Datacenter.</span></span>

<span data-ttu-id="1686d-144">Stel Hallo-gebruikersnaam en wachtwoord nodig voor Hallo-beheerdersaccount op Hallo virtuele machine met [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="1686d-144">Set hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="1686d-145">Hallo initiële configuratie maken voor Hallo virtuele machine met [nieuw AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span><span class="sxs-lookup"><span data-stu-id="1686d-145">Create hello initial configuration for hello virtual machine with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="1686d-146">Toevoegen van Hallo besturingssysteem informatie toohello Virtuele-machineconfiguratie met [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span><span class="sxs-lookup"><span data-stu-id="1686d-146">Add hello operating system information toohello virtual machine configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span></span>

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="1686d-147">Toevoegen van Hallo installatiekopie informatie toohello Virtuele-machineconfiguratie met [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span><span class="sxs-lookup"><span data-stu-id="1686d-147">Add hello image information toohello virtual machine configuration with [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

<span data-ttu-id="1686d-148">Toevoegen van Hallo besturingssysteem schijf instellingen toohello Virtuele-machineconfiguratie met [Set AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span><span class="sxs-lookup"><span data-stu-id="1686d-148">Add hello operating system disk settings toohello virtual machine configuration with [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

<span data-ttu-id="1686d-149">Add Hallo-netwerkinterfacekaart die u eerder hebt gemaakt toohello Virtuele-machineconfiguratie met [toevoegen AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="1686d-149">Add hello network interface card that you previously created toohello virtual machine configuration with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="1686d-150">Maak Hallo virtuele machine met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="1686d-150">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a><span data-ttu-id="1686d-151">Verbinding maken met tooVM</span><span class="sxs-lookup"><span data-stu-id="1686d-151">Connect tooVM</span></span>

<span data-ttu-id="1686d-152">Nadat het Hallo-implementatie is voltooid, maakt u een verbinding met extern bureaublad met Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1686d-152">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="1686d-153">Hallo volgende opdrachten tooreturn Hallo openbare IP-adres van Hallo virtuele machine worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1686d-153">Run hello following commands tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="1686d-154">Noteer dit IP-adres zodat tooit verbinding met uw browser tootest webverbindingen mogelijk in een toekomstige stap maken kunnen.</span><span class="sxs-lookup"><span data-stu-id="1686d-154">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

<span data-ttu-id="1686d-155">Gebruik Hallo volgende opdracht toocreate een extern-bureaubladsessie met Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1686d-155">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="1686d-156">Hallo IP-adres vervangen door Hallo *publicIPAddress* van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1686d-156">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="1686d-157">Wanneer u wordt gevraagd, voert u Hallo-referenties gebruikt bij het maken van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1686d-157">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a><span data-ttu-id="1686d-158">VM-installatiekopieën begrijpen</span><span class="sxs-lookup"><span data-stu-id="1686d-158">Understand VM images</span></span>

<span data-ttu-id="1686d-159">Hello Azure marketplace bevat veel installatiekopieën van virtuele machines die gebruikt toocreate een nieuwe virtuele machine worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="1686d-159">hello Azure marketplace includes many virtual machine images that can be used toocreate a new virtual machine.</span></span> <span data-ttu-id="1686d-160">In de vorige stappen hello, is een virtuele machine gemaakt met installatiekopie van Windows Server 2016-Datacenter Hallo.</span><span class="sxs-lookup"><span data-stu-id="1686d-160">In hello previous steps, a virtual machine was created using hello Windows Server 2016-Datacenter image.</span></span> <span data-ttu-id="1686d-161">In deze stap is Hallo PowerShell-module gebruikte toosearch Hallo marketplace voor andere Windows-installatiekopieën ook als basis voor de nieuwe virtuele machines kunnen.</span><span class="sxs-lookup"><span data-stu-id="1686d-161">In this step, hello PowerShell module is used toosearch hello marketplace for other Windows images, which can also as a base for new VMs.</span></span> <span data-ttu-id="1686d-162">Dit proces bestaat uit het Hallo-uitgever, aanbieding en Hallo installatiekopie met de naam (Sku) te zoeken.</span><span class="sxs-lookup"><span data-stu-id="1686d-162">This process consists of finding hello publisher, offer, and hello image name (Sku).</span></span> 

<span data-ttu-id="1686d-163">Gebruik Hallo [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) opdracht tooreturn een lijst van uitgevers van de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="1686d-163">Use hello [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command tooreturn a list of image publishers.</span></span>  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

<span data-ttu-id="1686d-164">Gebruik Hallo [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn een lijst met aanbiedingen van de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="1686d-164">Use hello [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn a list of image offers.</span></span> <span data-ttu-id="1686d-165">Met deze opdracht Hallo geretourneerd lijst wordt gefilterd op Hallo opgegeven uitgever.</span><span class="sxs-lookup"><span data-stu-id="1686d-165">With this command, hello returned list is filtered on hello specified publisher.</span></span> 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

<span data-ttu-id="1686d-166">Hallo [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) opdracht wordt vervolgens filteren op Hallo publisher en de aanbieding naam tooreturn een lijst met namen van afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="1686d-166">hello [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) command will then filter on hello publisher and offer name tooreturn a list of image names.</span></span>

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

<span data-ttu-id="1686d-167">Deze informatie kan worden gebruikt toodeploy een virtuele machine met een specifieke installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="1686d-167">This information can be used toodeploy a VM with a specific image.</span></span> <span data-ttu-id="1686d-168">In het volgende voorbeeld wordt de naam van de installatiekopie Hallo op Hallo VM-object.</span><span class="sxs-lookup"><span data-stu-id="1686d-168">This example sets hello image name on hello VM object.</span></span> <span data-ttu-id="1686d-169">Raadpleeg de eerdere voorbeelden toohello in deze zelfstudie voor volledige implementatiestappen.</span><span class="sxs-lookup"><span data-stu-id="1686d-169">Refer toohello previous examples in this tutorial for complete deployment steps.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="1686d-170">VM-grootten begrijpen</span><span class="sxs-lookup"><span data-stu-id="1686d-170">Understand VM sizes</span></span>

<span data-ttu-id="1686d-171">De grootte van een virtuele machine bepaalt Hallo hoeveelheid rekenresources zoals CPU en GPU geheugen die beschikbaar toohello virtuele machine zijn aangebracht.</span><span class="sxs-lookup"><span data-stu-id="1686d-171">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="1686d-172">Toobe gemaakt met een grootte geschikt voor Hallo werkbelasting verwacht, moeten virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1686d-172">Virtual machines need toobe created with a size appropriate for hello expect work load.</span></span> <span data-ttu-id="1686d-173">Als de werkbelasting toeneemt, kan een bestaande virtuele machine kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="1686d-173">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="1686d-174">VM-grootten</span><span class="sxs-lookup"><span data-stu-id="1686d-174">VM Sizes</span></span>

<span data-ttu-id="1686d-175">Hallo tabel categoriseert grootten in gebruiksvoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="1686d-175">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="1686d-176">Type</span><span class="sxs-lookup"><span data-stu-id="1686d-176">Type</span></span>                     | <span data-ttu-id="1686d-177">Grootten</span><span class="sxs-lookup"><span data-stu-id="1686d-177">Sizes</span></span>           |    <span data-ttu-id="1686d-178">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1686d-178">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1686d-179">Algemeen doel</span><span class="sxs-lookup"><span data-stu-id="1686d-179">General purpose</span></span>         |<span data-ttu-id="1686d-180">DSv2, Dv2, DS, D, Av2, A0 7</span><span class="sxs-lookup"><span data-stu-id="1686d-180">DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="1686d-181">Taakverdeling CPU-naar-geheugen.</span><span class="sxs-lookup"><span data-stu-id="1686d-181">Balanced CPU-to-memory.</span></span> <span data-ttu-id="1686d-182">Ideaal voor dev / test- en kleine toomedium toepassingen en gegevens oplossingen.</span><span class="sxs-lookup"><span data-stu-id="1686d-182">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| <span data-ttu-id="1686d-183">Geoptimaliseerde rekenkracht</span><span class="sxs-lookup"><span data-stu-id="1686d-183">Compute optimized</span></span>      | <span data-ttu-id="1686d-184">FS, F</span><span class="sxs-lookup"><span data-stu-id="1686d-184">Fs, F</span></span>             | <span data-ttu-id="1686d-185">Hoog CPU-naar-geheugen.</span><span class="sxs-lookup"><span data-stu-id="1686d-185">High CPU-to-memory.</span></span> <span data-ttu-id="1686d-186">Goede voor gemiddeld verkeer toepassingen, netwerkapparatuur en batchprocessen.</span><span class="sxs-lookup"><span data-stu-id="1686d-186">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| <span data-ttu-id="1686d-187">Geoptimaliseerd geheugen</span><span class="sxs-lookup"><span data-stu-id="1686d-187">Memory optimized</span></span>       | <span data-ttu-id="1686d-188">GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="1686d-188">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="1686d-189">Hoge geheugen-naar-core.</span><span class="sxs-lookup"><span data-stu-id="1686d-189">High memory-to-core.</span></span> <span data-ttu-id="1686d-190">Ideaal voor relationele databases, gemiddeld toolarge caches en in het geheugen analytics.</span><span class="sxs-lookup"><span data-stu-id="1686d-190">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| <span data-ttu-id="1686d-191">Geoptimaliseerde opslag</span><span class="sxs-lookup"><span data-stu-id="1686d-191">Storage optimized</span></span>       | <span data-ttu-id="1686d-192">Ls</span><span class="sxs-lookup"><span data-stu-id="1686d-192">Ls</span></span>                | <span data-ttu-id="1686d-193">Snelle doorvoer van schijfgegevens en IO.</span><span class="sxs-lookup"><span data-stu-id="1686d-193">High disk throughput and IO.</span></span> <span data-ttu-id="1686d-194">Ideaal voor big data-, SQL- en NoSQL-databases.</span><span class="sxs-lookup"><span data-stu-id="1686d-194">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| <span data-ttu-id="1686d-195">GPU</span><span class="sxs-lookup"><span data-stu-id="1686d-195">GPU</span></span>           | <span data-ttu-id="1686d-196">NV, NC</span><span class="sxs-lookup"><span data-stu-id="1686d-196">NV, NC</span></span>            | <span data-ttu-id="1686d-197">Gespecialiseerde VMs gericht voor zware grafische weergave en het bewerken van video's.</span><span class="sxs-lookup"><span data-stu-id="1686d-197">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| <span data-ttu-id="1686d-198">Hoge prestaties</span><span class="sxs-lookup"><span data-stu-id="1686d-198">High performance</span></span> | <span data-ttu-id="1686d-199">H, A8 11</span><span class="sxs-lookup"><span data-stu-id="1686d-199">H, A8-11</span></span>          | <span data-ttu-id="1686d-200">De krachtigste CPU VMs met optionele hoge gegevensdoorvoer netwerkinterfaces (RDMA).</span><span class="sxs-lookup"><span data-stu-id="1686d-200">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="1686d-201">Zoeken naar beschikbare VM-grootten</span><span class="sxs-lookup"><span data-stu-id="1686d-201">Find available VM sizes</span></span>

<span data-ttu-id="1686d-202">een lijst met VM toosee groottes beschikbaar in een bepaalde regio, gebruikt u Hallo [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1686d-202">toosee a list of VM sizes available in a particular region, use hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command.</span></span>

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a><span data-ttu-id="1686d-203">De grootte van een virtuele machine wijzigen</span><span class="sxs-lookup"><span data-stu-id="1686d-203">Resize a VM</span></span>

<span data-ttu-id="1686d-204">Nadat een virtuele machine is geïmplementeerd, kan het formaat is gewijzigd tooincrease of resourcetoewijzing verlagen.</span><span class="sxs-lookup"><span data-stu-id="1686d-204">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="1686d-205">Voordat het formaat van een virtuele machine, controleren als hello gewenste grootte beschikbaar op Hallo huidige VM-cluster is.</span><span class="sxs-lookup"><span data-stu-id="1686d-205">Before resizing a VM, check if hello desired size is available on hello current VM cluster.</span></span> <span data-ttu-id="1686d-206">Hallo [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) opdracht retourneert een lijst met grootten.</span><span class="sxs-lookup"><span data-stu-id="1686d-206">hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command returns a list of sizes.</span></span> 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

<span data-ttu-id="1686d-207">Desgewenst Hallo grootte is beschikbaar kan hello VM worden gewijzigd vanuit een status ingeschakeld op maar deze opnieuw wordt opgestart tijdens het Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="1686d-207">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

<span data-ttu-id="1686d-208">Desgewenst Hallo grootte is niet op Hallo huidig cluster Hallo VM behoeften toobe ongedaan voordat Hallo vergroten of verkleinen van de bewerking kan zich voordoen.</span><span class="sxs-lookup"><span data-stu-id="1686d-208">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="1686d-209">Houd er rekening mee wanneer Hallo VM weer is ingeschakeld, worden alle gegevens op de tijdelijke schijf Hallo verwijderd en Hallo openbaar IP-adres wijzigen tenzij u een statisch IP-adres wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1686d-209">Note, when hello VM is powered back on, any data on hello temp disk are removed, and hello public IP address change unless a static IP address is being used.</span></span> 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a><span data-ttu-id="1686d-210">VM-energiestatus</span><span class="sxs-lookup"><span data-stu-id="1686d-210">VM power states</span></span>

<span data-ttu-id="1686d-211">Een Azure VM kan een van de vele energiestatussen hebben.</span><span class="sxs-lookup"><span data-stu-id="1686d-211">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="1686d-212">Deze status vertegenwoordigt de huidige status Hallo Hallo VM Hallo verwerkt Hallo hypervisor.</span><span class="sxs-lookup"><span data-stu-id="1686d-212">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="1686d-213">Energiestatus</span><span class="sxs-lookup"><span data-stu-id="1686d-213">Power states</span></span>

| <span data-ttu-id="1686d-214">Energieniveau</span><span class="sxs-lookup"><span data-stu-id="1686d-214">Power State</span></span> | <span data-ttu-id="1686d-215">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1686d-215">Description</span></span>
|----|----|
| <span data-ttu-id="1686d-216">Starting</span><span class="sxs-lookup"><span data-stu-id="1686d-216">Starting</span></span> | <span data-ttu-id="1686d-217">Hiermee wordt aangegeven op Hallo virtuele machine wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="1686d-217">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="1686d-218">Running</span><span class="sxs-lookup"><span data-stu-id="1686d-218">Running</span></span> | <span data-ttu-id="1686d-219">Hiermee wordt aangegeven dat de Hallo virtuele machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1686d-219">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="1686d-220">Stopping</span><span class="sxs-lookup"><span data-stu-id="1686d-220">Stopping</span></span> | <span data-ttu-id="1686d-221">Hiermee wordt aangegeven dat de virtuele machine hello wordt gestopt.</span><span class="sxs-lookup"><span data-stu-id="1686d-221">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="1686d-222">Stopped</span><span class="sxs-lookup"><span data-stu-id="1686d-222">Stopped</span></span> | <span data-ttu-id="1686d-223">Geeft aan dat de virtuele machine Hallo is gestopt.</span><span class="sxs-lookup"><span data-stu-id="1686d-223">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="1686d-224">Houd er rekening mee dat virtuele machines in de status gestopt Hallo nog steeds compute worden kosten in rekening.</span><span class="sxs-lookup"><span data-stu-id="1686d-224">Note that virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="1686d-225">Toewijzing</span><span class="sxs-lookup"><span data-stu-id="1686d-225">Deallocating</span></span> | <span data-ttu-id="1686d-226">Hiermee wordt aangegeven dat de virtuele machine hello wordt opgeheven.</span><span class="sxs-lookup"><span data-stu-id="1686d-226">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="1686d-227">De toewijzing ongedaan gemaakt</span><span class="sxs-lookup"><span data-stu-id="1686d-227">Deallocated</span></span> | <span data-ttu-id="1686d-228">Hiermee wordt aangegeven dat de virtuele machine hello wordt volledig verwijderd uit Hallo hypervisor maar nog steeds beschikbaar in vlak voor Hallo-besturingselement.</span><span class="sxs-lookup"><span data-stu-id="1686d-228">Indicates that hello virtual machine is completely removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="1686d-229">Virtuele machines in Hallo Deallocated status kan niet worden compute-kosten in rekening.</span><span class="sxs-lookup"><span data-stu-id="1686d-229">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="1686d-230">Geeft aan dat de energiestatus Hallo van Hallo virtuele machine onbekend.</span><span class="sxs-lookup"><span data-stu-id="1686d-230">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="1686d-231">Energieniveau vinden</span><span class="sxs-lookup"><span data-stu-id="1686d-231">Find power state</span></span>

<span data-ttu-id="1686d-232">tooretrieve hello status van een bepaalde virtuele machine, gebruik Hallo [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1686d-232">tooretrieve hello state of a particular VM, use hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span> <span data-ttu-id="1686d-233">Niet zeker toospecify een geldige naam voor een virtuele machine en de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="1686d-233">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

<span data-ttu-id="1686d-234">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="1686d-234">Output:</span></span>

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a><span data-ttu-id="1686d-235">Beheertaken</span><span class="sxs-lookup"><span data-stu-id="1686d-235">Management tasks</span></span>

<span data-ttu-id="1686d-236">Tijdens het Hallo-levensduur van een virtuele machine kunt u beheertaken toorun zoals starten, stoppen of een virtuele machine wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1686d-236">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="1686d-237">U kunt bovendien toocreate scripts tooautomate herhalende of complexe taken.</span><span class="sxs-lookup"><span data-stu-id="1686d-237">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="1686d-238">Met Azure PowerShell, kunnen veel algemene beheertaken worden uitgevoerd vanaf de opdrachtregel hello, hetzij in scripts.</span><span class="sxs-lookup"><span data-stu-id="1686d-238">Using Azure PowerShell, many common management tasks can be run from hello command line or in scripts.</span></span>

### <a name="stop-virtual-machine"></a><span data-ttu-id="1686d-239">Virtuele machine stoppen</span><span class="sxs-lookup"><span data-stu-id="1686d-239">Stop virtual machine</span></span>

<span data-ttu-id="1686d-240">Stop en toewijzing van een virtuele machine met [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="1686d-240">Stop and deallocate a virtual machine with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

<span data-ttu-id="1686d-241">Als u tookeep Hallo virtuele machine in een ingerichte staat wilt, gebruikt u Hallo StayProvisioned - parameter.</span><span class="sxs-lookup"><span data-stu-id="1686d-241">If you want tookeep hello virtual machine in a provisioned state, use hello -StayProvisioned parameter.</span></span>

### <a name="start-virtual-machine"></a><span data-ttu-id="1686d-242">Virtuele machine starten</span><span class="sxs-lookup"><span data-stu-id="1686d-242">Start virtual machine</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="1686d-243">Verwijderen van resourcegroep</span><span class="sxs-lookup"><span data-stu-id="1686d-243">Delete resource group</span></span>

<span data-ttu-id="1686d-244">Verwijderen van een resourcegroep, worden ook alle resources binnen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1686d-244">Deleting a resource group also deletes all resources contained within.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a><span data-ttu-id="1686d-245">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1686d-245">Next steps</span></span>

<span data-ttu-id="1686d-246">In deze zelfstudie hebt u geleerd over basic VM maken en beheren zoals het:</span><span class="sxs-lookup"><span data-stu-id="1686d-246">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1686d-247">Maken en koppelen tooa VM</span><span class="sxs-lookup"><span data-stu-id="1686d-247">Create and connect tooa VM</span></span>
> * <span data-ttu-id="1686d-248">Selecteer en gebruik van VM-installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="1686d-248">Select and use VM images</span></span>
> * <span data-ttu-id="1686d-249">Weergeven en gebruiken van specifieke VM-grootten</span><span class="sxs-lookup"><span data-stu-id="1686d-249">View and use specific VM sizes</span></span>
> * <span data-ttu-id="1686d-250">De grootte van een virtuele machine wijzigen</span><span class="sxs-lookup"><span data-stu-id="1686d-250">Resize a VM</span></span>
> * <span data-ttu-id="1686d-251">Bekijken en te begrijpen status virtuele machine</span><span class="sxs-lookup"><span data-stu-id="1686d-251">View and understand VM state</span></span>

<span data-ttu-id="1686d-252">Ga toohello volgende zelfstudie toolearn over VM-schijven.</span><span class="sxs-lookup"><span data-stu-id="1686d-252">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="1686d-253">Maken en beheren van VM-schijven</span><span class="sxs-lookup"><span data-stu-id="1686d-253">Create and Manage VM disks</span></span>](./tutorial-manage-data-disk.md)
