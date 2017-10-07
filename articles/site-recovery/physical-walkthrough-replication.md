---
title: aaaSet van een replicatiebeleid voor voor de fysieke server replicatie tooAzure met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen u moet tooset van een beleid voor wachtwoordreplicatie als repliceren lokale fysieke servers tooAzure opslag met hello Azure Site Recovery-service
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
ms.openlocfilehash: d6bdeeffc24ffc8eaba24311f7c76452edb65648
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-tooazure"></a><span data-ttu-id="9d044-103">Stap 8: Een replicatiebeleid voor de fysieke server replicatie tooAzure instellen</span><span class="sxs-lookup"><span data-stu-id="9d044-103">Step 8: Set up a replication policy for physical server replication tooAzure</span></span>


<span data-ttu-id="9d044-104">Dit artikel wordt beschreven hoe tooset van een beleid voor wachtwoordreplicatie wanneer u Windows of Linux fysieke servers tooAzure met hello repliceert [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9d044-104">This article describes how tooset up a replication policy when you're replicating Windows/Linux physical servers tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="9d044-105">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="9d044-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="9d044-106">Een beleid configureren</span><span class="sxs-lookup"><span data-stu-id="9d044-106">Configure a policy</span></span>

1. <span data-ttu-id="9d044-107">Klik op **Site Recovery-infrastructuur** > **replicatiebeleid** > **+ replicatiebeleid**.</span><span class="sxs-lookup"><span data-stu-id="9d044-107">Click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="9d044-108">In **maken van beleid voor wachtwoordreplicatie**, een beleidsnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="9d044-108">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="9d044-109">In **RPO drempelwaarde**, Hallo RPO grootte opgeven.</span><span class="sxs-lookup"><span data-stu-id="9d044-109">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="9d044-110">Deze waarde geeft aan hoe vaak gegevens herstelpunten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9d044-110">This value indicates how often data recovery points are created.</span></span> <span data-ttu-id="9d044-111">Een waarschuwing wordt gegenereerd als continue replicatie deze limiet overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="9d044-111">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="9d044-112">In **herstel bewaarperiode**, opgeven hoe lang (in uren) Hallo bewaarperiode is voor elk herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="9d044-112">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="9d044-113">Gerepliceerde virtuele machines kunnen worden hersteld tooany punt in een venster.</span><span class="sxs-lookup"><span data-stu-id="9d044-113">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="9d044-114">Gerepliceerd toopremium opslag en 72 uur standaardopslag up too24 uren bewaren wordt ondersteund voor virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="9d044-114">Up too24 hours retention is supported for machines replicated toopremium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="9d044-115">In **App-consistente momentopname frequentie**, opgeven hoe vaak (in minuten) herstelpunten met toepassingsconsistente momentopnamen worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9d044-115">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="9d044-116">Klik op **OK** toocreate Hallo beleid.</span><span class="sxs-lookup"><span data-stu-id="9d044-116">Click **OK** toocreate hello policy.</span></span>

    ![Beleid voor replicatie](./media/physical-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="9d044-118">Wanneer u een nieuw beleid maakt is deze automatisch gekoppeld aan Hallo configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="9d044-118">When you create a new policy it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="9d044-119">Standaard wordt automatisch een overeenkomende beleid gemaakt voor failback.</span><span class="sxs-lookup"><span data-stu-id="9d044-119">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="9d044-120">Bijvoorbeeld, als hello replicatiebeleid is **rep beleid** wordt beleid voor failback Hallo **rep-beleid-failback**.</span><span class="sxs-lookup"><span data-stu-id="9d044-120">For example, if hello replication policy is **rep-policy** then hello failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="9d044-121">Dit beleid wordt niet gebruikt, totdat u een failback vanuit Azure initiëren.</span><span class="sxs-lookup"><span data-stu-id="9d044-121">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d044-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9d044-122">Next steps</span></span>

<span data-ttu-id="9d044-123">Ga te[stap 9: Hallo Mobility-service installeren](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="9d044-123">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>
