---
title: een testfailover voor Hyper-V-replicatie (zonder de System Center VMM) tooAzure aaaRun | Microsoft Docs
description: Geeft een overzicht van Hallo stappen die u nodig hebt voor een testfailover uitgevoerd voor Hyper-V-machines repliceren tooAzure met hello Azure Site Recovery-service.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c9a4c3ca-84a0-4668-b700-9b0046202299
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: dbcca080a8fa139e2ea0d132323101dd0f7cd265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-run-a-test-failover-for-hyper-v-replication-tooazure"></a>Stap 11: Een testfailover voor Hyper-V-replicatie tooAzure uitvoeren

Dit artikel wordt beschreven hoe toorun een testfailover van lokale Hyper-V virtuele machines (wordt niet beheerd door System Center VMM) tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.

Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Voordat u begint

Voordat u een testfailover die wordt aangeraden controleren Hallo VM-eigenschappen en breng de gewenste wijzigingen uitvoert moet u. U toegang hebt tot Hallo VM-eigenschappen in **gerepliceerde items**. Hallo **Essentials** blade ziet u informatie over machines instellingen en status.

## <a name="managed-disk-considerations"></a>Beheerde schijf-overwegingen

[Schijven die worden beheerd](../virtual-machines/windows/managed-disks-overview.md) Schijfbeheer voor Azure VM's vereenvoudigen door het beheer van Hallo storage-accounts die zijn gekoppeld aan Hallo VM-schijven. 

- Beheerde schijven worden gemaakt en gekoppeld toohello VM alleen wanneer een tooAzure failover plaatsvindt. Als u beveiliging inschakelt, repliceert gegevens van virtuele machines voor lokale accounts toostorage.
- Beheerde schijven kunnen alleen voor virtuele machines die zijn geïmplementeerd met Hallo Resource manager-implementatiemodel worden gemaakt.
- Failback vanuit Azure tooan een on-premises Hyper-V-omgeving wordt momenteel niet ondersteund voor computers met beheerde schijven. U moet alleen instellen **beheerde schijven gebruiken** te**Ja** als u alleen een migratie alleen (failover tooAzure zonder failback)
- Met deze instelling is ingeschakeld, alleen beschikbaarheidssets in resourcegroepen die beschikken over **beheerde schijven gebruiken** ingeschakeld kan worden geselecteerd. Virtuele machines met beheerde schijven moeten zich in beschikbaarheidssets met **beheerde schijven gebruiken** instellen te**Ja**. Als het Hallo-instelling is niet ingeschakeld voor virtuele machines, kunnen alleen in beschikbaarheidssets voor resourcegroepen zonder beheerde schijven ingeschakeld worden geselecteerd. [Meer informatie](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).
- - Als Hallo storage account dat u voor replicatie gebruikt zijn versleuteld met versleuteling van opslag-Service, kunnen beheerde schijven kunnen niet worden gemaakt tijdens de failover. In dit geval ofwel niet gebruik van beheerde schijven, inschakelen of schakel de beveiliging voor VM Hallo en u deze toouse een opslagaccount dat geen versleuteling ingeschakeld. [Meer informatie](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).

 
## <a name="network-considerations"></a>Aandachtspunten voor netwerken
    
- Hallo doel-IP-adres toobe voor hello Azure VM na een failover gebruikt, kunt u instellen. Als u een adres niet opgeeft, wordt Hallo failover machine DHCP gebruikt. Als u een adres dat is niet beschikbaar bij een failover instelt, mislukt Hallo failover. Hallo hetzelfde IP-adres van doel kan worden gebruikt voor een testfailover als Hallo adres in het testfailovernetwerk Hallo beschikbaar is.
- Hallo aantal netwerkadapters wordt bepaald door Hallo-grootte die u voor Hallo doel-virtuele machine, als volgt opgeeft:
    - Als het aantal netwerkadapters op de bronmachine Hallo Hallo kleiner dan of gelijk aantal adapters toohello toegestaan voor de doelgrootte machine Hallo vervolgens Hallo doel hetzelfde aantal adapters als bron Hallo Hallo.
    - Als het aantal adapters voor de virtuele bronmachine Hallo HALLO hallo maximum overschrijden voor Hallo doelgrootte, wordt maximaal Hallo doel wordt gebruikt.
    - Bijvoorbeeld als een bronmachine twee netwerkadapters heeft en de grootte van Hallo doelmachine vier ondersteunt, Hallo doelmachine twee adapters hebben. Als Hallo-bronmachine twee adapters heeft, maar hello ondersteunde doelgrootte biedt alleen ondersteuning voor een hebben Hallo doelmachine slechts één adapter.     
