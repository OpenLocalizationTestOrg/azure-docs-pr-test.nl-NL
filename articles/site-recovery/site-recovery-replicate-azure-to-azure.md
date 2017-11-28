---
title: aaaReplicate toepassingen (Azure tooAzure) | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooset van de replicatie van de virtuele machines die wordt uitgevoerd in een Azure-regio te een andere regio in Azure.
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a><span data-ttu-id="e724c-103">Virtuele machines in Azure tooanother Azure-regio worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="e724c-103">Replicate Azure virtual machines tooanother Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="e724c-104">Site Recovery replicatie voor virtuele machines in Azure is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="e724c-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="e724c-105">Dit artikel wordt beschreven hoe tooset van de replicatie van de virtuele machines die wordt uitgevoerd in een Azure-regio tooanother Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="e724c-105">This article describes how tooset up replication of virtual machines running in one Azure region tooanother Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e724c-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e724c-106">Prerequisites</span></span>

* <span data-ttu-id="e724c-107">Hallo artikel wordt ervan uitgegaan dat u al over de Site Recovery en de Recovery Services-kluis weet.</span><span class="sxs-lookup"><span data-stu-id="e724c-107">hello article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="e724c-108">U moet toohave een 'Recovery services-kluis' vooraf gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e724c-108">You need toohave a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="e724c-109">Het verdient aanbeveling om in te maken Hallo 'Recovery services-kluis' hello locatie waar u uw virtuele machines tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="e724c-109">It is recommended that you create hello 'Recovery services vault' in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="e724c-110">Als uw doellocatie 'VS-midden', bijvoorbeeld kluis in 'VS-midden' maken.</span><span class="sxs-lookup"><span data-stu-id="e724c-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="e724c-111">Als u regels van de Netwerkbeveiligingsgroep groepen (NSG) of firewall proxy toocontrol toegang toooutbound internetverbinding op Hallo Azure Virtual machines gebruikt, zorg ervoor dat geaccepteerde u Hallo URL's of IP-adressen vereist.</span><span class="sxs-lookup"><span data-stu-id="e724c-111">If you are using Network Security Groups (NSG) rules or firewall proxy toocontrol access toooutbound internet connectivity on hello Azure VMs, ensure that you whitelist hello required URLs or IPs.</span></span> <span data-ttu-id="e724c-112">Raadpleeg te[leidraad voor netwerken](./site-recovery-azure-to-azure-networking-guidance.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e724c-112">Refer too[Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="e724c-113">Als u een ExpressRoute- of een VPN-verbinding tussen on-premises en Hallo bronlocatie in Azure, voert u de [overwegingen voor het herstel voor ExpressRoute Azure tooon-premises Site / VPN-configuratie](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span><span class="sxs-lookup"><span data-stu-id="e724c-113">If you have an ExpressRoute or a VPN connection between on-premises and hello source location in Azure, follow [Site Recovery Considerations for Azure tooon-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="e724c-114">Uw Azure gebruikersaccount moet toohave bepaalde [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicatie van een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="e724c-114">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="e724c-115">Uw Azure-abonnement moet worden ingeschakeld toocreate virtuele machines in de doellocatie Hallo gewenste toouse als DR regio.</span><span class="sxs-lookup"><span data-stu-id="e724c-115">Your Azure subscription should be enabled toocreate VMs in hello target location you want toouse as DR region.</span></span> <span data-ttu-id="e724c-116">Neem contact op met ondersteuning tooenable Hallo vereist quotum.</span><span class="sxs-lookup"><span data-stu-id="e724c-116">You can contact support tooenable hello required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="e724c-117">Schakel replicatie van Azure Site Recovery-kluis</span><span class="sxs-lookup"><span data-stu-id="e724c-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="e724c-118">In dit voorbeeld wordt er VM's worden uitgevoerd in toohello voor Azure-locatie in Hallo Oost-Azië, Zuidoost-Azië ' locatie gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="e724c-118">For this illustration, we will replicate VMs running  in hello ‘East Asia’ Azure location toohello ‘South East Asia’ location.</span></span> <span data-ttu-id="e724c-119">Hallo stappen zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="e724c-119">hello steps are as follows:</span></span>

 <span data-ttu-id="e724c-120">Klik op **+ repliceren** in Hallo kluis tooenable replicatie voor Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="e724c-120">Click **+Replicate** in hello vault tooenable replication for hello virtual machines.</span></span>

