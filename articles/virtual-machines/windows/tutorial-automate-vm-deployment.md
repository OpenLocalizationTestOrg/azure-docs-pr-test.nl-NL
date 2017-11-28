---
title: een Windows-VM in Azure aaaCustomize | Microsoft Docs
description: Meer informatie over hoe toouse Hallo extensie voor aangepaste scripts en Sleutelkluis toocustomize Windows virtuele machines in Azure
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
ms.openlocfilehash: c03b2bb6d70875134c63ea2fe4c2e2c1777c2188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="b9e0e-103">Hoe toocustomize virtuele Windows-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="b9e0e-103">How toocustomize a Windows virtual machine in Azure</span></span>
<span data-ttu-id="b9e0e-104">tooconfigure virtuele machines (VM's) in een snelle en consistente manier, een vorm van automatisering is doorgaans gewenste.</span><span class="sxs-lookup"><span data-stu-id="b9e0e-104">tooconfigure virtual machines (VMs) in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="b9e0e-105">Een algemene methode toocustomize een virtuele machine van Windows is toouse [aangepast Script uitbreiding voor Windows](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="b9e0e-105">A common approach toocustomize a Windows VM is toouse [Custom Script Extension for Windows](extensions-customscript.md).</span></span> <span data-ttu-id="b9e0e-106">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="b9e0e-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b9e0e-107">Hallo aangepaste Scriptextensie tooinstall IIS gebruiken</span><span class="sxs-lookup"><span data-stu-id="b9e0e-107">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="b9e0e-108">Een virtuele machine die gebruikmaakt van de aangepaste Scriptextensie Hallo maken</span><span class="sxs-lookup"><span data-stu-id="b9e0e-108">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="b9e0e-109">Een actieve IIS-site weergeven nadat de Hallo-uitbreiding is toegepast</span><span class="sxs-lookup"><span data-stu-id="b9e0e-109">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="b9e0e-110">Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="b9e0e-110">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="b9e0e-111">Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="b9e0e-111">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="b9e0e-112">Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="b9e0e-112">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="custom-script-extension-overview"></a><span data-ttu-id="b9e0e-113">Overzicht van de extensie aangepast script</span><span class="sxs-lookup"><span data-stu-id="b9e0e-113">Custom script extension overview</span></span>
<span data-ttu-id="b9e0e-114">Hallo aangepaste Scriptextensie worden gedownload en scripts uitgevoerd op Azure Virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b9e0e-114">hello Custom Script Extension downloads and executes scripts on Azure VMs.</span></span> <span data-ttu-id="b9e0e-115">Deze uitbreiding is nuttig voor post-implementatieconfiguratie, software-installatie of een andere configuratie / beheertaak.</span><span class="sxs-lookup"><span data-stu-id="b9e0e-115">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="b9e0e-116">Scripts kunnen worden gedownload van Azure storage of GitHub, of toohello Azure-portal op extensie uitvoeringstijd.</span><span class="sxs-lookup"><span data-stu-id="b9e0e-116">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span>

<span data-ttu-id="b9e0e-117">Hallo-extensie voor aangepaste scripts worden geïntegreerd met Azure Resource Manager-sjablonen en kan ook worden uitgevoerd met hello Azure CLI, PowerShell, Azure-portal of hello Azure virtuele Machine REST-API.</span><span class="sxs-lookup"><span data-stu-id="b9e0e-117">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="b9e0e-118">U kunt Hallo aangepaste Scriptextensie gebruiken met Windows- en Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="b9e0e-118">You can use hello Custom Script Extension with both Windows and Linux VMs.</span></span>


## <a name="create-virtual-machine"></a><span data-ttu-id="b9e0e-119">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="b9e0e-119">Create virtual machine</span></span>
<span data-ttu-id="b9e0e-120">Voordat u een virtuele machine maken kunt, maakt u een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="b9e0e-120">Before you can create a VM, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="b9e0e-121">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupAutomate* in Hallo *EastUS* locatie:</span><span class="sxs-lookup"><span data-stu-id="b9e0e-121">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

<span data-ttu-id="b9e0e-122">Stel dat een beheerder gebruikersnaam en wachtwoord voor Hallo VM's met [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="b9e0e-122">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="b9e0e-123">Nu kunt u de virtuele machine met Hallo [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="b9e0e-123">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="b9e0e-124">Hallo volgende voorbeeld maakt Hallo vereist virtuele netwerkonderdelen, Hallo OS-configuratie, en maakt vervolgens een virtuele machine met de naam *myVM*:</span><span class="sxs-lookup"><span data-stu-id="b9e0e-124">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

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

<span data-ttu-id="b9e0e-125">Het duurt enkele minuten duren voordat het Hallo-resources en VM-toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b9e0e-125">It takes a few minutes for hello resources and VM toobe created.</span></span>


## <a name="automate-iis-install"></a><span data-ttu-id="b9e0e-126">IIS-installatie automatiseren</span><span class="sxs-lookup"><span data-stu-id="b9e0e-126">Automate IIS install</span></span>
<span data-ttu-id="b9e0e-127">Gebruik [Set AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall Hallo extensie voor aangepaste scripts.</span><span class="sxs-lookup"><span data-stu-id="b9e0e-127">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="b9e0e-128">Hallo-extensie wordt uitgevoerd `powershell Add-WindowsFeature Web-Server` tooinstall Hallo IIS-webserver en klik vervolgens op updates Hallo *Default.htm* pagina tooshow Hallo hostnaam Hallo VM:</span><span class="sxs-lookup"><span data-stu-id="b9e0e-128">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

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


## <a name="test-web-site"></a><span data-ttu-id="b9e0e-129">Test-website</span><span class="sxs-lookup"><span data-stu-id="b9e0e-129">Test web site</span></span>
<span data-ttu-id="b9e0e-130">Hallo openbare IP-adres van de load balancer met verkrijgen [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="b9e0e-130">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="b9e0e-131">Hallo volgende voorbeeld Hallo IP-adres krijgt voor *myPublicIP* eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="b9e0e-131">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

<span data-ttu-id="b9e0e-132">Vervolgens kunt u in de webbrowser tooa Hallo openbaar IP-adres invoeren.</span><span class="sxs-lookup"><span data-stu-id="b9e0e-132">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="b9e0e-133">Hallo-website wordt weergegeven, inclusief Hallo hostnaam Hallo VM die Hallo load balancer gedistribueerde tooas verkeer in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="b9e0e-133">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Actieve IIS-website](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a><span data-ttu-id="b9e0e-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b9e0e-135">Next steps</span></span>

<span data-ttu-id="b9e0e-136">In deze zelfstudie maakt geautomatiseerde u Hallo IIS op een virtuele machine installeren.</span><span class="sxs-lookup"><span data-stu-id="b9e0e-136">In this tutorial, you automated hello IIS install on a VM.</span></span> <span data-ttu-id="b9e0e-137">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="b9e0e-137">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b9e0e-138">Hallo aangepaste Scriptextensie tooinstall IIS gebruiken</span><span class="sxs-lookup"><span data-stu-id="b9e0e-138">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="b9e0e-139">Een virtuele machine die gebruikmaakt van de aangepaste Scriptextensie Hallo maken</span><span class="sxs-lookup"><span data-stu-id="b9e0e-139">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="b9e0e-140">Een actieve IIS-site weergeven nadat de Hallo-uitbreiding is toegepast</span><span class="sxs-lookup"><span data-stu-id="b9e0e-140">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="b9e0e-141">Hoe gaan van de volgende zelfstudie toolearn toohello toocreate aangepaste VM-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="b9e0e-141">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b9e0e-142">Aangepaste VM-installatiekopieën maken</span><span class="sxs-lookup"><span data-stu-id="b9e0e-142">Create custom VM images</span></span>](./tutorial-custom-images.md)
