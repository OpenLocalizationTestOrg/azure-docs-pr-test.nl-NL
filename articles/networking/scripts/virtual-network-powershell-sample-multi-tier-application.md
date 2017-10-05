---
title: Azure PowerShell-script steekproef - maken van een netwerk voor toepassingen met meerdere lagen | Microsoft Docs
description: 'Azure PowerShell-script voorbeeld: een virtueel netwerk voor toepassingen met meerdere lagen maken.'
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: ab49e78ef17b093d2bbe4e3276a1ece3a4247f91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="c6774-103">Een netwerk voor toepassingen met meerdere lagen maken</span><span class="sxs-lookup"><span data-stu-id="c6774-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="c6774-104">Dit voorbeeldscript wordt een virtueel netwerk gemaakt met front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="c6774-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="c6774-105">Het verkeer naar de front-end-subnet is beperkt tot HTTP- en SSH, terwijl het verkeer naar de back-end-subnet wordt beperkt tot MySQL, poort 3306.</span><span class="sxs-lookup"><span data-stu-id="c6774-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="c6774-106">Nadat het script is uitgevoerd, hebt u twee virtuele machines, één in elk subnet dat u kunt webserver en MySQL-software te implementeren.</span><span class="sxs-lookup"><span data-stu-id="c6774-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="c6774-107">Installeer zo nodig de Azure PowerShell met de instructie gevonden in de [Azure PowerShell handleiding](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), en voer vervolgens `Login-AzureRmAccount` geen verbinding maken met Azure.</span><span class="sxs-lookup"><span data-stu-id="c6774-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c6774-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="c6774-108">Sample script</span></span>


<span data-ttu-id="c6774-109">[!code-powershell[belangrijkste](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "virtuele netwerk voor de toepassing met meerdere lagen")]</span><span class="sxs-lookup"><span data-stu-id="c6774-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c6774-110">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="c6774-110">Clean up deployment</span></span> 

<span data-ttu-id="c6774-111">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c6774-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c6774-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="c6774-112">Script explanation</span></span>

<span data-ttu-id="c6774-113">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, het virtuele netwerk en netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="c6774-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="c6774-114">Elke opdracht in de tabel is gekoppeld aan de opdracht specifieke documentatie bij.</span><span class="sxs-lookup"><span data-stu-id="c6774-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="c6774-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="c6774-115">Command</span></span> | <span data-ttu-id="c6774-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="c6774-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c6774-117">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c6774-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c6774-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c6774-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c6774-119">Nieuwe-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="c6774-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="c6774-120">Maakt een virtueel Azure-netwerk en de front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="c6774-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="c6774-121">Nieuwe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="c6774-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="c6774-122">Maakt een back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="c6774-122">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="c6774-123">Nieuwe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="c6774-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="c6774-124">Hiermee maakt u een openbaar IP-adres voor toegang tot de virtuele machine via het Internet.</span><span class="sxs-lookup"><span data-stu-id="c6774-124">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="c6774-125">Nieuwe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="c6774-125">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="c6774-126">Virtuele netwerkinterfaces maakt en gekoppeld aan het virtuele netwerk front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="c6774-126">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="c6774-127">Nieuwe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="c6774-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="c6774-128">Netwerk maakt beveiligingsgroepen (NSG) die gekoppeld aan de front-end en back-end subnetten zijn.</span><span class="sxs-lookup"><span data-stu-id="c6774-128">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="c6774-129">Nieuwe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="c6774-129">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="c6774-130">Maakt NSG-regels die bepaalde poorten tot specifieke subnetten blokkeren of toestaan.</span><span class="sxs-lookup"><span data-stu-id="c6774-130">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="c6774-131">Nieuwe-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="c6774-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="c6774-132">Hiermee maakt u virtuele machines en een NIC koppelt aan elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c6774-132">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="c6774-133">Deze opdracht geeft ook aan de installatiekopie van de virtuele machine te gebruiken en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="c6774-133">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="c6774-134">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c6774-134">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c6774-135">Hiermee verwijdert u een resourcegroep en alle resources die deze bevat.</span><span class="sxs-lookup"><span data-stu-id="c6774-135">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c6774-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c6774-136">Next steps</span></span>

<span data-ttu-id="c6774-137">Zie voor meer informatie over Azure PowerShell [documentatie van Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c6774-137">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="c6774-138">Aanvullende voorbeelden voor netwerken PowerShell-script kunnen worden gevonden in de [overzicht van Azure-netwerken documentatie](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6774-138">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>