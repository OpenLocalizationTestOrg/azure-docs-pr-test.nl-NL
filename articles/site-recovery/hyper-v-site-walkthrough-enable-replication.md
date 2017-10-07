---
title: aaaEnable replicatie voor de Hyper-V-machines repliceren tooAzure (zonder de System Center VMM) met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen hebt u tooenable replicatie tooAzure voor Hyper-V-machines met behulp van hello Azure Site Recovery-service
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a>Stap 10: Replicatie inschakelen voor Hyper-V-machines repliceren tooAzure


Dit artikel wordt beschreven hoe tooenable replicatie voor de lokale Hyper-V virtuele machines (wordt niet beheerd door System Center VMM) tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.

Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="before-you-start"></a>Voordat u begint

Voordat u begint, zorg ervoor dat uw Azure gebruikersaccount Hallo vereist [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicatie van een nieuwe virtuele machine tooAzure.

## <a name="exclude-disks-from-replication"></a>Schijven uitsluiten van replicatie

Standaard worden alle schijven op een machine gerepliceerd. U kunt schijven uitsluiten van replicatie. Zo wilt u mogelijk niet tooreplicate schijven met tijdelijke gegevens of gegevens die telkens wanneer een machine is bijgewerkt of de toepassing opnieuw wordt gestart (bijvoorbeeld pagefile.sys of SQL Server tempdb). [Meer informatie](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a>Virtuele machines repliceren

Replicatie voor virtuele machines als volgt inschakelen:          

1. Klik op **toepassing repliceren** > **bron**. Nadat u replicatie voor Hallo eerst hebt ingesteld, klikt u op **+ repliceren** tooenable replicatie voor aanvullende machines.

    ![Replicatie inschakelen](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. In **bron**, selecteer Hallo Hyper-V-site. Klik vervolgens op **OK**.
3. In **doel**Hallo kluis abonnement en selecteer Hallo gewenste toouse in Azure (klassiek of de resource management) na een failover van failover-model.
4. Selecteer Hallo gewenste toouse storage-account. Als u een account dat u wilt dat toouse geen hebt, kunt u [maken van een](#set-up-an-azure-storage-account). Klik vervolgens op **OK**.
5. Selecteer hello Azure-netwerk en subnet toowhich virtuele Azure-machines verbinding maken wanneer ze failover worden gemaakt.

    - Selecteer tooapply Hallo instellingen tooall machines in het netwerk u inschakelen voor replicatie, **nu configureren voor geselecteerde machines**.
    - Selecteer **later configureren** tooselect hello Azure-netwerk per computer.
    - Als u een netwerk dat u wilt dat toouse geen hebt, kunt u [maken van een](#set-up-an-azure-network). Selecteer indien van toepassing een subnet. Klik vervolgens op **OK**.

   ![Replicatie inschakelen](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. In **virtuele Machines** > **virtuele machines selecteren**en klik op elke machine die u wilt dat tooreplicate selecteren. U kunt alleen machines selecteren waarvoor replicatie kan worden ingeschakeld. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. In **eigenschappen** > **eigenschappen configureren**Hallo-besturingssysteem voor virtuele machines Hallo geselecteerd en selecteer Hallo besturingssysteemschijf.
8. Controleer of deze Hallo Azure VM-naam (doelnaam) voldoet aan [vereisten van de virtuele machine van Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
9. Standaard worden alle Hallo schijven Hallo VM geselecteerd voor replicatie. Schakel schijven tooexclude ze.
10. Klik op **OK** toosave wijzigingen. Later kunt u eventueel extra eigenschappen instellen.

    ![Replicatie inschakelen](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. In **replicatie-instellingen** > **replicatie-instellingen configureren**, Hallo replicatiebeleid u tooapply voor Hallo virtuele machines beveiligde wilt selecteren. Klik vervolgens op **OK**. U kunt het replicatiebeleid Hallo in wijzigen **replicatiebeleid** > beleidsnaam > **instellingen bewerken**. De wijzigingen die u toepast, worden zowel gebruikt voor machines die al worden gerepliceerd, als voor nieuwe machines.


   ![Replicatie inschakelen](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

U kunt de voortgang van Hallo volgen **beveiliging inschakelen** taak **taken** > **Site Recovery-taken**. Na het Hallo **beveiliging voltooien** taak wordt uitgevoerd Hallo machine is gereed voor failover.


## <a name="next-steps"></a>Volgende stappen


Ga te[stap 11: een testfailover uitvoeren](hyper-v-site-walkthrough-test-failover.md)
