---
title: aaaRestore per virtuele machines van de back-up | Microsoft Docs
description: Meer informatie over hoe toorestore een virtuele machine van Azure vanaf een herstelpunt verwijzen
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: terugzetten van back-up. hoe toorestore; herstelpunt;
ms.assetid: fed877b3-b496-49fb-99e4-653be7c23e3a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: trinadhk; jimpark;
ms.openlocfilehash: 44c25f3248784accd1c2beaabb2c9a4dca3232d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-virtual-machines-in-azure"></a>Virtuele machines herstellen in Azure
> [!div class="op_single_selector"]
> * [Herstellen van virtuele machines in Azure-portal](backup-azure-arm-restore-vms.md)
> * [Herstellen van virtuele machines in de klassieke portal](backup-azure-restore-vms.md)
>
>

Herstellen van een virtuele machine tooa nieuwe virtuele machine vanuit Hallo back-ups die zijn opgeslagen in een Azure Backup-kluis Hello te volgen stappen.

> [!IMPORTANT]
> U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden. Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.<br/> **15 oktober 2017**, u niet langer kunnen toouse PowerShell toocreate Backup-kluizen. <br/> **Vanaf 1 november 2017**:
>- Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.
>- U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo. In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.
>

## <a name="restore-workflow"></a>Werkstroom herstellen
### <a name="step-1-choose-an-item-toorestore"></a>Stap 1: Kies een item toorestore
1. Navigeer toohello **beveiligde Items** tabblad en selecteer de virtuele machine die u wilt dat toorestore tooa Hallo nieuwe virtuele machine.

    ![Beveiligde items](./media/backup-azure-restore-vms/protected-items.png)

    Hallo **herstelpunt** kolom in Hallo **beveiligde Items** pagina vertelt u Hallo aantal herstelpunten voor een virtuele machine. Hallo **nieuwste herstelpunt** kolom ziet u Hallo Hallo meest recente back-up van waaruit een virtuele machine kunnen worden hersteld.
2. Klik op **herstellen** tooopen hello **een Item terugzetten** wizard.

    ![Een item terugzetten](./media/backup-azure-restore-vms/restore-item.png)

### <a name="step-2-pick-a-recovery-point"></a>Stap 2: Kies een herstelpunt
1. In Hallo **Selecteer een herstelpunt** scherm, u kunt herstellen van de meest recente herstelpunt hello, of van een eerder punt in tijd. Hallo standaardoptie ingeschakeld wanneer de wizard wordt geopend is *nieuwste herstelpunt*.

    ![Selecteer een herstelpunt](./media/backup-azure-restore-vms/select-recovery-point.png)
2. toopick een eerder punt in tijd, kies Hallo **Selecteer datum** optie Hallo vervolgkeuzelijst en selecteer een datum in Hallo kalenderbesturingselement door te klikken op Hallo **pictogram Agenda**. Hallo-controle alle datums waarvoor herstelpunten worden gevuld met een lichte grijze tint en kunnen worden geselecteerd door de gebruiker Hallo.

    ![Selecteer een datum](./media/backup-azure-restore-vms/select-date.png)

    Nadat u op een datum in kalenderbesturingselement hello, herstelpunten Hallo beschikbaar op dat de datum in recovery punten in de volgende tabel worden weergegeven. Hallo **tijd** kolom wordt aangegeven op welke Hallo momentopname werd gemaakt Hallo-tijd. Hallo **Type** kolom ziet u Hallo [consistentie](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points) Hallo herstelpunt werd gemaakt. Hallo tabelkoptekst ziet u het aantal herstelpunten beschikbaar Hallo op die dag tussen haakjes.

    ![Herstelpunten](./media/backup-azure-restore-vms/recovery-points.png)
3. Selecteer Hallo herstelpunt in Hallo **herstelpunten** tabel en klik op volgende pijl toogo toohello volgende welkomstscherm.

