---
title: aaaSet van een beleid voor wachtwoordreplicatie voor Hyper-V-machine (met VMM) replicatie tooAzure met Azure Site Recovery | Microsoft Docs
description: Hierin wordt beschreven hoe tooset van een beleid voor wachtwoordreplicatie voor Hyper-V-machine (met VMM) replicatie tooAzure met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a><span data-ttu-id="68109-103">Stap 10: Een replicatiebeleid voor virtuele machine van Hyper-V-replicatie (met VMM) tooAzure instellen</span><span class="sxs-lookup"><span data-stu-id="68109-103">Step 10: Set up a replication policy for Hyper-V VM replication (with VMM) tooAzure</span></span>


<span data-ttu-id="68109-104">Na het instellen van [netwerktoewijzing](vmm-to-azure-walkthrough-network-mapping.md), gebruik dit artikel tooconfigure een beleid voor wachtwoordreplicatie T\tooreplicate lokale Hyper-V virtuele machines die worden beheerd in System Center Virtual Machine Manager (VMM) clouds tooAzure, met behulp van Hallo [ Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="68109-104">After setting up [network mapping](vmm-to-azure-walkthrough-network-mapping.md), use this article tooconfigure a replication policy T\tooreplicate on-premises Hyper-V virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="68109-105">Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="68109-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="create-a-policy"></a><span data-ttu-id="68109-106">Een beleid maken</span><span class="sxs-lookup"><span data-stu-id="68109-106">Create a policy</span></span>

1. <span data-ttu-id="68109-107">toocreate een nieuw replicatiebeleid, klikt u op **infrastructuur voorbereiden** > **replicatie-instellingen** > **+ maken en koppelen**.</span><span class="sxs-lookup"><span data-stu-id="68109-107">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Netwerk](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="68109-109">Geef in **Beleid maken en koppelen** een beleidsnaam op.</span><span class="sxs-lookup"><span data-stu-id="68109-109">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="68109-110">In **Kopieerfrequentie**, geef aan hoe vaak u tooreplicate deltagegevens na de initiële replicatie van hello (elke 30 seconden, 5 of 15 minuten).</span><span class="sxs-lookup"><span data-stu-id="68109-110">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    >  <span data-ttu-id="68109-111">Een 30 tweede frequentie wordt niet ondersteund bij het repliceren van toopremium opslag.</span><span class="sxs-lookup"><span data-stu-id="68109-111">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="68109-112">Hallo-beperking wordt bepaald door Hallo aantal momentopnamen per blob (100) wordt ondersteund door de premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="68109-112">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> [<span data-ttu-id="68109-113">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="68109-113">Learn more</span></span>](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. <span data-ttu-id="68109-114">In **herstel bewaarperiode**, in uren opgeven hoe lang de retentieperiode Hallo wordt worden voor elk herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="68109-114">In **Recovery point retention**, specify in hours how long hello retention window will be for each recovery point.</span></span> <span data-ttu-id="68109-115">Beveiligde machines kunnen worden hersteld tooany punt in een venster.</span><span class="sxs-lookup"><span data-stu-id="68109-115">Protected machines can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="68109-116">Geef in **Frequentie van de app-consistente momentopname** op hoe vaak (elke 1-12 uur) er herstelpunten moeten worden gemaakt met toepassingsconsistente momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="68109-116">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="68109-117">Hyper-V gebruikt twee soorten momentopnamen: standaardmomentopnamen waarmee een incrementele momentopname van Hallo volledige virtuele machine en een toepassingsconsistente momentopnamen waarmee een momentopname van een punt in tijd van de toepassingsgegevens Hallo in Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="68109-117">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span> <span data-ttu-id="68109-118">Toepassingsconsistente momentopnamen gebruiken Volume Shadow Copy Service (VSS) tooensure die toepassingen zich in een consistente status wanneer Hallo momentopname wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="68109-118">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span> <span data-ttu-id="68109-119">Houd er rekening mee dat als u toepassingsconsistente momentopnamen inschakelt, het invloed is op Hallo prestaties van toepassingen die worden uitgevoerd op virtuele machines die bron.</span><span class="sxs-lookup"><span data-stu-id="68109-119">Note that if you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="68109-120">Zorg ervoor dat Hallo-waarde lager dan Hallo aantal aanvullende herstelpunten dat u configureert.</span><span class="sxs-lookup"><span data-stu-id="68109-120">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>
6. <span data-ttu-id="68109-121">In **begintijd initiële replicatie**, geven wanneer toostart Hallo initiële replicatie.</span><span class="sxs-lookup"><span data-stu-id="68109-121">In **Initial replication start time**, indicate when toostart hello initial replication.</span></span> <span data-ttu-id="68109-122">Hallo replicatie vindt plaats via uw internetbandbreedte zodat tooschedule kunt u deze buiten de drukste tijden.</span><span class="sxs-lookup"><span data-stu-id="68109-122">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span>
7. <span data-ttu-id="68109-123">In **versleutelen van gegevens die zijn opgeslagen in Azure**, opgeven of tooencrypt op rest-gegevens in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="68109-123">In **Encrypt data stored on Azure**, specify whether tooencrypt at rest data in Azure storage.</span></span> <span data-ttu-id="68109-124">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="68109-124">Then click **OK**.</span></span>

    ![Beleid voor replicatie](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="68109-126">Wanneer u een nieuw beleid maakt is deze automatisch gekoppeld aan Hallo VMM-cloud.</span><span class="sxs-lookup"><span data-stu-id="68109-126">When you create a new policy it's automatically associated with hello VMM cloud.</span></span> <span data-ttu-id="68109-127">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="68109-127">Click **OK**.</span></span> <span data-ttu-id="68109-128">U kunt aanvullende VMM-clouds (en Hallo virtuele machines erin) koppelen aan dit replicatiebeleid in **replicatie** > beleidsnaam > **VMM-Cloud koppelen**.</span><span class="sxs-lookup"><span data-stu-id="68109-128">You can associate additional VMM clouds (and hello VMs in them) with this replication policy in **Replication** > policy name > **Associate VMM Cloud**.</span></span>

    ![Beleid voor replicatie](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a><span data-ttu-id="68109-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="68109-130">Next steps</span></span>

<span data-ttu-id="68109-131">Ga te[stap 11: replicatie inschakelen](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="68109-131">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>
