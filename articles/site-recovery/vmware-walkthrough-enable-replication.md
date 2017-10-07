---
title: aaaEnable replicatie voor virtuele VMware-machines repliceren tooAzure met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen hebt u tooenable replicatie tooAzure voor virtuele VMware-machines met behulp van hello Azure Site Recovery-service
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 490782bbbfa3dd92c626d3985c75d771df53d566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-for-vmware-virtual-machines-tooazure"></a>Stap 11: Replicatie inschakelen voor tooAzure voor VMware-virtuele machines


Dit artikel wordt beschreven hoe tooenable replicatie voor de lokale VMware-virtuele machines tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.

Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Voordat u begint

- Virtuele VMware-machines moeten Hallo [Mobility-service zijn geïnstalleerd](vmware-walkthrough-install-mobility.md). -Als een virtuele machine is voorbereid voor de push-installatie, de processerver Hallo Hallo Mobility-service automatisch geïnstalleerd wanneer u replicatie inschakelt.
- Uw Azure gebruikersaccount moet specifieke [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicatie van een VM-tooAzure
- Wanneer u toevoegen of wijzigen van virtuele machines, het omhoog too15 minuten of langer kan duren voor wijzigingen tootake effect, en voor deze tooappear in Hallo-portal.
- U kunt tijd van laatste Hallo controleren voor virtuele machines in **configuratieservers** > **laatste Contact op**.
- tooadd virtuele machines zonder te wachten Hallo geplande detectie, markeer Hallo configuratieserver (Klik niet op deze), en klik op **vernieuwen**.



## <a name="exclude-disks-from-replication"></a>Schijven uitsluiten van replicatie

Standaard worden alle schijven op een machine gerepliceerd. U kunt schijven uitsluiten van replicatie. Zo wilt u mogelijk niet tooreplicate schijven met tijdelijke gegevens of gegevens die telkens wanneer een machine is bijgewerkt of de toepassing opnieuw wordt gestart (bijvoorbeeld pagefile.sys of SQL Server tempdb). [Meer informatie](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>Virtuele machines repliceren

Voordat u begint, bekijk een video-overzicht

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. Klik op **Stap 2: toepassing repliceren** > **Bron**.
2. In **bron**, selecteer Hallo configuratieserver.
3. In **type Machine**, selecteer **virtuele Machines**.
4. In **vCenter/vSphere-Hypervisor**, selecteert u Hallo vCenter-server die wordt beheerd Hallo vSphere host of selecteer Hallo host.
5. Selecteer de processerver Hallo. Dit is de configuratieserver Hallo als u geen processervers extra hebt gemaakt. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/vmware-walkthrough-enable-replication/enable-replication2.png)

6. In **doel**, selecteert u Hallo-abonnement en resourcegroep waarin u toocreate Hallo failover van virtuele machines wilt Hallo. Hallo-implementatiemodel dat u toouse in Azure (klassiek of de resource management), voor Hallo failover van virtuele machines wilt kiezen.


7. Selecteer hello Azure storage-account gewenste toouse voor het repliceren van gegevens. Als u niet dat toouse een account dat u al hebt ingesteld wilt, kunt u een nieuwe maken.

8. Selecteer hello Azure-netwerk en subnet toowhich Azure Virtual machines wordt verbinding gemaakt, wanneer ze zijn gemaakt na een failover. Selecteer **nu configureren voor geselecteerde machines**, tooapply Hallo instelling tooall machines in het netwerk u selecteert voor beveiliging. Selecteer **later configureren** tooselect hello Azure-netwerk per computer. Als u een bestaand netwerk toouse niet wilt, kunt u een kunt maken.

    ![Replicatie inschakelen](./media/vmware-walkthrough-enable-replication/enable-rep3.png)
9. In **virtuele Machines** > **virtuele machines selecteren**en klik op elke machine die u wilt dat tooreplicate selecteren. U kunt alleen machines selecteren waarvoor replicatie kan worden ingeschakeld. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/vmware-walkthrough-enable-replication/enable-replication5.png)
10. In **eigenschappen** > **eigenschappen configureren**, selecteer Hallo-account dat wordt gebruikt door Hallo proces server tooautomatically Hallo Mobility-service op Hallo computer installeren.
11. Standaard zijn alle schijven worden gerepliceerd. Klik op **alle schijven** en wis alle schijven die u niet wilt dat tooreplicate. Klik vervolgens op **OK**. U kunt later meer VM-eigenschappen instellen.

    ![Replicatie inschakelen](./media/vmware-walkthrough-enable-replication/enable-replication6.png)
11. In **replicatie-instellingen** > **replicatie-instellingen configureren**, Controleer of deze Hallo juist replicatiebeleid is geselecteerd. Als u een beleid wijzigt, worden wijzigingen worden toegepast tooreplicating machine en toonew machines.
12. Schakel **consistentie tussen meerdere VM's** als u wilt dat toogather machines in een replicatiegroep en geef een naam voor de groep Hallo. Klik vervolgens op **OK**. Opmerking:

    * Computers in de replicatiegroepen samen repliceren en gedeelde crashconsistent en toepassingsconsistente herstelpunten wanneer ze een failover.
    * Het is raadzaam dat u verzamelen virtuele machines en fysieke servers zodat ze uw werkbelastingen. Inschakelen van de consistentie tussen meerdere VM's kunnen invloed hebben op prestaties workload en mag alleen worden gebruikt als machines worden uitgevoerd Hallo dezelfde werkbelasting en u moet consistentie.

    ![Replicatie inschakelen](./media/vmware-walkthrough-enable-replication/enable-replication7.png)
13. Klik op **replicatie inschakelen**. U kunt de voortgang van Hallo volgen **beveiliging inschakelen** taak **instellingen** > **taken** > **Site Recovery-taken**. Na het Hallo **beveiliging voltooien** taak wordt uitgevoerd Hallo machine is gereed voor failover.

## <a name="next-steps"></a>Volgende stappen

Ga te[stap 12: een testfailover uitvoeren](vmware-walkthrough-test-failover.md)
