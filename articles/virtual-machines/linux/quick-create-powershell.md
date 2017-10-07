---
title: aaaAzure Quick Start - VM PowerShell maken | Microsoft Docs
description: Snel een virtuele Linux-machines met PowerShell meer toocreate
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: f05ea7fedafe4fda660dc6084ae57ebf9dced473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a><span data-ttu-id="8dcc8-103">Een virtuele Linux-machine maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="8dcc8-103">Create a Linux virtual machine with PowerShell</span></span>

<span data-ttu-id="8dcc8-104">Hello Azure PowerShell-module is gebruikte toocreate en Azure-resources te beheren vanaf Hallo PowerShell-opdrachtregel of in scripts.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="8dcc8-105">Deze handleiding details hello Azure PowerShell-module toodeploy met een virtuele machine met Ubuntu server.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-105">This guide details using hello Azure PowerShell module toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="8dcc8-106">Zodra Hallo-server is geïmplementeerd, een SSH-verbinding wordt gemaakt en een NGINX-webserver is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="8dcc8-107">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="8dcc8-108">Deze snel starten vereist hello Azure PowerShell-moduleversie 3,6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="8dcc8-109">Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="8dcc8-110">Als u tooinstall of upgrade nodig hebt, raadpleegt u [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="8dcc8-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="8dcc8-111">Ten slotte een openbare SSH sleutel met de naam van de Hallo *id_rsa.pub* toobe opgeslagen in Hallo moet *SSH* map van uw Windows-gebruikersprofiel.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-111">Finally, a public SSH key with hello name *id_rsa.pub* needs toobe stored in hello *.ssh* directory of your Windows user profile.</span></span> <span data-ttu-id="8dcc8-112">Zie voor gedetailleerde informatie over het maken van SSH-sleutels voor Azure [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (SSH-sleutels maken voor Azure).</span><span class="sxs-lookup"><span data-stu-id="8dcc8-112">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="8dcc8-113">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="8dcc8-113">Log in tooAzure</span></span>

<span data-ttu-id="8dcc8-114">Meld u bij de Azure-abonnement met Hallo tooyour `Login-AzureRmAccount` opdracht in en volg Hallo op het scherm instructies.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-114">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="8dcc8-115">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="8dcc8-115">Create resource group</span></span>

