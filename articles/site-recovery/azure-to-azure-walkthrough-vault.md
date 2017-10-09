---
title: aaaSet van een kluis voor de virtuele machine van Azure repliction tussen regio's met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen moet u tooset van een kluis voor Azure replicatie tussen Azure-regio's met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a><span data-ttu-id="65f14-103">Stap 4: Een kluis voor Azure tooAzure replicatie instellen</span><span class="sxs-lookup"><span data-stu-id="65f14-103">Step 4: Set up a vault for Azure tooAzure replication</span></span>

<span data-ttu-id="65f14-104">Na [netwerken plannen](azure-to-azure-walkthrough-network.md), gebruik dit artikel tooset van een kluis, voor Azure virtual machines (VM's) repliceren tooanother Azure-regio met Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="65f14-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article tooset up a vault, for Azure virtual machines (VMs) replicating tooanother Azure region, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

- <span data-ttu-id="65f14-105">Wanneer u klaar bent met Hallo artikel, moet u een Recovery Services-kluis instellen hebben.</span><span class="sxs-lookup"><span data-stu-id="65f14-105">When you finish hello article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="65f14-106">Eventuele opmerkingen onder Hallo van dit artikel plaatsen of vragen in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="65f14-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="65f14-107">Replicatie van Azure VM is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="65f14-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="65f14-108">Een kluis maken</span><span class="sxs-lookup"><span data-stu-id="65f14-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="65f14-109">U wordt aangeraden dat u Hallo Recovery Services-kluis maken in Hallo-locatie waar u uw virtuele machines tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="65f14-109">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="65f14-110">Bijvoorbeeld, als uw target-locatie wordt centraal ons hello, Hallo kluis in maken **VS-midden**.</span><span class="sxs-lookup"><span data-stu-id="65f14-110">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="65f14-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="65f14-111">Next steps</span></span>

<span data-ttu-id="65f14-112">Ga te[stap 5: replicatie inschakelen](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="65f14-112">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
