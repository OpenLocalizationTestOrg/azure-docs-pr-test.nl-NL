---
title: aaaSet van een replicatiebeleid voor voor de fysieke server replicatie tooAzure met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen u moet tooset van een beleid voor wachtwoordreplicatie als repliceren lokale fysieke servers tooAzure opslag met hello Azure Site Recovery-service
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
ms.openlocfilehash: d6bdeeffc24ffc8eaba24311f7c76452edb65648
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-tooazure"></a>Stap 8: Een replicatiebeleid voor de fysieke server replicatie tooAzure instellen


Dit artikel wordt beschreven hoe tooset van een beleid voor wachtwoordreplicatie wanneer u Windows of Linux fysieke servers tooAzure met hello repliceert [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.


Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="configure-a-policy"></a>Een beleid configureren

1. Klik op **Site Recovery-infrastructuur** > **replicatiebeleid** > **+ replicatiebeleid**.
2. In **maken van beleid voor wachtwoordreplicatie**, een beleidsnaam opgeven.
3. In **RPO drempelwaarde**, Hallo RPO grootte opgeven. Deze waarde geeft aan hoe vaak gegevens herstelpunten worden gemaakt. Een waarschuwing wordt gegenereerd als continue replicatie deze limiet overschrijdt.
4. In **herstel bewaarperiode**, opgeven hoe lang (in uren) Hallo bewaarperiode is voor elk herstelpunt. Gerepliceerde virtuele machines kunnen worden hersteld tooany punt in een venster. Gerepliceerd toopremium opslag en 72 uur standaardopslag up too24 uren bewaren wordt ondersteund voor virtuele machines.
5. In **App-consistente momentopname frequentie**, opgeven hoe vaak (in minuten) herstelpunten met toepassingsconsistente momentopnamen worden gemaakt. Klik op **OK** toocreate Hallo beleid.

    ![Beleid voor replicatie](./media/physical-walkthrough-replication/gs-replication2.png)
8. Wanneer u een nieuw beleid maakt is deze automatisch gekoppeld aan Hallo configuratieserver. Standaard wordt automatisch een overeenkomende beleid gemaakt voor failback. Bijvoorbeeld, als hello replicatiebeleid is **rep beleid** wordt beleid voor failback Hallo **rep-beleid-failback**. Dit beleid wordt niet gebruikt, totdat u een failback vanuit Azure initiëren.

## <a name="next-steps"></a>Volgende stappen

Ga te[stap 9: Hallo Mobility-service installeren](physical-walkthrough-install-mobility.md)
