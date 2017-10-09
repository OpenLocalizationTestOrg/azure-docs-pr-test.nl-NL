---
title: aaaEnable replicatie voor virtuele Azure-machines tooanother Azure-regio met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen moet u tooenable replicatie tooanother Azure-regio voor Azure VM's met behulp van hello Azure Site Recovery-service
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a><span data-ttu-id="fabb9-103">Stap 5: Replicatie inschakelen voor Azure Virtual machines</span><span class="sxs-lookup"><span data-stu-id="fabb9-103">Step 5: Enable replication for Azure VMs</span></span>


<span data-ttu-id="fabb9-104">Na het instellen van een [Recovery Services-kluis](azure-to-azure-walkthrough-vault.md), gebruiken deze artikel tooenable replicatie van virtuele machines (VM's), tooanother Azure-regio met [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fabb9-104">After setting up a [Recovery Services vault](azure-to-azure-walkthrough-vault.md), use this article tooenable replication of virtual machines (VMs), tooanother Azure region, with [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="fabb9-105">tooenable replicatie, het instellen van de bron en doel-instellingen controleren van het replicatiebeleid Hallo en selecteert u virtuele machines die u wilt dat tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="fabb9-105">tooenable replication, you set up source and target settings, verify hello replication policy, and select VMs you want tooreplicate.</span></span>

- <span data-ttu-id="fabb9-106">Wanneer u klaar bent Hallo artikel uw Azure VM's moet worden gerepliceerd als toohello secundaire Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="fabb9-106">When you finish hello article, your Azure VMs should be replicating toohello secondary Azure region.</span></span>
- <span data-ttu-id="fabb9-107">Eventuele opmerkingen onder Hallo van dit artikel plaatsen of vragen in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="fabb9-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="fabb9-108">Replicatie van Azure VM is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="fabb9-108">Azure VM replication is currently in preview.</span></span>


## <a name="select-hello-source"></a><span data-ttu-id="fabb9-109">Hallo bron selecteren</span><span class="sxs-lookup"><span data-stu-id="fabb9-109">Select hello source</span></span> 

1. <span data-ttu-id="fabb9-110">Klik in de Recovery Services-kluizen op Hallo kluisnaam > **+ repliceren**.</span><span class="sxs-lookup"><span data-stu-id="fabb9-110">In Recovery Services vaults, click hello vault name > **+Replicate**.</span></span>
2. <span data-ttu-id="fabb9-111">In **bron**, selecteer **Azure - PREVIEW**.</span><span class="sxs-lookup"><span data-stu-id="fabb9-111">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="fabb9-112">In **bronlocatie**, selecteer Hallo bron Azure-regio waarin uw virtuele machines worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fabb9-112">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="fabb9-113">Selecteer Hallo **virtuele machine van Azure-implementatiemodel** voor virtuele machines: **Resource Manager** of **klassieke**.</span><span class="sxs-lookup"><span data-stu-id="fabb9-113">Select hello **Azure virtual machine deployment model** for VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="fabb9-114">Selecteer Hallo **resourcegroep** voor Resource Manager-VM's of **cloudservice** voor klassieke virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="fabb9-114">Select hello **Source resource group** for Resource Manager VMs, or **cloud service** for classic VMs.</span></span>
5. <span data-ttu-id="fabb9-115">Klik op **OK** toosave Hallo instellingen.</span><span class="sxs-lookup"><span data-stu-id="fabb9-115">Click **OK** toosave hello settings.</span></span>

    ![Hallo bron configureren](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a><span data-ttu-id="fabb9-117">Hallo virtuele machines selecteren</span><span class="sxs-lookup"><span data-stu-id="fabb9-117">Select hello VMs</span></span>

<span data-ttu-id="fabb9-118">Site Recovery wordt een lijst met virtuele machines die zijn gekoppeld aan het Hallo-abonnement en de resource-group/cloudservice Hallo opgehaald.</span><span class="sxs-lookup"><span data-stu-id="fabb9-118">Site Recovery retrieves a list of hello VMs associated with hello subscription and resource group/cloud service.</span></span>

1. <span data-ttu-id="fabb9-119">In **virtuele Machines**, Hallo VMs u tooreplicate wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="fabb9-119">In **Virtual Machines**, select hello VMs you want tooreplicate.</span></span>
2. <span data-ttu-id="fabb9-120">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="fabb9-120">Click **OK**.</span></span>

    ![Selecteer de virtuele machines](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a><span data-ttu-id="fabb9-122">Instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="fabb9-122">Configure settings</span></span>

<span data-ttu-id="fabb9-123">Site Recovery standaardinstellingen voor Hallo doelregio (op basis van de regio broninstellingen Hallo), bepalingen en Hallo replicatiebeleid:</span><span class="sxs-lookup"><span data-stu-id="fabb9-123">Site Recovery provisions default settings for hello target region (based on hello source region settings), and hello replication policy:</span></span>

   - <span data-ttu-id="fabb9-124">**Doellocatie**: Hallo doelregio gewenste toouse voor herstel na noodgevallen.</span><span class="sxs-lookup"><span data-stu-id="fabb9-124">**Target location**: hello target region you want toouse for disaster recovery.</span></span> <span data-ttu-id="fabb9-125">U wordt aangeraden Hallo-locatie van de Site Recovery-kluis Hallo komt overeen met Hallo target-locatie.</span><span class="sxs-lookup"><span data-stu-id="fabb9-125">We recommend that hello target location matches hello location of hello Site Recovery vault.</span></span>
   - <span data-ttu-id="fabb9-126">**Doelresourcegroep**: Resource groep toowhich Azure VM's in de doelregio Hallo behoort na een failover.</span><span class="sxs-lookup"><span data-stu-id="fabb9-126">**Target resource group**: Resource group toowhich Azure VMs in hello target region will belong after failover.</span></span> <span data-ttu-id="fabb9-127">Site Recovery maakt standaard een nieuwe resourcegroep in Hallo doelregio met een achtervoegsel 'asr'.</span><span class="sxs-lookup"><span data-stu-id="fabb9-127">By default, Site Recovery creates a new resource group in hello target region with an "asr" suffix.</span></span> 
   - <span data-ttu-id="fabb9-128">**Virtuele doelnetwerk**: Hallo netwerk in welke Azure VM's in Hallo doelregio geplaatst na een failover worden.</span><span class="sxs-lookup"><span data-stu-id="fabb9-128">**Target virtual network**: hello network in which Azure VMs in hello target region will be located after failover.</span></span> <span data-ttu-id="fabb9-129">Site Recovery maakt standaard een nieuw virtueel netwerk (en subnetten) in de doelregio Hallo met een achtervoegsel 'asr'.</span><span class="sxs-lookup"><span data-stu-id="fabb9-129">By default, Site Recovery creates a new virtual network (and subnets) in hello target region with an "asr" suffix.</span></span> <span data-ttu-id="fabb9-130">Dit netwerk is toegewezen tooyour Bronnetwerk.</span><span class="sxs-lookup"><span data-stu-id="fabb9-130">This network is mapped tooyour source network.</span></span> <span data-ttu-id="fabb9-131">Houd er rekening mee dat u een specifiek IP-adres na een failover van een virtuele machine kunt toewijzen, als u tooretain Hallo moet dezelfde IP-adres van de bron- en doellocaties Hallo.</span><span class="sxs-lookup"><span data-stu-id="fabb9-131">Note that you can assign a specific IP address after failover of a VM, if you need tooretain hello same IP address in hello source and target locations.</span></span> 
   - <span data-ttu-id="fabb9-132">**Storage-accounts in de cache**: Site Recovery maakt gebruik van een opslagaccount in Hallo bron regio.</span><span class="sxs-lookup"><span data-stu-id="fabb9-132">**Cache storage accounts**: Site Recovery uses a storage account in hello source region.</span></span> <span data-ttu-id="fabb9-133">Wijzigingen op de bron-VM's verzonden toothis account voordat replicatie toohello target-locatie.</span><span class="sxs-lookup"><span data-stu-id="fabb9-133">Changes on source VMs are sent toothis account, before replication toohello target location.</span></span> 
   - <span data-ttu-id="fabb9-134">**Storage-accounts zijn gericht**: Site Recovery maakt standaard een nieuw opslagaccount in Hallo doelregio, toomirror Hallo bron VM storage-account.</span><span class="sxs-lookup"><span data-stu-id="fabb9-134">**Target storage accounts**: By default, Site Recovery creates a new storage account in hello target region, toomirror hello source VM storage account.</span></span>
   -  <span data-ttu-id="fabb9-135">**Beschikbaarheidssets doel**: Site Recovery maakt standaard een nieuwe beschikbaarheidsset voor de doelregio Hallo met Hallo 'asr' achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="fabb9-135">**Target availability sets**: By default, Site Recovery creates a new availability set in hello target region, with hello "asr" suffix.</span></span> 
   - <span data-ttu-id="fabb9-136">**Replicatie-beleidsnaam**: de naam van beleid.</span><span class="sxs-lookup"><span data-stu-id="fabb9-136">**Replication policy name**: Policy name.</span></span>
   - <span data-ttu-id="fabb9-137">**Herstel bewaarperiode**: standaard Site Recovery herstelpunten blijft gedurende 24 uur.</span><span class="sxs-lookup"><span data-stu-id="fabb9-137">**Recovery point retention**: By default Site Recovery keeps recovery points for 24 hours.</span></span> <span data-ttu-id="fabb9-138">U kunt een waarde tussen 1 en 72 uur configureren.</span><span class="sxs-lookup"><span data-stu-id="fabb9-138">You can configure a value between 1 and 72 hours.</span></span>
   - <span data-ttu-id="fabb9-139">**App-consistente momentopname frequentie**: standaard Site Recovery maakt een app-consistente momentopname elke 4 uur.</span><span class="sxs-lookup"><span data-stu-id="fabb9-139">**App-consistent snapshot frequency**: By default Site Recovery takes an app-consistent snapshot every 4 hours.</span></span> <span data-ttu-id="fabb9-140">U kunt een waarde tussen 1 en 12 uur.</span><span class="sxs-lookup"><span data-stu-id="fabb9-140">You can configure any value between 1 and 12 hours.</span></span> <span data-ttu-id="fabb9-141">Gegevens worden continu gerepliceerd:</span><span class="sxs-lookup"><span data-stu-id="fabb9-141">Data is replicated continuously:</span></span>
    - <span data-ttu-id="fabb9-142">Crashconsistent herstelpunten onderhouden consistente gegevens schrijven-volgorde wanneer gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fabb9-142">Crash-consistent recovery points maintain consistent data write-order when created.</span></span> <span data-ttu-id="fabb9-143">Dit type herstelpunt is meestal voldoende als uw app ontworpen toorecover van een crash zonder gegevensinconsistenties</span><span class="sxs-lookup"><span data-stu-id="fabb9-143">This type of recovery point is usually sufficient if your app is designed toorecover from a crash without data inconsistencies</span></span>
    - <span data-ttu-id="fabb9-144">Crashconsistente herstelpunten worden gegenereerd om de paar minuten.</span><span class="sxs-lookup"><span data-stu-id="fabb9-144">Crash-consistent recovery points are generated every few minutes.</span></span> <span data-ttu-id="fabb9-145">Met deze punten herstel toofail via en herstel biedt uw virtuele machines een herstel Herstelpuntdoel (RPO) in de volgorde Hallo van minuten.</span><span class="sxs-lookup"><span data-stu-id="fabb9-145">Using these recovery points toofail over and recover your VMs provides a Recovery Point Objective (RPO) in hello order of minutes.</span></span>
    - <span data-ttu-id="fabb9-146">Toepassingsconsistente herstelpunten (in aanvulling toowrite volgorde consistentie) Zorg ervoor dat actief apps alle bewerkingen voltooid en buffers toodisk (toepassing stilleggen leegmaken).</span><span class="sxs-lookup"><span data-stu-id="fabb9-146">App-consistent recovery points (in addition toowrite-order consistency) ensure that running apps complete all operations and flush buffers toodisk (application quiescing).</span></span> <span data-ttu-id="fabb9-147">U wordt aangeraden dat u deze herstelpunten gebruiken voor database-apps, zoals SQL Server, Oracle en Exchange.</span><span class="sxs-lookup"><span data-stu-id="fabb9-147">We recommend you use these recovery points for database apps such as SQL Server, Oracle, and Exchange.</span></span>
        
    ![Instellingen configureren](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a><span data-ttu-id="fabb9-149">Instellingen wijzigen</span><span class="sxs-lookup"><span data-stu-id="fabb9-149">Modify settings</span></span>

<span data-ttu-id="fabb9-150">Als u toomodify doel- en replicatie beleidsinstellingen wilt, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="fabb9-150">If you want toomodify target and replication policy settings, do hello following:</span></span>

1. <span data-ttu-id="fabb9-151">tooview of doelinstellingen wijzigen, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="fabb9-151">tooview or modify target settings, click **Settings**.</span></span>
2. <span data-ttu-id="fabb9-152">toooverride hello doel standaardinstellingen, en klik op **aanpassen**.</span><span class="sxs-lookup"><span data-stu-id="fabb9-152">toooverride hello default target settings, click **Customize**.</span></span> <span data-ttu-id="fabb9-153">U kunt een doelresourcegroep, virtueel netwerk, beschikbaarheidsset en doel storage-account opgeven.</span><span class="sxs-lookup"><span data-stu-id="fabb9-153">You can specify a target resource group, virtual network, availability set, and target storage account.</span></span> <span data-ttu-id="fabb9-154">U kunt alleen beschikbaarheidssets toevoegen als virtuele machines deel van een set in Hallo bron regio uitmaken.</span><span class="sxs-lookup"><span data-stu-id="fabb9-154">You can only add availability sets if VMs are part of a set in hello source region.</span></span>

    ![Instellingen configureren](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. <span data-ttu-id="fabb9-156">Klik op toooverride replicatie-instellingen voor herstelpunten en toepassingsconsistente momentopnamen **aanpassen** volgende te**replicatiebeleid**.</span><span class="sxs-lookup"><span data-stu-id="fabb9-156">toooverride replication settings for recovery points and app-consistent snapshots, click **Customize** next too**Replication Policy**.</span></span>
 
    ![Instellingen configureren](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. <span data-ttu-id="fabb9-158">toostart inrichting Hallo doelresources, klikt u op **doelresources maken**.</span><span class="sxs-lookup"><span data-stu-id="fabb9-158">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="fabb9-159">Inrichting duurt een minuut.</span><span class="sxs-lookup"><span data-stu-id="fabb9-159">Provisioning takes a minute or so.</span></span> <span data-ttu-id="fabb9-160">Sluit de blade Hallo niet tijdens het inrichten of hebt u toostart via.</span><span class="sxs-lookup"><span data-stu-id="fabb9-160">Don't close hello blade during provisioning, or you'll have toostart over.</span></span>




## <a name="enable-replication"></a><span data-ttu-id="fabb9-161">Replicatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="fabb9-161">Enable replication</span></span>

1. <span data-ttu-id="fabb9-162">In **instellingen**, klikt u op **replicatie inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="fabb9-162">In **Settings**, click **Enable replication**.</span></span> <span data-ttu-id="fabb9-163">Hierdoor kan de initiële replicatie van Hallo virtuele machines die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="fabb9-163">This enables initial replication of hello VMs you selected.</span></span> <span data-ttu-id="fabb9-164">Status van de initiële replicatie kan sommige toorefresh tijd duren.</span><span class="sxs-lookup"><span data-stu-id="fabb9-164">Initial replication status might take some time toorefresh.</span></span> <span data-ttu-id="fabb9-165">Klik op **vernieuwen** tooget Hallo laatste status.</span><span class="sxs-lookup"><span data-stu-id="fabb9-165">Click **Refresh** tooget hello latest status.</span></span>

2. <span data-ttu-id="fabb9-166">U kunt de voortgang van Hallo volgen **beveiliging inschakelen** taak **instellingen** > **taken** > **Site Recovery-taken**.</span><span class="sxs-lookup"><span data-stu-id="fabb9-166">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

3. <span data-ttu-id="fabb9-167">In **instellingen** > **gerepliceerde Items**, kunt u weergeven Hallo status van virtuele machines en Hallo initiële replicatie uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fabb9-167">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="fabb9-168">Klik op Hallo VM toodrill omlaag in de instellingen ervan.</span><span class="sxs-lookup"><span data-stu-id="fabb9-168">Click hello VM toodrill down into its settings.</span></span>



## <a name="next-steps"></a><span data-ttu-id="fabb9-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fabb9-169">Next steps</span></span>

<span data-ttu-id="fabb9-170">Ga te[stap 6: een testfailover uitvoeren](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="fabb9-170">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>
