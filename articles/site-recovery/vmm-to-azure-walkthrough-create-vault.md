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
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a>Stap 7: Een kluis voor Hyper-V-replicatie instellen

Dit artikel wordt beschreven hoe u tooset-up maken van een kluis en bepaal wat er tooreplicate van uw on-premises locatie, met behulp van Hallo tooAzure [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.


Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="create-a-recovery-services-vault"></a>Een Recovery Services-kluis maken

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a>Selecteer een beveiligingsdoel

Selecteer wat u tooreplicate, en waar u tooreplicate aan.

1. Klik op **Recovery Services-kluizen** > kluis.
2. In Hallo Resource Menu, klikt u op **siteherstel** > **infrastructuur voorbereiden** > **beveiligingsdoel**.
3. In **beveiligingsdoel**, selecteer **tooAzure** > **Ja, met Hyper-V**. Selecteer **Ja** tooconfirm je nSolutions VMM. 

     ![Doelstellingen kiezen](./media/vmm-to-azure-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a>Volgende stappen

Ga te[stap 8: bron- en doel instellen](vmm-to-azure-walkthrough-source-target.md)
