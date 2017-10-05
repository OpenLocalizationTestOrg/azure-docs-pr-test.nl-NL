---
title: Back-up en herstel na noodgevallen voor Azure IaaS-schijven | Microsoft Docs
description: In dit artikel wordt uitgelegd hoe u kunt plannen voor back-up en Disaster Recovery (DR) van IaaS virtuele machines (VM's) en de schijven in Azure. Dit document bevat informatie over zowel beheerde als onbeheerde schijven
services: storage
cloud: Azure
documentationcenter: na
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: luywang
ms.openlocfilehash: 03d38bc3383b5fd39eca5ca67c315b34b98f0c39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="backup-and-disaster-recovery-for-azure-iaas-disks"></a>Back-up en herstel na noodgevallen voor Azure IaaS-schijven

In dit artikel wordt uitgelegd hoe u kunt plannen voor back-up en Disaster Recovery (DR) van IaaS virtuele machines (VM's) en de schijven in Azure. Dit document bevat informatie over zowel beheerde als onbeheerde schijven.

Eerst bespreken we de ingebouwde mogelijkheden voor fouttolerantie in de Azure-platform waarmee bescherming tegen lokale fouten. We vervolgens bespreken de noodherstel scenario's die niet volledig wordt gedekt door de ingebouwde mogelijkheden die het hoofdonderwerp behandeld in dit document is. We laten enkele voorbeelden van werkbelasting scenario's waarbij andere overwegingen voor back-up en Noodherstel gelden ook zien. Vervolgens getoetst mogelijke oplossingen voor Noodherstel van IaaS-schijven. 

## <a name="introduction"></a>Inleiding

De Azure-platform gebruikt verschillende methoden voor redundantie en fouttolerantie voor klanten beschermen tegen gelokaliseerde hardwarefouten die zich kunnen voordoen. Lokale fouten, omvat mogelijk problemen met een Azure storage server-machine die deel uitmaken van de gegevens voor een virtuele schijf of fouten van een SSD of harde schijf op die server worden opgeslagen. Dergelijke geïsoleerde hardwarefouten onderdeel kunnen zich voordoen tijdens normale bewerkingen en het platform is ontworpen om deze fouten netwerkfouten. Grote rampen kunnen resulteren in fouten of inaccessibility van een groot aantal opslagservers of een hele datacenter. Terwijl de virtuele machines en de schijven zijn doorgaans beveiligd tegen gelokaliseerde fouten, zijn extra stappen nodig zijn om u te beschermen tegen de werkbelasting van uw regio hele onherstelbare storing van (zoals een noodgeval) die invloed hebben op de virtuele machine en de schijven.

Problemen met de Klanttoepassing of de gegevens kunnen naast de mogelijkheid van platform fouten optreden. Een nieuwe versie van uw toepassing kan bijvoorbeeld per ongeluk een recente wijzigen in de gegevens maakt. In dat geval wilt u de toepassing en de gegevens naar een eerdere versie met de laatst bekende goede status te herstellen. Hiervoor moet het onderhouden van regelmatige back-ups.

Voor de regionale noodherstel, moet u de back-up uw IaaS VM-schijven in een andere regio. 

Voordat we opties voor back-up en Noodherstel bekijkt, samenvatting gaan we een aantal methoden beschikbaar voor het verwerken van gelokaliseerde fouten.

### <a name="azure-iaas-resiliency"></a>Tolerantie van Azure IaaS

*Tolerantie* verwijst naar de tolerantie voor normale fouten die in de hardware-onderdelen optreden. Tolerantie is de mogelijkheid om te herstellen van fouten en blijven werken. Het is niet over de fouten te voorkomen, maar reageert op storingen op een manier die uitvaltijd of verlies van gegevens voorkomt. Het doel van de tolerantie is om de toepassing naar een volledig werkend status na een mislukte te retourneren. Azure virtuele Machines en de schijven zijn ontworpen om netwerkfouten algemene hardwarefouten. Laat het ons kijken hoe de Azure IaaS-platform biedt voor deze tolerantie genoemd.

Een virtuele machine bestaat voornamelijk uit twee delen: (1) A compute-server en (2) de permanente schijven. Beide invloed op de fouttolerantie van een virtuele machine.

Als de Azure compute-hostserver uw virtuele machine met een hardwarefout (dit is zeldzame) optreedt, wordt Azure is ontworpen voor het automatisch herstelt de virtuele machine op een andere server. Als dit gebeurt, wordt er opnieuw worden opgestart en de virtuele machine worden back-up na enige tijd. Azure dergelijke hardwarefouten detecteert automatisch en wordt uitgevoerd herstelbewerkingen om ervoor te zorgen dat de klant VM zo spoedig mogelijk beschikbaar zijn.

Met betrekking tot IaaS-schijven zijn duurzaamheid van gegevens is essentieel voor het platform van de permanente opslag. Azure-klanten belangrijke zakelijke toepassingen die worden uitgevoerd op IaaS hebben en ze afhankelijk van de persistentie van de gegevens. Azure-ontwerpen de beveiliging voor deze IaaS-schijven met drie kopieën van gegevens lokaal opgeslagen, bieden hoge duurzaamheid tegen fouten in de lokale. Als een van de hardwareonderdelen van de schijf uitvalt, wordt uw virtuele machine niet beïnvloed omdat er twee extra kopieën ter ondersteuning van schijfaanvragen. Dit werkt prima zelfs als twee verschillende hardwareonderdelen ondersteuning van een schijf niet op hetzelfde moment (die zijn zeldzame). Om ervoor te zorgen dat we drie replica's altijd onderhouden, hiermee de Azure Storage-service automatisch wordt een nieuwe kopie van gegevens op de achtergrond als een van de drie kopieën niet beschikbaar is. Daarom mag niet nodig zijn voor het gebruik van RAID met Azure-schijven voor fouttolerantie. Een eenvoudige RAID-0-configuratie moet voldoende zijn voor de schijven te verwijderen, indien nodig om grotere volumes te maken.

Vanwege deze architectuur **Azure heeft consistent bedrijfsniveau uitgebracht duurzaamheid voor IaaS-schijven, met een toonaangevende nul % [op basis van Faalpercentage](https://en.wikipedia.org/wiki/Annualized_failure_rate).**

Gelokaliseerde hardwarefouten in de berekening hosten of in de opslag-platform kunnen soms leiden tot een tijdelijk niet beschikbaar voor de virtuele machine waarvoor de [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) voor beschikbaarheid van de virtuele machine. Azure biedt ook een toonaangevende SLA voor één VM-exemplaren die gebruikmaken van Premium-opslag-schijven.

Ter bescherming van de toepassing werkbelastingen van downtime als gevolg van het tijdelijke ontbreken van een schijf of virtuele machine klanten gebruik kunnen maken [Beschikbaarheidssets](../../virtual-machines/windows/manage-availability.md). Twee of meer virtuele machines in een beschikbaarheidsset biedt redundantie voor de toepassing. Azure maakt vervolgens deze virtuele machines en de schijven in afzonderlijke foutdomeinen met verschillende voeding, netwerk- en server-onderdelen. Dus gelokaliseerde hardwarefouten doorgaans hebben geen invloed op meerdere virtuele machines in de set op hetzelfde moment maximale beschikbaarheid biedt voor uw toepassing. Dit wordt beschouwd als een goede gewoonte beschikbaarheidssets gebruiken als hoge beschikbaarheid vereist is. Zie voor meer informatie het herstel na noodgevallen aspecten zoals hieronder beschreven.

### <a name="backup-and-disaster-recovery"></a>Back-up en herstel na noodgevallen

Herstel na noodgeval (DR) is de mogelijkheid om te herstellen van zeldzame maar belangrijke incidenten: tijdelijke, schaal fouten, zoals onderbreking van de service die gevolgen heeft voor een hele regio. Herstel na noodgevallen omvat gegevensback-up en te archiveren, en bevatten mogelijk handmatige interventie, zoals het terugzetten van een database vanuit back-up.

De virtuele machines/schijven in het geval van grote rampen waardoor grootschalige storingen mogelijk niet volledig te ingebouwde bescherming tegen gelokaliseerde fouten van de Azure-platform beveiligen. Dit omvat onherstelbare gebeurtenissen, zoals een datacenter wordt bereikt door een orkaan, aardbeving, fire of grote schaal eenheid hardwarefouten. Bovendien kunnen storingen als gevolg van de toepassing of problemen optreden.

Als u wilt beschermen de werkbelasting van uw IaaS tegen storingen, moet u plannen voor redundantie en back-ups herstellen. Voor herstel na noodgevallen, moet u van plan bent redundantie en back-up in een andere geografische locatie van de primaire site. Dit zorgt ervoor dat uw back-up wordt niet beïnvloed door de dezelfde gebeurtenis die oorspronkelijk van invloed op de virtuele machine of de schijven. Zie voor meer informatie [herstel na noodgevallen voor toepassingen die zijn gebouwd op Azure](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications).

Uw DR-overwegingen omvatten de volgende aspecten:

1. Hoge beschikbaarheid (HA) is de mogelijkheid van de toepassing om te blijven uitvoeren in een foutloze toestand bevindt, zonder aanzienlijke uitvaltijd. Door 'status in orde,' dat we de toepassing reageert en kunnen gebruikers verbinding maken met de toepassing en ermee. Het is mogelijk dat bepaalde bedrijfskritieke toepassingen en -databases moet altijd beschikbaar, zelfs als er fouten van het platform zijn. Voor deze werkbelastingen, moet u wellicht redundantie voor de toepassing, evenals de gegevens van plan bent.

2. Duurzaamheid van gegevens: In sommige gevallen kan de belangrijkste overweging is ervoor zorgen dat de gegevens blijven behouden in het geval van een noodgeval. Daarom moet u een back-up van uw gegevens in een andere site. Voor deze werkbelastingen moet u mogelijk niet volledig redundantie voor de toepassing, maar een regelmatige back-up van de schijven.

## <a name="backup-and-dr-scenarios"></a>Back-up en Noodherstel scenario 's

Bekijken we enkele typische voorbeelden van de toepassing werklast scenario's en de overwegingen voor het plannen van herstel na noodgevallen.

### <a name="scenario-1-major-database-solutions"></a>Scenario 1: Primaire Database oplossingen

U kunt een productie-databaseserver zoals SQL Server- of Oracle die ondersteuning voor hoge beschikbaarheid bieden. Kritieke productietoepassingen en gebruikers, is afhankelijk van deze database. Het plan voor herstel na noodgevallen voor dit systeem moet mogelijk de volgende vereisten ondersteunen:

1. Gegevens moet zijn beveiligd en hersteld.
2.  Server moet beschikbaar zijn voor gebruik.

Mogelijk moet het onderhouden van een replica van de database in een andere regio als een back-up. De oplossing kan afhankelijk van de vereisten voor beschikbaarheid van de server en herstel van gegevens op periodieke offline back-ups van de gegevens variëren van een actief-actief of actief / passief replica-site. Relationele databases zoals SQL Server en Oracle bieden verschillende opties voor replicatie. Voor SQL Server, [SQL Server altijd op beschikbaarheidsgroepen](https://msdn.microsoft.com/library/hh510230.aspx) kan worden gebruikt voor hoge beschikbaarheid.

NoSQL-databases zoals MongoDB bieden ook ondersteuning voor [replica's](https://docs.mongodb.com/manual/replication/) voor redundantie. De replica's voor hoge beschikbaarheid kunnen worden gebruikt.

### <a name="scenario-2-a-cluster-of-redundant-vms"></a>Scenario 2: Een cluster van redundante virtuele machines

U kunt een werkbelasting die wordt verwerkt door een cluster van virtuele machines die redundantie en taakverdeling. Een voorbeeld hiervan is een Cassandra-cluster dat is geïmplementeerd in een regio. Dit type architectuur biedt al een hoog niveau van redundantie in deze regio. Echter, om te voorkomen dat de werkbelasting een regionaal niveau fout, moet u het cluster verspreid over twee regio's of periodiek back-ups maken naar een andere regio.

### <a name="scenario-3-iaas-application-workload"></a>Scenario 3: IaaS toepassing werklast

Dit kan een standaard productie-werkbelasting die wordt uitgevoerd op een Azure VM zijn. Bijvoorbeeld, wordt een webserver of bestandsserver die de inhoud en andere bronnen van een site. Dit kan ook worden een op maat gemaakte business-toepassing uitgevoerd op een virtuele machine die de gegevens, bronnen en de status van toepassing zijn opgeslagen op de VM-schijven. In dit geval is het belangrijk om ervoor te zorgen dat u rekening houden met back-ups regelmatig. Back-upfrequentie moet worden gebaseerd op de aard van de virtuele machine-werkbelasting. Bijvoorbeeld, als de toepassing wordt dagelijks uitgevoerd en gegevens worden gewijzigd, moet klikt u vervolgens de back-up worden gehouden om het uur.

Een ander voorbeeld is een rapportserver die pull-gegevens uit andere bronnen en genereert cumulatieve rapporten. Verlies van deze virtuele machine of de schijven zal leiden tot verlies van de rapporten. Echter mogelijk opnieuw uitvoeren van het proces voor rapportage en opnieuw genereren van de uitvoer. In dat geval echt er geen gegevensverlies zelfs als de rapportserver is bereikt, wordt met een ramp, zodat u een hoger niveau van tolerantie voor verliezen deel van de gegevens op de rapportserver kan hebben. In dat geval minder frequente back-ups is een optie om de kosten te beperken.

### <a name="scenario-4-iaas-application-data-issues"></a>Scenario 4: IaaS toepassingsproblemen gegevens

U hebt een toepassing die wordt berekend, onderhouden en kritieke commerciële gegevens zoals prijsgegevens fungeert. Een nieuwe versie van uw toepassing heeft een software-oplossingen die onjuist berekende prijzen en de bestaande commerce gegevens geleverd door het platform is beschadigd. De beste loop van de actie kan hier worden eerst de eerdere versie van de toepassing en de gegevens te herstellen. U kunt deze inschakelen worden periodiek back-ups van uw systeem.

## <a name="disaster-recovery-solution-azure-backup-service"></a>Noodherstel: Azure Backup-Service

[Azure Backup-Service](https://azure.microsoft.com/services/backup/) kan worden gebruikt voor back-up en Noodherstel is, en dit proces werkt met [schijven beheerd](../../virtual-machines/windows/managed-disks-overview.md) , evenals [niet-beheerde schijven](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks). U kunt een back-uptaak maken met back-ups op basis van tijd, eenvoudig herstel van de virtuele machine en back-up bewaarbeleid. 

Als u [Premium-opslag schijven](storage-premium-storage.md), [schijven beheerd](../../virtual-machines/windows/managed-disks-overview.md), of andere schijftypen met de [lokaal redundante opslag (LRS)](storage-redundancy.md#locally-redundant-storage) optie, het is vooral belangrijk voor het benutten periodieke DR back-ups. Azure Backup slaat de gegevens in de Recovery Services-kluis voor het bewaren van de lange termijn. Kies de [geografisch redundante opslag (GRS)](storage-redundancy.md#geo-redundant-storage) optie voor de back-up Recovery Services-kluis. Die zorgt ervoor dat back-ups worden gerepliceerd naar een andere Azure-regio voor de beveiliging van regionale noodsituaties.

Voor [niet-beheerde schijven](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks), u kunt het opslagtype LRS voor IaaS-schijven gebruiken, maar zorg ervoor dat de Azure Backup is ingeschakeld met de optie GRS voor de Recovery Services-kluis.

**Als u de [GRS](storage-redundancy.md#geo-redundant-storage)/[RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage) optie voor uw niet-beheerde schijven u nog steeds nodig toepassingsconsistente momentopnamen voor back-up en Noodherstel.** U moet een gebruiken [Azure Backup-Service](https://azure.microsoft.com/services/backup/) of [toepassingsconsistente momentopnamen](#alternative-solution-consistent-snapshots).

Hier volgt een samenvatting van oplossingen voor herstel na Noodgevallen.

| Scenario | Automatische replicatie | Oplossing voor Noodherstel |
| --- | --- | --- |
| *Premium-opslag-schijven* | Lokale ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Managed Disks* | Lokale ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Niet-beheerde LRS-schijven* | Lokale ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Niet-beheerde GRS schijven* | Cross-regio ([GRS](storage-redundancy.md#geo-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/)<br/>[Toepassingsconsistente momentopnamen](#alternative-solution-consistent-snapshots) |
| *Niet-beheerde RA-GRS-schijven* | Cross-regio ([RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/)<br/>[Toepassingsconsistente momentopnamen](#alternative-solution-consistent-snapshots) |

Hoge beschikbaarheid kan beste door voldaan door het gebruik van beheerde schijven in een Beschikbaarheidsset samen met Azure Backup. Als u niet-beheerde schijven gebruikt, kunt u Azure back-up voor herstel na Noodgevallen. Als u nog geen Azure back-up gebruiken, duurt [toepassingsconsistente momentopnamen](#alternative-solution-consistent-snapshots) zoals beschreven in een volgende sectie is een alternatieve oplossing voor back-up en Noodherstel.

Uw keuzes voor hoge beschikbaarheid, back-up en Noodherstel op niveau van de toepassing of infrastructuur aan de onderstaande kan worden weergegeven:

| *Niveau* | Hoge beschikbaarheid   | Back-up-/ DR |
| --- | --- | --- |
| *Toepassing* | SQL AlwaysOn | Azure Backup |
| *Infrastructuur*  | Beschikbaarheidsset  | GRS met toepassingsconsistente momentopnamen |

### <a name="using-the-azure-backup-service"></a>Met behulp van de Azure Backup-Service

[Azure Backup](../../backup/backup-azure-vms-introduction.md) kunnen back-up van uw virtuele machines met Windows of Linux naar de Azure Recovery Services-kluis. Back-up en herstellen van essentiële gegevens wordt bemoeilijkt door het feit dat essentiële bedrijfsgegevens moet een back-up terwijl de toepassingen die de gegevens produceren die worden uitgevoerd. Om dit op te lossen, biedt Azure Backup toepassingsconsistente back-ups voor Microsoft-werkbelastingen met behulp van de Volume Shadow Service (VSS) om ervoor te zorgen dat gegevens correct worden geschreven naar de opslag. Voor virtuele Linux-machines zijn alleen bestandsconsistente back-ups mogelijk, aangezien Linux geen functionaliteit in VSS.

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-1.png)   

Wanneer Azure Backup een back-uptaak op het geplande tijdstip initieert, wordt de Backup-extensie die is geïnstalleerd in de virtuele machine om een punt in tijd momentopname geactiveerd. Een momentopname wordt gemaakt in coördinatie met VSS ophalen van een consistente momentopname van de schijven in de virtuele machine zonder af te sluiten. De Backup-extensie in de virtuele machine leegmaakacties alle schrijfbewerkingen alvorens de consistente momentopname van de schijven. Nadat de momentopname wordt gemaakt, worden de gegevens door Azure Backup overgebracht naar de back-upkluis. Als u het back-upproces efficiënter, wordt de service identificeert en alleen de blokken met gegevens die zijn gewijzigd sinds de laatste back-up overdraagt.


Als u wilt herstellen, kunt u bekijken van de beschikbare back-ups via Azure Backup en start vervolgens een herstelpunt. U kunt maken en herstellen van Azure back-ups via de [Azure-portal](https://portal.azure.com/), [met behulp van PowerShell](../../backup/backup-azure-vms-automation.md ), of met behulp van de [Azure CLI](https://docs.microsoft.com/azure/xplat-cli-install). Zie de Azure Backup voor meer informatie.

### <a name="steps-to-enable-backup"></a>Stappen voor het inschakelen van de back-up

De volgende stappen worden doorgaans gebruikt voor het inschakelen van de back-ups van uw virtuele machines met behulp van de [Azure Portal](https://portal.azure.com/). Er zijn enkele variaties afhankelijk van uw exacte scenario. Raadpleeg de [Azure Backup](../../backup/backup-azure-vms-introduction.md) documentatie voor volledige informatie. Azure back-up ook [biedt ondersteuning voor virtuele machines met schijven beheerd](https://azure.microsoft.com/blog/azure-managed-disk-backup/).

1.  Maak een recovery services-kluis voor een virtuele machine met behulp van de volgende stappen uit:

    a.  Met behulp van de [Azure-portal](https://portal.azure.com/), alle resources te bladeren naar 'Recovery Services-kluizen'.

    b.  Klik op toevoegen in het menu Recovery Services-kluizen en volg de stappen voor het maken van een nieuwe kluis in dezelfde regio bevinden als de virtuele machine. Bijvoorbeeld, als uw virtuele machine zich in de regio VS-West, VS-West voor verzamelen de kluis.

2.  Controleer of de Storage-replicatie voor de nieuwe kluis. Hiertoe toegang hebben tot de kluis van de blade Recovery Services-kluizen en Ga naar de instellingen/back-configuratie. Zorg ervoor dat de GRS-optie is standaard geselecteerd. Dit zorgt ervoor dat uw kluis automatisch worden gerepliceerd naar een secundaire Datacenter. Uw kluis in VS-West wordt bijvoorbeeld automatisch gerepliceerd naar VS-Oost.

3.  Het back-beleid configureren en selecteer de virtuele machine in dezelfde gebruikersinterface.

4.  Zorg ervoor dat de Backup-Agent is geïnstalleerd op de virtuele machine. Als uw virtuele machine wordt gemaakt met behulp van een installatiekopie van een Azure-galerie, is klikt u vervolgens de backup-agent al geïnstalleerd. Anders (dat wil zeggen, als u een aangepaste installatiekopie), gebruikt u instructies voor het [de VM-Agent installeren op de virtuele machine](../../backup/backup-azure-arm-vms-prepare.md#install-the-vm-agent-on-the-virtual-machine).

5.  Zorg ervoor dat de virtuele machine netwerkverbinding voor de Backup-service naar de functie toestaat. Volg deze instructies voor [netwerkverbinding](../../backup/backup-azure-arm-vms-prepare.md#network-connectivity).

6.  Zodra de bovenstaande stappen zijn voltooid, wordt de back-up wordt uitgevoerd met regelmatige tussenpozen zoals opgegeven in de back-upbeleid. Indien nodig, kunt u de eerste back-up handmatig van het kluisdashboard op de Azure-portal activeren.

Voor het automatiseren van Azure Backup met behulp van scripts, Raadpleeg [PowerShell-cmdlets voor VM-back-](../../backup/backup-azure-vms-automation.md).

### <a name="steps-for-recovery"></a>Stappen voor herstel

Als u wilt herstellen of opnieuw opbouwen van een virtuele machine, kunt u de virtuele machine herstellen uit een van de back-up herstelpunten in de kluis. Er zijn een aantal verschillende opties voor het uitvoeren van het herstel:

1.  U kunt een nieuwe virtuele machine maken als een punt in tijd representatie van een back-up van de VM.

2.  U kunt de schijven herstellen en vervolgens de sjabloon voor de virtuele machine aan te passen en de herstelde virtuele machine opnieuw gebruiken. 

Zie de instructies voor het [gebruik Azure portal voor virtuele machines herstellen](../../backup/backup-azure-arm-restore-vms.md#restoring-a-vm-during-azure-datacenter-disaster). Het document wordt ook uitgelegd voor de specifieke stappen voor het terugzetten van back-up VMs tot gebruik van uw geografisch redundante back-upkluis in het geval van een noodgeval op het primaire Datacenter gekoppeld Datacenter. Azure Backup gebruikt in dat geval de Compute-service van de secundaire regio voor de herstelde virtuele machine maken.

U kunt ook PowerShell voor [herstellen van een virtuele machine](../../backup/backup-azure-vms-automation.md#restore-an-azure-vm) of voor [schijven maken van een nieuwe virtuele machine uit hersteld](../../backup/backup-azure-vms-automation.md#create-a-vm-from-restored-disks).

## <a name="alternative-solution-consistent-snapshots"></a>Alternatieve oplossing: Toepassingsconsistente momentopnamen

Als u geen gebruik van de Azure Backup-Service, kunt u uw eigen back-mechanisme met momentopnamen kunt implementeren. Het is ingewikkeld toepassingsconsistente momentopnamen voor alle schijven die worden gebruikt door een virtuele machine maken en deze momentopnamen worden vervolgens gerepliceerd naar een andere regio. Om deze reden beschouwt Azure gebruik te maken van de Backup-Service een betere optie dan een aangepaste oplossing bouwen. Als u met RA-GRS/GRS opslag voor schijven, momentopnamen automatisch gerepliceerd naar een secundaire Datacenter. Als u LRS opslag voor schijven gebruikt, moet u voor replicatie van de gegevens. Zie voor meer informatie [Back-up van Azure niet-beheerde VM-schijven met incrementele momentopnamen](../../virtual-machines/windows/incremental-snapshots.md).

Een momentopname is een weergave van een object op een bepaald punt in tijd. Een momentopname wordt in rekening gebracht facturering voor de incrementele hoeveelheid gegevens die deze bevat. Zie voor meer informatie [momentopname maken van een blob](../blobs/storage-blob-snapshots.md).

### <a name="creating-snapshots-while-the-vm-is-running"></a>Maken van momentopnamen terwijl de virtuele machine wordt uitgevoerd

Terwijl u een momentopname op elk gewenst moment uitvoeren kunt als de virtuele machine wordt uitgevoerd, er zijn nog steeds gegevens worden gestreamd naar de schijven en de momentopnamen gedeeltelijke bewerkingen die tijdens de vlucht zijn kunnen bevatten. Ook als er meerdere schijven die zijn betrokken, de momentopnamen van verschillende schijven mogelijk opgetreden op verschillende tijdstippen, wat betekent dat deze momentopnamen kunnen niet worden gecoördineerd. Dit is vooral problematisch voor striped volumes waarvan de bestanden beschadigd kunnen raken als wijzigingen tijdens de back-up wordt gemaakt.

Om deze situatie te voorkomen, moet het back-upproces implementeren de volgende stappen uit:

1.  Alle schijven blokkeren

2.  De in behandeling geschreven leegmaken

3.  Vervolgens [momentopname maken van een blob](../blobs/storage-blob-snapshots.md) voor alle schijven

Sommige Windows-toepassingen zoals SQL Server bieden een gecoördineerde back-mechanisme via VSS toepassingsconsistente back-ups maken. Op Linux, kunt u een hulpprogramma zoals fsfreeze voor de coördinatie van de schijven, zodat er bestandsconsistente back-ups, maar niet toepassingsconsistente momentopnamen. Dit proces is ingewikkeld, dus en moet u overwegen [Azure Backup](../../backup/backup-azure-vms-introduction.md) of een back-upoplossing van derden die dit al te implementeren.

De bovenstaande procedure resulteert in een verzameling van gecoördineerde momentopnamen voor alle VM schijven, voor een bepaald punt in tijd weergave van de virtuele machine. Dit is een herstelpunt voor back-up voor de virtuele machine. U kunt het proces herhalen met regelmatige tussenpozen periodiek back-ups maken. Hieronder vindt u de stappen voor het [kopiëren van de back-ups naar een andere regio](#copy-the-snapshots-to-another-region) voor herstel na Noodgevallen.

### <a name="creating-snapshots-while-the-vm-is-offline"></a>Maken van momentopnamen terwijl de virtuele machine offline is.

Een andere optie voor het maken van consistente back-ups is afgesloten met de virtuele machine en maken van momentopnamen van de blob van elke schijf. Dit is eenvoudiger dan coördinerende momentopnamen van een actieve virtuele machine, maar een paar minuten uitvaltijd is vereist. Bij dit proces wordt als volgt:

1. De virtuele machine afgesloten.

2. Maak een momentopname van elke VHD-blob, die slechts enkele seconden duurt.

    U kunt gebruiken voor het maken van een momentopname [PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blob-snapshots), wordt de [Rest-API van Azure Storage](https://msdn.microsoft.com/library/azure/ee691971.aspx), [Azure CLI](https://docs.microsoft.com/azure/xplat-cli-install), of een van de clientbibliotheken van Azure Storage, zoals [de Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/hh488361.aspx).

3. Start de virtuele machine, waardoor de uitvaltijd eindigt. Doorgaans het hele proces is voltooid binnen een paar minuten.

Dit proces resulteert in een verzameling van toepassingsconsistente momentopnamen voor alle schijven bieden een back-up herstelpunt voor de virtuele machine. Hieronder vindt u de stappen voor het kopiëren van de momentopnamen voor een andere regio voor herstel na Noodgevallen.

### <a name="copy-the-snapshots-to-another-region"></a>De momentopnamen kopiëren naar een andere regio

Het maken van de momentopnamen die alleen zijn mogelijk niet voldoende is voor herstel na Noodgevallen. U moet ook de momentopnameback-ups worden gerepliceerd naar een andere regio.

Als u GRS of RA-GRS van de schijven en vervolgens de momentopnamen automatisch naar de secundaire regio worden gerepliceerd. Er kan een paar minuten vertraging vóór de replicatie, en als het primaire Datacenter wordt uitgeschakeld voordat de momentopnamen voltooien repliceren, kunt u zich niet toegang hebben tot de momentopnamen van het secundaire Datacenter. De kans is klein.

> [!Note] 
> Alleen met de schijven in een GRS of RA-GRS-account, worden de virtuele machine niet beveiligd tegen rampen. U moet ook gecoördineerde momentopnamen maken of gebruiken van Azure Backup. Dit is vereist voor het herstellen van een virtuele machine naar een consistente status.

Als u LRS gebruikt, moet u de momentopnamen kopiëren naar een ander opslagaccount onmiddellijk na het maken van een momentopname. Het doel voor het kopiëren wordt mogelijk een LRS storage-account in een andere regio, wat resulteert in het exemplaar wordt in een externe regio. U kunt ook de momentopname kopiëren naar een RA-GRS-opslagaccount in dezelfde regio. In dit geval wordt worden de momentopname vertraagd gerepliceerd naar de externe secundaire regio. Uw back-up is beveiligd tegen rampen op de primaire site eenmaal het kopiëren en replicatie is voltooid.

Als u wilt kopiëren efficiënt uw incrementele momentopnamen voor herstel na Noodgevallen, lees de instructies in [Back-up van Azure niet-beheerde VM-schijven met incrementele momentopnamen](../../virtual-machines/windows/incremental-snapshots.md).

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-2.png)   

### <a name="recovery-from-snapshots"></a>Herstel van momentopnamen

Voor het ophalen van een momentopname, zodat een nieuwe blob te kopiëren. Als u de momentopname van de primaire account kopieert, kunt u de momentopname naar de base blob van de momentopname dus herstellen van de schijf voor de momentopname; Dit staat bekend als het promoveren van de momentopname. Als u kopieert de momentopname back-up van een secundaire account (bij RA-GRS), moet deze worden gekopieerd naar een primaire-account. U kunt een momentopname kopiëren [met behulp van PowerShell](storage-powershell-guide-full.md#how-to-copy-a-snapshot-of-a-blob) of met het AzCopy-hulpprogramma. Zie voor meer informatie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma](storage-use-azcopy.md).

In het geval van virtuele machines met meerdere schijven, moet u de momentopnamen die deel van hetzelfde gecoördineerde herstelpunt uitmaken kopiëren. Zodra u de momentopnamen naar beschrijfbare VHD-blobs kopiëren, kunt u de blobs kunt gebruiken om uw virtuele machine met de sjabloon voor de virtuele machine opnieuw te maken.

## <a name="other-options"></a>Andere opties

### <a name="sql-server"></a>SQL Server

SQL Server wordt uitgevoerd op een virtuele machine heeft een eigen ingebouwde mogelijkheden voor het back-up van uw SQL Server-database naar Azure Blob-opslag of een bestandsshare. Als het opslagaccount GRS of RA-GRS is, kunt u deze back-ups in het opslagaccount secundaire datacenter in het geval van een ramp, met dezelfde beperkingen openen, zoals eerder besproken. Zie voor meer informatie [back-up en herstel voor SQL Server in Azure Virtual Machines](../../virtual-machines/windows/sql/virtual-machines-windows-sql-backup-recovery.md). Naast back-up and restore [SQL Server altijd op beschikbaarheidsgroepen](../../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md) secundaire replica's van databases in aanzienlijk minder hersteltijd na noodgevallen kunt onderhouden.

## <a name="other-considerations"></a>Andere overwegingen

In dit artikel is beschreven hoe u back-up of momentopnamen van uw virtuele machines en hun schijven voor de ondersteuning van herstel na noodgevallen en hoe deze gebruiken om te herstellen. Met het Azure Resource Manager-model veel mensen sjablonen gebruiken hun virtuele machines en andere infrastructuur maken in Azure. Een sjabloon kunt u een virtuele machine met dezelfde configuratie elke keer maken. Als u aangepaste installatiekopieën gebruikt voor het maken van uw virtuele machines, moet u ervoor dat uw installatiekopieën zijn beveiligd met een RA-GRS-account wilt opslaan.

Uw back-upproces mogelijk als gevolg daarvan kan een combinatie van twee dingen:

1. Back-up van de gegevens (schijven)
2. Back-up van de configuratie (sjablonen, aangepaste installatiekopieën)

Wellicht hebt u voor het afhandelen van de back-up van zowel de gegevens en de configuratie, afhankelijk van de back-optie die u kiest, of de Backup-service al die voor u kan verwerken.

## <a name="appendix---understanding-the-impact-of-lrs-grs-and-ra-grs"></a>Bijlage - het effect van LRS GRS en RA-GRS

Voor de storage-accounts in Azure, er zijn drie typen van de redundantie van de gegevens die u met betrekking tot noodherstel – lokaal redundante (LRS) geografisch redundante (GRS overwegen moet) of geografisch redundante met lezen toegang (RA-GRS). 

Lokaal behoudt redundante opslag (LRS) drie kopieën van de gegevens in hetzelfde Datacenter. Bij het schrijven van de gegevens, worden alle drie kopieën worden bijgewerkt voordat succes aan de aanroeper wordt geretourneerd, zodat u weet dat ze identiek zijn. De schijf is beveiligd tegen lokale stroomstoringen, omdat het is zeer onwaarschijnlijk dat alle drie kopieën op hetzelfde moment zou worden beïnvloed. In het geval van LRS is er geen geografische redundantie, zodat de schijf is niet beveiligd tegen onherstelbare fouten die invloed op een volledige data center of de opslag-eenheid hebben kunnen.

Met GRS en RA-GRS drie kopieën van uw gegevens worden bewaard in de primaire regio (u hebt geselecteerd) en drie extra kopieën van uw gegevens blijven behouden in een bijbehorende secundaire regio (ingesteld door Azure). Als u gegevens in VS-West opslaat, wordt er bijvoorbeeld de gegevens worden gerepliceerd naar VS-Oost. Dit asynchroon wordt gedaan en er is een kleine vertraging tussen de updates naar de primaire en secundaire. Replica's van de schijven op de secundaire site zijn consistent op basis van per schijf (met de vertraging), maar de replica's van meerdere actieve schijven mogelijk niet synchroon **met elkaar**. Toepassingsconsistente momentopnamen zijn om een consistente replica's maken over meerdere schijven, nodig.

Het belangrijkste verschil tussen GRS en RA-GRS is met RA-GRS, kunt u de secundaire kopie lezen op elk gewenst moment. Als er een probleem dat de gegevens in de primaire regio niet toegankelijk samenstelt, is het team van Azure brengt alles in het werk toegang herstellen. Terwijl de primaire niet beschikbaar is, hebt u RA-GRS is ingeschakeld, kunt u toegang tot de gegevens in het secundaire Datacenter. Dus als u van plan bent om te lezen van de replica als de primaire niet toegankelijk is, moet klikt u vervolgens RA-GRS worden overwogen.

Als blijkt te zijn van een aanzienlijke onderbreking, mag het team van Azure activeert u een geo-failover en wijzigen van de primaire DNS-vermeldingen om te verwijzen naar de secundaire opslag. Als u beide GRS of RA-GRS ingeschakeld, kunt u nu de gegevens in de regio die wordt gebruikt om te worden van de secundaire openen. Met andere woorden, als uw storage-account GRS is en er een probleem is, u kunt toegang tot de secundaire opslag alleen als er een geo-failover.

Zie voor meer informatie [wat te doen als een Azure Storage-storing optreedt,](storage-disaster-recovery-guidance.md). 

Houd er rekening mee dat Microsoft kan bepalen of er een failover plaatsvindt. Failover niet per storage-account wordt beheerd, wordt daarom niet besloten door individuele klanten. Als u wilt implementeren herstel na noodgevallen voor specifieke storage-accounts of schijven op virtuele machine, moet u de technieken die eerder in dit artikel wordt beschreven.
