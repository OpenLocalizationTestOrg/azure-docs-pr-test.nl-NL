---
title: aaaReplicate Hyper-V-machines in VMM-clouds tooAzure | Microsoft Docs
description: Indelen van replicatie, failovers en herstel van Hyper-V-machines in System Center VMM-clouds tooAzure beheerd
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: 84182fe4b63862ac7643208a22f236a7515a25a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>Hyper-V virtuele machines in VMM-clouds tooAzure met Site Recovery in hello Azure-portal repliceren
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-azure.md)
> * [Klassieke Azure Portal](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell klassiek](site-recovery-deploy-with-powershell.md)


Dit artikel wordt beschreven hoe tooreplicate lokale Hyper-V virtuele machines die worden beheerd in System Center VMM-clouds tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.

Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Meer informatie als u wilt toomigrate machines tooAzure (zonder failback), [in dit artikel](site-recovery-migrate-to-azure.md).


## <a name="deployment-steps"></a>Implementatiestappen

Volgt Hallo artikel toocomplete implementatie:


1. [Meer informatie](site-recovery-components.md) over Hallo-architectuur voor deze implementatie. Lees ook [meer informatie](site-recovery-hyper-v-azure-architecture.md) over de werking van Hyper-V-replicatie in Site Recovery.
2. Controleer de vereisten en beperkingen.
3. Stel Azure-netwerk- en opslagaccounts in.
4. Bereid Hallo lokale VMM-server en Hyper-V-hosts.
5. Maak een Recovery Services-kluis. Hallo-kluis bevat configuratie-instellingen en stuurt replicatie.
6. Geef de broninstellingen op. Hallo VMM-server geregistreerd in kluis Hallo. Hello Azure Site Recovery Provider installeren op Hallo VMM server-installatie Hallo Microsoft Recovery Services agent op Hyper-V-hosts.
7. Stel de doel- en replicatie-instellingen in.
8. Replicatie inschakelen voor Hallo virtuele machines.
9. Een test failover toomake, controleren of dat alles werkt zoals verwacht worden uitgevoerd.



## <a name="prerequisites"></a>Vereisten


