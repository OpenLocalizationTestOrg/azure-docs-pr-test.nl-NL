---
title: aaaReplicate virtuele VMware-machines tooAzure | Microsoft Docs
description: Geeft een overzicht van Hallo stappen die u nodig hebt voor het repliceren van workloads die worden uitgevoerd op virtuele VMware-machines tooAzure opslag
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: vmware-walkthrough-overview
ms.openlocfilehash: f800e7d8a3b59a86809a995748eacf87630a1713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-tooazure-with-site-recovery"></a>VMware-virtuele machines tooAzure met Site Recovery repliceren

> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmware-to-azure.md)
> * [Klassieke Azure Portal](site-recovery-vmware-to-azure-classic.md)


Dit artikel wordt beschreven hoe tooreplicate lokale tooAzure virtuele machines van VMware, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.

Als u wilt dat toomigrate virtuele VMware-machines tooAzure (alleen failover), Lees [in dit artikel](site-recovery-migrate-to-azure.md) toolearn meer.

Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="deployment-steps"></a>Implementatiestappen

Dit is wat u moet toodo:

1. Controleer de vereisten en beperkingen.
2. Stel Azure-netwerk- en opslagaccounts in.
3. Hallo lokale machine voorbereiden die u wilt dat toodeploy als Hallo configuratieserver.
4. VMware-accounts toobe die worden gebruikt voor automatische detectie van virtuele machines, en desgewenst voor push-installatie van Mobility-service Hallo voorbereiden.
4. Maak een Recovery Services-kluis. Hallo-kluis bevat configuratie-instellingen en stuurt replicatie.
5. Bron, doel en replicatie-instellingen opgeven.
6. Hallo Mobility-service te implementeren op virtuele machines die u wilt tooreplicate.
7. Replicatie inschakelen voor Hallo virtuele machines.
7. Een test failover toomake, controleren of dat alles werkt zoals verwacht worden uitgevoerd.

## <a name="prerequisites"></a>Vereisten

