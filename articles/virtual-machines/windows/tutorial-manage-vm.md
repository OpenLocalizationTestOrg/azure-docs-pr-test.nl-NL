---
title: Maken en beheren van Windows virtuele machines met de Azure PowerShell-module | Microsoft Docs
description: Zelfstudie - maken en beheren van Windows virtuele machines met de Azure PowerShell-module
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
ms.openlocfilehash: ec1bb7834beb66dc28dd5b1db764bd358243292c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-windows-vms-with-the-azure-powershell-module"></a><span data-ttu-id="c36ae-103">Maken en beheren van Windows virtuele machines met de Azure PowerShell-module</span><span class="sxs-lookup"><span data-stu-id="c36ae-103">Create and Manage Windows VMs with the Azure PowerShell module</span></span>

<span data-ttu-id="c36ae-104">Virtuele machines van Azure bieden een volledig worden geconfigureerd en flexibele computeromgeving.</span><span class="sxs-lookup"><span data-stu-id="c36ae-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="c36ae-105">Deze zelfstudie bevat informatie over basic virtuele machine van Azure-implementatie items zoals het selecteren van een VM-grootte, een VM-installatiekopie te selecteren en implementeren van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c36ae-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="c36ae-106">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="c36ae-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c36ae-107">Maken en verbinding maken met een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c36ae-107">Create and connect to a VM</span></span>
> * <span data-ttu-id="c36ae-108">Selecteer en gebruik van VM-installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="c36ae-108">Select and use VM images</span></span>
> * <span data-ttu-id="c36ae-109">Weergeven en gebruiken van specifieke VM-grootten</span><span class="sxs-lookup"><span data-stu-id="c36ae-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="c36ae-110">De grootte van een virtuele machine wijzigen</span><span class="sxs-lookup"><span data-stu-id="c36ae-110">Resize a VM</span></span>
> * <span data-ttu-id="c36ae-111">Bekijken en te begrijpen status virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c36ae-111">View and understand VM state</span></span>

<span data-ttu-id="c36ae-112">Voor deze zelfstudie is moduleversie 3,6 of hoger van Azure PowerShell vereist.</span><span class="sxs-lookup"><span data-stu-id="c36ae-112">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="c36ae-113">Voer ` Get-Module -ListAvailable AzureRM` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="c36ae-113">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="c36ae-114">Als u upgraden wilt, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="c36ae-114">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="c36ae-115">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="c36ae-115">Create resource group</span></span>

