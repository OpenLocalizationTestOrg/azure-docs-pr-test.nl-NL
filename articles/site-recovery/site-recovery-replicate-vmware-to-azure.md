---
title: Toepassingen (VMware naar Azure) repliceren | Microsoft Docs
description: Dit artikel wordt beschreven hoe u de replicatie van virtuele machines waarop VMware naar Azure instelt.
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
ms.openlocfilehash: e0047a996c9bfd7d950b32f0871ddd7608924b42
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-applications-running-on-vmware-vms-to-azure"></a>Toepassingen die worden uitgevoerd op virtuele VMware-machines naar Azure repliceren



Dit artikel wordt beschreven hoe u de replicatie van virtuele machines waarop VMware naar Azure instelt.
## <a name="prerequisites"></a>Vereisten

Het artikel wordt ervan uitgegaan dat u al hebt

1.  [On-premises gegevensbron omgeving instellen](site-recovery-set-up-vmware-to-azure.md)
2.  [De doelomgeving instellen in Azure](site-recovery-prepare-target-vmware-to-azure.md)


## <a name="enable-replication"></a>Replicatie inschakelen
#### <a name="before-you-start"></a>Voordat u begint
Houd rekening met het volgende bij het repliceren van virtuele VMware-machines:

* Uw Azure gebruikersaccount moet zijn bepaalde [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) replicatie van een nieuwe virtuele machine naar Azure in te schakelen.
* Virtuele VMware-machines worden gedetecteerd om de 15 minuten. Het duurt 15 minuten of langer voordat ze worden weergegeven in de portal na de detectie. Evenzo detectie kunt 15 minuten of langer duren wanneer u een nieuwe vCenter-server of vSphere host toevoegt.
* Omgevingswijzigingen op de virtuele machine (zoals VMware tools-installatie) kunnen duren voordat de 15 minuten of langer worden bijgewerkt in de portal.
* U kunt de laatste keer dat gedetecteerde controleren op virtuele VMware-machines in de **laatste Contact op** veld voor de vCenter-server/vSphere-host op de **configuratieservers** blade.
* Als u wilt toevoegen machines voor replicatie zonder te wachten op de geplande detectie, markeer de configuratieserver (Klik niet op deze), en klik op de **vernieuwen** knop.
* Wanneer u replicatie inschakelt als de machine is voorbereid, installeert de processerver automatisch de Mobility-service op deze.


**Schakel replicatie nu als volgt**:

1. Klik op **Stap 2: toepassing repliceren** > **Bron**. Wanneer u replicatie voor het eerst inschakelt, klikt u in de kluis op **+Repliceren** om replicatie in te schakelen voor aanvullende machines.
2. In de **bron** blade > **bron**, selecteer de configuratieserver.
3. In **type Machine**, selecteer **virtuele Machines** of **fysieke Machines**.
4. In **vCenter/vSphere-Hypervisor**, selecteert u de vCenter-server die de host vSphere beheert of Selecteer de host. Deze instelling niet relevant als u fysieke machines repliceert.
5. Selecteer de processerver. Dit is de naam van de configuratieserver als u geen processervers extra hebt gemaakt. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. In **doel** Selecteer het abonnement en de resourcegroep waar u de mislukte over virtuele machines maken. Kies het implementatiemodel dat u wilt gebruiken in Azure (klassiek of resourcebeheer) voor de failover-VM's.
7. Selecteer de Azure storage-account dat u gebruiken wilt voor het repliceren van gegevens. Opmerking:

   * U kunt een premium- of standard-opslagaccount selecteren. Als u een premium-account selecteert, moet u een extra standard storage-account voor lopende replicatielogboeken opgeven. Accounts moeten in dezelfde regio bevinden als de Recovery Services-kluis.
   * Als u gebruiken een ander opslagaccount dan die u hebt wilt, kunt u een*tijdelijke aanduiding voor koppeling voor het maken van de storage-account met behulp van resource manager die worden behandeld in aan de slag*. Klik op om een opslagaccount met Resource Manager **nieuw**. Als u een opslagaccount wilt maken op basis van het klassieke model, doet u dat [in Azure Portal](../storage/common/storage-create-storage-account.md).