**Vereiste voor ondersteuning** | **Details**
--- | ---
**Azure** | Meer informatie over [Azure-vereisten](site-recovery-prereq.md#azure-requirements)
**On-premises configuratieserver** | U moet een VMware VM waarop Windows Server 2012 R2 of hoger. U kunt instellen om deze server tijdens de implementatie van Site Recovery.<br/><br/> Hallo standaardproces worden server en de hoofddoelserver ook geïnstalleerd op deze virtuele machine. Als u opschalen, u een afzonderlijk proces-server moet mogelijk en Hallo heeft dezelfde vereisten als Hallo configuratieserver.<br/><br/> Meer informatie over deze onderdelen [hier](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)
**On-premises VMware-servers** | Een of meer VMware vSphere servers, 6.0, 5.5, 5.1 uitgevoerd met de meest recente updates. Servers moeten zich bevinden in Hallo netwerk als de configuratieserver hello (of een afzonderlijk processerver).<br/><br/> We raden aan een vCenter server toomanage hosts met 6.0 of 5.5 met de nieuwste updates Hallo. Alleen de functies die beschikbaar in 5.5 zijn worden ondersteund bij het implementeren van versie 6.0 zijn.
**On-premises virtuele machines** | Virtuele machines die u wilt dat tooreplicate moet worden uitgevoerd een [ondersteund besturingssysteem](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), en voldoet aan de [vereisten voor Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). VM moet VMware-hulpprogramma's hebben.
**URL 's** | Hallo configuratieserver moet toegang tot toothese URL's:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Als u IP-adressen gebaseerde firewallregels, moet u dat ze tooAzure communicatie toestaan.<br/></br> Hallo toestaan [Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653), en Hallo HTTPS (443)-poort.<br/></br> IP-adresbereiken voor hello Azure-regio van uw abonnement en voor VS-West (gebruikt voor toegangsbeheer en identiteitsbeheer) toestaan.<br/><br/> Toestaan dat deze URL voor het downloaden van Hallo MySQL: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Mobility-service** | Geïnstalleerd op elke gerepliceerde virtuele machine.




## <a name="limitations"></a>Beperkingen

**Beperking** | **Details**
--- | ---
**Azure** | Accounts voor opslag en netwerk moet zich in Hallo dezelfde regio bevinden als Hallo kluis<br/><br/> Als u een premium storage-account gebruikt, moet u ook een standaard account toostore replicatielogboeken worden opgeslagen<br/><br/> Accounts in het midden- en Zuid, India toopremium kan niet worden gerepliceerd.
**On-premises configuratieserver** | VMware VM adaptertype moet VMXNET3. Dit niet het geval is, [deze update installeert](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)<br/><br/> vSphere PowerCLI 6.0 moet worden geïnstalleerd.<br/><br> Hallo machine mag niet een domeincontroller zijn. Hallo-machine moet een statisch IP-adres hebben.<br/><br/> Hallo-hostnaam moet 15 tekens of korter is, en het besturingssysteem moet in het Engels.
**VMware** | Alleen 5.5 functies worden ondersteund in vCenter 6.0. Site Recovery biedt geen ondersteuning voor nieuwe vCenter en vSphere 6.0 functies zoals cross vCenter vMotion, virtuele volumes en opslagruimten DRS.
**VM's** | Controleer of [beperkingen van de virtuele machine in Azure](site-recovery-prereq.md#azure-requirements)<br/><br/> U kunt virtuele machines met versleutelde schijven of virtuele machines met UEFI/EFI-opstarten kan niet repliceren.<br/><br> Gedeelde schijf worden niet ondersteund. Als de bron-Hallo VM heeft NIC-koppeling, wordt deze geconverteerd tooa enkel NIC na een failover.<br/><br/> Als VMs een iSCSI-schijf hebt, converteert deze Site Recovery tooa VHD-bestand na een failover. Als Hallo iSCSI-doel kan worden bereikt door Hallo virtuele Azure-machine, verbindt tooit en ziet deze en Hallo VHD. Als dit gebeurt, moet u Hallo iSCSI-doel.<br/><br/> Als u wilt dat tooenable multi-VM consistentie, waardoor de virtuele machines met dezelfde werkbelasting toobe hersteld hello wordt samen tooa consistente gegevens punt, open poort 20004 op Hallo VM.<br/><br/> Windows moet worden geïnstalleerd op Hallo C-station. Hallo besturingssysteemschijf moet de basis- en geen dynamische. Hallo gegevensschijf kan niet dynamisch zijn.<br/><br/> Linux/etc/hosts bestanden op virtuele machines moeten vermeldingen die zijn toegewezen Hallo lokale host naam tooIP adressen die zijn gekoppeld aan alle netwerkadapters bevatten. Hallo hostnaam, koppelpunten, apparaatnaam, systeempaden en bestandsnamen (/ enzovoort; /usr) mag alleen in het Engels zijn.<br/><br/> Specifieke typen [Linux opslag](site-recovery-support-matrix-to-azure.md#support-for-storage) worden ondersteund.<br/><br/>Maken of in te stellen **disk.enableUUID=true** in Hallo VM-instellingen. Dit biedt een consistente UUID toohello VMDK, zodat deze correct koppelt en zorgt ervoor dat alleen nog deltawijzigingen overgedragen back tooon lokale tijdens de failback zonder een volledige replicatie zijn.

## <a name="set-up-azure"></a>Instellen van Azure

1. [Een Azure-netwerk instellen](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    - Virtuele machines in Azure worden geplaatst in dit netwerk wanneer ze zijn gemaakt na een failover.
    - U kunt instellen met een netwerk in [Resource Manager](../resource-manager-deployment-model.md), of in de klassieke modus.

2. Instellen van een [Azure storage-account](../storage/storage-create-storage-account.md#create-a-storage-account) voor gerepliceerde gegevens.
    - Hallo-account kan worden standaard of [premium](../storage/storage-premium-storage.md).
    - U kunt een account in Resource Manager, of in de klassieke modus ingesteld.

3. [Voorbereiden van een account](#prepare-for-automatic-discovery-and-push-installation) op vSphere-hosts of Hallo vCenter-server, dus die Site Recovery kan automatisch detecteren virtuele VMware-machines.

## <a name="prepare-hello-configuration-server"></a>Hallo configuratieserver voorbereiden

1. Installeer Windows Server 2012 R2 of hoger, op een VMware-VM.
2. Zorg ervoor dat Hallo VM toegang toohello URL's die worden vermeld in [vereisten](#prerequisites).
3. Installeer [VMware vSphere PowerCLI 6.0](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1).


## <a name="prepare-for-automatic-discovery-and-push-installation"></a>Voorbereiden voor automatische detectie en push-installatie

- **Voorbereiden van een account voor automatische detectie**: Site Recovery-processerver Hallo detecteert automatisch virtuele machines. toodo deze, Site Recovery behoeften referenties die toegang hebben tot vCenter-servers en vSphere ESXi-hosts.

    1. een specifiek account toouse maakt u een rol (op Hallo vCenter niveau met deze [machtigingen](#vmware-account-permissions). Geef een naam zoals **Azure_Site_Recovery**.
    2. Vervolgens maken van een gebruiker op Hallo vSphere host/vCenter-server en Hallo rol toohello gebruiker toewijzen. U kunt dit gebruikersaccount opgeven tijdens de implementatie van Site Recovery.

- **Voorbereiden van een account toopush Hallo Mobility-service**: als u wilt dat tooVMs toopush Hallo Mobility-service, moet u een account dat door Hallo proces server tooaccess Hallo VM kan worden gebruikt. Hallo-account wordt alleen gebruikt voor Hallo push-installatie. U kunt een domein of lokale account gebruiken:

    - Voor Windows, als u niet een domeinaccount, moet u toodisable externe gebruiker toegangsbeheer op Hallo lokale machine. dit in Hallo registreert onder toodo **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, Hallo DWORD-vermelding toevoegen **LocalAccountTokenFilterPolicy**, met een waarde van 1.
    - Als u tooadd Hallo register-item voor Windows vanuit een CLI wilt, typt u:``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
    - Voor Linux moet Hallo account basiscertificaat op de bronserver Linux Hallo.

## <a name="create-a-recovery-services-vault"></a>Een Recovery Services-kluis maken

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-hello-protection-goal"></a>Hallo beveiligingsdoel selecteren

Selecteer wat u tooreplicate, en waar u tooreplicate aan.

1. Klik op **Recovery Services-kluizen** > kluis.
2. In Hallo Resource Menu, klikt u op **siteherstel** > **stap 1: infrastructuur voorbereiden** > **beveiligingsdoel**.

    ![Doelstellingen kiezen](./media/site-recovery-vmware-to-azure/choose-goals.png)
3. In **beveiligingsdoel**, selecteer **tooAzure** > **Ja, met VMware vSphere Hypervisor**.

    ![Doelstellingen kiezen](./media/site-recovery-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Hallo bronomgeving instellen

Hallo configuratieserver instellen, registreert u dit in de kluis Hallo en VM's detecteren.

1. Klik op **Site Recovery** > **stap 1: infrastructuur voorbereiden** > **bron**.
2. Als u een configuratieserver geen hebt, klikt u op **+ configuratieserver**.

    ![Bron instellen](./media/site-recovery-vmware-to-azure/set-source1.png)
3. In **Server toevoegen**, controleert u of **configuratieserver** wordt weergegeven in **servertype**.
4. Download het installatiebestand van de installatie van Site Recovery-Unified Hallo.
5. Hallo kluisregistratiesleutel downloaden. U moet dit wanneer u Unified Setup uitvoert. Hallo-sleutel is vijf dagen na het genereren ervan geldig.

   ![Bron instellen](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Voer Site Recovery Unified Setup

Hallo volgende voordat u start en voer vervolgens Setup Unified tooinstall Hallo configuratieserver processerver Hallo en Hallo hoofddoelserver.
    - Een video-overzicht

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - Op de configuratieserver VM hello, zorg ervoor dat systeemklok Hallo is gesynchroniseerd met een [tijdserver](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Deze moet overeenkomen. Als het op de voorgrond 15 minuten of achter de installatie mislukken.
    - Voer de installatie als een lokale beheerder op de configuratieserver Hallo VM.
    - Zorg ervoor dat TLS 1.0 op Hallo VM is ingeschakeld.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> Hallo configuratieserver kan ook worden geïnstalleerd [vanaf de opdrachtregel Hallo](http://aka.ms/installconfigsrv).



### <a name="add-hello-account-for-automatic-discovery"></a>Hallo-account voor automatische detectie toevoegen

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="connect-toovmware-servers"></a>TooVMware servers verbinden

Verbinding maken met toovSphere ESXi-hosts of vCenter-servers, toodiscover virtuele VMware-machines.

- Als u Hallo vCenter-server of vSphere-hosts met een account zonder beheerdersrechten op Hallo-server toevoegt, moet Hallo account deze bevoegdheden ingeschakeld:
    - Datacenter, gegevensopslag, map, Host, netwerk, Resource, virtuele machine, vSphere gedistribueerde Switch.
    - Hallo vCenter-server moet opslag weergaven machtigingen.
- Wanneer u een VMware-servers toevoegt, kan het 15 minuten duren of langer ze tooappear in Hallo-portal.
tooallow Azure Site Recovery toodiscover virtuele machines die worden uitgevoerd in uw on-premises-omgeving, moet u tooconnect uw VMware vCenter-Server of vSphere ESXi-hosts met Site Recovery.

Selecteer **+ vCenter** toostart gebruikmaken van een VMware vCenter-server of een VMware vSphere ESXi-host.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

Site Recovery verbindt tooVMware servers Hallo instellingen opgegeven gebruikt en detecteert van virtuele machines.

## <a name="set-up-hello-target"></a>Hallo doel instellen

Voordat u Hallo doelomgeving instellen, Controleer u hebt een [Azure storage-account en het netwerk](#set-up-azure)

1. Klik op **infrastructuur voorbereiden** > **doel**, en selecteer hello Azure-abonnement u wilt dat toouse.
2. Opgeven of de doel-implementatiemodel is Resource Manager gebaseerde of klassieke.
3. Site Recovery controleert of u een of meer compatibele Azure-opslagaccounts en -netwerken hebt.

   ![doel](./media/site-recovery-vmware-to-azure/gs-target.png)
4. Als u een opslagaccount of een netwerk dat nog niet hebt gemaakt, klikt u op **+ opslagaccount** of **+ netwerk**, een Resource Manager-account of netwerk inline toocreate.

## <a name="set-up-replication-settings"></a>Replicatie-instellingen instellen

Haal een snel overzicht van de video voordat u begint:
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate een nieuw replicatiebeleid, klikt u op **Site Recovery-infrastructuur** > **replicatiebeleid** > **+ replicatiebeleid**.
2. In **maken van beleid voor wachtwoordreplicatie**, een beleidsnaam opgeven.
3. In **RPO drempelwaarde**, Hallo RPO grootte opgeven. Deze waarde geeft aan hoe vaak gegevens herstelpunten worden gemaakt. Een waarschuwing wordt gegenereerd als continue replicatie deze limiet overschrijdt.
4. In **herstel bewaarperiode**, opgeven hoe lang (in uren) Hallo bewaarperiode is voor elk herstelpunt. Gerepliceerde virtuele machines kunnen worden hersteld tooany punt in een venster. Gerepliceerd toopremium opslag en 72 uur standaardopslag up too24 uren bewaren wordt ondersteund voor virtuele machines.
5. In **App-consistente momentopname frequentie**, opgeven hoe vaak (in minuten) herstelpunten met toepassingsconsistente momentopnamen worden gemaakt. Klik op **OK** toocreate Hallo beleid.

    ![Beleid voor replicatie](./media/site-recovery-vmware-to-azure/gs-replication2.png)
8. Wanneer u een nieuw beleid maakt is deze automatisch gekoppeld aan Hallo configuratieserver. Standaard wordt automatisch een overeenkomende beleid gemaakt voor failback. Bijvoorbeeld, als hello replicatiebeleid is **rep beleid** wordt beleid voor failback Hallo **rep-beleid-failback**. Dit beleid wordt niet gebruikt, totdat u een failback vanuit Azure initiëren.  



## <a name="plan-capacity"></a>Plannen van capaciteit

1. Nu dat u de basisinfrastructuur hebt ingesteld u nadenkt over capaciteitsplanning en achterhalen of u aanvullende resources nodig. [Meer informatie](site-recovery-plan-capacity-vmware.md).
2. Wanneer u met het plannen van capaciteit bent klaar, selecteert u **Ja** in **hebt u capaciteit plannen?**

   ![Capaciteitsplanning](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Virtuele machines voorbereiden voor replicatie

Hallo Mobility-service moet worden geïnstalleerd op alle virtuele VMware-machines dat u wilt dat tooreplicate. U kunt Hallo Mobility-service installeren op een aantal verschillende manieren:

1. Met een push-installatie van de processerver Hallo installeren. U moet deze methode tooprepare VMs toouse.
2. Installeer implementatieprogramma's, zoals System Center Configuration Manager of een Azure automation DSC.
3.  Handmatig installeren.

[Meer informatie](site-recovery-vmware-to-azure-install-mob-svc.md)


## <a name="enable-replication"></a>Replicatie inschakelen

Voordat u begint:

- Uw Azure gebruikersaccount moet toohave bepaalde [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicatie van een nieuwe virtuele machine tooAzure.
- Wanneer u toevoegen of wijzigen van virtuele machines, het omhoog too15 minuten of langer kan duren voor wijzigingen tootake effect, en voor deze tooappear in Hallo-portal.
- U kunt tijd van laatste Hallo controleren voor virtuele machines in **configuratieservers** > **laatste Contact op**.
- tooadd virtuele machines zonder te wachten Hallo geplande detectie, markeer Hallo configuratieserver (Klik niet op deze), en klik op **vernieuwen**.
- Als een virtuele machine wordt voorbereid voor de push-installatie, de processerver Hallo Hallo Mobility-service automatisch geïnstalleerd wanneer u replicatie inschakelt.


### <a name="exclude-disks-from-replication"></a>Schijven uitsluiten van replicatie

Standaard worden alle schijven op een machine gerepliceerd. U kunt schijven uitsluiten van replicatie. Zo wilt u mogelijk niet tooreplicate schijven met tijdelijke gegevens of gegevens die telkens wanneer een machine is bijgewerkt of de toepassing opnieuw wordt gestart (bijvoorbeeld pagefile.sys of SQL Server tempdb).

### <a name="replicate-vms"></a>Virtuele machines repliceren

Voordat u begint, bekijk een video-overzicht

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. Klik op **Stap 2: toepassing repliceren** > **Bron**.
2. In **bron**, selecteer Hallo configuratieserver.
3. In **type Machine**, selecteer **virtuele Machines**.
4. In **vCenter/vSphere-Hypervisor**, selecteert u Hallo vCenter-server die wordt beheerd Hallo vSphere host of selecteer Hallo host.
5. Selecteer de processerver Hallo. Dit is de configuratieserver Hallo als u geen processervers extra hebt gemaakt. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. In **doel**, selecteert u Hallo-abonnement en resourcegroep waarin u toocreate Hallo failover van virtuele machines wilt Hallo. Hallo-implementatiemodel dat u toouse in Azure (klassiek of de resource management), voor Hallo failover van virtuele machines wilt kiezen.


7. Selecteer hello Azure storage-account gewenste toouse voor het repliceren van gegevens. Als u niet dat toouse een account dat u al hebt ingesteld wilt, kunt u een nieuwe maken.

8. Selecteer hello Azure-netwerk en subnet toowhich Azure Virtual machines wordt verbinding gemaakt, wanneer ze zijn gemaakt na een failover. Selecteer **nu configureren voor geselecteerde machines**, tooapply Hallo instelling tooall machines in het netwerk u selecteert voor beveiliging. Selecteer **later configureren** tooselect hello Azure-netwerk per computer. Als u een bestaand netwerk toouse niet wilt, kunt u een kunt maken.

    ![Replicatie inschakelen](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. In **virtuele Machines** > **virtuele machines selecteren**en klik op elke machine die u wilt dat tooreplicate selecteren. U kunt alleen machines selecteren waarvoor replicatie kan worden ingeschakeld. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. In **eigenschappen** > **eigenschappen configureren**, selecteer Hallo-account dat wordt gebruikt door Hallo proces server tooautomatically Hallo Mobility-service op Hallo computer installeren.
11. Standaard zijn alle schijven worden gerepliceerd. Klik op **alle schijven** en wis alle schijven die u niet wilt dat tooreplicate. Klik vervolgens op **OK**. U kunt later meer VM-eigenschappen instellen.

    ![Replicatie inschakelen](./media/site-recovery-vmware-to-azure/enable-replication6.png)
11. In **replicatie-instellingen** > **replicatie-instellingen configureren**, Controleer of deze Hallo juist replicatiebeleid is geselecteerd. Als u een beleid wijzigt, worden wijzigingen worden toegepast tooreplicating machine en toonew machines.
12. Schakel **consistentie tussen meerdere VM's** als u wilt dat toogather machines in een replicatiegroep en geef een naam voor de groep Hallo. Klik vervolgens op **OK**. Opmerking:

    * Computers in de replicatiegroepen samen repliceren en gedeelde crashconsistent en toepassingsconsistente herstelpunten wanneer ze een failover.
    * Het is raadzaam dat u verzamelen virtuele machines en fysieke servers zodat ze uw werkbelastingen. Inschakelen van de consistentie tussen meerdere VM's kunnen invloed hebben op prestaties workload en mag alleen worden gebruikt als machines worden uitgevoerd Hallo dezelfde werkbelasting en u moet consistentie.

    ![Replicatie inschakelen](./media/site-recovery-vmware-to-azure/enable-replication7.png)
13. Klik op **replicatie inschakelen**. U kunt de voortgang van Hallo volgen **beveiliging inschakelen** taak **instellingen** > **taken** > **Site Recovery-taken**. Na het Hallo **beveiliging voltooien** taak wordt uitgevoerd Hallo machine is gereed voor failover.

### <a name="view-and-manage-vm-properties"></a>Eigenschappen van virtuele machines weergeven en beheren

U wordt aangeraden Hallo VM-eigenschappen controleren en eventuele wijzigingen die u wilt maken.

1. Klik op **gerepliceerde items** >, en selecteer Hallo-machine. Hallo **Essentials** blade ziet u informatie over machines instellingen en status.
2. In **eigenschappen**, vindt u replicatie en failover-informatie voor Hallo VM.
3. In **berekening en netwerk** > **eigenschappen berekenen**, kunt u de naam en doel van de grootte van virtuele machine van Azure Hallo opgeven. Hallo naam toocomply met wijzigen [Azure-vereisten](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) als u wilt.
4. Instellingen voor het doelnetwerk hello, subnet en IP-adres dat wordt toegewezen toohello Azure VM wijzigen:

   - U kunt IP-adres van Hallo doel instellen.

    - Als u een adres niet opgeeft, wordt Hallo failover machine DHCP gebruikt.
    - Als u een adres dat is niet beschikbaar bij een failover, werkt failover niet.
    - Hallo hetzelfde IP-adres van doel kan worden gebruikt voor testfailover als Hallo adres in het testfailovernetwerk Hallo beschikbaar is.

   - Hallo aantal netwerkadapters wordt bepaald door het Hallo-grootte die u voor de virtuele doelmachine Hallo opgeeft:

     - Als Hallo aantal netwerkadapters op de bronmachine Hallo Hallo dezelfde is als of kleiner is dan het aantal adapters dat is toegestaan voor de doelgrootte machine Hallo hello, wordt Hallo doel hetzelfde aantal adapters als bron Hallo Hallo.
     - Als Hallo aantal adapters voor de virtuele bronmachine Hallo Hallo dat is toegestaan voor de doelgrootte hello, overschrijdt en vervolgens maximaal Hallo doel wordt gebruikt.
     - Als een bronmachine twee netwerkadapters heeft en de grootte van Hallo doelmachine vier ondersteunt, wordt Hallo doelmachine twee adapters hebben. Als Hallo-bronmachine twee adapters heeft, maar hello ondersteunde doelgrootte biedt alleen ondersteuning voor een hebben Hallo doelmachine slechts één adapter.     
   - Als Hallo virtuele machine meerdere netwerkadapters heeft worden deze allemaal verbonden toohello hetzelfde netwerk.
   - Als Hallo virtuele machine meerdere netwerkadapters Hallo heeft eerst weergegeven in de lijst hello wordt Hallo *standaard* netwerkadapter in hello Azure virtuele machine.
4. In **schijven**, ziet u Hallo VM-besturingssysteem en Hallo gegevens schijven die worden gerepliceerd.

#### <a name="managed-disks"></a>Managed Disks

In **berekening en netwerk** > **eigenschappen berekenen**, u kunt instellen "Beheerde schijven gebruiken" te 'Ja' voor Hallo VM als u tooattach beheerde schijven tooyour machine op failover-tooAzure wilt. Beheerde schijven vereenvoudigt Schijfbeheer voor Azure IaaS VM's met Hallo storage-accounts die zijn gekoppeld aan het VM-schijven Hallo beheren. [Meer informatie over beheerde schijven.](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview)

   - Beheerde schijven zijn gemaakt en gekoppelde toohello virtuele machine alleen op een failover-tooAzure. Over het inschakelen van beveiliging, blijven gegevens uit de lokale machines tooreplicate toostorage accounts.  Beheerde schijven kunnen alleen voor virtuele machines die zijn geïmplementeerd met behulp van Hallo Resource manager-implementatiemodel worden gemaakt.  

   - Als u "Beheerde schijven gebruiken" te 'Ja', is alleen beschikbaarheidssets in de resourcegroep Hallo met "Beheerde schijven gebruiken" set te 'Ja' beschikbaar voor selectie. Dit is omdat de virtuele machines met beheerde schijven kan alleen deel uitmaken van beschikbaarheidssets met 'Gebruik beheerd schijven' eigenschappenset te 'Ja'. Zorg ervoor dat u beschikbaarheidssets met 'Gebruik beheerd schijven' eigenschap is ingesteld op basis van uw schijven opzet toouse beheerd op failover maken.  Op dezelfde manier als u "Beheerde schijven gebruiken" te 'Nee', is alleen in beschikbaarheidssets voor de resourcegroep Hallo met "Beheerde schijven gebruiken" eigenschappenset te 'Nee' beschikbaar voor selectie. [Meer informatie over beheerde schijven en beschikbaarheidssets](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Als het Hallo-opslagaccount gebruikt voor replicatie is versleuteld met versleuteling van de opslagruimte op elk gewenst moment in de tijd, mislukt het maken van beheerde schijven tijdens failover. U kunt instellen "Beheerde schijven gebruiken" te 'Nee' en probeer de failover of schakel de beveiliging voor Hallo virtuele machine en Beveilig de tooa storage-account die geen versleuteling van de opslagruimte-service is ingeschakeld op elk punt in tijd.
  > [Meer informatie over Versleuteling voor opslagservice en beheerde schijven](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="run-a-test-failover"></a>Een testfailover uitvoeren


Nadat u hebt ingesteld alles, voert u toomake van de test-failover of dat alles werkt zoals verwacht. Ophalen van een video-overzicht voordat u begint
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. toofail via één computer in **instellingen** > **gerepliceerde Items**, klikt u op Hallo VM > **+ Testfailover** pictogram.

    ![Testfailover](./media/site-recovery-vmware-to-azure/TestFailover.png)

1. plan toofail via een herstelbewerking **instellingen** > **herstelplannen**, klik met de rechtermuisknop Hallo plan > **Testfailover**. een herstelplan toocreate [Volg deze instructies](site-recovery-create-recovery-plans.md).  

1. In **Testfailover**, selecteer hello Azure-netwerk toowhich virtuele Azure-machines moet worden verbonden nadat er failover plaatsvindt.

1. Klik op **OK** toobegin Hallo failover. U kunt de voortgang volgen door te klikken op Hallo VM tooopen eigenschappen of op Hallo **Testfailover** taak in de kluisnaam > **instellingen** > **taken**  >  **Site Recovery-taken**.

1. Nadat de failover Hallo is voltooid, dient u zich kunt toosee Hallo replica machine van Azure in hello Azure-portal weergegeven > **virtuele Machines**. U moet ervoor zorgen dat Hallo VM is de juiste grootte hello, of deze is verbonden met het juiste netwerk toohello en dat deze wordt uitgevoerd.

1. Als u [voorbereid op verbindingen na een failover](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), moet u kunnen tooconnect toohello Azure VM.

1. Wanneer u bent klaar, klikt u op op **testfailover opschonen** op Hallo herstelplan. In **notities**, vastleggen en opslaan van eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo. Hiermee verwijdert u Hallo virtuele machines die zijn gemaakt tijdens de testfailover.

[Meer informatie](site-recovery-test-failover-to-azure.md) over testfailovers.


## <a name="vmware-account-permissions"></a>Machtigingen van de VMware-account

Site Recovery moet toegang tooVMware voor Hallo proces server tooautomatically VM's detecteren, en voor de failover en failback van virtuele machines.

- **Migreren**: als u wilt dat alleen toomigrate virtuele VMware-machines tooAzure, zonder ooit terug mislukt, kunt u een VMware-account gebruiken met een rol alleen-lezen. Een dergelijke rol failover kan worden uitgevoerd, maar kan niet worden beveiligde bronmachines afgesloten. Dit is niet nodig zijn voor migratie.
- **Repliceren/herstellen**: als u toodeploy volledige replicatie (repliceren, failover, failback) Hallo account moet kunnen toorun bewerkingen wilt zoals het maken en schijven verwijderen, inschakelen aan virtuele machines, enzovoort.
- **Automatische detectie**: ten minste een alleen-lezen-account is vereist.


**Taak** | **Vereiste account/functie** | **Machtigingen** | **Details**
--- | --- | --- | ---
**Processerver detecteert automatisch virtuele VMware-machines** | U moet ten minste een alleen-lezen-gebruiker | Data Center-object doorgeven tooChild Object, –> rol = alleen-lezen | Gebruiker datacenter niveau toewijzen en toegang tooall Hallo objecten heeft in Hallo datacenter.<br/><br/> toorestrict access toewijzen Hallo **geen toegang** rol met Hallo **toochild doorgegeven** object toohello onderliggende objecten (vSphere-hosts, datastores, VM's en -netwerken).
**Failover** | U moet ten minste een alleen-lezen-gebruiker | Data Center-object doorgeven tooChild Object, –> rol = alleen-lezen | Gebruiker datacenter niveau toewijzen en toegang tooall Hallo objecten heeft in Hallo datacenter.<br/><br/> toorestrict access toewijzen Hallo **geen toegang** rol met Hallo **toochild doorgegeven** object toohello onderliggende objecten (vSphere-hosts, datastores, VM's en -netwerken).<br/><br/> Dit is handig voor migratiedoeleinden, maar niet een volledige replicatie, failover en failback.
**Failover en failback** | We raden u een rol (Azure_Site_Recovery) met de Hallo vereist machtigingen maken en vervolgens Hallo rol tooa VMware gebruiker of groep toewijzen | Data Center-object doorgeven tooChild Object, –> rol Azure_Site_Recovery =<br/><br/> Datastore -> ruimte toewijzen, gegevensopslag, op laag niveau bestandsbewerkingen bladeren, bestand verwijderen, bestanden van virtuele machine bijwerken<br/><br/> Netwerk -> netwerk toewijzen<br/><br/> Resource -> toewijzen VM tooresource pool, migreren van virtuele machine is uitgeschakeld, stroomvoorziening op virtuele machine migreren<br/><br/> Taken maken taak, updatetaak -><br/><br/> Virtuele machine-configuratie ><br/><br/> Virtuele machine -> Interact -> vraag beantwoorden, apparaatverbinding, CD's configureren, configureren van diskettes, uitschakelen, inschakelen, VMware-hulpprogramma's installeren<br/><br/> Virtuele machine -> inventaris -> maken, registreren, registratie<br/><br/> Virtuele machine inrichten -> -> downloaden van de virtuele machine toestaan, toestaan uploaden van bestanden van virtuele machine<br/><br/> Virtuele machine-momentopnamen >-Remove momentopnamen > | Gebruiker datacenter niveau toewijzen en toegang tooall Hallo objecten heeft in Hallo datacenter.<br/><br/> toorestrict access toewijzen Hallo **geen toegang** rol met Hallo **toochild doorgegeven** object toohello onderliggende objecten (vSphere-hosts, datastores, VM's en -netwerken).


## <a name="next-steps"></a>Volgende stappen

Na het installeren van replicatie en wordt uitgevoerd, wanneer een storing optreedt, schakelt u over tooAzure en Azure VM's zijn gemaakt op basis van Hallo gerepliceerde gegevens. U kunt vervolgens toegang tot workloads en apps in Azure, totdat u niet de primaire locatie back tooyour wanneer deze toonormal bewerkingen weer.

- [Meer informatie](site-recovery-failover.md) over verschillende soorten failovers, en hoe toorun ze.
- Als u bij het migreren van computers in plaats van met repliceren en mislukt achter, [meer](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- [Meer informatie over failback](site-recovery-failback-azure-to-vmware.md), toofail back en repliceren Azure VM's weer toohello primaire on-premises-site.

## <a name="third-party-software-notices-and-information"></a>Software van derden kennisgevingen en informatie
Niet vertalen of Localize

Hallo-software en -firmware uitgevoerd in de Microsoft-product Hallo of de service is gebaseerd op of opgenomen met het materiaal van Hallo projecten onderstaande (gezamenlijk 'Code van derden').  Microsoft hello is geen oorspronkelijke auteur Hallo Code van derden.  de oorspronkelijke copyrightgegevens Hallo en licentie, waaronder Microsoft deze Code van derden ontvangen worden die hieronder ingesteld.

Hallo-informatie in de sectie A is met betrekking tot de Code van derden onderdelen van Hallo projecten hieronder vermeld. Deze licenties en informatie vindt u dient alleen ter informatie.  Deze Code van derden wordt relicensed tooyou door Microsoft onder de licentievoorwaarden voor Microsoft-product Hallo of -service van Microsoft-software.  

Hallo-informatie in de sectie B is met betrekking tot de Code van derden-onderdelen die worden aangebracht beschikbaar tooyou door Microsoft onder Hallo oorspronkelijke licentievoorwaarden.

Hallo volledige bestand kan worden gevonden op Hallo [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft behoudt alle rechten die in deze overeenkomst niet uitdrukkelijk zijn verleend, hetzij bij implicatie volgens of anderszins.
