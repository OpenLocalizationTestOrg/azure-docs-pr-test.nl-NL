---
title: aaaSet van een VMware-replicatie tooAzure met Azure Site Recovery-kluis | Microsoft Docs
description: Geeft een overzicht van Hallo stappen hebt u tooset van een kluis voor VMware replicatie tooAzure met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8bce940e-f19f-4418-8360-aee7b073519a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 8a7755a6c9a3f55f241c615e425285bc4b782493
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-tooazure"></a><span data-ttu-id="e854b-103">Stap 7: Een kluis voor VMware replicatie tooAzure instellen</span><span class="sxs-lookup"><span data-stu-id="e854b-103">Step 7: Set up a vault for VMware replication tooAzure</span></span>


<span data-ttu-id="e854b-104">Dit artikel wordt beschreven hoe u tooset-up maken van een kluis en bepaal wat er tooreplicate van uw on-premises locatie, met behulp van Hallo tooAzure [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e854b-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="e854b-105">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="e854b-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="e854b-106">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="e854b-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="e854b-107">Selecteer een beveiligingsdoel</span><span class="sxs-lookup"><span data-stu-id="e854b-107">Select a protection goal</span></span>

<span data-ttu-id="e854b-108">Selecteer wat u tooreplicate, en waar u tooreplicate aan.</span><span class="sxs-lookup"><span data-stu-id="e854b-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="e854b-109">Klik op **Recovery Services-kluizen** > kluis.</span><span class="sxs-lookup"><span data-stu-id="e854b-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="e854b-110">In Hallo Resource Menu, klikt u op **siteherstel** > **infrastructuur voorbereiden** > **beveiligingsdoel**.</span><span class="sxs-lookup"><span data-stu-id="e854b-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="e854b-111">In **beveiligingsdoel**, selecteer **tooAzure** > **Ja, met VMware vSphere Hypervisor**.</span><span class="sxs-lookup"><span data-stu-id="e854b-111">In **Protection goal**, select **tooAzure** > **Yes, with VMware vSphere Hypervisor**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="e854b-112">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e854b-112">Next steps</span></span>

<span data-ttu-id="e854b-113">Ga te[stap 8: bron- en doel instellen](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="e854b-113">Go too[Step 8: Set up source and target](vmware-walkthrough-source-target.md)</span></span>
