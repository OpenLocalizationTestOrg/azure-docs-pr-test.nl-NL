---
title: aaaIntroduction tootopology in Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina bevat een overzicht van Hallo netwerk-Watcher-topologie-mogelijkheden
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a><span data-ttu-id="f2e01-103">Inleiding tootopology in Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="f2e01-103">Introduction tootopology in Azure Network Watcher</span></span>

<span data-ttu-id="f2e01-104">Topologie retourneert een grafiek van netwerkbronnen in een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="f2e01-104">Topology returns a graph of network resources in a virtual network.</span></span> <span data-ttu-id="f2e01-105">Hallo-grafiek wordt Hallo koppeling tussen Hallo resources toorepresent Hallo end tooend verbinding met het netwerk.</span><span class="sxs-lookup"><span data-stu-id="f2e01-105">hello graph depicts hello interconnection between hello resources toorepresent hello end tooend network connectivity.</span></span>

![overzicht van de topologie][1]

<span data-ttu-id="f2e01-107">In de portal Hallo retourneert topologie Hallo resourceobjecten op een per per virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="f2e01-107">In hello portal, Topology returns hello resource objects on a per virtual network basis.</span></span> <span data-ttu-id="f2e01-108">Hallo relaties zijn afgebeeld met lijnen tussen Hallo resources bronnen buiten Hallo netwerk-Watcher regio, zelfs als in Hallo bron de groep niet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f2e01-108">hello relationships are depicted by lines between hello resources Resources outside of hello Network Watcher region, even if in hello resource group will not be displayed.</span></span> <span data-ttu-id="f2e01-109">Hallo bronnen geretourneerd in de portal weergave Hallo zijn een subset van Hallo netwerkonderdelen die diagram worden weergegeven aan.</span><span class="sxs-lookup"><span data-stu-id="f2e01-109">hello resources returned in hello portal view are a subset of hello networking components that are graphed.</span></span> <span data-ttu-id="f2e01-110">toosee hello volledige lijst met netwerkresources kunt u [PowerShell](network-watcher-topology-powershell.md) of [REST](network-watcher-topology-rest.md)</span><span class="sxs-lookup"><span data-stu-id="f2e01-110">toosee hello full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span></span>

> [!NOTE]
> <span data-ttu-id="f2e01-111">Een exemplaar van netwerk-Watcher is vereist in elke regio waarin u wilt dat toorun topologie op.</span><span class="sxs-lookup"><span data-stu-id="f2e01-111">An instance of Network Watcher is required in each region that you want toorun Topology on.</span></span>

<span data-ttu-id="f2e01-112">Resources Hallo verbinding tussen hen worden geretourneerd worden gemodelleerd onder twee-relaties.</span><span class="sxs-lookup"><span data-stu-id="f2e01-112">As resources are returned hello connection between them are modeled under two relationships.</span></span>

- <span data-ttu-id="f2e01-113">**Containment** -voorbeeld: virtueel netwerk bevat een Subnet met een NIC</span><span class="sxs-lookup"><span data-stu-id="f2e01-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span></span>
- <span data-ttu-id="f2e01-114">**Gekoppeld** -voorbeeld: een NIC is gekoppeld aan een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="f2e01-114">**Associated** - Example: A NIC is associated with a VM</span></span>

### <a name="next-steps"></a><span data-ttu-id="f2e01-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f2e01-115">Next steps</span></span>

<span data-ttu-id="f2e01-116">Meer informatie over hoe toouse PowerShell tooretrieve Hallo topologie bekijken op [netwerk-Watcher-topologie met PowerShell](network-watcher-topology-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="f2e01-116">Learn how toouse PowerShell tooretrieve hello Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span></span>

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
