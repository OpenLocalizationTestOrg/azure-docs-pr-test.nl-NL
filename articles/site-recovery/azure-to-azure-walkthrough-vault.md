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
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a>Stap 4: Een kluis voor Azure tooAzure replicatie instellen

Na [netwerken plannen](azure-to-azure-walkthrough-network.md), gebruik dit artikel tooset van een kluis, voor Azure virtual machines (VM's) repliceren tooanother Azure-regio met Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.

- Wanneer u klaar bent met Hallo artikel, moet u een Recovery Services-kluis instellen hebben.
- Eventuele opmerkingen onder Hallo van dit artikel plaatsen of vragen in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



>[!NOTE]
>
> Replicatie van Azure VM is momenteel in preview.




## <a name="create-a-vault"></a>Een kluis maken

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> U wordt aangeraden dat u Hallo Recovery Services-kluis maken in Hallo-locatie waar u uw virtuele machines tooreplicate. Bijvoorbeeld, als uw target-locatie wordt centraal ons hello, Hallo kluis in maken **VS-midden**.


## <a name="next-steps"></a>Volgende stappen

Ga te[stap 5: replicatie inschakelen](azure-to-azure-walkthrough-enable-replication.md)
