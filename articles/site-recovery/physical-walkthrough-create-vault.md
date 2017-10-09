---
title: aaaSet van een fysieke server replicatie tooAzure met Azure Site Recovery-kluis | Microsoft Docs
description: Geeft een overzicht van Hallo stappen u moet tooset van een kluis tooreplicate fysieke servers tooAzure met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 988928e3ece31116823f132cc39223fe44443468
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a><span data-ttu-id="a29c0-103">Stap 6: Een kluis voor de fysieke server replicatie tooAzure instellen</span><span class="sxs-lookup"><span data-stu-id="a29c0-103">Step 6: Set up a vault for physical server replication tooAzure</span></span>


<span data-ttu-id="a29c0-104">Dit artikel wordt beschreven hoe tooset van een kluis.</span><span class="sxs-lookup"><span data-stu-id="a29c0-104">This article describes how tooset up a vault.</span></span> <span data-ttu-id="a29c0-105">Hallo-kluis maken en geef op wat u wilt tooreplicate vanuit uw lokale locatie tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a29c0-105">You create hello vault, and specify what you want tooreplicate from your on-premises location tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="a29c0-106">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a29c0-106">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="a29c0-107">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="a29c0-107">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="a29c0-108">Selecteer een beveiligingsdoel</span><span class="sxs-lookup"><span data-stu-id="a29c0-108">Select a protection goal</span></span>

<span data-ttu-id="a29c0-109">Selecteer wat u tooreplicate, en waar u tooreplicate aan.</span><span class="sxs-lookup"><span data-stu-id="a29c0-109">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="a29c0-110">Klik op **Recovery Services-kluizen** > kluis.</span><span class="sxs-lookup"><span data-stu-id="a29c0-110">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="a29c0-111">In Hallo Resource Menu, klikt u op **siteherstel** > **infrastructuur voorbereiden** > **beveiligingsdoel**.</span><span class="sxs-lookup"><span data-stu-id="a29c0-111">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="a29c0-112">In **beveiligingsdoel**, selecteer **tooAzure** > **niet gevirtualiseerde/andere**.</span><span class="sxs-lookup"><span data-stu-id="a29c0-112">In **Protection goal**, select **tooAzure** > **Not virtualized/Other**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a29c0-113">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a29c0-113">Next steps</span></span>

<span data-ttu-id="a29c0-114">Ga te[stap 7: bron- en doel instellen](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="a29c0-114">Go too[Step 7: Set up source and target](physical-walkthrough-source-target.md)</span></span>
