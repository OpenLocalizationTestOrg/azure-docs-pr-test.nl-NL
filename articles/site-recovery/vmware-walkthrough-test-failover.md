---
title: Een testfailover voor VMware-replicatie uitvoeren naar Azure | Microsoft Docs
description: Geeft een overzicht van de stappen die u nodig hebt voor het uitvoeren van een testfailover voor virtuele VMware-machines repliceren naar Azure met behulp van de Azure Site Recovery-service.
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
ms.openlocfilehash: f1a6df56a2bb0094d972d2e659057cc124156b88
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="step-12-run-a-test-failover-to-azure-for-vmware-vms"></a>Stap 12: Een testfailover uitvoeren naar Azure voor virtuele VMware-machines

Dit artikel wordt beschreven hoe u een testfailover uitvoeren van on-premises virtuele VMware-machines naar Azure met behulp van de [Azure Site Recovery](site-recovery-overview.md) service in de Azure portal.

Opmerkingen en vragen plaatsen onder aan dit artikel of op de [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Voordat u begint

Voordat u een testfailover die wordt aangeraden Controleer of de VM-eigenschappen en breng de gewenste wijzigingen uitvoert moet u. u kunt toegang tot de VM-eigenschappen in **gerepliceerde items**. De **Essentials** blade ziet u informatie over machines instellingen en status.

## <a name="managed-disk-considerations"></a>Beheerde schijf-overwegingen

[Schijven die worden beheerd](../virtual-machines/windows/managed-disks-overview.md) Schijfbeheer voor Azure VM's vereenvoudigen door het beheer van de storage-accounts die zijn gekoppeld aan de VM-schijven. 

- Als u beveiliging voor een virtuele machine inschakelt, wordt virtuele machine worden gerepliceerd naar een opslagaccount. Beheerde schijven zijn gemaakt en gekoppeld aan de virtuele machine alleen wanneer failover plaatsvindt.
- Beheerde schijven kunnen alleen voor virtuele machines die zijn geïmplementeerd met behulp van de Resource Manager-model worden gemaakt.  
- Met deze instelling is ingeschakeld, alleen beschikbaarheidssets in resourcegroepen die beschikken over **beheerde schijven gebruiken** ingeschakeld kan worden geselecteerd. Virtuele machines met beheerde schijven moeten zich in beschikbaarheidssets met **beheerde schijven gebruiken** ingesteld op **Ja**. Als de instelling is niet ingeschakeld voor virtuele machines, kunnen alleen in beschikbaarheidssets voor resourcegroepen zonder beheerde schijven ingeschakeld worden geselecteerd.
- [Meer informatie](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set) over beheerde schijven en beschikbaarheid ingesteld.
- Als het opslagaccount dat u voor replicatie gebruikt zijn versleuteld met versleuteling van opslag-Service, kunnen beheerde schijven kunnen niet worden gemaakt tijdens de failover. In dit geval niet een gebruik van beheerde schijven, inschakelen of schakel de beveiliging voor de virtuele machine en opnieuw inschakelen voor gebruik van een opslagaccount dat geen versleuteling ingeschakeld. [Meer informatie](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="network-considerations"></a>Aandachtspunten voor netwerken

U kunt de IP-adres van doel instellen voor een virtuele machine in Azure gemaakt na een failover.

- Als u geen adres opgeeft, maakt de machine waarvoor een failover is uitgevoerd, gebruik van DHCP.
- Als u een adres dat is niet beschikbaar bij een failover, werkt failover niet.
- Hetzelfde doel-IP-adres kan worden gebruikt voor de testfailover, als het adres beschikbaar in het testfailovernetwerk is.
- Het aantal netwerkadapters wordt bepaald door de grootte die u voor de virtuele doelmachine opgeeft:

     - Als het aantal netwerkadapters op de bronmachine hetzelfde als of kleiner is dan het aantal adapters dat is toegestaan voor de grootte van de doelmachine, wordt het doel hetzelfde aantal adapters als de bron hebben.
     - Als het aantal adapters voor de virtuele bronmachine groter is dan het aantal dat is toegestaan voor de doelgrootte dan het maximum wordt gebruikt.
     - Als een bronmachine bijvoorbeeld twee netwerkadapters heeft en met de grootte van de doelmachine vier netwerkadapters worden ondersteund, heeft de doelcomputer twee adapters. Als de bronmachine twee adapters heeft, maar met de ondersteunde doelgrootte slechts één wordt ondersteund, heeft de doelcomputer slechts één adapter.     
   - Als de virtuele machine meerdere netwerkadapters die worden deze allemaal verbonden met hetzelfde netwerk heeft.
   - Als de virtuele machine meerdere netwerkadapters heeft dan het eerste beheerpunt dat wordt weergegeven in de lijst wordt de *standaard* netwerkadapter in de virtuele machine van Azure.
 - [Meer informatie](vmware-walkthrough-network.md) over IP-adressering.



## <a name="view-and-modify-vm-settings"></a>VM-instellingen weergeven en wijzigen

U wordt aangeraden de eigenschappen van de bronmachine te controleren voordat u een failover uitvoert.

1. In **beveiligde Items**, klikt u op **gerepliceerde Items**, en klik op de virtuele machine.
2. In de **gerepliceerde item** deelvenster ziet u een overzicht van de VM-informatie, de status en de meest recente beschikbare herstelpunten. Klik op **eigenschappen** om meer details te bekijken.
3. In **berekening en netwerk**, kunt u:
    - Wijzig de naam van de virtuele machine van Azure. De naam moet voldoen aan [Azure-vereisten](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
    - Geef een na een failover [resourcegroep].
    - Specificeer de doelgrootte van een voor de Azure VM
    - Selecteer een [beschikbaarheidsset](../virtual-machines/windows/tutorial-availability-sets.md).
    - Geef op of gebruik [schijven die worden beheerd](#managed-disk-considerations). Selecteer **Ja**als u wilt koppelen beheerde schijven aan de computer over de migratie naar Azure.
    - Netwerkinstellingen weergeven of wijzigen, met inbegrip van de netwerk-en het subnet waarin de virtuele machine in Azure worden opgeslagen na de failover- en het IP-adres dat wordt toegewezen aan deze.
4. In **schijven**, vindt u informatie over het besturingssysteem en gegevensschijven op de virtuele machine.

## <a name="run-a-test-failover"></a>Een testfailover uitvoeren

Nadat u hebt ingesteld alles, werkt uitvoeren van een testfailover om te controleren of Alles zoals verwacht.

- Als u wilt verbinding maken met virtuele Azure-machines met RDP na een failover [voorbereiden om verbinding te](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - Als u een volledige test wilt uitvoeren, moet u Active Directory en DNS naar uw testomgeving kopiëren. [Meer informatie](site-recovery-active-directory.md#test-failover-considerations).
 - Lees voor volledige informatie over de testfailover [in dit artikel](site-recovery-test-failover-to-azure.md) artikel.
- Haal een snel overzicht van de video voordat u begint:


     >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


Voer nu een failover:

1. Een enkele machine failover **instellingen** > **gerepliceerde Items**, klikt u op de virtuele machine > **+ Testfailover** pictogram.

    ![Testfailover](./media/vmware-walkthrough-test-failover/test-failover.png)

2. Als u een failover wilt uitvoeren op basis van een herstelplan, klikt u in **Instellingen** > **Herstelplannen** met de rechtermuisknop op het plan > **Testfailover**. Volg [deze instructies](site-recovery-create-recovery-plans.md) om een herstelplan te maken.  

3. In **Testfailover**, selecteer het Azure-netwerk welke virtuele Azure-machines moet worden verbonden nadat er failover plaatsvindt.

4. Klik op **OK** om te beginnen met de failover. U kunt de voortgang volgen door te klikken op de virtuele machine om de eigenschappen te openen of op de **Testfailover** taak in de kluisnaam > **instellingen** > **taken** > **Site Recovery-taken**.

5. Wanneer de failover is voltooid, moet u de gerepliceerde Azure-machine ook kunnen zien in Azure Portal > **Virtuele machines**. Controleer of de virtuele machine de juiste grootte heeft, of deze is verbonden met het juiste netwerk en of deze actief is.

6. Als u verbindingen hebt voorbereid na een failover, kunt u verbinding maken met de Azure-VM.

7. Als u klaar bent, klikt u op **testfailover opschonen** op het herstelplan. In **notities**, vastleggen en opslaan van eventuele opmerkingen die zijn gekoppeld aan de testfailover. Hiermee verwijdert u de virtuele machines die zijn gemaakt tijdens de testfailover.



## <a name="next-steps"></a>Volgende stappen

- [Meer informatie](site-recovery-failover.md) over verschillende soorten failovers en hoe ze uit te voeren.
- Als u bij het migreren van computers in plaats van met repliceren en mislukt achter, [meer](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- [Meer informatie over failback](site-recovery-failback-azure-to-vmware.md), zodat een failback- en virtuele Azure-machines repliceren naar de primaire lokale site.
