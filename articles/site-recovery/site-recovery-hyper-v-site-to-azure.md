---
title: aaaReplicate Hyper-V-machines tooAzure | Microsoft Docs
description: Hierin wordt beschreven hoe tooorchestrate replicatie, failover en herstel van on-premises Hyper-V-machines tooAzure
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 04/05/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: hyper-v-site-walkthrough-overview
ms.openlocfilehash: 6fba41e43823fc57511d51ea2e09691159693982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure-using-azure-site-recovery-with-hello-azure-portal"></a>Replicatie van Hyper-V virtuele machines (zonder VMM) tooAzure met Azure Site Recovery Hello Azure-portal

> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-hyper-v-site-to-azure.md)
> * [Klassieke Azure Portal](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell - Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

Dit artikel wordt beschreven hoe tooreplicate lokale Hyper-V virtuele machines tooAzure, met behulp van [Azure Site Recovery](site-recovery-overview.md) in hello Azure-portal. In deze implementatie van Hyper-V-machines worden niet beheerd door System Center Virtual Machine Manager (VMM).

Na het lezen van dit artikel, eventuele opmerkingen posten Hallo onderin of technische vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Meer informatie als u wilt toomigrate machines tooAzure (zonder failback), [in dit artikel](site-recovery-migrate-to-azure.md).



## <a name="deployment-steps"></a>Implementatiestappen

Volgt Hallo artikel toocomplete implementatie:

1. [Meer informatie](site-recovery-components.md#hyper-v-to-azure) over Hallo-architectuur voor deze implementatie. Lees ook [meer informatie](site-recovery-hyper-v-azure-architecture.md) over de werking van Hyper-V-replicatie in Site Recovery.
2. Controleer de vereisten en beperkingen.
3. Stel Azure-netwerk- en opslagaccounts in.
4. Bereid de Hyper-V-hosts.
5. Maak een Recovery Services-kluis. Hallo-kluis bevat configuratie-instellingen en stuurt replicatie.
6. Geef de broninstellingen op. Maken van een Hyper-V-site die Hallo Hyper-V-hosts bevat en Hallo site in Hallo kluis registreren. Hello Azure Site Recovery Provider en Hallo Microsoft Recovery Services-agent installeren op Hallo Hyper-V-hosts.
7. Stel de doel- en replicatie-instellingen in.
8. Replicatie inschakelen voor Hallo virtuele machines.
9. Een test failover toomake, controleren of dat alles werkt zoals verwacht worden uitgevoerd.



## <a name="prerequisites"></a>Vereisten


**Vereiste** | **Details** |
--- | --- |
**Azure** | Meer informatie over [Azure-vereisten](site-recovery-prereq.md#azure-requirements).
**On-premises servers** | [Meer informatie](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager) over de vereisten voor Hallo lokale Hyper-V-hosts.
**On-premises Hyper-V-VM's** | Virtuele machines die u wilt dat tooreplicate moet worden uitgevoerd een [ondersteund besturingssysteem](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), en voldoet aan de [vereisten voor Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**Azure-URL's** | Hyper-V-hosts moeten toegang tot toothese URL's:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Als u IP-adressen gebaseerde firewallregels, moet u dat ze tooAzure communicatie toestaan.<br/></br> Hallo toestaan [Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653), en Hallo HTTPS (443)-poort.<br/></br> IP-adresbereiken voor hello Azure-regio van uw abonnement en voor VS-West (gebruikt voor toegangsbeheer en identiteitsbeheer) toestaan.



## <a name="prepare-for-deployment"></a>Implementatie voorbereiden

tooprepare voor implementatie, u moet:

1. [Een Azure-netwerk instellen](#set-up-an-azure-network) in die virtuele Azure-machines geplaatst worden moeten nadat ze zijn gemaakt na een failover.
2. [Een Azure-opslagaccount instellen](#set-up-an-azure-storage-account) voor gerepliceerde gegevens.
3. [Hallo Hyper-V-hosts voorbereiden](#prepare-the-hyper-v-hosts) tooensure toegang te krijgen tot Hallo vereist URL's.

### <a name="set-up-an-azure-network"></a>Een Azure-netwerk instellen

Een Azure-netwerk instellen. U moet dit zodat hello Azure VM's die zijn gemaakt nadat de failover zijn verbonden tooa netwerk.

* Hallo-netwerk moet zich in Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis.
* Afhankelijk van het resourcemodel Hallo gewenste toouse voor failover is uitgevoerd op Azure VM's, u hebt ingesteld hello Azure-netwerk in [modus Resource Manager](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), of [klassieke modus](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).
* U doet er verstandig aan een netwerk in te stellen voordat u begint. Als u dat niet doet, moet u toodo tijdens de implementatie van Site Recovery.
- Storage-accounts die worden gebruikt door Site Recovery kunnen niet worden [verplaatst](../azure-resource-manager/resource-group-move-resources.md) binnen Hallo hetzelfde, of tussen verschillende abonnementen.


### <a name="set-up-an-azure-storage-account"></a>Een Azure-opslagaccount instellen

- U hebt een standaard/premium toohold gegevens gerepliceerd tooAzure Azure storage-account nodig. [Premium-opslag](../storage/storage-premium-storage.md) wordt doorgaans gebruikt voor virtuele machines die een consistent hoge i/o-prestaties en lage latentie toohost i/o-intensieve werkbelastingen nodig.
- Als u wilt dat toouse een premium account toostore gerepliceerde gegevens, moet u ook een standard-opslag account toostore replicatielogboeken dat vastleggen lopende tooon-premises gegevens is gewijzigd.
- Afhankelijk van het resourcemodel Hallo gewenste toouse voor failover is uitgevoerd op Azure Virtual machines, instellen van een account in [modus Resource Manager](../storage/storage-create-storage-account.md), of [klassieke modus](../storage/storage-create-storage-account-classic-portal.md).
- Het is raadzaam dat u een opslagaccount instellen voordat u begint. U moet toodo tijdens de implementatie van Site Recovery. Hallo-accounts moeten in Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis.
- U kunt niet verplaatsen storage-accounts gebruikt door Site Recovery via resourcegroepen binnen Hallo dezelfde abonnement, of tussen verschillende abonnementen behoren.


### <a name="prepare-hello-hyper-v-hosts"></a>Hallo Hyper-V-hosts voorbereiden

* Zorg ervoor dat Hallo Hyper-V-hosts voldoen aan Hallo [vereisten](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager).
- Zorg ervoor dat de Hallo hosts toegang hebben tot Hallo vereist URL's.


## <a name="create-a-recovery-services-vault"></a>Een Recovery Services-kluis maken
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op **Nieuw** > **Bewaking en beheer** > **Backup en Site Recovery (OMS)**.  

    ![Nieuwe kluis](./media/site-recovery-hyper-v-site-to-azure/new-vault.png)

3. In **naam**, Geef een beschrijvende naam tooidentify Hallo-kluis. Als u meer dan één abonnement hebt, selecteert u een van uw abonnementen.

4. [Maak een nieuwe resourcegroep](../azure-resource-manager/resource-group-template-deploy-portal.md) of Selecteer een bestaande en geef een Azure-regio. Machines worden gerepliceerd toothis regio. toocheck ondersteunde regio's, Zie geografische beschikbaarheid in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).

5. Als u wilt dat tooquickly toegang Hallo kluis van Hallo Dashboard, klikt u op **pincode toodashboard**, en klik vervolgens op **maken**.

    ![Nieuwe kluis](./media/site-recovery-hyper-v-site-to-azure/new-vault-settings.png)

Hallo nieuwe kluis wordt weergegeven in Hallo **Dashboard** > **alle resources** lijst en op Hallo belangrijkste **Recovery Services-kluizen** blade.



## <a name="select-hello-protection-goal"></a>Hallo beveiligingsdoel selecteren

Selecteer wat u tooreplicate, en waar u tooreplicate aan.

1. In Hallo **Recovery Services-kluizen**, selecteer Hallo kluis.
2. Klik in **Aan de slag** op **Site Recovery** > **Infrastructuur voorbereiden** > **Beveiligingsdoel**.

    ![Doelstellingen kiezen](./media/site-recovery-hyper-v-site-to-azure/choose-goals.png)
3. In **beveiligingsdoel**, selecteer **tooAzure**, en selecteer **Ja, met Hyper-V**. Selecteer **Nee** tooconfirm u VMM niet gebruikt. Klik vervolgens op **OK**.

    ![Doelstellingen kiezen](./media/site-recovery-hyper-v-site-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Hallo bronomgeving instellen

Hallo Hyper-V-site instellen, installeert hello Azure Site Recovery Provider en hello Azure Recovery Services agent op Hyper-V-hosts en Hallo site in Hallo kluis registreren.

1. In **infrastructuur voorbereiden**, klikt u op **bron**. tooadd een nieuwe Hyper-V-site als een container voor uw Hyper-V-hosts of clusters, klikt u op **+ Hyper-V-Site**.

    ![Bron instellen](./media/site-recovery-hyper-v-site-to-azure/set-source1.png)
2. In **maken van Hyper-V-site**, Geef een naam voor het Hallo-site. Klik vervolgens op **OK**. Selecteer Hallo site hebt gemaakt Klik op nu **+ Hyper-V Server** tooadd een toohello serversite.

    ![Bron instellen](./media/site-recovery-hyper-v-site-to-azure/set-source2.png)

3. In **Server toevoegen** > **servertype**, controleert u of **Hyper-V-server** wordt weergegeven.

    - Zorg ervoor dat Hallo Hyper-V-server die u wilt tooadd voldoet aan de Hallo [vereisten](#on-premises-prerequisites), en kunnen tooaccess Hallo is opgegeven URL's.
    - Download hello Azure Site Recovery Provider-installatiebestand. U voert dit bestand tooinstall Hallo Provider en Hallo Recovery Services-agent op elke Hyper-V-host.

    ![Bron instellen](./media/site-recovery-hyper-v-site-to-azure/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>Hallo Provider en agent installeren

1. Hallo Provider-installatiebestand op elke host uitvoeren u toohello Hyper-V-site toegevoegd. Als u op een Hyper-V-cluster installeert, moet u setup uitvoeren op elk clusterknooppunt. Installeren en registreren van elk clusterknooppunt Hyper-V zorgt ervoor dat virtuele machines worden beschermd, zelfs als ze via knooppunten migreren.
2. In **Microsoft Update** kunt u updates inschakelen, zodat de providerupdates volgens uw Microsoft Update-beleid worden geïnstalleerd.
3. In **installatie**, accepteer of wijzig Hallo Provider standaardlocatie voor installatie en klik op **installeren**.
4. In **Kluisinstellingen**, klikt u op **Bladeren** tooselect hello kluissleutelbestand die u hebt gedownload. Geef hello Azure Site Recovery-abonnement, Hallo kluisnaam, en Hallo Hyper-V-site toowhich Hallo Hyper-V server behoort.

    ![Serverregistratie](./media/site-recovery-hyper-v-site-to-azure/provider3.png)

5. In **Proxy-instellingen**, hoe Hallo Provider waarop Hyper-V-hosts tooAzure Site Recovery verbindt via internet Hallo opgeven.

    * Als u wilt dat Hallo Provider tooconnect rechtstreeks Selecteer **tooAzure siteherstel zonder een proxy rechtstreeks verbinding gemaakt**.
    * Als uw bestaande proxy verificatie vereist, of u een aangepaste proxy toouse voor Hallo providerverbinding wilt, schakelt u **verbinding maken met Site Recovery via een proxyserver tooAzure**.
    * Als u een proxy gebruikt:
        - Hallo-adres, poort en referenties opgeven
        - Zorg ervoor dat Hallo URL's die worden beschreven in Hallo [vereisten](#prerequisites) via proxy Hallo zijn toegestaan.

    ![internet](./media/site-recovery-hyper-v-site-to-azure/provider7.PNG)

6. Nadat de installatie is voltooid, klikt u op **registreren** tooregister Hallo-server in Hallo kluis.

    ![Installatielocatie](./media/site-recovery-hyper-v-site-to-azure/provider2.png)

7. Nadat de registratie is voltooid, metagegevens van Hallo Hyper-V server worden opgehaald door Azure Site Recovery en Hallo-server wordt weergegeven in **Site Recovery-infrastructuur** > **Hyper-V-Hosts**.


## <a name="set-up-hello-target-environment"></a>Hallo doelomgeving instellen

Geef hello Azure storage-account voor replicatie en hello Azure-netwerk toowhich virtuele Azure-machines na failover verbinding maakt.

1. Klik op **infrastructuur voorbereiden** > **doel**.
2. Hallo-abonnement en resourcegroep Hallo waarin u toocreate Hallo virtuele Azure-machines na een failover wilt selecteren. Kies Hallo implementatie model wilt u toouse in Azure (klassiek of de resource management) voor Hallo virtuele machines.

3. Site Recovery controleert of u een of meer compatibele Azure-opslagaccounts en -netwerken hebt.

    - Als u geen storage-account hebt, klikt u op **en opslag** toocreate een inline-account op basis van een Resource Manager. Meer informatie over [opslagvereisten](site-recovery-prereq.md#azure-requirements).
    - Als u geen Azure-netwerk hebt, klikt u op **+ netwerk** toocreate een inline Resource Manager-netwerk.

    ![Storage](./media/site-recovery-vmware-to-azure/enable-rep3.png)




## <a name="configure-replication-settings"></a>Replicatie-instellingen configureren

1. toocreate een nieuw replicatiebeleid, klikt u op **infrastructuur voorbereiden** > **replicatie-instellingen** > **+ maken en koppelen**.

    ![Netwerk](./media/site-recovery-hyper-v-site-to-azure/gs-replication.png)
2. Geef in **Beleid maken en koppelen** een beleidsnaam op.
3. In **Kopieerfrequentie**, geef aan hoe vaak u tooreplicate deltagegevens na de initiële replicatie van hello (elke 30 seconden, 5 of 15 minuten).

    > [!NOTE]
    > Een 30 tweede frequentie wordt niet ondersteund bij het repliceren van toopremium opslag. Hallo-beperking wordt bepaald door Hallo aantal momentopnamen per blob (100) wordt ondersteund door de premium-opslag. [Meer informatie](../storage/storage-premium-storage.md#snapshots-and-copy-blob).

4. In **herstel bewaarperiode**, geeft u in hoe lang uren Hallo bewaarperiode is voor elk herstelpunt. Virtuele machines kunnen worden hersteld tooany punt in een venster.
5. In **App-consistente momentopname frequentie**, opgeven hoe vaak (1-12 uur) herstelpunten met toepassingsconsistente momentopnamen worden gemaakt.

    - Hyper-V gebruikt twee soorten momentopnamen: standaardmomentopnamen waarmee een incrementele momentopname van Hallo volledige virtuele machine en een toepassingsconsistente momentopnamen waarmee een momentopname van een punt in tijd van de toepassingsgegevens Hallo in Hallo virtuele machine.
    - Toepassingsconsistente momentopnamen gebruiken Volume Shadow Copy Service (VSS) tooensure die toepassingen zich in een consistente status wanneer Hallo momentopname wordt gemaakt.
    - Als u toepassingsconsistente momentopnamen inschakelt, wordt het Hallo-prestaties van toepassingen die worden uitgevoerd op virtuele bronmachines beïnvloeden. Zorg ervoor dat Hallo-waarde lager dan Hallo aantal aanvullende herstelpunten dat u configureert.

6. In **begintijd initiële replicatie**, opgeven wanneer toostart Hallo initiële replicatie. Hallo replicatie vindt plaats via uw internetbandbreedte zodat tooschedule kunt u deze buiten de drukste tijden. Klik vervolgens op **OK**.

    ![Beleid voor replicatie](./media/site-recovery-hyper-v-site-to-azure/gs-replication2.png)

Wanneer u een nieuw beleid maakt, wordt dit automatisch gekoppeld met de Hallo Hyper-V-site. U kunt een Hyper-V-site (en Hallo virtuele machines erin) koppelen aan meerdere beleidsregels voor replicatie in **replicatie** > beleidsnaam > **Hyper-V-Site koppelen**.

## <a name="capacity-planning"></a>Capaciteitsplanning

Nu dat u uw basisinfrastructuur instellen hebt, kunt u nadenkt over capaciteitsplanning en bepalen of u aanvullende resources nodig.

Site Recovery biedt een capaciteit planner toohelp u de juiste resources Hallo voor compute, netwerk en opslag toewijzen. U kunt uitvoeren Hallo planner in de snelle modus voor schattingen op basis van een gemiddelde aantal virtuele machines, schijven en opslag, of in de gedetailleerde modus met aangepaste nummers op Hallo werkbelasting niveau. Voordat u begint moet u:

* Informatie verzamelen over uw replicatieomgeving, waaronder informatie over de virtuele machines, het aantal schijven per virtuele machine en de opslag per schijf.
* Schatting Hallo dagelijkse (verloop) wijzigingssnelheid voor uw gerepliceerde gegevens. U kunt Hallo [Capacity Planner voor Hyper-V Replica](https://www.microsoft.com/download/details.aspx?id=39057) toohelp u dit doen.

1. Klik op **downloaden** toodownload hulpprogramma Hallo en vervolgens uit te voeren. [Hallo-artikel lezen](site-recovery-capacity-planner.md) die wordt meegestuurd met Hallo-hulpprogramma.
2. Wanneer u bent klaar, selecteert u **Ja** in **hebben uitgevoerd Hallo Capacity Planner**?

   ![Capaciteitsplanning](./media/site-recovery-hyper-v-site-to-azure/gs-capacity-planning.png)

Meer informatie over [netwerkbandbreedte beheren](#network-bandwidth-considerations)



## <a name="enable-replication"></a>Replicatie inschakelen

Voordat u begint, zorg ervoor dat uw Azure gebruikersaccount Hallo vereist [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicatie van een nieuwe virtuele machine tooAzure.

Replicatie voor virtuele machines als volgt inschakelen:          

1. Klik op **toepassing repliceren** > **bron**. Nadat u replicatie voor Hallo eerst hebt ingesteld, klikt u op **+ repliceren** tooenable replicatie voor aanvullende machines.

    ![Replicatie inschakelen](./media/site-recovery-hyper-v-site-to-azure/enable-replication.png)
2. In **bron**, selecteer Hallo Hyper-V-site. Klik vervolgens op **OK**.
3. In **doel**Hallo kluis abonnement en selecteer Hallo gewenste toouse in Azure (klassiek of de resource management) na een failover van failover-model.
4. Selecteer Hallo gewenste toouse storage-account. Als u een account dat u wilt dat toouse geen hebt, kunt u [maken van een](#set-up-an-azure-storage-account). Klik vervolgens op **OK**.
5. Selecteer hello Azure-netwerk en subnet toowhich virtuele Azure-machines verbinding maken wanneer ze failover worden gemaakt.

    - Selecteer tooapply Hallo instellingen tooall machines in het netwerk u inschakelen voor replicatie, **nu configureren voor geselecteerde machines**.
    - Selecteer **later configureren** tooselect hello Azure-netwerk per computer.
    - Als u een netwerk dat u wilt dat toouse geen hebt, kunt u [maken van een](#set-up-an-azure-network). Selecteer indien van toepassing een subnet. Klik vervolgens op **OK**.

   ![Replicatie inschakelen](./media/site-recovery-hyper-v-site-to-azure/enable-replication11.png)

6. In **virtuele Machines** > **virtuele machines selecteren**en klik op elke machine die u wilt dat tooreplicate selecteren. U kunt alleen machines selecteren waarvoor replicatie kan worden ingeschakeld. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/site-recovery-hyper-v-site-to-azure/enable-replication5-for-exclude-disk.png)

7. In **eigenschappen** > **eigenschappen configureren**Hallo-besturingssysteem voor virtuele machines Hallo geselecteerd en selecteer Hallo besturingssysteemschijf.
8. Controleer of deze Hallo Azure VM-naam (doelnaam) voldoet aan [vereisten van de virtuele machine van Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
9. Standaard worden alle Hallo schijven Hallo VM geselecteerd voor replicatie, maar u kunt schijven tooexclude wissen ze.
    - U kunt tooexclude schijven tooreduce replicatie bandbreedte. Bijvoorbeeld, wilt u mogelijk niet tooreplicate schijven met tijdelijke gegevens of gegevens die is vernieuwd telkens wanneer een computer of apps (zoals pagefile.sys of Microsoft SQL Server tempdb) opnieuw wordt opgestart. U kunt Hallo schijf uitsluiten van replicatie door geïnstalleerd Hallo-schijf.
    - Alleen standaardschijven kunnen worden uitgesloten. U kunt geen besturingssysteemschijven uitsluiten.
    - We raden u aan geen dynamische schijven uit te sluiten. Met Site Recovery kan niet worden vastgesteld of een virtuele harde schijf in een gast-VM een basisschijf of een dynamische schijf is. Als u alle schijven van de afhankelijke dynamisch volume niet worden uitgesloten, worden Hallo beveiligde dynamische schijf wordt weergegeven als een niet-werkende schijf wanneer hello VM failover wordt uitgevoerd en Hallo gegevens op de schijf niet toegankelijk.
        - Nadat de replicatie is ingeschakeld, kunt u geen schijven meer toevoegen of verwijderen voor replicatie. Als u wilt dat tooadd of uitsluiten van een schijf, moet u toodisable beveiliging voor Hallo VM nodig en vervolgens opnieuw inschakelen.
        - Voor schijven die u handmatig hebt gemaakt in Azure, wordt geen failback uitgevoerd. Als u meer dan drie schijven mislukken en twee rechtstreeks in Azure VM maken, wordt bijvoorbeeld alleen Hallo drie schijven die zijn failover mislukt door Azure tooHyper-V. U kunt geen schijven die handmatig zijn gemaakt in de failback of in de omgekeerde replicatie van Hyper-V tooAzure opnemen.
        - Als u een schijf die nodig is voor een toepassing toooperate uitsluit, na failover tooAzure moet u toocreate handmatig in Azure, zodat die Hallo gerepliceerd toepassing uit te voeren. U kunt ook kan u integreren met Azure automation een herstelplan, toocreate Hallo schijf tijdens de failover van Hallo-machine.

10. Klik op **OK** toosave wijzigingen. Later kunt u eventueel extra eigenschappen instellen.

    ![Replicatie inschakelen](./media/site-recovery-hyper-v-site-to-azure/enable-replication6-with-exclude-disk.png)

11. In **replicatie-instellingen** > **replicatie-instellingen configureren**, Hallo replicatiebeleid u tooapply voor Hallo virtuele machines beveiligde wilt selecteren. Klik vervolgens op **OK**. U kunt het replicatiebeleid Hallo in wijzigen **replicatiebeleid** > beleidsnaam > **instellingen bewerken**. De wijzigingen die u toepast, worden zowel gebruikt voor machines die al worden gerepliceerd, als voor nieuwe machines.


   ![Replicatie inschakelen](./media/site-recovery-hyper-v-site-to-azure/enable-replication7.png)

U kunt de voortgang van Hallo volgen **beveiliging inschakelen** taak **taken** > **Site Recovery-taken**. Na het Hallo **beveiliging voltooien** taak wordt uitgevoerd Hallo machine is gereed voor failover.

### <a name="view-and-manage-vm-properties"></a>Eigenschappen van virtuele machines weergeven en beheren

Het is raadzaam om de eigenschappen van de bronmachine Hallo Hallo te controleren.

1. In **beveiligde Items**, klikt u op **gerepliceerde Items**, en selecteer Hallo-machine.

    ![Replicatie inschakelen](./media/site-recovery-hyper-v-site-to-azure/test-failover1.png)
2. In **eigenschappen**, vindt u replicatie en failover-informatie voor Hallo VM.

    ![Replicatie inschakelen](./media/site-recovery-hyper-v-site-to-azure/test-failover2.png)
3. In **berekening en netwerk** > **eigenschappen berekenen**, kunt u de naam en doel van de grootte van virtuele machine van Azure Hallo opgeven. Hallo naam toocomply met Azure-vereisten wijzigen als u wilt. U kunt ook bekijken en wijzigen van de informatie over het doelnetwerk Hallo, subnet en IP-adres dat wordt toegewezen toohello Azure VM. Let op Hallo volgende:

   * U kunt IP-adres van Hallo doel instellen. Als u een adres niet opgeeft, wordt Hallo failover machine DHCP gebruikt. Als u een adres dat is niet beschikbaar bij een failover instelt, mislukt Hallo failover. Hallo hetzelfde IP-adres van doel kan worden gebruikt voor een testfailover als Hallo adres in het testfailovernetwerk Hallo beschikbaar is.
   * Hallo aantal netwerkadapters wordt bepaald door Hallo-grootte die u voor Hallo doel-virtuele machine, als volgt opgeeft:

     * Als het aantal netwerkadapters op de bronmachine Hallo Hallo kleiner dan of gelijk aantal adapters toohello toegestaan voor de doelgrootte machine Hallo vervolgens Hallo doel hetzelfde aantal adapters als bron Hallo Hallo.
     * Als het aantal adapters voor de virtuele bronmachine Hallo HALLO hallo maximum overschrijden voor Hallo doelgrootte, wordt maximaal Hallo doel wordt gebruikt.
     * Bijvoorbeeld als een bronmachine twee netwerkadapters heeft en de grootte van Hallo doelmachine vier ondersteunt, Hallo doelmachine twee adapters hebben. Als Hallo-bronmachine twee adapters heeft, maar hello ondersteunde doelgrootte biedt alleen ondersteuning voor een hebben Hallo doelmachine slechts één adapter.     
     * Als Hallo VM meerdere netwerkadapters heeft worden deze allemaal verbonden toohello hetzelfde netwerk.
     * Als Hallo virtuele machine meerdere netwerkadapters Hallo heeft eerst weergegeven in de lijst hello wordt Hallo *standaard* netwerkadapter in hello Azure virtuele machine.

     ![Replicatie inschakelen](./media/site-recovery-hyper-v-site-to-azure/test-failover4.png)

4. In **schijven**, ziet u Hallo-besturingssysteem en gegevensschijven op Hallo VM die wordt gerepliceerd.

#### <a name="managed-disks"></a>Managed Disks

In **berekening en netwerk** > **eigenschappen berekenen**, u kunt instellen "Beheerde schijven gebruiken" te 'Ja' voor Hallo VM als u tooattach beheerde schijven tooyour machine op migratie tooAzure wilt. Beheerde schijven vereenvoudigt Schijfbeheer voor Azure IaaS VM's met Hallo storage-accounts die zijn gekoppeld aan het VM-schijven Hallo beheren. [Meer informatie over beheerde schijven](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - Beheerde schijven zijn gemaakt en gekoppelde toohello virtuele machine alleen op een failover-tooAzure. Over het inschakelen van beveiliging, blijven gegevens uit de lokale machines tooreplicate toostorage accounts.
   Beheerde schijven kunnen alleen voor virtuele machines die zijn geïmplementeerd met behulp van Hallo Resource manager-implementatiemodel worden gemaakt.

  > [!NOTE]
  > Failback vanuit Azure tooon lokale Hyper-V-omgeving is momenteel niet ondersteund voor computers met beheerde-schijven. "Beheerde schijven gebruiken" te 'Ja' alleen ingesteld als u van plan toomigrate deze machine tooAzure bent.

   - Als u "Beheerde schijven gebruiken" te 'Ja', is alleen beschikbaarheidssets in de resourcegroep Hallo met "Beheerde schijven gebruiken" set te 'Ja' beschikbaar voor selectie. Dit is omdat de virtuele machines met beheerde schijven kan alleen deel uitmaken van beschikbaarheidssets met 'Gebruik beheerd schijven' eigenschappenset te 'Ja'. Zorg ervoor dat u beschikbaarheidssets met 'Gebruik beheerd schijven' eigenschap is ingesteld op basis van uw schijven opzet toouse beheerd op failover maken. Op dezelfde manier als u "Beheerde schijven gebruiken" te 'Nee', is alleen in beschikbaarheidssets voor de resourcegroep Hallo met "Beheerde schijven gebruiken" eigenschappenset te 'Nee' beschikbaar voor selectie. [Meer informatie over beheerde schijven en beschikbaarheidssets](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Als het Hallo-opslagaccount gebruikt voor replicatie is versleuteld met versleuteling van de opslagruimte op elk gewenst moment in de tijd, mislukt het maken van beheerde schijven tijdens failover. U kunt instellen "Beheerde schijven gebruiken" te 'Nee' en probeer de failover of schakel de beveiliging voor Hallo virtuele machine en Beveilig de tooa storage-account die geen versleuteling van de opslagruimte-service is ingeschakeld op elk punt in tijd.
  > [Meer informatie over Versleuteling voor opslagservice en beheerde schijven](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-hello-deployment"></a>Hallo-implementatie testen

tootest hello implementatie kunt u een testfailover voor één virtuele machine of een herstelplan dat een of meer virtuele machines bevat uitvoeren.

### <a name="before-you-start"></a>Voordat u begint

 - Als u wilt dat tooconnect tooAzure virtuele machines met RDP na een failover meer informatie over [tooconnect voorbereiden](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - toofully test u toocopy van Active Directory en DNS moet in uw testomgeving. [Meer informatie](site-recovery-active-directory.md#test-failover-considerations).

### <a name="run-a-test-failover"></a>Een testfailover uitvoeren

1. toofail via één computer in **gerepliceerde Items**, klikt u op Hallo VM > **+ Testfailover** pictogram.
2. plan toofail via een herstelbewerking **herstelplannen**, klik met de rechtermuisknop Hallo plan > **Testfailover**. een herstelplan toocreate [Volg deze instructies](site-recovery-create-recovery-plans.md).
3. In **Testfailover**, selecteer hello Azure-netwerk toowhich virtuele Azure-machines moet worden verbonden nadat er failover plaatsvindt.
4. Klik op **OK** toobegin Hallo failover. U kunt de voortgang volgen door te klikken op Hallo VM tooopen eigenschappen of op Hallo **Testfailover** taak in de kluisnaam > **taken** > **Site Recovery-taken**.
5. Nadat de failover Hallo is voltooid, dient u zich kunt toosee Hallo replica machine van Azure in hello Azure-portal weergegeven > **virtuele Machines**. U moet ervoor zorgen dat Hallo VM is de juiste grootte hello, of deze is verbonden met het juiste netwerk toohello en dat deze wordt uitgevoerd.
6. Als u voorbereid op verbindingen na een failover, moet u kunnen tooconnect toohello Azure VM.
7. Wanneer u bent klaar, klikt u op op **testfailover opschonen** op Hallo herstelplan. In **notities** opnemen en eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo opslaan. Hiermee verwijdert u Hallo virtuele machines die zijn gemaakt tijdens de testfailover.

Voor meer informatie lezen Hallo [Test failover tooAzure](site-recovery-test-failover-to-azure.md) artikel.



## <a name="monitor-hello-deployment"></a>Monitor Hallo-implementatie

Hallo-configuratie-instellingen, en de status voor uw implementatie van Site Recovery bewaken:

1. Klik op Hallo kluis naam tooaccess hello **Essentials** dashboard. In dit dashboard kunt u Site Recovery-taken, replicatiestatus herstelplannen, serverstatus en gebeurtenissen bijhouden.  

    ![Essentials](./media/site-recovery-hyper-v-site-to-azure/essentials.png)
2. In Hallo **Health** tegel u siteservers die zijn momenteel problemen en gebeurtenissen die worden gegenereerd door Site Recovery in Hallo afgelopen 24 uur Hallo kunt bewaken. U kunt Essentials tooshow Hallo tegels en indelingen die vooral handig tooyou zijn, inclusief Hallo status van de andere Site Recovery en de Backup-kluizen aanpassen.
3. U kunt beheren en controleren van replicatie in Hallo **gerepliceerde Items**, **herstelplannen**, en **Site Recovery-taken** tegels. U kunt inzoomen op taken voor meer informatie in **taken** > **Site Recovery-taken**.

## <a name="command-line-provider-and-agent-installation"></a>Provider en agent-installatie vanaf de opdrachtregel

Hello Azure Site Recovery Provider en agent kunnen ook worden geïnstalleerd met Hallo opdrachtregel te volgen. Deze methode kan gebruikte tooinstall Hallo-provider op een Server Core voor Windows Server 2012 R2 zijn.

1. Hallo-Provider en de registratiesleutel sleutel tooa installatiemap downloaden. Bijvoorbeeld: C:\ASR.
2. Voer deze opdrachten tooextract Hallo Provider-installatieprogramma vanaf een opdrachtprompt met verhoogde bevoegdheid:

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Voer deze opdracht tooinstall Hallo-onderdelen:

            C:\ASR> setupdr.exe /i
4. Voer vervolgens deze opdrachten tooregister Hallo-server in de kluis Hallo:

            CD C:\Program Files\Microsoft Azure Site Recovery Provider\
            C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file>

<br/>
Waar:

* **/ Credentials**: verplichte parameter waarmee Hallo locatie in welke Hallo registratiesleutelbestand zich bevindt  
* **/ FriendlyName**: verplichte parameter voor de naam Hallo van Hallo Hyper-V-hostserver die wordt weergegeven in hello Azure Site Recovery-portal.
* **/ proxyaddress**: een optionele parameter waarmee het adres van de proxyserver Hallo Hallo.
* **/ proxyport** : optionele parameter waarmee het Hallo-poort van de proxyserver Hallo.
* **proxyusername**: optionele parameter waarmee de proxygebruikersnaam hello (als de proxyserver verificatie is vereist).
* **/ proxypassword**: optionele parameter waarmee hello wachtwoord voor verificatie met de proxyserver hello (als de proxyserver verificatie is vereist).


## <a name="network-bandwidth-considerations"></a>Overwegingen voor netwerkbandbreedte
U kunt Hallo [Capaciteitsplanner voor Hyper-V](site-recovery-capacity-planner.md) toocalculate Hallo bandbreedte die u nodig hebt voor replicatie (initiële replicatie en deltareplicaties). toocontrol hello bedrag van het gebruik van netwerkbandbreedte voor de replicatiegroep die u hebt een aantal opties:

* **Bandbreedte beperken**: Hyper-V-verkeer dat wordt gerepliceerd tooAzure verloopt via een specifieke Hyper-V-host. U kunt de bandbreedte op Hallo hostserver beperken.
* **Bandbreedte aanpassen**: U kunt zelf bepalen hoeveel Hallo-bandbreedte die wordt gebruikt voor replicatie via diverse registersleutels.

### <a name="throttle-bandwidth"></a>Bandbreedte beperken
1. Hallo Microsoft Azure Backup MMC-module openen op Hallo Hyper-V-hostserver. Een snelkoppeling naar Microsoft Azure Backup is standaard beschikbaar zijn op Hallo bureaublad of in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Klik in de module Hallo **eigenschappen wijzigen**.
3. Op Hallo **bandbreedtebeperking** tabblad Selecteer **inschakelen voor gebruik van internetbandbreedte voor back-upbewerkingen**, en Hallo limieten instellen voor werk en niet-werk uren. Geldige bereiken zijn afkomstig van 512 Kbps too102 Mbps per seconde.

    ![Bandbreedte beperken](./media/site-recovery-hyper-v-site-to-azure/throttle2.png)

U kunt ook Hallo [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset beperking. Hier volgt een voorbeeld:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** geeft aan dat er geen beperking is vereist.

### <a name="influence-network-bandwidth"></a>Netwerkbandbreedte beïnvloeden
1. Navigeer te in Hallo register**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * tooinfluence hello bandbreedte netwerkverkeer op een schijf replicerende wijzigen Hallo waarde Hallo **UploadThreadsPerVM**, of maak Hallo sleutel aan als deze niet bestaat.
   * tooinfluence hello bandbreedte voor failbackverkeer vanuit Azure, Hallo waarde wijzigen **DownloadThreadsPerVM**.
2. Hallo-standaardwaarde is 4. In een netwerk 'overprovisioning', moeten deze registersleutels van Hallo standaardwaarden worden gewijzigd. Hallo maximum is 32. Verkeer toooptimize Hallo waarde bewaken.

## <a name="next-steps"></a>Volgende stappen

Nadat de initiële replicatie is voltooid en u Hallo-implementatie hebt getest, kunt u failovers kunt aanroepen, zoals Hallo noodzaak zich voordoet. [Meer informatie](site-recovery-failover.md) over verschillende soorten failovers en hoe toorun ze.
