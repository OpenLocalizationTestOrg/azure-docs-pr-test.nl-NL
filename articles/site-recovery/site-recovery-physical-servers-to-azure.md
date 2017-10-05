---
title: Fysieke servers repliceren naar Azure | Microsoft Docs
description: Hierin wordt beschreven hoe u Azure Site Recovery implementeert om replicatie, failovers en herstel van on-premises Windows of Linux fysieke servers naar Azure indelen met behulp van de Azure-portal
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: physical-walkthrough-overview
ms.openlocfilehash: a9655ce1540c788d02d178eb619d2051cddda1c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
---
# <a name="replicate-physical-machines-to-azure-by-using-site-recovery"></a>Fysieke machines repliceren naar Azure met behulp van Site Recovery


In dit artikel wordt beschreven hoe lokale fysieke machines repliceren naar Azure met behulp van de Azure Site Recovery-service in de Azure-portal.

Als u wilt migreren van fysieke machines naar Azure (alleen failover), Lees [migreren naar Azure met Site Recovery](site-recovery-migrate-to-azure.md) voor meer informatie.

Opmerkingen en vragen boeken aan de onderkant van dit artikel of op de [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Vereisten

**Vereiste voor ondersteuning** | **Details**
--- | ---
**Azure** | Meer informatie over [Azure-vereisten](site-recovery-prereq.md#azure-requirements).
**On-premises configuratieserver** | Lokale machine (fysieke of VMware-VM) met Windows Server 2012 R2 of hoger. U instellen de configuratieserver tijdens de implementatie van Site Recovery.<br/><br/> Standaard worden de processerver en de hoofddoelserver ook geïnstalleerd op deze machine. Wanneer u opschalen, moet u mogelijk een afzonderlijk proces-server en heeft dezelfde vereisten als de configuratieserver.<br/><br/> Meer informatie over deze onderdelen in [de bronomgeving instellen](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).
**On-premises virtuele machines** | Computers die u wilt repliceren, moeten worden uitgevoerd een [ondersteund besturingssysteem](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) en voldoet aan de [vereisten voor Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URL 's** | De configuratieserver heeft toegang tot deze URL's:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Als u IP-adressen gebaseerde firewallregels, zorg ervoor dat ze de communicatie met Azure toestaan.<br/></br> Sta de [IP-adresbereiken voor Azure Datacenter](https://www.microsoft.com/download/confirmation.aspx?id=41653) en de HTTPS-poort (443) toe.<br/></br> IP-adresbereiken voor de Azure-regio van uw abonnement en voor VS-West (gebruikt voor beheer en de identiteit van toegangsbeheer) toestaan.<br/><br/> Deze URL voor het downloaden van de MySQL toestaan: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Mobility-service** | Deze service is geïnstalleerd op elke machine die u wilt repliceren.

## <a name="limitations"></a>Beperkingen

**Beperking** | **Details**
--- | ---
**Azure** | Accounts voor opslag en netwerk moeten zich in dezelfde regio bevinden als de kluis.<br/><br/> Als u een premium storage-account gebruikt, moet u ook een standaard store-account voor het opslaan van replicatielogboeken.<br/><br/> U kan naar de premium-accounts in het midden- en Zuid, India repliceren.
**On-premises configuratieserver** | Als u de configuratieserver op een VMware-VM installeert, moet het VM-adaptertype VMXNET3. Dit niet het geval is, [Installeer deze update](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).<br/><br/> Als u een VM VMware, moet vSphere PowerCLI 6.0 worden geïnstalleerd.<br/><br> De machine mag niet een domeincontroller zijn.<br/><br/> De machine moet een statisch IP-adres hebben.<br/><br/> De hostnaam moet 15 tekens of korter is, en het besturingssysteem moet in het Engels.
**Gerepliceerde machines** | Controleer of [beperkingen van de virtuele machine van Azure](site-recovery-prereq.md#azure-requirements).<br/><br/> Als u inschakelen van meerdere VM-consistentie waarmee machines met dezelfde werkbelasting wilt wilt herstellen, samen met een punt consistente gegevens, opent u poort 20004 op de computer.<br/><br/> Specifieke typen [Linux opslag](site-recovery-support-matrix-to-azure.md#support-for-storage) worden ondersteund.
**Failback** | U kunt geen failback van Azure aan een fysieke machine. Als u wilt dat naar on-premises mislukken na een failover, moet u een VMware-omgeving zodat u weer aan een VMware-VM kan uitvallen.


## <a name="set-up-azure"></a>Instellen van Azure

1. [Een Azure-netwerk instellen](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

      a. Virtuele machines in Azure worden geplaatst in dit netwerk wanneer ze zijn gemaakt na een failover.

      b. U kunt een Azure-netwerk instellen [Resource Manager](../resource-manager-deployment-model.md) of in de klassieke modus.

2. Instellen van een [Azure storage-account](../storage/storage-create-storage-account.md#create-a-storage-account) voor gerepliceerde gegevens.

    a. Het account kan worden standaard of [premium](../storage/storage-premium-storage.md).

    b. U kunt een account in Resource Manager of in de klassieke modus ingesteld.

## <a name="prepare-the-configuration-server"></a>De configuratieserver voorbereiden

1. Installeer Windows Server 2012 R2 of later op een on-premises fysieke server of een VMware-VM.

2. Zorg ervoor dat de computer toegang heeft tot de URL's die worden vermeld in [vereisten](#prerequisites).

## <a name="prepare-for-mobility-service-installation"></a>Voorbereiden voor de installatie van de Mobility-service

Als u pushen van de Mobility-service naar een fysieke computer wilt, moet u een account dat toegang tot de machines kan worden gebruikt door de processerver. Het account wordt alleen gebruikt voor de push-installatie. U kunt een domein of lokale account gebruiken:

  - Als u niet een domeinaccount voor Windows moet u externe gebruiker toegangsbeheer op de lokale computer uitschakelen. Om dit te doen, in het register onder **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, de DWORD-vermelding toevoegen **LocalAccountTokenFilterPolicy**, met een waarde van 1. Als u wilt de registervermelding voor Windows uit een opdrachtregelinterface toevoegen, typt u:

        ``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
  - Voor Linux moet het account een Hoofdgebruiker op de bronserver Linux zijn.


## <a name="create-a-recovery-services-vault"></a>Een Recovery Services-kluis maken

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="select-the-protection-goal"></a>Het beveiligingsdoel selecteren

Selecteer wat u wilt repliceren en waar u naar wilt repliceren.

1. Klik op **Recovery Services-kluizen** > **kluis**.
2. Op de **Resource** menu, klikt u op **siteherstel** > **infrastructuur voorbereiden** > **beveiligingsdoel** .

    ![Doelstellingen kiezen](./media/site-recovery-vmware-to-azure/choose-goal-physical.PNG)

3. In **beveiligingsdoel**, selecteer **naar Azure** > **niet gevirtualiseerde / andere**.


## <a name="set-up-the-source-environment"></a>De bronomgeving instellen

Instellen van de configuratieserver, registreert u dit in de kluis en VM's detecteren.

1. Klik op **Site Recovery** > **infrastructuur voorbereiden** > **bron**.
2. Als u een configuratieserver geen hebt, klikt u op **+ configuratieserver**.

    ![Bron instellen](./media/site-recovery-vmware-to-azure/set-source1.png)

3. In **Server toevoegen**, controleert u of **configuratieserver** wordt weergegeven in **servertype**.
4. Download de **Unified installatie van Site Recovery** -bestand voor installatie.
5. Download de **kluisregistratiesleutel**. Wanneer u Setup Unified uitvoert moet u deze sleutel. De sleutel blijft vijf dagen na het genereren ervan geldig.

   ![Bron instellen](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Voer Site Recovery Unified Setup

Voordat u begint, het volgende doen:

- Een snelle video-overzicht ophalen. (De video wordt beschreven hoe u virtuele VMware-machines repliceren, maar het proces is vergelijkbaar voor replicatie van fysieke machine.)

    > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

- Op de servercomputer van de configuratie, zorg ervoor dat de systeemklok is gesynchroniseerd met een [tijdserver](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Als het op de voorgrond 15 minuten of achter de installatie mislukken.
- Voer Setup uit als lokale beheerder op de servercomputer van de configuratie.
- Zorg ervoor dat TLS 1.0 op de machine is ingeschakeld.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> De configuratieserver kan ook worden geïnstalleerd [vanaf de opdrachtregel](http://aka.ms/installconfigsrv).


## <a name="set-up-the-target-environment"></a>De doelomgeving instellen

Controleer voordat u de doelomgeving instellen, om ervoor te zorgen dat u hebt een [Azure storage-account en het netwerk](#set-up-azure).

1. Klik op **infrastructuur voorbereiden** > **doel**, en selecteer het Azure-abonnement u wilt gebruiken.
2. Opgeven of de doel-implementatiemodel Resource Manager of klassiek.
3. Site Recovery wordt gecontroleerd om ervoor te zorgen dat u een of meer compatibele Azure storage-accounts en netwerken hebt.

   ![doel](./media/site-recovery-vmware-to-azure/gs-target.png)

4. Als u een opslagaccount of een netwerk dat nog niet hebt gemaakt, klikt u op **+ opslagaccount** of **+ netwerk** voor het maken van een Resource Manager-account of inline-netwerk.

## <a name="set-up-replication-settings"></a>Replicatie-instellingen instellen

Voordat u begint, krijgt u een snelle video overzicht. (De video wordt beschreven hoe u virtuele VMware-machines repliceren, maar het proces is vergelijkbaar voor replicatie van fysieke machine.)

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. Klik op om een nieuw beleid voor wachtwoordreplicatie **Site Recovery-infrastructuur** > **replicatiebeleid** > **+ replicatiebeleid**.
2. In **maken van beleid voor wachtwoordreplicatie**, een beleidsnaam opgeven.
3. Geef de limiet voor de RPO op bij **RPO-drempelwaarde**. Deze waarde geeft aan hoe vaak gegevens herstelpunten worden gemaakt. Een waarschuwing wordt gegenereerd als continue replicatie deze limiet overschrijdt.
4. In **herstel bewaarperiode**, opgeven (in uren) hoe lang de bewaarperiode voor elk herstelpunt. Gerepliceerde virtuele machines kunnen worden hersteld naar een willekeurig punt in een venster. Maximaal 24 uur bewaren wordt ondersteund voor computers die zijn gerepliceerd naar de premium-opslag. Tot 72 uur bewaren wordt ondersteund voor computers die zijn gerepliceerd naar de standard-opslag.
5. In **App-consistente momentopname frequentie**, opgeven hoe vaak (in minuten) herstelpunten met toepassingsconsistente momentopnamen worden gemaakt. Klik op **OK** om het beleid te maken.

    ![Beleid voor replicatie](./media/site-recovery-vmware-to-azure/gs-replication2.png)

6. Wanneer u een nieuw beleid maakt, wordt dit automatisch gekoppeld met de configuratieserver. Standaard wordt automatisch een overeenkomende beleid gemaakt voor failback. Bijvoorbeeld, als het replicatiebeleid **rep beleid**, dan is het failbackbeleid voor **rep-beleid-failback**. Dit beleid wordt niet gebruikt, totdat u een failback vanuit Azure initiëren.  


## <a name="plan-capacity"></a>Plannen van capaciteit

1. Nu dat u uw basisinfrastructuur instellen hebt, kunt u nadenkt over capaciteitsplanning en nagaan of u aanvullende resources nodig. [Meer informatie](site-recovery-plan-capacity-vmware.md).
2. Wanneer u met het plannen van capaciteit bent klaar, selecteert u **Ja** in **hebt u capaciteit plannen?**

   ![Capaciteitsplanning](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Virtuele machines voorbereiden voor replicatie

Alle machines die u wilt repliceren, moeten de Mobility-service geïnstalleerd hebben. U kunt de Mobility-service installeren op een aantal verschillende manieren:

- Installeer de service met een push-installatie van de processerver. U moet voorbereiden machines van tevoren aan deze methode gebruikt.
- Installeer de service met behulp van de implementatiehulpprogramma's zoals System Center Configuration Manager of Azure Automation Desired State Configuration.
- De service handmatig installeren.

[Meer informatie](site-recovery-vmware-to-azure-install-mob-svc.md).


## <a name="enable-replication"></a>Replicatie inschakelen

Voordat u begint:

- Uw Azure gebruikersaccount moet zijn bepaalde [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) replicatie van een nieuwe virtuele machine naar Azure in te schakelen.
- Wanneer u toevoegen of wijzigen van virtuele machines, kunnen er tot 15 minuten of langer wijzigingen van kracht te laten en ze kunnen worden weergegeven in de portal.
- U kunt de laatste keer dat gedetecteerde controleren voor virtuele machines in **configuratieservers** > **laatste Contact op**.
- Als u wilt toevoegen virtuele machines zonder te wachten op de geplande detectie, markeer de configuratieserver (Klik niet op deze), en klik op **vernieuwen**.
- Als een virtuele machine wordt voorbereid voor de push-installatie, de processerver wordt de Mobility-service geïnstalleerd wanneer u replicatie inschakelt.
- Een snelle video-overzicht ophalen. (De video wordt beschreven hoe u virtuele VMware-machines repliceren, maar het proces is vergelijkbaar voor replicatie van fysieke machine.)

    >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]


### <a name="exclude-disks-from-replication"></a>Schijven uitsluiten van replicatie

Standaard worden alle schijven op een machine gerepliceerd. U kunt schijven uitsluiten van replicatie. Bijvoorbeeld, u mogelijk niet naar wilt repliceren schijven met tijdelijke gegevens of gegevens die elk is vernieuwd wanneer een machine of de toepassing opnieuw wordt opgestart (bijvoorbeeld, pagefile.sys of SQL Server tempdb).

### <a name="replicate-vms"></a>Virtuele machines repliceren

1. Klik op **toepassing repliceren** > **bron**.
2. In **bron**, selecteer **On-premises**.
3. In **bronlocatie**, selecteert u de naam van de configuratie-server.
4. In **type Machine**, selecteer **fysieke Machines**.
5. In **processerver**, kies de processerver. Als u geen processervers extra hebt gemaakt, is deze server de configuratieserver. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/site-recovery-physical-to-azure/chooseVM.png)

6. In **doel**, selecteer de **abonnement** en de **resourcegroep** in die u wilt maken van de Azure VM's na een failover. Kies het implementatiemodel dat u wilt gebruiken in Azure (klassiek of Resource Manager) voor de failover-virtuele machines.

7. Selecteer de Azure storage-account dat u gebruiken wilt voor het repliceren van gegevens. Als u niet wilt gebruiken van een account dat u al hebt ingesteld, kunt u een nieuwe maken.

8. Selecteer de **Azure-netwerk** en **Subnet** waarmee virtuele Azure-machines verbinding maken na een failover. Selecteer **Nu configureren voor geselecteerde machines** om de netwerkinstelling toe te passen op alle machines die u voor beveiliging selecteert. Selecteer **Later configureren** om per machine een Azure-netwerk te selecteren. Als u niet dat een bestaand netwerk gebruiken wilt, kunt u een kunt maken.

    ![Replicatie inschakelen](./media/site-recovery-physical-to-azure/targetsettings.png)

9. In **fysieke machines**, klikt u op **+ fysieke machine** en voer de **naam** en **IP-adres**. Kies het besturingssysteem van de computer die u wilt repliceren. Het duurt enkele minuten totdat machines zijn gedetecteerd en weergegeven in de lijst.

    ![Replicatie inschakelen](./media/site-recovery-physical-to-azure/machineselect.png)

10. In **eigenschappen** > **eigenschappen configureren**, selecteer het account moet worden gebruikt door de processerver voor het installeren van de Mobility-service automatisch op de machine.
11. Standaard zijn alle schijven worden gerepliceerd. Klik op **alle schijven**, en wis alle schijven die u niet wilt repliceren. Klik vervolgens op **OK**. U kunt later meer VM-eigenschappen instellen.

    ![Replicatie inschakelen](./media/site-recovery-physical-to-azure/configprop.png)

12. In **replicatie-instellingen** > **replicatie-instellingen configureren**, Controleer of de juiste replicatiebeleid is geselecteerd. Als u een beleid wijzigt, worden de wijzigingen toegepast op de replicerende machine en nieuwe machines.
13. Schakel **consistentie tussen meerdere VM's** als u wilt verzamelen machines in een replicatiegroep en geef een naam voor de groep. Klik vervolgens op **OK**. Opmerking:

    a. Computers in de replicatiegroepen samen repliceren en de gedeelde crashconsistent en toepassingsconsistente herstelpunten wanneer ze een failover.

    b. Het is raadzaam dat u verzamelen virtuele machines en fysieke servers zodat ze uw werkbelastingen. Inschakelen van de consistentie tussen meerdere VM's kan werkbelasting prestaties beïnvloeden. Worden moet gebruikt als machines dezelfde werkbelasting worden uitgevoerd en moet u de consistentie.

    ![Replicatie inschakelen](./media/site-recovery-physical-to-azure/policy.png)

14. Klik op **replicatie inschakelen**. U kunt de voortgang van volgen de **beveiliging inschakelen** taak **instellingen** > **taken** > **Site Recovery-taken**. Nadat de taak **Beveiliging voltooien** is uitgevoerd, is de machine klaar voor een mogelijke failover.

Nadat u replicatie inschakelt, wordt de Mobility-service is geïnstalleerd als u push-installatie hebt ingesteld. Nadat de Mobility-service geïnstalleerd op een computer push is, wordt een beveiligingstaak wordt gestart en is mislukt. Na de fout moet u elke computer handmatig opnieuw te starten. De beveiligingstaak begint vervolgens opnieuw en initiële replicatie plaats.


### <a name="view-and-manage-azure-vm-properties"></a>Weergeven en beheren van Azure VM-eigenschappen

U wordt aangeraden dat u controleren of de VM-eigenschappen en breng eventuele wijzigingen die u nodig hebt.

1. Klik op **gerepliceerde items**, en selecteer de machine. De **Essentials** blade ziet u informatie over machines instellingen en status.
2. In **Eigenschappen** kunt u de replicatie- en failoverinformatie van de virtuele machine weergeven.
3. In **Berekening en netwerk** > **Eigenschappen berekenen** kunt u de naam van de virtuele Azure-machine opgeven, evenals de doelgrootte. Wijzig indien nodig de naam om te voldoen aan de [Azure-vereisten](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
4. Instellingen voor het doelnetwerk, subnet en IP-adres die zijn toegewezen aan de Azure VM wijzigen:

    a. U kunt het doel-IP-adres instellen.

    b.  Als u een adres niet opgeeft, gebruikt de failover-machine DHCP.

    c. Als u een adres dat is niet beschikbaar bij een failover, werkt failover niet.

    d. Hetzelfde doel-IP-adres kan worden gebruikt voor een testfailover als het adres beschikbaar is in het testfailovernetwerk.

    e. Het aantal netwerkadapters wordt bepaald door de grootte die u voor de virtuele doelmachine opgeeft:

     - Als het aantal netwerkadapters op de bronmachine hetzelfde als of kleiner is dan het aantal adapters dat is toegestaan voor de grootte van de doelmachine, wordt het doel hetzelfde aantal adapters als de bron heeft.
     - Als het aantal adapters op de virtuele bronmachine groter is dan voor de doelgrootte is toegestaan, wordt het maximum voor de doelgrootte gebruikt.
     - Als een bronmachine twee netwerkadapters heeft en de grootte van de doelmachine vier ondersteunt, heeft de doelmachine twee adapters. Als de bronmachine twee adapters heeft, maar de ondersteunde doelgrootte slechts één ondersteunt, heeft de doelmachine slechts één adapter.     
   - Als de virtuele machine meerdere netwerkadapters heeft, ze alle verbinding maken met hetzelfde netwerk.
   - Als de virtuele machine meerdere netwerkadapters heeft, wordt het eerste beheerpunt dat wordt weergegeven in de lijst wordt de *standaard* netwerkadapter in de Azure VM.
5. In **schijven**, ziet u het besturingssysteem van de virtuele machine en de gegevens schijven die worden gerepliceerd.

## <a name="run-a-test-failover"></a>Een testfailover uitvoeren

Nadat u alles hebt ingesteld, voert u een testfailover om te controleren of dat alles werkt zoals verwacht. Bekijk een video-overzicht voordat u begint.

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. Een enkele machine failover **instellingen** > **gerepliceerde Items**, klikt u op **testfailover**.

    ![Testfailover](./media/site-recovery-vmware-to-azure/TestFailover.png)

2. Als u een failover wilt uitvoeren op basis van een herstelplan, klikt u in **Instellingen** > **Herstelplannen** met de rechtermuisknop op het plan > **Testfailover**. Volg [deze instructies](site-recovery-create-recovery-plans.md) om een herstelplan te maken.  
3. In **Testfailover**, selecteer het Azure-netwerk waarmee virtuele Azure-machines zijn verbonden na failover plaatsvindt.
4. Klik op **OK** om te beginnen met de failover. U kunt de voortgang volgen door te klikken op de virtuele machine om de eigenschappen te openen of door te klikken op de **Testfailover** taak in de kluisnaam > **instellingen** > **taken**  >  **Site Recovery-taken**.
5. Nadat de failover is voltooid, kunt u moet ook de gerepliceerde Azure Zie machine worden weergegeven in de Azure portal > **virtuele Machines**. Zorg ervoor dat de virtuele machine is de juiste grootte heeft, of deze is verbonden met het juiste netwerk en dat deze wordt uitgevoerd.
6. Als u zich hebt [voorbereid op verbindingen na een failover](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), kunt u verbinding maken met het virtuele Azure-netwerk.
7. Nadat u bent klaar, klikt u op **testfailover opschonen** op het herstelplan. In **notities**, vastleggen en opslaan van eventuele opmerkingen die zijn gekoppeld aan de testfailover. Hiermee verwijdert u de virtuele machines die zijn gemaakt tijdens de testfailover.

Zie voor meer informatie de [testfailover naar Azure](site-recovery-test-failover-to-azure.md) document.

## <a name="next-steps"></a>Volgende stappen

Na het installeren van replicatie en wordt uitgevoerd, wanneer een storing optreedt, schakelt u over naar Azure en Azure VM's zijn gemaakt op basis van de gerepliceerde gegevens. U kunt vervolgens toegang tot workloads en apps in Azure, totdat u terug naar uw primaire locatie schakelt wanneer deze weer normaal functioneert.

- [Meer informatie](site-recovery-failover.md) over verschillende typen failovers en het uitvoeren hiervan.
- Als u bij het migreren van computers in plaats van met repliceren en mislukt achter, [meer](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- Bij het repliceren van fysieke computers, kunt u alleen een failback naar een VMware-omgeving. [Meer informatie over failback](site-recovery-failback-azure-to-vmware.md).

## <a name="third-party-software-notices-and-information"></a>Software van derden kennisgevingen en informatie
Niet vertalen of Localize

De software en firmware die wordt uitgevoerd in de Microsoft-product of de service is gebaseerd op of opgenomen met het materiaal uit de onderstaande projecten (gezamenlijk ' derde Code'). Microsoft is niet de oorspronkelijke auteur van de Code van derden. Het oorspronkelijke copyrightinformatie en de licentie, waaronder Microsoft deze Code van derden ontvangen worden die hieronder ingesteld.

De informatie in een sectie betrekking heeft op de Code van derden onderdelen uit de onderstaande projecten. Deze licenties en informatie vindt u dient alleen ter informatie. Deze Code van derden is aan u wordt relicensed door Microsoft onder de licentievoorwaarden voor Microsoft software voor de Microsoft-product of service.  

De informatie in de sectie B betrekking heeft op de Code van derden-onderdelen die worden beschikbaar gesteld aan u door Microsoft onder de oorspronkelijke licentievoorwaarden.

Het volledige bestand kan worden gevonden op de [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft behoudt alle rechten die in deze overeenkomst niet uitdrukkelijk zijn verleend, hetzij bij implicatie volgens, of anders.