<span data-ttu-id="8dcc8-116">Maak een Azure-resourcegroep met de opdracht [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="8dcc8-116">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="8dcc8-117">Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a><span data-ttu-id="8dcc8-118">Netwerkresources maken</span><span class="sxs-lookup"><span data-stu-id="8dcc8-118">Create networking resources</span></span>

<span data-ttu-id="8dcc8-119">Maak een virtueel netwerk, subnet en een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-119">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="8dcc8-120">Deze resources zijn gebruikte tooprovide network connectivity toohello virtuele machine en verbindt u deze toohello internet.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-120">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location eastus `
-Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location eastus `
-AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

<span data-ttu-id="8dcc8-121">Maak een netwerkbeveiligingsgroep en een regel voor de netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-121">Create a network security group and a network security group rule.</span></span> <span data-ttu-id="8dcc8-122">netwerkbeveiligingsgroep Hallo beveiligt Hallo virtuele machine met behulp van regels voor binnenkomende en uitgaande.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-122">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="8dcc8-123">In dit geval is er een binnenkomende regel gemaakt voor poort 22, waarmee binnenkomende SSH-verbindingen worden toegestaan.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-123">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span></span> <span data-ttu-id="8dcc8-124">Tevens willen we toocreate een inkomende regel voor poort 80, waardoor inkomend webverkeer.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-124">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleSSH  -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location eastus `
-Name myNetworkSecurityGroup -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

<span data-ttu-id="8dcc8-125">Maken van een netwerkkaart met [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-125">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="8dcc8-126">Hallo netwerkkaart verbindt Hallo tooa subnet met virtuele machines, netwerkbeveiligingsgroep en openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-126">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="8dcc8-127">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="8dcc8-127">Create virtual machine</span></span>

<span data-ttu-id="8dcc8-128">Maak een virtuele-machineconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-128">Create a virtual machine configuration.</span></span> <span data-ttu-id="8dcc8-129">Deze configuratie omvat Hallo-instellingen die worden gebruikt bij het implementeren van Hallo virtuele machine, zoals de configuratie van een virtuele machine-installatiekopie, grootte en verificatie.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-129">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span>

```powershell
# Define a credential object
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("azureuser", $securePassword)

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Linux -ComputerName myVM -Credential $cred -DisablePasswordAuthentication | `
Set-AzureRmVMSourceImage -PublisherName Canonical -Offer UbuntuServer -Skus 14.04.2-LTS -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmconfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"
```

<span data-ttu-id="8dcc8-130">Maak Hallo virtuele machine met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="8dcc8-130">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="8dcc8-131">Verbinding maken met toovirtual machine</span><span class="sxs-lookup"><span data-stu-id="8dcc8-131">Connect toovirtual machine</span></span>

<span data-ttu-id="8dcc8-132">Nadat het Hallo-implementatie is voltooid, moet u een SSH-verbinding maken met Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-132">After hello deployment has completed, create an SSH connection with hello virtual machine.</span></span>

<span data-ttu-id="8dcc8-133">Gebruik Hallo [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) opdracht tooreturn Hallo openbaar IP-adres van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-133">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="8dcc8-134">Gebruikte Hallo volgende opdracht uit een systeem met SSH geïnstalleerd, tooconnect toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-134">From a system with SSH installed, used hello following command tooconnect toohello virtual machine.</span></span> <span data-ttu-id="8dcc8-135">Als op Windows, werkt [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) gebruikte toocreate Hallo verbinding kan worden.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-135">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used toocreate hello connection.</span></span> 

```bash 
ssh <Public IP Address>
```

<span data-ttu-id="8dcc8-136">Wanneer u wordt gevraagd, Hallo aanmeldingsnaam is *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-136">When prompted, hello login user name is *azureuser*.</span></span> <span data-ttu-id="8dcc8-137">Als u een wachtwoordzin is ingevoerd bij het maken van SSH-sleutels, moet u dit ook tooenter.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-137">If a passphrase was entered when creating SSH keys, you need tooenter this as well.</span></span>


## <a name="install-nginx"></a><span data-ttu-id="8dcc8-138">NGINX installeren</span><span class="sxs-lookup"><span data-stu-id="8dcc8-138">Install NGINX</span></span>

<span data-ttu-id="8dcc8-139">Gebruik Hallo volgende scriptbronnen tooupdate pakket bash en installeer de meest recente NGINX-pakket Hallo.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-139">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a><span data-ttu-id="8dcc8-140">Hallo-NGIX welkomstpagina weergeven</span><span class="sxs-lookup"><span data-stu-id="8dcc8-140">View hello NGIX welcome page</span></span>

<span data-ttu-id="8dcc8-141">U kunt een webbrowser van uw keuze tooview hello NGINX standaardwelkomstpagina gebruiken van NGINX geïnstalleerd en de poort 80 is nu open op de virtuele machine van de Internet - Hallo.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-141">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="8dcc8-142">Worden ervoor toouse Hallo openbaar IP-adres die u hiervoor toovisit Hallo standaardpagina beschreven.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-142">Be sure toouse hello public IP address you documented above toovisit hello default page.</span></span> 

![Standaardsite van NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="8dcc8-144">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="8dcc8-144">Clean up resources</span></span>

<span data-ttu-id="8dcc8-145">Wanneer deze niet langer nodig is, kunt u Hallo [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-145">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="8dcc8-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8dcc8-146">Next steps</span></span>

<span data-ttu-id="8dcc8-147">In deze Snel starten hebt u een eenvoudige virtuele machine geïmplementeerd, een netwerkbeveiligingsgroepregel gemaakt en een webserver geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-147">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="8dcc8-148">toolearn meer informatie over virtuele machines in Azure, blijven toohello zelfstudie voor virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="8dcc8-148">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8dcc8-149">Zelfstudies over virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="8dcc8-149">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