- Als Hallo VM meerdere netwerkadapters heeft worden deze allemaal verbonden toohello hetzelfde netwerk.
- Als Hallo virtuele machine meerdere netwerkadapters Hallo heeft eerst weergegeven in de lijst hello wordt Hallo *standaard* netwerkadapter in hello Azure virtuele machine.


## <a name="view-and-manage-vm-settings"></a>Weergeven en beheren van instellingen voor VM

Het is raadzaam om de eigenschappen van de bronmachine Hallo Hallo te controleren voordat u een failover uitvoert.

1. In **beveiligde Items**, klikt u op **gerepliceerde Items**, en klik op Hallo VM.

    ![Replicatie inschakelen](./media/hyper-v-site-walkthrough-test-failover/test-failover1.png)
2. In Hallo **gerepliceerde item** deelvenster ziet u een samenvatting van VM-informatie, de status en Hallo meest recente beschikbare-herstelpunten. Klik op **eigenschappen** tooview om meer details.

    ![Replicatie inschakelen](./media/hyper-v-site-walkthrough-test-failover/test-failover2.png)
3. In **berekening en netwerk**, kunt u:
    - Naam van de virtuele machine van Azure Hallo wijzigen. Hallo-naam moet voldoen aan [Azure-vereisten](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
    - Geef een na een failover [resourcegroep].
    - Geef de doelgrootte van een voor hello Azure VM
    - Selecteer een [beschikbaarheidsset](../virtual-machines/windows/tutorial-availability-sets.md).
    - Opgeven of toouse [schijven die worden beheerd](#managed-disk-considerations). Selecteer **Ja**, als u tooattach beheerde schijven tooyour machine op migratie tooAzure wilt.
    - Weergeven of wijzigen van de netwerkinstellingen, inclusief Hallo netwerksubnet/in welke hello Azure VM worden geplaatst na een failover en Hallo IP-adres dat wordt toegewezen tooit.

    ![Replicatie inschakelen](./media/hyper-v-site-walkthrough-test-failover/test-failover4.png)
4. In **schijven**, ziet u informatie over Hallo-besturingssysteem en gegevensschijven op Hallo VM.


## <a name="run-a-test-failover"></a>Een testfailover uitvoeren

Voer nu een test failover toomake, controleren of dat alles werkt zoals verwacht.

- Als u wilt dat tooconnect tooAzure virtuele machines met RDP na een failover [tooconnect voorbereiden](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - toofully test u toocopy van Active Directory en DNS moet in uw testomgeving. [Meer informatie](site-recovery-active-directory.md#test-failover-considerations).
 - Lees voor volledige informatie over de testfailover [in dit artikel](site-recovery-test-failover-to-azure.md) artikel.
 
 Nu u een failover uitvoeren:

1. toofail via één computer in **gerepliceerde Items**, klikt u op Hallo VM > **+ Testfailover** pictogram.
2. plan toofail via een herstelbewerking **herstelplannen**, klik met de rechtermuisknop Hallo plan > **Testfailover**. een herstelplan toocreate [Volg deze instructies](site-recovery-create-recovery-plans.md).
3. In **Testfailover**, selecteer hello Azure-netwerk toowhich virtuele Azure-machines moet worden verbonden nadat er failover plaatsvindt.
4. Klik op **OK** toobegin Hallo failover. U kunt de voortgang volgen door te klikken op Hallo VM tooopen eigenschappen of op Hallo **Testfailover** taak in de kluisnaam > **taken** > **Site Recovery-taken**.
5. Nadat de failover Hallo is voltooid, dient u zich kunt toosee Hallo replica machine van Azure in hello Azure-portal weergegeven > **virtuele Machines**. U moet ervoor zorgen dat Hallo VM is de juiste grootte hello, of deze is verbonden met het juiste netwerk toohello en dat deze wordt uitgevoerd.
6. Als u voorbereid op verbindingen na een failover, moet u kunnen tooconnect toohello Azure VM.
7. Als u klaar bent, klikt u op **testfailover opschonen** op Hallo herstelplan. In **notities** opnemen en eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo opslaan. Hiermee verwijdert u Hallo virtuele machines die zijn gemaakt tijdens de testfailover.



## <a name="next-steps"></a>Volgende stappen

- [Meer informatie](site-recovery-failover.md) over verschillende soorten failovers, en hoe toorun ze.
- [Meer informatie over failback](site-recovery-failback-from-azure-to-hyper-v.md), toofail back en repliceren Azure VM's weer toohello primaire on-premises Hyper-V-site.

