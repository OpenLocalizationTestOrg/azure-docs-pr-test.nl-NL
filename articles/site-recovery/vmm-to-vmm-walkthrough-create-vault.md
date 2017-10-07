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
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a>Stap 5: Een kluis voor Hyper-V-replicatie tooa secundaire site maken

Na het voorbereiden van de lokale [System Center Virtual Machine Manager (VMM)-servers en Hyper-V-hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) voor het gebruik van Hyper-V-replicatie tooa secundaire site [Azure Site Recovery](site-recovery-overview.md), kunt u een Recovery Services-kluis en selecteer Hallo replicatiescenario.

Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="create-a-recovery-services-vault"></a>Een Recovery Services-kluis maken

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a>Kies een beveiligingsdoel

Selecteer wat u wilt dat tooreplicate en waar u tooreplicate aan.

1. Klik op **siteherstel** > **stap 1: infrastructuur voorbereiden** > **beveiligingsdoel**.
2. Selecteer **toorecovery site**, en selecteer **Ja, met Hyper-V**.
3. Selecteer **Ja** tooindicate u VMM toomanage Hallo Hyper-V-hosts.
4. Selecteer **Ja** hebt u een secundaire VMM-server. Als u replicatie tussen clouds op één VMM-server implementeert, klikt u op **Nee**. Klik vervolgens op **OK**.

    ![Doelstellingen kiezen](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a>Volgende stappen

Ga te[stap 6: Hallo replicatiebron en doel instellen](vmm-to-vmm-walkthrough-source-target.md).
