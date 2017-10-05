---
title: Instellen van een kluis voor de virtuele machine van Azure repliction tussen regio's met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van de stappen die u nodig hebt voor het instellen van een kluis voor Azure replicatie tussen Azure-regio's met Azure Site Recovery
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
ms.openlocfilehash: e03d17992ee0b12049636e40188950bcc4a6f31e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="step-4-set-up-a-vault-for-azure-to-azure-replication"></a><span data-ttu-id="ac311-103">Stap 4: Een kluis voor replicatie van Azure naar Azure instellen</span><span class="sxs-lookup"><span data-stu-id="ac311-103">Step 4: Set up a vault for Azure to Azure replication</span></span>

<span data-ttu-id="ac311-104">Na [netwerken plannen](azure-to-azure-walkthrough-network.md), gebruik dit artikel bij het instellen van een kluis, voor Azure virtual machines (VM's) repliceren naar een andere Azure-regio, met behulp van de [Azure Site Recovery](site-recovery-overview.md) service in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ac311-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article to set up a vault, for Azure virtual machines (VMs) replicating to another Azure region, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

- <span data-ttu-id="ac311-105">Wanneer u klaar bent met het artikel, moet u een Recovery Services-kluis instellen hebben.</span><span class="sxs-lookup"><span data-stu-id="ac311-105">When you finish the article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="ac311-106">Eventuele opmerkingen kunt u onderaan dit artikel plaatsen of vragen stellen op het [Azure Recovery Services-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ac311-106">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="ac311-107">Replicatie van Azure VM is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="ac311-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="ac311-108">Een kluis maken</span><span class="sxs-lookup"><span data-stu-id="ac311-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="ac311-109">U wordt aangeraden dat u de Recovery Services-kluis in de locatie waar u uw virtuele machines maken worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="ac311-109">We recommend that you create the Recovery Services vault in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="ac311-110">Bijvoorbeeld, als uw doellocatie is de centraal VS, maken de kluis in **VS-midden**.</span><span class="sxs-lookup"><span data-stu-id="ac311-110">For example, if your target location is the central US, create the vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ac311-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ac311-111">Next steps</span></span>

<span data-ttu-id="ac311-112">Ga naar [stap 5: replicatie inschakelen](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="ac311-112">Go to [Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
