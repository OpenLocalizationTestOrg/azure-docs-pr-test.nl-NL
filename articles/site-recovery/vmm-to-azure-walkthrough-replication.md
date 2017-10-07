---
title: aaaSet van een beleid voor wachtwoordreplicatie voor Hyper-V-machine (met VMM) replicatie tooAzure met Azure Site Recovery | Microsoft Docs
description: Hierin wordt beschreven hoe tooset van een beleid voor wachtwoordreplicatie voor Hyper-V-machine (met VMM) replicatie tooAzure met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a>Stap 10: Een replicatiebeleid voor virtuele machine van Hyper-V-replicatie (met VMM) tooAzure instellen


Na het instellen van [netwerktoewijzing](vmm-to-azure-walkthrough-network-mapping.md), gebruik dit artikel tooconfigure een beleid voor wachtwoordreplicatie T\tooreplicate lokale Hyper-V virtuele machines die worden beheerd in System Center Virtual Machine Manager (VMM) clouds tooAzure, met behulp van Hallo [ Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.

Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="create-a-policy"></a>Een beleid maken

1. toocreate een nieuw replicatiebeleid, klikt u op **infrastructuur voorbereiden** > **replicatie-instellingen** > **+ maken en koppelen**.

    ![Netwerk](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. Geef in **Beleid maken en koppelen** een beleidsnaam op.
3. In **Kopieerfrequentie**, geef aan hoe vaak u tooreplicate deltagegevens na de initiële replicatie van hello (elke 30 seconden, 5 of 15 minuten).

    > [!NOTE]
    >  Een 30 tweede frequentie wordt niet ondersteund bij het repliceren van toopremium opslag. Hallo-beperking wordt bepaald door Hallo aantal momentopnamen per blob (100) wordt ondersteund door de premium-opslag. [Meer informatie](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. In **herstel bewaarperiode**, in uren opgeven hoe lang de retentieperiode Hallo wordt worden voor elk herstelpunt. Beveiligde machines kunnen worden hersteld tooany punt in een venster.
5. Geef in **Frequentie van de app-consistente momentopname** op hoe vaak (elke 1-12 uur) er herstelpunten moeten worden gemaakt met toepassingsconsistente momentopnamen. Hyper-V gebruikt twee soorten momentopnamen: standaardmomentopnamen waarmee een incrementele momentopname van Hallo volledige virtuele machine en een toepassingsconsistente momentopnamen waarmee een momentopname van een punt in tijd van de toepassingsgegevens Hallo in Hallo virtuele machine. Toepassingsconsistente momentopnamen gebruiken Volume Shadow Copy Service (VSS) tooensure die toepassingen zich in een consistente status wanneer Hallo momentopname wordt gemaakt. Houd er rekening mee dat als u toepassingsconsistente momentopnamen inschakelt, het invloed is op Hallo prestaties van toepassingen die worden uitgevoerd op virtuele machines die bron. Zorg ervoor dat Hallo-waarde lager dan Hallo aantal aanvullende herstelpunten dat u configureert.
6. In **begintijd initiële replicatie**, geven wanneer toostart Hallo initiële replicatie. Hallo replicatie vindt plaats via uw internetbandbreedte zodat tooschedule kunt u deze buiten de drukste tijden.
7. In **versleutelen van gegevens die zijn opgeslagen in Azure**, opgeven of tooencrypt op rest-gegevens in Azure storage. Klik vervolgens op **OK**.

    ![Beleid voor replicatie](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. Wanneer u een nieuw beleid maakt is deze automatisch gekoppeld aan Hallo VMM-cloud. Klik op **OK**. U kunt aanvullende VMM-clouds (en Hallo virtuele machines erin) koppelen aan dit replicatiebeleid in **replicatie** > beleidsnaam > **VMM-Cloud koppelen**.

    ![Beleid voor replicatie](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a>Volgende stappen

Ga te[stap 11: replicatie inschakelen](vmm-to-azure-walkthrough-enable-replication.md)
