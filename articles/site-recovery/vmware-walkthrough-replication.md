---
title: aaaSet van een replicatiebeleid voor voor VMware VM replicatie tooAzure met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen u moet tooset van een beleid voor wachtwoordreplicatie bij het repliceren van virtuele VMware-machines tooAzure opslag
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 12870f3f98a4dd412221b817581403cd4bf7a76d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-tooazure"></a>Stap 9: Een replicatiebeleid voor VMware VM replicatie tooAzure instellen


Dit artikel wordt beschreven hoe tooset van een beleid voor wachtwoordreplicatie wanneer u virtuele VMware-machines tooAzure met hello repliceert [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.


Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="configure-a-policy"></a>Een beleid configureren

Haal een snel overzicht van de video voordat u begint:
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate een nieuw replicatiebeleid, klikt u op **Site Recovery-infrastructuur** > **replicatiebeleid** > **+ replicatiebeleid**.
2. In **maken van beleid voor wachtwoordreplicatie**, een beleidsnaam opgeven.
3. In **RPO drempelwaarde**, Hallo RPO grootte opgeven. Deze waarde geeft aan hoe vaak gegevens herstelpunten worden gemaakt. Een waarschuwing wordt gegenereerd als continue replicatie deze limiet overschrijdt.
4. In **herstel bewaarperiode**, opgeven hoe lang (in uren) Hallo bewaarperiode is voor elk herstelpunt. Gerepliceerde virtuele machines kunnen worden hersteld tooany punt in een venster. Gerepliceerd toopremium opslag en 72 uur standaardopslag up too24 uren bewaren wordt ondersteund voor virtuele machines.
5. In **App-consistente momentopname frequentie**, opgeven hoe vaak (in minuten) herstelpunten met toepassingsconsistente momentopnamen worden gemaakt. Klik op **OK** toocreate Hallo beleid.

    ![Beleid voor replicatie](./media/vmware-walkthrough-replication/gs-replication2.png)
8. Wanneer u een nieuw beleid maakt is deze automatisch gekoppeld aan Hallo configuratieserver. Standaard wordt automatisch een overeenkomende beleid gemaakt voor failback. Bijvoorbeeld, als hello replicatiebeleid is **rep beleid** wordt beleid voor failback Hallo **rep-beleid-failback**. Dit beleid wordt niet gebruikt, totdat u een failback vanuit Azure initiëren.

## <a name="next-steps"></a>Volgende stappen

Ga te[stap 10: Hallo Mobility-service installeren](vmware-walkthrough-install-mobility.md)
