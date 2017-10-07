---
title: een testfailover voor virtuele machine van Hyper-V-replicatie tooa secundaire site met Azure Site Recovery aaaRun | Microsoft Docs
description: Beschrijft hoe een testfailover voor virtuele machine van Hyper-V-replicatie tooa toorun secundaire System Center VMM site met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a>Stap 10: Een testfailover voor Hyper-V-replicatie tooa secundaire site uitvoeren


Nadat u replicatie voor Hyper-V virtuele machines (VM's) met inschakelen [Azure Site Recovery](site-recovery-overview.md), gebruik dit artikel toorun een testfailover. Een testfailover controleert of dat replicatie werkt, zonder enige impact op uw productieomgeving. 


Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Voordat u begint

- Wanneer u een testfailover activeren wilt, kunt u Hallo netwerk toowhich Hallo testreplica die VMS wordt verbinding gemaakt. [Meer informatie](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) over netwerkopties Hallo.
- Het is raadzaam dat u een netwerk dat u hebt geselecteerd tijdens de netwerktoewijzing niet kiezen.
- Hallo-instructies in dit artikel wordt beschreven hoe toofail via één VM. Meer informatie over [herstelplannen maken](site-recovery-create-recovery-plans.md) als u wilt dat toofail over meerdere virtuele machines samen.
- Meer informatie over [beperkingen voor testfailovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).
- Hallo IP-adres opgegeven tooa VM tijdens de testfailover is Hallo hetzelfde IP-adres dat Hallo VM ontvangt voor een geplande of niet-geplande failover (ervan uitgaande dat Hallo IP-adres beschikbaar in het testfailovernetwerk Hallo is). Als Hallo IP-adres is niet beschikbaar in het testfailovernetwerk hello, ontvangt Hallo VM een ander IP-adres dat beschikbaar is in het testfailovernetwerk Hallo.
- Als u een testfailover toodo in uw productienetwerk voor volledige validatation van end-to-end network connectivity machine wilt, houd er rekening mee dat:
    - Hallo die primaire virtuele machine moet worden afgesloten wanneer u Hallo testfailover uitvoert. Anders twee virtuele machines met dezelfde identiteit zal worden uitgevoerd in de Hallo Hallo netwerk op Hallo hetzelfde moment. 
    - Als u wijzigingen tootest virtuele machines aanbrengt, gaan deze wijzigingen verloren wanneer u opschonen Hallo failover testen. Deze wijzigingen worden niet-gerepliceerde back toohello primaire virtuele machine.
    - Testen van een een productienetwerk leidt toodowntime voor uw productie-workloads. Vraag gebruikers geen toouse Hallo app als Hallo disaster recovery inzoomen uitgevoerd wordt.  


## <a name="run-a-test-failover-for-a-vm"></a>Een testfailover uitvoeren voor een virtuele machine

1. toofail via één VM in **gerepliceerde Items**, klikt u op Hallo VM > **Testfailover**.
2. In **Testfailover**, opgeven hoe test-virtuele machines verbonden toonetworks worden na Hallo testfailover. 
3. Klik op **OK** toobegin Hallo failover. Voortgang volgen op Hallo **taken** tabblad.
5. Nadat de failover is voltooid, controleert u Hallo test start van de virtuele machines is of.
6. Wanneer u bent klaar, klikt u op **testfailover opschonen** op Hallo herstelplan.
7. In **notities**, vastleggen en opslaan van eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo. Deze stap verwijdert Hallo virtuele machines en netwerken die zijn gemaakt tijdens de testfailover.


## <a name="next-steps"></a>Volgende stappen

Nadat u Hallo-implementatie hebt getest, meer informatie over andere typen [failover](site-recovery-failover.md).
