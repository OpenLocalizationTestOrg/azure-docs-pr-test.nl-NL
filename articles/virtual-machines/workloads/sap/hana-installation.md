---
title: aaaInstall SAP HANA op SAP HANA in Azure (grote exemplaren) | Microsoft Docs
description: Hoe tooinstall SAP HANA op een SAP HANA in Azure (grote exemplaar).
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b2fe242270a1166cabcfae2f9249a8dd70ff3b93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-sap-hana-large-instances-on-azure"></a>Hoe tooinstall en SAP HANA (grote exemplaren) configureren in Azure

Hieronder vindt u enkele belangrijke definities tooknow voordat u deze handleiding leest. In [SAP HANA (grote exemplaren) overzicht en architectuur op Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) er zijn twee verschillende soorten HANA grote exemplaar eenheden met geïntroduceerd:

- S72, S72m S144, S144m, S192 en S192m die we tooas Hallo 'Type ik klasse' verwijzen van SKU's.
- S384, S384m S384xm, S576, S768 en S960 die we verwijzen tooas Hallo Type II klasse van SKU's.

Hallo-klasse-aanduiding is momenteel toobe in Hallo HANA grote exemplaar documentatie tooeventually verwijzen toodifferent mogelijkheden en vereisten op basis van HANA grote exemplaar SKU's gebruikt.

Er zijn andere definities die wordt vaak gebruikt:
- **Grote exemplaar stempel:** een hardware-infrastructuur stack die SAP HANA TDI gecertificeerd en specifiek toorun SAP HANA-exemplaren in Azure.
- **SAP HANA in Azure (grote exemplaren):** officiële taal voor de aanbieding Hallo in Azure toorun HANA-exemplaren in op SAP HANA TDI gecertificeerde hardware die wordt geïmplementeerd in grote exemplaar stempels in verschillende Azure-regio's. Hallo gerelateerde term **HANA grote exemplaar** kort voor SAP HANA in Azure (grote exemplaren) is en veel deze technische handleiding gebruikt.


Hallo-installatie van de SAP HANA is uw verantwoordelijkheid en u kunt Hallo activiteit starten na de levering van een nieuwe SAP HANA op Azure (grote exemplaren)-server. En nadat het Hallo-connectiviteit tussen uw Azure-VNet(s) en Hallo HANA grote exemplaar eenheid is gevestigd. 

> [!Note]
> Per SAP-beleid, moet de installatie van de Hallo van SAP HANA worden uitgevoerd door een persoon gecertificeerd tooperform SAP HANA-installaties. Een persoon, die is verstreken Hallo gecertificeerd SAP-technologie koppelen examen, SAP HANA installatie certificering, of door een SAP-certificering system integrator (SI).

