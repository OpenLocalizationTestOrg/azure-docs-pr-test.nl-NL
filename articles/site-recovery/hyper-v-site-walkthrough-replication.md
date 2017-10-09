---
title: aaaSet van een replicatiebeleid voor voor virtuele machine van Hyper-V-replicatie (zonder de System Center VMM) tooAzure met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen u moet tooset van een beleid voor wachtwoordreplicatie bij het repliceren van Hyper-V-machines tooAzure opslag
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a>Stap 9: Een replicatiebeleid voor virtuele machine van Hyper-V-replicatie tooAzure instellen

Dit artikel wordt beschreven hoe tooset van een beleid voor wachtwoordreplicatie wanneer u tooAzure van de Hyper-V-machines (zonder de System Center VMM repliceert) met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.


Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="about-snapshots"></a>Over momentopnamen

Hyper-V gebruikt twee soorten momentopnamen: standaardmomentopnamen waarmee een incrementele momentopname van Hallo volledige virtuele machine en een toepassingsconsistente momentopnamen waarmee een momentopname van een punt in tijd van de toepassingsgegevens Hallo in Hallo virtuele machine.
    - Toepassingsconsistente momentopnamen gebruiken Volume Shadow Copy Service (VSS) tooensure die toepassingen zich in een consistente status wanneer Hallo momentopname wordt gemaakt.
    - Als u toepassingsconsistente momentopnamen inschakelt, wordt het Hallo-prestaties van toepassingen die worden uitgevoerd op virtuele bronmachines beïnvloeden. Zorg ervoor dat Hallo-waarde lager dan Hallo aantal aanvullende herstelpunten dat u configureert.

## <a name="set-up-a-replication-policy"></a>Instellen van een beleid voor wachtwoordreplicatie

1. toocreate een nieuw replicatiebeleid, klikt u op **infrastructuur voorbereiden** > **replicatie-instellingen** > **+ maken en koppelen**.

    ![Netwerk](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. Geef in **Beleid maken en koppelen** een beleidsnaam op.
3. In **Kopieerfrequentie**, geef aan hoe vaak u tooreplicate deltagegevens na de initiële replicatie van hello (elke 30 seconden, 5 of 15 minuten).

    > [!NOTE]
    > Een 30 tweede frequentie wordt niet ondersteund bij het repliceren van toopremium opslag. Hallo-beperking wordt bepaald door Hallo aantal momentopnamen per blob (100) wordt ondersteund door de premium-opslag. [Meer informatie](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).

4. In **herstel bewaarperiode**, geeft u in hoe lang uren Hallo bewaarperiode is voor elk herstelpunt. Virtuele machines kunnen worden hersteld tooany punt in een venster.
5. In **App-consistente momentopname frequentie**, opgeven hoe vaak (1-12 uur) herstelpunten met toepassingsconsistente momentopnamen worden gemaakt.
6. In **begintijd initiële replicatie**, opgeven wanneer toostart Hallo initiële replicatie. Hallo replicatie vindt plaats via uw internetbandbreedte zodat tooschedule kunt u deze buiten de drukste tijden. Klik vervolgens op **OK**.

    ![Beleid voor replicatie](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

Wanneer u een nieuw beleid maakt, wordt dit automatisch gekoppeld met de Hallo Hyper-V-site. U kunt een Hyper-V-site (en Hallo virtuele machines erin) koppelen aan meerdere beleidsregels voor replicatie in **replicatie** > beleidsnaam > **Hyper-V-Site koppelen**.



## <a name="next-steps"></a>Volgende stappen

Ga te[stap 10: replicatie inschakelen](hyper-v-site-walkthrough-enable-replication.md)
