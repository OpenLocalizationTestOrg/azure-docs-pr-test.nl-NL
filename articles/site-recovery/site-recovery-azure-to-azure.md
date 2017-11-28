---
title: 'Virtuele Azure-machines repliceren tussen Azure-regio''s voor herstel na noodgevallen moet: Azure tooAzure | Microsoft Docs'
description: Geeft een overzicht van Hallo stappen u moet tooreplicate Azure VM's tussen Azure-regio's (Azure Azure) met hello Azure Site Recovery-service voor herstel nodig zijn na noodgevallen.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="8061f-103">Virtuele Azure-machines repliceren tussen regio's met Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="8061f-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="8061f-104">Azure Site Recovery-replicatie voor virtuele Azure-machines (VM's) is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="8061f-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="8061f-105">Dit artikel wordt beschreven hoe tooreplicate Azure VM's tussen Azure-regio's met behulp van Hallo [siteherstel](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8061f-105">This article describes how tooreplicate Azure VMs between Azure regions by using hello [Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="8061f-106">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="8061f-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="8061f-107">Herstel na noodgevallen in Azure</span><span class="sxs-lookup"><span data-stu-id="8061f-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="8061f-108">Ingebouwde Azure-infrastructuur functies en mogelijkheden die bijdragen tooa robuuste en robuuste beschikbaarheidsstrategie voor werkbelastingen die worden uitgevoerd op Azure Virtual machines.</span><span class="sxs-lookup"><span data-stu-id="8061f-108">Built-in Azure infrastructure capabilities and features contribute tooa robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="8061f-109">Er zijn echter diverse redenen waarom u nodig tooplan voor herstel na noodgevallen tussen Azure-regio's zelf hebt:</span><span class="sxs-lookup"><span data-stu-id="8061f-109">However, there are many reasons why you need tooplan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="8061f-110">U moet toomeet naleving richtlijnen voor specifieke toepassingen en werkbelastingen waarvoor een zakelijke continuïteit en noodherstelplan (BCDR).</span><span class="sxs-lookup"><span data-stu-id="8061f-110">You need toomeet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="8061f-111">U wilt Hallo mogelijkheid tooprotect en het herstellen van Azure VM's op basis van uw zakelijke beslissingen te nemen en niet alleen op basis van ingebouwde functionaliteit voor Azure.</span><span class="sxs-lookup"><span data-stu-id="8061f-111">You want hello ability tooprotect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="8061f-112">U moet tootest failovers en herstel in overeenstemming met uw behoeften bedrijven en naleving zonder impact op de productie.</span><span class="sxs-lookup"><span data-stu-id="8061f-112">You need tootest failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="8061f-113">U moet toofail via toohello herstel regio in geval van een noodgeval Hallo en de oorspronkelijke bron regio back toohello naadloos mislukken.</span><span class="sxs-lookup"><span data-stu-id="8061f-113">You need toofail over toohello recovery region in hello event of a disaster and fail back toohello original source region seamlessly.</span></span>

<span data-ttu-id="8061f-114">Site Recovery gebruiken voor de virtuele machine van Azure naar Azure replicatie toohelp bent u al deze taken.</span><span class="sxs-lookup"><span data-stu-id="8061f-114">Use Site Recovery for Azure-to-Azure VM replication toohelp you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="8061f-115">Waarom u Site Recovery moet gebruiken</span><span class="sxs-lookup"><span data-stu-id="8061f-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="8061f-116">Site Recovery biedt een eenvoudige manier tooreplicate Azure VM's tussen regio's:</span><span class="sxs-lookup"><span data-stu-id="8061f-116">Site Recovery provides a simple way tooreplicate Azure VMs between regions:</span></span>

- <span data-ttu-id="8061f-117">**Automatische implementatie**.</span><span class="sxs-lookup"><span data-stu-id="8061f-117">**Automatic deployment**.</span></span> <span data-ttu-id="8061f-118">In tegenstelling tot een actief / actief-replicatiemodel hoeft niet voor een dure en complexe infrastructuur in Hallo secundaire regio.</span><span class="sxs-lookup"><span data-stu-id="8061f-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in hello secondary region.</span></span> <span data-ttu-id="8061f-119">Wanneer u replicatie inschakelt, maakt Site Recovery automatisch Hallo vereist resources in Hallo doelregio, op basis van regio broninstellingen.</span><span class="sxs-lookup"><span data-stu-id="8061f-119">When you enable replication, Site Recovery automatically creates hello required resources in hello target region, based on source region settings.</span></span>
- <span data-ttu-id="8061f-120">**Regio's beheren**.</span><span class="sxs-lookup"><span data-stu-id="8061f-120">**Control regions**.</span></span> <span data-ttu-id="8061f-121">Met Site Recovery kunt u vanaf een willekeurige regio tooany regio binnen een continent repliceren.</span><span class="sxs-lookup"><span data-stu-id="8061f-121">With Site Recovery, you can replicate from any region tooany region within a continent.</span></span> <span data-ttu-id="8061f-122">Vergelijk deze met leestoegang geografisch redundante opslag, dat asynchroon tussen Standaard repliceert [regio's gekoppeld](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) alleen.</span><span class="sxs-lookup"><span data-stu-id="8061f-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="8061f-123">Geografisch redundante opslag met leestoegang biedt alleen-lezentoegang toohello gegevens in Hallo doelregio.</span><span class="sxs-lookup"><span data-stu-id="8061f-123">Read-access geo-redundant storage provides read-only access toohello data in hello target region.</span></span>
- <span data-ttu-id="8061f-124">**Automatische replicatie**.</span><span class="sxs-lookup"><span data-stu-id="8061f-124">**Automated replication**.</span></span> <span data-ttu-id="8061f-125">Site Recovery biedt geautomatiseerde continue replicatie.</span><span class="sxs-lookup"><span data-stu-id="8061f-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="8061f-126">Failover en failback kunnen worden geactiveerd met een enkele klik.</span><span class="sxs-lookup"><span data-stu-id="8061f-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="8061f-127">**RTO en RPO**.</span><span class="sxs-lookup"><span data-stu-id="8061f-127">**RTO and RPO**.</span></span> <span data-ttu-id="8061f-128">Site Recovery wordt gebruikgemaakt van hello Azure netwerkinfrastructuur die verbinding regio's tookeep maakt RTO en zeer lage RPO.</span><span class="sxs-lookup"><span data-stu-id="8061f-128">Site Recovery takes advantage of hello Azure network infrastructure that connects regions tookeep RTO and RPO very low.</span></span>
- <span data-ttu-id="8061f-129">**Testen van**.</span><span class="sxs-lookup"><span data-stu-id="8061f-129">**Testing**.</span></span> <span data-ttu-id="8061f-130">U kunt herstel na noodgevallen zoomt uitvoeren met op aanvraag testfailovers, wanneer nodig, zonder de productie-workloads of lopende replicatie te beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="8061f-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="8061f-131">**De herstelplannen**.</span><span class="sxs-lookup"><span data-stu-id="8061f-131">**Recovery plans**.</span></span> <span data-ttu-id="8061f-132">U kunt herstel plannen tooorchestrate failover en failback van de gehele toepassing hello uitgevoerd op meerdere virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8061f-132">You can use recovery plans tooorchestrate failover and failback of hello entire application running on multiple VMs.</span></span> <span data-ttu-id="8061f-133">Hallo-functie voor herstel plan heeft uitgebreide klas integratie met Azure automation-runbooks.</span><span class="sxs-lookup"><span data-stu-id="8061f-133">hello recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="8061f-134">Implementatieoverzicht</span><span class="sxs-lookup"><span data-stu-id="8061f-134">Deployment summary</span></span>

