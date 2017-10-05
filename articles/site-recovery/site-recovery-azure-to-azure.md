---
title: 'Virtuele Azure-machines repliceren tussen Azure-regio''s voor herstel na noodgevallen moet: Azure naar Azure | Microsoft Docs'
description: Geeft een overzicht van de stappen die u moet virtuele Azure-machines repliceren tussen Azure-regio's (Azure Azure) met de Azure Site Recovery-service voor herstel nodig zijn na noodgevallen.
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
ms.openlocfilehash: 9ca33057f6030fdcc233f6053fdc392d62f8f9f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="8b17f-103">Virtuele Azure-machines repliceren tussen regio's met Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="8b17f-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="8b17f-104">Azure Site Recovery-replicatie voor virtuele Azure-machines (VM's) is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="8b17f-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="8b17f-105">In dit artikel wordt beschreven hoe virtuele Azure-machines repliceren tussen Azure-regio's met behulp van de [siteherstel](site-recovery-overview.md) service in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8b17f-105">This article describes how to replicate Azure VMs between Azure regions by using the [Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="8b17f-106">Opmerkingen en vragen boeken aan de onderkant van dit artikel of op de [Azure Recovery Services-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="8b17f-106">Post comments and questions at the bottom of this article or on the [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="8b17f-107">Herstel na noodgevallen in Azure</span><span class="sxs-lookup"><span data-stu-id="8b17f-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="8b17f-108">Ingebouwde Azure-infrastructuur functies en mogelijkheden die bijdragen aan een robuuste en robuuste beschikbaarheidsstrategie voor de werkbelastingen die worden uitgevoerd op Azure Virtual machines.</span><span class="sxs-lookup"><span data-stu-id="8b17f-108">Built-in Azure infrastructure capabilities and features contribute to a robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="8b17f-109">Er zijn echter diverse redenen waarom u nodig hebt om te plannen voor herstel na noodgevallen tussen Azure-regio's zelf:</span><span class="sxs-lookup"><span data-stu-id="8b17f-109">However, there are many reasons why you need to plan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="8b17f-110">U moet voldoen aan de richtlijnen van naleving voor specifieke toepassingen en werkbelastingen waarvoor een zakelijke continuïteit en noodherstelplan (BCDR).</span><span class="sxs-lookup"><span data-stu-id="8b17f-110">You need to meet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="8b17f-111">U wilt dat de mogelijkheid om te beveiligen en herstellen van Azure VM's op basis van uw zakelijke beslissingen te nemen en niet alleen op basis van ingebouwde functionaliteit voor Azure.</span><span class="sxs-lookup"><span data-stu-id="8b17f-111">You want the ability to protect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="8b17f-112">U moet testen failovers en herstel in overeenstemming met uw behoeften bedrijven en naleving zonder impact op de productie.</span><span class="sxs-lookup"><span data-stu-id="8b17f-112">You need to test failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="8b17f-113">U moet voor de regio herstel in geval van een noodgeval failover en failback naar de oorspronkelijke bron regio naadloos.</span><span class="sxs-lookup"><span data-stu-id="8b17f-113">You need to fail over to the recovery region in the event of a disaster and fail back to the original source region seamlessly.</span></span>

<span data-ttu-id="8b17f-114">Met Site Recovery voor replicatie van de virtuele machine van Azure naar Azure kunt u deze taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8b17f-114">Use Site Recovery for Azure-to-Azure VM replication to help you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="8b17f-115">Waarom u Site Recovery moet gebruiken</span><span class="sxs-lookup"><span data-stu-id="8b17f-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="8b17f-116">Site Recovery biedt een eenvoudige manier om virtuele Azure-machines repliceren tussen regio's:</span><span class="sxs-lookup"><span data-stu-id="8b17f-116">Site Recovery provides a simple way to replicate Azure VMs between regions:</span></span>

- <span data-ttu-id="8b17f-117">**Automatische implementatie**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-117">**Automatic deployment**.</span></span> <span data-ttu-id="8b17f-118">In tegenstelling tot een actief / actief-replicatiemodel hoeft niet voor een dure en complexe infrastructuur in de secundaire regio.</span><span class="sxs-lookup"><span data-stu-id="8b17f-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in the secondary region.</span></span> <span data-ttu-id="8b17f-119">Wanneer u replicatie inschakelt, maakt Site Recovery automatisch de vereiste resources in de doelregio, op basis van regio broninstellingen.</span><span class="sxs-lookup"><span data-stu-id="8b17f-119">When you enable replication, Site Recovery automatically creates the required resources in the target region, based on source region settings.</span></span>
- <span data-ttu-id="8b17f-120">**Regio's beheren**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-120">**Control regions**.</span></span> <span data-ttu-id="8b17f-121">Met Site Recovery kunt u vanaf een willekeurige regio repliceren naar een willekeurige regio binnen een continent.</span><span class="sxs-lookup"><span data-stu-id="8b17f-121">With Site Recovery, you can replicate from any region to any region within a continent.</span></span> <span data-ttu-id="8b17f-122">Vergelijk deze met leestoegang geografisch redundante opslag, dat asynchroon tussen Standaard repliceert [regio's gekoppeld](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) alleen.</span><span class="sxs-lookup"><span data-stu-id="8b17f-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="8b17f-123">Geografisch redundante opslag met leestoegang biedt alleen-lezen toegang tot de gegevens in de doelregio.</span><span class="sxs-lookup"><span data-stu-id="8b17f-123">Read-access geo-redundant storage provides read-only access to the data in the target region.</span></span>
- <span data-ttu-id="8b17f-124">**Automatische replicatie**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-124">**Automated replication**.</span></span> <span data-ttu-id="8b17f-125">Site Recovery biedt geautomatiseerde continue replicatie.</span><span class="sxs-lookup"><span data-stu-id="8b17f-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="8b17f-126">Failover en failback kunnen worden geactiveerd met een enkele klik.</span><span class="sxs-lookup"><span data-stu-id="8b17f-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="8b17f-127">**RTO en RPO**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-127">**RTO and RPO**.</span></span> <span data-ttu-id="8b17f-128">Site Recovery wordt gebruikgemaakt van de Azure-netwerk-infrastructuur die verbinding maakt gebieden om te zorgen dat RTO en RPO zeer lage.</span><span class="sxs-lookup"><span data-stu-id="8b17f-128">Site Recovery takes advantage of the Azure network infrastructure that connects regions to keep RTO and RPO very low.</span></span>
- <span data-ttu-id="8b17f-129">**Testen van**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-129">**Testing**.</span></span> <span data-ttu-id="8b17f-130">U kunt herstel na noodgevallen zoomt uitvoeren met op aanvraag testfailovers, wanneer nodig, zonder de productie-workloads of lopende replicatie te beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="8b17f-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="8b17f-131">**De herstelplannen**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-131">**Recovery plans**.</span></span> <span data-ttu-id="8b17f-132">U kunt herstelplannen indelen failover en failback van de gehele toepassing uitgevoerd op meerdere virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8b17f-132">You can use recovery plans to orchestrate failover and failback of the entire application running on multiple VMs.</span></span> <span data-ttu-id="8b17f-133">De functie herstel plan heeft uitgebreide klas integratie met Azure automation-runbooks.</span><span class="sxs-lookup"><span data-stu-id="8b17f-133">The recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="8b17f-134">Implementatieoverzicht</span><span class="sxs-lookup"><span data-stu-id="8b17f-134">Deployment summary</span></span>

<span data-ttu-id="8b17f-135">Hier volgt een samenvatting van wat u moet doen voor het instellen van de replicatie van virtuele machines tussen Azure-regio's:</span><span class="sxs-lookup"><span data-stu-id="8b17f-135">Here's a summary of what you need to do to set up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="8b17f-136">Maak een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="8b17f-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="8b17f-137">De kluis bevat configuratie-instellingen en stuurt replicatie.</span><span class="sxs-lookup"><span data-stu-id="8b17f-137">The vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="8b17f-138">Replicatie inschakelen voor de Azure VM's.</span><span class="sxs-lookup"><span data-stu-id="8b17f-138">Enable replication for the Azure VMs.</span></span>
3. <span data-ttu-id="8b17f-139">Een testfailover om ervoor te zorgen dat alles werkt zoals verwacht worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8b17f-139">Run a test failover to make sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="8b17f-140">U kunt controleren de [ondersteuningsmatrix voor replicatie van de virtuele machine van Azure](./site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="8b17f-140">You can check the [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="8b17f-141">Zie voor meer informatie over het configureren van de vereiste uitgaande netwerkverbinding voor Azure virtuele machines voor replicatie van Site Recovery de [leidraad voor netwerken](./site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="8b17f-141">For information on how to configure the required network outbound connectivity for Azure VMs for Site Recovery replication, see the [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="8b17f-142">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="8b17f-142">Before you start</span></span>

* <span data-ttu-id="8b17f-143">Uw Azure gebruikersaccount moet zijn bepaalde [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) replicatie van Azure een virtuele machine in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="8b17f-143">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="8b17f-144">Uw Azure-abonnement moet worden ingeschakeld voor het maken van virtuele machines in de doellocatie die u wilt gebruiken als het herstel na noodgevallen regio.</span><span class="sxs-lookup"><span data-stu-id="8b17f-144">Your Azure subscription should be enabled to create VMs in the target location that you want to use as the disaster recovery region.</span></span> <span data-ttu-id="8b17f-145">Neem contact op met ondersteuning voor het inschakelen van de quota voor vereist.</span><span class="sxs-lookup"><span data-stu-id="8b17f-145">Contact support to enable the required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="8b17f-146">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="8b17f-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="8b17f-147">U wordt aangeraden dat u de Recovery Services-kluis in de locatie waar u uw virtuele machines maken worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="8b17f-147">We recommend that you create the Recovery Services vault in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="8b17f-148">Bijvoorbeeld, als uw doellocatie is de centraal VS, maken de kluis in **VS-midden**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-148">For example, if your target location is the central US, create the vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="8b17f-149">Replicatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="8b17f-149">Enable replication</span></span>

<span data-ttu-id="8b17f-150">In **Recovery Services-kluizen**, klikt u op de kluisnaam van de.</span><span class="sxs-lookup"><span data-stu-id="8b17f-150">In **Recovery Services vaults**, click the vault name.</span></span> <span data-ttu-id="8b17f-151">Klik in de kluis op de **+ repliceren** knop.</span><span class="sxs-lookup"><span data-stu-id="8b17f-151">In the vault, click the **+Replicate** button.</span></span>

### <a name="step-1-configure-the-source"></a><span data-ttu-id="8b17f-152">Step 1.</span><span class="sxs-lookup"><span data-stu-id="8b17f-152">Step 1.</span></span> <span data-ttu-id="8b17f-153">De configureren</span><span class="sxs-lookup"><span data-stu-id="8b17f-153">Configure the source</span></span>
1. <span data-ttu-id="8b17f-154">In **bron**, selecteer **Azure - PREVIEW**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="8b17f-155">In **bronlocatie**, selecteer de bron van Azure-regio waarin uw virtuele machines worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8b17f-155">In **Source location**, select the source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="8b17f-156">Selecteer het implementatiemodel van uw virtuele machines: **Resource Manager** of **klassieke**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-156">Select the deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="8b17f-157">Selecteer de **resourcegroep** voor Resource Manager virtuele machines of **cloudservice** voor klassieke virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8b17f-157">Select the **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![De configureren](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="8b17f-159">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="8b17f-159">Step 2.</span></span> <span data-ttu-id="8b17f-160">Selecteer de virtuele machines</span><span class="sxs-lookup"><span data-stu-id="8b17f-160">Select virtual machines</span></span>

* <span data-ttu-id="8b17f-161">Selecteer de virtuele machines die u wilt repliceren, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-161">Select the VMs you want to replicate, and then click **OK**.</span></span>

    ![Selecteer de virtuele machines](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="8b17f-163">Stap 3.</span><span class="sxs-lookup"><span data-stu-id="8b17f-163">Step 3.</span></span> <span data-ttu-id="8b17f-164">Instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="8b17f-164">Configure settings</span></span>

1. <span data-ttu-id="8b17f-165">Als u wilt overschrijven de standaardinstellingen van het doel en geef de instellingen van uw keuze, klikt u op **aanpassen**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-165">To override the default target settings and specify the settings of your choice, click **Customize**.</span></span> <span data-ttu-id="8b17f-166">Zie voor meer informatie [doelresources aanpassen](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span><span class="sxs-lookup"><span data-stu-id="8b17f-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![Instellingen configureren](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="8b17f-168">Standaard maakt Site Recovery een replicatiebeleid die ervoor zorgt dat toepassingsconsistente momentopnamen elke 4 uur handhaaft herstelpunten gedurende 24 uur.</span><span class="sxs-lookup"><span data-stu-id="8b17f-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="8b17f-169">Als een beleid maken met verschillende instellingen, klikt u op **aanpassen** naast **replicatiebeleid**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-169">To create a policy with different settings, click **Customize** next to **Replication Policy**.</span></span>

    ![Beleid aanpassen](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="8b17f-171">Als u wilt inrichten van de doelresources, klikt u op **doelresources maken**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-171">To start provisioning the target resources, click **Create target resources**.</span></span> <span data-ttu-id="8b17f-172">Inrichting duurt een minuut.</span><span class="sxs-lookup"><span data-stu-id="8b17f-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="8b17f-173">Sluit de blade niet tijdens het inrichten of u wilt beginnen.</span><span class="sxs-lookup"><span data-stu-id="8b17f-173">Don't close the blade during provisioning, or you need to start over.</span></span>

4. <span data-ttu-id="8b17f-174">Om replicatie van de geselecteerde virtuele machine, klikt u op **replicatie inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-174">To trigger replication of the selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="8b17f-175">U kunt de voortgang van volgen de **beveiliging inschakelen** taak **instellingen** > **taken** > **Site Recovery-taken**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-175">You can track progress of the **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="8b17f-176">In **instellingen** > **gerepliceerde Items**, vindt u de status van virtuele machines en de voortgang van de initiële replicatie.</span><span class="sxs-lookup"><span data-stu-id="8b17f-176">In **Settings** > **Replicated Items**, you can view the status of VMs and the initial replication progress.</span></span> <span data-ttu-id="8b17f-177">Klik op de virtuele machine Inzoomen op de instellingen ervan.</span><span class="sxs-lookup"><span data-stu-id="8b17f-177">Click the VM to drill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="8b17f-178">Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8b17f-178">Run a test failover</span></span>

<span data-ttu-id="8b17f-179">Nadat u alles instellen, voert u een testfailover om te controleren of dat alles werkt zoals verwacht:</span><span class="sxs-lookup"><span data-stu-id="8b17f-179">After you set up everything, run a test failover to make sure everything's working as expected:</span></span>

1. <span data-ttu-id="8b17f-180">Een enkele machine failover **instellingen** > **gerepliceerde Items**, klikt u op de virtuele machine **+ Testfailover** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8b17f-180">To fail over a single machine, in **Settings** > **Replicated Items**, click the VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="8b17f-181">Failover van een herstelplan **instellingen** > **herstelplannen**, met de rechtermuisknop op het plan **Testfailover**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-181">To fail over a recovery plan, in **Settings** > **Recovery Plans**, right-click the plan **Test Failover**.</span></span> <span data-ttu-id="8b17f-182">Volg [deze instructies](site-recovery-create-recovery-plans.md) om een herstelplan te maken.</span><span class="sxs-lookup"><span data-stu-id="8b17f-182">To create a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="8b17f-183">In **Testfailover**, selecteer het doelobject voor de virtuele Azure-netwerk voor welke Azure VM's na de failover zijn verbonden.</span><span class="sxs-lookup"><span data-stu-id="8b17f-183">In **Test Failover**, select the target Azure virtual network to which Azure VMs are connected after the failover occurs.</span></span>

4. <span data-ttu-id="8b17f-184">Voor het starten van de failover, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-184">To start the failover, click **OK**.</span></span> <span data-ttu-id="8b17f-185">Om de voortgang volgen, klikt u op de virtuele machine om de eigenschappen te openen.</span><span class="sxs-lookup"><span data-stu-id="8b17f-185">To track progress, click the VM to open its properties.</span></span> <span data-ttu-id="8b17f-186">U kunt ook op de **Testfailover** taak in de kluisnaam > **instellingen** > **taken** > **Site Recovery-taken**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-186">Or you can click the **Test Failover** job in the vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="8b17f-187">Nadat de failover is voltooid, de replica-machine van Azure wordt weergegeven in de Azure portal > **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="8b17f-187">After the failover finishes, the replica Azure machine appears in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="8b17f-188">Zorg ervoor dat de virtuele machine is de juiste grootte heeft, of deze is verbonden met het juiste netwerk en dat deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8b17f-188">Make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="8b17f-189">Als u wilt verwijderen van de virtuele machines die zijn gemaakt tijdens de testfailover, klikt u op **opschonen testfailover** voor het gerepliceerde artikel of het herstelplan.</span><span class="sxs-lookup"><span data-stu-id="8b17f-189">To delete the VMs that were created during the test failover, click **Cleanup test failover** on the replicated item or the recovery plan.</span></span> <span data-ttu-id="8b17f-190">In **notities**, vastleggen en opslaan van eventuele opmerkingen die zijn gekoppeld aan de testfailover.</span><span class="sxs-lookup"><span data-stu-id="8b17f-190">In **Notes**, record and save any observations associated with the test failover.</span></span> 

<span data-ttu-id="8b17f-191">[Meer informatie](site-recovery-test-failover-to-azure.md) over testfailovers.</span><span class="sxs-lookup"><span data-stu-id="8b17f-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8b17f-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8b17f-192">Next steps</span></span>

<span data-ttu-id="8b17f-193">Nadat u de implementatie te testen:</span><span class="sxs-lookup"><span data-stu-id="8b17f-193">After you test the deployment:</span></span>

- <span data-ttu-id="8b17f-194">[Meer informatie](site-recovery-failover.md) over verschillende typen failovers en het uitvoeren hiervan.</span><span class="sxs-lookup"><span data-stu-id="8b17f-194">[Learn more](site-recovery-failover.md) about different types of failovers and how to run them.</span></span>
- <span data-ttu-id="8b17f-195">Meer informatie over [met herstelplannen](site-recovery-create-recovery-plans.md) te verminderen RTO.</span><span class="sxs-lookup"><span data-stu-id="8b17f-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) to reduce RTO.</span></span>
