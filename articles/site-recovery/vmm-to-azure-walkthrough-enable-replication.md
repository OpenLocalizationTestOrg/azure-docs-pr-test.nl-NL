---
title: aaaEnable replicatie tooAzure voor Hyper-V-machines in VMM-clouds met Azure Site Recovery | Microsoft Docs
description: Hierin wordt beschreven hoe tooenable replicatie tooAzure voor Hyper-V-machines in VMM clouds, hello Azure Site Recovery-service
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 89a2c4fc-7e03-4a86-a2c0-52831ccebc1a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 1a39bf65490c59a89a5e891184cadfacc2adee6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-tooazure-for-hyper-v-vms-in-vmm-clouds"></a>Stap 11: TooAzure replicatie inschakelen voor Hyper-V-machines in VMM-clouds

Nadat u een beleid voor wachtwoordreplicatie hebt ingesteld, gebruiken deze artikel tooenable replicatie voor de on-premises Hyper-V virtuele machines (VM's) in System Center Virtual Machine Manager (VMM)-clouds worden beheerd), tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md)service in hello Azure-portal.

Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Voordat u begint

Zorg ervoor dat uw Azure-account juist Hallo [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate virtuele Azure-machines. [Meer informatie](../active-directory/role-based-access-built-in-roles.md) over op rollen gebaseerd toegangsbeheer van Azure.

## <a name="exclude-disks-from-replication"></a>Schijven uitsluiten van replicatie

Standaard worden alle schijven op een machine gerepliceerd. U kunt schijven uitsluiten van replicatie. Zo wilt u mogelijk niet tooreplicate schijven met tijdelijke gegevens of gegevens die telkens wanneer een machine is bijgewerkt of de toepassing opnieuw wordt gestart (bijvoorbeeld pagefile.sys of SQL Server tempdb). [Meer informatie](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>Virtuele machines repliceren

Replicatie voor virtuele machines als volgt inschakelen:  

1. Klik op **Stap 2: toepassing repliceren** > **Bron**. Nadat u replicatie voor Hallo eerst hebt ingeschakeld, klikt u op **+ repliceren** in Hallo kluis tooenable replicatie voor aanvullende machines.

    ![Replicatie inschakelen](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication1.png)
2. In Hallo **bron** blade, selecteer Hallo VMM-server en Hallo cloud in welke Hallo Hyper-V-hosts zich bevinden. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-source.png)
3. In **doel**, selecteert u Hallo-abonnement na een failover-implementatiemodel, en Hallo storage-account wordt gebruikt voor gerepliceerde gegevens.

    ![Replicatie inschakelen](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-target.png)
4. Selecteer Hallo gewenste toouse storage-account. Als u wilt dat toouse een ander opslagaccount dan die u hebt, kunt u [maken van een](#set-up-an-azure-storage-account). Als u een premium storage-account voor gerepliceerde gegevens gebruikt, moet u tooselect een extra standard-opslag account toostore replicatielogboeken die de doorlopende wijzigingen tooon-premises data.toocreate een opslagaccount met behulp van de Resource Manager-model Hallo vastleggen Klik op **nieuw**. Als u een opslagaccount met behulp van het klassieke model Hallo toocreate wilt, dat doen [in hello Azure-portal](../storage/common/storage-create-storage-account.md). Klik vervolgens op **OK**.
5. Selecteer hello Azure-netwerk en subnet toowhich Azure Virtual machines wordt verbinding gemaakt, wanneer ze zijn gemaakt na een failover. Selecteer **nu configureren voor geselecteerde machines**, tooapply Hallo instelling tooall machines in het netwerk u selecteert voor beveiliging. Selecteer **later configureren**, tooselect hello Azure-netwerk per computer. Als u wilt dat toouse een ander netwerk van de referenties die u hebt, kunt u [maken van een](#set-up-an-azure-network). een netwerk met toocreate Hallo klikt u op Resource Manager-model **nieuw**. Als u een netwerk met het klassieke model Hallo toocreate wilt, dat doen [in hello Azure-portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Selecteer indien van toepassing een subnet. Klik vervolgens op **OK**.
6. In **virtuele Machines** > **virtuele machines selecteren**en klik op elke machine die u wilt dat tooreplicate selecteren. U kunt alleen machines selecteren waarvoor replicatie kan worden ingeschakeld. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication5.png)

7. In **eigenschappen** > **eigenschappen configureren**Hallo-besturingssysteem voor virtuele machines Hallo geselecteerd en selecteer Hallo besturingssysteemschijf.

    - Controleer of deze Hallo Azure VM-naam (doelnaam) voldoet aan [vereisten van de virtuele machine van Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).   
    - Standaard worden alle Hallo schijven Hallo VM geselecteerd voor replicatie, maar u kunt schijven tooexclude wissen ze.

        - U kunt tooexclude schijven tooreduce replicatie bandbreedte. Bijvoorbeeld, wilt u mogelijk niet tooreplicate schijven met tijdelijke gegevens of gegevens die is vernieuwd telkens wanneer een computer of apps (zoals pagefile.sys of Microsoft SQL Server tempdb) opnieuw wordt opgestart. U kunt Hallo schijf uitsluiten van replicatie door geïnstalleerd Hallo-schijf.
        - Alleen standaardschijven kunnen worden uitgesloten. U kunt geen besturingssysteemschijven uitsluiten.
        - We raden u aan geen dynamische schijven uit te sluiten. Met Site Recovery kan niet worden vastgesteld of een virtuele harde schijf in een gast-VM een basisschijf of een dynamische schijf is. Als u alle schijven van de afhankelijke dynamisch volume niet worden uitgesloten, worden Hallo beveiligde dynamische schijf wordt weergegeven als een niet-werkende schijf wanneer hello VM failover wordt uitgevoerd en Hallo gegevens op de schijf niet toegankelijk.
        - Nadat de replicatie is ingeschakeld, kunt u geen schijven meer toevoegen of verwijderen voor replicatie. Als u wilt dat tooadd of uitsluiten van een schijf, moet u toodisable beveiliging voor Hallo VM nodig en vervolgens opnieuw inschakelen.
        - Voor schijven die u handmatig hebt gemaakt in Azure, wordt geen failback uitgevoerd. Als u meer dan drie schijven mislukken en twee rechtstreeks in Azure VM maken, wordt bijvoorbeeld alleen Hallo drie schijven die zijn failover mislukt door Azure tooHyper-V. U kunt geen schijven die handmatig zijn gemaakt in de failback of in de omgekeerde replicatie van Hyper-V tooAzure opnemen.
        - Als u een schijf die nodig is voor een toepassing toooperate uitsluit, na failover tooAzure moet u toocreate handmatig in Azure, zodat die Hallo gerepliceerd toepassing uit te voeren. U kunt ook kan u integreren met Azure automation een herstelplan, toocreate Hallo schijf tijdens de failover van Hallo-machine.

    Klik op **OK** toosave wijzigingen. Later kunt u eventueel extra eigenschappen instellen.

    ![Replicatie inschakelen](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

8. In **replicatie-instellingen** > **replicatie-instellingen configureren**, Hallo replicatiebeleid u tooapply voor Hallo virtuele machines beveiligde wilt selecteren. Klik vervolgens op **OK**. U kunt het replicatiebeleid Hallo in wijzigen **replicatiebeleid** > beleidsnaam > **instellingen bewerken**. De wijzigingen die u toepast, worden zowel gebruikt voor machines die al worden gerepliceerd, als voor nieuwe machines.

   ![Replicatie inschakelen](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication7.png)

U kunt de voortgang van Hallo volgen **beveiliging inschakelen** taak **taken** > **Site Recovery-taken**. Na het Hallo **beveiliging voltooien** taak wordt uitgevoerd, Hallo machine is gereed voor failover.



## <a name="next-steps"></a>Volgende stappen

Ga te[stap 12: een testfailover uitvoeren](vmm-to-azure-walkthrough-test-failover.md)
