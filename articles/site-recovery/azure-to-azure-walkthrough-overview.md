---
title: aaaReplicate Azure VM's tussen Azure-regio's | Microsoft-Docs
description: Geeft een overzicht van Hallo stappen vereist tooreplicate Azure VM's tussen Azure-regio's hello Azure Site Recovery-service in hello Azure-portal
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="479e3-103">Virtuele Azure-machines repliceren tussen regio's met Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="479e3-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

><span data-ttu-id="479e3-104">Dit artikel bevat een overzicht van Hallo stappen vereist tooreplicate Azure virtuele machines (VM's) in een Azure-regio tooAzure virtuele machines in een andere regio.</span><span class="sxs-lookup"><span data-stu-id="479e3-104">This article provides an overview of hello steps required tooreplicate Azure virtual machines (VMs) in one Azure region tooAzure VMs in a different region.</span></span> 

>[!NOTE]
>
> <span data-ttu-id="479e3-105">Replicatie van Azure VM is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="479e3-105">Azure VM replication is currently in preview.</span></span>

<span data-ttu-id="479e3-106">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="479e3-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="step-1-review-architecture"></a><span data-ttu-id="479e3-107">Stap 1: Bekijk architectuur</span><span class="sxs-lookup"><span data-stu-id="479e3-107">Step 1: Review architecture</span></span>

<span data-ttu-id="479e3-108">Voordat u een implementatie, Hallo scenario-architectuur en Hallo onderdelen moet u toodeploy bekijken.</span><span class="sxs-lookup"><span data-stu-id="479e3-108">Before you start deployment, review hello scenario architecture, and hello components you need toodeploy.</span></span>

<span data-ttu-id="479e3-109">Ga te[stap 1: Bekijk Hallo-architectuur](azure-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="479e3-109">Go too[Step 1: Review hello architecture](azure-to-azure-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="479e3-110">Stap 2: Controleer vereisten</span><span class="sxs-lookup"><span data-stu-id="479e3-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="479e3-111">Controleer dat u Azure-vereisten op plaatsen, met inbegrip van een abonnement, virtuele netwerken, opslagaccounts en VM-vereisten hebben Hallo.</span><span class="sxs-lookup"><span data-stu-id="479e3-111">Check that you have hello Azure prerequisites in places, including a subscription, virtual networks, storage accounts, and VM requirements.</span></span>

<span data-ttu-id="479e3-112">Ga te[stap 2: Controleer of de vereisten en beperkingen](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="479e3-112">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>


## <a name="step-3-plan-networking"></a><span data-ttu-id="479e3-113">Stap 3: Plannen netwerken</span><span class="sxs-lookup"><span data-stu-id="479e3-113">Step 3: Plan networking</span></span>

<span data-ttu-id="479e3-114">Controleer of uitgaande verbinding is ingesteld op Azure Virtual machines die u wilt tooreplicate, en dat de verbindingen van on-premises zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="479e3-114">Check that outbound connectivity is set up on Azure VMs you want tooreplicate, and that connections from on-premises are set up.</span></span>

<span data-ttu-id="479e3-115">Ga te[stap 4: netwerken plannen](azure-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="479e3-115">Go too[Step 4: Plan networking](azure-to-azure-walkthrough-network.md)</span></span>



## <a name="step-4-create-a-vault"></a><span data-ttu-id="479e3-116">Stap 4: Een kluis maken</span><span class="sxs-lookup"><span data-stu-id="479e3-116">Step 4: Create a vault</span></span> 

<span data-ttu-id="479e3-117">U moet tooset van een Recovery Services-kluis tooorchestrate en replicatie beheren en Hallo bron regio opgeven.</span><span class="sxs-lookup"><span data-stu-id="479e3-117">You need tooset up a Recovery Services vault tooorchestrate and manage replication, and specify hello source region.</span></span>

<span data-ttu-id="479e3-118">Ga te[stap 4: een kluis maken](azure-to-azure-walkthrough-vault.md)</span><span class="sxs-lookup"><span data-stu-id="479e3-118">Go too[Step 4: Create a vault](azure-to-azure-walkthrough-vault.md)</span></span>


## <a name="step-5-enable-replication"></a><span data-ttu-id="479e3-119">Stap 5: Replicatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="479e3-119">Step 5: Enable replication</span></span>


<span data-ttu-id="479e3-120">replicatie tooenable target-locatie-instellingen configureren, instellen van een beleid voor wachtwoordreplicatie en hello Azure VM's die u tooreplicate wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="479e3-120">tooenable replication, you configure target location settings, set up a replication policy, and select hello Azure VMs that you want tooreplicate.</span></span> <span data-ttu-id="479e3-121">Na het inschakelen, initiële replicatie van Hallo VM zich voordoet.</span><span class="sxs-lookup"><span data-stu-id="479e3-121">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="479e3-122">Ga te[stap 5: replicatie inschakelen](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="479e3-122">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-6-run-a-test-failover"></a><span data-ttu-id="479e3-123">Stap 6: Een testfailover uitvoeren</span><span class="sxs-lookup"><span data-stu-id="479e3-123">Step 6: Run a test failover</span></span>

<span data-ttu-id="479e3-124">Nadat de eerste replicatie is voltooid en replicatie van verschillen wordt uitgevoerd, kunt u een test failover toomake, controleren of dat alles werkt zoals verwacht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="479e3-124">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="479e3-125">Ga te[stap 6: een testfailover uitvoeren](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="479e3-125">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>


