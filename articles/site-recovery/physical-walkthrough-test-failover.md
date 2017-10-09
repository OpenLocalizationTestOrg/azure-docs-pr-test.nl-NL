---
title: een testfailover voor de fysieke server replicatie tooAzure met Azure Site Recovery aaaRun | Microsoft Docs
description: Geeft een overzicht van Hallo-stappen die u moet voor het uitvoeren van een testfailover voor [fysieke servers repliceren tooAzure hello Azure Site Recovery-service gebruiken.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a640e139-3a09-4ad8-8283-8fa92544f4c6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f8ed5ce585c5574be3018ce15339c4fd3b527eaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-run-a-test-failover-of-physical-servers-tooazure"></a>Stap 11: Een testfailover van fysieke servers tooAzure uitvoeren

Dit artikel wordt beschreven hoe toorun een testfailover van lokale fysieke servers tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.

Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Voordat u begint

Voordat u een testfailover die wordt aangeraden Hallo servereigenschappen controleren en breng de gewenste wijzigingen uitvoert moet u. U toegang hebt tot Hallo VM-eigenschappen in **gerepliceerde items**. Hallo **Essentials** blade ziet u informatie over machine-instellingen en status.

## <a name="managed-disk-considerations"></a>Beheerde schijf-overwegingen

[Schijven die worden beheerd](../virtual-machines/windows/managed-disks-overview.md) Schijfbeheer voor Azure VM's vereenvoudigen door het beheer van Hallo storage-accounts die zijn gekoppeld aan Hallo VM-schijven. 

- Als u beveiliging voor een server inschakelt, repliceert VM-gegevens tooa storage-account. Beheerde schijven worden gemaakt en gekoppeld toohello VM alleen wanneer failover plaatsvindt.
- Beheerde schijven kunnen alleen voor Azure Virtual machines die zijn geïmplementeerd met Resource Manager-model Hallo worden gemaakt.  
- Met deze instelling is ingeschakeld, alleen beschikbaarheidssets in resourcegroepen die beschikken over **beheerde schijven gebruiken** ingeschakeld kan worden geselecteerd. Virtuele machines met beheerde schijven moeten zich in beschikbaarheidssets met **beheerde schijven gebruiken** instellen te**Ja**. Als het Hallo-instelling is niet ingeschakeld voor virtuele machines, kunnen alleen in beschikbaarheidssets voor resourcegroepen zonder beheerde schijven ingeschakeld worden geselecteerd.
- [Meer informatie](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set) over beheerde schijven en beschikbaarheid ingesteld.
- Als Hallo storage account dat u voor replicatie gebruikt zijn versleuteld met versleuteling van opslag-Service, kunnen beheerde schijven kunnen niet worden gemaakt tijdens de failover. In dit geval ofwel niet gebruik van beheerde schijven, inschakelen of schakel de beveiliging voor VM Hallo en u deze toouse een opslagaccount dat geen versleuteling ingeschakeld. [Meer informatie](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="network-considerations"></a>Aandachtspunten voor netwerken

U kunt Hallo doel-IP-adres instellen voor een virtuele machine in Azure gemaakt na een failover.

- Als u een adres niet opgeeft, wordt Hallo failover machine DHCP gebruikt.
- Als u een adres dat is niet beschikbaar bij een failover, werkt failover niet.
- Hallo hetzelfde IP-adres van doel kan worden gebruikt voor testfailover als Hallo adres in het testfailovernetwerk Hallo beschikbaar is.
- Hallo aantal netwerkadapters wordt bepaald door het Hallo-grootte die u voor de virtuele doelmachine Hallo opgeeft:

     - Als Hallo aantal netwerkadapters op de bronmachine Hallo Hallo dezelfde is als of kleiner is dan het aantal adapters dat is toegestaan voor de doelgrootte machine Hallo hello, wordt Hallo doel hetzelfde aantal adapters als bron Hallo Hallo.
     - Als Hallo aantal adapters voor de virtuele bronmachine Hallo Hallo dat is toegestaan voor de doelgrootte hello, overschrijdt en vervolgens maximaal Hallo doel wordt gebruikt.
     - Als een bronmachine twee netwerkadapters heeft en de grootte van Hallo doelmachine vier ondersteunt, wordt Hallo doelmachine twee adapters hebben. Als Hallo-bronmachine twee adapters heeft, maar hello ondersteunde doelgrootte biedt alleen ondersteuning voor een hebben Hallo doelmachine slechts één adapter.     
   - Als Hallo virtuele machine meerdere netwerkadapters heeft worden deze allemaal verbonden toohello hetzelfde netwerk.
   - Als Hallo virtuele machine meerdere netwerkadapters Hallo heeft eerst weergegeven in de lijst hello wordt Hallo *standaard* netwerkadapter in hello Azure virtuele machine.
 - [Meer informatie](vmware-walkthrough-network.md) over IP-adressering.



## <a name="view-and-modify-vm-settings"></a>VM-instellingen weergeven en wijzigen

Het is raadzaam om de eigenschappen van de bronserver Hallo Hallo te controleren voordat u een failover uitvoert.

1. In **beveiligde Items**, klikt u op **gerepliceerde Items**, en klikt u op Hallo-machine.
2. In Hallo **gerepliceerde item** deelvenster ziet u een overzicht van de machine informatie, de status en Hallo meest recente beschikbare-herstelpunten. Klik op **eigenschappen** tooview om meer details.
3. In **berekening en netwerk**, kunt u:
    - Naam van de virtuele machine van Azure Hallo wijzigen. Hallo-naam moet voldoen aan [Azure-vereisten](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
    - Geef een na een failover [resourcegroep].
    - Geef de doelgrootte van een voor hello Azure VM
    - Selecteer een [beschikbaarheidsset](../virtual-machines/windows/tutorial-availability-sets.md).
    - Opgeven of toouse [schijven die worden beheerd](#managed-disk-considerations). Selecteer **Ja**, als u tooattach beheerde schijven tooyour machine op migratie tooAzure wilt.
    - Weergeven of wijzigen van de netwerkinstellingen, inclusief Hallo netwerksubnet/in welke hello Azure VM worden geplaatst na een failover en Hallo IP-adres dat wordt toegewezen tooit.
4. In **schijven**, ziet u informatie over Hallo-besturingssysteem en gegevensschijven op Hallo VM.

## <a name="run-a-test-failover"></a>Een testfailover uitvoeren

Nadat u hebt ingesteld alles, voert u toomake van de test-failover of dat alles werkt zoals verwacht.

- Als u wilt dat tooconnect tooAzure virtuele machines met RDP na een failover [tooconnect voorbereiden](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - toofully test u toocopy van Active Directory en DNS moet in uw testomgeving. [Meer informatie](site-recovery-active-directory.md#test-failover-considerations).
 - Lees voor volledige informatie over de testfailover [in dit artikel](site-recovery-test-failover-to-azure.md) artikel.
- Haal een snel overzicht van de video voordat u begint:

     
     >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]

Voer nu een failover:

1. toofail via één computer in **instellingen** > **gerepliceerde Items**, klikt u op de machine Hallo > **+ Testfailover** pictogram.

    ![Testfailover](./media/physical-walkthrough-test-failover/test-failover.png)

2. plan toofail via een herstelbewerking **instellingen** > **herstelplannen**, klik met de rechtermuisknop Hallo plan > **Testfailover**. een herstelplan toocreate [Volg deze instructies](site-recovery-create-recovery-plans.md).  

3. In **Testfailover**, selecteer hello Azure-netwerk toowhich virtuele Azure-machines moet worden verbonden nadat er failover plaatsvindt.

4. Klik op **OK** toobegin Hallo failover. U kunt de voortgang volgen door te klikken op Hallo machine tooopen eigenschappen of op Hallo **Testfailover** taak in de kluisnaam > **instellingen** > **taken**  >  **Site Recovery-taken**.

5. Nadat Hallo failover is voltooid, dient u zich kunt toosee Hallo replica virtuele machine in Azure worden weergegeven in hello Azure portal > **virtuele Machines**. U moet ervoor zorgen dat Hallo VM is de juiste grootte hello, of deze is verbonden met het juiste netwerk toohello en dat deze wordt uitgevoerd.

6. Als u voorbereid op verbindingen na een failover, moet u kunnen tooconnect toohello Azure VM.

### <a name="delete-test-failover-vms"></a>Testfailover van virtuele machines verwijderen

1. Als u klaar bent, klikt u op **testfailover opschonen** op Hallo herstelplan of machine.
2. In **notities**, vastleggen en opslaan van eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo.
3. Hallo opschonen actie verwijdert Azure VM's die zijn gemaakt tijdens de testfailover.

## <a name="summary"></a>Samenvatting

Als u een testfailover Hallo is voltooid, wordt uw fysieke servers repliceert en u hebt gecontroleerd of ze failover tooAzure. U kunt nu failovers uitvoeren in overeenstemming met de vereisten van uw organisatie. 

Houd er rekening mee dat u kan niet op dit moment een failback van Azure tooa fysieke server. U hebt toofail back-tooa VMware VM. Dit betekent dat u een on-premises VMware-infrastructuur in volgorde toofail back nodig. [Meer informatie](site-recovery-failback-azure-to-vmware.md) over mislukte back Azure Virtual machines tooVMware.


## <a name="next-steps"></a>Volgende stappen

- [Failovers uitvoeren](site-recovery-failover.md) indien nodig.