<span data-ttu-id="8061f-135">Hier volgt een samenvatting van wat u moet toodo tooset van de replicatie van virtuele machines tussen Azure-regio's:</span><span class="sxs-lookup"><span data-stu-id="8061f-135">Here's a summary of what you need toodo tooset up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="8061f-136">Maak een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="8061f-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="8061f-137">Hallo-kluis bevat configuratie-instellingen en stuurt replicatie.</span><span class="sxs-lookup"><span data-stu-id="8061f-137">hello vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="8061f-138">Replicatie inschakelen voor hello Azure VM's.</span><span class="sxs-lookup"><span data-stu-id="8061f-138">Enable replication for hello Azure VMs.</span></span>
3. <span data-ttu-id="8061f-139">Een test failover-toomake of alles werkt zoals verwacht worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8061f-139">Run a test failover toomake sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="8061f-140">U kunt controleren Hallo [ondersteuningsmatrix voor replicatie van de virtuele machine van Azure](./site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="8061f-140">You can check hello [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="8061f-141">Zie voor informatie over hoe tooconfigure Hallo uitgaande netwerkverbinding voor Azure Virtual Machines voor replicatie van Site Recovery vereist Hallo [leidraad voor netwerken](./site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="8061f-141">For information on how tooconfigure hello required network outbound connectivity for Azure VMs for Site Recovery replication, see hello [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="8061f-142">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="8061f-142">Before you start</span></span>

