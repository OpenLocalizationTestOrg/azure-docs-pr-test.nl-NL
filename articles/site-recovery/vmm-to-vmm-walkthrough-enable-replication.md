---
title: aaaEnable Hyper-V-replicatie tooa secundaire site met Azure Site Recovery | Microsoft Docs
description: Hierin wordt beschreven hoe tooenable replicatie voor de Hyper-V-machines repliceren tooa secundaire System Center VMM site met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a>Stap 9: Replicatie tooa secundaire site inschakelen voor Hyper-V virtuele machines


Na het instellen van een beleid voor wachtwoordreplicatie, kunt u deze site artikel tooenable replicatie tooa secundaire System Center Virtual Machine Manager (VMM) gebruiken voor on-premises Hyper-V virtuele machines (VM), met behulp van [Azure Site Recovery](site-recovery-overview.md).

Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="select-vms-tooreplicate"></a>Virtuele machines tooreplicate selecteren

1. Klik op **Stap 2: toepassing repliceren** > **Bron**. 

    ![Replicatie inschakelen](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. In **bron**Hallo VMM-server en selecteer Hallo cloud in welke Hallo gewenste tooreplicate van Hyper-V-hosts zich bevinden. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. In **doel**, controleert u of Hallo secundaire VMM-server en de cloud.
4. In **virtuele machines**, Hallo virtuele machines die u wilt dat tooprotect uit Hallo lijst selecteren.

    ![Beveiliging van de virtuele machine inschakelen](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

U kunt de voortgang van Hallo volgen **beveiliging inschakelen** actie in **taken** > **Site Recovery-taken**. Na het Hallo **beveiliging voltooien** taak is voltooid, Hallo initiële replicatie is voltooid en Hallo virtuele machine is gereed voor failover.

Opmerking:

- U kunt ook beveiliging voor virtuele machines in Hallo VMM-console inschakelen. Klik op **beveiliging inschakelen** op Hallo werkbalk in de eigenschappen van de virtuele machine Hallo > **Azure Site Recovery** tabblad.
- Nadat u replicatie hebt ingeschakeld, kunt u de eigenschappen voor Hallo VM weergeven in **gerepliceerde Items**. Op Hallo **Essentials** dashboard ziet u informatie over het replicatiebeleid Hallo voor Hallo VM en de status ervan. Klik op **eigenschappen** voor meer informatie.

## <a name="onboard-existing-vms"></a>Ingebouwde bestaande virtuele machines

Als u een bestaande virtuele machines in VMM die worden gerepliceerd met Hyper-V Replica hebt, kunt u vrijgeven ze voor Azure Site Recovery replicatie als volgt:

1. Zorg dat Hallo Hyper-V-hostserver Hallo bestaande virtuele machine bevindt zich in de primaire cloud Hallo en die Hallo Hyper-V-server die als host fungeert voor Hallo replica virtuele machine bevindt zich in Hallo secundaire cloud.
2. Zorg ervoor dat een beleid voor wachtwoordreplicatie is geconfigureerd voor Hallo primaire VMM-cloud.
3. Replicatie inschakelen voor Hallo primaire virtuele machine. Azure Site Recovery en VMM ervoor te zorgen dat hello dezelfde replicatiehost en virtuele machine wordt gedetecteerd, en Azure Site Recovery opnieuw wilt gebruiken en om opnieuw replicatie met Hallo instellingen opgegeven.


## <a name="next-steps"></a>Volgende stappen

Ga te[stap 10: een testfailover uitvoeren](vmm-to-vmm-walkthrough-test-failover.md).
