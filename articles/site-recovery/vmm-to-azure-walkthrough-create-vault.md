---
title: aaaSet van een Hyper-V-replicatie (met System Center VMM) tooAzure met Azure Site Recovery-kluis | Microsoft Docs
description: Geeft een overzicht van Hallo stappen hebt u tooset van een kluis voor Hyper-V-replicatie (met VMM) tooAzure met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: b3cd6f03-c33c-406d-91d4-5cba69f79abd
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: f2c90f3c8b0a48db1e57fefd9829d29cffff8d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="9f104-103">Stap 7: Een kluis voor Hyper-V-replicatie instellen</span><span class="sxs-lookup"><span data-stu-id="9f104-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="9f104-104">Dit artikel wordt beschreven hoe u tooset-up maken van een kluis en bepaal wat er tooreplicate van uw on-premises locatie, met behulp van Hallo tooAzure [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9f104-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="9f104-105">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="9f104-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="9f104-106">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="9f104-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="9f104-107">Selecteer een beveiligingsdoel</span><span class="sxs-lookup"><span data-stu-id="9f104-107">Select a protection goal</span></span>

<span data-ttu-id="9f104-108">Selecteer wat u tooreplicate, en waar u tooreplicate aan.</span><span class="sxs-lookup"><span data-stu-id="9f104-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="9f104-109">Klik op **Recovery Services-kluizen** > kluis.</span><span class="sxs-lookup"><span data-stu-id="9f104-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="9f104-110">In Hallo Resource Menu, klikt u op **siteherstel** > **infrastructuur voorbereiden** > **beveiligingsdoel**.</span><span class="sxs-lookup"><span data-stu-id="9f104-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="9f104-111">In **beveiligingsdoel**, selecteer **tooAzure** > **Ja, met Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="9f104-111">In **Protection goal**, select **tooAzure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="9f104-112">Selecteer **Ja** tooconfirm je nSolutions VMM.</span><span class="sxs-lookup"><span data-stu-id="9f104-112">Select **Yes** tooconfirm you're nusing VMM.</span></span> 

     ![Doelstellingen kiezen](./media/vmm-to-azure-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="9f104-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9f104-114">Next steps</span></span>

<span data-ttu-id="9f104-115">Ga te[stap 8: bron- en doel instellen](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="9f104-115">Go too[Step 8: Set up source and target](vmm-to-azure-walkthrough-source-target.md)</span></span>
