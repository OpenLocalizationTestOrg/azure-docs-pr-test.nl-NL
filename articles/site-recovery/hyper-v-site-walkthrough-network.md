---
title: netwerk voor Hyper-V (zonder de System Center VMM) tooAzure replicatie met Azure Site Recovery aaaPlan | Microsoft Docs
description: Dit artikel wordt beschreven netwerkplanning vereist wanneer tooAzure Hyper-V-machines (zonder VMM) repliceren
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5ca12254-975d-48e8-a84d-422825dac9b2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: a35de72b53ca921a7b9bfca00a0edcb9416d5aa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-hyper-v-tooazure-replication"></a><span data-ttu-id="cc15f-103">Stap 4: De netwerken voor Hyper-V tooAzure replicatie plannen</span><span class="sxs-lookup"><span data-stu-id="cc15f-103">Step 4: Plan networking for Hyper-V tooAzure replication</span></span>

<span data-ttu-id="cc15f-104">In dit artikel bevat een overzicht van netwerk planningsoverwegingen bij het repliceren van lokale Hyper-V-machines (zonder de System Center VMM) tooAzure met Hallo [Azure Site Recovery](site-recovery-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="cc15f-104">This article summarizes network planning considerations when replicating on-premises Hyper-V VMs (without System Center VMM) tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="cc15f-105">Eventuele opmerkingen onder Hallo van dit artikel plaatsen of vragen in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="cc15f-105">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="connecting-tooreplica-vms-after-failover"></a><span data-ttu-id="cc15f-106">Verbinding maken met virtuele machines tooreplica na een failover</span><span class="sxs-lookup"><span data-stu-id="cc15f-106">Connecting tooreplica VMs after failover</span></span>

<span data-ttu-id="cc15f-107">Bij het plannen van uw replicatie en failoverstrategie is een belangrijke vragen Hallo hoe tooconnect toohello virtuele Azure-machine na een failover.</span><span class="sxs-lookup"><span data-stu-id="cc15f-107">When planning your replication and failover strategy, one of hello key questions is how tooconnect toohello Azure VM after failover.</span></span> <span data-ttu-id="cc15f-108">Er zijn een aantal opties bij het ontwerpen van uw netwerk-strategie voor de replica virtuele Azure-machines:</span><span class="sxs-lookup"><span data-stu-id="cc15f-108">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="cc15f-109">**Ander IP-adres**: U kunt toouse een ander IP-adresbereik voor selecteren Hallo gerepliceerd Azure VM-netwerk.</span><span class="sxs-lookup"><span data-stu-id="cc15f-109">**Different IP address**: You can select toouse a different IP address range for hello replicated Azure VM network.</span></span> <span data-ttu-id="cc15f-110">In dit scenario Hallo VM krijgt een nieuwe IP-adres na een failover en een DNS-update is vereist.</span><span class="sxs-lookup"><span data-stu-id="cc15f-110">In this scenario hello VM gets a new IP address after failover, and a DNS update is required.</span></span> [<span data-ttu-id="cc15f-111">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="cc15f-111">Learn more</span></span>](site-recovery-test-failover-vmm-to-vmm.md#prepare-the-infrastructure-for-test-failover)
- <span data-ttu-id="cc15f-112">**Hetzelfde IP-adres**: U kunt toouse Hallo hetzelfde IP-adresbereik als die op uw primaire on-premises netwerk, voor hello Azure-netwerk na een failover.</span><span class="sxs-lookup"><span data-stu-id="cc15f-112">**Same IP address**: You might want toouse hello same IP address range as that in your primary on-premises network, for hello Azure network after failover.</span></span>  <span data-ttu-id="cc15f-113">Houden Hallo dezelfde IP-adressen vereenvoudigt Hallo recovery vermindert toegangsproblemen netwerk na een failover.</span><span class="sxs-lookup"><span data-stu-id="cc15f-113">Keeping hello same IP addresses simplifies hello recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="cc15f-114">Echter, wanneer u tooAzure repliceert, moet u tooupdate routes met de nieuwe locatie Hallo Hallo IP-adressen na een failover.</span><span class="sxs-lookup"><span data-stu-id="cc15f-114">However, when you're replicating tooAzure, you will need tooupdate routes with hello new location of hello IP addresses after failover.</span></span>


## <a name="retain-ip-addresses"></a><span data-ttu-id="cc15f-115">IP-adressen behouden</span><span class="sxs-lookup"><span data-stu-id="cc15f-115">Retain IP addresses</span></span>

<span data-ttu-id="cc15f-116">Site Recovery biedt Hallo mogelijkheid tooretain vaste IP-adressen wanneer failover tooAzure met de failover van een subnet.</span><span class="sxs-lookup"><span data-stu-id="cc15f-116">Site Recovery provides hello capability tooretain fixed IP addresses when failing over tooAzure, with a subnet failover.</span></span>

<span data-ttu-id="cc15f-117">Met subnet-failover is een specifiek subnet aanwezig op de Site 1 of 2, maar niet op beide sites tegelijkertijd.</span><span class="sxs-lookup"><span data-stu-id="cc15f-117">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="cc15f-118">In volgorde toomaintain Hallo IP-adresruimte in Hallo gebeurtenis van een failover rangschikt u programmatisch voor Hallo router infrastructuur toomove Hallo subnetten van één site tooanother.</span><span class="sxs-lookup"><span data-stu-id="cc15f-118">In order toomaintain hello IP address space in hello event of a failover, you programmatically arrange for hello router infrastructure toomove hello subnets from one site tooanother.</span></span> <span data-ttu-id="cc15f-119">Tijdens de failover gekoppelde Hallo subnetten verplaatsen Hello beveiligde virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="cc15f-119">During failover, hello subnets move with hello associated protected VMs.</span></span> <span data-ttu-id="cc15f-120">het grootste nadeel Hallo is dat in geval van storing Hallo u toomove Hallo hele subnet.</span><span class="sxs-lookup"><span data-stu-id="cc15f-120">hello main drawback is that in hello event of a failure, you have toomove hello whole subnet.</span></span>


### <a name="failover-example"></a><span data-ttu-id="cc15f-121">Failover-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="cc15f-121">Failover example</span></span>

<span data-ttu-id="cc15f-122">Bekijk een voorbeeld van failover-tooAzure.</span><span class="sxs-lookup"><span data-stu-id="cc15f-122">Let's look at an example for failover tooAzure.</span></span>

- <span data-ttu-id="cc15f-123">Een ficticious bedrijf Woodgrove Bank, heeft een on-premises infrastructuur die als host fungeert voor de business-apps.</span><span class="sxs-lookup"><span data-stu-id="cc15f-123">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="cc15f-124">Hun mobiele toepassingen worden gehost op Azure.</span><span class="sxs-lookup"><span data-stu-id="cc15f-124">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="cc15f-125">Connectiviteit tussen de Woodgrove Bank virtuele machines in Azure en on-premises servers wordt verstrekt door een site-naar-site (VPN)-verbinding tussen Hallo on-premises rand netwerk en Hallo virtuele Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="cc15f-125">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between hello on-premises edge network and hello Azure virtual network.</span></span>
- <span data-ttu-id="cc15f-126">Dit VPN-betekent dat het virtuele netwerk van bedrijf in Azure Hallo wordt weergegeven als een uitbreiding van hun on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="cc15f-126">This VPN means that hello company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="cc15f-127">Woodgrove wil toouse siteherstel tooreplicate lokale werkbelastingen tooAzure.</span><span class="sxs-lookup"><span data-stu-id="cc15f-127">Woodgrove wants toouse Site Recovery tooreplicate on-premises workloads tooAzure.</span></span>
 - <span data-ttu-id="cc15f-128">Woodgrove heeft toodeal met toepassingen en configuraties die afhankelijk zijn van vastgelegde IP-adressen en dus tooretain IP-adressen voor hun toepassingen na failover tooAzure nodig.</span><span class="sxs-lookup"><span data-stu-id="cc15f-128">Woodgrove has toodeal with applications and configurations which depend on hard-coded IP addresses, and thus need tooretain IP addresses for their applications after failover tooAzure.</span></span>
 - <span data-ttu-id="cc15f-129">Woodgrove heeft IP-adressen worden toegewezen uit het bereik 172.16.1.0/24, 172.16.2.0/24 tooits resources in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cc15f-129">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 tooits resources running in Azure.</span></span>


<span data-ttu-id="cc15f-130">Woodgrove toobe kunnen tooreplicate de tooAzure VMs terwijl behouden Hallo IP-adressen, is dit wat Hallo bedrijf behoefte heeft aan toodo:</span><span class="sxs-lookup"><span data-stu-id="cc15f-130">For Woodgrove toobe able tooreplicate its VMs tooAzure while retaining hello IP addresses, here's what hello company needs toodo:</span></span>

1. <span data-ttu-id="cc15f-131">Maak een Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="cc15f-131">Create an Azure virtual network.</span></span> <span data-ttu-id="cc15f-132">Deze moet een extensie van Hallo lokale netwerk, zodat toepassingen naadloos kunnen failover.</span><span class="sxs-lookup"><span data-stu-id="cc15f-132">It should be an extension of hello on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="cc15f-133">Azure kunt u tooadd site-naar-site VPN-verbindingen naast toopoint-naar-site-connectiviteit toohello virtuele netwerken in Azure gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cc15f-133">Azure allows you tooadd site-to-site VPN connectivity, in addition toopoint-to-site connectivity toohello virtual networks created in Azure.</span></span>
3. <span data-ttu-id="cc15f-134">Wanneer u site-naar-site-verbinding Hallo instelt, in hello Azure-netwerk, kunt u verkeer toohello on-premises locatie (LAN) routeren alleen als Hallo IP-adresbereik verschilt van Hallo lokale IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="cc15f-134">When setting up hello site-to-site connection, in hello Azure network, you can route traffic toohello on-premises location (local-network) only if hello IP address range is different from hello on-premises IP address range.</span></span>
    - <span data-ttu-id="cc15f-135">Dit is omdat Azure biedt geen ondersteuning voor gespreide subnetten.</span><span class="sxs-lookup"><span data-stu-id="cc15f-135">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="cc15f-136">Als u beschikt over subnet 192.168.1.0/24 on-premises, kan u dus een lokaal netwerk 192.168.1.0/24 toevoegen aan hello Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="cc15f-136">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in hello Azure network.</span></span>
    - <span data-ttu-id="cc15f-137">Dit is normaal omdat Azure niet weet dat er geen actieve VM's in Hallo subnet zijn en dat Hallo-subnet wordt gemaakt voor alleen herstel na noodgevallen.</span><span class="sxs-lookup"><span data-stu-id="cc15f-137">This is expected because Azure doesn’t know that there are no active VMs in hello subnet, and that hello subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="cc15f-138">toobe kunnen toocorrectly netwerkverkeer buiten een Azure-netwerk Hallo subnetten in Hallo netwerk- en LAN Hallo mag niet in conflict.</span><span class="sxs-lookup"><span data-stu-id="cc15f-138">toobe able toocorrectly route network traffic out of an Azure network hello subnets in hello network and hello local-network mustn't conflict.</span></span>

![Vóór de subnet-failover](./media/hyper-v-site-walkthrough-network/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="cc15f-140">Vóór de failover</span><span class="sxs-lookup"><span data-stu-id="cc15f-140">Before failover</span></span>

1. <span data-ttu-id="cc15f-141">Maak een extra netwerk (bijvoorbeeld herstel netwerk).</span><span class="sxs-lookup"><span data-stu-id="cc15f-141">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="cc15f-142">Dit is Hallo-netwerk op die failover van virtuele machines worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cc15f-142">This is hello network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="cc15f-143">tooensure die hello IP-adres voor een virtuele machine wordt bewaard na een failover, in de eigenschappen van de VM Hallo > **configureren**, geef dezelfde IP-adres dat Hallo VM een on-premises en klikt u op Hallo **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="cc15f-143">tooensure that hello IP address for a VM is retained after a failover, in hello VM properties > **Configure**, specify hello same IP address that hello VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="cc15f-144">Wanneer Hallo VM failover wordt uitgevoerd, wordt de Azure Site Recovery Hallo opgegeven IP-adres tooit toewijzen.</span><span class="sxs-lookup"><span data-stu-id="cc15f-144">When hello VM is failed over, Azure Site Recovery will assign hello provided IP address tooit.</span></span>

    ![Eigenschappen van het netwerk](./media/hyper-v-site-walkthrough-network/network-design8.png)

4. <span data-ttu-id="cc15f-146">Nadat de failover is de trigger wordt geactiveerd en Hallo VM's zijn gemaakt in Azure met Hallo vereist IP-adres, u kunt verbinden toohello netwerk via een [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="cc15f-146">After failover is trigger is triggered, and hello VMs are created in Azure with hello required IP address, you can connect toohello network using a [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="cc15f-147">Deze actie kan scripts worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cc15f-147">This action can be scripted.</span></span>
5. <span data-ttu-id="cc15f-148">Routes moeten op de juiste wijze zijn gewijzigd, toobe tooreflect die 192.168.1.0/24 is nu tooAzure verplaatst.</span><span class="sxs-lookup"><span data-stu-id="cc15f-148">Routes need toobe appropriately modified, tooreflect that 192.168.1.0/24 has now moved tooAzure.</span></span>

    ![Na een failover van subnet](./media/hyper-v-site-walkthrough-network/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="cc15f-150">Na een failover</span><span class="sxs-lookup"><span data-stu-id="cc15f-150">After failover</span></span>

<span data-ttu-id="cc15f-151">Als u niet een Azure-netwerk hebt, zoals wordt geïllustreerd hierboven, kunt u een site-naar-site VPN-verbinding tussen de primaire site en Azure na failvoer maken.</span><span class="sxs-lookup"><span data-stu-id="cc15f-151">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failvoer.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="cc15f-152">IP-adressen wijzigen</span><span class="sxs-lookup"><span data-stu-id="cc15f-152">Change IP addresses</span></span>

<span data-ttu-id="cc15f-153">Dit [blogbericht](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) wordt uitgelegd hoe tooset up hello Azure netwerkinfrastructuur wanneer u niet tooretain IP hoeft-adressen na een failover.</span><span class="sxs-lookup"><span data-stu-id="cc15f-153">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how tooset up hello Azure networking infrastructure when you don't need tooretain IP addresses after failover.</span></span> <span data-ttu-id="cc15f-154">Deze begint met een toepassingsbeschrijving, lijkt op hoe tooset netwerkinstellingen lokaal en in Azure en wordt afgesloten met informatie over het uitvoeren van failovers.</span><span class="sxs-lookup"><span data-stu-id="cc15f-154">It starts with an application description, looks at how tooset up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="cc15f-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cc15f-155">Next steps</span></span>

<span data-ttu-id="cc15f-156">Ga te[stap 5: Azure voorbereiden](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="cc15f-156">Go too[Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>
