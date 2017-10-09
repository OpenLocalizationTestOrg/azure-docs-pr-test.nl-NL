---
title: aaaSet van een replicatiebeleid voor voor virtuele machine van Hyper-V-replicatie (zonder de System Center VMM) tooAzure met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen u moet tooset van een beleid voor wachtwoordreplicatie bij het repliceren van Hyper-V-machines tooAzure opslag
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a><span data-ttu-id="389be-103">Stap 9: Een replicatiebeleid voor virtuele machine van Hyper-V-replicatie tooAzure instellen</span><span class="sxs-lookup"><span data-stu-id="389be-103">Step 9: Set up a replication policy for Hyper-V VM replication tooAzure</span></span>

<span data-ttu-id="389be-104">Dit artikel wordt beschreven hoe tooset van een beleid voor wachtwoordreplicatie wanneer u tooAzure van de Hyper-V-machines (zonder de System Center VMM repliceert) met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="389be-104">This article describes how tooset up a replication policy when you're replicating Hyper-V VMs tooAzure (without System Center VMM) using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="389be-105">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="389be-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="about-snapshots"></a><span data-ttu-id="389be-106">Over momentopnamen</span><span class="sxs-lookup"><span data-stu-id="389be-106">About snapshots</span></span>

<span data-ttu-id="389be-107">Hyper-V gebruikt twee soorten momentopnamen: standaardmomentopnamen waarmee een incrementele momentopname van Hallo volledige virtuele machine en een toepassingsconsistente momentopnamen waarmee een momentopname van een punt in tijd van de toepassingsgegevens Hallo in Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="389be-107">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span>
    - <span data-ttu-id="389be-108">Toepassingsconsistente momentopnamen gebruiken Volume Shadow Copy Service (VSS) tooensure die toepassingen zich in een consistente status wanneer Hallo momentopname wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="389be-108">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span>
    - <span data-ttu-id="389be-109">Als u toepassingsconsistente momentopnamen inschakelt, wordt het Hallo-prestaties van toepassingen die worden uitgevoerd op virtuele bronmachines beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="389be-109">If you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="389be-110">Zorg ervoor dat Hallo-waarde lager dan Hallo aantal aanvullende herstelpunten dat u configureert.</span><span class="sxs-lookup"><span data-stu-id="389be-110">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>

## <a name="set-up-a-replication-policy"></a><span data-ttu-id="389be-111">Instellen van een beleid voor wachtwoordreplicatie</span><span class="sxs-lookup"><span data-stu-id="389be-111">Set up a replication policy</span></span>

1. <span data-ttu-id="389be-112">toocreate een nieuw replicatiebeleid, klikt u op **infrastructuur voorbereiden** > **replicatie-instellingen** > **+ maken en koppelen**.</span><span class="sxs-lookup"><span data-stu-id="389be-112">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Netwerk](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="389be-114">Geef in **Beleid maken en koppelen** een beleidsnaam op.</span><span class="sxs-lookup"><span data-stu-id="389be-114">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="389be-115">In **Kopieerfrequentie**, geef aan hoe vaak u tooreplicate deltagegevens na de initiële replicatie van hello (elke 30 seconden, 5 of 15 minuten).</span><span class="sxs-lookup"><span data-stu-id="389be-115">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="389be-116">Een 30 tweede frequentie wordt niet ondersteund bij het repliceren van toopremium opslag.</span><span class="sxs-lookup"><span data-stu-id="389be-116">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="389be-117">Hallo-beperking wordt bepaald door Hallo aantal momentopnamen per blob (100) wordt ondersteund door de premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="389be-117">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="389be-118">[Meer informatie](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span><span class="sxs-lookup"><span data-stu-id="389be-118">[Learn more](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="389be-119">In **herstel bewaarperiode**, geeft u in hoe lang uren Hallo bewaarperiode is voor elk herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="389be-119">In **Recovery point retention**, specify in hours how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="389be-120">Virtuele machines kunnen worden hersteld tooany punt in een venster.</span><span class="sxs-lookup"><span data-stu-id="389be-120">VMs can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="389be-121">In **App-consistente momentopname frequentie**, opgeven hoe vaak (1-12 uur) herstelpunten met toepassingsconsistente momentopnamen worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="389be-121">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>
6. <span data-ttu-id="389be-122">In **begintijd initiële replicatie**, opgeven wanneer toostart Hallo initiële replicatie.</span><span class="sxs-lookup"><span data-stu-id="389be-122">In **Initial replication start time**, specify when toostart hello initial replication.</span></span> <span data-ttu-id="389be-123">Hallo replicatie vindt plaats via uw internetbandbreedte zodat tooschedule kunt u deze buiten de drukste tijden.</span><span class="sxs-lookup"><span data-stu-id="389be-123">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span> <span data-ttu-id="389be-124">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="389be-124">Then click **OK**.</span></span>

    ![Beleid voor replicatie](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

<span data-ttu-id="389be-126">Wanneer u een nieuw beleid maakt, wordt dit automatisch gekoppeld met de Hallo Hyper-V-site.</span><span class="sxs-lookup"><span data-stu-id="389be-126">When you create a new policy, it's automatically associated with hello Hyper-V site.</span></span> <span data-ttu-id="389be-127">U kunt een Hyper-V-site (en Hallo virtuele machines erin) koppelen aan meerdere beleidsregels voor replicatie in **replicatie** > beleidsnaam > **Hyper-V-Site koppelen**.</span><span class="sxs-lookup"><span data-stu-id="389be-127">You can associate a Hyper-V site (and hello VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="389be-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="389be-128">Next steps</span></span>

<span data-ttu-id="389be-129">Ga te[stap 10: replicatie inschakelen](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="389be-129">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>
