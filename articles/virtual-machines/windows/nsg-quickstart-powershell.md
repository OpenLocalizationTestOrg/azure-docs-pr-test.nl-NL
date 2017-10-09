---
title: aaaOpen poorten tooa VM die gebruikmaakt van Azure PowerShell | Microsoft Docs
description: Meer informatie over hoe tooopen een poort / maken van een eindpunt tooyour virtuele machine van Windows hello Azure resource manager deployment-modus en Azure PowerShell gebruiken
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a><span data-ttu-id="43d3e-103">Hoe tooopen poorten en eindpunten tooa virtuele machine in Azure met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="43d3e-103">How tooopen ports and endpoints tooa VM in Azure using PowerShell</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="43d3e-104">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="43d3e-104">Quick commands</span></span>
<span data-ttu-id="43d3e-105">toocreate een netwerkbeveiliging groeperen en ACL-regels moet u [Hallo meest recente versie van Azure PowerShell geïnstalleerd](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="43d3e-105">toocreate a Network Security Group and ACL rules you need [hello latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="43d3e-106">U kunt ook [u deze stappen uitvoert met behulp van Azure-portal Hallo](nsg-quickstart-portal.md).</span><span class="sxs-lookup"><span data-stu-id="43d3e-106">You can also [perform these steps using hello Azure portal](nsg-quickstart-portal.md).</span></span>

<span data-ttu-id="43d3e-107">Meld u bij tooyour Azure-account:</span><span class="sxs-lookup"><span data-stu-id="43d3e-107">Log in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="43d3e-108">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="43d3e-108">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="43d3e-109">Voorbeeld parameternamen opgenomen *myResourceGroup*, *myNetworkSecurityGroup*, en *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="43d3e-109">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="43d3e-110">Maak een regel met [nieuw AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="43d3e-110">Create a rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="43d3e-111">Hallo volgende voorbeeld maakt u een regel met naam *myNetworkSecurityGroupRule* tooallow *tcp* verkeer op poort *80*:</span><span class="sxs-lookup"><span data-stu-id="43d3e-111">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow *tcp* traffic on port *80*:</span></span>

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

<span data-ttu-id="43d3e-112">Maak vervolgens uw netwerk van een beveiligingsgroep met [nieuw AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) en toewijzen Hallo HTTP regel die u zojuist hebt gemaakt, als volgt.</span><span class="sxs-lookup"><span data-stu-id="43d3e-112">Next, create your Network Security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) and assign hello HTTP rule you just created as follows.</span></span> <span data-ttu-id="43d3e-113">Hallo volgende voorbeeld wordt een Netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="43d3e-113">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

<span data-ttu-id="43d3e-114">Nu gaan we uw Netwerkbeveiligingsgroep tooa subnet toewijzen.</span><span class="sxs-lookup"><span data-stu-id="43d3e-114">Now let's assign your Network Security Group tooa subnet.</span></span> <span data-ttu-id="43d3e-115">Hallo volgende voorbeeld wordt een bestaand virtueel netwerk met de naam *myVnet* toohello variabele *$vnet* met [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="43d3e-115">hello following example assigns an existing virtual network named *myVnet* toohello variable *$vnet* with [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

<span data-ttu-id="43d3e-116">De Netwerkbeveiligingsgroep koppelen aan uw subnet met [Set AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="43d3e-116">Associate your Network Security Group with your subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="43d3e-117">Hallo volgende voorbeeld wordt Hallo subnet met de naam *mySubnet* aan uw Netwerkbeveiligingsgroep:</span><span class="sxs-lookup"><span data-stu-id="43d3e-117">hello following example associates hello subnet named *mySubnet* with your Network Security Group:</span></span>

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="43d3e-118">Tot slot werkt uw virtuele netwerk met [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) om uw wijzigingen tootake effect:</span><span class="sxs-lookup"><span data-stu-id="43d3e-118">Finally, update your virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) in order for your changes tootake effect:</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="43d3e-119">Meer informatie over Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="43d3e-119">More information on Network Security Groups</span></span>
<span data-ttu-id="43d3e-120">Hallo-hier snelle opdrachten kunt u tooget up en wordt uitgevoerd met verkeer stromende tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="43d3e-120">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="43d3e-121">Netwerkbeveiligingsgroepen bieden veel handige functies en verfijning voor het beheren van toegang tot tooyour bronnen.</span><span class="sxs-lookup"><span data-stu-id="43d3e-121">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="43d3e-122">U kunt meer lezen over [hier maken van een Netwerkbeveiligingsgroep en ACL regels](tutorial-virtual-network.md#manage-internal-traffic).</span><span class="sxs-lookup"><span data-stu-id="43d3e-122">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#manage-internal-traffic).</span></span>

<span data-ttu-id="43d3e-123">Voor maximaal beschikbare webtoepassingen, moet u uw virtuele machines achter een Load Balancer van Azure plaatsen.</span><span class="sxs-lookup"><span data-stu-id="43d3e-123">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="43d3e-124">Hallo-taakverdeling verkeer tooVMs, met een Netwerkbeveiligingsgroep waarmee wordt verkeer gefilterd.</span><span class="sxs-lookup"><span data-stu-id="43d3e-124">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="43d3e-125">Zie voor meer informatie [hoe tooload saldo Linux virtuele machines in Azure toocreate een maximaal beschikbare toepassing](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="43d3e-125">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="43d3e-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="43d3e-126">Next steps</span></span>
<span data-ttu-id="43d3e-127">In dit voorbeeld moet u een eenvoudige regel tooallow HTTP-verkeer gemaakt.</span><span class="sxs-lookup"><span data-stu-id="43d3e-127">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="43d3e-128">Hier vindt u informatie over het maken van meer gedetailleerde omgevingen in Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="43d3e-128">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="43d3e-129">Overzicht van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="43d3e-129">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="43d3e-130">Wat is een netwerkbeveiligingsgroep (NSG)?</span><span class="sxs-lookup"><span data-stu-id="43d3e-130">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="43d3e-131">Overzicht van Azure Resource Manager voor Load Balancers</span><span class="sxs-lookup"><span data-stu-id="43d3e-131">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