8. Selecteer de Azure-netwerk en subnet waarmee virtuele Azure-machines verbinding maken, wanneer ze zijn gemaakt na een failover. Het netwerk moet zich in dezelfde regio bevinden als de Recovery Services-kluis. Selecteer **Nu configureren voor geselecteerde machines** om de netwerkinstelling toe te passen op alle machines die u voor beveiliging selecteert. Selecteer **Later configureren** om per machine een Azure-netwerk te selecteren. Als u een netwerk hebt, moet u [maken van een](#set-up-an-azure-network). Klik op om een netwerk met Resource Manager **nieuw**. Als u een netwerk wilt maken op basis van het klassieke model, doet u dat [in Azure Portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Selecteer indien van toepassing een subnet. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. Selecteer in **Virtuele machines** > **Virtuele machines selecteren** alle machines die u wilt repliceren. U kunt alleen machines selecteren waarvoor replicatie kan worden ingeschakeld. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. In **eigenschappen** > **eigenschappen configureren**, selecteer het account dat wordt gebruikt door de processerver voor het installeren van de Mobility-service automatisch op de machine.  
11. Standaard zijn alle schijven worden gerepliceerd. Als u wilt schijven uitsluiten van replicatie, klikt u op **alle schijven** en wis alle schijven die u niet wilt repliceren.  Klik vervolgens op **OK**. Later kunt u eventueel extra eigenschappen instellen. [Meer informatie](site-recovery-exclude-disk.md) over het uitsluiten van schijven.

    ![Replicatie inschakelen](./media/site-recovery-vmware-to-azure/enable-replication6.png)

12. In **replicatie-instellingen** > **replicatie-instellingen configureren**, Controleer of de juiste replicatiebeleid is geselecteerd. U kunt replicatie-beleidsinstellingen in wijzigen **instellingen** > **replicatiebeleid** > beleidsnaam > **instellingen bewerken**. Wijzigingen die u op een beleid toepast wordt toegepast op replicerende en nieuwe machines.
13. Schakel **consistentie tussen meerdere VM's** als u wilt verzamelen machines in een replicatiegroep en geef een naam voor de groep. Klik vervolgens op **OK**. Opmerking:

    * Computers in de replicatie repliceren groeperen en gedeelde crashconsistent en toepassingsconsistente herstelpunten wanneer ze een failover.
    * Het is raadzaam dat u verzamelen virtuele machines en fysieke servers zodat ze uw werkbelastingen. Inschakelen multi-VM consistentie kan invloed hebben op prestaties workload en mag alleen worden gebruikt als machines dezelfde werkbelasting worden uitgevoerd en moet u de consistentie.

    ![Replicatie inschakelen](./media/site-recovery-vmware-to-azure/enable-replication7.png)
14. Klik op **replicatie inschakelen**. U kunt de voortgang van volgen de **beveiliging inschakelen** taak **instellingen** > **taken** > **Site Recovery-taken**. Nadat de taak **Beveiliging voltooien** is uitgevoerd, is de machine klaar voor een mogelijke failover.

> [!NOTE]
> Als de machine is klaar voor de push-installatie die wordt het onderdeel van de Mobility-service geïnstalleerd wanneer beveiliging is ingeschakeld. Na het onderdeel wordt geïnstalleerd op de machine die een beveiligingstaak wordt gestart en mislukt. Na de fout moet u elke computer handmatig opnieuw te starten. Na het opnieuw opstarten de beveiligingstaak opnieuw begint en initiële replicatie plaatsvindt.
>
>

## <a name="view-and-manage-vm-properties"></a>Eigenschappen van virtuele machines weergeven en beheren

Het is raadzaam om de eigenschappen van de bronmachine te controleren. Houd er rekening mee dat de naam van de virtuele Azure-machine moet voldoen aan de [vereisten voor virtuele machines van Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. Klik op **instellingen** > **gerepliceerde items** >, en selecteer de machine. De **Essentials** blade ziet u informatie over machines instellingen en status.
2. In **Eigenschappen** kunt u de replicatie- en failoverinformatie van de virtuele machine weergeven.
3. In **Berekening en netwerk** > **Eigenschappen berekenen** kunt u de naam van de virtuele Azure-machine opgeven, evenals de doelgrootte. De naam om te voldoen aan de Azure-vereisten als u wilt wijzigen.
    ![Replicatie inschakelen](./media/site-recovery-vmware-to-azure/VMProperties_AVSET.png)
 
4.  Kunt u een [resourcegroep](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-resource-groups-guidelines) van welke machine wordt nu deel uit van na een failover. U kunt deze altijd vóór mislukken instelling via wijzigen. Na een failover, als u de machine naar een andere resourcegroep migreert en vervolgens verbreekt de beveiligingsinstellingen van een machine.
5. Kunt u een [beschikbaarheidsset](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) als de computer moet worden opgenomen als onderdeel van een bericht failover. Tijdens het instellen van de beschikbaarheid van de te selecteren, neem Houd rekening met:

    * Alleen beschikbaarheidssets die horen bij de opgegeven resourcegroep wordt weergegeven  
    * Computers met verschillende virtuele netwerken mag geen deel uit van dezelfde beschikbaarheidsset
    * Alleen virtuele machines met een grootte van dezelfde kan een deel uitmaken van dezelfde beschikbaarheidsset
5. U kunt ook bekijken en informatie over het doelnetwerk, subnet en IP-adres dat wordt toegewezen aan de Azure VM toevoegen.
6. In **schijven**, ziet u het besturingssysteem en gegevensschijven op de virtuele machine die wordt gerepliceerd.

### <a name="network-adapters-and-ip-addressing"></a>Netwerkadapters en IP-adressering 

- U kunt het doel-IP-adres instellen. Als u geen adres opgeeft, maakt de machine waarvoor een failover is uitgevoerd, gebruik van DHCP. Als u een adres dat is niet beschikbaar bij een failover, werkt de failover niet. Hetzelfde doel-IP-adres kan worden gebruikt voor een testfailover als het adres beschikbaar is in het testfailovernetwerk.
- Het aantal netwerkadapters wordt bepaald door de grootte die u voor de virtuele doelmachine opgeeft. Dat werkt als volgt:
    - Als het aantal netwerkadapters op de bronmachine kleiner is dan of gelijk is aan het aantal adapters dat is toegestaan voor de grootte van de doelmachine, heeft het doel hetzelfde aantal adapters als de bron.
    - Als het aantal adapters op de virtuele bronmachine groter is dan voor de doelgrootte is toegestaan, wordt het maximum voor de doelgrootte gebruikt.
    - Als de bronmachine bijvoorbeeld twee netwerkadapters heeft en de grootte van de doelmachine vier netwerkadapters ondersteunt, heeft de doelmachine twee adapters. Als de bronmachine twee adapters heeft, maar met de ondersteunde doelgrootte slechts één wordt ondersteund, heeft de doelcomputer slechts één adapter.
    - Als de virtuele machine meerdere netwerkadapters die worden deze allemaal verbonden met hetzelfde netwerk heeft.
    - Als de virtuele machine meerdere netwerkadapters heeft dan het eerste beheerpunt dat wordt weergegeven in de lijst wordt de *standaard* netwerkadapter in de virtuele machine van Azure.
   



## <a name="common-issues"></a>Algemene problemen

* Elke schijf moet minder dan 1TB groot zijn.
* De besturingssysteemschijf moet een standaardschijf zijn, geen dynamische schijf
* Voor virtuele machines waarop Generation 2/UEFI is ingeschakeld, moet Windows de besturingssysteemgroep zijn en de opstartschijf moet minder dan 300 GB groot zijn

## <a name="next-steps"></a>Volgende stappen

Zodra de beveiliging is voltooid, kunt u proberen [failover](site-recovery-failover.md) om te controleren of uw toepassing weergegeven in Azure of niet wordt.

Als u uitschakelen, beveiliging wilt, Controleer het [opschonen registratie en protection-instellingen](site-recovery-manage-registration-and-protection.md)
