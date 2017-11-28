---
title: problemen met de netwerkconnectiviteit tussen Azure Virtual machines aaaTroubleshooting | Microsoft Docs
description: Meer informatie over hoe tooTroubleshoot Hallo problemen met de netwerkconnectiviteit tussen Azure VM's.
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a><span data-ttu-id="da275-103">Het oplossen van problemen met de netwerkconnectiviteit tussen Azure VM 's</span><span class="sxs-lookup"><span data-stu-id="da275-103">Troubleshooting connectivity problems between Azure VMs</span></span>

<span data-ttu-id="da275-104">Er kunnen problemen met de netwerkconnectiviteit tussen Azure VM's.</span><span class="sxs-lookup"><span data-stu-id="da275-104">You might experience connectivity problems between Azure VMs.</span></span> <span data-ttu-id="da275-105">In dit artikel voor probleemoplossing stappen toohelp vindt u dit probleem oplossen.</span><span class="sxs-lookup"><span data-stu-id="da275-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="da275-106">Symptoom</span><span class="sxs-lookup"><span data-stu-id="da275-106">Symptom</span></span>

<span data-ttu-id="da275-107">Een virtuele machine van Azure kan geen verbinding tooanother Azure VM.</span><span class="sxs-lookup"><span data-stu-id="da275-107">An Azure VM cannot connect tooanother Azure VM.</span></span>

## <a name="troubleshooting-guidance"></a><span data-ttu-id="da275-108">Hulp bij het oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="da275-108">Troubleshooting guidance</span></span> 

