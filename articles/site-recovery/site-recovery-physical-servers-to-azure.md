---
title: aaaReplicate fysieke servers tooAzure | Microsoft Docs
description: Hierin wordt beschreven hoe toodeploy Azure Site Recovery tooorchestrate replicatie, failovers en herstel van on-premises Windows of Linux fysieke servers tooAzure door met behulp van hello Azure-portal
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
ms.openlocfilehash: cf5928fb631f6858d57b27f6f21babc312714e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
---
# <a name="replicate-physical-machines-tooazure-by-using-site-recovery"></a>Fysieke machines tooAzure repliceren met behulp van Site Recovery


Dit artikel wordt beschreven hoe tooreplicate on-premises fysieke machines tooAzure door gebruik van hello Azure Site Recovery-service in hello Azure-portal.

Als u wilt dat toomigrate fysieke machines tooAzure (alleen failover), Lees [tooAzure met Site Recovery migreren](site-recovery-migrate-to-azure.md) toolearn meer.

Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Vereisten

**Vereiste voor ondersteuning** | **Details**
--- | ---
**Azure** | Meer informatie over [Azure-vereisten](site-recovery-prereq.md#azure-requirements).
**On-premises configuratieserver** | Lokale machine (fysieke of VMware-VM) met Windows Server 2012 R2 of hoger. U instellen Hallo configuratieserver tijdens de implementatie van Site Recovery.<br/><br/> Standaard worden Hallo processerver en de hoofddoelserver ook geïnstalleerd op deze machine. Als u opschalen, u een afzonderlijk proces-server moet mogelijk en Hallo heeft dezelfde vereisten als Hallo configuratieserver.<br/><br/> Meer informatie over deze onderdelen in [Hallo bronomgeving instellen](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).
**On-premises virtuele machines** | Computers die u wilt dat tooreplicate moet worden uitgevoerd een [ondersteund besturingssysteem](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) en voldoet aan de [vereisten voor Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URL 's** | Hallo configuratieserver moet toegang tot toothese URL's:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Als u IP-adressen gebaseerde firewallregels, zorg ervoor dat ze tooAzure communicatie toestaan.<br/></br> Hallo toestaan [Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653) en Hallo HTTPS (443)-poort.<br/></br> IP-adresbereiken voor hello Azure-regio van uw abonnement en voor VS-West (gebruikt voor beheer en de identiteit van toegangsbeheer) toestaan.<br/><br/> Toestaan dat deze URL voor het downloaden van Hallo MySQL: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Mobility-service** | Deze service is geïnstalleerd op elke machine die u wilt tooreplicate.

## <a name="limitations"></a>Beperkingen

**Beperking** | **Details**
--- | ---
**Azure** | Accounts voor opslag en netwerk moet zich in Hallo dezelfde regio als Hallo-kluis.<br/><br/> Als u een premium storage-account gebruikt, moet u ook een standaard account toostore replicatielogboeken worden opgeslagen.<br/><br/> Accounts in het midden- en Zuid, India toopremium kan niet worden gerepliceerd.
**On-premises configuratieserver** | Als u de configuratieserver Hallo op een VMware-VM installeert, moet Hallo VM adaptertype VMXNET3. Dit niet het geval is, [Installeer deze update](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).<br/><br/> Als u een VM VMware, moet vSphere PowerCLI 6.0 worden geïnstalleerd.<br/><br> Hallo machine mag niet een domeincontroller zijn.<br/><br/> Hallo-machine moet een statisch IP-adres hebben.<br/><br/> Hallo-hostnaam moet 15 tekens of minder en Hallo-besturingssysteem moet in het Engels.
**Gerepliceerde machines** | Controleer of [beperkingen van de virtuele machine van Azure](site-recovery-prereq.md#azure-requirements).<br/><br/> Als u wilt dat tooenable multi-VM consistentie, waarmee computers met dezelfde werkbelasting toobe hersteld hello wordt samen tooa consistente gegevens punt, open poort 20004 op Hallo-machine.<br/><br/> Specifieke typen [Linux opslag](site-recovery-support-matrix-to-azure.md#support-for-storage) worden ondersteund.
**Failback** | U kunt geen een failback van Azure tooa fysieke machine. Als u wilt dat toobe kunnen toofail back tooon lokale na een failover, moet u een omgeving met VMware zodat u back-tooa VMware VM kan uitvallen.


## <a name="set-up-azure"></a>Instellen van Azure

1. [Een Azure-netwerk instellen](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

      a. Virtuele machines in Azure worden geplaatst in dit netwerk wanneer ze zijn gemaakt na een failover.

      b. U kunt een Azure-netwerk instellen [Resource Manager](../resource-manager-deployment-model.md) of in de klassieke modus.

2. Instellen van een [Azure storage-account](../storage/storage-create-storage-account.md#create-a-storage-account) voor gerepliceerde gegevens.

    a. Hallo-account kan worden standaard of [premium](../storage/storage-premium-storage.md).

    b. U kunt een account in Resource Manager of in de klassieke modus ingesteld.

## <a name="prepare-hello-configuration-server"></a>Hallo configuratieserver voorbereiden

1. Installeer Windows Server 2012 R2 of later op een on-premises fysieke server of een VMware-VM.

2. Zorg ervoor dat Hallo machine toegang toohello URL's die worden vermeld in [vereisten](#prerequisites).

## <a name="prepare-for-mobility-service-installation"></a>Voorbereiden voor de installatie van de Mobility-service

Als u wilt dat toopush Hallo Mobility service tooa fysieke machine, moet u een account dat door Hallo proces server tooaccess Hallo machines kan worden gebruikt. Hallo-account wordt alleen gebruikt voor Hallo push-installatie. U kunt een domein of lokale account gebruiken:

  - Voor Windows, als u niet een domeinaccount, moet u toodisable externe gebruiker toegangsbeheer op Hallo lokale machine. toodo dit in Hallo register onder **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, Hallo DWORD-vermelding toevoegen **LocalAccountTokenFilterPolicy**, met een waarde van 1. Als u tooadd Hallo register-item voor Windows vanaf een opdrachtregelinterface wilt, typt u:

        ``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
  - Voor Linux moet Hallo account een Hoofdgebruiker op de bronserver Linux Hallo.


## <a name="create-a-recovery-services-vault"></a>Een Recovery Services-kluis maken

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="select-hello-protection-goal"></a>Hallo beveiligingsdoel selecteren

Selecteer wat u wilt dat tooreplicate en waar u tooreplicate aan.

1. Klik op **Recovery Services-kluizen** > **kluis**.
2. Op Hallo **Resource** menu, klikt u op **siteherstel** > **infrastructuur voorbereiden** > **beveiligingsdoel**.

    ![Doelstellingen kiezen](./media/site-recovery-vmware-to-azure/choose-goal-physical.PNG)

3. In **beveiligingsdoel**, selecteer **tooAzure** > **niet gevirtualiseerde / andere**.


## <a name="set-up-hello-source-environment"></a>Hallo bronomgeving instellen

Hallo configuratieserver instellen, registreert u dit in de kluis Hallo en VM's detecteren.

1. Klik op **Site Recovery** > **infrastructuur voorbereiden** > **bron**.
2. Als u een configuratieserver geen hebt, klikt u op **+ configuratieserver**.

    ![Bron instellen](./media/site-recovery-vmware-to-azure/set-source1.png)

3. In **Server toevoegen**, controleert u of **configuratieserver** wordt weergegeven in **servertype**.
4. Hallo downloaden **Unified installatie van Site Recovery** -bestand voor installatie.
5. Hallo downloaden **kluisregistratiesleutel**. Wanneer u Setup Unified uitvoert moet u deze sleutel. Hallo-sleutel is vijf dagen na het genereren ervan geldig.

   ![Bron instellen](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Voer Site Recovery Unified Setup

Voordat u begint, Hallo te volgen:

- Een snelle video-overzicht ophalen. (Hallo video beschrijft het tooreplicate virtuele VMware-machines, maar het Hallo-proces is vergelijkbaar voor replicatie van fysieke machine.)

    > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

- Op Hallo configuratie-server, zorg ervoor dat systeemklok Hallo is gesynchroniseerd met een [tijdserver](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Als het op de voorgrond 15 minuten of achter de installatie mislukken.
- Voer Setup uit als lokale beheerder op Hallo configuratie server-machine.
- Zorg ervoor dat TLS 1.0 op Hallo machine is ingeschakeld.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> Hallo configuratieserver kan ook worden geïnstalleerd [vanaf de opdrachtregel Hallo](http://aka.ms/installconfigsrv).


## <a name="set-up-hello-target-environment"></a>Hallo doelomgeving instellen

Controleer voordat u Hallo doelomgeving instellen, toomake ervoor dat u hebt een [Azure storage-account en het netwerk](#set-up-azure).

1. Klik op **infrastructuur voorbereiden** > **doel**, en selecteer hello Azure-abonnement u wilt dat toouse.
2. Opgeven of de doel-implementatiemodel Resource Manager of klassiek.
3. Site Recovery controleert toomake ervoor dat u een of meer compatibele Azure storage-accounts en netwerken hebt.

   ![doel](./media/site-recovery-vmware-to-azure/gs-target.png)

4. Als u een opslagaccount of een netwerk dat nog niet hebt gemaakt, klikt u op **+ opslagaccount** of **+ netwerk** toocreate een Resource Manager-account of netwerk inline.

## <a name="set-up-replication-settings"></a>Replicatie-instellingen instellen

Voordat u begint, krijgt u een snelle video overzicht. (Hallo video beschrijft het tooreplicate virtuele VMware-machines, maar het Hallo-proces is vergelijkbaar voor replicatie van fysieke machine.)

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate een nieuw replicatiebeleid, klikt u op **Site Recovery-infrastructuur** > **replicatiebeleid** > **+ replicatiebeleid**.
2. In **maken van beleid voor wachtwoordreplicatie**, een beleidsnaam opgeven.
3. In **RPO drempelwaarde**, Hallo RPO grootte opgeven. Deze waarde geeft aan hoe vaak gegevens herstelpunten worden gemaakt. Een waarschuwing wordt gegenereerd als continue replicatie deze limiet overschrijdt.
4. In **herstel bewaarperiode**, opgeven hoe lang (in uren) Hallo bewaarperiode is voor elk herstelpunt. Gerepliceerde virtuele machines kunnen worden hersteld tooany punt in een venster. Up too24 wordt uur bewaren voor machines toopremium gerepliceerde opslag ondersteund. Up too72 wordt uur bewaren voor machines toostandard gerepliceerde opslag ondersteund.
5. In **App-consistente momentopname frequentie**, opgeven hoe vaak (in minuten) herstelpunten met toepassingsconsistente momentopnamen worden gemaakt. Klik op **OK** toocreate Hallo beleid.

    ![Beleid voor replicatie](./media/site-recovery-vmware-to-azure/gs-replication2.png)

6. Wanneer u een nieuw beleid maakt, wordt dit automatisch gekoppeld met de configuratieserver Hallo. Standaard wordt automatisch een overeenkomende beleid gemaakt voor failback. Bijvoorbeeld, als hello replicatiebeleid is **rep beleid**, is beleid voor failback Hallo **rep-beleid-failback**. Dit beleid wordt niet gebruikt, totdat u een failback vanuit Azure initiëren.  


## <a name="plan-capacity"></a>Plannen van capaciteit

1. Nu dat u uw basisinfrastructuur instellen hebt, kunt u nadenkt over capaciteitsplanning en nagaan of u aanvullende resources nodig. [Meer informatie](site-recovery-plan-capacity-vmware.md).
2. Wanneer u met het plannen van capaciteit bent klaar, selecteert u **Ja** in **hebt u capaciteit plannen?**

   ![Capaciteitsplanning](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Virtuele machines voorbereiden voor replicatie

Alle machines die u wilt dat tooreplicate Hallo Mobility-service geïnstalleerd moeten hebben. U kunt Hallo Mobility-service installeren op een aantal verschillende manieren:

- Hallo-service met een push-installatie van de processerver Hallo installeren. U moet deze methode tooprepare-machines in de voorafgaande toouse.
- Hallo-service installeren met behulp van de implementatiehulpprogramma's zoals System Center Configuration Manager of Azure Automation Desired State Configuration.
- Hallo-service handmatig installeren.

[Meer informatie](site-recovery-vmware-to-azure-install-mob-svc.md).


## <a name="enable-replication"></a>Replicatie inschakelen

Voordat u begint:

- Uw Azure gebruikersaccount moet toohave bepaalde [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicatie van een nieuwe virtuele machine tooAzure.
- Bij het toevoegen of wijzigen van virtuele machines, het omhoog too15 minuten of langer kan duren voor wijzigingen tootake effect als ze tooappear in Hallo-portal.
- U kunt tijd van laatste Hallo controleren voor virtuele machines in **configuratieservers** > **laatste Contact op**.
- tooadd virtuele machines zonder te wachten Hallo geplande detectie, markeer Hallo configuratieserver (Klik niet op deze), en klik op **vernieuwen**.
- Als een virtuele machine wordt voorbereid voor de push-installatie, de processerver Hallo Hallo Mobility-service automatisch geïnstalleerd wanneer u replicatie inschakelt.
- Een snelle video-overzicht ophalen. (Hallo video beschrijft het tooreplicate virtuele VMware-machines, maar het Hallo-proces is vergelijkbaar voor replicatie van fysieke machine.)

    >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]


### <a name="exclude-disks-from-replication"></a>Schijven uitsluiten van replicatie

Standaard worden alle schijven op een machine gerepliceerd. U kunt schijven uitsluiten van replicatie. Bijvoorbeeld, wilt u mogelijk niet tooreplicate schijven met tijdelijke gegevens of gegevens die elk is vernieuwd wanneer een machine of de toepassing opnieuw wordt opgestart (bijvoorbeeld, pagefile.sys of SQL Server tempdb).

### <a name="replicate-vms"></a>Virtuele machines repliceren

1. Klik op **toepassing repliceren** > **bron**.
2. In **bron**, selecteer **On-premises**.
3. In **bronlocatie**, selecteer servernaam Hallo-configuratie.
4. In **type Machine**, selecteer **fysieke Machines**.
5. In **processerver**, Hallo processerver kiezen. Als u geen processervers extra hebt gemaakt, is deze server Hallo configuratieserver. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/site-recovery-physical-to-azure/chooseVM.png)

6. In **doel**, selecteer Hallo **abonnement** en Hallo **resourcegroep** waarin u wilt dat toocreate Hallo virtuele Azure-machines na een failover. Kies Hallo implementatie model dat u wilt dat toouse in Azure (klassiek of Resource Manager) voor Hallo failover virtuele machines.

7. Selecteer hello Azure storage-account gewenste toouse voor het repliceren van gegevens. Als u niet dat toouse een account dat u al hebt ingesteld wilt, kunt u een nieuwe maken.

8. Selecteer Hallo **Azure-netwerk** en **Subnet** toowhich virtuele Azure-machines verbinding maken na een failover. Selecteer **nu configureren voor geselecteerde machines** tooapply Hallo instelling tooall machines in het netwerk u selecteert voor beveiliging. Selecteer **later configureren** tooselect hello Azure-netwerk per computer. Als u een bestaand netwerk toouse niet wilt, kunt u een kunt maken.

    ![Replicatie inschakelen](./media/site-recovery-physical-to-azure/targetsettings.png)

9. In **fysieke machines**, klikt u op **+ fysieke machine** en Voer Hallo **naam** en **IP-adres**. Kies Hallo besturingssysteem van de machine Hallo gewenste tooreplicate. Het duurt enkele minuten totdat de machines zijn gedetecteerd en weergegeven in de lijst Hallo.

    ![Replicatie inschakelen](./media/site-recovery-physical-to-azure/machineselect.png)

10. In **eigenschappen** > **eigenschappen configureren**, selecteer Hallo account die wordt gebruikt door Hallo proces server tooautomatically toobe Hallo Mobility-service op Hallo computer installeren.
11. Standaard zijn alle schijven worden gerepliceerd. Klik op **alle schijven**, en wis alle schijven die u niet wilt dat tooreplicate. Klik vervolgens op **OK**. U kunt later meer VM-eigenschappen instellen.

    ![Replicatie inschakelen](./media/site-recovery-physical-to-azure/configprop.png)

12. In **replicatie-instellingen** > **replicatie-instellingen configureren**, Controleer of deze Hallo juist replicatiebeleid is geselecteerd. Als u een beleid wijzigt, worden wijzigingen toegepaste toohello machine en toonew machines repliceren.
13. Schakel **consistentie tussen meerdere VM's** als u wilt dat toogather machines in een replicatiegroep en geef een naam voor de groep Hallo. Klik vervolgens op **OK**. Opmerking:

    a. Computers in de replicatiegroepen samen repliceren en de gedeelde crashconsistent en toepassingsconsistente herstelpunten wanneer ze een failover.

    b. Het is raadzaam dat u verzamelen virtuele machines en fysieke servers zodat ze uw werkbelastingen. Inschakelen van de consistentie tussen meerdere VM's kan werkbelasting prestaties beïnvloeden. Het moet alleen als machines uitgevoerd Hallo dezelfde werkbelasting en u een consistentiecontrole moet worden gebruikt.

    ![Replicatie inschakelen](./media/site-recovery-physical-to-azure/policy.png)

14. Klik op **replicatie inschakelen**. U kunt de voortgang van Hallo volgen **beveiliging inschakelen** taak **instellingen** > **taken** > **Site Recovery-taken**. Na het Hallo **beveiliging voltooien** taak wordt uitgevoerd, Hallo machine is gereed voor failover.

Nadat u replicatie inschakelt, worden de Hallo Mobility-service is geïnstalleerd als u push-installatie hebt ingesteld. Nadat de Hallo Mobility-service is geïnstalleerd op een computer push, wordt een beveiligingstaak wordt gestart en is mislukt. Na een storing hello, moet u toomanually start opnieuw op elke machine. Hallo beveiligingstaak begint vervolgens opnieuw en initiële replicatie plaats.


### <a name="view-and-manage-azure-vm-properties"></a>Weergeven en beheren van Azure VM-eigenschappen

U wordt aangeraden controleren Hallo VM-eigenschappen en breng eventuele wijzigingen die u nodig hebt.

1. Klik op **gerepliceerde items**, en selecteer Hallo-machine. Hallo **Essentials** blade ziet u informatie over machines instellingen en status.
2. In **eigenschappen**, vindt u replicatie en failover-informatie voor Hallo VM.
3. In **berekening en netwerk** > **eigenschappen berekenen**, kunt u de naam en doel van de grootte van virtuele machine van Azure Hallo opgeven. Hallo naam toocomply met wijzigen [Azure-vereisten](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) als u wilt.
4. Instellingen voor het doelnetwerk hello, subnet en IP-adres die zijn toegewezen toohello Azure VM wijzigen:

    a. U kunt IP-adres van Hallo doel instellen.

    b.  Als u een adres niet opgeeft, Hallo failover machine DHCP gebruikt.

    c. Als u een adres dat is niet beschikbaar bij een failover, werkt failover niet.

    d. Hallo hetzelfde IP-adres van doel kan worden gebruikt voor een testfailover als Hallo adres in het testfailovernetwerk Hallo beschikbaar is.

    e. Hallo aantal netwerkadapters wordt bepaald door het Hallo-grootte die u voor de virtuele doelmachine Hallo opgeeft:

     - Als Hallo aantal netwerkadapters op de bronmachine Hallo Hallo dezelfde is als of kleiner is dan het aantal adapters dat is toegestaan voor de doelgrootte machine Hallo hello, wordt Hallo doel Hallo heeft hetzelfde aantal adapters als Hallo bron.
     - Als het aantal adapters voor de virtuele bronmachine Hallo Hallo overschrijdt Hallo getal is toegestaan voor de doelgrootte Hallo vervolgens maximaal Hallo doel wordt gebruikt.
     - Als een bronmachine twee netwerkadapters heeft en de grootte van Hallo doelmachine vier ondersteunt, heeft Hallo doelmachine twee adapters. Als Hallo-bronmachine twee adapters heeft, maar de doelgrootte Hallo ondersteund slechts één ondersteunt, heeft de doelmachine Hallo slechts één adapter.     
   - Als Hallo virtuele machine meerdere netwerkadapters heeft, ze alle toohello verbinding maken met hetzelfde netwerk.
   - Als Hallo virtuele machine meerdere netwerkadapters heeft, wordt de hello eerst weergegeven in de lijst hello Hallo wordt *standaard* netwerkadapter in hello Azure VM.
5. In **schijven**, ziet u Hallo VM-besturingssysteem en gegevensschijven Hallo die zijn gerepliceerd.

## <a name="run-a-test-failover"></a>Een testfailover uitvoeren

Nadat u alles hebt ingesteld, voert u een test failover toomake, controleren of dat alles werkt zoals verwacht. Bekijk een video-overzicht voordat u begint.

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. toofail via één computer in **instellingen** > **gerepliceerde Items**, klikt u op **testfailover**.

    ![Testfailover](./media/site-recovery-vmware-to-azure/TestFailover.png)

2. plan toofail via een herstelbewerking **instellingen** > **herstelplannen**, klik met de rechtermuisknop Hallo plan > **Testfailover**. een herstelplan toocreate [Volg deze instructies](site-recovery-create-recovery-plans.md).  
3. In **Testfailover**, selecteer hello Azure-netwerk toowhich Azure VM's zijn verbonden na failover plaatsvindt.
4. Klik op **OK** toobegin Hallo failover. U kunt de voortgang volgen door te klikken op Hallo VM tooopen eigenschappen of door te klikken op Hallo **Testfailover** taak in de kluisnaam > **instellingen** > **taken**  >  **Site Recovery-taken**.
5. Nadat de failover Hallo is voltooid, dient u zich kunt toosee Hallo replica machine van Azure in hello Azure-portal weergegeven > **virtuele Machines**. Zorg ervoor dat Hallo VM is de juiste grootte hello, of deze is verbonden met het juiste netwerk toohello en dat deze wordt uitgevoerd.
6. Als u [voorbereid op verbindingen na een failover](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), moet u kunnen tooconnect toohello Azure VM.
7. Nadat u bent klaar, klikt u op **testfailover opschonen** op Hallo herstelplan. In **notities**, vastleggen en opslaan van eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo. Deze stap verwijdert Hallo virtuele machines die zijn gemaakt tijdens de testfailover.

Zie voor meer informatie, Hallo [Test failover tooAzure](site-recovery-test-failover-to-azure.md) document.

## <a name="next-steps"></a>Volgende stappen

Na het installeren van replicatie en wordt uitgevoerd, wanneer een storing optreedt, schakelt u over tooAzure en Azure VM's zijn gemaakt op basis van Hallo gerepliceerde gegevens. U kunt vervolgens toegang tot workloads en apps in Azure, totdat u niet de primaire locatie back tooyour wanneer deze toonormal bewerkingen weer.

- [Meer informatie](site-recovery-failover.md) over verschillende soorten failovers en hoe toorun ze.
- Als u bij het migreren van computers in plaats van met repliceren en mislukt achter, [meer](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- Bij het repliceren van fysieke computers, kunt u alleen failback tooa VMware-omgeving. [Meer informatie over failback](site-recovery-failback-azure-to-vmware.md).

## <a name="third-party-software-notices-and-information"></a>Software van derden kennisgevingen en informatie
Niet vertalen of Localize

Hallo-software en -firmware uitgevoerd in de Microsoft-product Hallo of de service is gebaseerd op of opgenomen met het materiaal van Hallo projecten onderstaande (gezamenlijk 'derde Code'). Microsoft is niet de oorspronkelijke auteur Hallo Hallo Code van derden. de oorspronkelijke copyrightgegevens Hallo en licentie, waaronder Microsoft deze Code van derden ontvangen worden die hieronder ingesteld.

Hallo-informatie in de sectie A betrekking heeft op derde Code-onderdelen uit Hallo projecten hieronder vermeld. Deze licenties en informatie vindt u dient alleen ter informatie. Deze Code van derden wordt relicensed tooyou door Microsoft onder de licentievoorwaarden voor Microsoft-product Hallo of -service van Microsoft-software.  

Hallo-informatie in de sectie B is met betrekking tot de Code van derden-onderdelen die worden aangebracht beschikbaar tooyou door Microsoft onder Hallo oorspronkelijke licentievoorwaarden.

Hallo volledige bestand kan gevonden worden op Hallo [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft behoudt alle rechten die in deze overeenkomst niet uitdrukkelijk zijn verleend, hetzij bij implicatie volgens, of anders.
