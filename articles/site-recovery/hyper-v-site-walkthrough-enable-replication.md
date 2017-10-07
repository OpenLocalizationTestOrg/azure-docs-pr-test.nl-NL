---
title: aaaEnable replicatie voor de Hyper-V-machines repliceren tooAzure (zonder de System Center VMM) met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen hebt u tooenable replicatie tooAzure voor Hyper-V-machines met behulp van hello Azure Site Recovery-service
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a><span data-ttu-id="1f45a-103">Stap 10: Replicatie inschakelen voor Hyper-V-machines repliceren tooAzure</span><span class="sxs-lookup"><span data-stu-id="1f45a-103">Step 10: Enable replication for Hyper-V VMs replicating tooAzure</span></span>


<span data-ttu-id="1f45a-104">Dit artikel wordt beschreven hoe tooenable replicatie voor de lokale Hyper-V virtuele machines (wordt niet beheerd door System Center VMM) tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1f45a-104">This article describes how tooenable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="1f45a-105">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="1f45a-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="1f45a-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="1f45a-106">Before you start</span></span>

<span data-ttu-id="1f45a-107">Voordat u begint, zorg ervoor dat uw Azure gebruikersaccount Hallo vereist [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicatie van een nieuwe virtuele machine tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1f45a-107">Before you start, ensure that your Azure user account has hello required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of a new virtual machine tooAzure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="1f45a-108">Schijven uitsluiten van replicatie</span><span class="sxs-lookup"><span data-stu-id="1f45a-108">Exclude disks from replication</span></span>

<span data-ttu-id="1f45a-109">Standaard worden alle schijven op een machine gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="1f45a-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="1f45a-110">U kunt schijven uitsluiten van replicatie.</span><span class="sxs-lookup"><span data-stu-id="1f45a-110">You can exclude disks from replication.</span></span> <span data-ttu-id="1f45a-111">Zo wilt u mogelijk niet tooreplicate schijven met tijdelijke gegevens of gegevens die telkens wanneer een machine is bijgewerkt of de toepassing opnieuw wordt gestart (bijvoorbeeld pagefile.sys of SQL Server tempdb).</span><span class="sxs-lookup"><span data-stu-id="1f45a-111">For example you might not want tooreplicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="1f45a-112">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="1f45a-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="1f45a-113">Virtuele machines repliceren</span><span class="sxs-lookup"><span data-stu-id="1f45a-113">Replicate VMs</span></span>

<span data-ttu-id="1f45a-114">Replicatie voor virtuele machines als volgt inschakelen:</span><span class="sxs-lookup"><span data-stu-id="1f45a-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="1f45a-115">Klik op **toepassing repliceren** > **bron**.</span><span class="sxs-lookup"><span data-stu-id="1f45a-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="1f45a-116">Nadat u replicatie voor Hallo eerst hebt ingesteld, klikt u op **+ repliceren** tooenable replicatie voor aanvullende machines.</span><span class="sxs-lookup"><span data-stu-id="1f45a-116">After you've set up replication for hello first time, you can click **+Replicate** tooenable replication for additional machines.</span></span>

    ![Replicatie inschakelen](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="1f45a-118">In **bron**, selecteer Hallo Hyper-V-site.</span><span class="sxs-lookup"><span data-stu-id="1f45a-118">In **Source**, select hello Hyper-V site.</span></span> <span data-ttu-id="1f45a-119">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f45a-119">Then click **OK**.</span></span>
3. <span data-ttu-id="1f45a-120">In **doel**Hallo kluis abonnement en selecteer Hallo gewenste toouse in Azure (klassiek of de resource management) na een failover van failover-model.</span><span class="sxs-lookup"><span data-stu-id="1f45a-120">In **Target**, select hello vault subscription, and hello failover model you want toouse in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="1f45a-121">Selecteer Hallo gewenste toouse storage-account.</span><span class="sxs-lookup"><span data-stu-id="1f45a-121">Select hello storage account you want toouse.</span></span> <span data-ttu-id="1f45a-122">Als u een account dat u wilt dat toouse geen hebt, kunt u [maken van een](#set-up-an-azure-storage-account).</span><span class="sxs-lookup"><span data-stu-id="1f45a-122">If you don't have an account you want toouse, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="1f45a-123">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f45a-123">Then click **OK**.</span></span>
5. <span data-ttu-id="1f45a-124">Selecteer hello Azure-netwerk en subnet toowhich virtuele Azure-machines verbinding maken wanneer ze failover worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1f45a-124">Select hello Azure network and subnet toowhich Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="1f45a-125">Selecteer tooapply Hallo instellingen tooall machines in het netwerk u inschakelen voor replicatie, **nu configureren voor geselecteerde machines**.</span><span class="sxs-lookup"><span data-stu-id="1f45a-125">tooapply hello network settings tooall machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="1f45a-126">Selecteer **later configureren** tooselect hello Azure-netwerk per computer.</span><span class="sxs-lookup"><span data-stu-id="1f45a-126">Select **Configure later** tooselect hello Azure network per machine.</span></span>
    - <span data-ttu-id="1f45a-127">Als u een netwerk dat u wilt dat toouse geen hebt, kunt u [maken van een](#set-up-an-azure-network).</span><span class="sxs-lookup"><span data-stu-id="1f45a-127">If you don't have a network you want toouse, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="1f45a-128">Selecteer indien van toepassing een subnet.</span><span class="sxs-lookup"><span data-stu-id="1f45a-128">Select a subnet if applicable.</span></span> <span data-ttu-id="1f45a-129">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f45a-129">Then click **OK**.</span></span>

   ![Replicatie inschakelen](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="1f45a-131">In **virtuele Machines** > **virtuele machines selecteren**en klik op elke machine die u wilt dat tooreplicate selecteren.</span><span class="sxs-lookup"><span data-stu-id="1f45a-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="1f45a-132">U kunt alleen machines selecteren waarvoor replicatie kan worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="1f45a-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="1f45a-133">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f45a-133">Then click **OK**.</span></span>

    ![Replicatie inschakelen](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="1f45a-135">In **eigenschappen** > **eigenschappen configureren**Hallo-besturingssysteem voor virtuele machines Hallo geselecteerd en selecteer Hallo besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="1f45a-135">In **Properties** > **Configure properties**, select hello operating system for hello selected VMs, and hello OS disk.</span></span>
8. <span data-ttu-id="1f45a-136">Controleer of deze Hallo Azure VM-naam (doelnaam) voldoet aan [vereisten van de virtuele machine van Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="1f45a-136">Verify that hello Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="1f45a-137">Standaard worden alle Hallo schijven Hallo VM geselecteerd voor replicatie.</span><span class="sxs-lookup"><span data-stu-id="1f45a-137">By default all hello disks of hello VM are selected for replication.</span></span> <span data-ttu-id="1f45a-138">Schakel schijven tooexclude ze.</span><span class="sxs-lookup"><span data-stu-id="1f45a-138">Clear disks tooexclude them.</span></span>
10. <span data-ttu-id="1f45a-139">Klik op **OK** toosave wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="1f45a-139">Click **OK** toosave changes.</span></span> <span data-ttu-id="1f45a-140">Later kunt u eventueel extra eigenschappen instellen.</span><span class="sxs-lookup"><span data-stu-id="1f45a-140">You can set additional properties later.</span></span>

    ![Replicatie inschakelen](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="1f45a-142">In **replicatie-instellingen** > **replicatie-instellingen configureren**, Hallo replicatiebeleid u tooapply voor Hallo virtuele machines beveiligde wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="1f45a-142">In **Replication settings** > **Configure replication settings**, select hello replication policy you want tooapply for hello protected VMs.</span></span> <span data-ttu-id="1f45a-143">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f45a-143">Then click **OK**.</span></span> <span data-ttu-id="1f45a-144">U kunt het replicatiebeleid Hallo in wijzigen **replicatiebeleid** > beleidsnaam > **instellingen bewerken**.</span><span class="sxs-lookup"><span data-stu-id="1f45a-144">You can modify hello replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="1f45a-145">De wijzigingen die u toepast, worden zowel gebruikt voor machines die al worden gerepliceerd, als voor nieuwe machines.</span><span class="sxs-lookup"><span data-stu-id="1f45a-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![Replicatie inschakelen](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="1f45a-147">U kunt de voortgang van Hallo volgen **beveiliging inschakelen** taak **taken** > **Site Recovery-taken**.</span><span class="sxs-lookup"><span data-stu-id="1f45a-147">You can track progress of hello **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="1f45a-148">Na het Hallo **beveiliging voltooien** taak wordt uitgevoerd Hallo machine is gereed voor failover.</span><span class="sxs-lookup"><span data-stu-id="1f45a-148">After hello **Finalize Protection** job runs hello machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1f45a-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1f45a-149">Next steps</span></span>


<span data-ttu-id="1f45a-150">Ga te[stap 11: een testfailover uitvoeren](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="1f45a-150">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
