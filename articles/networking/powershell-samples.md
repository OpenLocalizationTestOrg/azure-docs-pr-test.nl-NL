---
title: Voorbeelden van PowerShell aaaAzure | Microsoft Docs
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
ms.openlocfilehash: 130a6e755691b46a9549cad5acaa5bde4fe38e95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-networking"></a><span data-ttu-id="14a5f-103">Azure PowerShell-voorbeelden voor netwerken</span><span class="sxs-lookup"><span data-stu-id="14a5f-103">Azure PowerShell Samples for networking</span></span>

<span data-ttu-id="14a5f-104">Hallo bevat volgende tabel koppelingen tooscripts gebouwd met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14a5f-104">hello following table includes links tooscripts built using Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="14a5f-105">**Connectiviteit tussen Azure-resources**</span><span class="sxs-lookup"><span data-stu-id="14a5f-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="14a5f-106">Een virtueel netwerk voor toepassingen met meerdere lagen maken</span><span class="sxs-lookup"><span data-stu-id="14a5f-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="14a5f-107">Hiermee maakt een virtueel netwerk met front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="14a5f-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="14a5f-108">Verkeer toohello front-end-subnet is beperkt tooHTTP, tijdens het verkeer toohello back-end-subnet is beperkt tooSQL, poort 1433.</span><span class="sxs-lookup"><span data-stu-id="14a5f-108">Traffic toohello front-end subnet is limited tooHTTP, while traffic toohello back-end subnet is limited tooSQL, port 1433.</span></span> |
| [<span data-ttu-id="14a5f-109">Peer twee virtuele netwerken</span><span class="sxs-lookup"><span data-stu-id="14a5f-109">Peer two virtual networks</span></span>](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="14a5f-110">Maakt en verbinding maakt twee virtuele netwerken in Hallo dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="14a5f-110">Creates and connects two virtual networks in hello same region.</span></span> |
| [<span data-ttu-id="14a5f-111">-Routeverkeer via een virtueel netwerkapparaat</span><span class="sxs-lookup"><span data-stu-id="14a5f-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="14a5f-112">Maakt een virtueel netwerk met de front-end en back-end-subnetten en een virtuele machine die verkeer tussen Hallo twee subnetten kunnen tooroute is.</span><span class="sxs-lookup"><span data-stu-id="14a5f-112">Creates a virtual network with front-end and back-end subnets and a VM that is able tooroute traffic between hello two subnets.</span></span> |
| [<span data-ttu-id="14a5f-113">Filteren van binnenkomende en uitgaande netwerkverkeer voor VM</span><span class="sxs-lookup"><span data-stu-id="14a5f-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="14a5f-114">Hiermee maakt een virtueel netwerk met front-end en back-end-subnetten.</span><span class="sxs-lookup"><span data-stu-id="14a5f-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="14a5f-115">Binnenkomend netwerkverkeer toohello front-end-subnet is beperkt tooHTTP- en HTTPS...</span><span class="sxs-lookup"><span data-stu-id="14a5f-115">Inbound network traffic toohello front-end subnet is limited tooHTTP and HTTPS..</span></span> <span data-ttu-id="14a5f-116">Uitgaand verkeer toohello Internet van Hallo back-end-subnet is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="14a5f-116">Outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="14a5f-117">**Load balancing en verkeer richting**</span><span class="sxs-lookup"><span data-stu-id="14a5f-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="14a5f-118">Laden van saldo verkeer tooVMs voor hoge beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="14a5f-118">Load balance traffic tooVMs for high availability</span></span>](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="14a5f-119">Maakt verschillende virtuele machines in een maximaal beschikbare en configuratie van taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="14a5f-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="14a5f-120">Taakverdeling maken voor meerdere websites op virtuele machines</span><span class="sxs-lookup"><span data-stu-id="14a5f-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="14a5f-121">Hiermee maakt twee virtuele machines met meerdere IP-configuraties, gekoppelde tooan Azure Beschikbaarheidsset, toegankelijk via een Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="14a5f-121">Creates two VMs with multiple IP configurations, joined tooan Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="14a5f-122">Directe verkeer over meerdere regio's voor hoge beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="14a5f-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="14a5f-123">Hiermee maakt twee app-serviceabonnementen, twee web-apps, een traffic manager-profiel en twee traffic manager-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="14a5f-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
