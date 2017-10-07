---
title: aaaReplicate VMware-machines of fysieke servers tooanother site (klassieke Azure-portal) | Microsoft Docs
description: Dit artikel tooreplicate VMware-machines of Windows of Linux fysieke servers tooa secundaire site gebruiken met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: nsoneji
manager: jwhit
editor: 
ms.assetid: b2cba944-d3b4-473c-8d97-9945c7eabf63
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 5789ca07f0aa15cf194615fd33103dac930d7b7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-on-premises-vmware-virtual-machines-or-physical-servers-tooa-secondary-site-in-hello-classic-azure-portal"></a>On-premises VMware-virtuele machines of fysieke servers tooa secundaire site in de klassieke Azure portal Hallo repliceren

## <a name="overview"></a>Overzicht
InMage Scout in Azure Site Recovery biedt realtime replicatie tussen on-premises VMware-sites. InMage Scout is opgenomen in de Azure Site Recovery-service-abonnementen. 

## <a name="prerequisites"></a>Vereisten
**Azure-account**: U moet een [Microsoft Azure](https://azure.microsoft.com/) account. U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/). [Meer informatie](https://azure.microsoft.com/pricing/details/site-recovery/) over prijzen voor Site Recovery.

## <a name="step-1-create-a-vault"></a>Stap 1: Een kluis maken
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op Nieuw > Beheer > back-up en siteherstel (OMS). U kunt ook klikken op Bladeren > Recovery Services-kluis > toevoegen.
3. In **naam** Geef een beschrijvende naam tooidentify Hallo-kluis. Als u meer dan één abonnement hebt, selecteert u een van uw abonnementen.
4. In **resourcegroep** een nieuwe resourcegroep maken of een bestaande set selecteren. Geef de velden van een Azure-regio toocomplete vereist.
5. In **locatie**, selecteer de geografische regio voor de kluis Hallo Hallo. toocheck ondersteunde regio's, Zie [prijzen van Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Als u wilt dat wordt tooquickly toegang Hallo kluis van Hallo Dashboard klikt u op pincode toodashboard en klik op maken.
7. Hallo nieuwe kluis wordt weergegeven op Hallo Dashboard > alle resources en op Hallo belangrijkste Recovery Services-kluizen blade.

## <a name="step-2-configure-hello-vault-and-download-inmage-scout-components"></a>Stap 2: Configureer Hallo kluis en InMage Scout onderdelen downloaden
1. Selecteer uw kluis in Hallo Recovery Services-kluizen blade en klik op instellingen.
2. In **instellingen** > **aan de slag** klikt u op **siteherstel** > stap 1: **infrastructuur voorbereiden**  >  **Beveiligingsdoel**.
3. In **beveiligingsdoel** toorecovery-site hebt geselecteerd en selecteer Ja, met VMware vSphere-Hypervisor. Klik vervolgens op OK.
4. In **Scout setup**, klik op downloaden toodownload InMage Scout 8.0.1 GA software en registratie-sleutel. setup-bestanden voor alle Hallo Hallo vereiste onderdelen in Hallo gedownloade ZIP-bestand.

## <a name="step-3-install-component-updates"></a>Stap 3: Component updates installeren
Meest recente informatie over Hallo [updates](#updates). Installeert u de updatebestanden Hallo op servers in Hallo volgorde:

1. RX-server als er een
2. Van configuratieservers
3. Processervers
4. Hoofddoelservers
5. vContinuum-servers
6. Bronserver (Windows en Linux-Server)

Hallo-updates als volgt installeren:

1. Hallo downloaden [bijwerken](https://aka.ms/asr-scout-update5) ZIP-bestand. Dit zip-bestand bevat de volgende bestanden Hallo:

   * RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.GZ
   * CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe
   * UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe
   * UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
   * vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe
   * UA update4 bits voor RHEL5, OL5, OL6, SUSE 10, 11 SUSE: UA_<Linux OS>_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
2. Hallo ZIP-bestanden extraheren.<br>
3. **Voor Hallo RX server**: kopie **RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz** toohello RX-server en pak het bestand. Hallo opgehaald map **/installeren**.<br>
4. **Voor de server-proces configuratieserver Hallo**: kopie **CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe** toohello configuratieserver en de processerver. Dubbelklik op toorun deze.<br>
5. **Voor Hallo Windows hoofddoelserver**: tooupdate Hallo unified agent, kopie **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello hoofddoelserver. Dubbelklik erop toorun deze. Let op Hallo van unified agent is ook van toepassing toohello bronserver als bron niet tot Update4 bijgewerkt is. U moet deze installeren op de bronserver Hallo evenals, zoals verderop in deze lijst worden vermeld.<br>
6. **Voor de vContinuum-server Hallo**: kopie **vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe** toohello vContinuum-server.  Zorg ervoor dat u Hallo vContinuum-wizard hebt gesloten. Dubbelklik op Hallo bestand toorun.<br>
7. **Voor Hallo Linux hoofddoelserver**: tooupdate Hallo unified agent, kopie **UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello de hoofdsleutel van de doelserver en pak het bestand. Hallo opgehaald map **/installeren**.<br>
8. **Voor de bronserver voor Windows hello**: U hoeft geen tooinstall Update 5-agent op de bron als soruce al op update4 is. Als het is minder dan update4, van toepassing hello update 5-agent.
Hallo tooupdate unified agent, kopie **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello-bronserver. Dubbelklik erop toorun deze. <br>
9. **Voor Linux-bronserver Hallo**: tooupdate Hallo unified agent, bijbehorende versie van toohello UA-Linux bestandsserver kopiëren en pak het bestand. Hallo opgehaald map **/installeren**.  Voorbeeld: Voor RHEL 6,7 64-bits-server kopiëren **UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello server en pak het bestand. Hallo opgehaald map **/installeren**.

## <a name="step-4-set-up-replication"></a>Stap 4: De replicatie instellen
1. De replicatie instellen tussen Hallo bron en doel VMware sites.
2. Voor instructies Hallo InMage Scout documentatie die gedownload met Hallo product te gebruiken. U kunt ook Hallo documentatie als volgt openen:

   * [Releaseopmerkingen](https://aka.ms/asr-scout-release-notes)
   * [Compatibiliteit matrix](https://aka.ms/asr-scout-cm)
   * [Gebruikershandleiding](https://aka.ms/asr-scout-user-guide)
   * [RX-gebruikershandleiding](https://aka.ms/asr-scout-rx-user-guide)
   * [Handleiding voor snelle installatie](https://aka.ms/asr-scout-quick-install-guide)

## <a name="updates"></a>Updates
### <a name="azure-site-recovery-scout-801-update-5"></a>Azure Site Recovery Scout 8.0.1 Update 5
Scout Update 5 is een cumulatieve update. Heeft alle Hallo correcties van update1 tot update4 en nieuwe oplossingen voor problemen en verbeteringen te volgen.
Oplossingen die zijn toegevoegd vanuit ASR Scout update4 tooupdate5 zijn specifieke tooMaster doel en de vContinuum-onderdelen. Als al uw bronservers, hoofddoel, configuratieserver, processerver en RX al op ASR Scout update4 vervolgens u moet tooapply update 5 alleen op de hoofddoelserver. 

**Nieuwe platformondersteuning**
* SUSE Linux Enterprise Server 11 4(SP4) servicepack

> [!NOTE]
> SLES 11 SP4 64 bits **InMage_UA_8.0.1.0_SLES11-SP4-64_GA_13Apr2017_release.tar.gz** wordt verpakt met base Scout GA pakket **InMage_Scout_Standard_8.0.1 GA.zip**. Download Scout GA pakket van de portal, zoals vermeld in [stap 1](#step-1-create-a-vault).
>

**Oplossingen voor problemen en verbeteringen**

* Verbetering van de betrouwbaarheid van Windows Cluster-ondersteuning
    * Vaste Sometime aantal Hallo P2V MSCS clusterschijven worden RAW na herstel
    * Fixed-P2V MSCS-cluster herstellen mislukt vanwege toodisk volgorde verschil
    * Fixed-MSCS-cluster toevoegen schijven bewerking is mislukt met de schijf komt niet overeen
    * Fixed-bron MSCS-cluster met de gereedheidscontrole toewijzing van RDM LUN's in grootte-verificatie is mislukt
    * Beveiliging van de cluster Fixed-één knooppunt mislukt vanwege tooSCSI verschil probleem 
    * Fixed-opnieuw beveiligen van Hallo P2V Windows clusterserver mislukt als doel clusterschijven aanwezig zijn. 
    
* Tijdens de failback beveiliging, als de geselecteerde MT is niet op Hallo dezelfde ESXi-server als die Hallo bronmachine beveiligd (tijdens forward beveiliging) en vervolgens de vContinuum opgehaald Hallo verkeerde MT tijdens Failback herstel en vervolgens de herstelbewerking mislukt.

> [!NOTE]
> 
> * Zijn van toepassing tooonly die fysiek MSCS-cluster die zijn opnieuw worden beveiligd met ASR Scout update5 hierboven oplossingen voor P2V-cluster. tooavail hello cluster correcties op Hallo P2V MSCS-cluster met oudere updates al beveiligd, moet u toofollow Hallo Upgradestappen die worden vermeld in de sectie Hallo 12, Upgrade beveiligd P2V MSCS-cluster tooScout Update5 van [ASR Scout Release Opmerkingen bij de](https://aka.ms/asr-scout-release-notes).
> 
> * Opnieuw beveiligen van fysieke MSCS-cluster kunt opnieuw gebruiken bestaande doel schijven alleen als op Hallo moment van opnieuw beveiliging, Hallo dezelfde set schijven actief zijn op elk van de knooppunten als zijn wanneer u in eerste instantie beveiligd Hallo-cluster. Als niet zo is, klikt u vervolgens er handmatige stappen zoals vermeld in de sectie 12 van [ASR Scout Release-opmerkingen](https://aka.ms/asr-scout-release-notes) te verplaatsen Hallo doel aan clientzijde schijven toohello juiste datastore pad toore-gebruiken ze tijdens het opnieuw beveiligen. Als u Hallo MSCS-cluster in de modus voor P2V opnieuw beveiligen zonder de volgende stappen de upgrade wordt het nieuwe schijf maken op de doelserver ESXi Hallo. Toomanually verwijderen Hallo oude schijven uit Hallo gegevensarchief nodig.
> 
> * Wanneer bron SLES11 of SLES11 met een andere service pack server probleemloos opnieuw wordt opgestart, wordt een Hallo moet handmatig worden gemarkeerd **hoofdmap** paren van replicatie voor het opnieuw synchroniseren schijf zoals deze wordt niet gewaarschuwd in CX UI. Als u dit niet is ingeschakeld Hallo hoofdmap schijf voor resync, wordt er problemen met de gegevensintegriteit (DI).
> 

### <a name="azure-site-recovery-scout-801-update-4"></a>Azure Site Recovery Scout 8.0.1 Update 4
Scout Update 4 is een cumulatieve update. Heeft alle Hallo correcties van update1 tot update3 en nieuwe oplossingen voor problemen en verbeteringen te volgen.

**Nieuwe platformondersteuning**

* Is er ondersteuning toegevoegd voor de vCenter/vSphere 6.0, 6.1 en 6.2
* Is er ondersteuning toegevoegd voor de volgende Linux-besturingssystemen
  * Red Hat Enterprise Linux (RHEL) 7.0, 7.1 en 7.2
  * CentOS 7.0, 7.1 en 7.2
  * Red Hat Enterprise Linux (RHEL) 6,8
  * CentOS 6,8

> [!NOTE]
> RHEL/CentOS 7 64-bits **InMage_UA_8.0.1.0_RHEL7-64_GA_06Oct2016_release.tar.gz** wordt verpakt met base Scout GA pakket **InMage_Scout_Standard_8.0.1 GA.zip**. Download Scout GA pakket van de portal, zoals vermeld in [stap 1](#step-1-create-a-vault).
>
>

**Oplossingen voor problemen en verbeteringen**

* Verbeterde verwerking voor de volgende Linux OSes en klonen tooprevent problemen ongewenste opnieuw synchroniseren is afgesloten.
  * Red Hat Enterprise Linux (RHEL) 6.x
  * Oracle Linux (OL) 6.x
* Machtigingen in de map voor installatie van unified agent nu zijn toegang tot een volledige map beperkt voor Linux alleen toohello lokale gebruiker.
* In Windows geladen probleem time-out tijdens het uitgeven van de algemene gedistribueerde consistentie bladwijzer sterk op gedistribueerde toepassingen zoals SQL en SharePoint-clusters.
* Toegevoegde logboek gerelateerde herstellen in base CX-installatieprogramma.
* VMware vCLI 6.0 downloadkoppeling tooWindows hoofddoel base installatieprogramma toegevoegd.
* Meer controle en logboeken voor wijzigingen in het netwerk configuraties tijdens failover en Noodherstel zoomt toegevoegd.
* Sometime bewaren informatie is niet gemeld toohello CX.  
* Voor fysieke cluster mislukt volume bewerking formaat wijzigen via de wizard vContinuum bij het volume verkleinen van bron is opgetreden.
* Cluster-beveiliging is mislukt met fout 'Is mislukt voor toofind Hallo schijfhandtekening' wanneer clusterschijf PRDM schijf is.
* cxps transport server vastlopen vanwege uitzondering van buiten het bereik.
* Servernaam en IP-kolommen zijn nu formaat kunt wijzigen in push installeren pagina van de vContinuum-wizard.
* RX API-uitbreidingen
  * Biedt de vijf meest recente beschikbare algemene consistentiepunten (alleen gegarandeerd-tags).
  * Biedt de details van de capaciteit en beschikbare ruimte voor alle beveiligde apparaten Hallo.
  * Biedt Scout stuurprogramma status op de bronserver.

> [!NOTE]
> * **InMage_Scout_Standard_8.0.1_GA.zip** base pakket heeft nu bijgewerkte CX base installatieprogramma **InMage_CX_8.0.1.0_Windows_GA_26Feb2015_release.exe** en base hoofddoel Windows-installatieprogramma **InMage_ Scout_vContinuum_MT_8.0.1.0_Windows_GA_26Feb2015_release.exe**. Gebruik voor alle nieuwe installatie nieuwe CX- en Windows-hoofddoel GA-bits.
> * Update 4 rechtstreeks kan worden toegepast op 8.0.1 algemene beschikbaarheid.
> * Hallo configuratieserver en RX updates kunnen niet worden hersteld nadat deze worden toegepast op Hallo-systeem.
>
>

### <a name="azure-site-recovery-scout-801-update-3"></a>Azure Site Recovery Scout 8.0.1 Update 3
Update 3 omvat Hallo volgende oplossingen voor problemen en verbeteringen:

* Hallo configuratieserver mislukt RX en tooregister toohello Site Recovery-kluis wanneer ze achter Hallo proxy.
* Hallo aantal uren dat Hallo beoogd herstelpunt (RPO) wordt niet voldaan is niet bijgewerkt in het statusrapport Hallo.
* Hallo configuratieserver wordt niet gesynchroniseerd met RX wanneer Hallo ESX hardwaregegevens of netwerkdetails UTF-8 tekens bevatten.
* Windows Server 2008 R2-domeincontrollers mislukken tooboot na het herstel.
* Offlinesynchronisatie werkt niet zoals verwacht.
* Na een failover van de virtuele machine (VM), verwijderen van een replicatie-paar opgehaald vastgelopen in Hallo CX UI gedurende een lange periode en gebruikers geen Hallo failback voltooien of hervatten is.
* Algemene van de momentopname die worden uitgevoerd door Hallo consistentietaak zijn geoptimaliseerd toohelp beperken toepassingen zoals SQL-clients verbroken.
* Hallo-prestaties van Hallo consistentie hulpprogramma (VACP.exe) is doordat Hallo geheugengebruik dat is vereist voor het maken van momentopnamen op Windows verbeterd.
* Hallo push installeren service loopt vast als Hallo wachtwoord is groter dan 16 tekens.
* vContinuum is niet controleren en te vragen om nieuwe vCenter referenties wanneer Hallo referenties worden gewijzigd.
* Op Linux, is Hallo hoofddoel Cachebeheer (cachemgr) niet downloaden van bestanden vanaf de processerver hello, wat tot replicatie paar beperking leidt.
* Wanneer Hallo fysieke failover cluster (MSCS)-schijf volgorde Hallo dezelfde niet op alle knooppunten van het Hallo is, wordt replicatie is niet ingesteld voor een aantal Hallo clustervolumes.
  <br/>Houd er rekening mee dat cluster Hallo moet toobe opnieuw beveiligd tootake profiteren van deze oplossing.  
* SMTP-functionaliteit werkt niet zoals verwacht als RX van Scout 7.1 tooScout 8.0.1 is bijgewerkt.
* Meer statistieken zijn toegevoegd in logboek Hallo Hallo terugdraaien bewerking tootrack Hallo tijd heeft geduurd toocomplete deze.
* Is er ondersteuning toegevoegd voor Linux-besturingssystemen op de bronserver Hallo:
  * Red Hat Enterprise Linux (RHEL) 6 update 7
  * 6 van centOS bijwerken 7
* Hallo CX en RX-gebruikersinterface kan nu Hallo melding weergeven voor Hallo-paar probeert het bitmapmodus.
* Hallo zijn volgende beveiligingsproblemen toegevoegd in RX:

| **Beschrijving van probleem** | **Procedures voor implementatie** |
| --- | --- |
| Autorisatie via parameter knoeien overslaan |Van toepassing toonon gebruikers met beperkte toegang. |
| Aanvraagvervalsing op meerdere sites |Geïmplementeerde Hallo pagina token concept, waardoor willekeurig gegenereerd voor elke pagina. <br/>Hiermee ziet u het: <li> Er is slechts één aanmelden exemplaar voor Hallo dezelfde gebruiker.</li><li>Pagina vernieuwen werkt niet--het toohello dashboard worden omgeleid.</li> |
| Schadelijk bestand uploaden |Beperkte bestanden toocertain uitbreidingen. Extensies zijn toegestaan: 7z, aiff, AVP avi, bmp, csv, document, docx, fla, FLV-, gif, gz, gzip, JPEG-, jpg, logboek mid mov, mp3, mp4, mpc, mpeg, mpg, ods odt, PDF-, png, ppt, pptx, pxd, qt, ram, rar, DB, rmi, rmvb, RTF-, sdc, sitd, swf, sxc, sxw, tar , tgz, tif-, TIFF-, txt, vsd, wav, wma, wmv, xls, xlsx, xml en zip. |
| Permanente cross-site scripting |Input-validaties toegevoegd. |

> [!NOTE]
> * Alle Site Recovery-updates zijn cumulatief. Update 3 heeft alle Hallo correcties van Update 1 en 2 van de Update. Update 3 kan rechtstreeks worden toegepast op 8.0.1 algemene beschikbaarheid.
> * Hallo configuratieserver en RX updates kunnen niet worden hersteld nadat deze worden toegepast op Hallo-systeem.
>
>

### <a name="azure-site-recovery-scout-801-update-2-update-03dec15"></a>Azure Site Recovery Scout 8.0.1 Update 2 (03 december 15 Update)
Verbeteringen in Update 2 zijn onder andere:

* **Configuratieserver**: oplossing voor een probleem dat Hallo 31 dagen gratis softwarelicentiecontrole functie niet werken zoals verwacht wanneer hello configuratieserver is geregistreerd in Site Recovery.
* **Unified agent**: oplossing voor een probleem in Update 1 dat heeft geresulteerd in Hallo-update niet wordt geïnstalleerd op de hoofddoelserver Hallo wanneer deze is bijgewerkt van versie 8.0 too8.0.1.

### <a name="azure-site-recovery-scout-801-update-1"></a>Azure Site Recovery Scout 8.0.1 Update 1
Update 1 omvat Hallo volgende oplossingen voor problemen en nieuwe functies:

* 31 dagen van gratis bescherming per serverexemplaar. Hiermee kunt u tootest functionaliteit of stel een bewijs van concept.
  * Alle bewerkingen op Hallo-server, inclusief failover en failback zijn gratis voor Hallo eerste 31 dagen, vanaf Hallo-tijd die een server wordt eerst met Site Recovery Scout beveiligd.
  * Van Hallo 32nd dag en hoger, elke beveiligde server brengt snelheid Hallo standaard exemplaar voor Azure Site Recovery-beveiliging tooa klant die eigendom zijn van site.
  * Hallo aantal beveiligde servers die zijn momenteel in rekening worden gebracht is op elk gewenst moment beschikbaar op de dashboardpagina Hallo van hello Azure Site Recovery-kluis.
* Ondersteuning toegevoegd voor vSphere opdrachtregelinterface (vCLI) 5.5 Update 2.
* Ondersteuning toegevoegd voor Linux-besturingssystemen op de bronserver Hallo:
  * RHEL 6 Update 6
  * RHEL 5 11 bijwerken
  * CentOS 6 Update 6
  * CentOS 5 Update 11
* Oplossingen voor problemen tooaddress Hallo problemen te volgen:
  * Registratie van de kluis is mislukt voor de configuratieserver Hallo of RX-server.
  * Clustervolumes niet zoals verwacht wanneer de geclusterde virtuele machines worden opnieuw beveiligd wanneer ze weer.
  * Failback mislukt wanneer het Hallo-hoofddoelserver wordt gehost op een andere server ESXi van Hallo on-premises productie virtuele machines.
  * Bestandsmachtigingen configuratie worden gewijzigd wanneer u een upgrade too8.0.1 die van invloed op beveiliging en bewerkingen.
  * Hallo hersynchronisatie drempelwaarde niet afgedwongen zoals verwacht, wat resulteert tooinconsistent replicatie gedrag.
  * Hallo RPO-instellingen worden niet correct weergegeven in serverinterface Hallo-configuratie. Hallo ongecomprimeerde gegevenswaarde geeft ten onrechte Hallo gecomprimeerd waarde.
  * Hallo verwijderbewerking verwijdert niet zoals verwacht in Hallo vContinuum wizard en replicatie van serverinterface Hallo-configuratie is niet verwijderd.
  * In de wizard vContinuum Hallo Hallo schijf is automatisch uitgeschakeld wanneer u klikt op **Details** in Hallo schijf weergave tijdens het beveiligen van MSCS virtuele machines.
  * Tijdens het Hallo fysiek naar virtueel (P2V)-scenario is niet vereist HP-services, zoals CIMnotify en CqMgHost, verplaatste toomanual bij het herstellen van de virtuele machine. Dit leidt tot extra opstarten.
  * Beveiliging van Linux virtuele machine mislukt wanneer er meer dan 26 schijven op de hoofddoelserver Hallo zijn.

## <a name="next-steps"></a>Volgende stappen
Na de eventuele vragen die u op Hallo hebt [Azure Recovery Services-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).
