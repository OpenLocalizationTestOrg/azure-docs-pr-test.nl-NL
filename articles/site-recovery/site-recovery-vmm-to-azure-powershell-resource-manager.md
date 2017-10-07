---
title: aaaReplicate Hyper-V virtuele machines in VMM-clouds met Azure Site Recovery en PowerShell (Resource Manager) | Microsoft Docs
description: Hyper-V virtuele machines in VMM-clouds met Azure Site Recovery en PowerShell repliceren
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="2c3af-103">Hyper-V virtuele machines in VMM-clouds tooAzure met PowerShell en Azure Resource Manager repliceren</span><span class="sxs-lookup"><span data-stu-id="2c3af-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c3af-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2c3af-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="2c3af-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2c3af-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="2c3af-106">Klassieke portal</span><span class="sxs-lookup"><span data-stu-id="2c3af-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="2c3af-107">PowerShell - Klassiek</span><span class="sxs-lookup"><span data-stu-id="2c3af-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="2c3af-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2c3af-108">Overview</span></span>
<span data-ttu-id="2c3af-109">Azure Site Recovery draagt bij aan tooyour zakelijke continuïteit en noodherstel (BCDR) strategie door replicatie, failovers en herstel van virtuele machines in een aantal implementatiescenario's te organiseren.</span><span class="sxs-lookup"><span data-stu-id="2c3af-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="2c3af-110">Voor een volledige lijst van de implementatie van scenario's Hallo Zie [Azure Site Recovery-overzicht](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2c3af-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="2c3af-111">Dit artikel laat zien hoe toouse PowerShell tooautomate algemene taken moet u tooperform bij het instellen van Azure Site Recovery tooreplicate Hyper-V virtuele machines in System Center VMM-clouds tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="2c3af-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="2c3af-112">Hallo artikel bevat vereisten voor Hallo scenario en laat zien u</span><span class="sxs-lookup"><span data-stu-id="2c3af-112">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="2c3af-113">Hoe tooset van een Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="2c3af-113">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="2c3af-114">Hello Azure Site Recovery Provider installeren op de bronserver VMM Hallo</span><span class="sxs-lookup"><span data-stu-id="2c3af-114">Install hello Azure Site Recovery Provider on hello source VMM server</span></span>
* <span data-ttu-id="2c3af-115">Hallo-server registreren in de kluis hello, Azure storage-account toevoegen</span><span class="sxs-lookup"><span data-stu-id="2c3af-115">Register hello server in hello vault, add an Azure storage account</span></span>
* <span data-ttu-id="2c3af-116">Hello Azure Recovery Services agent op Hyper-V-host-servers installeren</span><span class="sxs-lookup"><span data-stu-id="2c3af-116">Install hello Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="2c3af-117">Configureer beveiligingsinstellingen voor VMM-clouds die toegepast tooall beveiligde virtuele machines worden</span><span class="sxs-lookup"><span data-stu-id="2c3af-117">Configure protection settings for VMM clouds, that will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="2c3af-118">Schakel de beveiliging voor deze virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="2c3af-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="2c3af-119">Test Hallo failover-toomake controleren of dat alles werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="2c3af-119">Test hello fail-over toomake sure everything's working as expected.</span></span>

<span data-ttu-id="2c3af-120">Als u problemen bij het instellen van dit scenario, stel uw vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2c3af-120">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="2c3af-121">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2c3af-121">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2c3af-122">In dit artikel bevat informatie over met behulp van Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="2c3af-122">This article covers using hello Resource Manager deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="2c3af-123">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="2c3af-123">Before you start</span></span>
<span data-ttu-id="2c3af-124">Zorg ervoor dat u deze vereisten hebt voldaan:</span><span class="sxs-lookup"><span data-stu-id="2c3af-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="2c3af-125">Vereisten voor Azure</span><span class="sxs-lookup"><span data-stu-id="2c3af-125">Azure prerequisites</span></span>
* <span data-ttu-id="2c3af-126">U hebt een [Microsoft Azure](https://azure.microsoft.com/)-account nodig.</span><span class="sxs-lookup"><span data-stu-id="2c3af-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="2c3af-127">Als u niet hebt, beginnen met een [gratis account](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="2c3af-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="2c3af-128">U kunt bovendien lezen over Hallo [prijzen van Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="2c3af-128">In addition, you can read about hello [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="2c3af-129">Als u uit Hallo tooa CSP abonnement replicatiescenario probeert, hebt u een CSP-abonnement nodig.</span><span class="sxs-lookup"><span data-stu-id="2c3af-129">You'll need a CSP subscription if you are trying out hello replication tooa CSP subscription scenario.</span></span> <span data-ttu-id="2c3af-130">Meer informatie over Hallo CSP programma in [hoe tooenroll Hallo CSP programma](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c3af-130">Learn more about hello CSP program in [how tooenroll in hello CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="2c3af-131">U moet een tooAzure toostore gerepliceerde gegevens van Azure v2-opslag (Resource Manager)-account.</span><span class="sxs-lookup"><span data-stu-id="2c3af-131">You'll need an Azure v2 storage (Resource Manager) account toostore data replicated tooAzure.</span></span> <span data-ttu-id="2c3af-132">Hallo-account moet geo-replicatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2c3af-132">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="2c3af-133">Deze moet in dezelfde regio bevinden als hello Azure Site Recovery-service hello, en worden gekoppeld aan Hallo hetzelfde abonnement of Hallo CSP-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2c3af-133">It should be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription or hello CSP subscription.</span></span> <span data-ttu-id="2c3af-134">toolearn meer informatie over het instellen van Azure-opslag, Zie Hallo [tooMicrosoft inleiding Azure Storage](../storage/common/storage-introduction.md) ter referentie.</span><span class="sxs-lookup"><span data-stu-id="2c3af-134">toolearn more about setting up Azure storage, see hello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="2c3af-135">U moet zorgen dat virtuele machines die u wilt dat tooprotect aan Hallo voldoen toomake [vereisten van de virtuele machine van Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="2c3af-135">You'll need toomake sure that virtual machines you want tooprotect comply with hello [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> <span data-ttu-id="2c3af-136">Er zijn momenteel alleen VM niveau bewerkingen mogelijk via Powershell.</span><span class="sxs-lookup"><span data-stu-id="2c3af-136">Currently, only VM level operations are possible through Powershell.</span></span> <span data-ttu-id="2c3af-137">Ondersteuning voor niveau herstelbewerkingen plan zal binnenkort worden gesteld.</span><span class="sxs-lookup"><span data-stu-id="2c3af-137">Support for recovery plan level operations will be made soon.</span></span>  <span data-ttu-id="2c3af-138">Nu bent u beperkt tooperforming failovers van datacenters alleen op een granulatie 'beveiligde virtuele machine' en niet op een herstelplan-niveau.</span><span class="sxs-lookup"><span data-stu-id="2c3af-138">For now, you are limited tooperforming fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.</span></span>
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="2c3af-139">VMM-vereisten</span><span class="sxs-lookup"><span data-stu-id="2c3af-139">VMM prerequisites</span></span>
* <span data-ttu-id="2c3af-140">U moet de VMM-server waarop System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="2c3af-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="2c3af-141">De VMM-servers die virtuele machines bevat die u wilt, tooprotect hello Azure Site Recovery Provider moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2c3af-141">Any VMM server containing virtual machines you want tooprotect must be running hello Azure Site Recovery Provider.</span></span> <span data-ttu-id="2c3af-142">Dit wordt geïnstalleerd tijdens de implementatie van Azure Site Recovery Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c3af-142">This is installed during hello Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="2c3af-143">U moet ten minste één cloud op Hallo gewenste tooprotect VMM-server.</span><span class="sxs-lookup"><span data-stu-id="2c3af-143">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="2c3af-144">Hallo cloud moet bevatten:</span><span class="sxs-lookup"><span data-stu-id="2c3af-144">hello cloud should contain:</span></span>
  * <span data-ttu-id="2c3af-145">Een of meer VMM-hostgroepen.</span><span class="sxs-lookup"><span data-stu-id="2c3af-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="2c3af-146">Een of meer Hyper-V-hostservers of -clusters in elke hostgroep.</span><span class="sxs-lookup"><span data-stu-id="2c3af-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="2c3af-147">Een of meer virtuele machines op Hallo bron Hyper-V-server.</span><span class="sxs-lookup"><span data-stu-id="2c3af-147">One or more virtual machines on hello source Hyper-V server.</span></span>
* <span data-ttu-id="2c3af-148">Meer informatie over het instellen van VMM-clouds:</span><span class="sxs-lookup"><span data-stu-id="2c3af-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="2c3af-149">Meer informatie over VMM-privéclouds in [What's New in een Privécloud met System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) en in [VMM 2012 en Hallo clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span><span class="sxs-lookup"><span data-stu-id="2c3af-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and hello clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="2c3af-150">Meer informatie over [configureren Hallo VMM fabric cloud](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="2c3af-150">Learn about [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="2c3af-151">Nadat uw cloud fabric-elementen voldaan zijn informatie over het maken van privéclouds in [maken van een privécloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) en in [overzicht: privéclouds maken met System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span><span class="sxs-lookup"><span data-stu-id="2c3af-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="2c3af-152">Hyper-V-vereisten</span><span class="sxs-lookup"><span data-stu-id="2c3af-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="2c3af-153">Hallo Hyper-V-hostservers moeten ten minste draaien **Windows Server 2012** met Hyper-V-rol of **Microsoft Hyper-V Server 2012** en hebben Hallo nieuwste updates zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="2c3af-153">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="2c3af-154">Als u Hyper-V in een cluster uitvoert, wordt die clusterbroker niet automatisch gemaakt als u een cluster op basis van een statisch IP-adres hebt.</span><span class="sxs-lookup"><span data-stu-id="2c3af-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="2c3af-155">U moet tooconfigure hello clusterbroker handmatig.</span><span class="sxs-lookup"><span data-stu-id="2c3af-155">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="2c3af-156">voor</span><span class="sxs-lookup"><span data-stu-id="2c3af-156">For</span></span>
* <span data-ttu-id="2c3af-157">Zie voor instructies [hoe tooConfigure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c3af-157">For instructions see [How tooConfigure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="2c3af-158">Alle Hyper-V-hostserver of het cluster waarvoor u de toomanage beveiliging moet worden opgenomen in een VMM-cloud.</span><span class="sxs-lookup"><span data-stu-id="2c3af-158">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="2c3af-159">Vereisten voor netwerktoewijzing</span><span class="sxs-lookup"><span data-stu-id="2c3af-159">Network mapping prerequisites</span></span>
<span data-ttu-id="2c3af-160">Wanneer u virtuele machines in Azure beveiligt, toegewezen netwerktoewijzing Hallo Hallo virtuele-machinenetwerken op Hallo bron-VMM-server en doel-Azure-netwerken tooenable Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="2c3af-160">When you protect virtual machines in Azure, hello network mapping  maps hello virtual machine networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="2c3af-161">Alle machines die een failover op Hallo dezelfde netwerk verbinding kan maken van andere, ongeacht welk herstelplan ze tooeach.</span><span class="sxs-lookup"><span data-stu-id="2c3af-161">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="2c3af-162">Als een netwerkgateway ingesteld op Hallo Azure-doelnetwerk is, kunnen virtuele machines verbinding tooother on-premises virtuele machines maken.</span><span class="sxs-lookup"><span data-stu-id="2c3af-162">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="2c3af-163">Als u geen netwerktoewijzing configureert, alleen virtuele machines met failover in Hallo dezelfde Hallo herstelplan kunnen tooconnect tooeach andere worden na de failover-tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2c3af-163">If you don’t configure network mapping, only hello virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after fail-over tooAzure.</span></span>

<span data-ttu-id="2c3af-164">Als u wilt dat de netwerktoewijzing toodeploy moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="2c3af-164">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="2c3af-165">Hallo virtuele machines die u wilt dat tooprotect op Hallo bron-VMM-server moet zijn verbonden tooa VM-netwerk.</span><span class="sxs-lookup"><span data-stu-id="2c3af-165">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="2c3af-166">Dit netwerk moet gekoppelde tooa logisch netwerk dat is gekoppeld aan Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="2c3af-166">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="2c3af-167">Een Azure-netwerk toowhich gerepliceerde virtuele machines verbinding kunnen maken na failover.</span><span class="sxs-lookup"><span data-stu-id="2c3af-167">An Azure network toowhich replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="2c3af-168">U selecteert dit netwerk op Hallo moment van failover.</span><span class="sxs-lookup"><span data-stu-id="2c3af-168">You'll select this network at hello time of fail-over.</span></span> <span data-ttu-id="2c3af-169">Hallo-netwerk moet zich in Hallo dezelfde regio bevinden als uw Azure Site Recovery-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2c3af-169">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="2c3af-170">Meer informatie over de netwerktoewijzing in</span><span class="sxs-lookup"><span data-stu-id="2c3af-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="2c3af-171">Hoe tooconfigure logische netwerken in VMM</span><span class="sxs-lookup"><span data-stu-id="2c3af-171">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="2c3af-172">Hoe tooconfigure VM-netwerken en gateways in VMM</span><span class="sxs-lookup"><span data-stu-id="2c3af-172">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="2c3af-173">Hoe tooconfigure en monitor virtuele netwerken in Azure</span><span class="sxs-lookup"><span data-stu-id="2c3af-173">How tooconfigure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="2c3af-174">PowerShell-vereisten</span><span class="sxs-lookup"><span data-stu-id="2c3af-174">PowerShell prerequisites</span></span>
<span data-ttu-id="2c3af-175">Zorg ervoor dat u Azure PowerShell gereed toogo hebt.</span><span class="sxs-lookup"><span data-stu-id="2c3af-175">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="2c3af-176">Als u al van PowerShell gebruikmaakt, moet u tooupgrade tooversion 0.8.10 of hoger.</span><span class="sxs-lookup"><span data-stu-id="2c3af-176">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="2c3af-177">Zie voor informatie over het instellen van PowerShell Hallo [tooinstall te leiden en configureer Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="2c3af-177">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="2c3af-178">Zodra u hebt ingesteld en geconfigureerd PowerShell, kunt u alle beschikbare Hallo-cmdlets voor Hallo service weergeven [hier](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2c3af-178">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="2c3af-179">toolearn over tips waarmee u Hallo-cmdlets, zoals hoe parameterwaarden, in- en uitgangen doorgaans worden uitgevoerd in Azure PowerShell gebruiken kunt Zie Hallo [tooget slag met Azure-Cmdlets begeleiden](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="2c3af-179">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="2c3af-180">Stap 1: Stel Hallo-abonnement</span><span class="sxs-lookup"><span data-stu-id="2c3af-180">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="2c3af-181">Van Azure powershell, aanmelding tooyour Azure-account: met behulp van de volgende cmdlets Hallo</span><span class="sxs-lookup"><span data-stu-id="2c3af-181">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="2c3af-182">Een lijst van uw abonnementen ophalen.</span><span class="sxs-lookup"><span data-stu-id="2c3af-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="2c3af-183">Dit worden Hallo subscriptionIDs voor elk Hallo abonnementen vermeld.</span><span class="sxs-lookup"><span data-stu-id="2c3af-183">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="2c3af-184">Noteer Hallo abonnements-id van het Hallo-abonnement waarmee u toocreate Hallo recovery services-kluis wenst</span><span class="sxs-lookup"><span data-stu-id="2c3af-184">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="2c3af-185">Hallo-abonnement in welke Hallo recovery services-kluis gemaakt is door de vermelding Hallo abonnements-ID toobe instellen</span><span class="sxs-lookup"><span data-stu-id="2c3af-185">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="2c3af-186">Stap 2: Maak een Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="2c3af-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="2c3af-187">Een resourcegroep maken in Azure Resource Manager als u nog niet hebt</span><span class="sxs-lookup"><span data-stu-id="2c3af-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="2c3af-188">Een nieuwe Recovery Services-kluis maken en opslaan van Hallo ASR kluis object is gemaakt in een variabele (later worden gebruikt).</span><span class="sxs-lookup"><span data-stu-id="2c3af-188">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="2c3af-189">U kunt ook Hallo ASR kluis post maken van het object met de cmdlet Get-AzureRMRecoveryServicesVault Hallo ophalen:-</span><span class="sxs-lookup"><span data-stu-id="2c3af-189">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="2c3af-190">Stap 3: Hallo Recovery Services-kluis context instellen</span><span class="sxs-lookup"><span data-stu-id="2c3af-190">Step 3: Set hello Recovery Services Vault context</span></span>

<span data-ttu-id="2c3af-191">Hallo kluis context instellen door te voeren Hallo onder opdracht.</span><span class="sxs-lookup"><span data-stu-id="2c3af-191">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="2c3af-192">Stap 4: Hello Azure Site Recovery Provider installeren</span><span class="sxs-lookup"><span data-stu-id="2c3af-192">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="2c3af-193">Maak een map door het uitvoeren van de volgende opdracht Hallo op Hallo-VMM-machine:</span><span class="sxs-lookup"><span data-stu-id="2c3af-193">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="2c3af-194">Hallo-bestanden met behulp van de provider Hallo gedownload door het uitvoeren van de volgende opdracht Hallo uitpakken</span><span class="sxs-lookup"><span data-stu-id="2c3af-194">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="2c3af-195">Hallo-provider met behulp van de volgende opdrachten Hallo installeren:</span><span class="sxs-lookup"><span data-stu-id="2c3af-195">Install hello provider using hello following commands:</span></span>

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   <span data-ttu-id="2c3af-196">Wachten op Hallo installatie toofinish.</span><span class="sxs-lookup"><span data-stu-id="2c3af-196">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="2c3af-197">Hallo-server registreren in met behulp van de volgende opdracht Hallo Hallo-kluis:</span><span class="sxs-lookup"><span data-stu-id="2c3af-197">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="2c3af-198">Stap 5: Een Azure storage-account maken</span><span class="sxs-lookup"><span data-stu-id="2c3af-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="2c3af-199">Als u geen Azure storage-account hebt, een geo-replicatie ingeschakeld-account maken in Hallo dezelfde geo als Hallo door het uitvoeren van de volgende opdracht Hallo-kluis:</span><span class="sxs-lookup"><span data-stu-id="2c3af-199">If you don't have an Azure storage account, create a geo-replication enabled account in hello same geo as hello vault by running hello following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="2c3af-200">Houd er rekening mee dat Hallo storage-account moet in dezelfde regio bevinden als de service Azure Site Recovery Hallo Hallo en worden gekoppeld aan hetzelfde abonnement Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c3af-200">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="2c3af-201">Stap 6: Hello Azure Recovery Services-Agent installeren</span><span class="sxs-lookup"><span data-stu-id="2c3af-201">Step 6: Install hello Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="2c3af-202">Hello Azure Recovery Services agent op downloaden [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) en installeren op elke Hyper-V-host-server zich bevindt in VMM Hallo u clouds wilt tooprotect.</span><span class="sxs-lookup"><span data-stu-id="2c3af-202">Download hello Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>
2. <span data-ttu-id="2c3af-203">Voer Hallo opdracht op alle VMM-hosts te volgen:</span><span class="sxs-lookup"><span data-stu-id="2c3af-203">Run hello following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="2c3af-204">Stap 7: Cloud configureren beveiligingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="2c3af-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="2c3af-205">Maak een beleid voor replicatie tooAzure door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="2c3af-205">Create a replication policy tooAzure by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="2c3af-206">Een beveiligingscontainer door het uitvoeren van de volgende opdrachten Hallo ophalen:</span><span class="sxs-lookup"><span data-stu-id="2c3af-206">Get a protection container by running hello following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="2c3af-207">Hallo beleid details tooa variabele Hallo-taak die is gemaakt met en houd Hallo beschrijvende naam krijgen:</span><span class="sxs-lookup"><span data-stu-id="2c3af-207">Get hello policy details tooa variable using hello job that was created and mentioning hello friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="2c3af-208">Koppeling van de beveiligingscontainer Hallo Hallo beginnen met Hallo replicatiebeleid:</span><span class="sxs-lookup"><span data-stu-id="2c3af-208">Start hello association of hello protection container with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="2c3af-209">Nadat het Hallo-taak is voltooid, voert u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2c3af-209">After hello job has finished, run hello following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="2c3af-210">Nadat het Hallo taak zijn verwerkt, voert u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2c3af-210">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="2c3af-211">Hallo-bewerking is toocheck Hallo voltooid Hallo stappen in [Monitoractiviteit](#monitor).</span><span class="sxs-lookup"><span data-stu-id="2c3af-211">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="2c3af-212">Stap 8: Netwerktoewijzing configureren</span><span class="sxs-lookup"><span data-stu-id="2c3af-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="2c3af-213">Voordat u begint met de netwerktoewijzing controleert u of virtuele machines op de bronserver VMM Hallo verbonden tooa VM-netwerk.</span><span class="sxs-lookup"><span data-stu-id="2c3af-213">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="2c3af-214">Daarnaast maakt u een of meer virtuele netwerken in Azure.</span><span class="sxs-lookup"><span data-stu-id="2c3af-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="2c3af-215">Meer informatie over hoe toocreate een virtueel netwerk met Azure Resource Manager en PowerShell in [een virtueel netwerk maken met een site-naar-site VPN-verbinding met Azure Resource Manager en PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="2c3af-215">Learn more about how toocreate a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="2c3af-216">Houd er rekening mee dat meerdere netwerken voor virtuele Machine toegewezen tooa één Azure-netwerk kunnen worden.</span><span class="sxs-lookup"><span data-stu-id="2c3af-216">Note that multiple Virtual Machine networks can be mapped tooa single Azure network.</span></span> <span data-ttu-id="2c3af-217">Als Hallo doelnetwerk meerdere subnetten heeft en een van deze subnetten Hallo heeft dezelfde naam als het subnet waarop Hallo bron virtual machine zich bevindt, wordt Hallo replica virtuele machine verbonden toothat Doelsubnet worden na failover.</span><span class="sxs-lookup"><span data-stu-id="2c3af-217">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after fail-over.</span></span> <span data-ttu-id="2c3af-218">Als er geen Doelsubnet met een overeenkomende naam, wordt de Hallo virtuele machine verbonden toohello eerste subnet in het Hallo-netwerk zijn.</span><span class="sxs-lookup"><span data-stu-id="2c3af-218">If there is no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

1. <span data-ttu-id="2c3af-219">de eerste opdracht Hallo opgehaald servers voor de huidige Azure Site Recovery-kluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c3af-219">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="2c3af-220">Hallo opdracht slaat Hallo Microsoft Azure Site Recovery-servers in Hallo $Servers matrixvariabele.</span><span class="sxs-lookup"><span data-stu-id="2c3af-220">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="2c3af-221">de tweede opdracht Hallo ophalen Hallo een netwerk met site recovery voor de eerste server Hallo in Hallo $Servers matrix.</span><span class="sxs-lookup"><span data-stu-id="2c3af-221">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="2c3af-222">Hallo opdracht slaat Hallo netwerken in Hallo $Networks variabele.</span><span class="sxs-lookup"><span data-stu-id="2c3af-222">hello command stores hello networks in hello $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="2c3af-223">Hallo derde opdracht haalt virtuele Azure-netwerken en dat de waarde in Hallo $AzureVmNetworks variabele.</span><span class="sxs-lookup"><span data-stu-id="2c3af-223">hello third command gets Azure virtual networks, and then that value in hello $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="2c3af-224">Hallo laatste cmdlet maakt een toewijzing tussen Hallo primaire netwerk en hello Azure virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2c3af-224">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="2c3af-225">het primaire netwerk Hallo geeft Hallo cmdlet als Hallo eerste element van $Networks.</span><span class="sxs-lookup"><span data-stu-id="2c3af-225">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="2c3af-226">Hallo cmdlet geeft een VM-netwerk als eerste element van $AzureVmNetworks Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c3af-226">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="2c3af-227">Stap 9: Beveiliging voor virtuele machines inschakelen</span><span class="sxs-lookup"><span data-stu-id="2c3af-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="2c3af-228">Nadat het Hallo-servers, clouds en netwerken correct zijn geconfigureerd, kunt u beveiliging voor virtuele machines in de cloud Hallo inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2c3af-228">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

 <span data-ttu-id="2c3af-229">Let op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="2c3af-229">Note hello following:</span></span>

* <span data-ttu-id="2c3af-230">Virtuele machines moeten voldoen aan de Azure-vereisten.</span><span class="sxs-lookup"><span data-stu-id="2c3af-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="2c3af-231">Controleer deze in [vereisten en ondersteuning](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in Hallo planning guide.</span><span class="sxs-lookup"><span data-stu-id="2c3af-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in hello planning guide.</span></span>
* <span data-ttu-id="2c3af-232">tooenable protection, Hallo-besturingssysteem en de schijfeigenschappen besturingssysteem moeten worden ingesteld voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2c3af-232">tooenable protection, hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="2c3af-233">Wanneer u een virtuele machine in VMM met een virtuele machine-sjabloon maakt, kunt u Hallo-eigenschap instellen.</span><span class="sxs-lookup"><span data-stu-id="2c3af-233">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="2c3af-234">U kunt deze eigenschappen voor de bestaande virtuele machines ook instellen op Hallo **algemene** en **hardwareconfiguratie** tabbladen van de eigenschappen van de virtuele machine Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c3af-234">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="2c3af-235">Als u deze eigenschappen niet ingesteld in VMM, moet u kunnen tooconfigure ze in hello Azure Site Recovery-portal.</span><span class="sxs-lookup"><span data-stu-id="2c3af-235">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="2c3af-236">tooenable beveiliging Hallo opdracht tooget hello beveiligingscontainer volgende uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="2c3af-236">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="2c3af-237">Hallo beveiligde entiteit (VM) door het uitvoeren van de volgende opdracht Hallo ophalen:</span><span class="sxs-lookup"><span data-stu-id="2c3af-237">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="2c3af-238">Hallo DR voor Hallo VM inschakelen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="2c3af-238">Enable hello DR for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="2c3af-239">Uw implementatie testen</span><span class="sxs-lookup"><span data-stu-id="2c3af-239">Test your deployment</span></span>
<span data-ttu-id="2c3af-240">tootest uw implementatie kunt u een test uitvoeren failover voor een enkele virtuele machine of een herstelplan dat bestaat uit meerdere virtuele machines maken en een test failover voor Hallo plan uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2c3af-240">tootest your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for hello plan.</span></span> <span data-ttu-id="2c3af-241">Failover van de test wordt uw failover- en herstelmechanisme in een geïsoleerd netwerk gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="2c3af-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="2c3af-242">Opmerking:</span><span class="sxs-lookup"><span data-stu-id="2c3af-242">Note that:</span></span>

* <span data-ttu-id="2c3af-243">Als u tooconnect toohello virtuele machine in Azure met extern bureaublad na failover Hallo wilt, moet u verbinding met extern bureaublad inschakelen op Hallo virtuele machine voordat u Hallo testfailover uitvoert.</span><span class="sxs-lookup"><span data-stu-id="2c3af-243">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello fail-over, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="2c3af-244">Na een failover gebruikt u een openbaar IP-adres tooconnect toohello virtuele machine in Azure met behulp van extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="2c3af-244">After fail-over, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="2c3af-245">Als u toodo dit wilt, zorg ervoor dat u geen domeinbeleid hebt geïmplementeerd die verhinderen dat u verbinding maakt tooa virtuele machine via een openbaar adres.</span><span class="sxs-lookup"><span data-stu-id="2c3af-245">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="2c3af-246">Hallo-bewerking is toocheck Hallo voltooid Hallo stappen in [Monitoractiviteit](#monitor).</span><span class="sxs-lookup"><span data-stu-id="2c3af-246">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="2c3af-247">Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2c3af-247">Run a test failover</span></span>
- <span data-ttu-id="2c3af-248">Start de testfailover Hallo door het uitvoeren van Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2c3af-248">Start hello test failover by running hello following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="2c3af-249">Een geplande failover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2c3af-249">Run a planned failover</span></span>
- <span data-ttu-id="2c3af-250">Start Hallo geplande failover door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="2c3af-250">Start hello planned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="2c3af-251">Een niet-geplande failover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2c3af-251">Run an unplanned failover</span></span>
- <span data-ttu-id="2c3af-252">Start niet-geplande failover door het uitvoeren van de volgende opdracht Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="2c3af-252">Start hello unplanned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <span data-ttu-id="2c3af-253"><a name=monitor></a>Voor Monitoractiviteit</span><span class="sxs-lookup"><span data-stu-id="2c3af-253"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="2c3af-254">Gebruik hello opdrachten toomonitor Hallo activiteit te volgen.</span><span class="sxs-lookup"><span data-stu-id="2c3af-254">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="2c3af-255">Houd er rekening mee dat u toowait Between-taken voor Hallo verwerking toofinish hebt.</span><span class="sxs-lookup"><span data-stu-id="2c3af-255">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="2c3af-256">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2c3af-256">Next steps</span></span>
<span data-ttu-id="2c3af-257">[Lees meer](/powershell/module/azurerm.recoveryservices.backup/#recovery) over Azure Site Recovery met Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="2c3af-257">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
