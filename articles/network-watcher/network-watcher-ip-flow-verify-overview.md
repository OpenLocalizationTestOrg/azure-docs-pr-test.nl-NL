---
title: aaaIntroduction tooIP stroom controleren in de Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina bevat een overzicht van Hallo netwerk-Watcher-IP-stroom mogelijkheid controleren
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="f26c9-103">Inleiding tooIP stroom controleren in de Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="f26c9-103">Introduction tooIP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="f26c9-104">IP-stroom Controleer controles of als een pakket wordt toegestaan of geweigerd tooor van een virtuele machine op basis van 5-tuple informatie.</span><span class="sxs-lookup"><span data-stu-id="f26c9-104">IP flow verify checks if a packet is allowed or denied tooor from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="f26c9-105">Deze informatie bestaat uit de richting, protocol, lokaal IP-, externe IP-, lokale poort en externe poort.</span><span class="sxs-lookup"><span data-stu-id="f26c9-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="f26c9-106">Als hello-pakket is geweigerd door een beveiligingsgroep, wordt Hallo-naam van Hallo-regel die geweigerd hello-pakket geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="f26c9-106">If hello packet is denied by a security group, hello name of hello rule that denied hello packet is returned.</span></span> <span data-ttu-id="f26c9-107">Terwijl de IP-bron- of doelserver kan worden gekozen, deze functie kan beheerders die Analyseer snel problemen met de netwerkverbinding van of toohello internet en van of toohello on-premises omgeving.</span><span class="sxs-lookup"><span data-stu-id="f26c9-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or toohello internet and from or toohello on-premises environment.</span></span>

<span data-ttu-id="f26c9-108">IP-stroom controleren is bedoeld voor een netwerkinterface van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f26c9-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="f26c9-109">Netwerkverkeer is geverifieerd op basis van Hallo geconfigureerd instellingen tooor van netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="f26c9-109">Traffic flow is then verified based on hello configured settings tooor from that network interface.</span></span> <span data-ttu-id="f26c9-110">Deze functie is handig bij de bevestiging als toegangsroutes en uitgaande verkeer tooor van een virtuele machine wordt geblokkeerd door een regel in een Netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="f26c9-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic tooor from a virtual machine.</span></span>

<span data-ttu-id="f26c9-111">Een exemplaar van netwerk-Watcher behoeften toobe gemaakt in alle regio's dat u van plan toorun IP-stroom bent controleren.</span><span class="sxs-lookup"><span data-stu-id="f26c9-111">An instance of Network Watcher needs toobe created in all regions that you plan toorun IP flow verify.</span></span> <span data-ttu-id="f26c9-112">Netwerk-Watcher is een regionale service en kan alleen worden uitgevoerd op resources in Hallo dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="f26c9-112">Network Watcher is a regional service and can only be ran against resources in hello same region.</span></span> <span data-ttu-id="f26c9-113">Dit heeft geen invloed op Hallo resultaten van IP-stroom controleren als Hallo route gekoppeld Hallo die NIC nog steeds worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="f26c9-113">This does not affect hello results of IP flow verify as hello route associated with hello NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="f26c9-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f26c9-115">Next steps</span></span>

<span data-ttu-id="f26c9-116">Ga naar de volgende artikel toolearn als een pakket wordt toegestaan of geweigerd voor een specifieke virtuele machine via de portal Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="f26c9-116">Visit hello following article toolearn if a packet is allowed or denied for a specific virtual machine through hello portal.</span></span> [<span data-ttu-id="f26c9-117">Controleer of verkeer is toegestaan op een virtuele machine met het IP-stromen controleren met behulp van de portal Hallo</span><span class="sxs-lookup"><span data-stu-id="f26c9-117">Check if traffic is allowed on a VM with IP Flow Verify using hello portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












