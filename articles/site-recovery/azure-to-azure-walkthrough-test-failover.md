---
title: een testfailover voor replicatie van de virtuele machine van Azure met Azure Site Recovery aaaRun | Microsoft Docs
description: Geeft een overzicht van Hallo stappen die u nodig hebt voor het uitvoeren van een testfailover voor virtuele Azure-machines repliceren tooanother Azure-regio met behulp van hello Azure Site Recovery-service.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: e15c1b0c-5d75-4fdf-acb0-e61def9e9339
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: c1f765aa94c59dd70b33317ebbcd04beb7977969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a>Stap 6: Een testfailover voor replicatie van de virtuele machine in Azure uitvoeren

Nadat u replicatie voor virtuele Azure-machine (VM's) hebt ingeschakeld, voert u de stappen in dit artikel, toorun testfailover van een Azure-regio tooanother, met behulp van Hallo Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.

- Wanneer u klaar bent met Hallo artikel, moet met een testfailover hebt gecontroleerd dat ten minste één virtuele machine van Azure kunt Failover-overschakeling tooyour secundaire Azure-regio. 
- Eventuele opmerkingen onder Hallo van dit artikel plaatsen of vragen in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> Replicatie van Azure VM is momenteel in preview.


## <a name="before-you-start"></a>Voordat u begint

- Voordat u een failovertest uitvoert, wordt aangeraden Hallo VM-eigenschappen controleren en eventuele wijzigingen die u wilt maken. U toegang hebt tot Hallo VM-eigenschappen in **gerepliceerde items**. Hallo **Essentials** blade ziet u informatie over machines instellingen en status.
- Het is raadzaam u een afzonderlijk Azure VM-netwerk gebruiken voor testfailover hello en niet Hallo-netwerk (standaard of aangepast) die is geconfigureerd voor failover voor productie.
- Hallo test failover mislukt via Azure Virtual machines (en hun opslag) toohello secundaire Azure-regio. Het niet alle afhankelijke apps of resources worden gerepliceerd. Als apps worden uitgevoerd op mislukte gedurende VM's afhankelijk van andere resources, zoals Active Directory en DNS zijn, moet u tooreplicate deze ook als ze nog niet beschikbaar in uw secundaire regio. [Meer informatie](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- Als u wilt dat tooaccess virtuele machines na failover van een on-premises site gerepliceerd, moet u deze te[voorbereiden tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese virtuele machines.

## <a name="run-a-test-failover"></a>Een testfailover uitvoeren

1. In **instellingen** > **gerepliceerde Items**, klikt u op Hallo VM **+ Testfailover** pictogram. 

2. In **Testfailover**, selecteert u een herstel punt toouse voor Hallo failover:

    - **Meest recente verwerkte**: mislukt Hallo VM via toohello meest recente herstelpunt dat is verwerkt door Hallo Site Recovery-service. Hallo tijdstempel wordt weergegeven. Met deze optie geen tijd besteed aan het verwerken van gegevens, zodat het biedt een laag RTO (beoogde hersteltijd).
    - **Meest recente app-consistente**: deze optie is overgenomen van alle virtuele machines toohello laatste app-consistente herstelpunt. Hallo tijdstempel wordt weergegeven. 
    - **Aangepaste**: eender welk herstelpunt kiezen.
 
3. Selecteer Hallo doel virtuele Azure-netwerk toowhich virtuele Azure-machines in de secundaire regio Hallo moet worden verbonden, nadat Hallo failover plaatsvindt.
4. toostart Hallo failover, klikt u op **OK**. tootrack voortgang, klikt u op Hallo VM tooopen eigenschappen ervan. U kunt ook op Hallo **Testfailover** taak in de kluisnaam Hallo > **instellingen** > **taken** > **Site Recovery-taken**.
5. Na het Hallo failover is voltooid, Hallo replica virtuele machine van Azure in hello Azure-portal weergegeven > **virtuele Machines**. Zorg ervoor dat Hallo VM is de juiste grootte hello, of deze is verbonden met het juiste netwerk toohello en dat deze wordt uitgevoerd.
6. toodelete hello virtuele machines die zijn gemaakt tijdens de testfailover hello, klikt u op **testfailover opschonen** op Hallo gerepliceerd item of Hallo herstelplan. In **notities**, vastleggen en opslaan van eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo. 

[Meer informatie](site-recovery-test-failover-to-azure.md) over testfailovers.

## <a name="next-steps"></a>Volgende stappen

Nadat u de failover hebt getest, wordt in dit scenario is voltooid. Nu kunt u informatie over het uitvoeren van failovers in productie:

- [Meer informatie](site-recovery-failover.md) over verschillende soorten failovers, en hoe toorun ze.
- Meer informatie over mislukte over meerdere virtuele machines [met behulp van een herstelplan](site-recovery-create-recovery-plans.md).
- Meer informatie over [herstelplannen met](site-recovery-create-recovery-plans.md).
- Meer informatie over [andere virtuele Azure-machines](site-recovery-how-to-reprotect.md) na een failover.

