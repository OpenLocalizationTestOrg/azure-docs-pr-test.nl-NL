---
title: Windows virtuele Machines en virtuele netwerken in Azure | Microsoft Docs
description: Zelfstudie - virtuele Azure-netwerken en virtuele Machines van Windows met Azure PowerShell beheren
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: c71c07f8ecd123a7e27848ba5043d46e315fcf03
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="19a87-103">Virtuele Azure-netwerken en virtuele Machines van Windows met Azure PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="19a87-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="19a87-104">Azure netwerken virtuele Azure-machines gebruiken voor interne en externe communicatie.</span><span class="sxs-lookup"><span data-stu-id="19a87-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="19a87-105">In deze zelfstudie maakt u meerdere virtuele machines (VM's) in een virtueel netwerk maken en netwerkconnectiviteit tussen deze twee configureren.</span><span class="sxs-lookup"><span data-stu-id="19a87-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="19a87-106">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="19a87-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="19a87-107">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="19a87-107">Create a virtual network</span></span>
> * <span data-ttu-id="19a87-108">Subnetten virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="19a87-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="19a87-109">Het netwerkverkeer met Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="19a87-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="19a87-110">Regels voor het netwerkverkeer in actie weergeven</span><span class="sxs-lookup"><span data-stu-id="19a87-110">View traffic rules in action</span></span>

<span data-ttu-id="19a87-111">Voor deze zelfstudie is moduleversie 3,6 of hoger van Azure PowerShell vereist.</span><span class="sxs-lookup"><span data-stu-id="19a87-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="19a87-112">Voer ` Get-Module -ListAvailable AzureRM` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="19a87-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="19a87-113">Als u upgraden wilt, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="19a87-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="19a87-114">VNet maken</span><span class="sxs-lookup"><span data-stu-id="19a87-114">Create VNet</span></span>

<span data-ttu-id="19a87-115">Een VNet is een weergave van uw eigen netwerk in de cloud.</span><span class="sxs-lookup"><span data-stu-id="19a87-115">A VNet is a representation of your own network in the cloud.</span></span> <span data-ttu-id="19a87-116">Een VNet is een logische isolatie van de Azure-cloud toegewezen aan uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="19a87-116">A VNet is a logical isolation of the Azure cloud dedicated to your subscription.</span></span> <span data-ttu-id="19a87-117">U vindt subnetten, regels voor verbinding met deze subnetten en verbindingen van de virtuele machines naar de subnetten binnen een VNet.</span><span class="sxs-lookup"><span data-stu-id="19a87-117">Within a VNet, you find subnets, rules for connectivity to those subnets, and connections from the VMs to the subnets.</span></span>

<span data-ttu-id="19a87-118">Voordat u alle andere Azure-resources maken kunt, moet u een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="19a87-118">Before you can create any other Azure resources, you need to create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="19a87-119">Het volgende voorbeeld wordt een resourcegroep met de naam *myRGNetwork* in de *EastUS* locatie:</span><span class="sxs-lookup"><span data-stu-id="19a87-119">The following example creates a resource group named *myRGNetwork* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="19a87-120">Een subnet is een onderliggende resource van een VNet en helpt bij het segmenten van adresruimten binnen een CIDR-blok met behulp van IP-adresvoorvoegsels definiëren.</span><span class="sxs-lookup"><span data-stu-id="19a87-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="19a87-121">NIC's worden toegevoegd aan subnetten en verbonden met virtuele machines, tegelijk connectiviteit biedt voor verschillende werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="19a87-121">NICs can be added to subnets, and connected to VMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="19a87-122">Maak een subnet met [nieuw AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="19a87-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="19a87-123">Maak een VNET met de naam *myVNet* met *myFrontendSubnet* met [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="19a87-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="19a87-124">Front-virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="19a87-124">Create front-end VM</span></span>

<span data-ttu-id="19a87-125">Voor een virtuele machine om te communiceren in een VNet, moet de virtuele netwerkinterface (NIC).</span><span class="sxs-lookup"><span data-stu-id="19a87-125">For a VM to communicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="19a87-126">De *myFrontendVM* is toegankelijk vanuit het internet, dus u moet ook een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="19a87-126">The *myFrontendVM* is accessed from the internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="19a87-127">Maken van een openbaar IP-adres met [nieuw AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="19a87-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="19a87-128">Maak een NIC met [nieuwe AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="19a87-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="19a87-129">Stel de gebruikersnaam en wachtwoord nodig voor de administrator-account op de virtuele machine met [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="19a87-129">Set the username and password needed for the administrator account on the VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="19a87-130">Maken van het VMs met een [nieuwe AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [toevoegen AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), en [nieuwe-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="19a87-130">Create the VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a><span data-ttu-id="19a87-131">Webserver installeren</span><span class="sxs-lookup"><span data-stu-id="19a87-131">Install web server</span></span>

<span data-ttu-id="19a87-132">U kunt IIS installeren op *myFrontendVM* met behulp van een extern bureaublad-sessiehost.</span><span class="sxs-lookup"><span data-stu-id="19a87-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="19a87-133">U moet het openbare IP-adres van de virtuele machine om deze te openen.</span><span class="sxs-lookup"><span data-stu-id="19a87-133">You need to get the public IP address of the VM to access it.</span></span>

<span data-ttu-id="19a87-134">U kunt het openbare IP-adres ophalen *myFrontendVM* met [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="19a87-134">You can get the public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="19a87-135">Het volgende voorbeeld verkrijgt het IP-adres voor *myPublicIPAddress* eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="19a87-135">The following example obtains the IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="19a87-136">Noteer dit IP-adres zodat u deze in toekomstige stappen gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="19a87-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="19a87-137">Gebruik de volgende opdracht voor het maken van een extern-bureaubladsessie met *myFrontendVM*.</span><span class="sxs-lookup"><span data-stu-id="19a87-137">Use the following command to create a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="19a87-138">Vervang  *<publicIPAddress>*  met het adres dat u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="19a87-138">Replace *<publicIPAddress>* with the address that you previously recorded.</span></span> <span data-ttu-id="19a87-139">Voer desgevraagd de referenties die worden gebruikt bij het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="19a87-139">When prompted, enter the credentials used when you created the VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="19a87-140">Nu dat u zich hebt aangemeld bij *myFrontendVM*, kunt u één regel PowerShell IIS installeren en activeren van de lokale firewallregel webverkeer toestaan.</span><span class="sxs-lookup"><span data-stu-id="19a87-140">Now that you have logged in to *myFrontendVM*, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="19a87-141">Open een PowerShell-prompt en voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="19a87-141">Open a PowerShell prompt and run the following command:</span></span>

<span data-ttu-id="19a87-142">Gebruik [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) om uit te voeren van de extensie voor aangepaste scripts die de IIS-webserver installeert:</span><span class="sxs-lookup"><span data-stu-id="19a87-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) to run the custom script extension that installs the IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="19a87-143">U kunt nu het openbare IP-adres gebruiken om te bladeren naar de virtuele machine om te zien van de IIS-site.</span><span class="sxs-lookup"><span data-stu-id="19a87-143">Now you can use the public IP address to browse to the VM to see the IIS site.</span></span>

![Standaardsite van IIS](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="19a87-145">Interne verkeer beheren</span><span class="sxs-lookup"><span data-stu-id="19a87-145">Manage internal traffic</span></span>

<span data-ttu-id="19a87-146">Een netwerkbeveiligingsgroep (NSG) bevat een lijst met regels voor toestaan of weigeren van netwerkverkeer naar bronnen die zijn verbonden met een VNet.</span><span class="sxs-lookup"><span data-stu-id="19a87-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic to resources connected to a VNet.</span></span> <span data-ttu-id="19a87-147">Nsg's kunnen worden gekoppeld aan subnetten of afzonderlijke NIC's die zijn gekoppeld aan virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="19a87-147">NSGs can be associated to subnets or individual NICs attached to VMs.</span></span> <span data-ttu-id="19a87-148">Openen of sluiten van toegang tot virtuele machines via poorten wordt gedaan met behulp van NSG-regels.</span><span class="sxs-lookup"><span data-stu-id="19a87-148">Opening or closing access to VMs through ports is done using NSG rules.</span></span> <span data-ttu-id="19a87-149">Tijdens het maken van *myFrontendVM*, binnenkomende poort 3389 automatisch voor RDP-verbinding is geopend.</span><span class="sxs-lookup"><span data-stu-id="19a87-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="19a87-150">Interne communicatie van virtuele machines kan worden geconfigureerd met een NSG.</span><span class="sxs-lookup"><span data-stu-id="19a87-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="19a87-151">In dit gedeelte vindt u informatie over het maken van een ander subnet in het netwerk en een NSG toewijzen aan toe te staan een verbinding van *myFrontendVM* naar *myBackendVM* op poort 1433.</span><span class="sxs-lookup"><span data-stu-id="19a87-151">In this section, you learn how to create an additional subnet in the network and assign an NSG to it to allow a connection from *myFrontendVM* to *myBackendVM* on port 1433.</span></span> <span data-ttu-id="19a87-152">Het subnet wordt vervolgens toegewezen aan de virtuele machine wanneer deze wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="19a87-152">The subnet is then assigned to the VM when it is created.</span></span>

<span data-ttu-id="19a87-153">U kunt interne verkeer beperkt tot *myBackendVM* alleen *myFrontendVM* door het maken van een NSG voor het subnet voor back-end.</span><span class="sxs-lookup"><span data-stu-id="19a87-153">You can limit internal traffic to *myBackendVM* from only *myFrontendVM* by creating an NSG for the back-end subnet.</span></span> <span data-ttu-id="19a87-154">Het volgende voorbeeld wordt een NSG regel voor licentiecontrole *myBackendNSGRule* met [nieuw AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span><span class="sxs-lookup"><span data-stu-id="19a87-154">The following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

<span data-ttu-id="19a87-155">Toevoegen van een netwerkbeveiligingsgroep met de naam *myBackendNSG* met [nieuw AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="19a87-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="19a87-156">Back-end subnet toevoegen</span><span class="sxs-lookup"><span data-stu-id="19a87-156">Add back-end subnet</span></span>

<span data-ttu-id="19a87-157">Add *myBackEndSubnet* naar *myVNet* met [toevoegen AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="19a87-157">Add *myBackEndSubnet* to *myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a><span data-ttu-id="19a87-158">Back-end virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="19a87-158">Create back-end VM</span></span>

<span data-ttu-id="19a87-159">Er is de eenvoudigste manier om de back-end virtuele machine maken met behulp van een installatiekopie van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="19a87-159">The easiest way to create the back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="19a87-160">Deze zelfstudie alleen de virtuele machine maakt met de database-server, maar geen biedt informatie over het openen van de database.</span><span class="sxs-lookup"><span data-stu-id="19a87-160">This tutorial only creates the VM with the database server, but doesn't provide information about accessing the database.</span></span>

<span data-ttu-id="19a87-161">Maak *myBackendNic*:</span><span class="sxs-lookup"><span data-stu-id="19a87-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="19a87-162">De gebruikersnaam en wachtwoord nodig voor het beheerdersaccount op de virtuele machine met Get-Credential instellen:</span><span class="sxs-lookup"><span data-stu-id="19a87-162">Set the username and password needed for the administrator account on the VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="19a87-163">Maak *myBackendVM*:</span><span class="sxs-lookup"><span data-stu-id="19a87-163">Create *myBackendVM*:</span></span>

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

<span data-ttu-id="19a87-164">De afbeelding die wordt gebruikt SQL Server is geïnstalleerd, maar niet in deze zelfstudie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="19a87-164">The image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="19a87-165">Het is opgenomen om weer te geven hoe u een virtuele machine voor het afhandelen van webverkeer en een virtuele machine voor het afhandelen van database-beheer kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="19a87-165">It is included to show you how you can configure a VM to handle web traffic and a VM to handle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19a87-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="19a87-166">Next steps</span></span>

<span data-ttu-id="19a87-167">In deze zelfstudie hebt gemaakt en beveiligd Azure-netwerken met betrekking tot virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="19a87-167">In this tutorial, you created and secured Azure networks as related to virtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="19a87-168">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="19a87-168">Create a virtual network</span></span>
> * <span data-ttu-id="19a87-169">Subnetten virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="19a87-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="19a87-170">Het netwerkverkeer met Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="19a87-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="19a87-171">Regels voor het netwerkverkeer in actie weergeven</span><span class="sxs-lookup"><span data-stu-id="19a87-171">View traffic rules in action</span></span>

<span data-ttu-id="19a87-172">Ga naar de volgende zelfstudie voor meer informatie over het controleren van het beveiligen van gegevens op virtuele machines met behulp van Azure backup.</span><span class="sxs-lookup"><span data-stu-id="19a87-172">Advance to the next tutorial to learn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="19a87-173">.</span><span class="sxs-lookup"><span data-stu-id="19a87-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="19a87-174">Back-up van Windows virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="19a87-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
