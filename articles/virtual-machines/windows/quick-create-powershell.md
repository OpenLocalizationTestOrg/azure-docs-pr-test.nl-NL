---
title: Quick Start - aaaAzure maken Windows VM PowerShell | Microsoft Docs
description: Snel een virtuele Windows-machines met PowerShell meer toocreate
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
ms.openlocfilehash: 5e92435bf7ee443a01c158fed91c356363e2f425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a><span data-ttu-id="61ed5-103">Een virtuele Windows-machine maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="61ed5-103">Create a Windows virtual machine with PowerShell</span></span>

<span data-ttu-id="61ed5-104">Hello Azure PowerShell-module is gebruikte toocreate en Azure-resources te beheren vanaf Hallo PowerShell-opdrachtregel of in scripts.</span><span class="sxs-lookup"><span data-stu-id="61ed5-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="61ed5-105">Deze handleiding gegevens met behulp van PowerShell toocreate en Azure virtuele machine met Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="61ed5-105">This guide details using PowerShell toocreate and Azure virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="61ed5-106">Zodra de implementatie is voltooid, we toohello server verbinden en IIS installeren.</span><span class="sxs-lookup"><span data-stu-id="61ed5-106">Once deployment is complete, we connect toohello server and install IIS.</span></span>  

<span data-ttu-id="61ed5-107">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="61ed5-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="61ed5-108">Deze snel starten vereist hello Azure PowerShell-moduleversie 3,6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="61ed5-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="61ed5-109">Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="61ed5-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="61ed5-110">Als u tooinstall of upgrade nodig hebt, raadpleegt u [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="61ed5-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="61ed5-111">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="61ed5-111">Log in tooAzure</span></span>

<span data-ttu-id="61ed5-112">Meld u bij de Azure-abonnement met Hallo tooyour `Login-AzureRmAccount` opdracht in en volg Hallo op het scherm instructies.</span><span class="sxs-lookup"><span data-stu-id="61ed5-112">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="61ed5-113">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="61ed5-113">Create resource group</span></span>

