---
title: Vinden van de volgende hop met Azure-netwerk-Watcher volgende Hop - Azure CLI 2.0 | Microsoft Docs
description: In dit artikel wordt beschreven hoe u kunt vinden wat het volgende hoptype is en IP-adres met de volgende Hop met Azure CLI.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d1ee6870ba0188ff2c473e4cca12a5bdc1f97d3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="c984d-103">Uitzoeken wat het volgende hoptype gebruikt de mogelijkheid van de volgende Hop in Azure met Azure CLI 2.0 netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="c984d-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c984d-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c984d-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="c984d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c984d-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="c984d-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c984d-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="c984d-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c984d-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="c984d-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="c984d-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="c984d-109">De volgende hop is een functie van netwerk-Watcher die de mogelijkheid get biedt de volgende hoptype en IP-adres op basis van een opgegeven virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c984d-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="c984d-110">Deze functie is handig bij het bepalen of een virtuele machine uitgaand verkeer van een gateway, internet of virtuele netwerken om te gaan naar de bestemming passeert.</span><span class="sxs-lookup"><span data-stu-id="c984d-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

<span data-ttu-id="c984d-111">Dit artikel wordt de volgende generatie CLI gebruikt voor de resource management-implementatiemodel, Azure CLI 2.0, die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="c984d-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="c984d-112">Als u wilt de stappen in dit artikel uitvoert, moet u [installeren van de Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="c984d-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c984d-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="c984d-113">Before you begin</span></span>

<span data-ttu-id="c984d-114">In dit scenario gebruikt u de Azure CLI het volgende hoptype en IP-adres vinden.</span><span class="sxs-lookup"><span data-stu-id="c984d-114">In this scenario, you will use the Azure CLI to find the next hop type and IP address.</span></span>

<span data-ttu-id="c984d-115">Dit scenario wordt ervan uitgegaan dat u de stappen in al hebt gevolgd [maken van een netwerk-Watcher](network-watcher-create.md) voor het maken van een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="c984d-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="c984d-116">Het scenario wordt ervan uitgegaan dat er een resourcegroep met een geldige virtuele machine bestaat om te worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c984d-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="c984d-117">Scenario</span><span class="sxs-lookup"><span data-stu-id="c984d-117">Scenario</span></span>

<span data-ttu-id="c984d-118">Het scenario beschreven in dit artikel maakt gebruik van volgende Hop, een functie van netwerk-Watcher waarmee wordt gezocht naar de volgende hoptype en IP-adres voor een resource.</span><span class="sxs-lookup"><span data-stu-id="c984d-118">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="c984d-119">Voor meer informatie over de volgende Hop, gaat u naar [volgende Hop overzicht](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c984d-119">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="c984d-120">Ophalen van de volgende Hop</span><span class="sxs-lookup"><span data-stu-id="c984d-120">Get Next Hop</span></span>

<span data-ttu-id="c984d-121">Ophalen van de volgende hop we noemen de `az network watcher show-next-hop` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c984d-121">To get the next hop we call the `az network watcher show-next-hop` cmdlet.</span></span> <span data-ttu-id="c984d-122">De cmdlet geven we de resourcegroep voor netwerk-Watcher, de NetworkWatcher virtuele machine Id, IP-bronadres en IP-doeladres.</span><span class="sxs-lookup"><span data-stu-id="c984d-122">We pass the cmdlet the Network Watcher resource group, the NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="c984d-123">In dit voorbeeld is het IP-doeladres voor een virtuele machine in een ander virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="c984d-123">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="c984d-124">Er is een virtuele netwerkgateway tussen de twee virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="c984d-124">There is a virtual network gateway between the two virtual networks.</span></span>

<span data-ttu-id="c984d-125">Als u dit nog niet hebt nog installeren en configureren van de meest recente [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u aan op een Azure-account met [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c984d-125">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="c984d-126">Voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="c984d-126">Then run the following command:</span></span>

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
<span data-ttu-id="c984d-127">Als de virtuele machine meerdere NIC's heeft en doorsturen via IP is ingeschakeld op een van de NIC's en vervolgens de NIC-parameter (-ik nic-id) moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c984d-127">If the VM has multiple NICs and IP forwarding is enabled on any of the NICs, then the NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="c984d-128">Anders is optioneel.</span><span class="sxs-lookup"><span data-stu-id="c984d-128">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="c984d-129">Resultaten bekijken</span><span class="sxs-lookup"><span data-stu-id="c984d-129">Review results</span></span>

<span data-ttu-id="c984d-130">Na voltooiing wordt worden de resultaten geleverd.</span><span class="sxs-lookup"><span data-stu-id="c984d-130">When complete, the results are provided.</span></span> <span data-ttu-id="c984d-131">De volgende hop-IP-adres en het type resource dat is geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="c984d-131">The next hop IP address is returned as well as the type of resource it is.</span></span>

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

<span data-ttu-id="c984d-132">De volgende lijst bevat de momenteel beschikbare NextHopType waarden:</span><span class="sxs-lookup"><span data-stu-id="c984d-132">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="c984d-133">**Volgend Hoptype**</span><span class="sxs-lookup"><span data-stu-id="c984d-133">**Next Hop Type**</span></span>

* <span data-ttu-id="c984d-134">Internet</span><span class="sxs-lookup"><span data-stu-id="c984d-134">Internet</span></span>
* <span data-ttu-id="c984d-135">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="c984d-135">VirtualAppliance</span></span>
* <span data-ttu-id="c984d-136">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="c984d-136">VirtualNetworkGateway</span></span>
* <span data-ttu-id="c984d-137">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="c984d-137">VnetLocal</span></span>
* <span data-ttu-id="c984d-138">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="c984d-138">HyperNetGateway</span></span>
* <span data-ttu-id="c984d-139">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="c984d-139">VnetPeering</span></span>
* <span data-ttu-id="c984d-140">Geen</span><span class="sxs-lookup"><span data-stu-id="c984d-140">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="c984d-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c984d-141">Next steps</span></span>

<span data-ttu-id="c984d-142">Meer informatie over het bekijken van de groep beveiligingsinstellingen van uw netwerk via een programma te bezoeken [NSG controleren met de netwerk-Watcher](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="c984d-142">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
