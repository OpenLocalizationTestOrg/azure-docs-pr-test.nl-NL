---
title: aaaAzure virtuele netwerken en virtuele Machines van Windows | Microsoft Docs
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
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="a5bf7-103">Virtuele Azure-netwerken en virtuele Machines van Windows met Azure PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="a5bf7-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="a5bf7-104">Azure netwerken virtuele Azure-machines gebruiken voor interne en externe communicatie.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="a5bf7-105">In deze zelfstudie maakt u meerdere virtuele machines (VM's) in een virtueel netwerk maken en netwerkconnectiviteit tussen deze twee configureren.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="a5bf7-106">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="a5bf7-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a5bf7-107">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="a5bf7-107">Create a virtual network</span></span>
> * <span data-ttu-id="a5bf7-108">Subnetten virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="a5bf7-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="a5bf7-109">Het netwerkverkeer met Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="a5bf7-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="a5bf7-110">Regels voor het netwerkverkeer in actie weergeven</span><span class="sxs-lookup"><span data-stu-id="a5bf7-110">View traffic rules in action</span></span>

<span data-ttu-id="a5bf7-111">Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="a5bf7-112">Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="a5bf7-113">Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="a5bf7-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="a5bf7-114">VNet maken</span><span class="sxs-lookup"><span data-stu-id="a5bf7-114">Create VNet</span></span>

<span data-ttu-id="a5bf7-115">Een VNet is een weergave van uw eigen netwerk in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-115">A VNet is a representation of your own network in hello cloud.</span></span> <span data-ttu-id="a5bf7-116">Een VNet is een logische isolatie van hello Azure cloud toegewezen tooyour-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-116">A VNet is a logical isolation of hello Azure cloud dedicated tooyour subscription.</span></span> <span data-ttu-id="a5bf7-117">Binnen een VNet vindt u subnetten, regels voor connectiviteit toothose subnetten en verbindingen van Hallo VMs toohello subnetten.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-117">Within a VNet, you find subnets, rules for connectivity toothose subnets, and connections from hello VMs toohello subnets.</span></span>

<span data-ttu-id="a5bf7-118">Voordat u een andere Azure-resources maken kunt, moet u toocreate een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="a5bf7-118">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="a5bf7-119">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myRGNetwork* in Hallo *EastUS* locatie:</span><span class="sxs-lookup"><span data-stu-id="a5bf7-119">hello following example creates a resource group named *myRGNetwork* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="a5bf7-120">Een subnet is een onderliggende resource van een VNet en helpt bij het segmenten van adresruimten binnen een CIDR-blok met behulp van IP-adresvoorvoegsels definiëren.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="a5bf7-121">NIC's kunnen worden toegevoegd, toosubnets en verbonden tooVMs, tegelijk connectiviteit biedt voor verschillende werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-121">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="a5bf7-122">Maak een subnet met [nieuw AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="a5bf7-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="a5bf7-123">Maak een VNET met de naam *myVNet* met *myFrontendSubnet* met [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="a5bf7-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="a5bf7-124">Front-virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="a5bf7-124">Create front-end VM</span></span>