1. <span data-ttu-id="e724c-121">**Bron:** toohello punt van oorsprong Hallo machines die in dit geval verwijst **Azure**.</span><span class="sxs-lookup"><span data-stu-id="e724c-121">**Source:** It refers toohello point of origin of hello machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="e724c-122">**Bronlocatie:** is hello Azure-regio waar u tooprotect uw virtuele machines wilt.</span><span class="sxs-lookup"><span data-stu-id="e724c-122">**Source location:** It is hello Azure region from where you want tooprotect your virtual machines.</span></span> <span data-ttu-id="e724c-123">In dit voorbeeld worden Hallo bronlocatie Oost-Azië</span><span class="sxs-lookup"><span data-stu-id="e724c-123">For this illustration, hello source location will be 'East Asia'</span></span>

3. <span data-ttu-id="e724c-124">**Implementatiemodel:** toohello Azure implementatiemodel Hallo bron machines verwijst.</span><span class="sxs-lookup"><span data-stu-id="e724c-124">**Deployment model:** It refers toohello Azure deployment model of hello source machines.</span></span> <span data-ttu-id="e724c-125">U kunt ofwel classic selecteren of resourcemanager en de machines die horen toohello specifiek model voor beveiliging in de volgende stap hello wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e724c-125">You can select either classic or resource manager and machines belonging toohello specific model will be listed for protection in hello next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="e724c-126">U kunt alleen een klassieke virtuele machine repliceren en deze herstellen als een klassieke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e724c-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="e724c-127">U kunt deze niet herstellen als de virtuele machine van een Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e724c-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="e724c-128">**Resourcegroep:** de Hallo resource groep toowhich deel uitmaken van uw virtuele bronmachines.</span><span class="sxs-lookup"><span data-stu-id="e724c-128">**Resource Group:** It’s hello resource group toowhich your source virtual machines belong.</span></span> <span data-ttu-id="e724c-129">Alle Hallo VM's onder de geselecteerde resourcegroep hello wordt vermeld voor beveiliging in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="e724c-129">All hello VMs under hello selected resource group will be listed for protection in hello next step.</span></span>

    ![Replicatie inschakelen](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="e724c-131">In **virtuele Machines > Selecteer de virtuele machines**en klik op elke machine die u wilt dat tooreplicate selecteren.</span><span class="sxs-lookup"><span data-stu-id="e724c-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="e724c-132">U kunt alleen machines selecteren waarvoor replicatie kan worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e724c-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="e724c-133">Klik vervolgens op OK.</span><span class="sxs-lookup"><span data-stu-id="e724c-133">Then click OK.</span></span>
    <span data-ttu-id="e724c-134">![Replicatie inschakelen](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="e724c-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="e724c-135">Onder de sectie instellingen kunt u doel voor site-eigenschappen configureren</span><span class="sxs-lookup"><span data-stu-id="e724c-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="e724c-136">**Doellocatie:** dit is Hallo-locatie waar de brongegevens van de virtuele machine wordt gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="e724c-136">**Target Location:**  This is hello location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="e724c-137">Afhankelijk van uw locatie voor geselecteerde machines, biedt Site Recovery dat u een lijst met doelregio geschikte Hallo.</span><span class="sxs-lookup"><span data-stu-id="e724c-137">Depending upon your selected machines location, Site Recovery will provide you hello list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="e724c-138">Het verdient aanbeveling tookeep doellocatie dezelfde vanaf uw recovery services-kluis.</span><span class="sxs-lookup"><span data-stu-id="e724c-138">It is recommended tookeep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="e724c-139">**Doelresourcegroep:** is Hallo resource groep toowhich uw gerepliceerde virtuele machines deel van uitmaakt. Standaard maakt ASR een nieuwe resourcegroep in Hallo doelregio met naam 'asr' achtervoegsel heeft.</span><span class="sxs-lookup"><span data-stu-id="e724c-139">**Target resource group :** It is hello resource group toowhich all your replicated virtual machines will belong.By default ASR will create a new resource group in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="e724c-140">Als de resourcegroep die zijn gemaakt door ASR al bestaat, wordt opnieuw gebruikt. U kunt ook toocustomize deze zoals weergegeven in onderstaande Hallo-sectie.</span><span class="sxs-lookup"><span data-stu-id="e724c-140">In case resource group created by ASR already exist, it will be reused.You can also choose toocustomize it as shown in hello section below.</span></span>    
3. <span data-ttu-id="e724c-141">**Virtuele doelnetwerk:** standaard ASR maakt een nieuw virtueel netwerk in Hallo doelregio met naam 'asr' achtervoegsel heeft.</span><span class="sxs-lookup"><span data-stu-id="e724c-141">**Target Virtual Network:** By default, ASR will create a new virtual network in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="e724c-142">Dit is de toegewezen tooyour Bronnetwerk en wordt gebruikt voor alle toekomstige beveiliging.</span><span class="sxs-lookup"><span data-stu-id="e724c-142">This will be mapped tooyour source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e724c-143">[Controleer de gegevens van de netwerken](site-recovery-network-mapping-azure-to-azure.md) tooknow meer informatie over de netwerktoewijzing.</span><span class="sxs-lookup"><span data-stu-id="e724c-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) tooknow more about network mapping.</span></span>

4. <span data-ttu-id="e724c-144">**Storage-accounts als doel:** ASR maakt standaard Hallo nieuwe opslag doelaccount mimicking de opslagconfiguratie van de bron-VM.</span><span class="sxs-lookup"><span data-stu-id="e724c-144">**Target Storage accounts:** By default, ASR will create hello new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="e724c-145">Als storage-account gemaakt door ASR al bestaat, wordt opnieuw gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e724c-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="e724c-146">**Storage-accounts in de cache:** ASR moet extra opslagruimte account met de naam van cache-opslag in Hallo bron regio.</span><span class="sxs-lookup"><span data-stu-id="e724c-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in hello source region.</span></span> <span data-ttu-id="e724c-147">Alle Hallo wijzigingen die plaatsvinden op Hallo Bronmachines worden bijgehouden en toocache opslagaccount verzonden voordat de doellocatie toohello repliceren.</span><span class="sxs-lookup"><span data-stu-id="e724c-147">All hello changes happening on hello source VMs are tracked and sent toocache storage account before replicating those toohello target location.</span></span>

6. <span data-ttu-id="e724c-148">**Beschikbaarheidsset:** ASR maakt standaard een nieuwe beschikbaarheidsset Hallo doelregio met naam 'asr' achtervoegsel heeft.</span><span class="sxs-lookup"><span data-stu-id="e724c-148">**Availability set :** By default, ASR will create a new availability set in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="e724c-149">Als beschikbaarheidsset gemaakt door ASR al bestaat, wordt opnieuw gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e724c-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="e724c-150">**Beleid voor wachtwoordreplicatie:** het Hallo-instellingen voor herstelpunt bewaartermijn geschiedenis en app consistente momentopname upfrequentie definieert.</span><span class="sxs-lookup"><span data-stu-id="e724c-150">**Replication Policy:** It defines hello settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="e724c-151">Standaard maakt ASR een nieuw replicatiebeleid voor met de standaardinstellingen van 24 uur voor herstel bewaarperiode en "60 minuten voor de frequentie van app-consistente momentopname te maken.</span><span class="sxs-lookup"><span data-stu-id="e724c-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![Replicatie inschakelen](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="e724c-153">Doelresources aanpassen</span><span class="sxs-lookup"><span data-stu-id="e724c-153">Customize target resources</span></span>

<span data-ttu-id="e724c-154">Als u wilt dat toochange Hallo standaardwaarden door ASR gebruikt, kunt u het Hallo-instellingen op basis van uw behoeften kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e724c-154">In case you want toochange hello defaults used by ASR, you can change hello settings based on your needs.</span></span>

1. <span data-ttu-id="e724c-155">**Aanpassen:** klikt u op het toochange Hallo standaardwaarden worden gebruikt door ASR.</span><span class="sxs-lookup"><span data-stu-id="e724c-155">**Customize:** Click it toochange hello defaults used by ASR.</span></span>

2. <span data-ttu-id="e724c-156">**Doelresourcegroep:** kunt u de resourcegroep Hallo uit Hallo lijst met alle Hallo resourcegroepen in de doellocatie Hallo binnen Hallo abonnement bestaande.</span><span class="sxs-lookup"><span data-stu-id="e724c-156">**Target resource group :**  You can select hello resource group from hello list of all hello resource groups existing in hello target location within hello subscription.</span></span>

3. <span data-ttu-id="e724c-157">**Virtuele doelnetwerk:** vindt u Hallo-lijst van alle Hallo virtueel netwerk in Hallo target-locatie.</span><span class="sxs-lookup"><span data-stu-id="e724c-157">**Target Virtual Network:** You can find hello list of all hello virtual network in hello target location.</span></span>

4. <span data-ttu-id="e724c-158">**Beschikbaarheidsset:** kunt u alleen beschikbaarheid sets instellingen toohello van virtuele machines die deel van de beschikbaarheid in regio bron uitmaken toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e724c-158">**Availability set :** You can only add availability sets settings toohello virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="e724c-159">**Doel Storage-accounts:**</span><span class="sxs-lookup"><span data-stu-id="e724c-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="e724c-160">![Replicatie inschakelen](./media/site-recovery-replicate-azure-to-azure/customize.PNG) klikt u op **doelbron maken** en replicatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="e724c-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="e724c-161">Wanneer virtuele machines zijn beveiligd kunt u Hallo status van de status van de virtuele machines onder controleren **gerepliceerde items**</span><span class="sxs-lookup"><span data-stu-id="e724c-161">Once virtual machines are protected you can check hello status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="e724c-162">Tijdens het Hallo kan tijd van de initiële replicatie er een kans dat status tijd toorefresh duurt en dat er geen uitgevoerd gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="e724c-162">During hello time of initial replication there could a possibility that status takes time toorefresh and you don't see progress for some time.</span></span> <span data-ttu-id="e724c-163">U kunt klikken Hallo vernieuwen op Hallo Hallo blade tooget Hallo laatste status bovenaan.</span><span class="sxs-lookup"><span data-stu-id="e724c-163">You can click hello Refresh button on hello top of hello blade tooget hello latest status.</span></span>
>

![Replicatie inschakelen](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="e724c-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e724c-165">Next steps</span></span>
- <span data-ttu-id="e724c-166">[Meer informatie](site-recovery-test-failover-to-azure.md) over het uitvoeren van een testfailover.</span><span class="sxs-lookup"><span data-stu-id="e724c-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="e724c-167">[Meer informatie](site-recovery-failover.md) over verschillende soorten failovers, en hoe toorun ze.</span><span class="sxs-lookup"><span data-stu-id="e724c-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="e724c-168">Meer informatie over [met herstelplannen](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="e724c-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
- <span data-ttu-id="e724c-169">Meer informatie over [andere virtuele Azure-machines](site-recovery-how-to-reprotect.md) na een failover.</span><span class="sxs-lookup"><span data-stu-id="e724c-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>
