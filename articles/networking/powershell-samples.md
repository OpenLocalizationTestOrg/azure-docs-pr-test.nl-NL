---
title: Voorbeelden van Azure PowerShell | Microsoft Docs
description: Voorbeelden van Azure PowerShell
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/24/2017
ms.author: georgewallace
ms.openlocfilehash: 0bca4fb6874bd265f0ae9faeb4219abeb4ffb6d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples-for-networking"></a><span data-ttu-id="fc134-103">Azure PowerShell-voorbeelden voor netwerken</span><span class="sxs-lookup"><span data-stu-id="fc134-103">Azure PowerShell Samples for networking</span></span>

<span data-ttu-id="fc134-104">De volgende tabel bevat koppelingen naar de scripts die zijn gebouwd met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc134-104">The following table includes links to scripts built using Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="fc134-105">**Connectiviteit tussen Azure-resources**</span><span class="sxs-lookup"><span data-stu-id="fc134-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="fc134-106">Een virtueel netwerk voor toepassingen met meerdere lagen maken</span><span class="sxs-lookup"><span data-stu-id="fc134-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="fc134-107">Hiermee maakt een virtueel netwerk met front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="fc134-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="fc134-108">Het verkeer naar de front-end-subnet is beperkt tot HTTP, terwijl het verkeer naar de back-end-subnet wordt beperkt tot de SQL-poort 1433.</span><span class="sxs-lookup"><span data-stu-id="fc134-108">Traffic to the front-end subnet is limited to HTTP, while traffic to the back-end subnet is limited to SQL, port 1433.</span></span> |
| [<span data-ttu-id="fc134-109">Peer twee virtuele netwerken</span><span class="sxs-lookup"><span data-stu-id="fc134-109">Peer two virtual networks</span></span>](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="fc134-110">Maakt en verbinding maakt twee virtuele netwerken in dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="fc134-110">Creates and connects two virtual networks in the same region.</span></span> |
| [<span data-ttu-id="fc134-111">-Routeverkeer via een virtueel netwerkapparaat</span><span class="sxs-lookup"><span data-stu-id="fc134-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="fc134-112">Maakt een virtueel netwerk met de front-end en back-end-subnetten en een virtuele machine kan verkeer leiden tussen de twee subnetten.</span><span class="sxs-lookup"><span data-stu-id="fc134-112">Creates a virtual network with front-end and back-end subnets and a VM that is able to route traffic between the two subnets.</span></span> |
| [<span data-ttu-id="fc134-113">Filteren van binnenkomende en uitgaande netwerkverkeer voor VM</span><span class="sxs-lookup"><span data-stu-id="fc134-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="fc134-114">Hiermee maakt een virtueel netwerk met front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="fc134-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="fc134-115">Binnenkomend netwerkverkeer naar de front-end-subnet is beperkt tot HTTP en HTTPS...</span><span class="sxs-lookup"><span data-stu-id="fc134-115">Inbound network traffic to the front-end subnet is limited to HTTP and HTTPS..</span></span> <span data-ttu-id="fc134-116">Uitgaand verkeer naar Internet van de back-end-subnet is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="fc134-116">Outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="fc134-117">**Load balancing en verkeer richting**</span><span class="sxs-lookup"><span data-stu-id="fc134-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="fc134-118">Load balance verkeer naar VM's voor hoge beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="fc134-118">Load balance traffic to VMs for high availability</span></span>](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="fc134-119">Maakt verschillende virtuele machines in een maximaal beschikbare en configuratie van taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="fc134-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="fc134-120">Taakverdeling maken voor meerdere websites op virtuele machines</span><span class="sxs-lookup"><span data-stu-id="fc134-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="fc134-121">Hiermee maakt twee virtuele machines met meerdere IP-configuraties, lid is van een Azure Beschikbaarheidsset, toegankelijk via een Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="fc134-121">Creates two VMs with multiple IP configurations, joined to an Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="fc134-122">Directe verkeer over meerdere regio's voor hoge beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="fc134-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="fc134-123">Hiermee maakt twee app-serviceabonnementen, twee web-apps, een traffic manager-profiel en twee traffic manager-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="fc134-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