<span data-ttu-id="c36ae-116">Maak een resourcegroep met de opdracht [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="c36ae-116">Create a resource group with the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> 

<span data-ttu-id="c36ae-117">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="c36ae-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="c36ae-118">Een resourcegroep moet worden gemaakt voordat een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c36ae-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="c36ae-119">In dit voorbeeld wordt een resourcegroep met de naam *myResourceGroupVM* wordt gemaakt in de *EastUS* regio.</span><span class="sxs-lookup"><span data-stu-id="c36ae-119">In this example, a resource group named *myResourceGroupVM* is created in the *EastUS* region.</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

<span data-ttu-id="c36ae-120">De resourcegroep is opgegeven bij het maken of wijzigen van een virtuele machine die in deze zelfstudie kan worden gezien.</span><span class="sxs-lookup"><span data-stu-id="c36ae-120">The resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="c36ae-121">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="c36ae-121">Create virtual machine</span></span>

<span data-ttu-id="c36ae-122">Een virtuele machine moet worden verbonden met een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="c36ae-122">A virtual machine must be connected to a virtual network.</span></span> <span data-ttu-id="c36ae-123">U communiceren met de virtuele machine via een openbaar IP-adres via een netwerkinterfacekaart.</span><span class="sxs-lookup"><span data-stu-id="c36ae-123">You communicate with the virtual machine using a public IP address through a network interface card.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="c36ae-124">Virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="c36ae-124">Create virtual network</span></span>

<span data-ttu-id="c36ae-125">Maak een subnet met [nieuw AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="c36ae-125">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="c36ae-126">Maak een virtueel netwerk met [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="c36ae-126">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a><span data-ttu-id="c36ae-127">Openbare IP-adres maken</span><span class="sxs-lookup"><span data-stu-id="c36ae-127">Create public IP address</span></span>

<span data-ttu-id="c36ae-128">Maken van een openbaar IP-adres met [nieuw AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="c36ae-128">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a><span data-ttu-id="c36ae-129">Maken van netwerkinterfacekaart</span><span class="sxs-lookup"><span data-stu-id="c36ae-129">Create network interface card</span></span>

<span data-ttu-id="c36ae-130">Maken van een netwerkkaart met [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="c36ae-130">Create a network interface card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a><span data-ttu-id="c36ae-131">Netwerkbeveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="c36ae-131">Create network security group</span></span>

<span data-ttu-id="c36ae-132">Een Azure [netwerkbeveiligingsgroep](../../virtual-network/virtual-networks-nsg.md) (NSG) Hiermee wordt bepaald binnenkomend en uitgaand verkeer voor een of meer virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c36ae-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="c36ae-133">Netwerkbeveiligingsgroepen toestaan of weigeren van netwerkverkeer op een specifieke poort of een poortbereik.</span><span class="sxs-lookup"><span data-stu-id="c36ae-133">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="c36ae-134">Deze regels kunnen ook een voorvoegsel voor bronadres bevatten, zodat alleen verkeer dat afkomstig is op een vooraf gedefinieerde bron met een virtuele machine communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="c36ae-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span> <span data-ttu-id="c36ae-135">Voor toegang tot de IIS-webserver die u installeert, moet u een inkomende NSG-regel toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c36ae-135">To access the IIS webserver that you are installing, you must add an inbound NSG rule.</span></span>

<span data-ttu-id="c36ae-136">Gebruik voor het maken van een inkomende regel voor het NSG [toevoegen AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="c36ae-136">To create an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="c36ae-137">Het volgende voorbeeld wordt een NSG regel voor licentiecontrole *myNSGRule* opent die poort *3389* voor de virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="c36ae-137">The following example creates an NSG rule named *myNSGRule* that opens port *3389* for the virtual machine:</span></span>

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

<span data-ttu-id="c36ae-138">Maak het NSG met *myNSGRule* met [nieuw AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="c36ae-138">Create the NSG using *myNSGRule* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

<span data-ttu-id="c36ae-139">Het NSG toevoegen aan het subnet in het virtuele netwerk met [Set AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="c36ae-139">Add the NSG to the subnet in the virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="c36ae-140">Bijwerken van het virtuele netwerk met [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="c36ae-140">Update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a><span data-ttu-id="c36ae-141">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="c36ae-141">Create virtual machine</span></span>

<span data-ttu-id="c36ae-142">Wanneer u een virtuele machine maakt, er zijn diverse opties beschikbaar zoals besturingssysteemkopie schijf sizing en administratieve referenties.</span><span class="sxs-lookup"><span data-stu-id="c36ae-142">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="c36ae-143">In dit voorbeeld wordt een virtuele machine gemaakt met de naam *myVM* de nieuwste versie van Windows Server 2016 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="c36ae-143">In this example, a virtual machine is created with a name of *myVM* running the latest version of Windows Server 2016 Datacenter.</span></span>

<span data-ttu-id="c36ae-144">Stel de gebruikersnaam en wachtwoord nodig voor het beheerdersaccount op de virtuele machine met [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="c36ae-144">Set the username and password needed for the administrator account on the virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="c36ae-145">Maken van de eerste configuratie voor de virtuele machine met [nieuw AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span><span class="sxs-lookup"><span data-stu-id="c36ae-145">Create the initial configuration for the virtual machine with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="c36ae-146">Informatie over het besturingssysteem toevoegen aan de virtuele-machineconfiguratie met [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span><span class="sxs-lookup"><span data-stu-id="c36ae-146">Add the operating system information to the virtual machine configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span></span>

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="c36ae-147">De informatie van de installatiekopie toevoegen aan de virtuele-machineconfiguratie met [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span><span class="sxs-lookup"><span data-stu-id="c36ae-147">Add the image information to the virtual machine configuration with [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

<span data-ttu-id="c36ae-148">De instellingen van het besturingssysteem schijf toevoegen aan de virtuele-machineconfiguratie met [Set AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span><span class="sxs-lookup"><span data-stu-id="c36ae-148">Add the operating system disk settings to the virtual machine configuration with [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

<span data-ttu-id="c36ae-149">Toevoegen van de netwerkinterfacekaart die u eerder hebt gemaakt voor de virtuele-machineconfiguratie met [toevoegen AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="c36ae-149">Add the network interface card that you previously created to the virtual machine configuration with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="c36ae-150">Maak de virtuele machine met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="c36ae-150">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-to-vm"></a><span data-ttu-id="c36ae-151">Verbinding maken met virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c36ae-151">Connect to VM</span></span>

<span data-ttu-id="c36ae-152">Wanneer de implementatie is voltooid, maakt u via een extern bureaublad verbinding met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c36ae-152">After the deployment has completed, create a remote desktop connection with the virtual machine.</span></span>

<span data-ttu-id="c36ae-153">Voer de volgende opdrachten uit om het openbare IP-adres van de virtuele machine te retourneren.</span><span class="sxs-lookup"><span data-stu-id="c36ae-153">Run the following commands to return the public IP address of the virtual machine.</span></span> <span data-ttu-id="c36ae-154">Noteer dit IP-adres zodat u vanuit uw browser verbinding kunt maken met het adres om webverbindingen te testen.</span><span class="sxs-lookup"><span data-stu-id="c36ae-154">Take note of this IP Address so you can connect to it with your browser to test web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

<span data-ttu-id="c36ae-155">Gebruik de volgende opdracht om een sessie met een extern bureaublad te starten voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c36ae-155">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="c36ae-156">Vervang het IP-adres door het *publicIPAddress* van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c36ae-156">Replace the IP address with the *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="c36ae-157">Wanneer u hierom wordt gevraagd, typt u de referenties die zijn gebruikt bij het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c36ae-157">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a><span data-ttu-id="c36ae-158">VM-installatiekopieën begrijpen</span><span class="sxs-lookup"><span data-stu-id="c36ae-158">Understand VM images</span></span>

<span data-ttu-id="c36ae-159">De Azure marketplace bevat veel installatiekopieën van virtuele machines die kunnen worden gebruikt voor het maken van een nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c36ae-159">The Azure marketplace includes many virtual machine images that can be used to create a new virtual machine.</span></span> <span data-ttu-id="c36ae-160">In de vorige stappen is een virtuele machine gemaakt met behulp van de installatiekopie van het Windows Server 2016-Datacenter.</span><span class="sxs-lookup"><span data-stu-id="c36ae-160">In the previous steps, a virtual machine was created using the Windows Server 2016-Datacenter image.</span></span> <span data-ttu-id="c36ae-161">In deze stap wordt de PowerShell-module gebruikt voor het zoeken van de marketplace voor andere Windows-installatiekopieën ook als basis voor de nieuwe virtuele machines kunnen.</span><span class="sxs-lookup"><span data-stu-id="c36ae-161">In this step, the PowerShell module is used to search the marketplace for other Windows images, which can also as a base for new VMs.</span></span> <span data-ttu-id="c36ae-162">Dit proces bestaat uit het vinden van de uitgever, aanbieding en de naam van de installatiekopie (Sku).</span><span class="sxs-lookup"><span data-stu-id="c36ae-162">This process consists of finding the publisher, offer, and the image name (Sku).</span></span> 

<span data-ttu-id="c36ae-163">Gebruik de [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) opdracht voor het retourneren van een lijst van uitgevers van de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="c36ae-163">Use the [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command to return a list of image publishers.</span></span>  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

<span data-ttu-id="c36ae-164">Gebruik de [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) retourneren een lijst met aanbiedingen van de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="c36ae-164">Use the [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) to return a list of image offers.</span></span> <span data-ttu-id="c36ae-165">Met deze opdracht wordt de geretourneerde lijst gefilterd op de opgegeven uitgever.</span><span class="sxs-lookup"><span data-stu-id="c36ae-165">With this command, the returned list is filtered on the specified publisher.</span></span> 

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

<span data-ttu-id="c36ae-166">De [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) opdracht filter vervolgens op de naam van de uitgever en de aanbieding te retourneren van een lijst met namen van afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="c36ae-166">The [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) command will then filter on the publisher and offer name to return a list of image names.</span></span>

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

<span data-ttu-id="c36ae-167">Deze informatie kan worden gebruikt voor het implementeren van een virtuele machine met een specifieke installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="c36ae-167">This information can be used to deploy a VM with a specific image.</span></span> <span data-ttu-id="c36ae-168">In het volgende voorbeeld wordt de naam van de installatiekopie van het VM-object.</span><span class="sxs-lookup"><span data-stu-id="c36ae-168">This example sets the image name on the VM object.</span></span> <span data-ttu-id="c36ae-169">Raadpleeg de eerdere voorbeelden in deze zelfstudie voor volledige implementatiestappen.</span><span class="sxs-lookup"><span data-stu-id="c36ae-169">Refer to the previous examples in this tutorial for complete deployment steps.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="c36ae-170">VM-grootten begrijpen</span><span class="sxs-lookup"><span data-stu-id="c36ae-170">Understand VM sizes</span></span>

<span data-ttu-id="c36ae-171">De grootte van een virtuele machine bepaalt de hoeveelheid compute-bronnen zoals CPU en GPU geheugen die beschikbaar zijn gesteld voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c36ae-171">A virtual machine size determines the amount of compute resources such as CPU, GPU, and memory that are made available to the virtual machine.</span></span> <span data-ttu-id="c36ae-172">Virtuele machines moeten worden gemaakt met een geschikt is voor de werklast van de verwachte grootte.</span><span class="sxs-lookup"><span data-stu-id="c36ae-172">Virtual machines need to be created with a size appropriate for the expect work load.</span></span> <span data-ttu-id="c36ae-173">Als de werkbelasting toeneemt, kan een bestaande virtuele machine kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c36ae-173">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="c36ae-174">VM-grootten</span><span class="sxs-lookup"><span data-stu-id="c36ae-174">VM Sizes</span></span>

<span data-ttu-id="c36ae-175">De volgende tabel categoriseert grootten in gebruiksvoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="c36ae-175">The following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="c36ae-176">Type</span><span class="sxs-lookup"><span data-stu-id="c36ae-176">Type</span></span>                     | <span data-ttu-id="c36ae-177">Grootten</span><span class="sxs-lookup"><span data-stu-id="c36ae-177">Sizes</span></span>           |    <span data-ttu-id="c36ae-178">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c36ae-178">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c36ae-179">Algemeen doel</span><span class="sxs-lookup"><span data-stu-id="c36ae-179">General purpose</span></span>         |<span data-ttu-id="c36ae-180">DSv2, Dv2, DS, D, Av2, A0 7</span><span class="sxs-lookup"><span data-stu-id="c36ae-180">DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="c36ae-181">Taakverdeling CPU-naar-geheugen.</span><span class="sxs-lookup"><span data-stu-id="c36ae-181">Balanced CPU-to-memory.</span></span> <span data-ttu-id="c36ae-182">Ideaal voor dev / testen en in kleine tot middelgrote oplossingen voor toepassingen en gegevens.</span><span class="sxs-lookup"><span data-stu-id="c36ae-182">Ideal for dev / test and small to medium applications and data solutions.</span></span>  |
| <span data-ttu-id="c36ae-183">Geoptimaliseerde rekenkracht</span><span class="sxs-lookup"><span data-stu-id="c36ae-183">Compute optimized</span></span>      | <span data-ttu-id="c36ae-184">FS, F</span><span class="sxs-lookup"><span data-stu-id="c36ae-184">Fs, F</span></span>             | <span data-ttu-id="c36ae-185">Hoog CPU-naar-geheugen.</span><span class="sxs-lookup"><span data-stu-id="c36ae-185">High CPU-to-memory.</span></span> <span data-ttu-id="c36ae-186">Goede voor gemiddeld verkeer toepassingen, netwerkapparatuur en batchprocessen.</span><span class="sxs-lookup"><span data-stu-id="c36ae-186">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| <span data-ttu-id="c36ae-187">Geoptimaliseerd geheugen</span><span class="sxs-lookup"><span data-stu-id="c36ae-187">Memory optimized</span></span>       | <span data-ttu-id="c36ae-188">GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="c36ae-188">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="c36ae-189">Hoge geheugen-naar-core.</span><span class="sxs-lookup"><span data-stu-id="c36ae-189">High memory-to-core.</span></span> <span data-ttu-id="c36ae-190">Ideaal voor relationele databases, middelgrote tot grote caches en in het geheugen analytics.</span><span class="sxs-lookup"><span data-stu-id="c36ae-190">Great for relational databases, medium to large caches, and in-memory analytics.</span></span>                 |
| <span data-ttu-id="c36ae-191">Geoptimaliseerde opslag</span><span class="sxs-lookup"><span data-stu-id="c36ae-191">Storage optimized</span></span>       | <span data-ttu-id="c36ae-192">Ls</span><span class="sxs-lookup"><span data-stu-id="c36ae-192">Ls</span></span>                | <span data-ttu-id="c36ae-193">Snelle doorvoer van schijfgegevens en IO.</span><span class="sxs-lookup"><span data-stu-id="c36ae-193">High disk throughput and IO.</span></span> <span data-ttu-id="c36ae-194">Ideaal voor big data-, SQL- en NoSQL-databases.</span><span class="sxs-lookup"><span data-stu-id="c36ae-194">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| <span data-ttu-id="c36ae-195">GPU</span><span class="sxs-lookup"><span data-stu-id="c36ae-195">GPU</span></span>           | <span data-ttu-id="c36ae-196">NV, NC</span><span class="sxs-lookup"><span data-stu-id="c36ae-196">NV, NC</span></span>            | <span data-ttu-id="c36ae-197">Gespecialiseerde VMs gericht voor zware grafische weergave en het bewerken van video's.</span><span class="sxs-lookup"><span data-stu-id="c36ae-197">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| <span data-ttu-id="c36ae-198">Hoge prestaties</span><span class="sxs-lookup"><span data-stu-id="c36ae-198">High performance</span></span> | <span data-ttu-id="c36ae-199">H, A8 11</span><span class="sxs-lookup"><span data-stu-id="c36ae-199">H, A8-11</span></span>          | <span data-ttu-id="c36ae-200">De krachtigste CPU VMs met optionele hoge gegevensdoorvoer netwerkinterfaces (RDMA).</span><span class="sxs-lookup"><span data-stu-id="c36ae-200">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="c36ae-201">Zoeken naar beschikbare VM-grootten</span><span class="sxs-lookup"><span data-stu-id="c36ae-201">Find available VM sizes</span></span>

<span data-ttu-id="c36ae-202">Als een lijst met VM-grootten die beschikbaar zijn in een bepaalde regio wilt weergeven, gebruikt de [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) opdracht.</span><span class="sxs-lookup"><span data-stu-id="c36ae-202">To see a list of VM sizes available in a particular region, use the [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command.</span></span>

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a><span data-ttu-id="c36ae-203">De grootte van een virtuele machine wijzigen</span><span class="sxs-lookup"><span data-stu-id="c36ae-203">Resize a VM</span></span>

<span data-ttu-id="c36ae-204">Nadat een virtuele machine is geïmplementeerd, kan het vergroten of verkleinen resourcetoewijzing worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c36ae-204">After a VM has been deployed, it can be resized to increase or decrease resource allocation.</span></span>

<span data-ttu-id="c36ae-205">Grootte wijzigen van een virtuele machine, Controleer of de gewenste grootte beschikbaar op de huidige VM-cluster is.</span><span class="sxs-lookup"><span data-stu-id="c36ae-205">Before resizing a VM, check if the desired size is available on the current VM cluster.</span></span> <span data-ttu-id="c36ae-206">De [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) opdracht retourneert een lijst met grootten.</span><span class="sxs-lookup"><span data-stu-id="c36ae-206">The [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command returns a list of sizes.</span></span> 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

<span data-ttu-id="c36ae-207">Als de gewenste grootte beschikbaar is, kan de virtuele machine worden gewijzigd van een status ingeschakeld op, maar deze opnieuw wordt opgestart tijdens de bewerking.</span><span class="sxs-lookup"><span data-stu-id="c36ae-207">If the desired size is available, the VM can be resized from a powered-on state, however it is rebooted during the operation.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

<span data-ttu-id="c36ae-208">Als de gewenste grootte niet op het huidige cluster is, moet de VM ongedaan voordat de bewerking formaat kan plaatsvinden.</span><span class="sxs-lookup"><span data-stu-id="c36ae-208">If the desired size is not on the current cluster, the VM needs to be deallocated before the resize operation can occur.</span></span> <span data-ttu-id="c36ae-209">Opmerking: als de virtuele machine weer is ingeschakeld, alle gegevens op de tijdelijke schijf worden verwijderd en wordt de openbare IP-adressen wijzigen tenzij u een statisch IP-adres wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c36ae-209">Note, when the VM is powered back on, any data on the temp disk are removed, and the public IP address change unless a static IP address is being used.</span></span> 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a><span data-ttu-id="c36ae-210">VM-energiestatus</span><span class="sxs-lookup"><span data-stu-id="c36ae-210">VM power states</span></span>

<span data-ttu-id="c36ae-211">Een Azure VM kan een van de vele energiestatussen hebben.</span><span class="sxs-lookup"><span data-stu-id="c36ae-211">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="c36ae-212">Deze status vertegenwoordigt de huidige status van de virtuele machine vanuit het oogpunt van de hypervisor.</span><span class="sxs-lookup"><span data-stu-id="c36ae-212">This state represents the current state of the VM from the standpoint of the hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="c36ae-213">Energiestatus</span><span class="sxs-lookup"><span data-stu-id="c36ae-213">Power states</span></span>

| <span data-ttu-id="c36ae-214">Energieniveau</span><span class="sxs-lookup"><span data-stu-id="c36ae-214">Power State</span></span> | <span data-ttu-id="c36ae-215">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c36ae-215">Description</span></span>
|----|----|
| <span data-ttu-id="c36ae-216">Starting</span><span class="sxs-lookup"><span data-stu-id="c36ae-216">Starting</span></span> | <span data-ttu-id="c36ae-217">Geeft aan dat de virtuele machine wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="c36ae-217">Indicates the virtual machine is being started.</span></span> |
| <span data-ttu-id="c36ae-218">Running</span><span class="sxs-lookup"><span data-stu-id="c36ae-218">Running</span></span> | <span data-ttu-id="c36ae-219">Hiermee wordt aangegeven dat de virtuele machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c36ae-219">Indicates that the virtual machine is running.</span></span> |
| <span data-ttu-id="c36ae-220">Stopping</span><span class="sxs-lookup"><span data-stu-id="c36ae-220">Stopping</span></span> | <span data-ttu-id="c36ae-221">Hiermee wordt aangegeven dat de virtuele machine wordt gestopt.</span><span class="sxs-lookup"><span data-stu-id="c36ae-221">Indicates that the virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="c36ae-222">Stopped</span><span class="sxs-lookup"><span data-stu-id="c36ae-222">Stopped</span></span> | <span data-ttu-id="c36ae-223">Hiermee wordt aangegeven dat de virtuele machine is gestopt.</span><span class="sxs-lookup"><span data-stu-id="c36ae-223">Indicates that the virtual machine is stopped.</span></span> <span data-ttu-id="c36ae-224">Houd er rekening mee dat virtuele machines in de gestopte status nog steeds compute worden kosten in rekening.</span><span class="sxs-lookup"><span data-stu-id="c36ae-224">Note that virtual machines in the stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="c36ae-225">Toewijzing</span><span class="sxs-lookup"><span data-stu-id="c36ae-225">Deallocating</span></span> | <span data-ttu-id="c36ae-226">Hiermee wordt aangegeven dat de virtuele machine wordt opgeheven.</span><span class="sxs-lookup"><span data-stu-id="c36ae-226">Indicates that the virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="c36ae-227">De toewijzing ongedaan gemaakt</span><span class="sxs-lookup"><span data-stu-id="c36ae-227">Deallocated</span></span> | <span data-ttu-id="c36ae-228">Hiermee wordt aangegeven dat de virtuele machine volledig verwijderd van de hypervisor, maar nog steeds beschikbaar in het vlak van het besturingselement wordt.</span><span class="sxs-lookup"><span data-stu-id="c36ae-228">Indicates that the virtual machine is completely removed from the hypervisor but still available in the control plane.</span></span> <span data-ttu-id="c36ae-229">Virtuele machines in de status van de Deallocated kan niet worden compute-kosten in rekening.</span><span class="sxs-lookup"><span data-stu-id="c36ae-229">Virtual machines in the Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="c36ae-230">Hiermee wordt aangegeven dat de voedingsstatus van de virtuele machine onbekend is.</span><span class="sxs-lookup"><span data-stu-id="c36ae-230">Indicates that the power state of the virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="c36ae-231">Energieniveau vinden</span><span class="sxs-lookup"><span data-stu-id="c36ae-231">Find power state</span></span>

<span data-ttu-id="c36ae-232">Voor het ophalen van de status van een bepaalde virtuele machine, gebruikt u de [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) opdracht.</span><span class="sxs-lookup"><span data-stu-id="c36ae-232">To retrieve the state of a particular VM, use the [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span> <span data-ttu-id="c36ae-233">Zorg ervoor dat een geldige naam voor een virtuele machine en de resourcegroep opgeven.</span><span class="sxs-lookup"><span data-stu-id="c36ae-233">Be sure to specify a valid name for a virtual machine and resource group.</span></span> 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

<span data-ttu-id="c36ae-234">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c36ae-234">Output:</span></span>

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a><span data-ttu-id="c36ae-235">Beheertaken</span><span class="sxs-lookup"><span data-stu-id="c36ae-235">Management tasks</span></span>

<span data-ttu-id="c36ae-236">Tijdens de levenscyclus van een virtuele machine, kan u wilt uitvoeren van beheertaken, zoals starten, stoppen of een virtuele machine wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c36ae-236">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="c36ae-237">Bovendien wilt u maken van scripts voor terugkerende of complexe taken automatiseren.</span><span class="sxs-lookup"><span data-stu-id="c36ae-237">Additionally, you may want to create scripts to automate repetitive or complex tasks.</span></span> <span data-ttu-id="c36ae-238">Met Azure PowerShell, kunnen veel algemene beheertaken worden uitgevoerd vanaf de opdrachtregel of in scripts.</span><span class="sxs-lookup"><span data-stu-id="c36ae-238">Using Azure PowerShell, many common management tasks can be run from the command line or in scripts.</span></span>

### <a name="stop-virtual-machine"></a><span data-ttu-id="c36ae-239">Virtuele machine stoppen</span><span class="sxs-lookup"><span data-stu-id="c36ae-239">Stop virtual machine</span></span>

<span data-ttu-id="c36ae-240">Stop en toewijzing van een virtuele machine met [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="c36ae-240">Stop and deallocate a virtual machine with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

<span data-ttu-id="c36ae-241">Als u behouden van de virtuele machine in een ingerichte staat wilt, moet u de parameter - StayProvisioned gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c36ae-241">If you want to keep the virtual machine in a provisioned state, use the -StayProvisioned parameter.</span></span>

### <a name="start-virtual-machine"></a><span data-ttu-id="c36ae-242">Virtuele machine starten</span><span class="sxs-lookup"><span data-stu-id="c36ae-242">Start virtual machine</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="c36ae-243">Verwijderen van resourcegroep</span><span class="sxs-lookup"><span data-stu-id="c36ae-243">Delete resource group</span></span>

<span data-ttu-id="c36ae-244">Verwijderen van een resourcegroep, worden ook alle resources binnen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c36ae-244">Deleting a resource group also deletes all resources contained within.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a><span data-ttu-id="c36ae-245">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c36ae-245">Next steps</span></span>

<span data-ttu-id="c36ae-246">In deze zelfstudie hebt u geleerd over basic VM maken en beheren zoals het:</span><span class="sxs-lookup"><span data-stu-id="c36ae-246">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c36ae-247">Maken en verbinding maken met een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c36ae-247">Create and connect to a VM</span></span>
> * <span data-ttu-id="c36ae-248">Selecteer en gebruik van VM-installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="c36ae-248">Select and use VM images</span></span>
> * <span data-ttu-id="c36ae-249">Weergeven en gebruiken van specifieke VM-grootten</span><span class="sxs-lookup"><span data-stu-id="c36ae-249">View and use specific VM sizes</span></span>
> * <span data-ttu-id="c36ae-250">De grootte van een virtuele machine wijzigen</span><span class="sxs-lookup"><span data-stu-id="c36ae-250">Resize a VM</span></span>
> * <span data-ttu-id="c36ae-251">Bekijken en te begrijpen status virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c36ae-251">View and understand VM state</span></span>

<span data-ttu-id="c36ae-252">Ga naar de volgende zelfstudie voor meer informatie over de VM-schijven.</span><span class="sxs-lookup"><span data-stu-id="c36ae-252">Advance to the next tutorial to learn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="c36ae-253">Maken en beheren van VM-schijven</span><span class="sxs-lookup"><span data-stu-id="c36ae-253">Create and Manage VM disks</span></span>](./tutorial-manage-data-disk.md)
