---
title: Toepassingen (VMware tooAzure) repliceren | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooset van de replicatie van de virtuele machines die wordt uitgevoerd in VMware in Azure.
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: asgang
ms.openlocfilehash: b07aabdacec521c7bd89e50f6a1427a774ff0287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-applications-running-on-vmware-vms-tooazure"></a>Toepassingen die worden uitgevoerd op virtuele VMware-machines tooAzure repliceren



Dit artikel wordt beschreven hoe tooset van de replicatie van de virtuele machines die wordt uitgevoerd in VMware in Azure.
## <a name="prerequisites"></a>Vereisten

Hallo artikel wordt ervan uitgegaan dat u al hebt

1.  [On-premises gegevensbron omgeving instellen](site-recovery-set-up-vmware-to-azure.md)
2.  [De doelomgeving instellen in Azure](site-recovery-prepare-target-vmware-to-azure.md)


## <a name="enable-replication"></a>Replicatie inschakelen
#### <a name="before-you-start"></a>Voordat u begint
Houd rekening met het volgende bij het repliceren van virtuele VMware-machines:

* Uw Azure gebruikersaccount moet toohave bepaalde [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicatie van een nieuwe virtuele machine tooAzure.
* Virtuele VMware-machines worden gedetecteerd om de 15 minuten. Kan duren voordat de 15 minuten of langer ze tooappear in de portal Hallo na de detectie. Evenzo detectie kunt 15 minuten of langer duren wanneer u een nieuwe vCenter-server of vSphere host toevoegt.
* Omgevingswijzigingen op Hallo virtuele machine (zoals VMware tools-installatie) duurt 15 minuten of meer toobe bijgewerkt in Hallo-portal.
* U kunt controleren tijd voor virtuele VMware-machines in Hallo Hallo laatste gedetecteerd **laatste Contact op** veld Hallo vCenter server/vSphere host op Hallo **configuratieservers** blade.
* tooadd machines voor replicatie zonder te wachten Hallo geplande detectie, markeer de configuratieserver hello (Klik niet op deze), en klik op Hallo **vernieuwen** knop.
* Wanneer u replicatie inschakelt als Hallo machine is voorbereid, installeert de processerver Hallo Hallo Mobility-service automatisch erop.


**Schakel replicatie nu als volgt**:

1. Klik op **Stap 2: toepassing repliceren** > **Bron**. Nadat u replicatie voor Hallo eerst hebt ingeschakeld, klikt u op **+ repliceren** in Hallo kluis tooenable replicatie voor aanvullende machines.
2. In Hallo **bron** blade > **bron**, selecteer Hallo configuratieserver.
3. In **type Machine**, selecteer **virtuele Machines** of **fysieke Machines**.
4. In **vCenter/vSphere-Hypervisor**, selecteert u Hallo vCenter-server die wordt beheerd Hallo vSphere host of selecteer Hallo host. Deze instelling niet relevant als u fysieke machines repliceert.
5. Selecteer de processerver Hallo. Als u geen processervers extra hebt gemaakt, wordt dit Hallo-naam van de configuratieserver Hallo zijn. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. In **doel** Hallo-abonnement en resourcegroep Hallo waar u toocreate Hallo failover van virtuele machines wilt selecteren. Hallo-implementatiemodel dat u toouse in Azure (klassiek of de resource management) voor Hallo failover van virtuele machines wilt kiezen.
7. Selecteer hello Azure storage-account gewenste toouse voor het repliceren van gegevens. Opmerking:

   * U kunt een premium- of standard-opslagaccount selecteren. Als u een premium-account selecteren, moet u toospecify een extra standard storage-account voor lopende replicatielogboeken. Accounts moeten in Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis.
   * Als u wilt dat toouse een ander opslagaccount dan die u hebt, kunt u een*tijdelijke aanduiding voor koppeling voor het maken van de storage-account met behulp van resource manager die worden behandeld in aan de slag*. toocreate een opslagaccount met Resource Manager, klikt u op **nieuw**. Als u een opslagaccount met behulp van het klassieke model Hallo toocreate wilt, u dat doen [in hello Azure-portal](../storage/common/storage-create-storage-account.md).

8. Selecteer hello Azure-netwerk en subnet toowhich Azure Virtual machines wordt verbinding gemaakt, wanneer ze zijn gemaakt na een failover. Hallo-netwerk moet zich op Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis. Selecteer **nu configureren voor geselecteerde machines**, tooapply Hallo instelling tooall machines in het netwerk u selecteert voor beveiliging. Selecteer **later configureren** tooselect hello Azure-netwerk per computer. Als u een netwerk hebt, moet u deze te[maken van een](#set-up-an-azure-network). toocreate een netwerk met Resource Manager, klikt u op **nieuw**. Als u een netwerk met het klassieke model Hallo toocreate wilt, dat doen [in hello Azure-portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Selecteer indien van toepassing een subnet. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. In **virtuele Machines** > **virtuele machines selecteren**en klik op elke machine die u wilt dat tooreplicate selecteren. U kunt alleen machines selecteren waarvoor replicatie kan worden ingeschakeld. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. In **eigenschappen** > **eigenschappen configureren**, selecteer Hallo-account dat wordt gebruikt door Hallo proces server tooautomatically Hallo Mobility-service op Hallo computer installeren.  
11. Standaard zijn alle schijven worden gerepliceerd. tooexclude schijven van replicatie, klikt u op **alle schijven** en wis alle schijven die u niet wilt dat tooreplicate.  Klik vervolgens op **OK**. Later kunt u eventueel extra eigenschappen instellen. [Meer informatie](site-recovery-exclude-disk.md) over het uitsluiten van schijven.

    ![Replicatie inschakelen](./media/site-recovery-vmware-to-azure/enable-replication6.png)

12. In **replicatie-instellingen** > **replicatie-instellingen configureren**, Controleer of deze Hallo juist replicatiebeleid is geselecteerd. U kunt replicatie-beleidsinstellingen in wijzigen **instellingen** > **replicatiebeleid** > beleidsnaam > **instellingen bewerken**. Wijzigingen die u toepast tooa beleid worden toegepast tooreplicating en nieuwe machines.
13. Schakel **consistentie tussen meerdere VM's** als u wilt dat toogather machines in een replicatiegroep en geef een naam voor de groep Hallo. Klik vervolgens op **OK**. Opmerking:

    * Computers in de replicatie repliceren groeperen en gedeelde crashconsistent en toepassingsconsistente herstelpunten wanneer ze een failover.
    * Het is raadzaam dat u verzamelen virtuele machines en fysieke servers zodat ze uw werkbelastingen. Inschakelen van de consistentie tussen meerdere VM's kunnen invloed hebben op prestaties van de werkbelasting en mag alleen worden gebruikt als machines worden uitgevoerd Hallo dezelfde werkbelasting en u moet consistentie.

    ![Replicatie inschakelen](./media/site-recovery-vmware-to-azure/enable-replication7.png)
14. Klik op **replicatie inschakelen**. U kunt de voortgang van Hallo volgen **beveiliging inschakelen** taak **instellingen** > **taken** > **Site Recovery-taken**. Na het Hallo **beveiliging voltooien** taak wordt uitgevoerd Hallo machine is gereed voor failover.

> [!NOTE]
> Als het Hallo-machine is voorbereid voor de push-installatie Hallo Mobility serviceonderdeel wordt geïnstalleerd wanneer beveiliging is ingeschakeld. Na het Hallo wordt onderdeel geïnstalleerd op Hallo-computer die een beveiligingstaak wordt gestart en mislukt. Na een storing op Hallo moet u toomanually start opnieuw op elke machine. Na Hallo herstart Hallo beveiliging begint taak opnieuw en initiële replicatie plaatsvindt.
>
>

## <a name="view-and-manage-vm-properties"></a>Eigenschappen van virtuele machines weergeven en beheren

Het is raadzaam om de eigenschappen van de bronmachine Hallo Hallo te controleren. Houd er rekening mee dat hello Azure VM-naam moet voldoen aan [vereisten van de virtuele machine van Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. Klik op **instellingen** > **gerepliceerde items** >, en selecteer Hallo-machine. Hallo **Essentials** blade ziet u informatie over machines instellingen en status.
2. In **eigenschappen**, vindt u replicatie en failover-informatie voor Hallo VM.
3. In **berekening en netwerk** > **eigenschappen berekenen**, kunt u de naam en doel van de grootte van virtuele machine van Azure Hallo opgeven. Hallo naam toocomply met Azure-vereisten wijzigen als u wilt.
    ![Replicatie inschakelen](./media/site-recovery-vmware-to-azure/VMProperties_AVSET.png)
 
4.  Kunt u een [resourcegroep](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-resource-groups-guidelines) van welke machine wordt nu deel uit van na een failover. U kunt deze altijd vóór mislukken instelling via wijzigen. Na een failover, als u migreert Hallo machine tooa andere resourcegroep vervolgens verbreekt de beveiligingsinstellingen van een machine.
5. Kunt u een [beschikbaarheidsset](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) als uw computer vereist toobe deel uitmaken van één na een failover. Tijdens het instellen van de beschikbaarheid van de te selecteren, neem Houd rekening met:

    * Alleen beschikbaarheidssets behoren toohello opgegeven wordt resourcegroep weergegeven  
    * Computers met verschillende virtuele netwerken mag geen deel uit van dezelfde beschikbaarheidsset
    * Alleen virtuele machines met een grootte van dezelfde kan een deel uitmaken van dezelfde beschikbaarheidsset
5. U kunt ook bekijken en informatie over het doelnetwerk hello, subnet en IP-adres dat wordt toegewezen toohello virtuele Azure-machine toevoegen.
6. In **schijven**, ziet u Hallo-besturingssysteem en gegevensschijven op Hallo VM die wordt gerepliceerd.

### <a name="network-adapters-and-ip-addressing"></a>Netwerkadapters en IP-adressering 

- U kunt IP-adres van Hallo doel instellen. Als u een adres niet opgeeft, wordt Hallo failover machine DHCP gebruikt. Als u een adres dat is niet beschikbaar bij een failover, werkt Hallo failover niet. Hallo hetzelfde IP-adres van doel kan worden gebruikt voor een testfailover als Hallo adres in het testfailovernetwerk Hallo beschikbaar is.
- Hallo aantal netwerkadapters wordt bepaald door Hallo-grootte die u voor Hallo doel-virtuele machine, als volgt opgeeft:
    - Als het aantal netwerkadapters op de bronmachine Hallo Hallo kleiner dan of gelijk aantal adapters toohello toegestaan voor de doelgrootte machine Hallo vervolgens Hallo doel hetzelfde aantal adapters als bron Hallo Hallo.
    - Als het aantal adapters voor de virtuele bronmachine Hallo HALLO hallo maximum overschrijden voor Hallo doelgrootte, wordt maximaal Hallo doel wordt gebruikt.
    - Bijvoorbeeld als een bronmachine twee netwerkadapters heeft en de grootte van Hallo doelmachine vier ondersteunt, Hallo doelmachine twee adapters hebben. Als Hallo-bronmachine twee adapters heeft, maar hello ondersteunde doelgrootte biedt alleen ondersteuning voor een hebben Hallo doelmachine slechts één adapter.
    - Als Hallo virtuele machine meerdere netwerkadapters heeft worden deze allemaal verbonden toohello hetzelfde netwerk.
    - Als Hallo virtuele machine meerdere netwerkadapters Hallo heeft eerst weergegeven in de lijst hello wordt Hallo *standaard* netwerkadapter in hello Azure virtuele machine.
   



## <a name="common-issues"></a>Algemene problemen

* Elke schijf moet minder dan 1TB groot zijn.
* Hallo OS-schijf moet een standaardschijf zijn en niet-dynamische schijf
* Voor generatie 2/UEFI ingeschakeld voor virtuele machines, de besturingssysteemgroep Hallo moet Windows en opstartschijf moet minder dan 300GB

## <a name="next-steps"></a>Volgende stappen

Zodra het Hallo-beveiliging is voltooid, kunt u proberen [failover](site-recovery-failover.md) toocheck of uw toepassing wordt weergegeven in Azure of niet.

Als u wilt dat toodisable beveiliging, controleren hoe te[opschonen registratie en protection-instellingen](site-recovery-manage-registration-and-protection.md)