### <a name="step-3-specify-a-destination-location"></a>Stap 3: Geef een bestemmingslocatie
1. In Hallo **Selecteer terugzetten exemplaar** scherm Geef details op van het waar toorestore Hallo voor virtuele machine.

   * Geef de naam van de virtuele machine Hallo: In een bepaalde cloud-service, de naam van de virtuele machine Hallo moet uniek zijn. Bestaande VM te veel schrijven ondersteund niet.
   * Selecteer een cloudservice voor Hallo VM: dit is verplicht voor het maken van een virtuele machine. U kunt kiezen tooeither gebruik een bestaande cloudservice of maak een nieuwe cloudservice.

        De naam van de cloudservice wordt gekozen moet globaal uniek zijn. Normaal gesproken Hallo cloudservicenaam gekoppeld aan een openbare URL in de vorm Hallo van [cloudservice] opgehaald. cloudapp.net. Azure kunt niet u een nieuwe cloudservice toocreate als Hallo naam wordt al gebruikt. Als u op een nieuwe cloudservice toocreate kiest, worden deze naam verzameld moet gegeven Hallo dezelfde naam als Hallo virtuele machine – in welk geval Hallo VM cloudservice voor unieke genoeg toobe toegepast toohello die zijn gekoppeld.

        We alleen cloud-services worden weergegeven en virtuele netwerken die niet gekoppeld aan een affiniteitsgroepen in Hallo zijn gegevens over exemplaar herstellen. [Meer informatie](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
2. Selecteer een opslagaccount voor Hallo VM: dit is verplicht voor het maken van Hallo VM. U kunt kiezen uit bestaande opslagaccounts in Hallo dezelfde regio bevinden als hello Azure Backup-kluis. Storage-accounts die Zone redundant of van het type Premium-opslag zijn ondersteund niet.

    Als er geen opslagaccounts met een ondersteunde configuratie, maakt u een opslagaccount van de ondersteunde configuratie voorafgaande toostarting restore-bewerking.

    ![Een virtueel netwerk selecteren](./media/backup-azure-restore-vms/restore-sa.png)
3. Een virtueel netwerk selecteert: Hallo virtueel netwerk (VNET) voor Hallo virtuele machine moet worden geselecteerd op moment van het maken van Hallo Hallo VM. Hallo herstellen UI toont alle Hallo VNETs binnen dit abonnement die kunnen worden gebruikt. Dit is niet verplicht een VNET tooselect voor Hallo hersteld VM – kunt u zich kunt tooconnect toohello hersteld virtuele machine via Hallo internet zelfs als hello VNET is niet toegepast.

    Als Hallo cloud is geselecteerd-service is gekoppeld aan een virtueel netwerk, en vervolgens kunt u het virtuele netwerk Hallo niet wijzigen.

    ![Een virtueel netwerk selecteren](./media/backup-azure-restore-vms/restore-cs-vnet.png)
4. Selecteer een subnet: als Hallo VNET over subnetten, standaard het eerste subnet hello wordt geselecteerd. Kies Hallo subnet van uw keuze uit Hallo dropdown-opties. Ga voor subnet informatie tooNetworks-extensie in de Hallo [portal startpagina](https://manage.windowsazure.com/), gaat u te**virtuele netwerken** en selecteer Hallo virtueel netwerk en inzoomen naar configureren toosee subnetgegevens.

    ![Een subnet selecteren](./media/backup-azure-restore-vms/select-subnet.png)
5. Klik op Hallo **indienen** pictogram in Hallo wizard toosubmit Hallo details en een hersteltaak maken.

## <a name="track-hello-restore-operation"></a>Hallo-herstelbewerking bijhouden
Zodra u hebt alle Hallo-informatie in de wizard Systeemherstel Hallo invoeren en deze ingediend probeert Azure Backup toocreate een taak tootrack Hallo restore-bewerking.

![Er wordt een taak terugzetten](./media/backup-azure-restore-vms/create-restore-job.png)

Als het Hallo-taak maken is voltooid, ziet u een toast-melding die aangeeft dat Hallo-taak is gemaakt. U kunt meer informatie krijgen door te klikken op Hallo **taak weergeven** knop die u te gaat**taken** tabblad.

![Herstellen van de taak is gemaakt](./media/backup-azure-restore-vms/restore-job-created.png)

Zodra het Hallo-herstelbewerking is voltooid, wordt gemarkeerd als voltooid in de **taken** tabblad.

![Herstellen van de taak is voltooid](./media/backup-azure-restore-vms/restore-job-complete.png)

Nadat het herstellen van virtuele machine moet u mogelijk toore-Installeer Hallo extensies op Hallo Hallo oorspronkelijke VM en [Hallo eindpunten wijzigen](../virtual-machines/windows/classic/setup-endpoints.md) voor Hallo virtuele machine in hello Azure-portal.

## <a name="post-restore-steps"></a>Stappen na herstellen
Als u van een cloud-init op basis van Linux-distributie zoals Ubuntu, uit veiligheidsoverwegingen gebruikmaakt, wachtwoord geblokkeerd boeken terugzetten. Neem hersteld gebruik VMAccess-extensie op Hallo VM te[Hallo-wachtwoord opnieuw instellen](../virtual-machines/linux/classic/reset-access.md). U wordt aangeraden met behulp van SSH-sleutels op deze distributies tooavoid opnieuw instellen van wachtwoord post terugzetten.

## <a name="backup-for-restored-vms"></a>Back-up voor de herstelde virtuele machines
Als u VM toosame-cloudservice met dezelfde naam als het oorspronkelijk back-up VM Hallo hebt teruggezet, wordt back-up voortgezet op Hallo VM post terugzetten. Als u hebt hersteld VM tooa andere cloudservice of een andere naam voor de herstelde virtuele machine wordt opgegeven, wordt dit beschouwd als een nieuwe virtuele machine en moet u toosetup back-up voor de herstelde virtuele machine.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Herstellen van een virtuele machine tijdens Azure DataCenter na noodgevallen
Azure Backup kan herstellen van een back-up VMs toohello gekoppeld Datacenter geval Hallo primaire datacenters waarin VM's worden uitgevoerd na noodgevallen ervaringen en u back-up kluis toobe geografisch redundante geconfigureerd. Tijdens deze scenario's, moet u een opslagaccount die aanwezig is in een gekoppeld Datacenter tooselect en rest van het herstelproces Hallo blijft hetzelfde. Azure Backup maakt gebruik van Compute-service van de gekoppelde geo toocreate Hallo hersteld virtuele machine. Meer informatie over [Azure Data center tolerantie](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Domain Controller virtuele machines herstellen
Back-up van de domeincontroller (DC) virtuele machines is een ondersteund scenario met Azure Backup. Maar wees voorzichtig tijdens het terugzetten van een Hallo. de juiste herstelproces Hallo is afhankelijk van Hallo-structuur van Hallo-domein. In de meest eenvoudige geval Hallo hebt u een enkele DC in één domein. Meer vaak voor productie-belastingen hebt u één domein met meerdere DC's, mogelijk met sommige domeincontrollers on-premises. Mogelijk hebt u ten slotte een forest met meerdere domeinen.

Vanuit een Active Directory perspectief hello is Azure VM net als elke andere virtuele machine op een moderne ondersteunde hypervisor. Hallo belangrijk verschil met lokale hypervisors is dat er geen VM-console beschikbaar in Azure is. Er is een console vereist voor bepaalde scenario's zoals herstellen met behulp van een Bare Metal Recovery (BMR) type back-up. Virtuele machine herstellen vanuit back-upkluis Hallo is echter een volledige vervanging voor BMR. Active Directory Restore Mode (DSRM) is ook beschikbaar is, zodat alle Active Directory herstelscenario's mogelijk of gewenst zijn is. Zie voor meer achtergrondinformatie [back-up en herstellen van de overwegingen voor gevirtualiseerde domeincontrollers](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) en [plannen voor herstel van Active Directory-Forest](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).

### <a name="single-dc-in-a-single-domain"></a>Enkele DC in één domein
Hallo VM kan worden hersteld (zoals VM) vanuit hello Azure portal of met behulp van PowerShell.

### <a name="multiple-dcs-in-a-single-domain"></a>Meerdere domeincontrollers in één domein
Wanneer andere DC's van hetzelfde domein kan worden bereikt via Hallo hello netwerk, kan Hallo DC zoals een VM worden hersteld. Als het laatste resterende DC in domein Hallo hello of een herstel in een geïsoleerd netwerk wordt uitgevoerd, kan een herstelprocedure forest moet worden gevolgd.

### <a name="multiple-domains-in-one-forest"></a>Meerdere domeinen in een forest
Wanneer andere DC's van hetzelfde domein kan worden bereikt via Hallo hello netwerk, kan Hallo DC zoals een VM worden hersteld. In alle andere gevallen wordt een forestherstel echter aanbevolen.

<!--- WK: this following original supportability statement is incorrect, taking it out.
hello challenge arises because DSRM mode is not present in Azure. So toorestore such a VM, you cannot use hello Azure portal. hello only supported restore mechanism is disk-based restore using PowerShell.

> [!WARNING]
> For Domain Controller VMs in a multi-DC environment, do not use hello Azure portal for restore! Only PowerShell based restore is supported
>
>

Read more about hello [USN rollback problem](https://technet.microsoft.com/library/dd363553) and hello strategies suggested toofix it.
--->

## <a name="restoring-vms-with-special-network-configurations"></a>Herstellen van virtuele machines met speciale netwerkconfiguraties
Azure Backup ondersteunt back-up voor speciale configuraties van virtuele machines te volgen.

* VM's onder de load balancer (intern en extern)
* Virtuele machines met meerdere gereserveerde IP 's
* Virtuele machines met meerdere NIC 's

Deze configuraties verplichten na overwegingen bij het terugzetten.

> [!TIP]
> Gebruik PowerShell gebaseerd terugzetten stroom toorecreate Hallo speciale netwerkconfiguratie van virtuele machines post terugzetten.
>
>

### <a name="restoring-from-hello-ui"></a>Terugzetten van Hallo gebruikersinterface:
Tijdens het terugzetten van de gebruikersinterface, **Kies altijd een nieuwe cloudservice**. Houd er rekening mee dat sinds portal slechts verplichte duurt parameters tijdens herstel flow, virtuele machines die zijn teruggezet met behulp van de gebruikersinterface verliest speciale netwerkconfiguratie Hallo die ze beschikken. Terugzetten van virtuele machines worden met andere woorden, normale virtuele machines zonder configuratie van load balancer of meerdere NIC of meerdere gereserveerde IP-adres.

### <a name="restoring-from-powershell"></a>Terugzetten vanuit PowerShell:
PowerShell heeft Hallo mogelijkheid toojust Hallo VM schijven herstellen vanuit back-up en Hallo virtuele machine niet worden gemaakt. Dit is handig bij het herstellen van virtuele machines waarvoor speciale netwerkconfiguraties hierboven vermeld.

In de volgorde toofully Hallo virtuele machine na het herstellen van de schijven opnieuw te maken, als volgt te werk:

1. Hallo schijven herstellen vanuit back-upkluis met [Azure back-PowerShell](backup-azure-vms-classic-automation.md#restore-an-azure-vm)
2. Hallo VM-configuratie is vereist voor de load balancer maken / meerdere NIC/meerdere gereserveerde IP-met behulp van PowerShell-cmdlets Hallo en deze toocreate Hallo VM van de gewenste configuratie gebruiken.

   * Virtuele machine maken in een cloudservice met [interne Load balancer](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Te maken van VM tooconnect[Internet gerichte load balancer](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * Met virtuele machine maken [meerdere NIC's](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * Met virtuele machine maken [meerdere gereserveerde IP-adressen](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Volgende stappen
* [Het oplossen van problemen](backup-azure-vms-troubleshoot.md#restore)
* [Virtuele machines beheren](backup-azure-manage-vms.md)
