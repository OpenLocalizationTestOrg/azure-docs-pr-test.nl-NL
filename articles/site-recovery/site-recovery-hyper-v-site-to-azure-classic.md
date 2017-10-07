---
title: aaaReplicate Hyper-V-machines tooAzure in de klassieke portal Hallo | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooreplicate Hyper-V virtuele machines tooAzure wanneer computers worden niet beheerd in VMM-clouds.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 3f4c4483-e3dd-495a-bd02-c16e9e28c88d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 02/21/2017
ms.author: raynew
ms.openlocfilehash: 12d08d950a79e956436cb03ffc87ab40e86c589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-without-vmm-with-azure-site-recovery"></a>Repliceren tussen on-premises Hyper-V virtuele machines en Azure (zonder VMM) met Azure Site Recovery
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Klassieke portal](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

Dit artikel wordt beschreven hoe tooreplicate lokale Hyper-V virtuele machines tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal. Hyper-V-servers worden in dit scenario wordt niet beheerd in VMM-clouds.

Na het lezen van dit artikel, eventuele opmerkingen posten Hallo onderin of technische vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="site-recovery-in-hello-azure-portal"></a>Site Recovery in hello Azure-portal

Azure heeft twee verschillende [implementatiemodellen](../resource-manager-deployment-model.md) voor het maken van en werken met resources: Azure Resource Manager en het klassieke model. Azure heeft bovendien twee portals: hello klassieke Azure-portal en hello Azure-portal.

Dit artikel wordt beschreven hoe toodeploy in de klassieke portal Hallo. klassieke portal Hallo kan gebruikte toomaintain bestaande kluizen zijn. U kunt geen nieuwe kluizen met de klassieke portal Hallo maken.

## <a name="site-recovery-in-your-business"></a>Site Recovery in uw bedrijf

Organisaties moeten een BCDR-strategie die bepaalt hoe apps en gegevens beschikbaar tijdens geplande en ongeplande uitval blijven, en toonormal werkomstandigheden zo snel mogelijk te herstellen. Dit is wat Site Recovery kan:

* Off-sitebeveiliging voor business-apps op virtuele Hyper-V-machines worden uitgevoerd.
* Een tooset één locatie, beheren en controleren van replicatie, failovers en herstel.
* TooAzure eenvoudige failover en failback (herstel) van Azure tooHyper-V-hostservers in uw on-premises site.
* Herstelplannen met meerdere virtuele machines configureren, zodat er voor gelaagde toepassingsworkloads gelijktijdig een failover wordt uitgevoerd.

## <a name="azure-prerequisites"></a>Vereisten voor Azure
* U hebt een [Microsoft Azure](https://azure.microsoft.com/)-account nodig. U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).
* U moet een Azure storage-account toostore gerepliceerde gegevens. Hallo-account moet geo-replicatie is ingeschakeld. Deze moet in dezelfde regio als de Azure Site Recovery-kluis Hallo Hallo en worden gekoppeld aan hetzelfde abonnement Hallo. [Meer informatie over Azure storage](../storage/common/storage-introduction.md). We geen bewegende opslagaccounts die zijn gemaakt met behulp van Hallo ondersteuning [nieuwe Azure portal](../storage/common/storage-create-storage-account.md) over resourcegroepen.
* U hebt een Azure-netwerk nodig, zodat virtuele machines in Azure verbonden tooa netwerk worden wanneer u een failover van de primaire site.

## <a name="hyper-v-prerequisites"></a>Hyper-V-vereisten
* In de bronsite lokale Hallo moet u een of meer servers met **Windows Server 2012 R2** met Hallo Hyper-V-rol is geïnstalleerd of **Microsoft Hyper-V Server 2012 R2**. Deze server moet het volgende doen:
* Een of meer virtuele machines bevatten.
* Zijn verbonden toohello Internet, rechtstreeks of via een proxyserver.
* Hallo-oplossingen die zijn beschreven in KB actief [2961977](https://support.microsoft.com/en-us/kb/2961977 "KB2961977").

## <a name="virtual-machine-prerequisites"></a>Vereisten voor virtuele machine
Virtuele machines die u wilt dat tooprotect moet voldoen aan [vereisten van de virtuele machine van Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="provider-and-agent-prerequisites"></a>Provider en agent-vereisten
Als onderdeel van de implementatie van Azure Site Recovery past u hello Azure Site Recovery Provider installeren en hello Azure Recovery Services Agent op elke Hyper-V-server. Opmerking:

* We raden u altijd de meest recente versies Hallo Hallo Provider en agent worden uitgevoerd. Dit zijn beschikbaar in Hallo Site Recovery-portal.
* Alle Hyper-V-servers in een kluis moet hebben Hallo dezelfde versies van Hallo Provider en agent.
* Hallo Provider die wordt uitgevoerd op de server Hallo verbindt tooSite herstel via Hallo internet. U kunt dit doen zonder een proxy Hallo proxy-instellingen die momenteel zijn geconfigureerd op Hallo Hyper-V server of met een aangepaste proxy-instellingen die u tijdens de installatie van de Provider configureren. U moet zorgen dat Hallo proxyserver gewenste toouse toegang tot deze Hallo URL's voor het verbinden van tooAzure toomake:

  * *.accesscontrol.windows.net
  * *.backup.windowsazure.com
  * *.hypervrecoverymanager.windowsazure.com
  * *.store.core.windows.net      
  * *.blob.core.windows.net
  - https://www.msftncsi.com/ncsi.txt
  - time.windows.com
  - time.nist.gov
* Bovendien toestaan Hallo IP-adressen die worden beschreven [Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/details.aspx?id=41653) en het protocol HTTPS (443). U hebt tooallow Hallo IP-adresbereiken van hello Azure-regio die u van plan toouse en die van de VS-West bent.

Deze afbeelding ziet u de verschillende communicatiekanalen Hallo en poorten gebruikt door Site Recovery voor de orchestration- en replicatie

![B2A-topologie](./media/site-recovery-hyper-v-site-to-azure-classic/b2a-topology.png)

## <a name="step-1-create-a-vault"></a>Stap 1: Een kluis maken
1. Meld u aan toohello [beheerportal](https://portal.azure.com).
2. Vouw **Data Services** > **Recovery Services** en klik op **Site Recovery-kluis**.
3. Klik op **Nieuw maken** > **Snelle invoer**.
4. In **naam**, voer een beschrijvende naam tooidentify Hallo-kluis.
5. In **regio**, selecteer de geografische regio voor de kluis Hallo Hallo. toocheck ondersteunde regio's Zie geografische beschikbaarheid in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Klik op **Kluis maken**.

    ![Nieuwe kluis](./media/site-recovery-hyper-v-site-to-azure-classic/vault.png)

Selectievakje Hallo status balk tooconfirm die Hallo kluis is gemaakt. Hallo-kluis wordt weergegeven als **Active** op Hallo hoofdpagina Recovery Services.

## <a name="step-2-create-a-hyper-v-site"></a>Stap 2: Een Hyper-V-site maken
1. Klik op Hallo kluis tooopen Hallo snel starten-pagina op Hallo Recovery Services-pagina. Snel starten kan ook worden geopend op elk gewenst moment Hallo-pictogram.

    ![Snel starten](./media/site-recovery-hyper-v-site-to-azure-classic/quick-start-icon.png)
2. Selecteer in de vervolgkeuzelijst Hallo **tussen een lokale Hyper-V-site en Azure**.

    ![Hyper-V-site-scenario](./media/site-recovery-hyper-v-site-to-azure-classic/select-scenario.png)
3. In **een Hyper-V-Site maken** klikt u op **maken van Hyper-V-site**. Geef een sitenaam op en sla.

    ![Hyper-V-site](./media/site-recovery-hyper-v-site-to-azure-classic/create-site.png)

## <a name="step-3-install-hello-provider-and-agent"></a>Stap 3: Hallo Provider en agent installeren
Hallo Provider en agent installeren op elke Hyper-V-server die virtuele machines die u wilt dat tooprotect heeft.

Als u op een Hyper-V-cluster installeert, voert stap 5-11 op elk knooppunt in Hallo failover-cluster. Nadat alle knooppunten zijn geregistreerd en beveiliging is ingeschakeld, wordt virtuele machines worden beveiligd, zelfs als ze via knooppunten in cluster Hallo migreren.

1. In **voorbereiden Hyper-V-servers**, klikt u op **Download een registratiesleutel** bestand.
2. Op Hallo **registratiesleutel downloaden** pagina, klikt u op **downloaden** volgende toohello-site. Hallo sleutel tooa veilige locatie die gemakkelijk toegankelijk zijn voor Hallo Hyper-V-server downloaden. Hallo-sleutel is geldig tot 5 dagen nadat deze gegenereerd.

    ![Registratiesleutel](./media/site-recovery-hyper-v-site-to-azure-classic/download-key.png)
3. Klik op **downloaden Hallo Provider** tooobtain Hallo meest recente versie.
4. Hallo-bestand op elke Hyper-V-server die u wilt dat tooregister in Hallo kluis uitgevoerd. Hallo-bestand installeert twee onderdelen:
   * **Azure Site Recovery Provider**: zorgt voor communicatie en orchestration tussen Hallo Hyper-V-server en hello Azure Site Recovery-portal.
   * **Azure Recovery Services-Agent**, verwerkt gegevenstransport tussen virtuele machines op de bronserver Hyper-V Hallo en Azure storage.
5. U kunt zich in **Microsoft Update** aanmelden voor updates. Met deze instelling is ingeschakeld, worden Provider en Agent-updates geïnstalleerd op basis van beleid voor tooyour Microsoft Update.

    ![Microsoft-updates](./media/site-recovery-hyper-v-site-to-azure-classic/provider1.png)
6. In **installatie** opgeven waar tooinstall Hallo Provider en Agent op Hallo Hyper-V-server.

    ![Installatielocatie](./media/site-recovery-hyper-v-site-to-azure-classic/provider2.png)
7. Nadat de installatie is voltooid blijven Hallo kluis setup tooregister Hallo-server.
8. Op Hallo **Kluisinstellingen** pagina, klikt u op **Bladeren** tooselect Hallo-sleutelbestand. Geef hello Azure Site Recovery-abonnement, Hallo kluisnaam, en Hallo Hyper-V-site toowhich Hallo Hyper-V server behoort.

    ![Serverregistratie](./media/site-recovery-hyper-v-site-to-azure-classic/provider8.PNG)
9. Op Hallo **internetverbinding** pagina die u opgeeft hoe Hallo Provider verbinding maakt met tooAzure Site Recovery. Selecteer **standaardsysteemproxyinstellingen gebruiken** toouse Hallo standaardinstellingen voor internetverbindingen op Hallo-server geconfigureerd. Als u niet een waarde Hallo standaard instellingen worden gebruikt.

   ![Instellingen voor internet](./media/site-recovery-hyper-v-site-to-azure-classic/provider7.PNG)
10. De registratie begint tooregister Hallo server in Hallo kluis.

    ![Serverregistratie](./media/site-recovery-hyper-v-site-to-azure-classic/provider15.PNG)
11. Nadat de registratie is voltooid metagegevens van Hallo Hyper-V server wordt opgehaald door Azure Site Recovery en Hallo-server wordt weergegeven op Hallo **Hyper-V-Sites** tabblad op Hallo **Servers** pagina in Hallo kluis.

### <a name="install-hello-provider-from-hello-command-line"></a>Hallo Provider installeren vanaf de opdrachtregel Hallo
Als alternatief kunt u hello Azure Site Recovery Provider installeren vanaf de opdrachtregel Hallo. Als u wilt dat tooinstall Hallo Provider op een computer met Windows Server Core 2012 R2, moet u deze methode gebruiken. Vanaf de opdrachtregel Hallo als volgt uitvoeren:

1. Hallo-Provider en de registratiesleutel sleutel tooa installatiemap downloaden. Bijvoorbeeld: C:\ASR.
2. Voer een opdrachtprompt als beheerder en typ:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Installeer Provider Hallo door te voeren:

        C:\ASR> setupdr.exe /i
4. Voer Hallo toocomplete registratie te volgen:

        CD C:\Program Files\Microsoft Azure Site Recovery Provider
        C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

Parameters zijn waar:

* **/ Credentials**: Geef de locatie Hallo van Hallo-registratiesleutel die u hebt gedownload.
* **/ FriendlyName**: Geef een naam tooidentify Hallo Hyper-V-hostserver. Deze naam wordt weergegeven in het Hallo-portal
* **/ EncryptionEnabled**: optioneel. Geef op of tooencrypt replica virtuele machines in Azure (versleuteling bij rust).
* **/ proxyaddress**; **/proxyport**; **proxyusername**; **/proxypassword**: optioneel. Proxyparameters opgeven als u een aangepaste proxy toouse wilt, of uw bestaande proxy verificatie vereist.

## <a name="step-4-create-an-azure-storage-account"></a>Stap 4: Een Azure Storage-account maken
* In **voorbereiden resources** Selecteer **Storage-Account maken** toocreate Azure storage-account als u niet hebt. Hallo-account hebt geo-replicatie is ingeschakeld. Deze moet in dezelfde regio als de Azure Site Recovery-kluis Hallo Hallo en worden gekoppeld aan hetzelfde abonnement Hallo.

    ![Storage-account maken](./media/site-recovery-hyper-v-site-to-azure-classic/create-resources.png)

> [!NOTE]
> 1. We bieden geen ondersteuning voor Hallo verplaatsing van Storage-accounts die zijn gemaakt met behulp van Hallo [nieuwe Azure portal](../storage/common/storage-create-storage-account.md) over resourcegroepen.
> 2. [Migratie van opslagaccounts](../azure-resource-manager/resource-group-move-resources.md) via resource groepen binnen hetzelfde abonnement Hallo of voor abonnementen wordt niet ondersteund voor storage-accounts gebruikt voor de implementatie van Site Recovery.
>

## <a name="step-5-create-and-configure-protection-groups"></a>Stap 5: Maken en beveiligingsgroepen configureren
Beveiligingsgroepen zijn logische groeperingen van virtuele machines die u wilt met behulp van tooprotect Hallo dezelfde beveiligingsinstellingen. U beveiligingsgroep instellingen tooa beveiliging toepassen en deze instellingen zijn toegepast tooall virtuele machines dat u toohello groep toevoegen.

1. In **maken en configureren van beveiligingsgroepen** klikt u op **een beveiligingsgroep maakt**. Als alle vereiste onderdelen niet aanwezig zijn een bericht wordt uitgegeven en klikt u op **details weergeven** voor meer informatie.
2. In Hallo **beveiligingsgroepen** tabblad een beveiligingsgroep toevoegen. Geef een naam, het Hallo-bronsite Hyper-V, Hallo doel **Azure**, de naam van de Azure Site Recovery-abonnement en hello Azure storage-account.

    ![Beveiligingsgroep](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group.png)
3. In **replicatie-instellingen** set Hallo **Kopieerfrequentie** toospecify hoe vaak Hallo gegevens verschillen moet worden gesynchroniseerd tussen Hallo bron en doel. U kunt too30 seconden, 5 minuten of 15 minuten instellen.
4. In **herstelpunten bewaren** opgeven hoeveel uren herstelgeschiedenis moeten worden opgeslagen.
5. In **frequentie van toepassingsconsistente momentopnamen** kunt u opgeven of tootake momentopnamen die gebruikmaken van Volume Shadow Copy Service (VSS) tooensure die toepassingen zich in een consistente status wanneer Hallo momentopname wordt gemaakt. Deze worden niet standaard overgenomen. Zorg ervoor dat deze waarde is ingesteld tooless dan Hallo aantal aanvullende herstelpunten dat u configureert. Dit wordt alleen ondersteund als Hallo virtuele machine wordt uitgevoerd op een Windows-besturingssysteem.
6. In **begintijd initiële replicatie** wanneer initiële replicatie van virtuele machines in de beveiligingsgroep Hallo moet worden verzonden tooAzure opgeven.

    ![Beveiligingsgroep](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group2.png)

## <a name="step-6-enable-virtual-machine-protection"></a>Stap 6: Beveiliging van virtuele machines inschakelen
Virtuele machines tooa beveiliging groep tooenable beveiliging voor hen toevoegen.

> [!NOTE]
> Het beveiligen van virtuele machines waarop Linux wordt uitgevoerd met een statisch IP-adres, wordt niet ondersteund.
>
>

1. Op Hallo **Machines** tabblad voor de beveiligingsgroep hello, klikt u op ** toevoegen virtuele machines tooprotection groepen tooenable beveiliging **.
2. Op Hallo **beveiliging voor virtuele Machine inschakelen** Selecteer Hallo virtuele machines die u wilt dat tooprotect pagina.

    ![Beveiliging van de virtuele machine inschakelen](./media/site-recovery-hyper-v-site-to-azure-classic/add-vm.png)

    Hallo inschakelen beveiligingstaken begint. U kunt de voortgang volgen op Hallo **taken** tabblad. Nadat de taak beveiliging voltooien Hallo is uitgevoerd Hallo virtuele machine gereed voor failover.
3. Nadat de beveiliging is instellen, dus u kunt doen:

   * Weergeven van virtuele machines in **beveiligde Items** > **beveiligingsgroepen** > *protectiongroup_name*  >  **Virtuele Machines** kunt u de details in Hallo toomachine inzoomen **eigenschappen** tabblad...
   * Hallo failover-eigenschappen configureren voor een virtuele machines in **beveiligde Items** > **beveiligingsgroepen** > *protectiongroup_name*  >  **Virtuele Machines** *virtual_machine_name* > **configureren**. U kunt configureren:

     * **Naam**: Hallo-naam van Hallo virtuele machine in Azure.
     * **De grootte van**: Hallo doelgrootte van Hallo virtuele machine die overgenomen wordt.

       ![Eigenschappen van virtuele machine configureren](./media/site-recovery-hyper-v-site-to-azure-classic/vm-properties.png)
   * Configureert instellingen voor extra virtuele machine in *beveiligde Items** > **beveiligingsgroepen** > *protectiongroup_name* > **virtuele Machines** *virtual_machine_name* > **configureren**, waaronder:

     * **Netwerkadapters**: Hallo aantal netwerkadapters wordt bepaald door het Hallo-grootte die u voor de virtuele doelmachine Hallo opgeeft. Controleer [specificaties van de grootte van de virtuele machine](../virtual-machines/linux/sizes.md) voor het aantal NIC's ondersteund door de grootte van de virtuele machine Hallo Hallo.

       Wanneer u Hallo grootte voor een virtuele machine wijzigen en het Hallo-instellingen opslaan, Hallo aantal netwerkadapters wordt gewijzigd wanneer u opent **configureren** pagina Hallo volgende keer. Hallo aantal netwerkadapters van de virtuele doelmachines is minimaal Hallo aantal netwerkadapters op de virtuele bronmachine en het maximum aantal netwerkadapters wordt ondersteund door Hallo grootte van de gekozen Hallo virtuele machine. Deze wordt hieronder beschreven:

       * Als het aantal netwerkadapters op de bronmachine Hallo Hallo kleiner dan of gelijk aantal adapters toohello toegestaan voor de doelgrootte machine Hallo vervolgens Hallo doel hetzelfde aantal adapters als bron Hallo Hallo.
       * Als het aantal adapters voor de virtuele bronmachine Hallo HALLO hallo maximum overschrijden voor Hallo doelgrootte, wordt maximaal Hallo doel wordt gebruikt.
       * Bijvoorbeeld als een bronmachine twee netwerkadapters heeft en de grootte van Hallo doelmachine vier ondersteunt, Hallo doelmachine twee adapters hebben. Als Hallo-bronmachine twee adapters heeft, maar hello ondersteunde doelgrootte biedt alleen ondersteuning voor een hebben Hallo doelmachine slechts één adapter.

     * **Azure-netwerk**: Geef Hallo netwerk toowhich Hallo virtuele machine failover moet uitvoeren. Als Hallo virtuele machine meerdere netwerkadapters alle netwerkadapters heeft moet u verbonden toohello dezelfde Azure-netwerk.
     * **Subnet** voor elke netwerkadapter op Hallo virtuele machine, selecteer Hallo subnet in hello Azure-netwerk toowhich Hallo machine na een failover moet verbinding maken.
     * **Doel-IP-adres**: als Hallo-netwerkadapter van de virtuele bronmachine geconfigureerde statische toouse is een IP-adres daarna kunt u Hallo IP-adres opgeven voor Hallo doel-virtuele machine tooensure die machine Hallo Hallo heeft hetzelfde IP-adres na een failover .  Als u een IP-adres niet opgeeft wordt een beschikbaar adres worden toegewezen op Hallo moment van failover. Als u een adres dat wordt gebruikt, mislukt de failover.

     > [!NOTE]
     > [Migratie van netwerken](../azure-resource-manager/resource-group-move-resources.md) via resource groepen binnen hetzelfde abonnement Hallo of voor abonnementen wordt niet ondersteund voor netwerken gebruikt voor de implementatie van Site Recovery.
     >

     ![Eigenschappen van virtuele machine configureren](./media/site-recovery-hyper-v-site-to-azure-classic/multiple-nic.png)




## <a name="step-7-create-a-recovery-plan"></a>Stap 7: Een herstelplan maken
U kunt een testfailover voor één virtuele machine of een herstelplan dat een of meer virtuele machines bevat uitvoeren in volgorde tootest Hallo-implementatie. [Meer informatie](site-recovery-create-recovery-plans.md) over het maken van een herstelplan.

## <a name="step-8-test-hello-deployment"></a>Stap 8: Hallo-implementatie testen
Er zijn twee manieren toorun een test failover tooAzure.

* **Testfailover zonder een Azure-netwerk**: dit type testfailover wordt gecontroleerd dat de virtuele machine Hallo voordoet correct in Azure. Hallo virtuele machine niet verbonden tooany Azure-netwerk na een failover.
* **Testfailover met een Azure-netwerk**: dit type failover controleert of de volledige replicatieomgeving Hallo maximaal zoals verwacht wordt geleverd en die failover Hallo virtuele machines toohello opgegeven doel-Azure-netwerk is verbonden. Houd er rekening mee dat voor een testfailover Hallo subnet van de virtuele testmachine Hallo zal worden gekeken hoe op basis van het subnet van de virtuele replicamachine Hallo Hallo. Dit is de verschillende tooregular replicatie wanneer Hallo subnet van een replica virtuele machine is gebaseerd op het subnet van de virtuele bronmachine Hallo Hallo.

Als u een testfailover toorun zonder op te geven van een Azure-netwerk wilt hoeft u niet tooprepare alles.

toorun een testfailover met een doel-Azure-netwerk u een nieuw Azure-netwerk dat is geïsoleerd toocreate van uw Azure productienetwerk (standaardwerking moet wanneer u een nieuw netwerk in Azure maakt). Lees [een testfailover uitvoeren](site-recovery-failover.md) voor meer informatie.

toofully test uw replicatie- en implementatie moet u tooset Hallo-infrastructuur zodat die Hallo gerepliceerd toowork van de virtuele machine zoals verwacht. Op één manier doen dit tootooset een virtuele machine als een domeincontroller met DNS en repliceert met behulp van Site Recovery toocreate in Hallo test netwerk door het uitvoeren van een testfailover tooAzure.  [Lees meer](site-recovery-active-directory.md#test-failover-considerations) over test failover-overwegingen voor Active Directory.

Hallo testfailover als volgt uitvoeren:

> [!NOTE]
> tooget hello beste prestaties als u een failover-tooAzure doet, zorg ervoor dat u hello Azure-Agent in Hallo beveiligde computer hebt geïnstalleerd. Dit helpt bij het sneller opstarten en helpt ook bij de diagnose in geval van problemen. De Linux-agent is [hier](https://github.com/Azure/WALinuxAgent) en de Windows-agent [hier](http://go.microsoft.com/fwlink/?LinkID=394789) beschikbaar.
>
>

1. Op Hallo **herstelplannen** tabblad, selecteer Hallo-plan en klik op **Testfailover**.
2. Op Hallo **Testfailover bevestigen** pagina **geen** of een specifieke Azure-netwerk.  Houd er rekening mee dat als u selecteert **geen** hello testfailover gecontroleerd dat de virtuele machine Hallo gerepliceerd correct tooAzure maar configuratie van het replicatienetwerk niet gecontroleerd.

    ![Testfailover](./media/site-recovery-hyper-v-site-to-azure-classic/test-nonetwork.png)
3. Op Hallo **taken** tabblad kunt u failover voortgang bijhouden. U moet ook kunnen toosee Hallo virtuele machine testreplica in hello Azure-portal. Als u van uw on-premises netwerk tooaccess virtuele machines alles hebt ingesteld, kunt u een extern bureaublad verbinding toohello virtuele machine starten.
4. Wanneer failover Hallo Hallo bereikt **testen voltooien** fase, klikt u op **Test voltooien** toofinish up Hallo testfailover. U kunt inzoomen van toohello **taak** tootrack failover voortgang en status en tooperform tabblad acties die nodig zijn.
5. Na een failover, moet u kunnen toosee Hallo virtuele machine testreplica in hello Azure-portal. Als u van uw on-premises netwerk tooaccess virtuele machines alles hebt ingesteld, kunt u een extern bureaublad verbinding toohello virtuele machine starten.

   1. Controleren of Hallo virtuele machines worden gestart.
   2. Als u tooconnect toohello virtuele machine in Azure met extern bureaublad na een failover Hallo wilt, moet u verbinding met extern bureaublad inschakelen op Hallo virtuele machine voordat u Hallo testfailover uitvoeren. U moet ook tooadd een RDP-eindpunt op Hallo virtuele machine. U kunt gebruikmaken van een [Azure automation-runbook](site-recovery-runbook-automation.md) toodo die.
   3. Nadat de failover als u een openbaar IP-adres tooconnect toohello virtuele machine in Azure met behulp van extern bureaublad, zorg ervoor dat hebt u geen domeinbeleid die verbinden tooa virtuele machine via een openbaar adres wordt verhinderd.
6. Voer Hallo te volgen nadat Hallo testen voltooid is:

   * Klik op **Hallo testfailover is voltooid**. Hallo opschonen omgeving tooautomatically power testen uit en verwijdert u Hallo test-virtuele machines.
   * Klik op **notities** toorecord en eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo op te slaan.
7. Wanneer failover Hallo Hallo bereikt **testen voltooien** fase voltooien Hallo verificatie als volgt:
   1. Hallo replica virtuele machine weergeven in hello Azure-portal. Controleer of dat de virtuele machine Hallo kan worden gestart.
   2. Als u van uw on-premises netwerk tooaccess virtuele machines alles hebt ingesteld, kunt u een extern bureaublad verbinding toohello virtuele machine starten.
   3. Klik op **voltooid Hallo test** toofinish deze.
   4. Klik op **notities** toorecord en eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo op te slaan.
   5. Klik op **Hallo testfailover is voltooid**. Opruimen van Hallo omgeving tooautomatically power test uitschakelen en verwijderen van de virtuele testmachine Hallo.

## <a name="next-steps"></a>Volgende stappen
Wanneer uw implementatie actief is, kunt u [hier](site-recovery-failover.md) meer lezen over failovers.
