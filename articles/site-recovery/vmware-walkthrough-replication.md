---
title: aaaSet van een replicatiebeleid voor voor VMware VM replicatie tooAzure met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen u moet tooset van een beleid voor wachtwoordreplicatie bij het repliceren van virtuele VMware-machines tooAzure opslag
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 12870f3f98a4dd412221b817581403cd4bf7a76d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-tooazure"></a><span data-ttu-id="7c546-103">Stap 9: Een replicatiebeleid voor VMware VM replicatie tooAzure instellen</span><span class="sxs-lookup"><span data-stu-id="7c546-103">Step 9: Set up a replication policy for VMware VM replication tooAzure</span></span>


<span data-ttu-id="7c546-104">Dit artikel wordt beschreven hoe tooset van een beleid voor wachtwoordreplicatie wanneer u virtuele VMware-machines tooAzure met hello repliceert [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7c546-104">This article describes how tooset up a replication policy when you're replicating VMware VMs tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="7c546-105">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7c546-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="7c546-106">Een beleid configureren</span><span class="sxs-lookup"><span data-stu-id="7c546-106">Configure a policy</span></span>

<span data-ttu-id="7c546-107">Haal een snel overzicht van de video voordat u begint:</span><span class="sxs-lookup"><span data-stu-id="7c546-107">Get a quick video overview before you start:</span></span>
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. <span data-ttu-id="7c546-108">toocreate een nieuw replicatiebeleid, klikt u op **Site Recovery-infrastructuur** > **replicatiebeleid** > **+ replicatiebeleid**.</span><span class="sxs-lookup"><span data-stu-id="7c546-108">toocreate a new replication policy, click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="7c546-109">In **maken van beleid voor wachtwoordreplicatie**, een beleidsnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="7c546-109">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="7c546-110">In **RPO drempelwaarde**, Hallo RPO grootte opgeven.</span><span class="sxs-lookup"><span data-stu-id="7c546-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="7c546-111">Deze waarde geeft aan hoe vaak gegevens herstelpunten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7c546-111">This value specifies how often data recovery points are created.</span></span> <span data-ttu-id="7c546-112">Een waarschuwing wordt gegenereerd als continue replicatie deze limiet overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="7c546-112">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="7c546-113">In **herstel bewaarperiode**, opgeven hoe lang (in uren) Hallo bewaarperiode is voor elk herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="7c546-113">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="7c546-114">Gerepliceerde virtuele machines kunnen worden hersteld tooany punt in een venster.</span><span class="sxs-lookup"><span data-stu-id="7c546-114">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="7c546-115">Gerepliceerd toopremium opslag en 72 uur standaardopslag up too24 uren bewaren wordt ondersteund voor virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="7c546-115">Up too24 hours retention is supported for machines replicated toopremium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="7c546-116">In **App-consistente momentopname frequentie**, opgeven hoe vaak (in minuten) herstelpunten met toepassingsconsistente momentopnamen worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7c546-116">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="7c546-117">Klik op **OK** toocreate Hallo beleid.</span><span class="sxs-lookup"><span data-stu-id="7c546-117">Click **OK** toocreate hello policy.</span></span>

    ![Beleid voor replicatie](./media/vmware-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="7c546-119">Wanneer u een nieuw beleid maakt is deze automatisch gekoppeld aan Hallo configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="7c546-119">When you create a new policy it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="7c546-120">Standaard wordt automatisch een overeenkomende beleid gemaakt voor failback.</span><span class="sxs-lookup"><span data-stu-id="7c546-120">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="7c546-121">Bijvoorbeeld, als hello replicatiebeleid is **rep beleid** wordt beleid voor failback Hallo **rep-beleid-failback**.</span><span class="sxs-lookup"><span data-stu-id="7c546-121">For example, if hello replication policy is **rep-policy** then hello failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="7c546-122">Dit beleid wordt niet gebruikt, totdat u een failback vanuit Azure initiëren.</span><span class="sxs-lookup"><span data-stu-id="7c546-122">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c546-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7c546-123">Next steps</span></span>

<span data-ttu-id="7c546-124">Ga te[stap 10: Hallo Mobility-service installeren](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="7c546-124">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>
