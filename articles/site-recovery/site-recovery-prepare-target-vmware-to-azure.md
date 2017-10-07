---
title: Doel (VMware tooAzure) voorbereiden | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooprepare uw Azure-omgeving toostart tooAzure voor VMware-virtuele machines repliceren.
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 5975d3c122032f92f8df370ee74fa0c7012ebe2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a><span data-ttu-id="33953-103">Doel (VMware tooAzure) voorbereiden</span><span class="sxs-lookup"><span data-stu-id="33953-103">Prepare target (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="33953-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="33953-104">VMware tooAzure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="33953-105">Fysieke tooAzure</span><span class="sxs-lookup"><span data-stu-id="33953-105">Physical tooAzure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="33953-106">Dit artikel wordt beschreven hoe tooprepare uw Azure-omgeving toostart tooAzure voor VMware-virtuele machines repliceren.</span><span class="sxs-lookup"><span data-stu-id="33953-106">This article describes how tooprepare your Azure environment toostart replicating VMware virtual machines tooAzure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33953-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="33953-107">Prerequisites</span></span>

<span data-ttu-id="33953-108">Hallo artikel wordt ervan uitgegaan dat de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="33953-108">hello article assumes hello following:</span></span>
- <span data-ttu-id="33953-109">Uw virtuele VMware-machines, hebt u een Recovery Services-kluis tooprotect gemaakt.</span><span class="sxs-lookup"><span data-stu-id="33953-109">You have created a Recovery Services Vault tooprotect your VMware virtual machines.</span></span> <span data-ttu-id="33953-110">U kunt een Recovery Services-kluis maken van Hallo [Azure-portal](http://portal.azure.com "Azure-portal").</span><span class="sxs-lookup"><span data-stu-id="33953-110">You can create a Recovery Services Vault from hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="33953-111">U hebt [instellen van uw on-premises omgeving](./site-recovery-set-up-vmware-to-azure.md) tooreplicate VMware-virtuele machines tooAzure.</span><span class="sxs-lookup"><span data-stu-id="33953-111">You have [setup your on-premises environment](./site-recovery-set-up-vmware-to-azure.md) tooreplicate VMware virtual machines tooAzure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="33953-112">Doel voorbereiden</span><span class="sxs-lookup"><span data-stu-id="33953-112">Prepare target</span></span>

<span data-ttu-id="33953-113">Na het voltooien van Hallo **stap 1: Selecteer beveiligingsdoel** en **stap 2: bereid bron**, gaat u te**stap 3: doel**</span><span class="sxs-lookup"><span data-stu-id="33953-113">After completing hello **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken too**Step 3: Target**</span></span>

![Doel voorbereiden](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. <span data-ttu-id="33953-115">**Abonnement:** van Hallo vervolgkeuzemenu, selecteer Hallo abonnement dat u wilt dat tooreplicate uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="33953-115">**Subscription:** From hello drop down menu, select hello Subscription that you want tooreplicate your virtual machines to.</span></span>
2. <span data-ttu-id="33953-116">**Implementatiemodel:** Selecteer Hallo implementatiemodel (klassiek of Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="33953-116">**Deployment Model:** Select hello deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="33953-117">Op basis van Hallo implementatiemodel gekozen, wordt een validatie tooensure die u ten minste één compatibel storage-account en het virtuele netwerk in Hallo doel abonnement tooreplicate en failover uw virtuele machine hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="33953-117">Based on hello chosen deployment model, a validation is run tooensure that you have at least one compatible storage account and virtual network in hello target subscription tooreplicate and failover your virtual machine to.</span></span>

<span data-ttu-id="33953-118">Zodra het Hallo-validaties wordt voltooid, klikt u op OK toogo toohello volgende stap.</span><span class="sxs-lookup"><span data-stu-id="33953-118">Once hello validations complete successfully, click OK toogo toohello next step.</span></span>

<span data-ttu-id="33953-119">Als u geen compatibel Resource Manager-opslagaccount of virtueel netwerk hebt of tooadd meer wilt, kunt u doen door te klikken op Hallo **+ Opslagaccount** of **+ netwerk** knoppen in de rechterbovenhoek Hallo Hallo blade.</span><span class="sxs-lookup"><span data-stu-id="33953-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like tooadd more, you can do so by clicking hello **+ Storage Account** or **+ Network** buttons on hello top of hello blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33953-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="33953-120">Next steps</span></span>
<span data-ttu-id="33953-121">[Replicatie-instellingen configureren](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="33953-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
