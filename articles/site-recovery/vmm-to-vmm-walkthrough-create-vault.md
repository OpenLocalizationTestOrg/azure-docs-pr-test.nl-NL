---
title: een Hyper-V-replicatie tooa secundaire site met Azure Site Recovery-kluis aaaCreate | Microsoft Docs
description: Beschrijft hoe een kluis bij het repliceren van Hyper-V-machines tooa toocreate secundaire System Center VMM site met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ff65dbfb-cb26-410e-ab48-76971625db08
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 96ee09cbf2376a5089b9efa09dc7ab3fb7d472cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="31652-103">Stap 5: Een kluis voor Hyper-V-replicatie tooa secundaire site maken</span><span class="sxs-lookup"><span data-stu-id="31652-103">Step 5: Create a vault for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="31652-104">Na het voorbereiden van de lokale [System Center Virtual Machine Manager (VMM)-servers en Hyper-V-hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) voor het gebruik van Hyper-V-replicatie tooa secundaire site [Azure Site Recovery](site-recovery-overview.md), kunt u een Recovery Services-kluis en selecteer Hallo replicatiescenario.</span><span class="sxs-lookup"><span data-stu-id="31652-104">After preparing on-premises [System Center Virtual Machine Manager (VMM) servers and Hyper-V hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) for Hyper-V replication tooa secondary site using [Azure Site Recovery](site-recovery-overview.md), you can create a Recovery Services vault, and select hello replication scenario.</span></span>

<span data-ttu-id="31652-105">Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="31652-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="31652-106">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="31652-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a><span data-ttu-id="31652-107">Kies een beveiligingsdoel</span><span class="sxs-lookup"><span data-stu-id="31652-107">Choose a protection goal</span></span>

<span data-ttu-id="31652-108">Selecteer wat u wilt dat tooreplicate en waar u tooreplicate aan.</span><span class="sxs-lookup"><span data-stu-id="31652-108">Select what you want tooreplicate and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="31652-109">Klik op **siteherstel** > **stap 1: infrastructuur voorbereiden** > **beveiligingsdoel**.</span><span class="sxs-lookup"><span data-stu-id="31652-109">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>
2. <span data-ttu-id="31652-110">Selecteer **toorecovery site**, en selecteer **Ja, met Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="31652-110">Select **toorecovery site**, and select **Yes, with Hyper-V**.</span></span>
3. <span data-ttu-id="31652-111">Selecteer **Ja** tooindicate u VMM toomanage Hallo Hyper-V-hosts.</span><span class="sxs-lookup"><span data-stu-id="31652-111">Select **Yes** tooindicate you're using VMM toomanage hello Hyper-V hosts.</span></span>
4. <span data-ttu-id="31652-112">Selecteer **Ja** hebt u een secundaire VMM-server.</span><span class="sxs-lookup"><span data-stu-id="31652-112">Select **Yes** if you have a secondary VMM server.</span></span> <span data-ttu-id="31652-113">Als u replicatie tussen clouds op één VMM-server implementeert, klikt u op **Nee**.</span><span class="sxs-lookup"><span data-stu-id="31652-113">If you're deploying replication between clouds on a single VMM server, click **No**.</span></span> <span data-ttu-id="31652-114">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="31652-114">Then click **OK**.</span></span>

    ![Doelstellingen kiezen](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="31652-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="31652-116">Next steps</span></span>

<span data-ttu-id="31652-117">Ga te[stap 6: Hallo replicatiebron en doel instellen](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="31652-117">Go too[Step 6: Set up hello replication source and target](vmm-to-vmm-walkthrough-source-target.md).</span></span>