1. [<span data-ttu-id="da275-109">Controleer als NIC is onjuist geconfigureerd</span><span class="sxs-lookup"><span data-stu-id="da275-109">Check if NIC is misconfigured</span></span>](#step-1-check-if-nic-is-misconfigured)
2. [<span data-ttu-id="da275-110">Als het netwerkverkeer wordt geblokkeerd door NSG of UDR controleren</span><span class="sxs-lookup"><span data-stu-id="da275-110">Check if network traffic is blocked by NSG or UDR</span></span>](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [<span data-ttu-id="da275-111">Controleer als netwerkverkeer wordt geblokkeerd door VM-firewall</span><span class="sxs-lookup"><span data-stu-id="da275-111">Check if network traffic is blocked by VM firewall</span></span>](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [<span data-ttu-id="da275-112">Controleer of VM-app of service op poort Hallo luistert</span><span class="sxs-lookup"><span data-stu-id="da275-112">Check whether VM app or service is listening on hello port</span></span>](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [<span data-ttu-id="da275-113">Controleer of de Hallo probleem wordt veroorzaakt door snat omzetten</span><span class="sxs-lookup"><span data-stu-id="da275-113">Check whether hello problem is caused by SNAT</span></span>](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [<span data-ttu-id="da275-114">Controleer of het verkeer wordt geblokkeerd door de ACL's voor Hallo klassieke VM</span><span class="sxs-lookup"><span data-stu-id="da275-114">Check whether traffic is blocked by ACLs for hello classic VM</span></span>](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [<span data-ttu-id="da275-115">Controleer of het Hallo-eindpunt is gemaakt voor Hallo klassieke VM</span><span class="sxs-lookup"><span data-stu-id="da275-115">Check whether hello endpoint is created for hello classic VM</span></span>](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [<span data-ttu-id="da275-116">Kan geen tooconnect tooa VM-netwerkshare</span><span class="sxs-lookup"><span data-stu-id="da275-116">Unable tooconnect tooa VM network share</span></span>](#step-8-unable-to-connect-to-a-vm-network-share)
9. [<span data-ttu-id="da275-117">Inter Vnet-connectiviteit</span><span class="sxs-lookup"><span data-stu-id="da275-117">Inter-Vnet connectivity</span></span>](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a><span data-ttu-id="da275-118">Stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="da275-118">Troubleshooting steps</span></span>

<span data-ttu-id="da275-119">Volg deze stappen tootroubleshoot Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="da275-119">Follow these steps tootroubleshoot hello problem.</span></span> <span data-ttu-id="da275-120">Controleer of het Hallo-probleem opgelost na elke stap is.</span><span class="sxs-lookup"><span data-stu-id="da275-120">Check whether hello problem is resolved after each step.</span></span> 

### <a name="step-1-check-if-nic-is-misconfigured"></a><span data-ttu-id="da275-121">Stap 1: Controleer of NIC is onjuist geconfigureerd</span><span class="sxs-lookup"><span data-stu-id="da275-121">Step 1: Check if NIC is misconfigured</span></span>

<span data-ttu-id="da275-122">Ga als volgt [hoe tooreset netwerkinterface voor virtuele machine van Windows Azure](../virtual-machines/windows/reset-network-interface.md).</span><span class="sxs-lookup"><span data-stu-id="da275-122">Follow [How tooreset network interface for Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span></span> 

<span data-ttu-id="da275-123">Als Hallo probleem optreedt nadat u de netwerkinterface hello (NIC) wijzigen, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="da275-123">If hello problem occurs after you modify hello network interface (NIC), follow these steps:</span></span>

<span data-ttu-id="da275-124">**Virtuele machines mulit-NIC**</span><span class="sxs-lookup"><span data-stu-id="da275-124">**Mulit-NIC VMs**</span></span>

1. <span data-ttu-id="da275-125">Toevoegen van een NIC.</span><span class="sxs-lookup"><span data-stu-id="da275-125">Add a NIC.</span></span>
2. <span data-ttu-id="da275-126">Hallo-problemen oplossen in Hallo onjuiste NIC of Verwijder ongeldige NIC.</span><span class="sxs-lookup"><span data-stu-id="da275-126">Fix hello problems in hello bad NIC or remove bad NIC.</span></span>  <span data-ttu-id="da275-127">Vervolgens readd Hallo NIC.</span><span class="sxs-lookup"><span data-stu-id="da275-127">Then readd hello NIC.</span></span>

<span data-ttu-id="da275-128">Zie voor meer informatie [toevoegen network interfaces tooor verwijderen van virtuele machines](virtual-network-network-interface-vm.md).</span><span class="sxs-lookup"><span data-stu-id="da275-128">For more information, see [Add network interfaces tooor remove from virtual machines](virtual-network-network-interface-vm.md).</span></span>

<span data-ttu-id="da275-129">**Één NIC VM**</span><span class="sxs-lookup"><span data-stu-id="da275-129">**Single-NIC VM**</span></span> 

- [<span data-ttu-id="da275-130">Implementeer Windows VM opnieuw</span><span class="sxs-lookup"><span data-stu-id="da275-130">Redeploy Windows VM</span></span>](../virtual-machines/windows/redeploy-to-new-node.md)
- [<span data-ttu-id="da275-131">Virtuele Linux-machine implementeren</span><span class="sxs-lookup"><span data-stu-id="da275-131">Redeploy Linux VM</span></span>](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a><span data-ttu-id="da275-132">Stap 2: Controleer of het netwerkverkeer wordt geblokkeerd door NSG of UDR</span><span class="sxs-lookup"><span data-stu-id="da275-132">Step 2: Check if network traffic is blocked by NSG or UDR</span></span>

<span data-ttu-id="da275-133">Gebruikmaken van [netwerk-Watcher IP-stroom controleren](../network-watcher/network-watcher-ip-flow-verify-overview.md) en [NSG stroom logboekregistratie](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify als er een Netwerkbeveiligingsgroep of door de gebruiker gedefinieerde Route die netwerkverkeer verstoort.</span><span class="sxs-lookup"><span data-stu-id="da275-133">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span>

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a><span data-ttu-id="da275-134">Stap 3: Controleren als netwerkverkeer wordt geblokkeerd door VM-firewall</span><span class="sxs-lookup"><span data-stu-id="da275-134">Step 3: Check if network traffic is blocked by VM firewall</span></span>

<span data-ttu-id="da275-135">Hallo firewall uitschakelen en test Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="da275-135">Disable hello firewall, and then test hello result.</span></span> <span data-ttu-id="da275-136">Als het Hallo-probleem is opgelost, Hallo-instellingen in de firewall Hallo valideren en opnieuw inschakelen.</span><span class="sxs-lookup"><span data-stu-id="da275-136">If hello problem is resolved, validate hello settings in hello firewall and re-enable.</span></span>

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a><span data-ttu-id="da275-137">Stap 4: Controleren of VM-app of service op poort Hallo luistert</span><span class="sxs-lookup"><span data-stu-id="da275-137">Step 4: Check whether VM app or service is listening on hello port</span></span>

<span data-ttu-id="da275-138">U kunt een van de volgende methoden toocheck of VM-toepassing of Service op poort Hallo luistert Hallo</span><span class="sxs-lookup"><span data-stu-id="da275-138">You can use one of hello following methods toocheck whether VM Application or Service is listening on hello port</span></span>

- <span data-ttu-id="da275-139">Hallo opdrachten toocheck te volgen of Hallo server op deze poort luistert worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="da275-139">Run hello following commands toocheck whether hello server is listening on that port.</span></span>

<span data-ttu-id="da275-140">**Windows-VM**</span><span class="sxs-lookup"><span data-stu-id="da275-140">**Windows VM**</span></span>

    netstat –ano

<span data-ttu-id="da275-141">**Linux-VM**</span><span class="sxs-lookup"><span data-stu-id="da275-141">**Linux VM**</span></span>

    netstat -l

- <span data-ttu-id="da275-142">Voer Hallo **Telnet** opdracht op Hallo VM tooitself tootest Hallo poort.</span><span class="sxs-lookup"><span data-stu-id="da275-142">Run hello **Telnet** command on hello VM tooitself tootest hello port.</span></span> <span data-ttu-id="da275-143">Hallo-test niet slaagt, is toepassing of service niet als geconfigureerde toolisten op Hallo-poort.</span><span class="sxs-lookup"><span data-stu-id="da275-143">If hello test fails, application or service is not configured toolisten on hello port.</span></span>

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a><span data-ttu-id="da275-144">Stap 5: Controleren of Hallo probleem wordt veroorzaakt door snat omzetten</span><span class="sxs-lookup"><span data-stu-id="da275-144">Step 5: Check whether hello problem is caused by SNAT</span></span>

<span data-ttu-id="da275-145">In sommige scenario's, hello VM geplaatst achter een Load balance oplossing met een afhankelijkheid op resources buiten Azure.</span><span class="sxs-lookup"><span data-stu-id="da275-145">In some scenarios, hello VM is placed behind a Load balance solution that has a dependency on resources outside of Azure.</span></span> <span data-ttu-id="da275-146">In deze scenario's, als u met de verbinding problemen, Hallo probleem kan worden veroorzaakt door [snat omzetten poort bronuitputting](../load-balancer/load-balancer-outbound-connections.md).</span><span class="sxs-lookup"><span data-stu-id="da275-146">In these scenarios, if you experience intermittent connection problems, hello problem may be caused by [SNAT port exhaustion](../load-balancer/load-balancer-outbound-connections.md).</span></span> <span data-ttu-id="da275-147">tooresolve hello probleem, een VIP (of ILPIP voor klassieke) voor elke VM die achter Hallo Load balancer maken en beveiligen met NSG of ACL.</span><span class="sxs-lookup"><span data-stu-id="da275-147">tooresolve hello issue, create a VIP (or ILPIP for classic) for each VM that is behind hello Load balancer and secure with NSG or ACL.</span></span> 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a><span data-ttu-id="da275-148">Stap 6: Controleer of het verkeer wordt geblokkeerd door de ACL's voor Hallo klassieke VM</span><span class="sxs-lookup"><span data-stu-id="da275-148">Step 6: Check whether traffic is blocked by ACLs for hello classic VM</span></span>

<span data-ttu-id="da275-149">Een ACL biedt Hallo mogelijkheid tooselectively toestaan of weigeren van verkeer voor het eindpunt van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="da275-149">An ACL provides hello ability tooselectively permit or deny traffic for a virtual machine endpoint.</span></span> <span data-ttu-id="da275-150">Zie voor meer informatie [beheren Hallo ACL op een eindpunt](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span><span class="sxs-lookup"><span data-stu-id="da275-150">For more information, see [Manage hello ACL on an endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a><span data-ttu-id="da275-151">Stap 7: Controleer of het Hallo-eindpunt is gemaakt voor Hallo klassieke VM</span><span class="sxs-lookup"><span data-stu-id="da275-151">Step 7: Check whether hello endpoint is created for hello classic VM</span></span>

<span data-ttu-id="da275-152">Alle virtuele machines die u maakt in Azure met behulp van het klassieke implementatiemodel Hallo kunnen automatisch communiceren via een particulier netwerkkanaal met andere virtuele machines in Hallo dat dezelfde cloud service- of virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="da275-152">All VMs that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="da275-153">Computers met andere virtuele netwerken vereisen echter eindpunten toodirect Hallo netwerk binnenkomend verkeer tooa virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="da275-153">However, computers on other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="da275-154">Zie voor meer informatie [hoe tooset eindpunten](../virtual-machines/windows/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="da275-154">For more information, see [How tooset up endpoints](../virtual-machines/windows/classic/setup-endpoints.md).</span></span>

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a><span data-ttu-id="da275-155">Stap 8: Kan geen tooconnect tooa VM-netwerkshare</span><span class="sxs-lookup"><span data-stu-id="da275-155">Step 8: Unable tooconnect tooa VM network share</span></span>

<span data-ttu-id="da275-156">Als u tooconnect tooa VM netwerkshare bevindt, kan Hallo probleem worden veroorzaakt door niet beschikbaar NIC's in Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="da275-156">If you are unable tooconnect tooa VM network share, hello problem can be caused by unavailable NICs in hello VM.</span></span> <span data-ttu-id="da275-157">toodelete Hallo niet beschikbaar NIC's, Zie [hoe toodelete Hallo niet beschikbaar NIC's](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span><span class="sxs-lookup"><span data-stu-id="da275-157">toodelete hello unavailable NICs, see [How toodelete hello unavailable NICs](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span></span>

### <a name="step-9-inter-vnet-connectivity"></a><span data-ttu-id="da275-158">Stap 9: Inter Vnet-connectiviteit</span><span class="sxs-lookup"><span data-stu-id="da275-158">Step 9: Inter-Vnet connectivity</span></span>

<span data-ttu-id="da275-159">Gebruikmaken van [netwerk-Watcher IP-stroom controleren](../network-watcher/network-watcher-ip-flow-verify-overview.md) en [NSG stroom logboekregistratie](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify als er een Netwerkbeveiligingsgroep of door de gebruiker gedefinieerde Route die netwerkverkeer verstoort.</span><span class="sxs-lookup"><span data-stu-id="da275-159">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span> <span data-ttu-id="da275-160">U kunt ook uw Inter Vnet-configuratie valideren [hier](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span><span class="sxs-lookup"><span data-stu-id="da275-160">You can also validate your Inter-Vnet configuration [here](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span></span>

### <a name="need-help-contact-support"></a><span data-ttu-id="da275-161">Hulp nodig?</span><span class="sxs-lookup"><span data-stu-id="da275-161">Need help?</span></span> <span data-ttu-id="da275-162">Neem contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="da275-162">Contact support.</span></span>
<span data-ttu-id="da275-163">Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget uw probleem snel worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="da275-163">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
