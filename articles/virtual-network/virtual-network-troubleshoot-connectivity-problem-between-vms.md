---
title: Het oplossen van problemen met de netwerkconnectiviteit tussen Azure Virtual machines | Microsoft Docs
description: Informatie over het oplossen van de connectiviteit tussen virtuele Azure-machines.
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
ms.openlocfilehash: fd0f25c07cb3f385d3e8480ce1e33dec1ae0a214
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a><span data-ttu-id="b0c77-103">Het oplossen van problemen met de netwerkconnectiviteit tussen Azure VM 's</span><span class="sxs-lookup"><span data-stu-id="b0c77-103">Troubleshooting connectivity problems between Azure VMs</span></span>

<span data-ttu-id="b0c77-104">Er kunnen problemen met de netwerkconnectiviteit tussen Azure VM's.</span><span class="sxs-lookup"><span data-stu-id="b0c77-104">You might experience connectivity problems between Azure VMs.</span></span> <span data-ttu-id="b0c77-105">Dit artikel bevat de stappen voor probleemoplossing waarmee u kunt dit probleem oplossen.</span><span class="sxs-lookup"><span data-stu-id="b0c77-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="b0c77-106">Symptoom</span><span class="sxs-lookup"><span data-stu-id="b0c77-106">Symptom</span></span>

<span data-ttu-id="b0c77-107">Een virtuele machine van Azure kan geen verbinding met een andere virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="b0c77-107">An Azure VM cannot connect to another Azure VM.</span></span>

## <a name="troubleshooting-guidance"></a><span data-ttu-id="b0c77-108">Hulp bij het oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="b0c77-108">Troubleshooting guidance</span></span> 