* <span data-ttu-id="8061f-143">Uw Azure gebruikersaccount moet toohave bepaalde [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicatie van een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="8061f-143">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="8061f-144">Uw Azure-abonnement moet zijn ingeschakeld toocreate virtuele machines in Hallo target-locatie die u toouse als Hallo disaster recovery regio wilt.</span><span class="sxs-lookup"><span data-stu-id="8061f-144">Your Azure subscription should be enabled toocreate VMs in hello target location that you want toouse as hello disaster recovery region.</span></span> <span data-ttu-id="8061f-145">Neem contact op met ondersteuning tooenable Hallo vereist quota.</span><span class="sxs-lookup"><span data-stu-id="8061f-145">Contact support tooenable hello required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="8061f-146">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="8061f-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="8061f-147">U wordt aangeraden dat u Hallo Recovery Services-kluis maken in Hallo-locatie waar u uw virtuele machines tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="8061f-147">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="8061f-148">Bijvoorbeeld, als uw target-locatie wordt centraal ons hello, Hallo kluis in maken **VS-midden**.</span><span class="sxs-lookup"><span data-stu-id="8061f-148">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="8061f-149">Replicatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="8061f-149">Enable replication</span></span>

<span data-ttu-id="8061f-150">In **Recovery Services-kluizen**, klikt u op de kluisnaam Hallo.</span><span class="sxs-lookup"><span data-stu-id="8061f-150">In **Recovery Services vaults**, click hello vault name.</span></span> <span data-ttu-id="8061f-151">Klik in het Hallo-kluis op Hallo **+ repliceren** knop.</span><span class="sxs-lookup"><span data-stu-id="8061f-151">In hello vault, click hello **+Replicate** button.</span></span>

### <a name="step-1-configure-hello-source"></a><span data-ttu-id="8061f-152">Step 1.</span><span class="sxs-lookup"><span data-stu-id="8061f-152">Step 1.</span></span> <span data-ttu-id="8061f-153">Hallo bron configureren</span><span class="sxs-lookup"><span data-stu-id="8061f-153">Configure hello source</span></span>
1. <span data-ttu-id="8061f-154">In **bron**, selecteer **Azure - PREVIEW**.</span><span class="sxs-lookup"><span data-stu-id="8061f-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="8061f-155">In **bronlocatie**, selecteer Hallo bron Azure-regio waarin uw virtuele machines worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8061f-155">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="8061f-156">Selecteer Hallo implementatiemodel van uw virtuele machines: **Resource Manager** of **klassieke**.</span><span class="sxs-lookup"><span data-stu-id="8061f-156">Select hello deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="8061f-157">Selecteer Hallo **resourcegroep** voor Resource Manager virtuele machines of **cloudservice** voor klassieke virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8061f-157">Select hello **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![Hallo bron configureren](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="8061f-159">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="8061f-159">Step 2.</span></span> <span data-ttu-id="8061f-160">Selecteer de virtuele machines</span><span class="sxs-lookup"><span data-stu-id="8061f-160">Select virtual machines</span></span>

* <span data-ttu-id="8061f-161">Selecteer Hallo VMs u tooreplicate wilt en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8061f-161">Select hello VMs you want tooreplicate, and then click **OK**.</span></span>

    ![Selecteer de virtuele machines](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="8061f-163">Stap 3.</span><span class="sxs-lookup"><span data-stu-id="8061f-163">Step 3.</span></span> <span data-ttu-id="8061f-164">Instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="8061f-164">Configure settings</span></span>

1. <span data-ttu-id="8061f-165">toooverride hello standaard instellingen als doel en geef instellingen op Hallo van uw keuze, klikt u op **aanpassen**.</span><span class="sxs-lookup"><span data-stu-id="8061f-165">toooverride hello default target settings and specify hello settings of your choice, click **Customize**.</span></span> <span data-ttu-id="8061f-166">Zie voor meer informatie [doelresources aanpassen](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span><span class="sxs-lookup"><span data-stu-id="8061f-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![Instellingen configureren](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="8061f-168">Standaard maakt Site Recovery een replicatiebeleid die ervoor zorgt dat toepassingsconsistente momentopnamen elke 4 uur handhaaft herstelpunten gedurende 24 uur.</span><span class="sxs-lookup"><span data-stu-id="8061f-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="8061f-169">toocreate beleid met verschillende instellingen, klikt u op **aanpassen** volgende te**replicatiebeleid**.</span><span class="sxs-lookup"><span data-stu-id="8061f-169">toocreate a policy with different settings, click **Customize** next too**Replication Policy**.</span></span>

    ![Beleid aanpassen](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="8061f-171">toostart inrichting Hallo doelresources, klikt u op **doelresources maken**.</span><span class="sxs-lookup"><span data-stu-id="8061f-171">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="8061f-172">Inrichting duurt een minuut.</span><span class="sxs-lookup"><span data-stu-id="8061f-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="8061f-173">Sluit de blade Hallo niet tijdens het inrichten of u toostart dan nodig.</span><span class="sxs-lookup"><span data-stu-id="8061f-173">Don't close hello blade during provisioning, or you need toostart over.</span></span>

4. <span data-ttu-id="8061f-174">replicatie tootrigger Hallo VM geselecteerd, klikt u op **replicatie inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="8061f-174">tootrigger replication of hello selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="8061f-175">U kunt de voortgang van Hallo volgen **beveiliging inschakelen** taak **instellingen** > **taken** > **Site Recovery-taken**.</span><span class="sxs-lookup"><span data-stu-id="8061f-175">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="8061f-176">In **instellingen** > **gerepliceerde Items**, kunt u weergeven Hallo status van virtuele machines en Hallo initiële replicatie uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8061f-176">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="8061f-177">Klik op Hallo VM toodrill omlaag in de instellingen ervan.</span><span class="sxs-lookup"><span data-stu-id="8061f-177">Click hello VM toodrill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="8061f-178">Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8061f-178">Run a test failover</span></span>

<span data-ttu-id="8061f-179">Nadat u alles instellen, voert u een test failover toomake, controleren of dat alles werkt zoals verwacht:</span><span class="sxs-lookup"><span data-stu-id="8061f-179">After you set up everything, run a test failover toomake sure everything's working as expected:</span></span>

1. <span data-ttu-id="8061f-180">toofail via één computer in **instellingen** > **gerepliceerde Items**, klikt u op Hallo VM **+ Testfailover** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8061f-180">toofail over a single machine, in **Settings** > **Replicated Items**, click hello VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="8061f-181">plan toofail via een herstelbewerking **instellingen** > **herstelplannen**, klik met de rechtermuisknop Hallo plan **Testfailover**.</span><span class="sxs-lookup"><span data-stu-id="8061f-181">toofail over a recovery plan, in **Settings** > **Recovery Plans**, right-click hello plan **Test Failover**.</span></span> <span data-ttu-id="8061f-182">een herstelplan toocreate [Volg deze instructies](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="8061f-182">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="8061f-183">In **Testfailover**, selecteer Hallo doel virtuele Azure-netwerk toowhich virtuele Azure-machines worden verbonden nadat er een Hallo failover plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="8061f-183">In **Test Failover**, select hello target Azure virtual network toowhich Azure VMs are connected after hello failover occurs.</span></span>

4. <span data-ttu-id="8061f-184">toostart Hallo failover, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8061f-184">toostart hello failover, click **OK**.</span></span> <span data-ttu-id="8061f-185">tootrack voortgang, klikt u op Hallo VM tooopen eigenschappen ervan.</span><span class="sxs-lookup"><span data-stu-id="8061f-185">tootrack progress, click hello VM tooopen its properties.</span></span> <span data-ttu-id="8061f-186">U kunt ook op Hallo **Testfailover** taak in de kluisnaam Hallo > **instellingen** > **taken** > **Site Recovery-taken**.</span><span class="sxs-lookup"><span data-stu-id="8061f-186">Or you can click hello **Test Failover** job in hello vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="8061f-187">Na het Hallo failover is voltooid, Hallo replica machine van Azure in hello Azure-portal weergegeven > **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="8061f-187">After hello failover finishes, hello replica Azure machine appears in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="8061f-188">Zorg ervoor dat Hallo VM is de juiste grootte hello, of deze is verbonden met het juiste netwerk toohello en dat deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8061f-188">Make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="8061f-189">toodelete hello virtuele machines die zijn gemaakt tijdens de testfailover hello, klikt u op **testfailover opschonen** op Hallo gerepliceerd item of Hallo herstelplan.</span><span class="sxs-lookup"><span data-stu-id="8061f-189">toodelete hello VMs that were created during hello test failover, click **Cleanup test failover** on hello replicated item or hello recovery plan.</span></span> <span data-ttu-id="8061f-190">In **notities**, vastleggen en opslaan van eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo.</span><span class="sxs-lookup"><span data-stu-id="8061f-190">In **Notes**, record and save any observations associated with hello test failover.</span></span> 

<span data-ttu-id="8061f-191">[Meer informatie](site-recovery-test-failover-to-azure.md) over testfailovers.</span><span class="sxs-lookup"><span data-stu-id="8061f-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8061f-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8061f-192">Next steps</span></span>

<span data-ttu-id="8061f-193">Na het Hallo-implementatie te testen:</span><span class="sxs-lookup"><span data-stu-id="8061f-193">After you test hello deployment:</span></span>

- <span data-ttu-id="8061f-194">[Meer informatie](site-recovery-failover.md) over verschillende soorten failovers en hoe toorun ze.</span><span class="sxs-lookup"><span data-stu-id="8061f-194">[Learn more](site-recovery-failover.md) about different types of failovers and how toorun them.</span></span>
- <span data-ttu-id="8061f-195">Meer informatie over [met herstelplannen](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="8061f-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
