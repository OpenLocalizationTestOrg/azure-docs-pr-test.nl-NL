---
title: aaaSet van een Hyper-V-replicatie (zonder de System Center VMM) tooAzure met Azure Site Recovery-kluis | Microsoft Docs
description: Geeft een overzicht van Hallo stappen hebt u tooset van een kluis voor Hyper-V-replicatie tooAzure met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a936b3e2-0dbe-47ac-a98e-5285d96dc786
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: e3ef8758faab36d19d0968d98a23105bed7830f6
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
3. In **beveiligingsdoel**, selecteer **tooAzure** > **Ja, met Hyper-V**. Selecteer **Nee** tooconfirm u VMM niet gebruikt. 

    ![Doelstellingen kiezen](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a>Volgende stappen

Ga te[stap 8: bron- en doel instellen](hyper-v-site-walkthrough-source-target.md)
