---
title: aaaBackup handleiding voor SAP HANA op Azure Virtual Machines | Microsoft Docs
description: Back-handleiding voor SAP HANA bevat twee belangrijke back-mogelijkheden voor SAP HANA voor virtuele machines in Azure
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: e651091bb5da2698ec8bf80cad405bfce5b192cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="backup-guide-for-sap-hana-on-azure-virtual-machines"></a>Back-uphandleiding voor SAP HANA op Azure Virtual Machines

## <a name="getting-started"></a>Aan de slag

Hallo back-handleiding voor SAP HANA uitgevoerd op virtuele Machines in Azure wordt alleen Azure-specifieke onderwerpen beschreven. Raadpleeg voor algemene SAP HANA back-up verwante items, Hallo SAP HANA-documentatie (Zie _back-documentatie voor SAP HANA_ verderop in dit artikel).

Hallo dit artikel gericht is op twee belangrijke back-mogelijkheden voor SAP HANA op Azure virtuele machines:

- HANA back-toohello bestandssysteem in een Azure virtuele Linux-Machine (Zie [SAP HANA Azure Backup op bestandsniveau](sap-hana-backup-file-level.md))
- HANA back-up op basis van opslag-momentopnamen met hello Azure storage-blob momentopname functie handmatig of Azure Backup-Service (Zie [SAP HANA back-up op basis van opslag-momentopnamen](sap-hana-backup-storage-snapshots.md))

SAP HANA biedt een back-up van de API waarmee de back-uphulpprogramma's van derden toointegrate rechtstreeks met SAP HANA. (Dat is niet binnen het bereik van deze handleiding Hallo.) Er is geen directe integratie van SAP HANA met Azure Backup-service beschikbaar is genomen op basis van deze API.

