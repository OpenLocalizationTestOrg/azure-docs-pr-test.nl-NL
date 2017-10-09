---
title: aaaReplicate Hyper-V-machines tooa secundaire site met Azure Site Recovery | Microsoft Docs
description: Hierin wordt beschreven hoe tooreplicate Hyper-V-machines in VMM clouds tooa secundaire VMM site met behulp van hello Azure-portal.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: b33a1922-aed6-4916-9209-0e257620fded
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: e79dbdeab74266e843e5146298dc5aadfe66b5df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-hello-azure-portal"></a>Hyper-V virtuele machines in VMM-clouds tooa secundaire VMM-site met behulp van Azure-portal Hallo repliceren
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-vmm.md)
> * [Klassieke portal](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Dit artikel wordt beschreven hoe tooreplicate lokale Hyper-V virtuele machines die worden beheerd in System Center Virtual Machine Manager (VMM)-clouds, secundaire site met behulp van tooa [Azure Site Recovery](site-recovery-overview.md) in hello Azure-portal. Meer informatie over deze [scenarioarchitectuur](site-recovery-components.md).

Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Vereisten

**Vereiste** | **Details**
--- | ---
**Azure** | U hebt een [Microsoft Azure](http://azure.microsoft.com/)-account nodig. U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/). [Meer informatie](https://azure.microsoft.com/pricing/details/site-recovery/) over prijzen voor Site Recovery.
**On-premises VMM** | U hebt twee VMM-servers, één in Hallo primaire site en één in Hallo secundaire wordt aangeraden.<br/><br/> U kunt repliceren tussen clouds op één VMM-server.<br/><br/> VMM-servers waarop ten minste System Center 2012 SP1 met de nieuwste updates Hallo.<br/><br/> VMM-servers moeten toegang tot internet.
**VMM-clouds** | Elke VMM-server moet op een of meer clouds, en alle clouds Hallo Hyper-V Capaciteitsprofiel ingesteld moeten hebben. <br/><br/>Clouds moeten een of meer VMM-hostgroepen bevatten.<br/><br/> Als u slechts één VMM-server hebt, moet deze ten minste twee clouds, tooact als primaire en secundaire.
**Hyper-V** | Hyper-V-servers moeten ten minste draaien op Windows Server 2012 met Hallo Hyper-V-rol en hebben Hallo nieuwste updates zijn geïnstalleerd.<br/><br/> Een Hyper-V-server moet een of meer virtuele machines bevatten.<br/><br/>  Hyper-V-hostservers moeten zich in hostgroepen in Hallo primaire en secundaire VMM-clouds.<br/><br/> Als u op Windows Server 2012 R2 Hyper-V in een cluster uitvoert, installeert u [2961977 bijwerken](https://support.microsoft.com/kb/2961977)<br/><br/> Als u op Windows Server 2012 Hyper-V in een cluster uitvoert, wordt niet clusterbroker automatisch als u een statisch IP-adressen gebaseerde cluster hebt gemaakt. Hallo clusterbroker handmatig configureren. [Lees meer](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> Hyper-V-servers moeten toegang tot internet.
**URL 's** | VMM-servers en Hyper-V-hosts moeten kunnen tooreach deze URL's:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]

## <a name="deployment-steps"></a>Implementatiestappen

Dit is wat u doen:

1. Controleer of vereisten.
2. Bereid Hallo VMM-server en Hyper-V-hosts.
3. Maak een Recovery Services-kluis. Hallo-kluis bevat configuratie-instellingen en stuurt replicatie.
4. Bron, doel en replicatie-instellingen opgeven.
5. Hallo Mobility-service op de virtuele machines implementeert u tooreplicate.
6. Voorbereiden voor replicatie en replicatie inschakelen voor Hyper-V-machines.
7. Een test failover toomake, controleren of dat alles werkt zoals verwacht worden uitgevoerd.

## <a name="prepare-vmm-servers-and-hyper-v-hosts"></a>VMM-servers en Hyper-V-hosts voorbereiden

tooprepare voor implementatie:

1. Zorg ervoor dat Hallo VMM-server en Hyper-V-hosts voldoen aan de hierboven beschreven Hallo-vereisten en Hallo vereist URL's kunnen bereiken.
2. Instellen van VMM-netwerken, zodat u kunt configureren [netwerktoewijzing](#network-mapping-overview).

    - Zorg ervoor dat virtuele machines op Hallo bron Hyper-V-hostserver verbonden tooa VMM VM-netwerk. Dit netwerk moet gekoppelde tooa logisch netwerk dat is gekoppeld aan Hallo cloud.
    Controleer of Hallo secundaire cloud die u voor herstel gebruikt heeft een bijbehorende VM-netwerk is geconfigureerd. Deze VM-netwerk moet gekoppelde tooa logisch netwerk dat is gekoppeld aan Hallo secundaire cloud.

3. Voorbereiden voor een [single server-implementatie](#single-vmm-server-deployment), als u tooreplicate virtuele machines tussen clouds op Hallo wilt dezelfde VMM-server.

## <a name="create-a-recovery-services-vault"></a>Een Recovery Services-kluis maken
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op **Nieuw** > **Beheer** > **Recovery Services**.
3. In **naam**, Geef een beschrijvende naam tooidentify Hallo-kluis. Als u meer dan één abonnement hebt, selecteert u een van uw abonnementen.
4. [Maak een resourcegroep](../azure-resource-manager/resource-group-template-deploy-portal.md) of selecteer een bestaande resourcegroep. Geef een Azure-regio op. Machines zijn gerepliceerde toothis regio. toocheck ondersteunde regio's Zie geografische beschikbaarheid in [prijsinformatie voor Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Als u wilt dat tooquickly toegang Hallo kluis van Hallo Dashboard, klikt u op **pincode toodashboard** > **kluis maken**.

    ![Nieuwe kluis](./media/site-recovery-vmm-to-vmm/new-vault-settings.png)

Hallo nieuwe kluis wordt weergegeven op Hallo **Dashboard**in **alle resources**, en op Hallo belangrijkste **Recovery Services-kluizen** blade.


## <a name="choose-a-protection-goal"></a>Kies een beveiligingsdoel

Selecteer wat u wilt dat tooreplicate en waar u tooreplicate aan.

2. Klik op **siteherstel** > **stap 1: infrastructuur voorbereiden** > **beveiligingsdoel**.
3. Selecteer **toorecovery site**, en selecteer **Ja, met Hyper-V**.
4. Selecteer **Ja** tooindicate u VMM toomanage Hallo Hyper-V-hosts.
5. Selecteer **Ja** hebt u een secundaire VMM-server. Als u replicatie tussen clouds op één VMM-server implementeert, klikt u op **Nee**. Klik vervolgens op **OK**.

    ![Doelstellingen kiezen](./media/site-recovery-vmm-to-vmm/choose-goals.png)

## <a name="set-up-hello-source-environment"></a>Hallo bronomgeving instellen

Hello Azure Site Recovery Provider installeren op VMM-servers en detecteren en beheerservers in Hallo kluis registreren.

1. Klik op **stap 1: infrastructuur voorbereiden** > **bron**.

    ![Bron instellen](./media/site-recovery-vmm-to-vmm/goals-source.png)
2. In **bron voorbereiden**, klikt u op **+ VMM** tooadd een VMM-server.

    ![Bron instellen](./media/site-recovery-vmm-to-vmm/set-source1.png)
3. In **Server toevoegen**, controleert u of **System Center VMM-server** wordt weergegeven in **servertype** en die Hallo VMM-server voldoet aan Hallo [vereisten](#prerequisites).
4. Download hello Azure Site Recovery Provider-installatiebestand.
5. Download de registratiesleutel Hallo. U hebt deze nodig wanneer u de installatie uitvoert. Hallo-sleutel is vijf dagen na het genereren ervan geldig.

    ![Bron instellen](./media/site-recovery-vmm-to-vmm/set-source3.png)
6. Hello Azure Site Recovery Provider installeren op Hallo VMM-server. U hoeft niet tooexplicitly niets mee geïnstalleerd op Hyper-V-hostservers.


### <a name="install-hello-azure-site-recovery-provider"></a>Hello Azure Site Recovery Provider installeren

1. Hallo Provider setup-bestand op elke VMM-server wordt uitgevoerd. Als VMM is geïmplementeerd in een cluster, voert u Hallo Hallo na eerste keer dat u installeert:
    -  Hallo-provider installeren op een actief knooppunt en Hallo installatie tooregister Hallo VMM-server in de kluis Hallo voltooien.
    - Vervolgens installeert u Hallo Provider op Hallo andere knooppunten. Clusterknooppunten moeten alle Hallo uitgevoerd dezelfde versie van Provider Hallo.
2. Setup enkele vereiste controles uitgevoerd en vraagt toestemming toostop Hallo VMM-service. Hallo VMM-service wordt opnieuw opgestart nadat setup is voltooid. Als u op een VMM-cluster installeert, bent u na vragen aan gebruiker toostop Hallo Cluster-rol.
3. In **Microsoft Update**, kunt u ervoor kiezen in toospecify dat de provider-updates zijn geïnstalleerd in overeenstemming met uw Microsoft Update-beleid.
4. In **installatie**, accepteer of wijzig Hallo standaardlocatie voor installatie, en klikt u op **installeren**.

    ![Installatielocatie](./media/site-recovery-vmm-to-vmm/provider-location.png)
5. Nadat de installatie is voltooid, klikt u op **registreren** tooregister Hallo-server in Hallo kluis.

    ![Installatielocatie](./media/site-recovery-vmm-to-vmm/provider-register.png)
6. In **kluisnaam**, Controleer de naam van de Hallo van Hallo kluis in welke Hallo server wordt geregistreerd. Klik op *Volgende*.

    ![Serverregistratie](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
7. In **internetverbinding**, opgeven hoe Hallo-provider die wordt uitgevoerd op de VMM-server Hallo tooAzure verbindt.

    ![Instellingen voor internet](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   - U kunt opgeven die Hallo-provider moet rechtstreeks verbinding gemaakt toohello internet, of via een proxyserver.
   - Proxy-instellingen opgeven, indien nodig.
   - Als u een proxy gebruikt, een VMM RunAs-account (DRAProxyAccount) wordt automatisch gemaakt met Hallo opgegeven proxyreferenties. Hallo-proxyserver zodanig configureren dat dit account kan worden geverifieerd. Hallo RunAs-Accountinstellingen kunnen worden gewijzigd in de VMM-console Hallo > **instellingen** > **beveiliging** > **Run As-Accounts**. Hallo VMM servicewijzigingen tooupdate opnieuw opstarten
8. In **registratiesleutel**, selecteer Hallo sleutel gedownload uit Azure Site Recovery uit te voeren en toohello VMM-server gekopieerd.
9. Hallo-instelling voor wachtwoordversleuteling wordt alleen gebruikt wanneer u Hyper-V-machines in VMM-clouds tooAzure repliceert. Als u tooa secundaire site repliceert wordt het niet gebruikt.
10. In **servernaam**, Geef een beschrijvende naam tooidentify Hallo VMM-server in Hallo kluis. Geef in een clusterconfiguratie Hallo VMM-clusterrolnaam op.
11. In **cloudmetagegevens synchroniseren**Selecteer of u voor alle clouds op de VMM-server met de kluis Hallo Hallo toosynchronize metagegevens wilt instellen. Deze actie hoeft alleen toohappen eenmaal op elke server. Als u niet toosynchronize alle clouds wilt, kunt u laat u deze instelling uitgeschakeld en synchroniseert u elke cloud afzonderlijk in de eigenschappen van de cloud Hallo in Hallo VMM-console.
12. Klik op **volgende** toocomplete Hallo proces. Na registratie worden metagegevens van Hallo VMM-server opgehaald door Azure Site Recovery. Hallo-server wordt weergegeven op Hallo **VMM-Servers** tabblad op Hallo **Servers** pagina in Hallo kluis.

    ![Server](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)
13. Nadat het Hallo-server is beschikbaar in Hallo Site Recovery-console, in **bron** > **bron voorbereiden** Selecteer Hallo VMM-server en selecteer Hallo cloud welke Hallo Hyper-V host bevindt. Klik vervolgens op **OK**.

U kunt ook Hallo-provider installeren vanaf de opdrachtregel Hallo:

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Hallo doelomgeving instellen

Selecteer Hallo doel-VMM-server en de cloud.

1. Klik op **infrastructuur voorbereiden** > **doel**, en selecteer Hallo doel VMM-server die u wilt dat toouse.
2. Clouds op Hallo-server die zijn gesynchroniseerd met Site Recovery wordt weergegeven. Selecteer de doelcloud Hallo.

   ![doel](./media/site-recovery-vmm-to-vmm/target-vmm.png)

## <a name="set-up-replication-settings"></a>Replicatie-instellingen instellen

- Wanneer u een beleid voor wachtwoordreplicatie maakt, moet alle host met behulp van beleid Hallo hetzelfde besturingssysteem hebt Hallo. Hallo VMM-cloud Hyper-V-hosts met verschillende versies van Windows Server kan bevatten, maar in dit geval moet u meerdere beleidsregels voor replicatie.
- U kunt Hallo offline initiële replicatie uitvoeren. [Meer informatie](#prepare-for-initial-offline-replication)

1. een nieuw beleid voor wachtwoordreplicatie toocreate klikt u op **infrastructuur voorbereiden** > **replicatie-instellingen** > **+ maken en koppelen**.

    ![Netwerk](./media/site-recovery-vmm-to-vmm/gs-replication.png)
2. Geef in **Beleid maken en koppelen** een beleidsnaam op. Hallo bron en doel-type moet **Hyper-V**.
3. In **versie van Hyper-V-host**, selecteer welk besturingssysteem wordt uitgevoerd op Hallo host.
4. In **verificatietype** en **verificatiepoort**, opgeven hoe verkeer wordt geverifieerd tussen primaire Hallo en herstel Hyper-V-hostservers. Selecteer **certificaat** tenzij u beschikken over een werkende Kerberos-omgeving. Azure Site Recovery configureert automatisch certificaten voor HTTPS-verificatie. U hoeft niet toodo iets handmatig. Standaard wordt poort 8083 en 8084 (voor certificaten) in Hallo Windows Firewall op Hallo Hyper-V-hostservers worden geopend. Als u selecteert **Kerberos**, een Kerberos-ticket wordt gebruikt voor wederzijdse verificatie van Hallo host-servers. Houd er rekening mee dat deze instelling is alleen relevant voor Hyper-V-host-servers waarop Windows Server 2012 R2.
5. In **Kopieerfrequentie**, geef aan hoe vaak u tooreplicate deltagegevens na de initiële replicatie van hello (elke 30 seconden, 5 of 15 minuten).
6. In **herstel bewaarperiode**, in uren opgeven hoe lang de retentieperiode Hallo wordt worden voor elk herstelpunt. Beveiligde machines kunnen worden hersteld tooany punt in een venster.
7. In **App-consistente momentopname frequentie**, opgeven hoe vaak (1-12 uur) herstelpunten met toepassingsconsistente momentopnamen worden gemaakt. Hyper-V gebruikt twee soorten momentopnamen: standaardmomentopnamen waarmee een incrementele momentopname van Hallo volledige virtuele machine en een toepassingsconsistente momentopnamen waarmee een momentopname van een punt in tijd van de toepassingsgegevens Hallo in Hallo virtuele machine. Toepassingsconsistente momentopnamen gebruiken Volume Shadow Copy Service (VSS) tooensure die toepassingen zich in een consistente status wanneer Hallo momentopname wordt gemaakt. Als u toepassingsconsistente momentopnamen inschakelt, wordt het Hallo-prestaties van toepassingen die worden uitgevoerd op virtuele bronmachines beïnvloeden. Zorg ervoor dat Hallo-waarde lager dan Hallo aantal aanvullende herstelpunten dat u configureert.
8. In **gegevensoverdracht compressie**, opgeven of de gerepliceerde gegevens die worden overgedragen moeten worden gecomprimeerd.
9. Selecteer **replica verwijderen VM**, toospecify die Hallo replica virtuele machine moet worden verwijderd als u beveiliging voor Hallo bron-VM uitschakelt. Als u deze instelling inschakelt wanneer u beveiliging voor Hallo bron-VM wordt deze verwijderd uit de Site Recovery-console Hallo uitschakelt, Site Recovery-instellingen voor Hallo VMM worden verwijderd uit de VMM-console Hallo en Hallo replica is verwijderd.
10. In **initiële replicatiemethode**, als u via netwerk hello repliceert, opgeven of toostart Hallo initiële replicatie of plannen. toosave netwerkbandbreedte, kunt u tooschedule deze buiten de drukste tijden. Klik vervolgens op **OK**.

     ![Beleid voor replicatie](./media/site-recovery-vmm-to-vmm/gs-replication2.png)
11. Wanneer u een nieuw beleid maakt is deze automatisch gekoppeld aan Hallo VMM-cloud. In **replicatiebeleid**, klikt u op **OK**. U kunt aanvullende VMM-Clouds (en Hallo virtuele machines erin) koppelen aan dit replicatiebeleid in **replicatie** > beleidsnaam > **VMM-Cloud koppelen**.

     ![Beleid voor replicatie](./media/site-recovery-vmm-to-vmm/policy-associate.png)


### <a name="configure-network-mapping"></a>Netwerktoewijzing configureren

- Meer informatie over [netwerktoewijzing](#prepare-for-network-mapping) voordat u begint.
- Controleer of de virtuele machines op de VMM-servers zijn verbonden tooa VM-netwerk.


1. In **Site Recovery-infrastructuur** > **netwerktoewijzing** > **Netwerktoewijzingen**, klikt u op **+ netwerktoewijzing**.

    ![Netwerktoewijzing](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. In **netwerktoewijzing toevoegen** tabblad, selecteert u Hallo bron en doel van de VMM-servers. Hallo VM-netwerken die zijn gekoppeld aan de VMM-servers Hallo worden opgehaald.
3. In **Bronnetwerk**, selecteer toouse uit Hallo lijst met VM-netwerken die zijn gekoppeld aan de primaire VMM-server Hallo gewenste Hallo-netwerk.
4. In **doelnetwerk**, selecteer Hallo netwerk gewenste toouse op Hallo secundaire VMM-server. Klik vervolgens op **OK**.

    ![Netwerktoewijzing](./media/site-recovery-vmm-to-vmm/network-mapping2.png)

Dit is wat er gebeurt wanneer er netwerktoewijzing wordt uitgevoerd:

* Alle bestaande gerepliceerde virtuele machines die overeenkomen met toohello bron-VM-netwerk is verbonden toohello doel VM-netwerk.
* Nieuwe virtuele machines die verbonden toohello bron-VM-netwerk zijn worden toegewezen doelnetwerk verbonden toohello na de replicatie.
* Als u een bestaande toewijzing met een nieuw netwerk wijzigt, worden gerepliceerde virtuele machines verbonden met de nieuwe instellingen Hallo.
* Als Hallo doelnetwerk meerdere subnetten heeft en een van deze subnetten Hallo heeft dezelfde naam als het subnet waarop Hallo bron virtual machine zich bevindt, wordt Hallo replica virtuele machine na een failover worden verbonden toothat Doelsubnet. Als er geen Doelsubnet met een overeenkomende naam, wordt de Hallo virtuele machine verbonden toohello eerste subnet in het Hallo-netwerk zijn.

### <a name="configure-storage-mapping"></a>Toewijzing van opslag configureren.

[Toewijzing van opslag](#prepare-for-storage-mapping) wordt niet ondersteund in Hallo nieuwe Azure-portal. Echter, kan worden ingeschakeld met Powershell. [Meer informatie](site-recovery-vmm-to-vmm-powershell-resource-manager.md#step-7-configure-storage-mapping).

## <a name="step-5-capacity-planning"></a>Stap 5: capaciteitsplanning

Nu u de basisinfrastructuur hebt ingesteld, kunt u gaan nadenken over de capaciteitsplanning en nagaan of u aanvullende resources nodig hebt.

- Downloaden en uitvoeren van Hallo [Azure Site Recovery-Capaciteitsplanner](site-recovery-capacity-planner.md), toogather informatie over uw replicatieomgeving, met inbegrip van virtuele machines, schijven per virtuele machine en opslag per schijf.
- Als u realtime replicatie-informatie hebt verzameld, kunt u Hallo NetQos beleid toocontrol replicatie bandbreedte wijzigen voor virtuele machines. Lees meer over [beperking Hyper-V Replica verkeer](http://www.thomasmaurer.ch/2013/12/throttling-hyper-v-replica-traffic/), op de blog van Thomas Maurer. Meer informatie over Hallo [cmdlet New-NetQosPolicy](https://technet.microsoft.com/library/hh967468.aspx.).

## <a name="enable-replication"></a>Replicatie inschakelen

1. Klik op **Stap 2: toepassing repliceren** > **Bron**. Nadat u replicatie voor Hallo eerst hebt ingeschakeld, u klikt u op **+ repliceren** in Hallo kluis tooenable replicatie voor aanvullende machines.

    ![Replicatie inschakelen](./media/site-recovery-vmm-to-vmm/enable-replication1.png)
2. In **bron**Hallo VMM-server en selecteer Hallo cloud in welke Hallo gewenste tooreplicate van Hyper-V-hosts zich bevinden. Klik vervolgens op **OK**.

    ![Replicatie inschakelen](./media/site-recovery-vmm-to-vmm/enable-replication2.png)
3. In **doel**, controleert u of Hallo secundaire VMM-server en de cloud.
4. In **virtuele machines**, Hallo virtuele machines die u wilt dat tooprotect uit Hallo lijst selecteren.

    ![Beveiliging van de virtuele machine inschakelen](./media/site-recovery-vmm-to-vmm/enable-replication5.png)

U kunt de voortgang van Hallo volgen **beveiliging inschakelen** actie in **taken** > **Site Recovery-taken**. Na het Hallo **beveiliging voltooien** taak is voltooid, Hallo virtuele machine is gereed voor failover.

Opmerking:

- U kunt ook beveiliging voor virtuele machines in Hallo VMM-console inschakelen. Klik op **beveiliging inschakelen** op Hallo werkbalk in de eigenschappen van de virtuele machine Hallo > **Azure Site Recovery** tabblad.
- Nadat u replicatie hebt ingeschakeld, kunt u de eigenschappen voor Hallo VM weergeven in **gerepliceerde Items**. Op Hallo **Essentials** dashboard ziet u informatie over het replicatiebeleid Hallo voor Hallo VM en de status ervan. Klik op **eigenschappen** voor meer informatie.

### <a name="onboard-existing-virtual-machines"></a>Ingebouwde bestaande virtuele machines
Als u een bestaande virtuele machines in VMM die worden gerepliceerd met Hyper-V Replica hebt, kunt u vrijgeven ze voor Azure Site Recovery replicatie als volgt:

1. Zorg dat Hallo Hyper-V-hostserver Hallo bestaande virtuele machine bevindt zich in de primaire cloud Hallo en die Hallo Hyper-V-server die als host fungeert voor Hallo replica virtuele machine bevindt zich in Hallo secundaire cloud.
2. Zorg ervoor dat een beleid voor wachtwoordreplicatie is geconfigureerd voor Hallo primaire VMM-cloud.
3. Replicatie inschakelen voor Hallo primaire virtuele machine. Azure Site Recovery en VMM ervoor te zorgen dat hello dezelfde replicatiehost en virtuele machine wordt gedetecteerd, en Azure Site Recovery opnieuw wilt gebruiken en om opnieuw replicatie met Hallo instellingen opgegeven.

## <a name="test-your-deployment"></a>Uw implementatie testen

tootest uw implementatie, die u kunt uitvoeren een [testfailover](site-recovery-test-failover-vmm-to-vmm.md) voor een enkele virtuele machine of [een herstelplan maken](site-recovery-create-recovery-plans.md) die een of meer virtuele machines bevat.



## <a name="prepare-for-offline-initial-replication"></a>Voorbereiden voor de offline initiële replicatie

U kunt doen offline replicatie voor Hallo initiële gegevens kopiëren. U kunt dit als volgt voorbereiden:

* Op de bronserver hello geeft u de padlocatie van een van welke Hallo exporteren van gegevens wordt gehouden. Volledig beheer voor machtigingen voor NTFS en deelmachtigingen toohello VMM-service op Hallo exportpad toewijzen. Op de doelserver hello geeft u een locatie waarvan Hallo gegevens importeren wordt uitgevoerd. Hallo dezelfde machtigingen voor dit pad importeren toewijzen.
* Als hello importeren of exporteren pad wordt gedeeld, Administrator, Hoofdgebruikers, Print Operators of Server Operator groepslidmaatschap voor Hallo VMM-serviceaccount op de externe computer Hallo toewijzen welke Hallo gedeeld zich bevindt.
* Als u geen Run As-accounts tooadd hosts, op Hallo importeren en exporteren van paden, lezen toewijzen en schrijfmachtigingen toohello-Run As-accounts in VMM.
* Hallo importeren en exporteren van shares niet moet zich bevinden op een computer die wordt gebruikt als een Hyper-V-hostserver, omdat de loopback-configuratie wordt niet ondersteund door Hyper-V.
* In Active Directory is op elke Hyper-V-hostserver die bevat virtuele machines die u wilt dat tooprotect, inschakelen en configureren van beperkte delegering tootrust Hallo externe computers op welke Hallo importeren en exporteren paden zich bevinden, als volgt:
  1. Open op de domeincontroller hello, **Active Directory: gebruikers en Computers**.
  2. Klik in de consolestructuur Hallo **DomainName** > **Computers**.
  3. Klik met de rechtermuisknop Hallo Hyper-V-host-servernaam > **eigenschappen**.
  4. Op Hallo **delegering** tabblad **deze computer alleen overdracht toospecified services**.
  5. Klik op **elk verificatieprotocol voor gebruiken**.
  6. Klik op **toevoegen** > **gebruikers en Computers**.
  7. Hallo-typenaam van Hallo-computer die als host fungeert voor Hallo exportpad > **OK**. Hallo-lijst met beschikbare services, Hallo CTRL-toets ingedrukt en klik op **cifs** > **OK**. Herhaal voor Hallo naam van de computer Hallo dat pad hosts Hallo importeren. Herhaal zo nodig voor extra Hyper-V-hostservers.



## <a name="prepare-for-network-mapping"></a>Voorbereiden op netwerktoewijzing
Koppelingen van Netwerktoewijzingen tussen VMM VM-netwerken op Hallo primaire en secundaire VMM-servers:

* Replica-VM optimaal op secundaire Hyper-V-hosts plaatsen na een failover.
* Verbinding met het maken van replica VMs tooappropriate VM-netwerken na een failover.

Opmerking:
- Netwerktoewijzing kunnen worden geconfigureerd tussen VM-netwerken op twee VMM-servers of op één VMM-server als de twee sites worden beheerd door dezelfde Hallo server.
- Als de toewijzing correct is geconfigureerd en replicatie is ingeschakeld, worden een virtuele machine op de primaire locatie Hallo tooa verbonden netwerk en de replica op de doellocatie Hallo worden aangesloten toegewezen tooits netwerk.
- Als netwerken hebt wanneer u een VM-netwerk van het doel bij netwerktoewijzing selecteert in VMM correct is ingesteld, wordt Hallo VMM bron clouds die Hallo bron-VM-netwerk weergegeven, samen met de Hallo beschikbare doelservers VM-netwerken op Hallo doel clouds die worden gebruikt voor beveiliging.
- Als Hallo doelnetwerk meerdere subnetten heeft en een van deze subnetten dezelfde naam als het subnet op welke Hallo virtuele bronmachine zich bevindt, Hallo vervolgens Hallo Hallo heeft worden replica virtuele machine verbonden toothat Doelsubnet na een failover. Als er geen Doelsubnet met een overeenkomende naam, wordt de Hallo virtuele machine verbonden toohello eerste subnet in het Hallo-netwerk zijn.


Hier volgt een voorbeeld tooillustrate dit mechanisme. U gaat nu een organisatie met twee locaties in New York en Chicago.

| **Locatie** | **VMM-server** | **VM-netwerken** | **Toegewezen aan** |
| --- | --- | --- | --- |
| New York |VMM-NewYork |VMNetwork1 NewYork |Toegewezen tooVMNetwork1-Chicago |
| VMNetwork2 NewYork |Niet toegewezen | | |
| Chicago |VMM-Chicago |VMNetwork1 Chicago |Toegewezen tooVMNetwork1-NewYork |
| VMNetwork2 Chicago |Niet toegewezen | | |

Met dit voorbeeld:

* Wanneer een replica virtuele machine wordt gemaakt voor elke virtuele machine die is verbonden tooVMNetwork1-NewYork, zal de tooVMNetwork1-Chicago verbonden zijn.
* Wanneer een replica virtuele machine wordt gemaakt voor VMNetwork2 NewYork of VMNetwork2 Chicago, het is niet verbonden tooany netwerk mogelijk.

Hier volgt hoe VMM-clouds in ons voorbeeldorganisatie en Hallo logische netwerken die zijn gekoppeld aan clouds Hallo zijn ingesteld.

### <a name="cloud-protection-settings"></a>Instellingen voor cloudbeveiliging
| **Beveiligde cloud** | **Beveiligen van de cloud** | **Logisch netwerk (Den Haag)** |
| --- | --- | --- |
| GoldCloud1 |GoldCloud2 | |
| SilverCloud1 |SilverCloud2 | |
| GoldCloud2 |<p>N.v.t.</p><p></p> |<p>LogicalNetwork1 NewYork</p><p>LogicalNetwork1 Chicago</p> |
| SilverCloud2 |<p>N.v.t.</p><p></p> |<p>LogicalNetwork1 NewYork</p><p>LogicalNetwork1 Chicago</p> |

### <a name="logical-and-vm-network-settings"></a>Logische schijf als VM-netwerkinstellingen
| **Locatie** | **Logisch netwerk** | **Bijbehorende VM-netwerk** |
| --- | --- | --- |
| New York |LogicalNetwork1 NewYork |VMNetwork1 NewYork |
| Chicago |LogicalNetwork1 Chicago |VMNetwork1 Chicago |
| LogicalNetwork2Chicago |VMNetwork2 Chicago | |

### <a name="target-networks"></a>Doelnetwerken
Op basis van deze instellingen wanneer u Hallo doel VM-netwerk selecteert, worden Hallo tabel Hallo-opties die beschikbaar zijn.

| **Selecteren** | **Beveiligde cloud** | **Beveiligen van de cloud** | **Doelnetwerk beschikbaar** |
| --- | --- | --- | --- |
| VMNetwork1 Chicago |SilverCloud1 |SilverCloud2 |Beschikbaar |
| GoldCloud1 |GoldCloud2 |Beschikbaar | |
| VMNetwork2 Chicago |SilverCloud1 |SilverCloud2 |Niet beschikbaar |
| GoldCloud1 |GoldCloud2 |Beschikbaar | |


### <a name="failback"></a>Failback
Wat gebeurt er in geval van failback (omgekeerde replicatie) Hallo toosee gaan we ervan uit dat VMNetwork1 NewYork is toegewezen tooVMNetwork1-Chicago, hello instellingen te volgen.

| **Virtuele machine** | **TooVM verbonden netwerk** |
| --- | --- |
| VM1 |VMNetwork1-netwerk |
| VM2 (replica van VM1) |VMNetwork1 Chicago |

Met deze instellingen gaan we bekijken wat er gebeurt in een aantal mogelijke scenario's.

| **Scenario** | **Resultaat** |
| --- | --- |
| Geen wijziging in hello netwerkgegevens van VM-2 na een failover. |VM-1 blijft verbonden toohello Bronnetwerk. |
| Netwerkeigenschappen van VM-2 worden gewijzigd na een failover en is verbroken. |VM-1 wordt verbroken. |
| Netwerkeigenschappen van VM-2 zijn gewijzigd na een failover en is verbonden tooVMNetwork2-Chicago. |Als VMNetwork2 Chicago niet is toegewezen, kunt u VM-1 wordt verbroken. |
| Netwerktoewijzing van VMNetwork1 Chicago wordt gewijzigd. |VM-1 zijn verbonden toohello netwerk nu toegewezen tooVMNetwork1-Chicago. |


## <a name="prepare-for-single-server-deployment"></a>Voorbereiden voor implementatie met één server


Als u slechts één VMM-server hebt, kunt u virtuele machines te repliceren in Hyper-V-hosts in VMM-cloud Hallo[Azure](site-recovery-vmm-to-azure.md) of tooa secundaire VMM-cloud. De eerste optie hello wordt aangeraden omdat repliceren tussen clouds niet naadloos. Als u tooreplicate tussen clouds wilt, kunt u met een enkele zelfstandige VMM-server of met één VMM-server geïmplementeerd in een Windows-cluster gespreide repliceren

### <a name="standalone-vmm-server"></a>Standalone VMM-server

In dit scenario kunt u Hallo één VMM-server implementeren als een virtuele machine in de primaire site Hallo en repliceren van deze VM tooa secundaire site met Site Recovery en Hyper-V Replica.

1. **Instellen van VMM op een Hyper-V-virtuele machine**. We raden aan dat u Hallo SQL Server-exemplaar dat door VMM gebruikt op Hallo plaatsen dezelfde virtuele machine. Dit bespaart tijd als slechts één VM toobe gemaakt heeft. Als u wilt dat toouse extern exemplaar van SQL Server en een storing optreedt, moet u toorecover dat exemplaar voordat u VMM kunt herstellen.
2. **Controleer Hallo VMM-beheerserver is ten minste twee clouds die zijn geconfigureerd**. Één cloud bevat virtuele machines u wilt tooreplicate en andere cloud Hallo als de secundaire locatie Hallo fungeert Hallo. Hallo van cloud met Hallo virtuele machines die u wilt dat tooprotect moeten voldoen aan [vereisten](#prerequisites).
3. Site Recovery ingesteld zoals beschreven in dit artikel. Maken en Hallo VMM-server geregistreerd in een kluis, instellen van een beleid voor wachtwoordreplicatie en replicatie inschakelen. namen van Hallo bron en doel-VMM wordt dezelfde Hallo. Geef op dat de initiële replicatie vindt plaats via Hallo-netwerk.
4. Wanneer u netwerktoewijzing instellen kunt u VM-netwerk voor de primaire cloud toohello VM-netwerk voor de secundaire cloud Hallo HALLO hallo toewijzen.
5. Hyper-V Replica hebt ingeschakeld op Hallo Hyper-V-host met Hallo VMM VM in Hallo Hyper-V Manager-console en replicatie inschakelen voor Hallo VM. Zorg ervoor dat u Hallo VMM virtuele machine tooclouds die zijn beveiligd door Site Recovery, tooensure dat Hyper-V Replica-instellingen worden niet door Site Recovery overschreven niet toevoegen.
6. Als u herstelplannen voor failover die u maakt Hallo dezelfde VMM-server voor de bron en doel.
7. In een volledige onderbreking failover en als volgt herstellen:

   1. Een niet-geplande failover worden uitgevoerd in Hallo Hyper-V Manager-console in Hallo secundaire site toofail via Hallo primaire VMM VM toohello secundaire site.
   2. Controleer of dat Hallo die VMM VM is en actief en in de kluis hello, worden uitgevoerd een niet-geplande failover toofail via Hallo virtuele machines van primaire toosecondary clouds. Hallo failover doorvoeren en selecteert u een alternatief herstelpunt indien nodig.
   3. Nadat hello niet-geplande failover voltooid is, zijn alle resources toegankelijk vanaf de primaire site Hallo opnieuw.
   4. Te Hallo primaire site opnieuw in Hallo Hyper-V Manager-console op de secundaire site Hallo beschikbaar is, kunt u omgekeerde replicatie voor Hallo VMM VM. Hiermee start u replicatie voor virtuele machine Hallo van secundaire tooprimary.
   5. Een geplande failover uitvoeren in Hallo Hyper-V Manager-console in Hallo secundaire site, toofail via Hallo VMM VM toohello primaire site. Hallo failover doorvoeren. Omgekeerde replicatie activeert zodat hello VMM VM wordt opnieuw gerepliceerd van primaire toosecondary.
   6. In de Recovery Services-kluis Hallo, schakelt u omgekeerde replicatie voor de Hallo werkbelasting van virtuele machines, toostart ze van secundaire tooprimary te repliceren.
   7. In Hallo Recovery Services-kluis, voer een geplande failover toofail back Hallo werkbelasting VMs toohello primaire site. Hallo failover toocomplete doorvoeren deze. Omgekeerde replicatie toostart replicerende Hallo werkbelasting van virtuele machines van primaire toosecondary activeert.

### <a name="stretched-vmm-cluster"></a>Gespreide VMM-cluster

In plaats van een zelfstandige VMM-server implementeren als een virtuele machine die wordt gerepliceerd tooa secundaire site, kunt u VMM maximaal beschikbaar maken door deze te implementeren als een virtuele machine in een Windows-failovercluster. Dit biedt veerkracht werkbelasting en bescherming tegen hardwarefouten. toodeploy met Site Recovery Hallo VMM VM moet worden geïmplementeerd in een cluster stretch geografisch afzonderlijke sites. toodo dit:

1. Installeer VMM op een virtuele machine in een Windows-failovercluster en selecteer Hallo optie toorun Hallo server als maximaal beschikbaar tijdens de installatie.
2. Hallo SQL Server-exemplaar dat wordt gebruikt door VMM moet worden gerepliceerd met SQL Server AlwaysOn-beschikbaarheidsgroepen, zodat er een replica van de database Hallo in Hallo secundaire site is.
3. Hallo-instructies in dit artikel toocreate een kluis, Hallo-server registreren en de beveiliging instelt. U moet tooregister elke VMM-server in het Hallo-cluster in Hallo Recovery Services-kluis. toodo dit Hallo Provider te installeren op een actief knooppunt en Hallo VMM-server geregistreerd. U kunt vervolgens Hallo Provider installeren op andere knooppunten.
4. Wanneer er een storing optreedt, worden Hallo VMM-server en de bijbehorende SQL Server-database failover, en toegankelijk vanuit Hallo secundaire site.



## <a name="prepare-for-storage-mapping"></a>Voorbereiden op opslagkoppeling


U opslag instellen toewijzing door toewijzing opslagclassificaties in een bron en doel van de VMM-servers toodo Hallo volgende:

  * **Doelopslag voor gerepliceerde virtuele machines identificeren**: een bron VM hardeschijf wordt gerepliceerd toohello opslag die u hebt opgegeven (SMB-share of het cluster shared volumes (CSV's)) in de doellocatie Hallo.
  * **Plaatsing van de replica virtuele machine**: de toewijzing van de opslag is gebruikte toooptimally plaats gerepliceerde virtuele machines op Hyper-V-hostservers. Virtuele replicamachines worden geplaatst op hosts die toegang heeft tot opslagclassificatie Hallo toegewezen.
  * **Er is geen toewijzing van opslag**— als u de toewijzing van opslag niet configureert, worden virtuele machines gerepliceerde toohello standaardopslaglocatie op Hallo Hyper-V-hostserver die zijn gekoppeld aan de virtuele replicamachine Hallo opgegeven.

Opmerking:
- U kunt de toewijzing tussen twee VMM-clouds op één server instellen.
- Opslagclassificaties moet beschikbaar toohello hostgroepen bevinden zich in de bron en doel-clouds.
- Classificaties hoeft niet toohave Hallo hetzelfde type opslag. U kunt bijvoorbeeld een bron-classificatie met SMB-shares tooa doel classificatie met CSV's toewijzen.

### <a name="example"></a>Voorbeeld
Als classificaties juist zijn geconfigureerd in VMM wanneer u Hallo bron en doel-VMM-server tijdens de toewijzing van opslag selecteert, is de bron en doel classificaties Hallo wordt weergegeven. Hier volgt een voorbeeld van bestandsshares voor opslag en de classificaties voor een organisatie met twee locaties in New York en Chicago.

| **Locatie** | **VMM-server** | **Bestandsshare (bron)** | **Classificatie (bron)** | **Toegewezen aan** | **Bestandsshare (doel)** |
| --- | --- | --- | --- | --- | --- |
| New York |VMM_Source |SourceShare1 |GOUD |GOLD_TARGET |TargetShare1 |
| SourceShare2 |ZILVER |SILVER_TARGET |TargetShare2 | | |
| SourceShare3 |BRONS |BRONZE_TARGET |TargetShare3 | | |
| Chicago |VMM_Target | |GOLD_TARGET |Niet toegewezen | |
|  |SILVER_TARGET |Niet toegewezen | | | |
|  |BRONZE_TARGET |Niet toegewezen | | | |

Met dit voorbeeld:

* Wanneer een replica virtuele machine wordt gemaakt voor elke virtuele machine op GOLD-opslag (SourceShare1), worden gerepliceerde tooa GOLD_TARGET opslag (TargetShare1).
* Wanneer een replica virtuele machine wordt gemaakt voor elke virtuele machine op zilver opslag (SourceShare2), wordt deze gerepliceerd tooa SILVER_TARGET (TargetShare2) opslag, enzovoort.

### <a name="multiple-storage-locations"></a>Meerdere opslaglocaties
Als Hallo doel classificatie is toegewezen toomultiple SMB-shares of CSV's, wordt de optimale opslaglocatie Hallo automatisch geselecteerd wanneer Hallo virtuele machine is beveiligd. Als er geen geschikte doelopslag beschikbaar met is Hallo classificatie Hallo standaard opgegeven opslaglocatie opgegeven op Hallo Hyper-V-host is gebruikte tooplace Hallo replica virtuele harde schijven.

Hallo volgende tabel wordt weergegeven hoe opslagclassificatie en gedeelde clustervolumes zijn ingesteld in ons voorbeeld.

| **Locatie** | **Classificatie** | **Gekoppelde opslag** |
| --- | --- | --- |
| New York |GOUD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> |
| ZILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p> | |
| Chicago |GOLD_TARGET |<p>C:\ClusterStorage\TargetVolume1</p><p>\\FileServer\TargetShare1</p> |
| SILVER_TARGET |<p>C:\ClusterStorage\TargetVolume2</p><p>\\FileServer\TargetShare2</p> | |

Deze tabel bevat een overzicht van Hallo gedrag wanneer u de beveiliging voor virtuele machines (VM1 - VM5) in dit Voorbeeldomgeving inschakelen.

| **Virtuele machine** | **Bron-opslag** | **Classificatie van bron** | **Toegewezen doelopslag** |
| --- | --- | --- | --- |
| VM1 |C:\ClusterStorage\SourceVolume1 |GOUD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\\FileServer\SourceShare1</p><p>Beide GOLD_TARGET</p> |
| VM2 |\\FileServer\SourceShare1 |GOUD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> <p>Beide GOLD_TARGET</p> |
| VM3 |C:\ClusterStorage\SourceVolume2 |ZILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\FileServer\SourceShare2</p> |
| VM4 |\FileServer\SourceShare2 |ZILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p><p>Beide SILVER_TARGET</p> |
| VM5 |C:\ClusterStorage\SourceVolume3 |N.v.t. |Er is geen toewijzing, zodat de standaardopslaglocatie Hallo van Hallo Hyper-V-host wordt gebruikt |



### <a name="data-privacy-overview"></a>Overzicht van privacy

Deze tabel ziet u hoe gegevens worden opgeslagen in dit scenario:

- - -
| Actie | **Details** | **Verzamelde gegevens** | **Gebruiken** | **Vereist** |
| --- | --- | --- | --- | --- |
| **Registratie** | U kunt een VMM-server registreren in een Recovery Services-kluis. Als u later toounregister een server wilt, kunt u dit doen door Hallo-servergegevens uit hello Azure-portal te verwijderen. | Wanneer een VMM-server is geregistreerd Site Recovery worden verzameld, processen, en de metagegevens over Hallo VMM-server en het Hallo-namen van de VMM-clouds Hallo gedetecteerd door Site Recovery. | Hallo gegevens gebruikte tooidentify is en communicatie met de juiste VMM-beheerserver Hallo en configureren van instellingen voor de juiste VMM-clouds. | Deze functie is vereist. Als u deze informatie tooSite herstel niet dat toosend wilt kunt u Hallo Site Recovery-service niet gebruiken. |
| **Replicatie inschakelen** | Hello Azure Site Recovery Provider is geïnstalleerd op de VMM-server Hallo en Hallo-kanaal voor communicatie met de Hallo Site Recovery-service. Hallo Provider is een dynamic-link library (DLL) gehost Hallo VMM. Hallo 'Datacenterherstel' functie opgehaald na het Hallo-Provider is geïnstalleerd, ingeschakeld in Hallo VMM administrator-console. Nieuwe en bestaande virtuele machines kunnen deze functie tooenable beveiliging voor een virtuele machine inschakelen. |Met deze eigenschap is ingesteld verzendt Hallo Provider Hallo naam en de ID van Hallo VM tooSite herstel.  Replicatie is ingeschakeld door Windows Server 2012 of Windows Server 2012 R2 Hyper-V Replica. Hallo virtuele machinegegevens worden gerepliceerd van een Hyper-V-host tooanother (doorgaans te vinden in een datacenter van verschillende "herstelpunt'). |Site Recovery gebruikt Hallo toopopulate Hallo VM metagegevens in hello Azure-portal. | Deze functie is een essentieel onderdeel van het Hallo-service en kan niet worden uitgeschakeld. Als u niet toosend deze informatie wilt, niet de Site Recovery-beveiliging voor virtuele machines inschakelt. Houd er rekening mee dat alle gegevens die worden verzonden door Hallo Provider tooSite herstel wordt verzonden via HTTPS. |
| **Plan voor herstel** | Herstelplannen helpen u bij het maken van een plan orchestration voor Hallo recovery Datacenter. Hallo volgorde waarin virtuele machines of een groep van virtuele machines op Hallo herstelsite moet worden gestart, kunt u definiëren. U kunt ook een geautomatiseerde scripts toobe uitvoeren of een handmatige actie toobe genomen op Hallo moment van herstel voor elke virtuele machine opgeven. Failover wordt doorgaans geactiveerd op Hallo recovery plan niveau voor gecoördineerde herstel. | Site Recovery worden verzameld, verwerkt en metagegevens voor het herstelplan hello, met inbegrip van metagegevens van de virtuele machine en metagegevens van eventuele automatiseringsscripts en -opmerkingen bij de handmatige actie verzendt. |Hallo-metagegevens zijn gebruikte toobuild Hallo herstelplan in hello Azure-portal. |Deze functie is een essentieel onderdeel van het Hallo-service en kan niet worden uitgeschakeld. Als u niet toosend deze informatie tooSite herstel wilt, niet herstelplannen maken. |
| **Netwerktoewijzing** | Maps netwerkgegevens van Hallo primaire data center toohello herstel Datacenter. Wanneer virtuele machines zijn hersteld op de herstelsite hello, helpt het netwerktoewijzing netwerkverbinding tot stand wordt gebracht. |Site Recovery worden verzameld, verwerkt en verzendt Hallo metagegevens van de logische netwerken Hallo voor elke site (primair en datacenter). |Hallo metagegevens is gebruikte toopopulate netwerkinstellingen, zodat u hello netwerkgegevens kunt toewijzen. | Deze functie is een essentieel onderdeel van het Hallo-service en kan niet worden uitgeschakeld. Als u niet toosend deze informatie tooSite herstel wilt, hoeft u netwerktoewijzing. |
| **Failover (geplande en ongeplande/testen)** | Failover wordt overgenomen virtuele machines van één VMM-beheerde gegevens center tooanother. Hallo failover gestart handmatig in hello Azure-portal. |Hallo Provider op Hallo VMM-server is op de hoogte van Hallo failover-gebeurtenis met Site Recovery en wordt een actie voor failover uitgevoerd op Hallo Hyper-V-host via de VMM-interfaces. Werkelijke failover van een virtuele machine is van een Hyper-V-host tooanother en verwerkt door Windows Server 2012 of Windows Server 2012 R2 Hyper-V Replica. Of achterwaartse richting Site Recovery gebruikt Hallo-informatie toopopulate Hallo status van Hallo failover actie informatie verzonden in hello Azure-portal. | Deze functie is een essentieel onderdeel van het Hallo-service en kan niet worden uitgeschakeld. Als u niet toosend deze informatie tooSite herstel wilt, hoeft u failover. |

## <a name="next-steps"></a>Volgende stappen

Nadat u Hallo-implementatie hebt getest, meer informatie over andere typen [failover](site-recovery-failover.md)