1. [<span data-ttu-id="b0c77-109">Controleer als NIC is onjuist geconfigureerd</span><span class="sxs-lookup"><span data-stu-id="b0c77-109">Check if NIC is misconfigured</span></span>](#step-1-check-if-nic-is-misconfigured)
2. [<span data-ttu-id="b0c77-110">Als het netwerkverkeer wordt geblokkeerd door NSG of UDR controleren</span><span class="sxs-lookup"><span data-stu-id="b0c77-110">Check if network traffic is blocked by NSG or UDR</span></span>](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [<span data-ttu-id="b0c77-111">Controleer als netwerkverkeer wordt geblokkeerd door VM-firewall</span><span class="sxs-lookup"><span data-stu-id="b0c77-111">Check if network traffic is blocked by VM firewall</span></span>](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [<span data-ttu-id="b0c77-112">Controleer of VM-app of service op poort luistert</span><span class="sxs-lookup"><span data-stu-id="b0c77-112">Check whether VM app or service is listening on the port</span></span>](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [<span data-ttu-id="b0c77-113">Controleer of het probleem wordt veroorzaakt door snat omzetten</span><span class="sxs-lookup"><span data-stu-id="b0c77-113">Check whether the problem is caused by SNAT</span></span>](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [<span data-ttu-id="b0c77-114">Controleer of verkeer wordt geblokkeerd door de ACL's voor de klassieke virtuele machine</span><span class="sxs-lookup"><span data-stu-id="b0c77-114">Check whether traffic is blocked by ACLs for the classic VM</span></span>](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [<span data-ttu-id="b0c77-115">Controleer of het eindpunt voor de klassieke virtuele machine wordt gemaakt</span><span class="sxs-lookup"><span data-stu-id="b0c77-115">Check whether the endpoint is created for the classic VM</span></span>](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [<span data-ttu-id="b0c77-116">Kan geen verbinding met een VM-netwerkshare</span><span class="sxs-lookup"><span data-stu-id="b0c77-116">Unable to connect to a VM network share</span></span>](#step-8-unable-to-connect-to-a-vm-network-share)
9. [<span data-ttu-id="b0c77-117">Inter Vnet-connectiviteit</span><span class="sxs-lookup"><span data-stu-id="b0c77-117">Inter-Vnet connectivity</span></span>](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a><span data-ttu-id="b0c77-118">Stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="b0c77-118">Troubleshooting steps</span></span>

<span data-ttu-id="b0c77-119">Volg deze stappen voor het oplossen van het probleem.</span><span class="sxs-lookup"><span data-stu-id="b0c77-119">Follow these steps to troubleshoot the problem.</span></span> <span data-ttu-id="b0c77-120">Controleer of het probleem opgelost na elke stap is.</span><span class="sxs-lookup"><span data-stu-id="b0c77-120">Check whether the problem is resolved after each step.</span></span> 

### <a name="step-1-check-if-nic-is-misconfigured"></a><span data-ttu-id="b0c77-121">Stap 1: Controleer of NIC is onjuist geconfigureerd</span><span class="sxs-lookup"><span data-stu-id="b0c77-121">Step 1: Check if NIC is misconfigured</span></span>

<span data-ttu-id="b0c77-122">Ga als volgt [netwerkinterface herstellen voor virtuele machine van Windows Azure](../virtual-machines/windows/reset-network-interface.md).</span><span class="sxs-lookup"><span data-stu-id="b0c77-122">Follow [How to reset network interface for Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span></span> 

<span data-ttu-id="b0c77-123">Als het probleem optreedt nadat u de netwerkinterface (NIC) hebt gewijzigd, voert u deze stappen:</span><span class="sxs-lookup"><span data-stu-id="b0c77-123">If the problem occurs after you modify the network interface (NIC), follow these steps:</span></span>

<span data-ttu-id="b0c77-124">**Virtuele machines mulit-NIC**</span><span class="sxs-lookup"><span data-stu-id="b0c77-124">**Mulit-NIC VMs**</span></span>

1. <span data-ttu-id="b0c77-125">Toevoegen van een NIC.</span><span class="sxs-lookup"><span data-stu-id="b0c77-125">Add a NIC.</span></span>
2. <span data-ttu-id="b0c77-126">Los de problemen op de onjuiste NIC of verwijderen van ongeldige NIC.</span><span class="sxs-lookup"><span data-stu-id="b0c77-126">Fix the problems in the bad NIC or remove bad NIC.</span></span>  <span data-ttu-id="b0c77-127">Vervolgens readd de NIC.</span><span class="sxs-lookup"><span data-stu-id="b0c77-127">Then readd the NIC.</span></span>

<span data-ttu-id="b0c77-128">Zie voor meer informatie [netwerkinterfaces toevoegen of verwijderen van virtuele machines](virtual-network-network-interface-vm.md).</span><span class="sxs-lookup"><span data-stu-id="b0c77-128">For more information, see [Add network interfaces to or remove from virtual machines](virtual-network-network-interface-vm.md).</span></span>

<span data-ttu-id="b0c77-129">**Één NIC VM**</span><span class="sxs-lookup"><span data-stu-id="b0c77-129">**Single-NIC VM**</span></span> 

- [<span data-ttu-id="b0c77-130">Implementeer Windows VM opnieuw</span><span class="sxs-lookup"><span data-stu-id="b0c77-130">Redeploy Windows VM</span></span>](../virtual-machines/windows/redeploy-to-new-node.md)
- [<span data-ttu-id="b0c77-131">Virtuele Linux-machine implementeren</span><span class="sxs-lookup"><span data-stu-id="b0c77-131">Redeploy Linux VM</span></span>](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a><span data-ttu-id="b0c77-132">Stap 2: Controleer of het netwerkverkeer wordt geblokkeerd door NSG of UDR</span><span class="sxs-lookup"><span data-stu-id="b0c77-132">Step 2: Check if network traffic is blocked by NSG or UDR</span></span>

<span data-ttu-id="b0c77-133">Gebruikmaken van [netwerk-Watcher IP-stroom controleren](../network-watcher/network-watcher-ip-flow-verify-overview.md) en [NSG stroom logboekregistratie](../network-watcher/network-watcher-nsg-flow-logging-overview.md) om te bepalen of er is een Netwerkbeveiligingsgroep of door de gebruiker gedefinieerde Route die netwerkverkeer verstoort.</span><span class="sxs-lookup"><span data-stu-id="b0c77-133">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) to identify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span>

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a><span data-ttu-id="b0c77-134">Stap 3: Controleren als netwerkverkeer wordt geblokkeerd door VM-firewall</span><span class="sxs-lookup"><span data-stu-id="b0c77-134">Step 3: Check if network traffic is blocked by VM firewall</span></span>

<span data-ttu-id="b0c77-135">De firewall uitschakelen en vervolgens het resultaat te testen.</span><span class="sxs-lookup"><span data-stu-id="b0c77-135">Disable the firewall, and then test the result.</span></span> <span data-ttu-id="b0c77-136">Als het probleem is opgelost, Controleer de instellingen in de firewall en opnieuw in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="b0c77-136">If the problem is resolved, validate the settings in the firewall and re-enable.</span></span>

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-the-port"></a><span data-ttu-id="b0c77-137">Stap 4: Controleren of VM-app of service op poort luistert</span><span class="sxs-lookup"><span data-stu-id="b0c77-137">Step 4: Check whether VM app or service is listening on the port</span></span>

<span data-ttu-id="b0c77-138">U kunt een van de volgende methoden gebruiken om te controleren of VM-toepassing of Service op poort luistert</span><span class="sxs-lookup"><span data-stu-id="b0c77-138">You can use one of the following methods to check whether VM Application or Service is listening on the port</span></span>

- <span data-ttu-id="b0c77-139">Voer de volgende opdrachten om te controleren of de server op deze poort luistert.</span><span class="sxs-lookup"><span data-stu-id="b0c77-139">Run the following commands to check whether the server is listening on that port.</span></span>

<span data-ttu-id="b0c77-140">**Windows-VM**</span><span class="sxs-lookup"><span data-stu-id="b0c77-140">**Windows VM**</span></span>

    netstat –ano

<span data-ttu-id="b0c77-141">**Linux-VM**</span><span class="sxs-lookup"><span data-stu-id="b0c77-141">**Linux VM**</span></span>

    netstat -l

- <span data-ttu-id="b0c77-142">Voer de **Telnet** opdracht op de virtuele machine naar zichzelf voor het testen van de poort.</span><span class="sxs-lookup"><span data-stu-id="b0c77-142">Run the **Telnet** command on the VM to itself to test the port.</span></span> <span data-ttu-id="b0c77-143">Als de test mislukt, is niet toepassing of service geconfigureerd om te luisteren op poort.</span><span class="sxs-lookup"><span data-stu-id="b0c77-143">If the test fails, application or service is not configured to listen on the port.</span></span>

### <a name="step-5-check-whether-the-problem-is-caused-by-snat"></a><span data-ttu-id="b0c77-144">Stap 5: Controleer of het probleem wordt veroorzaakt door snat omzetten</span><span class="sxs-lookup"><span data-stu-id="b0c77-144">Step 5: Check whether the problem is caused by SNAT</span></span>

<span data-ttu-id="b0c77-145">In sommige scenario's, wordt de virtuele machine geplaatst achter een Load balance oplossing met een afhankelijkheid op resources buiten Azure.</span><span class="sxs-lookup"><span data-stu-id="b0c77-145">In some scenarios, the VM is placed behind a Load balance solution that has a dependency on resources outside of Azure.</span></span> <span data-ttu-id="b0c77-146">In deze scenario's, als u met de verbinding problemen, het probleem mogelijk worden veroorzaakt door [snat omzetten poort bronuitputting](../load-balancer/load-balancer-outbound-connections.md).</span><span class="sxs-lookup"><span data-stu-id="b0c77-146">In these scenarios, if you experience intermittent connection problems, the problem may be caused by [SNAT port exhaustion](../load-balancer/load-balancer-outbound-connections.md).</span></span> <span data-ttu-id="b0c77-147">Het probleem op te lossen moet u een VIP (of ILPIP voor klassiek) maken voor elke virtuele machine die zich achter de Load balancer en beveiligen met NSG of ACL.</span><span class="sxs-lookup"><span data-stu-id="b0c77-147">To resolve the issue, create a VIP (or ILPIP for classic) for each VM that is behind the Load balancer and secure with NSG or ACL.</span></span> 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm"></a><span data-ttu-id="b0c77-148">Stap 6: Controleren of verkeer wordt geblokkeerd door de ACL's voor de klassieke virtuele machine</span><span class="sxs-lookup"><span data-stu-id="b0c77-148">Step 6: Check whether traffic is blocked by ACLs for the classic VM</span></span>

<span data-ttu-id="b0c77-149">Een ACL biedt de mogelijkheid om selectief toestaan of weigeren van verkeer voor het eindpunt van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b0c77-149">An ACL provides the ability to selectively permit or deny traffic for a virtual machine endpoint.</span></span> <span data-ttu-id="b0c77-150">Zie voor meer informatie [beheren de ACL voor een eindpunt](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span><span class="sxs-lookup"><span data-stu-id="b0c77-150">For more information, see [Manage the ACL on an endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

### <a name="step-7-check-whether-the-endpoint-is-created-for-the-classic-vm"></a><span data-ttu-id="b0c77-151">Stap 7: Controleren of het eindpunt voor de klassieke virtuele machine wordt gemaakt</span><span class="sxs-lookup"><span data-stu-id="b0c77-151">Step 7: Check whether the endpoint is created for the classic VM</span></span>

<span data-ttu-id="b0c77-152">Alle virtuele machines die u maakt in Azure met behulp van het klassieke implementatiemodel kunnen automatisch via een particulier netwerkkanaal met andere virtuele machines in dezelfde cloudservice- of virtueel netwerk communiceren.</span><span class="sxs-lookup"><span data-stu-id="b0c77-152">All VMs that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="b0c77-153">Computers met andere virtuele netwerken vereisen echter eindpunten het binnenkomend netwerkverkeer naar een virtuele machine wordt omgeleid.</span><span class="sxs-lookup"><span data-stu-id="b0c77-153">However, computers on other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="b0c77-154">Zie voor meer informatie [het instellen van eindpunten](../virtual-machines/windows/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="b0c77-154">For more information, see [How to set up endpoints](../virtual-machines/windows/classic/setup-endpoints.md).</span></span>

### <a name="step-8-unable-to-connect-to-a-vm-network-share"></a><span data-ttu-id="b0c77-155">Stap 8: Kan geen verbinding met een VM-netwerkshare</span><span class="sxs-lookup"><span data-stu-id="b0c77-155">Step 8: Unable to connect to a VM network share</span></span>

<span data-ttu-id="b0c77-156">Als u geen verbinding maken met een VM-netwerkshare, kunt u het probleem veroorzaakt door niet beschikbaar NIC's in de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b0c77-156">If you are unable to connect to a VM network share, the problem can be caused by unavailable NICs in the VM.</span></span> <span data-ttu-id="b0c77-157">Zie het verwijderen van de niet beschikbaar NIC's [het verwijderen van de niet beschikbaar NIC's](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span><span class="sxs-lookup"><span data-stu-id="b0c77-157">To delete the unavailable NICs, see [How to delete the unavailable NICs](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span></span>

### <a name="step-9-inter-vnet-connectivity"></a><span data-ttu-id="b0c77-158">Stap 9: Inter Vnet-connectiviteit</span><span class="sxs-lookup"><span data-stu-id="b0c77-158">Step 9: Inter-Vnet connectivity</span></span>

<span data-ttu-id="b0c77-159">Gebruikmaken van [netwerk-Watcher IP-stroom controleren](../network-watcher/network-watcher-ip-flow-verify-overview.md) en [NSG stroom logboekregistratie](../network-watcher/network-watcher-nsg-flow-logging-overview.md) om te bepalen of er is een Netwerkbeveiligingsgroep of door de gebruiker gedefinieerde Route die netwerkverkeer verstoort.</span><span class="sxs-lookup"><span data-stu-id="b0c77-159">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) to identify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span> <span data-ttu-id="b0c77-160">U kunt ook uw Inter Vnet-configuratie valideren [hier](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span><span class="sxs-lookup"><span data-stu-id="b0c77-160">You can also validate your Inter-Vnet configuration [here](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span></span>

### <a name="need-help-contact-support"></a><span data-ttu-id="b0c77-161">Hulp nodig?</span><span class="sxs-lookup"><span data-stu-id="b0c77-161">Need help?</span></span> <span data-ttu-id="b0c77-162">Neem contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="b0c77-162">Contact support.</span></span>
<span data-ttu-id="b0c77-163">Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ophalen van uw probleem snel worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="b0c77-163">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>