**Vereiste voor ondersteuning** | **Details**
--- | ---
**Azure** | Meer informatie over [Azure-vereisten](site-recovery-prereq.md#azure-requirements).
**On-premises servers** | [Meer informatie](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-in-vmm-clouds-to-azure) over de vereisten voor Hallo lokale VMM-server en Hyper-V-hosts.
**On-premises Hyper-V-VM's** | Virtuele machines die u wilt dat tooreplicate moet worden uitgevoerd een [ondersteund besturingssysteem](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), en voldoet aan de [vereisten voor Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**Azure-URL's** | Hallo VMM-beheerserver moet toegang tot toothese URL's:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Als u IP-adressen gebaseerde firewallregels, moet u dat ze tooAzure communicatie toestaan.<br/></br> Hallo toestaan [Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653), en Hallo HTTPS (443)-poort.<br/></br> IP-adresbereiken voor hello Azure-regio van uw abonnement en voor VS-West (gebruikt voor toegangsbeheer en identiteitsbeheer) toestaan.


## <a name="prepare-for-deployment"></a>Implementatie voorbereiden
tooprepare voor implementatie, moet u:

1. [Een Azure-netwerk instellen](#set-up-an-azure-network) waarin de virtuele Azure-machines worden opgeslagen na de failover.
2. [Een Azure-opslagaccount instellen](#set-up-an-azure-storage-account) voor gerepliceerde gegevens.
3. [Hallo VMM-server voorbereiden](#prepare-the-vmm-server) voor implementatie van Site Recovery.
4. Voorbereiden op netwerktoewijzing. Stel netwerken zodanig in dat u tijdens de implementatie van Site Recovery netwerktoewijzing kunt configureren.

### <a name="set-up-an-azure-network"></a>Een Azure-netwerk instellen
U moet een Azure-netwerk toowhich virtuele Azure-machines die zijn gemaakt nadat de failover verbinding maakt.

* Hallo-netwerk moet zich in Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis.
* Afhankelijk van het resourcemodel Hallo gewenste toouse voor failover is uitgevoerd op Azure VM's, u hebt ingesteld hello Azure-netwerk in [modus Resource Manager](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) of [klassieke modus](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).
* U doet er verstandig aan een netwerk in te stellen voordat u begint. Als u dat niet doet, moet u toodo tijdens de implementatie van Site Recovery.
Azure-netwerken die worden gebruikt door Site Recovery kunnen niet worden [verplaatst](../azure-resource-manager/resource-group-move-resources.md) binnen Hallo hetzelfde, of tussen verschillende abonnementen.

### <a name="set-up-an-azure-storage-account"></a>Een Azure-opslagaccount instellen
* U hebt een standaard/premium toohold gegevens gerepliceerd tooAzure Azure storage-account nodig. [Premium-opslag](../storage/common/storage-premium-storage.md) wordt gebruikt voor virtuele machines die een consistent hoge i/o-prestaties en lage latentie toohost i/o-intensieve werkbelastingen nodig. Als u wilt dat toouse een premium account toostore gerepliceerde gegevens, moet u ook een standard-opslag account toostore replicatielogboeken dat vastleggen lopende tooon-premises gegevens is gewijzigd. Hallo-account moet zich in Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis.
* Afhankelijk van het resourcemodel Hallo gewenste toouse voor failover is uitgevoerd op Azure Virtual machines, instellen van een account in [modus Resource Manager](../storage/common/storage-create-storage-account.md) of [klassieke modus](../storage/common/storage-create-storage-account.md).
* U doet er verstandig aan een account in te stellen voordat u begint. Als u dat niet doet, moet u toodo tijdens de implementatie van Site Recovery.
- Houd er rekening mee dat de storage-accounts die worden gebruikt door Site Recovery kunnen niet worden [verplaatst](../azure-resource-manager/resource-group-move-resources.md) binnen Hallo hetzelfde, of tussen verschillende abonnementen.

### <a name="prepare-hello-vmm-server"></a>Hallo VMM-server voorbereiden
* Ervoor zorgen dat Hallo VMM-server voldoet aan de Hallo [vereisten](#prerequisites).
* Tijdens de implementatie van Site Recovery kunt u opgeven dat alle clouds op een VMM-server beschikbaar zijn in hello Azure-portal moet. Als u wilt dat alleen bepaalde clouds tooappear in Hallo-portal, kunt u die instelling in de cloud in VMM-beheerconsole Hallo Hallo inschakelen.

### <a name="prepare-for-network-mapping"></a>Voorbereiden op netwerktoewijzing
Tijdens de implementatie van Site Recovery moet u netwerktoewijzing instellen. Koppelingen van Netwerktoewijzingen tussen bron VMM VM-netwerken en gericht op Azure-netwerken tooenable hello te volgen:

* Machines met failover op Hallo hetzelfde netwerk kan verbinding maken met andere tooeach, zelfs als ze failover niet Hallo dezelfde manier of Hallo hetzelfde herstelplan wordt uitgevoerd.
* Als een netwerkgateway is ingesteld op Hallo Azure-doelnetwerk, kunnen virtuele Azure-machines verbinding tooon-premises virtuele machines maken.
* tooset up netwerktoewijzing, dit is wat u nodig hebt:

  * Zorg ervoor dat virtuele machines op Hallo bron Hyper-V-hostserver verbonden tooa VMM VM-netwerk. Dit netwerk moet gekoppelde tooa logisch netwerk dat is gekoppeld aan Hallo cloud.
  * Een Azure-netwerk zoals [hierboven](#set-up-an-azure-network) wordt beschreven

## <a name="create-a-recovery-services-vault"></a>Een Recovery Services-kluis maken
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op **Nieuw** > **Bewaking en beheer** > **Backup en Site Recovery (OMS)**.

    ![Nieuwe kluis](./media/site-recovery-vmm-to-azure/new-vault3.png)
3. In **naam**, Geef een beschrijvende naam tooidentify Hallo-kluis. Als u meer dan één abonnement hebt, selecteert u een van uw abonnementen.
4. [Maak een resourcegroep](../azure-resource-manager/resource-group-template-deploy-portal.md) of selecteer een bestaande resourcegroep. Geef een Azure-regio op. Machines worden gerepliceerd toothis regio. toocheck ondersteunde regio's Zie geografische beschikbaarheid in [prijsinformatie voor Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Als u wilt dat tooquickly toegang Hallo kluis van Hallo Dashboard, klikt u op **pincode toodashboard** > **kluis maken**.

    ![Nieuwe kluis](./media/site-recovery-vmm-to-azure/new-vault.png)

Hallo nieuwe kluis wordt weergegeven op Hallo **Dashboard** > **alle resources**, en op Hallo belangrijkste **Recovery Services-kluizen** blade.


## <a name="select-hello-protection-goal"></a>Hallo beveiligingsdoel selecteren

Selecteer wat u tooreplicate, en waar u tooreplicate aan.

1. In **Recovery Services-kluizen**, selecteer Hallo kluis.
2. Klik in **Aan de slag** op **Site Recovery** > **Infrastructuur voorbereiden** > **Beveiligingsdoel**.

    ![Doelstellingen kiezen](./media/site-recovery-vmm-to-azure/choose-goals.png)
3. In **beveiligingsdoel** Selecteer **tooAzure**, en selecteer **Ja, met Hyper-V**. Selecteer **Ja** tooconfirm u VMM toomanage Hyper-V-hosts en Hallo herstelsite. Klik vervolgens op **OK**.

## <a name="set-up-hello-source-environment"></a>Hallo bronomgeving instellen

Hello Azure Site Recovery Provider installeren op Hallo VMM-server en Hallo-server in Hallo kluis registreren. Installeer hello Azure Recovery Services agent op Hyper-V-hosts.

1. Klik op **Infrastructuur voorbereiden** > **Bron**.

    ![Bron instellen](./media/site-recovery-vmm-to-azure/set-source1.png)

2. In **bron voorbereiden**, klikt u op **+ VMM** tooadd een VMM-server.

    ![Bron instellen](./media/site-recovery-vmm-to-azure/set-source2.png)

3. In **Server toevoegen**, controleert u of **System Center VMM-server** wordt weergegeven in **servertype** en die Hallo VMM-server voldoet aan Hallo [vereisten en -URL vereisten voor](#prerequisites).
4. Download hello Azure Site Recovery Provider-installatiebestand.
5. Download de registratiesleutel Hallo. U hebt deze nodig wanneer u de installatie uitvoert. Hallo-sleutel is vijf dagen na het genereren ervan geldig.

    ![Bron instellen](./media/site-recovery-vmm-to-azure/set-source3.png)


## <a name="install-hello-provider-on-hello-vmm-server"></a>Hallo Provider installeren op Hallo VMM-server

1. Hallo Provider-installatiebestand op Hallo VMM-server wordt uitgevoerd.
2. In **Microsoft Update** kunt u updates inschakelen, zodat de providerupdates volgens uw Microsoft Update-beleid worden geïnstalleerd.
3. In **installatie**, accepteer of wijzig Hallo Provider standaardlocatie voor installatie en klik op **installeren**.

    ![Installatielocatie](./media/site-recovery-vmm-to-azure/provider2.png)
4. Wanneer de installatie is voltooid, klikt u op **registreren** tooregister Hallo VMM-server in Hallo kluis.
5. In Hallo **Kluisinstellingen** pagina, klikt u op **Bladeren** kluissleutelbestand hello tooselect. Hello Azure Site Recovery-abonnement en de kluisnaam Hallo opgeven.

    ![Serverregistratie](./media/site-recovery-vmm-to-azure/provider10.PNG)
6. In **internetverbinding**, hoe Hallo Provider die wordt uitgevoerd op Hallo VMM-server de tooSite herstel verbinding maken via internet Hallo opgeven.

   * Als u rechtstreeks Hallo Provider tooconnect wilt, schakelt **tooAzure siteherstel zonder een proxy rechtstreeks verbinding gemaakt**.
   * Als uw bestaande proxy verificatie vereist, of u een aangepaste proxy toouse wilt, schakelt u **verbinding maken met Site Recovery via een proxyserver tooAzure**.
   * Als u een aangepaste proxy gebruikt, geef Hallo-adres, poort en referenties.
   * Als u een proxy gebruikt, u moet hebben al toegestaan Hallo URL's die worden beschreven [vereisten](#on-premises-prerequisites).
   * Als u een aangepaste proxy gebruikt, een VMM RunAs-account (DRAProxyAccount) wordt automatisch gemaakt met Hallo opgegeven proxyreferenties. Hallo-proxyserver zodanig configureren dat dit account kan worden geverifieerd. Hallo VMM RunAs-Accountinstellingen kunnen worden gewijzigd in Hallo VMM-console. In **instellingen**, vouw **beveiliging** > **Run As-Accounts**, en wijzig vervolgens Hallo wachtwoord voor DRAProxyAccount. U moet toorestart Hallo VMM-service zodat deze instelling wordt van kracht.

     ![internet](./media/site-recovery-vmm-to-azure/provider13.PNG)
7. Accepteer of wijzig de locatie Hallo van een SSL-certificaat dat automatisch gegenereerd voor gegevensversleuteling. Dit certificaat wordt gebruikt als u gegevensversleuteling voor een cloud die wordt beveiligd door Azure in hello Azure Site Recovery-portal inschakelt. Bewaar dit certificaat op een veilige plaats. Wanneer u een failover-tooAzure uitvoert moet u deze toodecrypt, als gegevensversleuteling is ingeschakeld.

    > [!NOTE]
    > Het verdient aanbeveling toouse Hallo mogelijkheid van stationsversleuteling geleverd door Azure voor het versleutelen van gegevens in rust in plaats van met de optie Hallo gegevens versleuteling geleverd door Azure Site Recovery. mogelijkheid van stationsversleuteling Hallo verstrekt door Azure kan worden ingeschakeld voor een opslag >-account in en helpt leveren betere prestaties als Hallo codering/decodering wordt verwerkt door de Azure-opslag.
    > [Meer informatie over de Storage-versleutelingsservice van Azure](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption).
    
8. In **servernaam**, Geef een beschrijvende naam tooidentify Hallo VMM-server in Hallo kluis. Geef in een clusterconfiguratie Hallo VMM-clusterrolnaam op.
9. Schakel **cloudmetagegevens synchroniseren**, als u wilt dat toosynchronize metagegevens voor alle clouds op Hallo VMM-server op Hallo kluis. Deze actie hoeft alleen toohappen eenmaal op elke server. Als u niet toosynchronize alle clouds wilt, kunt u laat u deze instelling uitgeschakeld en synchroniseert u elke cloud afzonderlijk in de eigenschappen van de cloud Hallo in Hallo VMM-console. Klik op **registreren** toocomplete Hallo proces.

    ![Serverregistratie](./media/site-recovery-vmm-to-azure/provider16.PNG)
10. De registratie begint. Nadat de registratie is voltooid, Hallo-server wordt weergegeven in **Site Recovery-infrastructuur** > **VMM-Servers**.


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>Hello Azure Recovery Services-agent installeren op Hyper-V-hosts

1. Nadat u Hallo Provider hebt ingesteld, moet u toodownload Hallo-installatiebestand voor hello Azure Recovery Services agent. Voer setup uit op elke Hyper-V-server in Hallo VMM-cloud.

    ![Hyper-V-sites](./media/site-recovery-vmm-to-azure/hyperv-agent1.png)
2. Klik in **Controle van vereisten** op **Volgende**. Ontbrekende vereiste onderdelen worden automatisch geïnstalleerd.

    ![Vereisten voor de Recovery Services-agent](./media/site-recovery-vmm-to-azure/hyperv-agent2.png)
3. In **installatie-instellingen**Accepteer of wijzig de installatielocatie Hallo en Hallo cachelocatie. U kunt Hallo-cache configureren op een station met ten minste 5 GB aan opslagruimte maar we raden een cachestation met 600 GB of meer aan vrije ruimte. Klik vervolgens op **Installeren**.
4. Nadat de installatie is voltooid, klikt u op **sluiten** toofinish.

    ![MARS-agent registreren](./media/site-recovery-vmm-to-azure/hyperv-agent3.png)

### <a name="command-line-installation"></a>Installatie vanaf de opdrachtregel
U kunt Hallo Microsoft Azure Recovery Services Agent installeren vanaf de opdrachtregel met behulp van de volgende opdracht Hallo:

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>Internet proxy toegang tooSite herstel van Hyper-V-hosts instellen

Hallo Recovery Services agent waarop Hyper-V-hosts moet internet toegang tooAzure voor VM-replicatie. Als u toegang hebt tot Hallo internet via een proxy instellen als volgt:

1. Open Hallo Microsoft Azure Backup MMC-module op Hallo Hyper-V-host. Een snelkoppeling naar Microsoft Azure Backup is standaard beschikbaar zijn op Hallo bureaublad of in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Klik in het Hallo-module op **eigenschappen wijzigen**.
3. Op Hallo **proxyconfiguratie** tabblad, proxyservergegevens opgeven.

    ![MARS-agent registreren](./media/site-recovery-vmm-to-azure/mars-proxy.png)
4. Controleer die agent Hallo Hallo URL's die worden beschreven in Hallo kan bereiken [vereisten](#on-premises-prerequisites).

## <a name="set-up-hello-target-environment"></a>Hallo doelomgeving instellen
Geef hello Azure storage-account toobe gebruikt voor replicatie en hello Azure-netwerk toowhich virtuele Azure-machines na failover verbinding maakt.

1. Klik op **infrastructuur voorbereiden** > **doel**en selecteer Hallo abonnement Hallo resourcegroep waar u toocreate Hallo failover van virtuele machines. Hallo-implementatiemodel dat u toouse in Azure (klassiek of de resource management) voor Hallo failover van virtuele machines wilt kiezen.

    ![Storage](./media/site-recovery-vmm-to-azure/enablerep3.png)

2. Site Recovery controleert of u een of meer compatibele Azure-opslagaccounts en -netwerken hebt.

    ![Storage](./media/site-recovery-vmm-to-azure/compatible-storage.png)

3. Als u een opslagaccount dat nog niet hebt gemaakt, en toocreate een gewenste met Resource Manager, klikt u op **+ opslagaccount** toodo dat inline.  Op Hallo **storage-account maken** blade een naam, type, abonnement en locatie opgeven. Hallo-account moet zich op Hallo dezelfde locatie als Hallo Recovery Services-kluis.

   ![Storage](./media/site-recovery-vmm-to-azure/gs-createstorage.png)


   * Als u een opslagaccount met behulp van het klassieke model Hallo toocreate wilt, doet u dat in hello Azure-portal. [Meer informatie](../storage/common/storage-create-storage-account.md)
   * Als u een premium storage-account voor gerepliceerde gegevens, instellen van een extra standard-opslagaccount, toostore replicatielogboeken die de doorlopende wijzigingen tooon-premises gegevens vastleggen.
5. Als u een Azure-netwerk dat nog niet hebt gemaakt, en toocreate een gewenste met Resource Manager, klikt u op **+ netwerk** toodo dat inline. Op Hallo **virtueel netwerk maken** blade een netwerknaam, adresbereik subnetgegevens, abonnement en locatie opgeven. Hallo-netwerk moet zich in Hallo dezelfde locatie als Hallo Recovery Services-kluis.

   ![Netwerk](./media/site-recovery-vmm-to-azure/gs-createnetwork.png)

   Als u een netwerk met het klassieke model Hallo toocreate wilt, doet u dat in hello Azure-portal. [Meer informatie](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).

### <a name="configure-network-mapping"></a>Netwerktoewijzing configureren

* [Lees](#prepare-for-network-mapping) een kort overzicht van wat netwerktoewijzing inhoudt.
* Verifieer dat de virtuele machines op Hallo VMM-server verbonden tooa VM-netwerk zijn en dat u ten minste één virtuele Azure-netwerk hebt gemaakt. Meerdere VM-netwerken kunnen worden toegewezen tooa één Azure-netwerk.

Configureer het toewijzen als volgt:

1. In **Site Recovery-infrastructuur** > **Netwerktoewijzingen** > **netwerktoewijzing**, klikt u op Hallo **+ netwerktoewijzing**  pictogram.

    ![Netwerktoewijzing](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. In **netwerktoewijzing toevoegen**, selecteer Hallo bron-VMM-server, en **Azure** als Hallo doel.
3. Controleer of u Hallo-abonnement en Hallo implementatiemodel na een failover.
4. In **Bronnetwerk**, selecteer Hallo bron on-premises VM-netwerk gewenste toomap uit die zijn gekoppeld aan de VMM-server Hallo Hallo-lijst.
5. In **doelnetwerk**, selecteer hello Azure-netwerk in welke replica virtuele Azure-machines geplaatst worden moeten nadat ze zijn gemaakt. Klik vervolgens op **OK**.

    ![Netwerktoewijzing](./media/site-recovery-vmm-to-azure/network-mapping2.png)

Dit is wat er gebeurt wanneer er netwerktoewijzing wordt uitgevoerd:

* Bestaande virtuele machines op Hallo bron VM-netwerk zijn verbonden toohello doelnetwerk bij toewijzing begint. Nieuwe virtuele machines verbonden toohello bron VM-netwerk zijn verbonden toohello toegewezen Azure-netwerk wanneer er replicatie plaatsvindt.
* Als u een bestaande netwerktoewijzing wijzigt, gerepliceerde virtuele machines verbinding maken met behulp van de nieuwe instellingen Hallo.
* Als Hallo doelnetwerk meerdere subnetten heeft en een van deze subnetten Hallo heeft dezelfde naam als het subnet waarop Hallo bron virtuele machine zich bevindt en vervolgens Hallo replica virtuele machine verbindt toothat Doelsubnet na een failover.
* Als er geen Doelsubnet met een overeenkomende naam, verbindt Hallo virtuele machine toohello eerste subnet in het Hallo-netwerk.

## <a name="configure-replication-settings"></a>Replicatie-instellingen configureren
1. toocreate een nieuw replicatiebeleid, klikt u op **infrastructuur voorbereiden** > **replicatie-instellingen** > **+ maken en koppelen**.

    ![Netwerk](./media/site-recovery-vmm-to-azure/gs-replication.png)
2. Geef in **Beleid maken en koppelen** een beleidsnaam op.
3. In **Kopieerfrequentie**, geef aan hoe vaak u tooreplicate deltagegevens na de initiële replicatie van hello (elke 30 seconden, 5 of 15 minuten).

    > [!NOTE]
    >  Een 30 tweede frequentie wordt niet ondersteund bij het repliceren van toopremium opslag. Hallo-beperking wordt bepaald door Hallo aantal momentopnamen per blob (100) wordt ondersteund door de premium-opslag. [Meer informatie](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. In **herstel bewaarperiode**, in uren opgeven hoe lang de retentieperiode Hallo wordt worden voor elk herstelpunt. Beveiligde machines kunnen worden hersteld tooany punt in een venster.
5. Geef in **Frequentie van de app-consistente momentopname** op hoe vaak (elke 1-12 uur) er herstelpunten moeten worden gemaakt met toepassingsconsistente momentopnamen. Hyper-V gebruikt twee soorten momentopnamen: standaardmomentopnamen waarmee een incrementele momentopname van Hallo volledige virtuele machine en een toepassingsconsistente momentopnamen waarmee een momentopname van een punt in tijd van de toepassingsgegevens Hallo in Hallo virtuele machine. Toepassingsconsistente momentopnamen gebruiken Volume Shadow Copy Service (VSS) tooensure die toepassingen zich in een consistente status wanneer Hallo momentopname wordt gemaakt. Houd er rekening mee dat als u toepassingsconsistente momentopnamen inschakelt, het invloed is op Hallo prestaties van toepassingen die worden uitgevoerd op virtuele machines die bron. Zorg ervoor dat Hallo-waarde lager dan Hallo aantal aanvullende herstelpunten dat u configureert.
6. In **begintijd initiële replicatie**, geven wanneer toostart Hallo initiële replicatie. Hallo replicatie vindt plaats via uw internetbandbreedte zodat tooschedule kunt u deze buiten de drukste tijden.
7. In **versleutelen van gegevens die zijn opgeslagen in Azure**, opgeven of tooencrypt op rest-gegevens in Azure storage. Klik vervolgens op **OK**.

    ![Beleid voor replicatie](./media/site-recovery-vmm-to-azure/gs-replication2.png)
8. Wanneer u een nieuw beleid maakt is deze automatisch gekoppeld aan Hallo VMM-cloud. Klik op **OK**. U kunt aanvullende VMM-clouds (en Hallo virtuele machines erin) koppelen aan dit replicatiebeleid in **replicatie** > beleidsnaam > **VMM-Cloud koppelen**.

    ![Beleid voor replicatie](./media/site-recovery-vmm-to-azure/policy-associate.png)

## <a name="capacity-planning"></a>Capaciteitsplanning

Nu u de basisinfrastructuur hebt ingesteld, kunt u gaan nadenken over de capaciteitsplanning en nagaan of u aanvullende resources nodig hebt.

Site Recovery biedt een capaciteit planner toohelp u de juiste resources Hallo toewijzen voor uw bronomgeving, onderdelen van Site Recovery, netwerken en opslag. In de snelle modus voor schattingen op basis van een gemiddelde aantal virtuele machines, schijven en opslag, of in de gedetailleerde modus waarin ingevoerde cijfers op Hallo werkbelasting niveau, kunt u Hallo planner uitvoeren. Voordat u begint:

* Informatie verzamelen over uw replicatieomgeving, waaronder informatie over de virtuele machines, het aantal schijven per virtuele machine en de opslag per schijf.
* Schatting Hallo dagelijkse (verloop) wijzigingssnelheid hebt u voor gerepliceerde gegevens. U kunt Hallo [Capaciteitsplanner voor Hyper-V Replica](https://www.microsoft.com/download/details.aspx?id=39057) toohelp u dit doen.

1. Klik op **downloaden**, toodownload hulpprogramma Hallo en vervolgens uit te voeren. [Hallo-artikel lezen](site-recovery-capacity-planner.md) die wordt meegestuurd met Hallo-hulpprogramma.
2. Wanneer u bent klaar, selecteert u **Ja** in **hebben uitgevoerd Hallo Capacity Planner**?

   ![Capaciteitsplanning](./media/site-recovery-vmm-to-azure/gs-capacity-planning.png)

   Meer informatie over [netwerkbandbreedte beheren](#network-bandwidth-considerations)




## <a name="enable-replication"></a>Replicatie inschakelen

Voordat u begint, zorg ervoor dat uw Azure gebruikersaccount Hallo vereist [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicatie van een nieuwe virtuele machine tooAzure.

Schakel nu als volgt replicatie in:

1. Klik op **Stap 2: toepassing repliceren** > **Bron**. Nadat u replicatie voor Hallo eerst hebt ingeschakeld, klikt u op **+ repliceren** in Hallo kluis tooenable replicatie voor aanvullende machines.

    ![Replicatie inschakelen](./media/site-recovery-vmm-to-azure/enable-replication1.png)
2. In Hallo **bron** blade, selecteer Hallo VMM-server en Hallo cloud in welke Hallo Hyper-V-hosts zich bevinden. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/site-recovery-vmm-to-azure/enable-replication-source.png)
3. In **doel**, selecteert u Hallo-abonnement na een failover-implementatiemodel, en Hallo storage-account wordt gebruikt voor gerepliceerde gegevens.

    ![Replicatie inschakelen](./media/site-recovery-vmm-to-azure/enable-replication-target.png)
4. Selecteer Hallo gewenste toouse storage-account. Als u wilt dat toouse een ander opslagaccount dan die u hebt, kunt u [maken van een](#set-up-an-azure-storage-account). Als u een premium storage-account voor gerepliceerde gegevens gebruikt, moet u tooselect een extra standard-opslag account toostore replicatielogboeken die de doorlopende wijzigingen tooon-premises data.toocreate een opslagaccount met behulp van de Resource Manager-model Hallo vastleggen Klik op **nieuw**. Als u een opslagaccount met behulp van het klassieke model Hallo toocreate wilt, dat doen [in hello Azure-portal](../storage/common/storage-create-storage-account.md). Klik vervolgens op **OK**.
5. Selecteer hello Azure-netwerk en subnet toowhich Azure Virtual machines wordt verbinding gemaakt, wanneer ze zijn gemaakt na een failover. Selecteer **nu configureren voor geselecteerde machines**, tooapply Hallo instelling tooall machines in het netwerk u selecteert voor beveiliging. Selecteer **later configureren**, tooselect hello Azure-netwerk per computer. Als u wilt dat toouse een ander netwerk van de referenties die u hebt, kunt u [maken van een](#set-up-an-azure-network). een netwerk met toocreate Hallo klikt u op Resource Manager-model **nieuw**. Als u een netwerk met het klassieke model Hallo toocreate wilt, dat doen [in hello Azure-portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Selecteer indien van toepassing een subnet. Klik vervolgens op **OK**.
6. In **virtuele Machines** > **virtuele machines selecteren**en klik op elke machine die u wilt dat tooreplicate selecteren. U kunt alleen machines selecteren waarvoor replicatie kan worden ingeschakeld. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/site-recovery-vmm-to-azure/enable-replication5.png)

7. In **eigenschappen** > **eigenschappen configureren**Hallo-besturingssysteem voor virtuele machines Hallo geselecteerd en selecteer Hallo besturingssysteemschijf.

    - Controleer of deze Hallo Azure VM-naam (doelnaam) voldoet aan [vereisten van de virtuele machine van Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).   
    - Standaard worden alle Hallo schijven Hallo VM geselecteerd voor replicatie, maar u kunt schijven tooexclude wissen ze.

        - U kunt tooexclude schijven tooreduce replicatie bandbreedte. Bijvoorbeeld, wilt u mogelijk niet tooreplicate schijven met tijdelijke gegevens of gegevens die is vernieuwd telkens wanneer een computer of apps (zoals pagefile.sys of Microsoft SQL Server tempdb) opnieuw wordt opgestart. U kunt Hallo schijf uitsluiten van replicatie door geïnstalleerd Hallo-schijf.
        - Alleen standaardschijven kunnen worden uitgesloten. U kunt geen besturingssysteemschijven uitsluiten.
        - We raden u aan geen dynamische schijven uit te sluiten. Met Site Recovery kan niet worden vastgesteld of een virtuele harde schijf in een gast-VM een basisschijf of een dynamische schijf is. Als u alle schijven van de afhankelijke dynamisch volume niet worden uitgesloten, worden Hallo beveiligde dynamische schijf wordt weergegeven als een niet-werkende schijf wanneer hello VM failover wordt uitgevoerd en Hallo gegevens op de schijf niet toegankelijk.
        - Nadat de replicatie is ingeschakeld, kunt u geen schijven meer toevoegen of verwijderen voor replicatie. Als u wilt dat tooadd of uitsluiten van een schijf, moet u toodisable beveiliging voor Hallo VM nodig en vervolgens opnieuw inschakelen.
        - Voor schijven die u handmatig hebt gemaakt in Azure, wordt geen failback uitgevoerd. Als u meer dan drie schijven mislukken en twee rechtstreeks in Azure VM maken, wordt bijvoorbeeld alleen Hallo drie schijven die zijn failover mislukt door Azure tooHyper-V. U kunt geen schijven die handmatig zijn gemaakt in de failback of in de omgekeerde replicatie van Hyper-V tooAzure opnemen.
        - Als u een schijf die nodig is voor een toepassing toooperate uitsluit, na failover tooAzure moet u toocreate handmatig in Azure, zodat die Hallo gerepliceerd toepassing uit te voeren. U kunt ook kan u integreren met Azure automation een herstelplan, toocreate Hallo schijf tijdens de failover van Hallo-machine.

    Klik op **OK** toosave wijzigingen. Later kunt u eventueel extra eigenschappen instellen.

    ![Replicatie inschakelen](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

8. In **replicatie-instellingen** > **replicatie-instellingen configureren**, Hallo replicatiebeleid u tooapply voor Hallo virtuele machines beveiligde wilt selecteren. Klik vervolgens op **OK**. U kunt het replicatiebeleid Hallo in wijzigen **replicatiebeleid** > beleidsnaam > **instellingen bewerken**. De wijzigingen die u toepast, worden zowel gebruikt voor machines die al worden gerepliceerd, als voor nieuwe machines.

   ![Replicatie inschakelen](./media/site-recovery-vmm-to-azure/enable-replication7.png)

U kunt de voortgang van Hallo volgen **beveiliging inschakelen** taak **taken** > **Site Recovery-taken**. Na het Hallo **beveiliging voltooien** taak wordt uitgevoerd, Hallo machine is gereed voor failover.

### <a name="view-and-manage-vm-properties"></a>Eigenschappen van virtuele machines weergeven en beheren

Het is raadzaam om de eigenschappen van de bronmachine Hallo Hallo te controleren. Houd er rekening mee dat hello Azure VM-naam moet voldoen aan [vereisten van de virtuele machine van Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. In **beveiligde Items**, klikt u op **gerepliceerde Items**, en selecteer Hallo machine toosee de details ervan.

    ![Replicatie inschakelen](./media/site-recovery-vmm-to-azure/vm-essentials.png)
2. In **eigenschappen**, vindt u replicatie en failover-informatie voor Hallo VM.

    ![Replicatie inschakelen](./media/site-recovery-vmm-to-azure/test-failover2.png)
3. In **berekening en netwerk** > **eigenschappen berekenen**, kunt u de naam en doel van de grootte van virtuele machine van Azure Hallo opgeven. Hallo naam toocomply met wijzigen [Azure-vereisten](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) als u wilt. U kunt ook bekijken en wijzigen van de informatie over het doelnetwerk hello, subnet en Hallo IP-adres dat toegewezen toohello Azure VM.
Opmerking:

   * U kunt IP-adres van Hallo doel instellen. Als u een adres niet opgeeft, wordt Hallo failover machine DHCP gebruikt. Als u een adres dat is niet beschikbaar bij een failover instelt, mislukt Hallo failover. Hallo hetzelfde IP-adres van doel kan worden gebruikt voor een testfailover als Hallo adres in het testfailovernetwerk Hallo beschikbaar is.
   * Hallo aantal netwerkadapters wordt bepaald door Hallo-grootte die u voor Hallo doel-virtuele machine, als volgt opgeeft:

     * Als het aantal netwerkadapters op de bronmachine Hallo Hallo kleiner dan of gelijk aantal adapters toohello toegestaan voor de doelgrootte machine Hallo vervolgens Hallo doel hetzelfde aantal adapters als bron Hallo Hallo.
     * Als het aantal adapters voor de virtuele bronmachine Hallo Hallo overschrijdt Hallo getal is toegestaan voor de doelgrootte Hallo vervolgens maximaal Hallo doel wordt gebruikt.
     * Bijvoorbeeld als een bronmachine twee netwerkadapters heeft en de grootte van Hallo doelmachine vier ondersteunt, Hallo doelmachine twee adapters hebben. Als Hallo-bronmachine twee adapters heeft, maar hello ondersteunde doelgrootte slechts één ondersteunt, hebben Hallo doelmachine slechts één adapter.     
     * Als Hallo VM meerdere netwerkadapters heeft, worden deze allemaal verbonden toohello hetzelfde netwerk.

     ![Replicatie inschakelen](./media/site-recovery-vmm-to-azure/test-failover4.png)

4. In **schijven** ziet u Hallo-besturingssysteem en gegevensschijven op Hallo VM die wordt gerepliceerd.

#### <a name="managed-disks"></a>Managed Disks

In **berekening en netwerk** > **eigenschappen berekenen**, u kunt instellen "Beheerde schijven gebruiken" te 'Ja' voor Hallo VM als u tooattach beheerde schijven tooyour machine op migratie tooAzure wilt. Beheerde schijven vereenvoudigt Schijfbeheer voor Azure IaaS VM's met Hallo storage-accounts die zijn gekoppeld aan het VM-schijven Hallo beheren. [Meer informatie over beheerde schijven](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - Beheerde schijven zijn gemaakt en gekoppelde toohello virtuele machine alleen op een failover-tooAzure. Over het inschakelen van beveiliging, blijven gegevens uit de lokale machines tooreplicate toostorage accounts.
   Beheerde schijven kunnen alleen voor virtuele machines die zijn geïmplementeerd met behulp van Hallo Resource manager-implementatiemodel worden gemaakt.  

  > [!NOTE]
  > Failback vanuit Azure tooon lokale Hyper-V-omgeving is momenteel niet ondersteund voor computers met beheerde-schijven. "Beheerde schijven gebruiken" te 'Ja' alleen ingesteld als u van plan toomigrate deze machine in Azure bent.

   - Als u "Beheerde schijven gebruiken" te 'Ja', is alleen beschikbaarheidssets in de resourcegroep Hallo met "Beheerde schijven gebruiken" set te 'Ja' beschikbaar voor selectie. Dit is omdat de virtuele machines met beheerde schijven kan alleen deel uitmaken van beschikbaarheidssets met 'Gebruik beheerd schijven' eigenschappenset te 'Ja'. Zorg ervoor dat u beschikbaarheidssets met 'Gebruik beheerd schijven' eigenschap is ingesteld op basis van uw schijven opzet toouse beheerd op failover maken.  Op dezelfde manier als u "Beheerde schijven gebruiken" te 'Nee', is alleen in beschikbaarheidssets voor de resourcegroep Hallo met "Beheerde schijven gebruiken" eigenschappenset te 'Nee' beschikbaar voor selectie. [Meer informatie over beheerde schijven en beschikbaarheidssets](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Als het Hallo-opslagaccount gebruikt voor replicatie is versleuteld met versleuteling van de opslagruimte op elk gewenst moment in de tijd, mislukt het maken van beheerde schijven tijdens failover. U kunt instellen "Beheerde schijven gebruiken" te 'Nee' en probeer de failover of schakel de beveiliging voor Hallo virtuele machine en Beveilig de tooa storage-account die geen versleuteling van de opslagruimte-service is ingeschakeld op elk punt in tijd.
  > [Meer informatie over Versleuteling voor opslagservice en beheerde schijven](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-hello-deployment"></a>Hallo-implementatie testen

tootest hello implementatie kunt u een testfailover voor één virtuele machine of een herstelplan dat een of meer virtuele machines bevat uitvoeren.

### <a name="before-you-start"></a>Voordat u begint

 - Als u wilt dat tooconnect tooAzure virtuele machines met RDP na een failover meer informatie over [tooconnect voorbereiden](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - toofully test u toocopy van Active Directory en DNS moet in uw testomgeving. [Meer informatie](site-recovery-active-directory.md#test-failover-considerations).

### <a name="run-a-test-failover"></a>Een testfailover uitvoeren

1. toofail via één VM in **gerepliceerde Items**, klikt u op Hallo VM > **+ Testfailover**.
2. plan toofail via een herstelbewerking **herstelplannen**, klik met de rechtermuisknop Hallo plan > **Testfailover**. een herstelplan toocreate [Volg deze instructies](site-recovery-create-recovery-plans.md).
3. In **Testfailover**, selecteer hello Azure-netwerk toowhich virtuele Azure-machines verbinding maken wanneer failover plaatsvindt.
4. Klik op **OK** toobegin Hallo failover. U kunt de voortgang volgen door te klikken op Hallo VM tooopen eigenschappen of op Hallo **Testfailover** taak **Site Recovery-taken**.
5. Nadat de failover Hallo is voltooid, dient u zich kunt toosee Hallo replica machine van Azure in hello Azure-portal weergegeven > **virtuele Machines**. U moet ervoor zorgen dat Hallo VM is Hallo juiste grootte heeft, dat het juiste toohello-netwerk is verbonden en wordt uitgevoerd.
6. Als u voorbereid op verbindingen na een failover, moet u kunnen tooconnect toohello Azure VM.
7. Wanneer u bent klaar, klikt u op op **testfailover opschonen** op Hallo herstelplan. In **notities** opnemen en eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo opslaan. Hiermee verwijdert u Hallo virtuele machines die zijn gemaakt tijdens de testfailover.

Voor meer informatie lezen Hallo [Test failover tooAzure](site-recovery-test-failover-to-azure.md) artikel.

## <a name="monitor-hello-deployment"></a>Monitor Hallo-implementatie

Hier ziet u hoe u configuratie-instellingen, en de status voor de implementatie van Site Recovery Hallo kunt bewaken:

1. Klik op Hallo kluis naam tooaccess hello **Essentials** dashboard. Op dit dashboard ziet u een overzicht van de Site Recovery-taken, de replicatiestatus, de herstelplannen, de serverstatus en de gebeurtenissen.  U kunt aanpassen **Essentials** tooshow Hallo tegels en indelingen die vooral handig tooyou, inclusief Hallo status van de andere Site Recovery en Backup-kluizen zijn.

    ![Essentials](./media/site-recovery-vmm-to-azure/essentials.png)
2. In **Health**, kunt u problemen met de voor lokale servers (servers VMM- of configuratieservers) bewaken en Hallo gebeurtenissen die worden gegenereerd door Site Recovery in Hallo afgelopen 24 uur.
3. In Hallo **gerepliceerde Items**, **herstelplannen**, en **Site Recovery-taken** tegels die u kunt beheren en controleren van replicatie. U kunt inzoomen op taken via **Taken** > **Site Recovery-taken**.

## <a name="command-line-installation-for-hello-azure-site-recovery-provider"></a>Installatie vanaf de opdrachtregel voor hello Azure Site Recovery Provider

Hello Azure Site Recovery Provider kan worden geïnstalleerd vanaf de opdrachtregel Hallo. Deze methode kan gebruikte tooinstall Hallo-Provider op Server Core voor Windows Server 2012 R2 zijn.

1. Hallo-Provider en de registratiesleutel sleutel tooa installatiemap downloaden. Bijvoorbeeld: C:\ASR.
2. Voer deze opdrachten tooextract Hallo Provider-installatieprogramma vanaf een opdrachtprompt met verhoogde bevoegdheid:

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Voer deze opdracht tooinstall Hallo-onderdelen:

            C:\ASR> setupdr.exe /i
4. Voer vervolgens deze opdrachten, tooregister Hallo server in de kluis Hallo:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>       

Waar:

* **/ Credentials**: verplichte parameter waarmee wordt aangegeven waar Hallo registratiesleutelbestand zich bevindt.  
* **/ FriendlyName**: verplichte parameter voor de naam Hallo van Hallo Hyper-V-hostserver die wordt weergegeven in hello Azure Site Recovery-portal.
* * **/ EncryptionEnabled**: een optionele parameter wanneer u Hyper-V-machines in VMM repliceert tooAzure clouds. Geef desgewenst tooencrypt virtuele machines in Azure (versleuteling bij rust). Zorg ervoor dat Hallo naam van het Hallo-bestand heeft een **.pfx** extensie. Versleuteling is standaard uitgeschakeld.

    > [!NOTE]
    > Het verdient aanbeveling toouse Hallo mogelijkheid van stationsversleuteling geleverd door Azure voor het versleutelen van gegevens in rust in plaats van Hallo-versleutelingsoptie (EncryptionEnabled optie) opgegeven door Azure Site Recovery. mogelijkheid van stationsversleuteling Hallo verstrekt door Azure kan worden ingeschakeld voor een opslagaccount en helpt bij het bereiken van betere prestaties zoals Hallo ontsleutelen door Azure wordt uitgevoerd  
    > Storage.
    > [Meer informatie over de Storage-versleutelingsservice in Azure](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption).
    
* **/ proxyaddress**: een optionele parameter waarmee het adres van de proxyserver Hallo Hallo.
* **/ proxyport**: optionele parameter waarmee het Hallo-poort van de proxyserver Hallo.
* **proxyusername**: optionele parameter waarmee de proxygebruikersnaam hello (als de proxyserver verificatie is vereist).
* **/ proxypassword**: optionele parameter waarmee Hallo wachtwoord tooauthenticate met de proxyserver (als Hallo proxy verificatie is vereist).


### <a name="network-bandwidth-considerations"></a>Overwegingen voor netwerkbandbreedte
U kunt Hallo capaciteit planner hulpprogramma toocalculate Hallo bandbreedte die u nodig hebt voor replicatie (initiële replicatie en deltareplicaties) gebruiken. toocontrol hello hoeveelheid bandbreedte voor replicatie wordt gebruikt, hebt u een aantal opties:

* **Bandbreedte beperken**: Hyper-V-verkeer dat wordt gerepliceerd van de secundaire site tooa verloopt via een specifieke Hyper-V-host. U kunt de bandbreedte op Hallo hostserver beperken.
* **Bandbreedte aanpassen**: U kunt zelf bepalen hoeveel Hallo-bandbreedte die wordt gebruikt voor replicatie via diverse registersleutels.

#### <a name="throttle-bandwidth"></a>Bandbreedte beperken
1. Hallo Microsoft Azure Backup MMC-module openen op Hallo Hyper-V-hostserver. Een snelkoppeling naar Microsoft Azure Backup is standaard beschikbaar zijn op Hallo bureaublad of in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Klik in het Hallo-module op **eigenschappen wijzigen**.
3. Op Hallo **bandbreedtebeperking** tabblad **inschakelen voor gebruik van internetbandbreedte voor back-upbewerkingen**, en Hallo limieten instellen voor werk en niet-werk uren. Geldige bereiken zijn afkomstig van 512 Kbps too102 Mbps per seconde.

    ![Bandbreedte beperken](./media/site-recovery-vmm-to-azure/throttle2.png)

U kunt ook Hallo [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset beperking. Hier volgt een voorbeeld:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** geeft aan dat er geen beperking is vereist.

#### <a name="influence-network-bandwidth"></a>Netwerkbandbreedte beïnvloeden
Hallo **UploadThreadsPerVM** register waarde bepaalt Hallo aantal threads die worden gebruikt voor gegevensoverdracht (initiële replicatie of deltareplicatie) van een schijf. Een hogere waarde verhoogt Hallo netwerkbandbreedte gebruikt voor replicatie. Hallo **DownloadThreadsPerVM** registerwaarde geeft u het aantal threads die worden gebruikt voor gegevensoverdracht tijdens failback Hallo.

1. Hallo-register, navigeert u in te**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.

   * De waarde van de Hallo wijzigen **UploadThreadsPerVM** (of Hallo sleutel maken als deze niet bestaat) toocontrol threads gebruikt voor schijfreplicatie.
   * De waarde van de Hallo wijzigen **DownloadThreadsPerVM** (of Hallo sleutel maken als deze niet bestaat) toocontrol threads voor failbackverkeer vanuit Azure gebruikt.
2. Hallo-standaardwaarde is 4. In een netwerk 'overprovisioning', moeten deze registersleutels van Hallo standaardwaarden worden gewijzigd. Hallo maximum is 32. Verkeer toooptimize Hallo waarde bewaken.

## <a name="next-steps"></a>Volgende stappen

Nadat de initiële replicatie is voltooid en u Hallo-implementatie hebt getest, kunt u failovers kunt aanroepen, zoals Hallo noodzaak zich voordoet. [Meer informatie](site-recovery-failover.md) over verschillende soorten failovers en hoe toorun ze.
