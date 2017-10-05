---
title: Azure Quick Start - Een Windows VM PowerShell maken | Microsoft Docs
description: Ontdek snel hoe u virtuele Windows-machines maakt met PowerShell
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 8516cfa2272694496eb353a83eca77c13a516750
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a><span data-ttu-id="db7c0-103">Een virtuele Windows-machine maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="db7c0-103">Create a Windows virtual machine with PowerShell</span></span>

<span data-ttu-id="db7c0-104">De Azure PowerShell-module wordt gebruikt voor het maken en beheren van Azure-resources vanaf de PowerShell-opdrachtregel of in scripts.</span><span class="sxs-lookup"><span data-stu-id="db7c0-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span></span> <span data-ttu-id="db7c0-105">In deze handleiding wordt beschreven hoe u PowerShell gebruikt voor het maken van een virtuele Azure-machine met Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="db7c0-105">This guide details using PowerShell to create and Azure virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="db7c0-106">Als de implementatie is voltooid, maken we verbinding met de server en installeren we ISS.</span><span class="sxs-lookup"><span data-stu-id="db7c0-106">Once deployment is complete, we connect to the server and install IIS.</span></span>  

<span data-ttu-id="db7c0-107">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="db7c0-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="db7c0-108">Voor deze Quick Start is moduleversie 3.6 of hoger van Azure PowerShell vereist.</span><span class="sxs-lookup"><span data-stu-id="db7c0-108">This quick start requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="db7c0-109">Voer ` Get-Module -ListAvailable AzureRM` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="db7c0-109">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="db7c0-110">Als u PowerShell wilt installeren of upgraden, raadpleegt u [De Azure PowerShell-module installeren](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="db7c0-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="db7c0-111">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="db7c0-111">Log in to Azure</span></span>