Controle op opnieuw, vooral bij het plannen van tooinstall HANA 2.0, [SAP ondersteuning Opmerking #2235581 - SAP HANA: ondersteunde besturingssystemen](https://launchpad.support.sap.com/#/notes/2235581/E) in volgorde toomake ervoor dat Hallo OS wordt ondersteund door hello SAP HANA release u tooinstall beslist. Zult u ontdekken dat Hallo ondersteund besturingssysteem voor HANA 2.0 beperkter dan is Hallo voor HANA 1.0 ondersteunde besturingssystemen. 

## <a name="first-steps-after-receiving-hello-hana-large-instance-units"></a>Eerste stappen na de ontvangst van Hallo HANA grote exemplaar eenheid

**Stap 1** na ontvangst Hallo HANA grote exemplaar en zij toegang en connectiviteit toohello exemplaren heeft vastgesteld, tooregister Hallo OS van Hallo-exemplaar met uw OS-provider is. Deze stap omvat het registreren van uw SUSE Linux-besturingssysteem in een exemplaar van SUSE SMT die u nodig hebt toohave geïmplementeerd in een virtuele machine in Azure. Hallo HANA grote exemplaar eenheid kan verbinding maken toothis SMT-exemplaar (Zie verderop in deze documentatie). Of uw besturingssysteem RedHat moet toobe Hello Red Hat abonnement Manager u tooconnect om te moet worden geregistreerd. Zie ook opmerkingen in deze [document](https://docs.microsoft.com/azure/virtual-machines/linux/sap-hana-overview-architecture?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Deze stap is ook nodig toobe kunnen toopatch Hallo OS. Een taak die in de verantwoordelijkheid van de klant Hallo Hallo is. Voor SUSE, documentatie tooinstall is gevonden en configureer SMT [hier](https://www.suse.com/documentation/sles-12/book_smt/data/smt_installation.html).

**Tweede stap** toocheck voor nieuwe patches en verbeteringen van Hallo specifieke release/versie van het besturingssysteem is. Controleer of patchniveau Hallo Hallo HANA grote exemplaar op de meest recente toestand Hallo. Op basis van de timing van de patch/releases en wijzigingen toohello installatiekopie van het besturingssysteem die Microsoft kunt implementeren, kunnen er gevallen waarbij de meest recente patches Hallo niet opgenomen worden kunnen. Daarom is een verplichte stap na een grote exemplaar HANA-eenheid, toocheck overname of patches die relevant zijn voor beveiliging, functionaliteit, beschikbaarheid en prestaties ondertussen zijn uitgegeven door Hallo bepaalde Linux leverancier en toobe toegepast moeten.

**Het derde stap** toocheck uit Hallo relevante SAP opmerkingen is voor het installeren en configureren van SAP HANA op Hallo specifieke release/versie van het besturingssysteem. Vervaldatum toochanging aanbevelingen of wijzigingen tooSAP opmerkingen of configuraties die afhankelijk van afzonderlijke installatiescenario's zijn, Microsoft niet altijd worden kunnen toohave een grote exemplaar HANA eenheid perfect geconfigureerd. Daarom is het noodzakelijk dat u als klant tooread Hallo SAP notities gerelateerde tooSAP HANA op de exacte versie van Linux. Controleer Hallo configuraties van Hallo OS/releaseversie nodig ook en Hallo configuratie-instellingen toepassen waarbij niet is gebeurd.

In specifieke aangepast selectievakje Hallo volgende parameters en uiteindelijk naar:

- NET.Core.rmem_max 16777216 =
- NET.Core.wmem_max 16777216 =
- NET.Core.rmem_default 16777216 =
- NET.Core.wmem_default 16777216 =
- NET.Core.optmem_max 16777216 =
- NET.IPv4.tcp_rmem 65536 16777216 16777216 =
- NET.IPv4.tcp_wmem 65536 16777216 16777216 =

Beginnen met SLES12 SP1 en RHEL 7.2, moeten deze parameters worden ingesteld in een configuratiebestand in Hallo /etc/sysctl.d directory. Bijvoorbeeld, moet een configuratiebestand met de naam van Hallo 91-NetApp-HANA.conf worden gemaakt. Voor oudere versies van SLES en RHEL moet deze parameters set in/etc/sysctl.conf.

Voor alle RHEL vrijgegeven en beginnen met SLES12, Hallo 
- sunrpc.tcp_slot_table_entries = 128

parameter moet worden ingesteld als in/etc/modprobe.d/sunrpc-local.conf. Als het Hallo-bestand niet bestaat, moet het eerst door toe te voegen Hallo na datum gemaakt: 
- Opties voor sunrpc tcp_max_slot_table_entries = 128

**Vierde stap** toocheck Hallo systeemtijd van uw exemplaar van HANA grote eenheid is. Hallo-exemplaren worden geïmplementeerd met een systeemtijdzone die Hallo locatie hello Azure-regio Hallo die HANA grote exemplaar stempel bevindt zich in vertegenwoordigen. U bent gratis toochange Hallo systeemtijd of de tijdzone van Hallo-exemplaren die u bezit. Dit leidt en ordening meer exemplaren in uw tenant, moet u tooadapt Hallo tijdzone Hallo zojuist bezorgd exemplaren worden voorbereid. Microsoft-bewerkingen hebben geen inzichten in Hallo systeemtijdzone dat u instellen met Hallo exemplaren na Hallo overdracht. Daarom geïmplementeerde exemplaren kunnen niet worden ingesteld in Hallo dezelfde tijdzone als Hallo een u gewijzigd in. Als gevolg hiervan is uw verantwoordelijkheid als klant toocheck en zo nodig aan te passen Hallo tijdzone van Hallo instanties afgegeven. 

**Vijfde stap** toocheck etc/hosts is. Hallo blades ophalen afgegeven, hebben ze verschillende IP-adressen toegewezen voor verschillende doeleinden (Zie volgende sectie). Controleer Hallo etc/hosts-bestand. In gevallen waar eenheden zijn toegevoegd aan een bestaande tenant verwacht niet dat toohave etc/hosts van Hallo zojuist geïmplementeerde systemen correct worden beheerd met Hallo IP-adressen van eerder geleverde systemen. Daarom is u als klant toocheck Hallo juiste instellingen, dat een zojuist geïmplementeerde exemplaar kan communiceren en omzetten van namen op Hallo van eerder geïmplementeerde eenheden in uw tenant. 

## <a name="networking"></a>Netwerken
Er wordt ervan uitgegaan dat u Hallo aanbevelingen bij het ontwerpen van uw Azure VNets en verbinding maken met de VNets toohello HANA grote instanties, zoals beschreven in deze documenten gevolgd:

- [Overzicht van de SAP HANA (grote exemplaar) en architectuur op Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)
- [Infrastructuur voor SAP HANA (grote exemplaren) en de verbindingen van Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Er zijn een aantal details waard toomention over netwerken Hallo Hallo één eenheden. Elke eenheid HANA grote exemplaar wordt geleverd met twee of drie IP-adressen die zijn toegewezen tootwo of drie NIC-poorten van Hallo-eenheid. Drie IP-adressen worden gebruikt in HANA scale-out configuraties en Hallo HANA System Replication scenario. Een van de Hallo IP-adressen toegewezen toohello NIC van Hallo eenheid valt buiten het Hallo-Server IP-adresgroep die is beschreven in Hallo [SAP HANA (grote exemplaar) overzicht en architectuur op Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture).

Hallo-distributie voor eenheden met twee IP-adressen toegewezen moet eruitzien als:

- eth0.xx moet een IP-adres toegewezen die buiten het Hallo-Server IP-adresgroepbereik dat u hebt ingediend tooMicrosoft hebben. Dit IP-adres moet worden gebruikt voor het onderhouden van in/etc/hosts Hallo OS.
- eth1.xx moet een IP-adres toegewezen dat wordt gebruikt voor communicatie tooNFS hebben. Daarom deze adressen komen **niet** moet toobe onderhouden in etc/hosts in de volgorde tooallow exemplaar tooinstance verkeer binnen Hallo-tenant.

Een bladeconfiguratie met twee IP-adressen toegewezen is niet geschikt is voor implementatie gevallen van HANA System Replication of HANA scale-out. Als twee IP-adressen toegewezen alleen gelet en toodeploy dergelijke configuratie productiviteitsniveau contact opneemt met SAP HANA op Azure Service Management tooget een derde IP-adressen in een derde toegewezen VLAN. Voor grote exemplaar HANA eenheden met drie IP-adressen toegewezen op drie NIC-poorten, hello gelden volgende gebruiksregels:

- eth0.xx moet een IP-adres toegewezen die buiten het Hallo-Server IP-adresgroepbereik dat u hebt ingediend tooMicrosoft hebben. Dit IP-adres wordt daarom niet worden gebruikt voor het onderhouden van in/etc/hosts Hallo OS.
- eth1.xx moet een IP-adres toegewezen dat wordt gebruikt voor communicatie tooNFS opslag hebben. Dit type adressen moet daarom niet worden beheerd in etc/hosts.
- eth2.xx moet exclusief gebruikte toobe onderhouden in etc/hosts voor de communicatie tussen de verschillende exemplaren Hallo. Deze adressen zou Hallo IP-adressen die toobe blijven IP-adressen die HANA wordt gebruikt voor de configuratie van Hallo tussen knooppunten in scale-out HANA configuraties moeten ook zijn.



## <a name="storage"></a>Storage

Hallo opslagindeling voor SAP HANA in Azure (grote exemplaren) wordt geconfigureerd SAP HANA op Azure Service Management via SAP hulplijnen aanbevolen zoals beschreven in [opslagvereisten voor SAP HANA](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) witboek. ruwe grootte van de andere volumes Hallo Hallo Hello verschillende HANA grote-exemplaren SKU's is beschreven in [SAP HANA (grote exemplaar) overzicht en architectuur op Azure](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

naamgeving van opslagvolumes Hallo Hallo worden vermeld in de volgende tabel Hallo:

| Opslaggebruik | De naam van koppelpunt | Volumenaam | 
| --- | --- | ---|
| HANA gegevens | /Hana/Data/SID/mnt0000<m> | Opslag IP: / hana_data_SID_mnt00001_tenant_vol |
| HANA-logboek | /Hana/log/SID/mnt0000<m> | Opslag IP: / hana_log_SID_mnt00001_tenant_vol |
| HANA logboekback-up | /Hana/log/backups | Opslag IP: / hana_log_backups_SID_mnt00001_tenant_vol |
| HANA gedeeld | /Hana/Shared/SID | Opslag IP: / hana_shared_SID_mnt00001_tenant_vol/gedeeld |
| usr/sap | /usr/SAP/SID | Opslag IP: / hana_shared_SID_mnt00001_tenant_vol/usr_sap |

Waar SID = Hallo HANA instantie systeem-ID 

- En tenantverkeer = van een interne opsomming van bewerkingen bij het implementeren van een tenant.

Zoals u ziet, HANA gedeeld en usr/sap delen Hallo hetzelfde volume. Hallo naamgeving volgt de namen van Hallo quorumbron: omvat Hallo Hallo HANA exemplaren, evenals Hallo mount-nummer van systeem-ID. In implementaties van scale-up alleen is één koppelpunt, zoals mnt00001. Terwijl in scale-out-implementatie u zoveel koppelingen als ziet hebben u worker en master knooppunten. Back-logboekvolumes zijn voor Hallo scale-out-omgeving, gegevens, logboek, gedeelde en gekoppelde tooeach knooppunt in de configuratie van Hallo scale-out. Voor configuraties met meerdere exemplaren van het SAP, is een andere set volumes gemaakt en gekoppelde toohello HAN grote exemplaar eenheid.

Als u Hallo artikel lezen en zoeken van een grote exemplaar HANA-eenheid, zult u ontdekken dat Hallo eenheden worden geleverd met in plaats daarvan vriendelijke schijfvolume HANA/gegevens en dat we een volume HANA/log/back-up hebben. Hallo reden waarom we Hallo HANA/gegevens zo groot grootte is dat Hallo-opslag-momentopnamen we bieden voor u als klant gebruikt dezelfde schijfvolume Hallo. Hallo betekent meer opslag-momentopnamen die u uitvoert, Hallo meer ruimte is verbruikt door momentopnamen in de opslagvolumes toegewezen. Hallo HANA/log/back-volume is niet gedachte toobe Hallo volume tooput databaseback-ups in. Het is formaat toobe gebruikt als back-upvolume voor Hallo HANA transactielogboekback-ups. In toekomstige versies van Hallo opslag snapshot-self service dat we heeft betrekking op deze specifieke volume toohave meer frequente momentopnamen. En met die frequentere replicaties toohello disaster recovery site als u wenst toooption in voor Hallo disaster recovery functionaliteit van Hallo HANA grote exemplaar infrastructuur. Zie voor meer informatie [SAP HANA (grote exemplaren) hoge beschikbaarheid en herstel na noodgevallen op Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 

Bovendien toohello opslag hebt opgegeven, kunt u kopen extra opslagcapaciteit in stappen van 1 TB. Deze extra opslagruimte kan worden toegevoegd als nieuwe volumes tooa HANA grote exemplaren.

Tijdens de voorbereiding met SAP HANA op Azure Service Management Hallo klant Hiermee geeft u een gebruikers-ID (UID) en groep-ID (GID) voor Hallo sidadm gebruiker en een sapsys (ex: 1000,500) is het nodig dat tijdens de installatie van Hallo SAP HANA-systeem, deze dezelfde waarden worden gebruikt. Als u meerdere HANA-exemplaren op een eenheid toodeploy wilt, kunt u meerdere sets van volumes (één ingesteld voor elk exemplaar) ophalen. Als gevolg hiervan moet u tijdens de implementatie toodefine:

- Hallo SID van Hallo verschillende HANA exemplaren (sidadm is buiten deze afgeleid).
- De grootte van het geheugen van Hallo verschillende HANA exemplaren. Aangezien Hallo geheugengrootte per exemplaren Hallo grootte van Hallo volumes in elke set afzonderlijk volume definieert.

Op basis van de provider opslagaanbevelingen Hallo volgend mount-opties zijn geconfigureerd voor alle gekoppelde volumes (met uitzondering van opstarten LUN):

- NFS-rw bergen = 4, hard, timeo = 600, rsize = 1048576, wsize = 1048576, Intro, noatime, vergrendelen 0 0

Deze koppeling punten zijn geconfigureerd in/etc/fstab zoals weergegeven in Hallo afbeeldingen te volgen:

![fstab van gekoppelde volumes in grote exemplaar HANA-eenheid](./media/hana-installation/image1_fstab.PNG)

Hallo-uitvoer van Hallo opdracht df -h op een eenheid S72m HANA grote exemplaar eruit als:

![fstab van gekoppelde volumes in grote exemplaar HANA-eenheid](./media/hana-installation/image2_df_output.PNG)


Hallo opslagcontroller en knooppunten in Hallo grote exemplaar stempels worden gesynchroniseerde tooNTP-servers. Met u Hallo SAP HANA op Azure (grote exemplaren) units en virtuele Azure-machines op een NTP-server te synchroniseren, moet er geen aanzienlijke tijd afwijking gebeurt tussen Hallo-infrastructuur en Hallo compute eenheden in Azure of grote exemplaar stempels.

In volgorde toooptimize SAP HANA toohello opslag onder gebruikt, moet u ook Hallo SAP HANA-configuratieparameters volgende instellen:

- max_parallel_io_requests 128
- async_read_submit op
- async_write_submit_active op
- alle async_write_submit_blocks
 
Voor SAP HANA 1.0-versies van tooSPS12, deze parameters worden ingesteld tijdens de installatie van de Hallo van Hallo SAP HANA-database, zoals beschreven in [SAP Opmerking #2267798 - configuratie van Hallo SAP HANA-Database](https://launchpad.support.sap.com/#/notes/2267798)

U kunt ook Hallo parameters na de installatie van een Hallo SAP HANA-database configureren met behulp van Hallo hdbparam framework. 

Met SAP HANA 2.0, is Hallo hdbparam framework afgeschaft. Hallo-parameters moeten als gevolg hiervan worden ingesteld met behulp van SQL-opdrachten. Zie voor meer informatie [SAP-notitie #2399079: eliminatie van hdbparam in HANA 2](https://launchpad.support.sap.com/#/notes/2399079).


## <a name="operating-system"></a>Besturingssysteem

Wisselruimte Hallo geleverde installatiekopie van het besturingssysteem is ingesteld too2 GB op basis van toohello [SAP ondersteuning Opmerking #1999997 - Veelgestelde vragen over: SAP HANA geheugen](https://launchpad.support.sap.com/#/notes/1999997/E). Alle andere instellen gewenste behoeften toobe ingesteld door u als klant.

[SUSE Linux Enterprise Server 12 SP1 voor SAP-toepassingen](https://www.suse.com/products/sles-for-sap/hana) Hallo distributie van Linux voor SAP HANA in Azure (grote exemplaren) geïnstalleerd is. Deze bepaalde distributie biedt mogelijkheden voor SAP-specifieke &quot;out of box Hallo&quot; (inclusief vooraf ingestelde parameters voor het uitvoeren van de SAP effectief op SLES).

Zie [Resource bibliotheek/White Papers](https://www.suse.com/products/sles-for-sap/resource-library#white-papers) op Hallo SUSE website en [SAP op SUSE](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE) op Hallo SAP Community netwerk (SCN) voor verschillende nuttige informatiebronnen toodeploying SAP HANA op SLES (inclusief Hallo instellen verwante van hoge beschikbaarheid, beveiligingsbewerkingen hardening specifieke tooSAP en meer).

Aanvullende en nuttige SAP op SUSE-gerelateerde koppelingen:

- [SAP HANA op SUSE Linux Site](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE)
- [Best Practice voor SAP: in de wachtrij plaatsen replicatie – SAP NetWeaver op SUSE Linux Enterprise 12](https://www.suse.com/docrepcontent/container.jsp?containerId=9113).
- [ClamSAP – SLES virusbeveiliging voor SAP](http://scn.sap.com/community/linux/blog/2014/04/14/clamsap--suse-linux-enterprise-server-integrates-virus-protection-for-sap) (inclusief SLES 12 voor SAP-toepassingen).

SAP-opmerkingen bij de ondersteuning van toepassing tooimplementing SAP HANA op SLES 12:

- [SAP ondersteuning Opmerking #1944799 – SAP HANA richtlijnen voor de installatie van het besturingssysteem SLES](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html).
- [SAP ondersteuning Opmerking #2205917 – SAP HANA DB aanbevolen OS-instellingen voor SLES 12 voor SAP-toepassingen](https://launchpad.support.sap.com/#/notes/2205917/E).
- [SAP ondersteuning Opmerking #1984787 – SUSE Linux Enterprise Server 12: Opmerkingen bij de installatie van de](https://launchpad.support.sap.com/#/notes/1984787).
- [SAP ondersteuning Opmerking #171356 – SAP-Software op Linux: algemene informatie](https://launchpad.support.sap.com/#/notes/1984787).
- [SAP ondersteuning Opmerking #1391070 – Linux UUID oplossingen](https://launchpad.support.sap.com/#/notes/1391070).

[Red Hat Enterprise Linux voor SAP HANA](https://www.redhat.com/en/resources/red-hat-enterprise-linux-sap-hana) is een andere aanbieding voor SAP HANA uitgevoerd op grote HANA-exemplaren. Releases van RHEL 6.7 en 7.2 zijn beschikbaar. 

Aanvullende en nuttige SAP op Red Hat verwante koppelingen:
- [SAP HANA op Red Hat Linux Site](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+Red+Hat).

Opmerkingen bij de ondersteuning van toepassing tooimplementing SAP HANA op Red Hat SAP:

- [SAP ondersteuning Opmerking #2009879 - SAP HANA richtlijnen voor het Red Hat Enterprise Linux (RHEL)-besturingssysteem](https://launchpad.support.sap.com/#/notes/2009879/E).
- [SAP ondersteuning Opmerking #2292690 - SAP HANA-database: OS aanbevolen instellingen voor RHEL 7](https://launchpad.support.sap.com/#/notes/2292690).
- [SAP ondersteuning Opmerking #2247020 - SAP HANA-database: OS aanbevolen instellingen voor RHEL 6.7](https://launchpad.support.sap.com/#/notes/2247020).
- [SAP ondersteuning Opmerking #1391070 – Linux UUID oplossingen](https://launchpad.support.sap.com/#/notes/1391070).
- [SAP ondersteuning Opmerking #2228351 - Linux: SAP HANA-Database SP's 11 revisie 110 (of hoger) op de RHEL 6 of SLES 11](https://launchpad.support.sap.com/#/notes/2228351).
- [#2397039 - Veelgestelde vragen over SAP ondersteuning Opmerking: SAP-op de RHEL](https://launchpad.support.sap.com/#/notes/2397039).
- [SAP ondersteuning Opmerking #1496410 - Red Hat Enterprise Linux 6.x: installatie en Upgrade](https://launchpad.support.sap.com/#/notes/1496410).
- [SAP ondersteuning Opmerking #2002167 - Red Hat Enterprise Linux 7.x: installatie en Upgrade](https://launchpad.support.sap.com/#/notes/2002167).

## <a name="time-synchronization"></a>Tijdsynchronisatie

SAP-toepassingen die zijn gebaseerd op Hallo SAP NetWeaver architectuur zijn gevoelig voor tijdsverschil voor hello bestaat uit verschillende onderdelen Hallo SAP-systeem. SAP ABAP korte dumpen met Hallo fouttitel van ZDATE\_grote\_tijd\_DIFF zijn waarschijnlijk vertrouwd, zoals deze korte dumpbestanden weergegeven wanneer hello systeemtijd van de andere servers of virtuele machines te ver uit elkaar is verhuizen.

Voor SAP HANA in Azure (grote exemplaren) uitgevoerd in Azure heeft &#39; tijdsynchronisatie toepassing t toohello compute eenheden in Hallo grote exemplaar stempels. Deze synchronisatie is niet van toepassing voor het uitvoeren van SAP-toepassingen in systeemeigen Azure VM's, zoals Azure zorgt ervoor een systeem & #39 dat; s tijd juist is gesynchroniseerd. Een afzonderlijke tijd server moet worden ingesteld die kan worden gebruikt door toepassingsservers SAP uitgevoerd op Azure VM's en Hallo SAP HANA-database als gevolg hiervan instanties die worden uitgevoerd op grote HANA-exemplaren. Hallo opslaginfrastructuur in grote exemplaar stempels is tijd die zijn gesynchroniseerd met NTP-servers.

## <a name="setting-up-smt-server-for-suse-linux"></a>SMT-server instellen voor SUSE Linux
SAP HANA grote exemplaren hebben geen directe verbinding toohello Internet. Daarom is niet een eenvoudig tooregister eenheid met Hallo OS-provider en toodownload en patches toepassen. In geval van SUSE Linux Hallo mogelijk een oplossing tooset van een SMT-server in een Azure VM. Terwijl hello Azure VM moet toobe gehost in een Azure VNet dat is verbonden toohello HANA grote exemplaar. Met dergelijke een SMT-server, kan Hallo HANA grote exemplaar eenheid registreren en patches te downloaden. 

SUSE biedt een uitgebreidere handleiding op hun [abonnement beheerprogramma voor SLES 12 SP2](https://www.suse.com/documentation/sles-12/pdfdoc/book_smt/book_smt.pdf). 

Als de voorwaarde voor de installatie van een SMT-server die voldoet aan de taak Hallo voor grote exemplaar HANA Hallo moet:

- Een Azure-VNet dat is verbonden toohello HANA grote exemplaar ER circuit.
- Een SUSE-account dat is gekoppeld aan een organisatie. Terwijl het Hallo-organisatie moet toohave sommige geldig SUSE-abonnement.

### <a name="installation-of-smt-server-on-azure-vm"></a>Installatie van SMT-server op Azure VM

In deze stap installeert u Hallo SMT-server in een Azure VM. de eerste eenheid Hallo is toolog in toohello [SUSE Customer Center](https://scc.suse.com/)

Als u bent aangemeld, gaat u tooOrganization--> referenties van de organisatie. In deze sectie zult u Hallo-referenties die nodig zijn tooset Hallo SMT-server zijn.

de derde stap Hallo is tooinstall een SUSE Linux VM in hello Azure VNet. toodeploy hello VM, nemen de installatiekopie van een SLES 12 SP2 galerie van Azure. In het implementatieproces Hallo een DNS-naam niet gedefinieerd en gebruik geen statische IP-adressen zoals in deze schermafbeelding te maken

![VM-implementatie voor SMT-server](./media/hana-installation/image3_vm_deployment.png)

Hallo geïmplementeerde virtuele machine een kleinere VM is en kreeg Hallo interne IP-adres in hello Azure VNet van 10.34.1.4. Naam van Hallo VM is smtserver. Na de installatie Hallo is Hallo connectiviteit toohello HANA grote exemplaar eenheid gecontroleerd. Afhankelijk van hoe u naamomzetting geordend moet u mogelijk tooconfigure resolutie van Hallo HANA grote exemplaar eenheden in etc/hosts Hallo Azure VM. Voeg een extra schijf toohello VM die u toobe toohold Hallo patches gebruikt. Hallo-opstartschijf zelf mogelijk te klein. Hallo-schijf is in geval van Hallo gedemonstreerd, gekoppelde te/srv/www/htdocs zoals weergegeven in de volgende schermafbeelding Hallo. Er moet een schijf van 100 GB voldoende.

![VM-implementatie voor SMT-server](./media/hana-installation/image4_additional_disk_on_smtserver.PNG)

Toohello HANA grote exemplaar eenheid aanmelden, / etc/hosts onderhouden en controleren of u hello Azure virtuele machine die toorun Hallo SMT-server via Hallo netwerk hoort kunt bereiken.

Nadat deze controle is voltooid, moet u toolog in toohello Azure virtuele machine die Hallo SMT-server moet worden uitgevoerd. Als u putty toolog in toohello VM gebruikt, moet u op tooexecute deze reeks opdrachten in het venster bash:

```
cd ~
echo "export NCURSES_NO_UTF8_ACS=1" >> .bashrc
```

Start na het uitvoeren van deze opdrachten opnieuw uw bash tooactivate Hallo-instellingen. Start vervolgens YAST.

Ga in de YAST, tooSoftware onderhoud en zoek naar smt. Selecteer smt schakelt automatisch tooyast2 smt zoals hieronder wordt weergegeven

![SMT in yast](./media/hana-installation/image5_smt_in_yast.PNG)


Hallo selectie voor installatie op Hallo smtserver accepteren. Zodra geïnstalleerd, gaat u toohello SMT-serverconfiguratie en Hallo organisatie referenties invoeren van Hallo SUSE Customer Center die u eerder hebt opgehaald. Ook uw Azure VM-hostnaam als Hallo SMT Server-URL invoeren. In deze demonstratie was https://smtserver zoals weergegeven in de volgende afbeeldingen Hallo.

![Configuratie van SMT-server](./media/hana-installation/image6_configuration_of_smtserver1.png)

Volgende stap moet u tootest of Hallo verbinding toohello SUSE Customer Center werkt. Zoals u ziet in Hallo volgende afbeeldingen, in geval van de demonstratie hello, het werkt.

![Test tooSUSE Customer Center verbinding maken](./media/hana-installation/image7_test_connect.png)

Eenmaal Hallo SMT setup wordt gestart, moet u een wachtwoord tooprovide. Omdat het een nieuwe installatie, moet u toodefine dat wachtwoord zoals weergegeven in de volgende afbeeldingen Hallo.

![Wachtwoord voor de database definiëren](./media/hana-installation/image8_define_db_passwd.PNG)

Hallo volgende interactie die u hebt is wanneer een certificaat wordt gemaakt. Ga via Hallo dialoogvenster zoals volgende en Hallo stap moet worden voortgezet.

![Certificaat voor SMT-server maken](./media/hana-installation/image9_certificate_creation.PNG)

Er zijn mogelijk enkele minuten gespendeerd aan het Hallo-stap van "Controle uitvoeren synchronisatie" achter Hallo Hallo-configuratie. Na het Hallo-installatie en configuratie van Hallo SMT-server, zult u Hallo directory opslagplaats onder Hallo koppelpunt punt /srv/www/htdocs/plus een aantal submappen onder de opslagplaats. 

Hallo SMT-server en de verwante services met de volgende opdrachten opnieuw gestart.

```
rcsmt restart
systemctl restart smt.service
systemctl restart apache2
```

### <a name="download-of-packages-onto-smt-server"></a>Tijdens het downloaden van pakketten naar SMT-server

Nadat alle hello services opnieuw worden gestart, selecteer Hallo juiste pakketten in SMT-beheer met behulp van Yast. selectie van het pakket Hallo is afhankelijk van de besturingssysteemkopie Hallo Hallo HANA grote van server met exemplaar en niet Hallo SLES release of versie van Hallo VM waarop Hallo SMT server. Een voorbeeld van Hallo selectiescherm worden hieronder weergegeven.

![Pakketten selecteren](./media/hana-installation/image10_select_packages.PNG)

Zodra u klaar met selectie van het pakket hello bent, moet u toostart Hallo initiële kopie van Hallo Selecteer pakketten toohello SMT server die u ingesteld. Dit exemplaar is geactiveerd in Hallo-shell met Hallo-opdracht smt-mirror zoals hieronder wordt weergegeven


![Pakketten tooSMT server downloaden](./media/hana-installation/image11_download_packages.PNG)

Als u hierboven ziet, moeten hello-pakketten naar Hallo-mappen die zijn gemaakt onder Hallo koppelpunt punt /srv/www/htdocs ophalen gekopieerd. Dit kan even duren. Afhankelijk van hoeveel pakketten die u selecteert, het kan duren tooone uur of langer.
Als dit proces is voltooid, moet u toomove toohello SMT-clientinstallatie. 

### <a name="set-up-hello-smt-client-on-hana-large-instance-units"></a>Hallo SMT-client op grote exemplaar HANA eenheden ingesteld

Hallo client (s) zijn in dit geval Hallo HANA grote exemplaar eenheden. setup van SMT Hallo Hallo script clientSetup4SMT.sh naar hello Azure VM gekopieerd. Script via toohello HANA grote exemplaar eenheid u tooconnect tooyour SMT-server wilt kopiëren. Hallo script starten met de Hallo -h optie en geeft dit als parameter Hallo-naam van uw SMT-server. In dit voorbeeld smtserver.

![SMT-client configureren](./media/hana-installation/image12_configure_client.PNG)

Er is mogelijk een scenario waarbij hello laden van het certificaat van de server door de client Hallo HALLO hallo is voltooid, maar Hallo-registratie mislukt zoals hieronder wordt weergegeven.

![De registratie van de client is mislukt](./media/hana-installation/image13_registration_failed.PNG)

Als het Hallo-registratie is mislukt, leest u dit [SUSE ondersteunen document](https://www.suse.com/de-de/support/kb/doc/?id=7006024) en Hallo stappen er uit te voeren.

> [!IMPORTANT] 
> Als de servernaam van de moet u tooprovide Hallo naam van de VM, Hallo in deze case smtserver, zonder Hallo volledig gekwalificeerde domeinnaam. NET Hallo VM naam werkt. 

Nadat u deze stappen zijn uitgevoerd, moet u tooexecute Hallo volgende opdracht op Hallo HANA grote exemplaar eenheid

```
SUSEConnect –cleanup
```

> [!Note] 
> In onze tests hebben altijd we toowait een paar minuten na deze stap. Hallo clientSetup4SMT.sh direct worden uitgevoerd, nadat hello corrigerende maatregelen in artikel SUSE Hallo beschreven is beëindigd met dat Hallo-certificaat niet geldig nog berichten. Meestal 5-10 minuten wachten en het uitvoeren van clientSetup4SMT.sh beëindigd in een geslaagde clientconfiguratie.

Als u in Hallo probleem dat u toofix op basis van Hallo stappen van Hallo SUSE artikel nodig hebt uitgevoerd, moet u toorestart clientSetup4SMT.sh op Hallo HANA grote exemplaar eenheid opnieuw. Nu het moet worden voltooid zoals hieronder wordt weergegeven.

![Clientregistratie is geslaagd](./media/hana-installation/image14_finish_client_config.PNG)

Met deze stap maakt u Hallo SMT-client van Hallo HANA grote exemplaar eenheid tooconnect tegen Hallo SMT server die u hebt geïnstalleerd in hello Azure VM geconfigureerd. U kunt nu 'zypper up' of 'zypper in' tooinstall OS patches duren tooHANA grote exemplaren of extra pakketten installeren. Ervan wordt uitgegaan dat u alleen patches die u hebt gedownload krijgen kunt voordat op Hallo SMT-server.


## <a name="example-of-an-sap-hana-installation-on-hana-large-instances"></a>Voorbeeld van een SAP HANA-installatie op grote HANA-exemplaren
Deze sectie ziet u hoe tooinstall SAP HANA op een grote exemplaar HANA-eenheid. we hebben de status van de Hallo start eruitzien als:

- U hebt opgegeven Microsoft alle Hallo gegevens toodeploy u een grote SAP HANA-exemplaar.
- U ontvangen Hallo SAP HANA grote exemplaar van Microsoft.
- U hebt een Azure VNet dat is verbonden tooyour on-premises netwerk gemaakt.
- U Hallo ExpressRotue circuit voor grote exemplaren HANA toohello verbonden hetzelfde Azure VNet.
- U hebt een Azure VM u als een korte inleiding voor grote exemplaren HANA gebruiken geïnstalleerd.
- U hebt aangebracht of dat u verbinding van Hallo jump vak tooyour HANA grote exemplaar eenheid en vice versa maken kunt.
- U hebt gecontroleerd of alle vereiste pakketten Hallo en patches worden geïnstalleerd.
- U leest Hallo SAP opmerkingen en documentatie over de installatie HANA op Hallo besturingssysteem u gebruikt en ervoor hebt gezorgd dat Hallo HANA release van keuze op Hallo OS-versie wordt ondersteund.

Wat wordt weergegeven in de volgende reeksen Hallo is Hallo downloaden van Hallo HANA Setup pakketten toohello korte inleiding in VM, in dit geval wordt uitgevoerd op een Windows-besturingssysteem, Hallo kopie van hello-pakketten toohello HANA grote exemplaar eenheid en Hallo reeks Hallo setup.

### <a name="download-of-hello-sap-hana-installation-bits"></a>Het downloaden van de Hallo SAP HANA installatie bits
Aangezien Hallo HANA grote exemplaar eenheden geen directe verbinding toohello internet, u niet rechtstreeks downloaden Hallo installatiepakketten van toohello SAP HANA grote exemplaar VM. tooovercome hello ontbrekende directe verbinding met internet, moet u Hallo jump vak. U downloaden hello-pakketten toohello jump vak VM.

In de volgorde toodownload Hallo HANA installatiepakketten moet u een SAP-S-gebruiker of een andere gebruiker, waardoor u tooaccess Hallo SAP Marketplace. Deze reeks schermen doorlopen na het aanmelden:

Ga te[SAP Service Marketplace](https://support.sap.com/en/index.html) > Software downloaden klikt u op >-installaties en -Upgrade > alfabetische Index > onder H – SAP HANA Platform editie > SAP HANA Platform Edition 2.0 > installatie > downloaden Hallo volgende bestanden

![HANA installatie downloaden](./media/hana-installation/image16_download_hana.PNG)

In geval van de demonstratie hello, hebben we installatiepakketten voor SAP HANA 2.0 gedownload. Vouw op Hallo Azure jump vak VM Hallo zelfuitpakkend archieven in Hallo directory zoals hieronder wordt weergegeven.

![Pak HANA installatie](./media/hana-installation/image17_extract_hana.PNG)

Wanneer het Hallo-archieven zijn uitgepakt, kopieert u Hallo directory gemaakt door Hallo extraheren in geval van Hallo hierboven 51052030, toohello HANA grote exemplaar eenheid Hallo /hana/shared volume in een map die u hebt gemaakt.

> [!Important]
> Geen Hallo installatiepakketten kopiëren naar de hoofdmap Hallo of LUN omdat ruimte beperkt is en toobe gebruikt door andere processen ook moet worden opgestart.


### <a name="install-sap-hana-on-hello-hana-large-instance-unit"></a>SAP HANA op Hallo HANA grote exemplaar eenheid installeren
In de volgorde tooinstall SAP HANA moet u toolog in als de hoofdmap van de gebruiker. Alleen hoofdmap heeft onvoldoende machtigingen tooinstall SAP HANA.
Hallo Allereerst moet u toodo is tooset machtigingen op Hallo directory die u gekopieerd naar/hana/gedeeld. Hallo-machtigingen nodig tooset zoals

```
chmod –R 744 <Installation bits folder>
```

Als u wilt dat tooinstall SAP HANA Hallo grafische setup gebruikt, Hallo gtk2 pakket behoeften toobe op Hallo HANA grote exemplaren geïnstalleerd. Controleer of deze is geïnstalleerd met Hallo-opdracht

```
rpm –qa | grep gtk2
```

We zijn Hallo SAP HANA-instelling met de grafische gebruikersinterface Hallo demonstreren in verdere stappen. Volgende stap gaat u naar de installatiemap Hallo en navigeer naar Hallo sub directory HDB_LCM_LINUX_X86_64. Starten

```
./hdblcmgui 
```
buiten-map. Nu ophalen u door geleid een reeks schermen waar u tooprovide Hallo gegevens nodig voor Hallo-installatie. In geval van Hallo gedemonstreerd, zijn we Hallo SAP HANA-database-server en de Hallo SAP HANA-clientonderdelen geïnstalleerd. Onze selectie is daarom 'SAP HANA-Database, zoals hieronder wordt weergegeven

![Selecteer HANA in installatie](./media/hana-installation/image18_hana_selection.PNG)

In het volgende scherm hello optie Hallo nieuw systeem installeren

![Selecteer de nieuwe installatie HANA](./media/hana-installation/image19_select_new.PNG)

Na deze stap moet u tooselect tussen verschillende extra onderdelen die verder kunnen worden geïnstalleerd toohello SAP HANA-database-server.

![Aanvullende HANA onderdelen selecteren](./media/hana-installation/image20_select_components.PNG)

Voor Hallo doel van deze documentatie, we gekozen Hallo SAP HANA-Client en Hallo SAP HANA Studio. We ook een scale-up-exemplaar geïnstalleerd. in het volgende scherm hello moet u daarom toochoose één Host-systeem 

![Selecteer de installatie van de scale-up](./media/hana-installation/image21_single_host.PNG)

In het volgende scherm hello moet u tooprovide sommige gegevens

![Geef SAP HANA-SID](./media/hana-installation/image22_provide_sid.PNG)

> [!Important]
> Als HANA systeem-ID (SID), moet u tooprovide Hallo dezelfde SID als u Microsoft wanneer u besteld Hallo HANA grote exemplaar implementatie. Een andere SID is Hallo installatie mislukken vanwege problemen met machtigingen op verschillende volumes Hallo tooaccess

Als de installatiemap u Hallo /hana/shared directory. In de volgende stap hello moet u tooprovide Hallo locaties voor Hallo HANA gegevensbestanden en Hallo HANA-logboekbestanden


![Geef de locatie van de HANA-logboek](./media/hana-installation/image23_provide_log.PNG)

> [!Note]
> U moet definiëren als gegevens en logboekbestanden Hallo volumes die al bij Hallo koppelpunten die Hallo SID die u hebt gekozen in Hallo scherm selectie voordat dit scherm bevatten. Als Hallo beveiligings-id niet overeen met Hallo een u hebt getypt, in het welkomstscherm voordat, gaat u terug en Hallo SID toohello-waarde op Hallo koppelpunten.

In de volgende stap Hallo, bekijk Hallo-hostnaam en uiteindelijk te corrigeren. 

![De hostnaam controleren](./media/hana-installation/image24_review_host_name.PNG)

In de volgende stap hello moet u ook tooretrieve gegevens u tooMicrosoft is opgegeven toen u besteld Hallo HANA grote exemplaar implementatie. 

![Geef systeemgebruiker UID en GID](./media/hana-installation/image25_provide_guid.PNG)

> [!Important]
> U moet tooprovide Hallo dezelfde gebruikers-ID van systeem en ID van de groep van de gebruiker u bedoelde Microsoft u Hallo eenheid implementatie rangschikken. Als u zeer toogive Hallo mislukken wordt dezelfde id's, installatie van de Hallo van SAP HANA op Hallo HANA grote exemplaar eenheid mislukt.

In de volgende twee schermen hello, die we niet zichtbaar zijn in deze documentatie, moet u tooprovide Hallo wachtwoord voor de systeemgebruiker Hallo van Hallo SAP HANA-database en het Hallo-wachtwoord voor Hallo sapadm gebruiker, dat wordt gebruikt voor Hallo SAP Host-Agent die wordt geïnstalleerd als onderdeel van Hallo SAP HANA-database-exemplaar.

Na het definiëren van Hallo wachtwoord, wordt een bevestigingsvenster weergegeven. Controleer alle Hallo gegevens vermeld en doorgaan met de Hallo-installatie. U hebt een voortgangsscherm die documenten Hallo installatievoortgang zoals Hallo hieronder bereikt

![Controleer de voortgang van installatie](./media/hana-installation/image27_show_progress.PNG)

Als het Hallo-installatie is voltooid, moet u een afbeelding zoals Hallo volgt

![De installatie is voltooid](./media/hana-installation/image28_install_finished.PNG)

Op dit moment moet Hallo SAP HANA-exemplaar actief en werkend en klaar voor gebruik. U moet kunnen tooconnect tooit vanuit SAP HANA Studio. Ook voor zorgen dat u voor de meest recente patches Hallo van SAP HANA controleren en deze patches toepassen.
























































 







 