<span data-ttu-id="61ed5-114">Maak een Azure-resourcegroep met de opdracht [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="61ed5-114">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="61ed5-115">Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="61ed5-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a><span data-ttu-id="61ed5-116">Netwerkresources maken</span><span class="sxs-lookup"><span data-stu-id="61ed5-116">Create networking resources</span></span>

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a><span data-ttu-id="61ed5-117">Maak een virtueel netwerk, subnet en een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="61ed5-117">Create a virtual network, subnet, and a public IP address.</span></span> 
<span data-ttu-id="61ed5-118">Deze resources zijn gebruikte tooprovide network connectivity toohello virtuele machine en verbindt u deze toohello internet.</span><span class="sxs-lookup"><span data-stu-id="61ed5-118">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

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

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="61ed5-119">Maak een netwerkbeveiligingsgroep en een regel voor de netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="61ed5-119">Create a network security group and a network security group rule.</span></span> 
<span data-ttu-id="61ed5-120">netwerkbeveiligingsgroep Hallo beveiligt Hallo virtuele machine met behulp van regels voor binnenkomende en uitgaande.</span><span class="sxs-lookup"><span data-stu-id="61ed5-120">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="61ed5-121">In dit geval is er een binnenkomende regel gemaakt voor poort 3389, waarmee binnenkomende verbindingen met een extern bureaublad worden toegestaan.</span><span class="sxs-lookup"><span data-stu-id="61ed5-121">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span> <span data-ttu-id="61ed5-122">Tevens willen we toocreate een inkomende regel voor poort 80, waardoor inkomend webverkeer.</span><span class="sxs-lookup"><span data-stu-id="61ed5-122">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

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

### <a name="create-a-network-card-for-hello-virtual-machine"></a><span data-ttu-id="61ed5-123">Maak een netwerkkaart voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="61ed5-123">Create a network card for hello virtual machine.</span></span> 
<span data-ttu-id="61ed5-124">Maken van een netwerkkaart met [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="61ed5-124">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="61ed5-125">Hallo netwerkkaart verbindt Hallo tooa subnet met virtuele machines, netwerkbeveiligingsgroep en openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="61ed5-125">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="61ed5-126">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="61ed5-126">Create virtual machine</span></span>

<span data-ttu-id="61ed5-127">Maak een virtuele-machineconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="61ed5-127">Create a virtual machine configuration.</span></span> <span data-ttu-id="61ed5-128">Deze configuratie omvat Hallo-instellingen die worden gebruikt bij het implementeren van Hallo virtuele machine, zoals de configuratie van een virtuele machine-installatiekopie, grootte en verificatie.</span><span class="sxs-lookup"><span data-stu-id="61ed5-128">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span> <span data-ttu-id="61ed5-129">Als deze stap wordt uitgevoerd, wordt u gevraagd referenties op te geven.</span><span class="sxs-lookup"><span data-stu-id="61ed5-129">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="61ed5-130">Hallo-waarden die u invoert worden geconfigureerd als Hallo-gebruikersnaam en wachtwoord voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="61ed5-130">hello values that you enter are configured as hello user name and password for hello virtual machine.</span></span>

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

<span data-ttu-id="61ed5-131">Maak Hallo virtuele machine met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="61ed5-131">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="61ed5-132">Verbinding maken met toovirtual machine</span><span class="sxs-lookup"><span data-stu-id="61ed5-132">Connect toovirtual machine</span></span>

<span data-ttu-id="61ed5-133">Nadat het Hallo-implementatie is voltooid, maakt u een verbinding met extern bureaublad met Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="61ed5-133">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="61ed5-134">Gebruik Hallo [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) opdracht tooreturn Hallo openbaar IP-adres van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="61ed5-134">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="61ed5-135">Noteer dit IP-adres zodat tooit verbinding met uw browser tootest webverbindingen mogelijk in een toekomstige stap maken kunnen.</span><span class="sxs-lookup"><span data-stu-id="61ed5-135">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="61ed5-136">Gebruik Hallo volgende opdracht toocreate een extern-bureaubladsessie met Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="61ed5-136">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="61ed5-137">Hallo IP-adres vervangen door Hallo *publicIPAddress* van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="61ed5-137">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="61ed5-138">Wanneer u wordt gevraagd, voert u Hallo-referenties gebruikt bij het maken van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="61ed5-138">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a><span data-ttu-id="61ed5-139">IIS installeren met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="61ed5-139">Install IIS via PowerShell</span></span>

<span data-ttu-id="61ed5-140">Nu dat u hebt geregistreerd in Azure VM toohello, kunt u één regel PowerShell tooinstall IIS gebruiken en Hallo lokale firewall regel tooallow-webverkeer inschakelen.</span><span class="sxs-lookup"><span data-stu-id="61ed5-140">Now that you have logged in toohello Azure VM, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="61ed5-141">Open een PowerShell-prompt en Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="61ed5-141">Open a PowerShell prompt and run hello following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="61ed5-142">Weergave Hallo IIS-welkomstpagina</span><span class="sxs-lookup"><span data-stu-id="61ed5-142">View hello IIS welcome page</span></span>

<span data-ttu-id="61ed5-143">Met IIS is geïnstalleerd en poort 80 is nu open op de virtuele machine uit Hallo Internet, kunt u een webbrowser van uw keuze tooview Hallo IIS standaardwelkomstpagina.</span><span class="sxs-lookup"><span data-stu-id="61ed5-143">With IIS installed and port 80 now open on your VM from hello Internet, you can use a web browser of your choice tooview hello default IIS welcome page.</span></span> <span data-ttu-id="61ed5-144">Ervoor toouse Hallo worden *publicIpAddress* u hiervoor toovisit Hallo standaardpagina beschreven.</span><span class="sxs-lookup"><span data-stu-id="61ed5-144">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![Standaardsite van IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="61ed5-146">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="61ed5-146">Clean up resources</span></span>

<span data-ttu-id="61ed5-147">Wanneer deze niet langer nodig is, kunt u Hallo [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="61ed5-147">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="61ed5-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="61ed5-148">Next steps</span></span>

<span data-ttu-id="61ed5-149">In deze Snel starten hebt u een eenvoudige virtuele machine geïmplementeerd, een netwerkbeveiligingsgroepregel gemaakt en een webserver geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="61ed5-149">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="61ed5-150">toolearn meer informatie over virtuele machines in Azure, blijven toohello zelfstudie voor VM's van Windows.</span><span class="sxs-lookup"><span data-stu-id="61ed5-150">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="61ed5-151">Zelfstudies over virtuele Windows-machines</span><span class="sxs-lookup"><span data-stu-id="61ed5-151">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