<span data-ttu-id="db7c0-112">Meld u aan bij uw Azure-abonnement met de opdracht `Login-AzureRmAccount` en volg de instructies op het scherm.</span><span class="sxs-lookup"><span data-stu-id="db7c0-112">Log in to your Azure subscription with the `Login-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="db7c0-113">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="db7c0-113">Create resource group</span></span>

<span data-ttu-id="db7c0-114">Maak een Azure-resourcegroep met de opdracht [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="db7c0-114">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="db7c0-115">Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="db7c0-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a><span data-ttu-id="db7c0-116">Netwerkresources maken</span><span class="sxs-lookup"><span data-stu-id="db7c0-116">Create networking resources</span></span>

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a><span data-ttu-id="db7c0-117">Maak een virtueel netwerk, subnet en een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="db7c0-117">Create a virtual network, subnet, and a public IP address.</span></span> 
<span data-ttu-id="db7c0-118">Deze resources worden gebruikt voor netwerkconnectiviteit met de virtuele machine en om verbinding met internet te maken.</span><span class="sxs-lookup"><span data-stu-id="db7c0-118">These resources are used to provide network connectivity to the virtual machine and connect it to the internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location EastUS `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location EastUS `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="db7c0-119">Maak een netwerkbeveiligingsgroep en een regel voor de netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="db7c0-119">Create a network security group and a network security group rule.</span></span> 
<span data-ttu-id="db7c0-120">De netwerkbeveiligingsgroep beveiligt de virtuele machine met binnenkomende en uitgaande regels.</span><span class="sxs-lookup"><span data-stu-id="db7c0-120">The network security group secures the virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="db7c0-121">In dit geval is er een binnenkomende regel gemaakt voor poort 3389, waarmee binnenkomende verbindingen met een extern bureaublad worden toegestaan.</span><span class="sxs-lookup"><span data-stu-id="db7c0-121">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span> <span data-ttu-id="db7c0-122">We willen ook een regel maken voor poort 80, de poort voor binnenkomend webverkeer.</span><span class="sxs-lookup"><span data-stu-id="db7c0-122">We also want to create an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-the-virtual-machine"></a><span data-ttu-id="db7c0-123">Maak een netwerkkaart voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="db7c0-123">Create a network card for the virtual machine.</span></span> 
<span data-ttu-id="db7c0-124">Maak een netwerkkaart met [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="db7c0-124">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for the virtual machine.</span></span> <span data-ttu-id="db7c0-125">De netwerkkaart verbindt de virtuele machine met een subnet, netwerkbeveiligingsgroep en openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="db7c0-125">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="db7c0-126">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="db7c0-126">Create virtual machine</span></span>

<span data-ttu-id="db7c0-127">Maak een virtuele-machineconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="db7c0-127">Create a virtual machine configuration.</span></span> <span data-ttu-id="db7c0-128">Deze configuratie bevat de instellingen die worden gebruikt bij het implementeren van de virtuele machine, zoals een installatiekopie van de virtuele machine, de grootte en de verificatieconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="db7c0-128">This configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, and authentication configuration.</span></span> <span data-ttu-id="db7c0-129">Als deze stap wordt uitgevoerd, wordt u gevraagd referenties op te geven.</span><span class="sxs-lookup"><span data-stu-id="db7c0-129">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="db7c0-130">De waarden die u invoert, worden geconfigureerd als de gebruikersnaam en het wachtwoord voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="db7c0-130">The values that you enter are configured as the user name and password for the virtual machine.</span></span>

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

<span data-ttu-id="db7c0-131">Maak de virtuele machine met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="db7c0-131">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-to-virtual-machine"></a><span data-ttu-id="db7c0-132">Verbinding maken met de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="db7c0-132">Connect to virtual machine</span></span>

<span data-ttu-id="db7c0-133">Wanneer de implementatie is voltooid, maakt u via een extern bureaublad verbinding met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="db7c0-133">After the deployment has completed, create a remote desktop connection with the virtual machine.</span></span>

<span data-ttu-id="db7c0-134">Gebruik de opdracht [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) om het openbare IP-adres van de virtuele machine te retourneren.</span><span class="sxs-lookup"><span data-stu-id="db7c0-134">Use the [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command to return the public IP address of the virtual machine.</span></span> <span data-ttu-id="db7c0-135">Noteer dit IP-adres zodat u vanuit uw browser verbinding kunt maken met het adres om webverbindingen te testen.</span><span class="sxs-lookup"><span data-stu-id="db7c0-135">Take note of this IP Address so you can connect to it with your browser to test web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="db7c0-136">Gebruik de volgende opdracht om een sessie met een extern bureaublad te starten voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="db7c0-136">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="db7c0-137">Vervang het IP-adres door het *publicIPAddress* van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="db7c0-137">Replace the IP address with the *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="db7c0-138">Wanneer u hierom wordt gevraagd, typt u de referenties die zijn gebruikt bij het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="db7c0-138">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a><span data-ttu-id="db7c0-139">IIS installeren met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="db7c0-139">Install IIS via PowerShell</span></span>

<span data-ttu-id="db7c0-140">U bent nu aangemeld bij de VM van Azure en er is nog maar één regel code van PowerShell nodig om IIS te installeren en de regel voor de lokale firewall in te schakelen om webverkeer toe te staan.</span><span class="sxs-lookup"><span data-stu-id="db7c0-140">Now that you have logged in to the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="db7c0-141">Open een PowerShell-prompt en voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="db7c0-141">Open a PowerShell prompt and run the following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="db7c0-142">De welkomstpagina van IIS weergeven</span><span class="sxs-lookup"><span data-stu-id="db7c0-142">View the IIS welcome page</span></span>

<span data-ttu-id="db7c0-143">Nu IIS is geïnstalleerd en poort 80 op de virtuele machine is geopend voor toegang vanaf internet, kunt u een webbrowser van uw keuze gebruiken om de standaardwelkomstpagina van IIS weer te geven.</span><span class="sxs-lookup"><span data-stu-id="db7c0-143">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span></span> <span data-ttu-id="db7c0-144">Zorg ervoor dat u de standaardpagina bezoekt met het *publicIpAddress* dat u hierboven hebt gedocumenteerd.</span><span class="sxs-lookup"><span data-stu-id="db7c0-144">Be sure to use the *publicIpAddress* you documented above to visit the default page.</span></span> 

![Standaardsite van IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="db7c0-146">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="db7c0-146">Clean up resources</span></span>

<span data-ttu-id="db7c0-147">U kunt de opdracht [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) gebruiken om de resourcegroep, de VM en alle gerelateerde resources te verwijderen wanneer u ze niet meer nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="db7c0-147">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="db7c0-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="db7c0-148">Next steps</span></span>

<span data-ttu-id="db7c0-149">In deze Snel starten hebt u een eenvoudige virtuele machine geïmplementeerd, een netwerkbeveiligingsgroepregel gemaakt en een webserver geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="db7c0-149">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="db7c0-150">Voor meer informatie over virtuele machines in Azure, gaat u verder met de zelfstudie voor virtuele Windows-machines.</span><span class="sxs-lookup"><span data-stu-id="db7c0-150">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="db7c0-151">Zelfstudies over virtuele Windows-machines</span><span class="sxs-lookup"><span data-stu-id="db7c0-151">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
