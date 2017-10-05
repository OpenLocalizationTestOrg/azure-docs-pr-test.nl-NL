---
title: Aanpassen van een Windows virtuele machine in Azure | Microsoft Docs
description: Informatie over het gebruik van de extensie voor aangepaste scripts en Sleutelkluis om aan te passen Windows virtuele machines in Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 3be58bf8afbcff018b2b0d69a0e08c2c9ab1fca7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-customize-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="db9af-103">Het aanpassen van een virtuele Windows-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="db9af-103">How to customize a Windows virtual machine in Azure</span></span>
<span data-ttu-id="db9af-104">Als u wilt configureren (virtuele machines) in een snelle en consistente manier, is een vorm van automatisering doorgaans gewenst.</span><span class="sxs-lookup"><span data-stu-id="db9af-104">To configure virtual machines (VMs) in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="db9af-105">Een gemeenschappelijke aanpak voor het aanpassen van een virtuele machine van Windows is met [aangepast Script uitbreiding voor Windows](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="db9af-105">A common approach to customize a Windows VM is to use [Custom Script Extension for Windows](extensions-customscript.md).</span></span> <span data-ttu-id="db9af-106">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="db9af-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="db9af-107">De extensie voor aangepaste scripts gebruiken voor het installeren van IIS</span><span class="sxs-lookup"><span data-stu-id="db9af-107">Use the Custom Script Extension to install IIS</span></span>
> * <span data-ttu-id="db9af-108">Een virtuele machine die gebruikmaakt van de aangepaste Scriptextensie maken</span><span class="sxs-lookup"><span data-stu-id="db9af-108">Create a VM that uses the Custom Script Extension</span></span>
> * <span data-ttu-id="db9af-109">Een actieve IIS-site weergeven nadat de uitbreiding is toegepast</span><span class="sxs-lookup"><span data-stu-id="db9af-109">View a running IIS site after the extension is applied</span></span>

<span data-ttu-id="db9af-110">Voor deze zelfstudie is moduleversie 3,6 of hoger van Azure PowerShell vereist.</span><span class="sxs-lookup"><span data-stu-id="db9af-110">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="db9af-111">Voer ` Get-Module -ListAvailable AzureRM` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="db9af-111">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="db9af-112">Als u upgraden wilt, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="db9af-112">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="custom-script-extension-overview"></a><span data-ttu-id="db9af-113">Overzicht van de extensie aangepast script</span><span class="sxs-lookup"><span data-stu-id="db9af-113">Custom script extension overview</span></span>
<span data-ttu-id="db9af-114">De aangepaste Scriptextensie downloads en scripts worden uitgevoerd op Azure Virtual machines.</span><span class="sxs-lookup"><span data-stu-id="db9af-114">The Custom Script Extension downloads and executes scripts on Azure VMs.</span></span> <span data-ttu-id="db9af-115">Deze uitbreiding is nuttig voor post-implementatieconfiguratie, software-installatie of een andere configuratie / beheertaak.</span><span class="sxs-lookup"><span data-stu-id="db9af-115">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="db9af-116">Scripts kunnen worden gedownload van Azure storage of GitHub, of naar de Azure portal op extensie uitvoeringstijd.</span><span class="sxs-lookup"><span data-stu-id="db9af-116">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span></span>

<span data-ttu-id="db9af-117">De aangepaste scriptextensie kan worden geïntegreerd met Azure Resource Manager-sjablonen en kan ook worden uitgevoerd met de Azure CLI, PowerShell, Azure-portal of de REST-API van Azure virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="db9af-117">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="db9af-118">U kunt de aangepaste Scriptextensie gebruiken met Windows- en Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="db9af-118">You can use the Custom Script Extension with both Windows and Linux VMs.</span></span>


## <a name="create-virtual-machine"></a><span data-ttu-id="db9af-119">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="db9af-119">Create virtual machine</span></span>
<span data-ttu-id="db9af-120">Voordat u een virtuele machine maken kunt, maakt u een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="db9af-120">Before you can create a VM, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="db9af-121">Het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroupAutomate* in de *EastUS* locatie:</span><span class="sxs-lookup"><span data-stu-id="db9af-121">The following example creates a resource group named *myResourceGroupAutomate* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

<span data-ttu-id="db9af-122">Stel dat een beheerder gebruikersnaam en wachtwoord voor de virtuele machines met [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="db9af-122">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="db9af-123">Nu kunt u de virtuele machine met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="db9af-123">Now you can create the VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="db9af-124">Het volgende voorbeeld maakt de vereiste virtuele netwerkonderdelen, de configuratie van het besturingssysteem, en maakt vervolgens een virtuele machine met de naam *myVM*:</span><span class="sxs-lookup"><span data-stu-id="db9af-124">The following example creates the required virtual network components, the OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName myResourceGroupAutomate -Location EastUS -VM $vmConfig
```

<span data-ttu-id="db9af-125">Het duurt enkele minuten duren voordat de resources en de VM moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="db9af-125">It takes a few minutes for the resources and VM to be created.</span></span>


## <a name="automate-iis-install"></a><span data-ttu-id="db9af-126">IIS-installatie automatiseren</span><span class="sxs-lookup"><span data-stu-id="db9af-126">Automate IIS install</span></span>
<span data-ttu-id="db9af-127">Gebruik [Set AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) voor het installeren van de aangepaste Scriptextensie.</span><span class="sxs-lookup"><span data-stu-id="db9af-127">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to install the Custom Script Extension.</span></span> <span data-ttu-id="db9af-128">De extensie wordt uitgevoerd `powershell Add-WindowsFeature Web-Server` voor het installeren van de IIS-webserver en updates van de *Default.htm* pagina voor het weergeven van de hostnaam van de virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="db9af-128">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver and then updates the *Default.htm* page to show the hostname of the VM:</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName myResourceGroupAutomate `
    -ExtensionName IIS `
    -VMName myVM `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
    -Location EastUS
```


## <a name="test-web-site"></a><span data-ttu-id="db9af-129">Test-website</span><span class="sxs-lookup"><span data-stu-id="db9af-129">Test web site</span></span>
<span data-ttu-id="db9af-130">Het openbare IP-adres van de load balancer met [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="db9af-130">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="db9af-131">Het volgende voorbeeld verkrijgt het IP-adres voor *myPublicIP* eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="db9af-131">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

<span data-ttu-id="db9af-132">Vervolgens kunt u het openbare IP-adres in invoeren aan een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="db9af-132">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="db9af-133">De website wordt weergegeven, inclusief de hostnaam van de virtuele machine die de load balancer verkeer naar het volgende voorbeeld gedistribueerde:</span><span class="sxs-lookup"><span data-stu-id="db9af-133">The website is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![Actieve IIS-website](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a><span data-ttu-id="db9af-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="db9af-135">Next steps</span></span>

<span data-ttu-id="db9af-136">In deze zelfstudie maakt automatisch u de IIS-installatie op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="db9af-136">In this tutorial, you automated the IIS install on a VM.</span></span> <span data-ttu-id="db9af-137">U leert hoe naar:</span><span class="sxs-lookup"><span data-stu-id="db9af-137">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="db9af-138">De extensie voor aangepaste scripts gebruiken voor het installeren van IIS</span><span class="sxs-lookup"><span data-stu-id="db9af-138">Use the Custom Script Extension to install IIS</span></span>
> * <span data-ttu-id="db9af-139">Een virtuele machine die gebruikmaakt van de aangepaste Scriptextensie maken</span><span class="sxs-lookup"><span data-stu-id="db9af-139">Create a VM that uses the Custom Script Extension</span></span>
> * <span data-ttu-id="db9af-140">Een actieve IIS-site weergeven nadat de uitbreiding is toegepast</span><span class="sxs-lookup"><span data-stu-id="db9af-140">View a running IIS site after the extension is applied</span></span>

<span data-ttu-id="db9af-141">Ga naar de volgende zelfstudie voor informatie over het maken van aangepaste installatiekopieën van virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="db9af-141">Advance to the next tutorial to learn how to create custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="db9af-142">Aangepaste VM-installatiekopieën maken</span><span class="sxs-lookup"><span data-stu-id="db9af-142">Create custom VM images</span></span>](./tutorial-custom-images.md)
