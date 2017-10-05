---
title: Een kluis voor Hyper-V-replicatie naar een secundaire site maken met Azure Site Recovery | Microsoft Docs
description: Beschrijft hoe een kluis maken bij het Hyper-V-machines repliceren naar een secundaire site van System Center VMM met Azure Site Recovery.
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
ms.openlocfilehash: 28cfcf12b2e369f96664c163c0b6f2aa8a6ddcb9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-to-a-secondary-site"></a><span data-ttu-id="fc4fb-103">Stap 5: Een kluis voor Hyper-V-replicatie naar een secundaire site maken</span><span class="sxs-lookup"><span data-stu-id="fc4fb-103">Step 5: Create a vault for Hyper-V replication to a secondary site</span></span>

<span data-ttu-id="fc4fb-104">Na het voorbereiden van de lokale [System Center Virtual Machine Manager (VMM)-servers en Hyper-V-hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) voor Hyper-V-replicatie in een secundaire site met [Azure Site Recovery](site-recovery-overview.md), kunt u een Recovery Services-kluis en selecteer het replicatiescenario voor.</span><span class="sxs-lookup"><span data-stu-id="fc4fb-104">After preparing on-premises [System Center Virtual Machine Manager (VMM) servers and Hyper-V hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) for Hyper-V replication to a secondary site using [Azure Site Recovery](site-recovery-overview.md), you can create a Recovery Services vault, and select the replication scenario.</span></span>

<span data-ttu-id="fc4fb-105">Na het lezen van dit artikel kunt u onder aan dit artikel of op het [Azure Recovery Services-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) opmerkingen of vragen plaatsen.</span><span class="sxs-lookup"><span data-stu-id="fc4fb-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="fc4fb-106">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="fc4fb-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a><span data-ttu-id="fc4fb-107">Kies een beveiligingsdoel</span><span class="sxs-lookup"><span data-stu-id="fc4fb-107">Choose a protection goal</span></span>

<span data-ttu-id="fc4fb-108">Selecteer wat u wilt repliceren en waar u naar wilt repliceren.</span><span class="sxs-lookup"><span data-stu-id="fc4fb-108">Select what you want to replicate and where you want to replicate to.</span></span>

1. <span data-ttu-id="fc4fb-109">Klik op **siteherstel** > **stap 1: infrastructuur voorbereiden** > **beveiligingsdoel**.</span><span class="sxs-lookup"><span data-stu-id="fc4fb-109">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>
2. <span data-ttu-id="fc4fb-110">Selecteer **met site recovery**, en selecteer **Ja, met Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="fc4fb-110">Select **To recovery site**, and select **Yes, with Hyper-V**.</span></span>
3. <span data-ttu-id="fc4fb-111">Selecteer **Ja** om aan te geven u VMM voor het beheren van Hyper-V-hosts.</span><span class="sxs-lookup"><span data-stu-id="fc4fb-111">Select **Yes** to indicate you're using VMM to manage the Hyper-V hosts.</span></span>
4. <span data-ttu-id="fc4fb-112">Selecteer **Ja** hebt u een secundaire VMM-server.</span><span class="sxs-lookup"><span data-stu-id="fc4fb-112">Select **Yes** if you have a secondary VMM server.</span></span> <span data-ttu-id="fc4fb-113">Als u replicatie tussen clouds op één VMM-server implementeert, klikt u op **Nee**.</span><span class="sxs-lookup"><span data-stu-id="fc4fb-113">If you're deploying replication between clouds on a single VMM server, click **No**.</span></span> <span data-ttu-id="fc4fb-114">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="fc4fb-114">Then click **OK**.</span></span>

    ![Doelstellingen kiezen](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="fc4fb-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fc4fb-116">Next steps</span></span>

<span data-ttu-id="fc4fb-117">Ga naar [stap 6: instellen van de replicatiebron en de doelserver](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="fc4fb-117">Go to [Step 6: Set up the replication source and target](vmm-to-vmm-walkthrough-source-target.md).</span></span>