SAP HANA officieel als één exemplaar met een aanvullende beperking tooOLAP werkbelastingen op Azure VM-type GS5 wordt ondersteund (Zie [vinden gecertificeerd IaaS Platforms](https://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html) op Hallo SAP website). In dit artikel wordt bijgewerkt als nieuwe aanbiedingen voor SAP HANA op Azure beschikbaar.

Er is ook een SAP HANA hybride oplossing beschikbaar in Azure, waarbij SAP HANA waarop niet-gevirtualiseerde fysieke servers. Deze back-handleiding voor SAP HANA Azure bestrijkt echter een pure Azure-omgeving waarin SAP HANA wordt uitgevoerd in een virtuele machine van Azure niet SAP HANA waarop &quot;grote exemplaren.&quot; Zie [SAP HANA (grote exemplaren) overzicht en architectuur op Azure](hana-overview-architecture.md) voor meer informatie over deze back-upoplossing op &quot;grote exemplaren&quot; op basis van opslag-momentopnamen.

Algemene informatie over SAP producten die worden ondersteund in Azure vindt u in [SAP-notitie 1928533](https://launchpad.support.sap.com/#/notes/1928533).

Hallo onderstaande drie cijfers biedt een overzicht van Hallo SAP HANA back-upopties systeemeigen mogelijkheden van Azure op dit moment gebruikt en drie mogelijke toekomstige back-scenario's worden ook weergegeven. Hallo verwante artikelen [SAP HANA Azure Backup op bestandsniveau](sap-hana-backup-file-level.md) en [SAP HANA back-up op basis van opslag-momentopnamen](sap-hana-backup-storage-snapshots.md) beschrijven van deze opties in meer detail, met inbegrip van grootte- en Prestatieoverwegingen voor SAP HANA back-ups die multi-terabyte groot zijn.

![Deze afbeelding ziet u twee mogelijkheden voor het opslaan van de huidige VM-status Hallo](media/sap-hana-backup-guide/image001.png)

Deze afbeelding ziet u de mogelijkheid Hallo Hallo huidige status virtuele machine, hetzij via Azure Backup-service of handmatige momentopname van de VM-schijven op te slaan. Met deze benadering, één &#39; hebben t toomanage SAP HANA back-ups. Hallo uitdaging van het scenario voor Hallo schijven momentopname is consistentie van het bestandssysteem en de status van een toepassingsconsistente schijf. Hallo consistentie onderwerp wordt besproken in de sectie Hallo _SAP HANA gegevensconsistentie bij het maken van opslag-momentopnamen_ verderop in dit artikel. Mogelijkheden en beperkingen van Azure Backup-service gerelateerd tooSAP HANA back-ups worden ook besproken verderop in dit artikel.

![Deze afbeelding ziet u opties voor het maken van een SAP HANA bestandsback-up binnen Hallo VM](media/sap-hana-backup-guide/image002.png)

In deze afbeelding ziet u opties voor het nemen van een SAP HANA bestandsback-up binnen Hallo VM en bewaren van die back-upbestanden HANA ergens anders met verschillende hulpprogramma's. Een HANA back-up duurt langer dan een back-oplossing op basis van een momentopname vereist, maar heeft voordelen ten met betrekking tot de integriteit en consistentie. Verderop in dit artikel vindt u meer informatie.

![De volgende afbeelding toont een mogelijke toekomstige SAP HANA back-scenario](media/sap-hana-backup-guide/image003.png)

De volgende afbeelding toont een mogelijke toekomstige SAP HANA back-scenario. Als SAP HANA toegestaan voor het maken van back-ups van een secundaire replicatie, zou deze extra opties voor back-strategieën toevoegen. Op dit moment is het niet mogelijk op basis van tooa post in Hallo SAP HANA-Wiki:

_&quot;Is het mogelijk tootake back-ups op Hallo secundaire zijde?_

_Nee, momenteel kunnen alleen gegevens en logboekback-ups op Hallo primaire kant. Als automatische back-up is ingeschakeld, na overname toohello secundaire kant Hallo logboekback-ups automatisch er geschreven.&quot;_

## <a name="sap-resources-for-hana-backup"></a>SAP-resources voor HANA back-up

### <a name="sap-hana-backup-documentation"></a>Back-documentatie voor SAP HANA

- [Inleiding tooSAP HANA beheer](https://help.sap.com/viewer/6b94445c94ae495c83a19646e7c3fd56/2.0.00/en-US)
- [Uw back-up en herstelstrategie plannen](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm)
- [HANA back-up met behulp van ABAP DBACOCKPIT plannen](http://www.hanatutorials.com/p/schedule-hana-backup-using-abap.html)
- [Planning gegevensback-ups (SAP HANA Cockpit)](http://help.sap.com/saphelp_hanaplatform/helpdata/en/6d/385fa14ef64a6bab2c97a3d3e40292/frameset.htm)
- Veelgestelde vragen over SAP HANA back-up [SAP-notitie 1642148](https://launchpad.support.sap.com/#/notes/1642148)
- Veelgestelde vragen over SAP HANA-database en -opslag-momentopnamen in [SAP-notitie 2039883](https://launchpad.support.sap.com/#/notes/2039883)
- Bestandssystemen ongeschikt netwerk voor back-up en herstel in [SAP-notitie 1820529](https://launchpad.support.sap.com/#/notes/1820529)

### <a name="why-sap-hana-backup"></a>Waarom SAP HANA back-up?

Azure storage biedt beschikbaarheid en betrouwbaarheid out of box hello (Zie [tooMicrosoft inleiding Azure Storage](../../../storage/common/storage-introduction.md) voor meer informatie over Azure storage).

Hallo minimum voor &quot;back-&quot; toorely op Hallo Azure Sla's, te bewaren Hallo SAP HANA-gegevens en logboekbestanden bestanden op Azure VHD's aangesloten toohello SAP HANA server VM is. Deze aanpak bevat informatie over fouten van de VM, maar niet potentiële schade toohello SAP HANA-gegevens en logboekbestanden of logische fouten, zoals het verwijderen van gegevens of bestanden per ongeluk. Back-ups zijn ook vereist voor naleving of wettelijke redenen. Kortom, is altijd een nodig voor SAP HANA back-ups.

### <a name="how-tooverify-correctness-of-sap-hana-backup"></a>Hoe tooverify juistheid van SAP HANA back-up
Wanneer u opslag-momentopnamen, wordt een terugzetbewerking test uitgevoerd op een andere site aanbevolen. Deze aanpak biedt een manier tooensure dat een back-up correct en interne processen voor back-up en herstel werk is zoals verwacht. Hoewel dit een aanzienlijke drempel on-premises is veel eenvoudiger tooaccomplish in de cloud Hallo dankzij de benodigde resources tijdelijk voor dit doel.

Houd er rekening mee die tijdens het doorzoeken van een eenvoudig terugzetten en controle of HANA actief is en wordt uitgevoerd, is niet voldoende. In het ideale geval moet een een tabel consistentie selectievakje toobe-ervoor dat die database Hallo hersteld goed is uitgevoerd. SAP HANA biedt verschillende soorten consistentiecontroles beschreven in [SAP-notitie 1977584](https://launchpad.support.sap.com/#/notes/1977584).

Informatie over Hallo tabel consistentiecontrole kan ook worden gevonden op Hallo SAP-website op [tabel en consistentiecontroles catalogus](http://help.sap.com/saphelp_hanaplatform/helpdata/en/25/84ec2e324d44529edc8221956359ea/content.htm#loio9357bf52c7324bee9567dca417ad9f8b).

Voor standaardbestandback-ups is een terugzetbewerking test niet nodig. Er zijn twee SAP HANA-hulpmiddelen waarmee toocheck welke back-up kan worden gebruikt om te herstellen: hdbbackupdiag en hdbbackupcheck. Zie [handmatig controleren of een herstel is mogelijk](https://help.sap.com/saphelp_hanaplatform/helpdata/en/77/522ef1e3cb4d799bab33e0aeb9c93b/content.htm) voor meer informatie over deze hulpprogramma's.

### <a name="pros-and-cons-of-hana-backup-versus-storage-snapshot"></a>Voordelen en nadelen van HANA back-up versus opslag momentopname

SAP bestaat &#39; t geven voorkeur tooeither HANA back-up en opslag-momentopnamen. Geeft de voor- en nadelen, zodat een welke toouse, afhankelijk van de situatie Hallo en beschikbare opslag-technologie bepalen kan (Zie [plannen van uw back-up- en herstelstrategie](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm)).

Op Azure, houd rekening met de Hallo feit dat Azure blob momentopname functie bestaat & #39 Hallo; t garanderen van de consistentie van het bestandssysteem (Zie [Using blob momentopnamen met PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/)). Hallo van de volgende sectie _SAP HANA gegevensconsistentie bij het maken van opslag-momentopnamen_, enkele overwegingen met betrekking tot deze functie wordt besproken.

Bovendien een toounderstand Hallo facturering gevolgen wanneer vaak werken met blobs momentopnamen, zoals beschreven in dit artikel is: [begrijpen hoe momentopnamen doorlopen kosten](/rest/api/storageservices/understanding-how-snapshots-accrue-charges)— deze &#39; t als duidelijk als het gebruik van Azure virtuele schijven.

### <a name="sap-hana-data-consistency-when-taking-storage-snapshots"></a>SAP HANA gegevensconsistentie bij het maken van opslag-momentopnamen

Systeem- en consistentie van bestand is een complex probleem bij het maken van opslag-momentopnamen. Hallo gemakkelijkste manier tooavoid problemen zou worden tooshut omlaag SAP HANA en mogelijk zelfs Hallo hele virtuele machine. Afsluiten mogelijk goed met een demo of prototype of zelfs een ontwikkelsysteem, maar is geen optie voor een productiesysteem.

In Azure heeft een tookeep er rekening mee dat Azure blob momentopname functie bestaat & #39 Hallo; t consistentie van het bestandssysteem te garanderen. Dit werkt goed samen met behulp van Hallo echter momentopname SAP HANA-functie, zolang er slechts één virtuele schijf die betrokken zijn is. Maar zelfs met een enkele schijf hebben extra items toobe gecontroleerd. [SAP-notitie 2039883](https://launchpad.support.sap.com/#/notes/2039883) belangrijke informatie over SAP HANA back-ups via opslag-momentopnamen heeft. Bijvoorbeeld noemt dat met Hallo XFS file system noodzakelijk toorun is **xfs\_blokkeren** voordat vanaf een opslag momentopname tooguarantee consistentiecontrole (Zie [xfs\_freeze(8) - man Linux pagina](https://linux.die.net/man/8/xfs_freeze) voor meer informatie over **xfs\_blokkeren**).

Hallo-onderwerp aan consistentie wordt nog meer lastig in geval waarbij een enkel bestandssysteem verspreid over meerdere schijven/volumes. Bijvoorbeeld, met behulp mdadm of LVM en te verwijderen. Hallo SAP-notitie bovengenoemde statussen:

_&quot;Maar houd er rekening mee dat Hallo opslagsysteem tooguarantee i/o-consistentie heeft tijdens het maken van een momentopname van de opslag per SAP HANA-gegevensvolume, dat wil zeggen vastleggen van een SAP HANA servicespecifieke gegevensvolume moet een atomic-bewerking.&quot;_

Ervan uitgaande dat er een XFS bestandssysteem spanning vier Azure virtuele schijven, hello volgende stappen bevatten een consistente momentopname te maken die Hallo HANA gegevensgebied vertegenwoordigt:

- HANA momentopname voorbereiden
- Hallo-bestandssysteem blokkeren (bijvoorbeeld gebruiken **xfs\_blokkeren**)
- Alle momentopnamen van de benodigde blob in Azure maken
- Hallo-bestandssysteem blokkering opheffen
- Hallo HANA momentopname bevestigen

Aanbevolen wordt toouse Hallo bovenstaande procedure in alle gevallen toobe Hallo veilige zijde, ongeacht welk bestandssysteem. Of als één schijf of striping via mdadm of LVM over meerdere schijven.

Het is belangrijk tooconfirm Hallo HANA momentopname. Vervaldatum toohello &quot;kopiëren bij schrijven&quot; SAP HANA mogelijk geen extra schijfruimte, terwijl in deze modus momentopname voorbereiden. &#39; s ook niet mogelijk toostart nieuwe back-ups tot Hallo SAP HANA momentopname is bevestigd.

Azure Backup-service maakt gebruik van Azure VM-extensies tootake antwoord Hallo consistentie van het bestandssysteem. Deze VM-uitbreidingen zijn niet beschikbaar voor zelfstandig gebruik. Een heeft nog steeds toomanage SAP HANA consistentie. Zie Verwante artikel Hallo [SAP HANA Azure back-up op bestandsniveau](sap-hana-backup-file-level.md) voor meer informatie.

### <a name="sap-hana-backup-scheduling-strategy"></a>SAP HANA-strategie voor back-up plannen

Hallo SAP HANA artikel [plannen van uw back-up- en herstelstrategie](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm) statussen een basic toodo back-ups plannen:

- Opslag-momentopnamen (dagelijks)
- Voltooid de back-up met behulp van bestands- of bacint-indeling (één keer per week)
- Automatische logboekback-ups

U kunt desgewenst kan een volledig zonder opslag-momentopnamen; gaan ze kunnen worden vervangen door HANA delta back-ups, zoals incrementele of differentiële back-ups (Zie [Delta back-ups](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm)).

Hallo HANA Administration guide bevat een lijst met voorbeelden. Dit wijst erop dat een SAP HANA tooa bepaald punt in tijd met behulp van de volgende volgorde van de back-ups Hallo herstellen:

1. Volledige back-up
2. Differentiële back-up
3. Incrementele back-up 1
4. Incrementele back-up 2
5. Logboekback-ups

Met betrekking tot een exacte planning als toowhen en hoe vaak een specifieke back-uptype moet gebeuren, is het niet mogelijk toogive een algemene richtlijn: het bestand te klantspecifieke is en is afhankelijk van hoeveel gegevenswijzigingen in Hallo systeem optreden. Een basic aanbeveling SAP-kant kunnen worden gezien als algemene richtlijnen, is toomake één volledige HANA back-up eenmaal per week.
Met betrekking tot logboekback-ups, Zie Hallo SAP HANA documentatie [logboekback-ups](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm).

SAP wordt ook aangeraden tijdens het doorzoeken van sommige housekeeping van Hallo back-upcatalogus tookeep uit groeiende oneindig (Zie [huishoudelijke voor back-upcatalogus en back-upopslag](http://help.sap.com/saphelp_hanaplatform/helpdata/en/ca/c903c28b0e4301b39814ef41dbf568/content.htm)).

### <a name="sap-hana-configuration-files"></a>SAP HANA-configuratiebestanden

Zoals vermeld in de veelgestelde vragen over het Hallo in [SAP-notitie 1642148](https://launchpad.support.sap.com/#/notes/1642148), Hallo SAP HANA-configuratiebestanden maken geen deel uit van een standaard HANA back-up. Ze zijn geen essentiële toorestore een systeem. Hallo HANA configuratie kan handmatig worden gewijzigd na het terugzetten van Hallo. Als een wilt tooget Hallo dezelfde aangepaste configuratie tijdens het herstelproces Hallo, is het nodig tooback up Hallo HANA configuratiebestanden afzonderlijk.

Als standaard HANA back-ups gaat tooa HANA back-upbestand system specifiek, een kan ook Hallo configuratie bestanden toohello kopiëren dezelfde back-up bestandssysteem en kopieert u alles samen toohello laatste opslaglocatie zoals cool blob-opslag.

### <a name="sap-hana-cockpit"></a>SAP HANA Cockpit

SAP HANA Cockpit biedt de mogelijkheid Hallo van controleren en beheren van SAP HANA via een browser. Het kan ook de verwerking van SAP HANA back-ups en daarom kan worden gebruikt als een alternatieve tooSAP HANA Studio en ABAP DBACOCKPIT (Zie [SAP HANA Cockpit](https://help.sap.com/saphelp_hanaplatform/helpdata/en/73/c37822444344f3973e0e976b77958e/content.htm) voor meer informatie).

![Deze afbeelding ziet u Hallo SAP HANA Cockpit Database beheer scherm](media/sap-hana-backup-guide/image004.png)

Deze afbeelding toont Hallo SAP HANA Cockpit Database beheer scherm en Hallo back-tegel op Hallo links. De juiste gebruikersmachtigingen vereist zien Hallo back-tegel voor aanmeldingsaccount.

![Back-ups kunnen worden bewaakt in SAP HANA Cockpit zolang deze lopende](media/sap-hana-backup-guide/image005.png)

Back-ups kunnen worden bewaakt in SAP HANA Cockpit terwijl ze voortdurend zijn en zodra deze is voltooid, alle Hallo back-details beschikbaar zijn.

![Een voorbeeld van Firefox op een Azure-VM SLES 12 met Gnome bureaublad](media/sap-hana-backup-guide/image006.png)

Hallo vorige schermafbeeldingen zijn aangebracht in een Windows Azure VM. Dit is een voorbeeld Firefox gebruiken op een Azure-VM SLES 12 met Gnome bureaublad. Hallo optie toodefine SAP HANA back-upschema's wordt in SAP HANA Cockpit. Zoals ook zien kunnen, maar er wordt verwezen datum/tijd als een voorvoegsel voor de back-upbestanden Hallo. SAP HANA Studio Hallo standaardvoorvoegsel is &quot;COMPLETE\_gegevens\_back-&quot; bij het uitvoeren van een volledige back-up. Gebruik een uniek voorvoegsel wordt aanbevolen.

### <a name="sap-hana-backup-encryption"></a>Back-up SAP HANA-versleuteling

SAP HANA biedt versleuteling van gegevens en logboekbestanden. Als voor SAP HANA-gegevens en logboekbestanden worden niet versleuteld, zijn vervolgens Hallo back-ups ook niet versleuteld. Is toohello klant toouse een vorm van de oplossing van derden tooencrypt Hallo SAP HANA back-ups. Zie [gegevens en versleuteling voor volumes van logboek](https://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/01f36fbb5710148b668201a6e95cf2/content.htm) toofind voor meer informatie over SAP HANA-versleuteling.

Een klant kan Hallo IaaS VM versleuteling functie tooencrypt gebruiken in Microsoft Azure. Bijvoorbeeld, kan een specifieke gegevens schijven gekoppelde toohello VM, gebruiken deze gebruikte toostore SAP HANA back-ups zijn vervolgens kopieën te maken van deze schijven.

Azure Backup-service kan versleutelde VM's / schijven verwerken (Zie [hoe tooback up en herstel virtuele machines met Azure Backup versleuteld](../../../backup/backup-azure-vms-encryption.md)).

Een andere optie zou worden toomaintain Hallo SAP HANA-virtuele machine en de schijven zonder versleuteling en Hallo SAP HANA-back-upbestanden opslaan in een opslagaccount waarvoor versleuteling is ingeschakeld (Zie [Azure Storage Service: versleuteling van gegevens in rust](../../../storage/common/storage-service-encryption.md)) .

## <a name="test-setup"></a>Test setup

### <a name="test-virtual-machine-on-azure"></a>Test-virtuele Machine in Azure

Een SAP HANA-installatie in een virtuele machine van Azure GS5 is gebruikt voor Hallo back-up/herstel tests te volgen.

![Deze afbeelding ziet u deel Hallo overzicht van Azure portal voor Hallo HANA test VM](media/sap-hana-backup-guide/image007.png)

In deze afbeelding ziet u deel Hallo overzicht van Azure portal voor Hallo HANA test VM.

### <a name="test-backup-size"></a>Back-grootte testen

![In deze afbeelding is overgenomen van de back-console in HANA Studio Hallo en toont Hallo back-upbestand grootte van 229 GB voor Hallo HANA indexserver](media/sap-hana-backup-guide/image008.png)

Een dummy-tabel is gevuld met tooget gegevens een back-grootte van de totale gegevens van meer dan 200 GB tooderive realistische prestatiegegevens. Hallo-afbeelding is overgenomen van de back-console in HANA Studio Hallo en Hallo back-upbestand grootte van 229 GB voor Hallo HANA indexserver laat zien. Voor de tests hello, is Hallo standaard back-voorvoegsel 'COMPLETE_DATA_BACKUP' in SAP HANA Studio gebruikt. In de echte productiesystemen, moet een nuttiger voorvoegsel worden gedefinieerd. SAP HANA Cockpit stelt datum/tijd.

### <a name="test-tool-toocopy-files-directly-tooazure-storage"></a>Test hulpprogramma toocopy bestanden rechtstreeks tooAzure opslag

tootransfer SAP HANA back-upbestanden rechtstreeks tooAzure blob-opslag- of Azure-bestandsshares Hallo blobxfer hulpprogramma gebruikt omdat het ondersteunt zowel doelen en kunnen eenvoudig worden geïntegreerd in automatiseringsscripts vanwege tooits opdrachtregelinterface. Hallo blobxfer hulpprogramma is beschikbaar op [GitHub](https://github.com/Azure/blobxfer).

### <a name="test-backup-size-estimation"></a>De grootte van de back-schatting testen

Het is belangrijk tooestimate Hallo back-grootte van SAP HANA. Deze schatting tooimprove prestaties door te definiëren Hallo back-upbestand van maximale grootte voor een aantal back-upbestanden helpt vanwege tooparallelism tijdens het kopiëren van een bestand. (Deze informatie worden verderop in dit artikel uitgelegd.) Een moet ook bepalen of een volledige back-up of een delta-toodo back-up (incrementele of differentiële).

Gelukkig is er een eenvoudige SQL-instructie die u maakt een schatting van grootte van de back-upbestanden Hallo Hallo: **Selecteer \* van M\_back-\_grootte\_SCHATTINGEN** (Zie [ Schatting Hallo ruimte nodig in hello bestandssysteem voor een gegevensback-up](https://help.sap.com/saphelp_hanaplatform/helpdata/en/7d/46337b7a9c4c708d965b65bc0f343c/content.htm)).

![Hallo-uitvoer van deze SQL-instructie komt overeen met echte grootte bijna hetzelfde Hallo Hallo volledige gegevens back-up op schijf](media/sap-hana-backup-guide/image009.png)

Hallo-uitvoer van deze SQL-instructie voor het testsysteem hello, komt overeen met echte grootte bijna hetzelfde Hallo Hallo volledige gegevens back-up op schijf.

### <a name="test-hana-backup-file-size"></a>Grootte van back-upbestand HANA testen

![Hallo HANA Studio back-console kan één toorestrict Hallo maximale bestandsgrootte van de back-upbestanden HANA](media/sap-hana-backup-guide/image010.png)

Hallo HANA Studio back-console kan één toorestrict Hallo maximale bestandsgrootte van de back-upbestanden HANA. In de voorbeeld-omgeving Hallo maakt deze functie het mogelijk tooget meerdere kleinere back-in plaats van een back-upbestand van 230 GB upbestanden. Kleinere bestanden heeft een aanzienlijke invloed op prestaties (Zie Hallo verwant artikel [SAP HANA Azure back-up op bestandsniveau](sap-hana-backup-file-level.md)).

## <a name="summary"></a>Samenvatting

Op basis van de testresultaten Hallo Hallo volgende tabellen tonen voordelen en nadelen van oplossingen tooback een SAP HANA-database op Azure virtuele machines.

**Maak een back-up van bestandssysteem voor SAP HANA toohello en kopieer upbestanden back-daarna de laatste back-upbestemming toohello**

|Oplossing                                           |Professionals                                 |Nadelen                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|Behoudt HANA back-ups op VM-schijven                      |Er zijn geen extra risicobeheerinspanningen     |Lokale VM schijfruimte vrij eats           |
|Blobxfer hulpprogramma toocopy back-upbestanden tooblob opslag |Parallelle uitvoering toocopy meerdere bestanden, keuze toouse cool blob-opslag | Extra hulpprogramma onderhoud en aangepaste scripts | 
|BLOB kopiëren via Powershell of CLI                    |Geen aanvullende hulpprogramma nodig kan worden geconfigureerd via Azure Powershell of CLI |handmatig proces klant heeft tootake antwoord scripting en het beheer van de gekopieerde blobs voor terugzetten|
|TooNFS share kopiëren                                  |Na de verwerking van back-upbestanden op andere virtuele machine zonder gevolgen voor Hallo HANA server|Trage kopieerproces|
|Blobxfer kopiëren tooAzure File-Service                |Geen eat ruimte op de lokale VM-schijven|Er zijn geen directe ondersteuning door back-up, de grootte van beperking van de bestandsshare dat zich momenteel in 5 TB HANA schrijven|
|Azure Backup-Agent                                 | Zou worden aanbevolen oplossing         | Momenteel niet beschikbaar op Linux    |



**Back-up SAP HANA op basis van opslag-momentopnamen**

|Oplossing                                           |Professionals                                 |Nadelen                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|Azure Backup-Service                               | Kan back-up van de virtuele machine op basis van de blob-momentopnamen | Wanneer u geen bestand herstelbewerkingen, Hallo maken van een nieuwe virtuele machine is vereist voor Hallo terugzetten, wat vervolgens Hallo moet een nieuwe sleutel voor SAP HANA-licentie impliceert|
|Handmatige blob momentopnamen                              | Flexibiliteit toocreate en terugzetten specifieke VM-schijven zonder Hallo unieke ID voor VM|Alle handmatig werk met toobe gedaan door de klant Hallo|

## <a name="next-steps"></a>Volgende stappen
* [SAP HANA Azure Backup op bestandsniveau](sap-hana-backup-file-level.md) back-optie Hallo op basis van bestanden wordt beschreven.
* [SAP HANA back-up op basis van opslag-momentopnamen](sap-hana-backup-storage-snapshots.md) beschrijft Hallo opslag op basis van een momentopname optie back-up.
* hoe tooestablish hoge beschikbaarheid en herstel na noodgevallen van SAP HANA plannen in Azure (grote exemplaren), Zie toolearn [SAP HANA (grote exemplaren) hoge beschikbaarheid en herstel na noodgevallen op Azure](hana-overview-high-availability-disaster-recovery.md).
