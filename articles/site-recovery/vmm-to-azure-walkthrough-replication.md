---
title: Instellen van een beleid voor wachtwoordreplicatie voor replicatie naar Azure met Azure Site Recovery Hyper-V-machine (met VMM) | Microsoft Docs
description: Hierin wordt beschreven hoe u een beleid voor wachtwoordreplicatie voor Hyper-V-machine (met VMM)-replicatie naar Azure met Azure Site Recovery instellen
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
ms.openlocfilehash: 592e1c3f647e5b1f1d9aa776657e8f89b60349e1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-to-azure"></a><span data-ttu-id="76407-103">Stap 10: Een replicatiebeleid voor virtuele machine van Hyper-V-replicatie (met VMM) naar Azure instellen</span><span class="sxs-lookup"><span data-stu-id="76407-103">Step 10: Set up a replication policy for Hyper-V VM replication (with VMM) to Azure</span></span>


<span data-ttu-id="76407-104">Na het instellen van [netwerktoewijzing](vmm-to-azure-walkthrough-network-mapping.md), gebruik dit artikel voor het configureren van een beleid voor wachtwoordreplicatie T\to repliceren lokale Hyper-V virtuele machines die worden beheerd in System Center Virtual Machine Manager (VMM)-clouds naar Azure met behulp van de [Azure Site Recovery](site-recovery-overview.md) service in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="76407-104">After setting up [network mapping](vmm-to-azure-walkthrough-network-mapping.md), use this article to configure a replication policy T\to replicate on-premises Hyper-V virtual machines managed in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="76407-105">Na het lezen van dit artikel kunt u onder aan dit artikel of op het [Azure Recovery Services-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) opmerkingen of vragen plaatsen.</span><span class="sxs-lookup"><span data-stu-id="76407-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="create-a-policy"></a><span data-ttu-id="76407-106">Een beleid maken</span><span class="sxs-lookup"><span data-stu-id="76407-106">Create a policy</span></span>

1. <span data-ttu-id="76407-107">Als u nieuw replicatiebeleid wilt maken, klikt u op **Infrastructuur voorbereiden** > **Replicatie-instellingen** > **+Maken en koppelen**.</span><span class="sxs-lookup"><span data-stu-id="76407-107">To create a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Netwerk](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="76407-109">Geef in **Beleid maken en koppelen** een beleidsnaam op.</span><span class="sxs-lookup"><span data-stu-id="76407-109">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="76407-110">Geef in **Kopieerfrequentie** op hoe vaak u na de eerste replicatie de verschillen wilt repliceren (elke 30 seconden of elke 5 of 15 minuten).</span><span class="sxs-lookup"><span data-stu-id="76407-110">In **Copy frequency**, specify how often you want to replicate delta data after the initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    >  <span data-ttu-id="76407-111">Een frequentie van 30 seconden wordt niet ondersteund bij het repliceren naar Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="76407-111">A 30 second frequency isn't supported when replicating to premium storage.</span></span> <span data-ttu-id="76407-112">De beperking wordt bepaald door het aantal momentopnamen per blob (100) dat wordt ondersteund door Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="76407-112">The limitation is determined by the number of snapshots per blob (100) supported by premium storage.</span></span> [<span data-ttu-id="76407-113">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="76407-113">Learn more</span></span>](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. <span data-ttu-id="76407-114">Geef in **Bewaarperiode van het herstelpunt** op hoeveel uur elk herstelpunt moet worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="76407-114">In **Recovery point retention**, specify in hours how long the retention window will be for each recovery point.</span></span> <span data-ttu-id="76407-115">Beveiligde machines kunnen te allen tijde worden hersteld naar een willekeurig punt (binnen een bepaald tijdsvenster).</span><span class="sxs-lookup"><span data-stu-id="76407-115">Protected machines can be recovered to any point within a window.</span></span>
5. <span data-ttu-id="76407-116">Geef in **Frequentie van de app-consistente momentopname** op hoe vaak (elke 1-12 uur) er herstelpunten moeten worden gemaakt met toepassingsconsistente momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="76407-116">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="76407-117">Hyper-V maakt gebruik van twee soorten momentopnamen: standaardmomentopnamen waarmee steeds incrementele momentopnamen van de volledige virtuele machine worden gemaakt, en toepassingsconsistente momentopnamen waarmee een tijdsgebonden momentopname wordt gemaakt van de toepassingsgegevens in de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="76407-117">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of the entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of the application data inside the virtual machine.</span></span> <span data-ttu-id="76407-118">Toepassingsconsistente momentopnamen gebruiken Volume Shadow Copy Service (VSS) om ervoor te zorgen dat toepassingen een consistente status hebben wanneer er een momentopname wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="76407-118">Application-consistent snapshots use Volume Shadow Copy Service (VSS) to ensure that applications are in a consistent state when the snapshot is taken.</span></span> <span data-ttu-id="76407-119">Als u toepassingsconsistente momentopnamen inschakelt, is dit van invloed op de prestaties van de toepassingen die via de virtuele bronmachines worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="76407-119">Note that if you enable application-consistent snapshots, it will affect the performance of applications running on source virtual machines.</span></span> <span data-ttu-id="76407-120">Zorg ervoor dat de waarde die u instelt, kleiner is dan het aantal aanvullende herstelpunten dat u configureert.</span><span class="sxs-lookup"><span data-stu-id="76407-120">Ensure that the value you set is less than the number of additional recovery points you configure.</span></span>
6. <span data-ttu-id="76407-121">Geef in **Begintijd initiële replicatie** aan wanneer de initiële replicatie moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="76407-121">In **Initial replication start time**, indicate when to start the initial replication.</span></span> <span data-ttu-id="76407-122">De replicatie maakt gebruik van uw internetbandbreedte. Daarom is het een goed idee om de replicatie buiten de drukste tijden in te plannen.</span><span class="sxs-lookup"><span data-stu-id="76407-122">The replication occurs over your internet bandwidth so you might want to schedule it outside your busy hours.</span></span>
7. <span data-ttu-id="76407-123">Geef in **Gegevens versleutelen die zijn opgeslagen in Azure** op of u at-rest-gegevens in de Azure-opslag wilt versleutelen.</span><span class="sxs-lookup"><span data-stu-id="76407-123">In **Encrypt data stored on Azure**, specify whether to encrypt at rest data in Azure storage.</span></span> <span data-ttu-id="76407-124">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="76407-124">Then click **OK**.</span></span>

    ![Beleid voor replicatie](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="76407-126">Wanneer u nieuw beleid maakt, wordt dit automatisch gekoppeld aan de VMM-cloud.</span><span class="sxs-lookup"><span data-stu-id="76407-126">When you create a new policy it's automatically associated with the VMM cloud.</span></span> <span data-ttu-id="76407-127">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="76407-127">Click **OK**.</span></span> <span data-ttu-id="76407-128">U kunt aanvullende VMM-clouds (en de virtuele machines hierin) koppelen aan dit replicatiebeleid. Dit doet u via **Replicatie** > beleidsnaam > **VMM-cloud koppelen**.</span><span class="sxs-lookup"><span data-stu-id="76407-128">You can associate additional VMM clouds (and the VMs in them) with this replication policy in **Replication** > policy name > **Associate VMM Cloud**.</span></span>

    ![Beleid voor replicatie](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a><span data-ttu-id="76407-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="76407-130">Next steps</span></span>

<span data-ttu-id="76407-131">Ga naar [stap 11: replicatie inschakelen](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="76407-131">Go to [Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>