<span data-ttu-id="a5bf7-125">Voor een VM-toocommunicate in een VNet moet de virtuele netwerkinterface (NIC).</span><span class="sxs-lookup"><span data-stu-id="a5bf7-125">For a VM toocommunicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="a5bf7-126">Hallo *myFrontendVM* is toegankelijk vanuit Hallo internet, dus u moet ook een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-126">hello *myFrontendVM* is accessed from hello internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="a5bf7-127">Maken van een openbaar IP-adres met [nieuw AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="a5bf7-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="a5bf7-128">Maak een NIC met [nieuwe AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="a5bf7-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="a5bf7-129">Stel Hallo-gebruikersnaam en wachtwoord nodig voor Hallo-beheerdersaccount op Hallo VM met [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="a5bf7-129">Set hello username and password needed for hello administrator account on hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="a5bf7-130">Maken van Hallo virtuele machines met [nieuw AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Toevoegen AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), en [nieuwe-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="a5bf7-130">Create hello VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

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

## <a name="install-web-server"></a><span data-ttu-id="a5bf7-131">Webserver installeren</span><span class="sxs-lookup"><span data-stu-id="a5bf7-131">Install web server</span></span>

<span data-ttu-id="a5bf7-132">U kunt IIS installeren op *myFrontendVM* met behulp van een extern bureaublad-sessiehost.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="a5bf7-133">U moet tooget Hallo openbare IP-adres van VM tooaccess Hallo deze.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-133">You need tooget hello public IP address of hello VM tooaccess it.</span></span>

<span data-ttu-id="a5bf7-134">U krijgt Hallo openbare IP-adres van *myFrontendVM* met [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="a5bf7-134">You can get hello public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="a5bf7-135">Hallo volgende voorbeeld Hallo IP-adres krijgt voor *myPublicIPAddress* eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="a5bf7-135">hello following example obtains hello IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="a5bf7-136">Noteer dit IP-adres zodat u deze in toekomstige stappen gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="a5bf7-137">Gebruik Hallo volgende opdracht toocreate een extern-bureaubladsessie met *myFrontendVM*.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-137">Use hello following command toocreate a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="a5bf7-138">Vervang  *<publicIPAddress>*  met Hallo-adres dat u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-138">Replace *<publicIPAddress>* with hello address that you previously recorded.</span></span> <span data-ttu-id="a5bf7-139">Voer desgevraagd Hallo referenties gebruikt wanneer u Hallo VM gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-139">When prompted, enter hello credentials used when you created hello VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="a5bf7-140">Nu dat u hebt geregistreerd te*myFrontendVM*, kunt u één regel PowerShell tooinstall IIS gebruiken en Hallo lokale firewall regel tooallow-webverkeer inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-140">Now that you have logged in too*myFrontendVM*, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="a5bf7-141">Open een PowerShell-prompt en Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a5bf7-141">Open a PowerShell prompt and run hello following command:</span></span>

<span data-ttu-id="a5bf7-142">Gebruik [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun Hallo extensie voor aangepaste scripts die Hallo IIS-webserver installeert:</span><span class="sxs-lookup"><span data-stu-id="a5bf7-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello custom script extension that installs hello IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="a5bf7-143">U kunt nu Hallo openbare IP-adres toobrowse toohello VM toosee Hallo ISS-site gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-143">Now you can use hello public IP address toobrowse toohello VM toosee hello IIS site.</span></span>

![Standaardsite van IIS](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="a5bf7-145">Interne verkeer beheren</span><span class="sxs-lookup"><span data-stu-id="a5bf7-145">Manage internal traffic</span></span>

<span data-ttu-id="a5bf7-146">Een netwerkbeveiligingsgroep (NSG) bevat een lijst met regels voor toestaan of weigeren netwerkverkeer tooresources verbonden tooa VNet.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooa VNet.</span></span> <span data-ttu-id="a5bf7-147">Nsg's kunnen worden gekoppeld toosubnets of afzonderlijke NIC's gekoppeld tooVMs.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-147">NSGs can be associated toosubnets or individual NICs attached tooVMs.</span></span> <span data-ttu-id="a5bf7-148">Openen en sluiten tooVMs toegang via poorten wordt gedaan met behulp van NSG-regels.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-148">Opening or closing access tooVMs through ports is done using NSG rules.</span></span> <span data-ttu-id="a5bf7-149">Tijdens het maken van *myFrontendVM*, binnenkomende poort 3389 automatisch voor RDP-verbinding is geopend.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="a5bf7-150">Interne communicatie van virtuele machines kan worden geconfigureerd met een NSG.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="a5bf7-151">In deze sectie leest u hoe een ander subnet in Hallo toocreate netwerk en een verbinding van een NSG tooit tooallow toewijzen *myFrontendVM* te*myBackendVM* op poort 1433.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-151">In this section, you learn how toocreate an additional subnet in hello network and assign an NSG tooit tooallow a connection from *myFrontendVM* too*myBackendVM* on port 1433.</span></span> <span data-ttu-id="a5bf7-152">Hallo-subnet wordt vervolgens toohello VM toegewezen wanneer deze wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-152">hello subnet is then assigned toohello VM when it is created.</span></span>

<span data-ttu-id="a5bf7-153">U kunt interne verkeer te beperken*myBackendVM* alleen *myFrontendVM* door het maken van een NSG voor subnet van Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-153">You can limit internal traffic too*myBackendVM* from only *myFrontendVM* by creating an NSG for hello back-end subnet.</span></span> <span data-ttu-id="a5bf7-154">Hallo volgende voorbeeld maakt u een NSG regel voor licentiecontrole *myBackendNSGRule* met [nieuw AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span><span class="sxs-lookup"><span data-stu-id="a5bf7-154">hello following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

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

<span data-ttu-id="a5bf7-155">Toevoegen van een netwerkbeveiligingsgroep met de naam *myBackendNSG* met [nieuw AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="a5bf7-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="a5bf7-156">Back-end subnet toevoegen</span><span class="sxs-lookup"><span data-stu-id="a5bf7-156">Add back-end subnet</span></span>

<span data-ttu-id="a5bf7-157">Add *myBackEndSubnet* te*myVNet* met [toevoegen AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="a5bf7-157">Add *myBackEndSubnet* too*myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

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

## <a name="create-back-end-vm"></a><span data-ttu-id="a5bf7-158">Back-end virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="a5bf7-158">Create back-end VM</span></span>

<span data-ttu-id="a5bf7-159">Hallo gemakkelijkste manier toocreate hello die back-end virtuele machine wordt met behulp van een installatiekopie van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-159">hello easiest way toocreate hello back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="a5bf7-160">Deze zelfstudie alleen Hallo VM maakt met de databaseserver hello, maar niet bevatten informatie over het Hallo-database te openen.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-160">This tutorial only creates hello VM with hello database server, but doesn't provide information about accessing hello database.</span></span>

<span data-ttu-id="a5bf7-161">Maak *myBackendNic*:</span><span class="sxs-lookup"><span data-stu-id="a5bf7-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="a5bf7-162">Hallo-gebruikersnaam en wachtwoord nodig voor Hallo-beheerdersaccount op Hallo VM met Get-Credential instellen:</span><span class="sxs-lookup"><span data-stu-id="a5bf7-162">Set hello username and password needed for hello administrator account on hello VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="a5bf7-163">Maak *myBackendVM*:</span><span class="sxs-lookup"><span data-stu-id="a5bf7-163">Create *myBackendVM*:</span></span>

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

<span data-ttu-id="a5bf7-164">Hallo-afbeelding die wordt gebruikt SQL Server is geïnstalleerd, maar niet in deze zelfstudie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-164">hello image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="a5bf7-165">Het is opgenomen tooshow u hoe u een VM toohandle-webverkeer en het beheer van een VM toohandle databases kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-165">It is included tooshow you how you can configure a VM toohandle web traffic and a VM toohandle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5bf7-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a5bf7-166">Next steps</span></span>

<span data-ttu-id="a5bf7-167">In deze zelfstudie hebt gemaakt en Azure-netwerken als verwante toovirtual machines beveiligd.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-167">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="a5bf7-168">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="a5bf7-168">Create a virtual network</span></span>
> * <span data-ttu-id="a5bf7-169">Subnetten virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="a5bf7-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="a5bf7-170">Het netwerkverkeer met Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="a5bf7-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="a5bf7-171">Regels voor het netwerkverkeer in actie weergeven</span><span class="sxs-lookup"><span data-stu-id="a5bf7-171">View traffic rules in action</span></span>

<span data-ttu-id="a5bf7-172">Ga toohello volgende zelfstudie toolearn over het controleren van het beveiligen van gegevens op virtuele machines met behulp van Azure backup.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-172">Advance toohello next tutorial toolearn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="a5bf7-173">.</span><span class="sxs-lookup"><span data-stu-id="a5bf7-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a5bf7-174">Back-up van Windows virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="a5bf7-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
