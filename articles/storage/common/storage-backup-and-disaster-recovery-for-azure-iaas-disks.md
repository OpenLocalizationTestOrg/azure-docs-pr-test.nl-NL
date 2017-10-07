---
title: aaaBackup en herstel na noodgevallen voor Azure IaaS-schijven | Microsoft Docs
description: In dit artikel wordt uitgelegd hoe tooplan voor back-up en Disaster Recovery (DR) van IaaS virtuele machines (VM's) en de schijven in Azure. Dit document bevat informatie over zowel beheerde als onbeheerde schijven
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
ms.openlocfilehash: 49b0e7732d6df9407e1e44d9af2500c99a85b37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-disaster-recovery-for-azure-iaas-disks"></a>Back-up en herstel na noodgevallen voor Azure IaaS-schijven

In dit artikel wordt uitgelegd hoe tooplan voor back-up en Disaster Recovery (DR) van IaaS virtuele machines (VM's) en de schijven in Azure. Dit document bevat informatie over zowel beheerde als onbeheerde schijven.

Eerst bespreken we Hallo ingebouwde mogelijkheden voor fouttolerantie in hello Azure-platform waarmee bescherming tegen lokale fouten. We bespreken Hallo na noodgevallen scenario's niet volledig gedekt door Hallo ingebouwde mogelijkheden, namelijk Hallo hoofdonderwerp behandeld in dit document vervolgens. We laten enkele voorbeelden van werkbelasting scenario's waarbij andere overwegingen voor back-up en Noodherstel gelden ook zien. Vervolgens getoetst mogelijke oplossingen voor Noodherstel van IaaS-schijven. 

## <a name="introduction"></a>Inleiding

Hello Azure-platform gebruikt verschillende methoden voor redundantie en fouttolerantie tolerantie toohelp klanten beschermen tegen gelokaliseerde hardwarefouten die zich kunnen voordoen. Lokale fouten, omvat mogelijk problemen met een Azure storage server-machine die deel uitmaken van het Hallo-gegevens voor een virtuele schijf of fouten van een SSD of harde schijf op die server worden opgeslagen. Dergelijke geïsoleerde hardwarefouten onderdeel kunnen zich voordoen tijdens normale bewerkingen en Hallo platform is ontworpen toobe robuuste toothese fouten. Grote rampen kunnen resulteren in fouten of inaccessibility van een groot aantal opslagservers of een hele datacenter. Terwijl de virtuele machines en de schijven zijn doorgaans beveiligd tegen gelokaliseerde fouten, zijn extra stappen nodig tooprotect uw werkbelasting van de regio hele onherstelbare fouten (zoals een noodgeval) die invloed hebben op de virtuele machine en de schijven.

Bovendien toohello mogelijkheid van platform fouten met Hallo Klanttoepassing of gegevens kunnen problemen optreden. Een nieuwe versie van uw toepassing kan bijvoorbeeld per ongeluk maakt voor een recente toohello gegevens wijzigen. In dat geval kunt u toorevert Hallo toepassing en Hallo gegevens tooa eerdere versie met Hallo laatst bekende goede status. Hiervoor moet het onderhouden van regelmatige back-ups.

Voor de regionale noodherstel, moet u de back-up uw IaaS VM schijven tooa andere regio. 

Voordat we opties voor back-up en Noodherstel bekijkt, samenvatting gaan we een aantal methoden beschikbaar voor het verwerken van gelokaliseerde fouten.

### <a name="azure-iaas-resiliency"></a>Tolerantie van Azure IaaS

*Tolerantie* toohello tolerantie verwijst voor normale fouten die in de hardware-onderdelen optreden. Tolerantie Hallo mogelijkheid toorecover van fouten wordt en toofunction worden voortgezet. Het is niet over de fouten te voorkomen, maar reageert toofailures op een manier die uitvaltijd of verlies van gegevens voorkomt. Hallo-doel van de tolerantie is tooreturn hello tooa volledig werkend toepassingsstatus na een mislukte. Azure virtuele Machines en de schijven zijn ontworpen toobe robuuste toocommon hardwarefouten. Laat het ons kijken hoe hello Azure IaaS-platform biedt voor deze tolerantie genoemd.

Een virtuele machine bestaat voornamelijk uit twee delen: (1) A compute-server en (2) Hallo permanente schijven. Beide invloed hebben op Hallo fouttolerantie van een virtuele machine.

Als hello Azure compute-hostserver uw virtuele machine met een hardwarefout (dit is zeldzame) optreedt, is Azure ontworpen tooautomatically terugzetten Hallo VM op een andere server. Als dit gebeurt, wordt er opnieuw worden opgestart en Hallo VM worden back-up na enige tijd. Azure dergelijke hardwarefouten detecteert automatisch en herstelbewerkingen uitvoert toohelp zorg Hallo klant VM zo spoedig mogelijk beschikbaar zijn.

Met betrekking tot IaaS-schijven zijn duurzaamheid van gegevens is essentieel voor Hallo permanente opslag platform. Azure-klanten belangrijke zakelijke toepassingen die worden uitgevoerd op IaaS hebben en ze afhankelijk zijn van Hallo persistentie van Hallo-gegevens. Azure-ontwerpen de beveiliging voor deze IaaS-schijven met drie kopieën van gegevens lokaal opgeslagen, bieden hoge duurzaamheid tegen fouten in de lokale. Als een Hallo hardwareonderdelen waarin de schijf uitvalt, wordt uw virtuele machine niet beïnvloed omdat er twee extra kopieën toosupport schijfaanvragen zijn. Werkt probleemloos zelfs als twee verschillende hardwareonderdelen ondersteuning van een schijf op Hallo dezelfde mislukt tijd (die zijn zeldzame). toohelp Zorg altijd onderhouden we drie replica's, een nieuwe kopie van gegevens op de achtergrond Hallo hello Azure Storage-service automatisch gestart als een van drie kopieën van Hallo niet beschikbaar is. Daarom mag niet nodig toouse RAID met Azure-schijven voor fouttolerantie. Een eenvoudige RAID 0-configuratie moet voldoende zijn voor striping Hallo schijven als grotere volumes nodig toocreate.

Vanwege deze architectuur **Azure heeft consistent bedrijfsniveau uitgebracht duurzaamheid voor IaaS-schijven, met een toonaangevende nul % [op basis van Faalpercentage](https://en.wikipedia.org/wiki/Annualized_failure_rate).**

Gelokaliseerde hardwarestoringen op Hallo compute hosten of in de opslag van Hallo platform soms kan leiden tot tijdelijk niet beschikbaar voor VM die onder Hallo vallen Hallo [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) voor beschikbaarheid van de virtuele machine. Azure biedt ook een toonaangevende SLA voor één VM-exemplaren die gebruikmaken van Premium-opslag-schijven.

toepassingsworkloads toosafeguard van uitvaltijd vanwege toohello tijdelijk niet beschikbaar zijn van een schijf of de VM, klanten gebruik kunnen maken [Beschikbaarheidssets](../../virtual-machines/windows/manage-availability.md). Twee of meer virtuele machines in een beschikbaarheidsset biedt redundantie voor Hallo-toepassing. Azure maakt vervolgens deze virtuele machines en de schijven in afzonderlijke foutdomeinen met verschillende voeding, netwerk- en server-onderdelen. Dus gelokaliseerde hardwarefouten doorgaans geen invloed op meerdere virtuele machines in Hallo ingesteld op Hallo tegelijkertijd maximale beschikbaarheid biedt voor uw toepassing. Dit wordt beschouwd als dat een goede gewoonte toouse beschikbaarheidssets als hoge beschikbaarheid vereist is. Zie voor meer informatie Hallo herstel na noodgevallen aspecten zoals hieronder beschreven.

### <a name="backup-and-disaster-recovery"></a>Back-up en herstel na noodgevallen

Noodherstel (DR) is Hallo mogelijkheid toorecover van zeldzame maar belangrijke incidenten: tijdelijke, schaal fouten, zoals onderbreking van de service die gevolgen heeft voor een hele regio. Herstel na noodgevallen omvat gegevensback-up en te archiveren, en bevatten mogelijk handmatige interventie, zoals het terugzetten van een database vanuit back-up.

Hello Azure-platform van ingebouwde bescherming tegen gelokaliseerde fouten mogelijk niet volledig te beveiligen Hallo VM's / schijven in geval van grote rampen waardoor grootschalige uitval Hallo. Dit omvat onherstelbare gebeurtenissen, zoals een datacenter wordt bereikt door een orkaan, aardbeving, fire of grote schaal eenheid hardwarefouten. Bovendien kunnen fouten vanwege tooapplication of gegevens problemen optreden.

toohelp uw IaaS-werkbelastingen beschermen tegen storingen, moet u plannen voor redundantie en back-ups tooenable herstel. Voor herstel na noodgevallen, moet u van plan bent redundantie en back-up in een andere geografische locatie weg Hallo primaire site. Dit zorgt ervoor uw back-up wordt niet beïnvloed door Hallo dezelfde gebeurtenis die oorspronkelijk beïnvloed Hallo VM of de schijven. Zie voor meer informatie [herstel na noodgevallen voor toepassingen die zijn gebouwd op Azure](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications).

Uw DR-overwegingen omvatten Hallo volgende aspecten:

1. Hoge beschikbaarheid (HA) is de mogelijkheid Hallo van Hallo toepassing toocontinue uitgevoerd in een foutloze toestand bevindt, zonder aanzienlijke uitvaltijd. We dat door 'status in orde,' Hallo toepassing reageert en kunnen gebruikers verbinding maken met de toepassing toohello en ermee. Bepaalde essentiële toepassingen en databases kunnen altijd vereist toobe beschikbaar, zelfs wanneer er fouten in Hallo-platform zijn. Voor deze werkbelastingen moet u tooplan redundantie voor de toepassing hello, evenals Hallo-gegevens.

2. Duurzaamheid van gegevens: In sommige gevallen kan de belangrijkste overweging Hallo is ervoor zorgen dat Hallo gegevens blijven behouden in geval van een noodgeval Hallo. Daarom moet u een back-up van uw gegevens in een andere site. Voor deze werkbelastingen moet u mogelijk niet volledig redundantie voor de toepassing hello, maar een regelmatige back-up van Hallo-schijven.

## <a name="backup-and-dr-scenarios"></a>Back-up en Noodherstel scenario 's

Bekijken we enkele typische voorbeelden van toepassing werklast scenario's en Hallo overwegingen voor het plannen van herstel na noodgevallen.

### <a name="scenario-1-major-database-solutions"></a>Scenario 1: Primaire Database oplossingen

U kunt een productie-databaseserver zoals SQL Server- of Oracle die ondersteuning voor hoge beschikbaarheid bieden. Kritieke productietoepassingen en gebruikers, is afhankelijk van deze database. Hallo herstel na noodgevallen plannen voor dit systeem moet mogelijk toosupport Hallo volgens de vereisten:

1. Gegevens moet zijn beveiligd en hersteld.
2.  Server moet beschikbaar zijn voor gebruik.

Mogelijk moet het onderhouden van een replica van Hallo-database in een andere regio als een back-up. Hallo-oplossing kan, afhankelijk van het Hallo-vereisten voor beschikbaarheid van de server en herstel van gegevens variëren van een actief-actief of actief / passief replica site tooperiodic offline back-ups van gegevens Hallo. Relationele databases zoals SQL Server en Oracle bieden verschillende opties voor replicatie. Voor SQL Server, [SQL Server altijd op beschikbaarheidsgroepen](https://msdn.microsoft.com/library/hh510230.aspx) kan worden gebruikt voor hoge beschikbaarheid.

NoSQL-databases zoals MongoDB bieden ook ondersteuning voor [replica's](https://docs.mongodb.com/manual/replication/) voor redundantie. Hallo-replica's voor hoge beschikbaarheid kunnen worden gebruikt.

### <a name="scenario-2-a-cluster-of-redundant-vms"></a>Scenario 2: Een cluster van redundante virtuele machines

U kunt een werkbelasting die wordt verwerkt door een cluster van virtuele machines die redundantie en taakverdeling. Een voorbeeld hiervan is een Cassandra-cluster dat is geïmplementeerd in een regio. Dit type architectuur biedt al een hoog niveau van redundantie in deze regio. Echter tooprotect Hallo werkbelasting van een regionaal niveau fout, moet u Hallo cluster verspreid over twee regio's of periodiek back-ups tooanother regio maken.

### <a name="scenario-3-iaas-application-workload"></a>Scenario 3: IaaS toepassing werklast

Dit kan een standaard productie-werkbelasting die wordt uitgevoerd op een Azure VM zijn. Bijvoorbeeld, wordt een webserver of bestandsserver houden Hallo inhoud en andere bronnen van een site. Dit kan ook een op maat gemaakte business-toepassing uitgevoerd op een virtuele machine die de gegevens, bronnen en de status van toepassing zijn opgeslagen op Hallo VM schijven worden. In dit geval is het belangrijk toomake zeker dat u rekening houden met back-ups regelmatig. Back-upfrequentie moet worden gebaseerd op Hallo aard van Hallo VM werkbelasting. Bijvoorbeeld, als de toepassing hello elke dag wordt uitgevoerd en gegevens worden gewijzigd, moet klikt u vervolgens Hallo back-up worden gehouden elk uur.

Een ander voorbeeld is een rapportserver die pull-gegevens uit andere bronnen en genereert cumulatieve rapporten. Verlies van deze virtuele machine of de schijven leidt toohello verlies van Hallo-rapporten. Het kan echter mogelijk toorerun Hallo reporting proces en opnieuw genereren Hallo uitvoer zijn. In dat geval echt er geen gegevensverlies zelfs als de rapportserver Hallo is bereikt, wordt met een ramp, zodat u een hoger niveau van tolerantie voor het onderdeel van het Hallo-gegevens op Hallo reporting server verliezen kunnen hebben. In dat geval minder frequente back-ups is een optie tooreduce Hallo kosten.

### <a name="scenario-4-iaas-application-data-issues"></a>Scenario 4: IaaS toepassingsproblemen gegevens

U hebt een toepassing die wordt berekend, onderhouden en kritieke commerciële gegevens zoals prijsgegevens fungeert. Een nieuwe versie van uw toepassing heeft een software-oplossingen die onjuist berekende Hallo-prijzen en Hallo bestaande commerce gegevens die worden bediend door Hallo platform is beschadigd. Hier Hallo oplossing komen toorevert toohello zou worden eerdere versie van het Hallo-toepassings- en Hallo eerste. tooenable deze, nemen periodiek back-ups van uw systeem.

## <a name="disaster-recovery-solution-azure-backup-service"></a>Noodherstel: Azure Backup-Service

[Azure Backup-Service](https://azure.microsoft.com/services/backup/) kan worden gebruikt voor back-up en Noodherstel is, en dit proces werkt met [schijven beheerd](../../virtual-machines/windows/managed-disks-overview.md) , evenals [niet-beheerde schijven](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks). U kunt een back-uptaak maken met back-ups op basis van tijd, eenvoudig herstel van de virtuele machine en back-up bewaarbeleid. 

Als u [Premium-opslag schijven](storage-premium-storage.md), [schijven beheerd](../../virtual-machines/windows/managed-disks-overview.md), of andere schijftypen Hello [lokaal redundante opslag (LRS)](storage-redundancy.md#locally-redundant-storage) optie, het is vooral belangrijk tooleverage periodieke DR back-ups. Azure Backup opslaat Hallo-gegevens in de Recovery Services-kluis voor het bewaren van de lange termijn. Kies Hallo [geografisch redundante opslag (GRS)](storage-redundancy.md#geo-redundant-storage) optie voor Hallo back-up Recovery Services-kluis. Die zorgt ervoor dat back-ups zijn gerepliceerde tooa andere Azure-regio voor de beveiliging van regionale noodsituaties.

Voor [niet-beheerde schijven](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks), kunt u Hallo LRS opslagtype voor IaaS-schijven gebruiken, maar zorg ervoor dat de Azure Backup Hello GRS-optie voor Hallo Recovery Services-kluis is ingeschakeld.

**Als u Hallo [GRS](storage-redundancy.md#geo-redundant-storage)/[RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage) optie voor uw niet-beheerde schijven u nog steeds nodig toepassingsconsistente momentopnamen voor back-up en Noodherstel.** U moet een gebruiken [Azure Backup-Service](https://azure.microsoft.com/services/backup/) of [toepassingsconsistente momentopnamen](#alternative-solution-consistent-snapshots).

Hallo Hieronder volgt een samenvatting van oplossingen voor herstel na Noodgevallen.

| Scenario | Automatische replicatie | Oplossing voor Noodherstel |
| --- | --- | --- |
| *Premium-opslag-schijven* | Lokale ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Managed Disks* | Lokale ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Niet-beheerde LRS-schijven* | Lokale ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/) |
| *Niet-beheerde GRS schijven* | Cross-regio ([GRS](storage-redundancy.md#geo-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/)<br/>[Toepassingsconsistente momentopnamen](#alternative-solution-consistent-snapshots) |
| *Niet-beheerde RA-GRS-schijven* | Cross-regio ([RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage)) | [Azure Backup](https://azure.microsoft.com/services/backup/)<br/>[Toepassingsconsistente momentopnamen](#alternative-solution-consistent-snapshots) |

Hoge beschikbaarheid kan beste door voldaan door Hallo gebruik van beheerde schijven in een Beschikbaarheidsset samen met Azure Backup. Als u niet-beheerde schijven gebruikt, kunt u Azure back-up voor herstel na Noodgevallen. Als u toouse Azure Backup, duurt [toepassingsconsistente momentopnamen](#alternative-solution-consistent-snapshots) zoals beschreven in een volgende sectie is een alternatieve oplossing voor back-up en Noodherstel.

Uw keuzes voor hoge beschikbaarheid, back-up en Noodherstel op niveau van de toepassing of infrastructuur aan de onderstaande kan worden weergegeven:

| *Niveau* | Hoge beschikbaarheid   | Back-up-/ DR |
| --- | --- | --- |
| *Toepassing* | SQL AlwaysOn | Azure Backup |
| *Infrastructuur*  | Beschikbaarheidsset  | GRS met toepassingsconsistente momentopnamen |

### <a name="using-hello-azure-backup-service"></a>Met behulp van hello Azure Backup-Service

[Azure Backup](../../backup/backup-azure-vms-introduction.md) kunnen back-up van uw virtuele machines met Windows of Linux toohello Azure Recovery Services-kluis. Back-ups maken en herstellen van essentiële gegevens wordt bemoeilijkt door Hallo feit dat essentiële bedrijfsgegevens moet een back-up tijdens het Hallo-toepassingen die produceren Hallo gegevens worden uitgevoerd. tooaddress, biedt Azure Backup toepassingsconsistente back-ups voor Microsoft-werkbelastingen met behulp van Hallo Volume Shadow Service (VSS) tooensure dat gegevens worden geschreven correct toostorage. Voor virtuele Linux-machines zijn alleen bestandsconsistente back-ups mogelijk, aangezien Linux geen equivalente tooVSS functionaliteit.

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-1.png)   

Wanneer Azure Backup een back-uptaak op Hallo geplande tijdstip initieert, activeert het Hallo Backup-extensie in Hallo VM tootake een momentopname van een punt in tijd geïnstalleerd. Een momentopname wordt gemaakt in coördinatie met VSS tooget een consistente momentopname te maken van de schijven Hallo in Hallo virtuele machine zonder tooshut deze niet actief. Hallo Backup-extensie in Hallo VM leegmaakacties alle schrijfbewerkingen alvorens Hallo consistente momentopname te maken van alle Hallo-schijven. Nadat het Hallo-momentopname wordt gemaakt, worden Hallo gegevens worden overgedragen door Azure Backup toohello back-upkluis. toomake hello back-upproces efficiënter Hallo service identificeert en alleen Hallo blokken met gegevens die zijn gewijzigd sinds de laatste back-up Hallo overdraagt.


toorestore, kunt u weergeven Hallo beschikbare back-ups via Azure Backup en start vervolgens een herstelpunt. U kunt maken en herstellen van Azure back-ups via Hallo [Azure-portal](https://portal.azure.com/), [met behulp van PowerShell](../../backup/backup-azure-vms-automation.md ), of met behulp van Hallo [Azure CLI](https://docs.microsoft.com/azure/xplat-cli-install). Zie de Azure Backup voor meer informatie.

### <a name="steps-tooenable-backup"></a>Stappen tooEnable back-up

Hallo volgende stappen zijn gewoonlijk gebruikte tooenable back-ups van uw virtuele machines met behulp van Hallo [Azure Portal](https://portal.azure.com/). Er zijn enkele variaties afhankelijk van uw exacte scenario. Raadpleeg toohello [Azure Backup](../../backup/backup-azure-vms-introduction.md) documentatie voor volledige informatie. Azure back-up ook [biedt ondersteuning voor virtuele machines met schijven beheerd](https://azure.microsoft.com/blog/azure-managed-disk-backup/).

1.  Maak een recovery services-kluis voor een virtuele machine met behulp van Hallo stappen te volgen:

    a.  Met behulp van Hallo [Azure-portal](https://portal.azure.com/), alle resources te bladeren naar 'Recovery Services-kluizen'.

    b.  Op Hallo Recovery Services-kluizen menu en klik op toevoegen Volg Hallo stappen toocreate een nieuwe kluis in Hallo dezelfde regio bevinden als Hallo VM. Bijvoorbeeld, als uw virtuele machine zich in de regio VS-West, VS-West voor verzamelen Hallo kluis.

2.  Controleer of Storage-replicatie voor nieuw gemaakte kluis Hallo Hallo. toodo deze, toegang Hallo-kluis van Hallo Recovery Services-kluizen blade en gaat u naar toohello instellingen/back-configuratie. Zorg ervoor dat Hallo GRS-optie is standaard geselecteerd. Dit zorgt ervoor dat uw kluis automatisch gerepliceerde tooa secundaire datacenter is. Uw kluis in VS-West worden bijvoorbeeld automatisch gerepliceerde tooEast VS.

3.  Configureren van de back-upbeleid Hallo en selecteert u Hallo VM in Hallo dezelfde gebruikersinterface.

4.  Zorg ervoor dat Hallo die Backup-Agent is geïnstalleerd op Hallo VM. Als uw virtuele machine wordt gemaakt met behulp van een installatiekopie van een Azure-galerie, is al Hallo backup-agent geïnstalleerd. Anders (dat wil zeggen, als u een aangepaste installatiekopie), volg de instructies te[installeren Hallo VM-Agent op de virtuele machine van Hallo](../../backup/backup-azure-arm-vms-prepare.md#install-the-vm-agent-on-the-virtual-machine).

5.  Zorg ervoor dat Hallo VM kunt netwerkverbinding voor Hallo Backup-service toofunction. Volg deze instructies voor [netwerkverbinding](../../backup/backup-azure-arm-vms-prepare.md#network-connectivity).

6.  Zodra Hallo bovenstaande stappen zijn voltooid, wordt met regelmatige tussenpozen zoals opgegeven in de back-upbeleid Hallo Hallo back-up uitgevoerd. Indien nodig, kunt u Hallo eerste back-up handmatig van het kluisdashboard Hallo op Hallo Azure-portal activeren.

Voor het automatiseren van Azure Backup met behulp van scripts, Raadpleeg te[PowerShell-cmdlets voor VM-back-](../../backup/backup-azure-vms-automation.md).

### <a name="steps-for-recovery"></a>Stappen voor herstel

Als u toorepair moet of opnieuw opbouwen van een virtuele machine, kunt u Hallo VM herstellen vanaf een back-up herstelpunten in de kluis Hallo Hallo. Er zijn een aantal verschillende opties voor het uitvoeren van Hallo herstel:

1.  U kunt een nieuwe virtuele machine maken als een punt in tijd representatie van een back-up van de VM.

2.  Kunt u schijven Hallo herstellen en vervolgens Hallo-sjabloon gebruiken voor Hallo VM toocustomize en rebuild Hallo VM hersteld. 

Zie de instructies te[gebruik Azure portal toorestore virtuele machines](../../backup/backup-azure-arm-restore-vms.md#restoring-a-vm-during-azure-datacenter-disaster). Hallo document ook specifieke stappen voor het terugzetten van back-up VMs toohello gekoppeld datacenter met behulp van uw geografisch redundante back-upkluis in geval van een noodgeval op de primaire Datacenter Hallo HALLO hallo uitgelegd. In dat geval Hallo Compute-service van Hallo secundaire regio toocreate Hallo hersteld virtuele machine maakt gebruik van Azure Backup.

U kunt ook PowerShell voor [herstellen van een virtuele machine](../../backup/backup-azure-vms-automation.md#restore-an-azure-vm) of voor [schijven maken van een nieuwe virtuele machine uit hersteld](../../backup/backup-azure-vms-automation.md#create-a-vm-from-restored-disks).

## <a name="alternative-solution-consistent-snapshots"></a>Alternatieve oplossing: Toepassingsconsistente momentopnamen

Als u toouse hello Azure Backup-Service, kunt u uw eigen back-mechanisme met momentopnamen kunt implementeren. Het is ingewikkeld toocreate toepassingsconsistente momentopnamen voor alle schijven die worden gebruikt door een virtuele machine en vervolgens deze momentopnamen tooanother regio worden gerepliceerd. Om deze reden beschouwt Azure inzetten Hallo Backup-Service een betere optie dan een aangepaste oplossing bouwen. Als u met RA-GRS/GRS opslag voor schijven, zijn momentopnamen automatisch gerepliceerde tooa secundaire Datacenter. Als u LRS opslag voor schijven gebruikt, moet u tooreplicate Hallo gegevens zelf. Zie voor meer informatie [Back-up van Azure niet-beheerde VM-schijven met incrementele momentopnamen](../../virtual-machines/windows/incremental-snapshots.md).

Een momentopname is een weergave van een object op een bepaald punt in tijd. Een momentopname wordt in rekening gebracht facturering voor Hallo incrementele grootte van Hallo gegevens het blokkeringen. Zie voor meer informatie [momentopname maken van een blob](../blobs/storage-blob-snapshots.md).

### <a name="creating-snapshots-while-hello-vm-is-running"></a>Maken van momentopnamen terwijl de Hallo wordt VM uitgevoerd

Terwijl u een momentopname op elk gewenst moment uitvoeren kunt als hello VM wordt uitgevoerd, er zijn nog steeds gegevens gestreamd toohello schijven en Hallo momentopnamen gedeeltelijke bewerkingen die tijdens de vlucht waren kunnen bevatten. Ook als er meerdere schijven die zijn betrokken, Hallo momentopnamen van verschillende schijven mogelijk opgetreden op verschillende tijdstippen, wat betekent dat deze momentopnamen kunnen niet worden gecoördineerd. Dit is vooral problematisch voor striped volumes waarvan de bestanden beschadigd kunnen raken als wijzigingen tijdens de back-up wordt gemaakt.

tooavoid deze situatie Hallo back-upproces moet implementeren Hallo stappen te volgen:

1.  Blokkeert alle Hallo-schijven

2.  Alle Hallo wachtende schrijfopdrachten leegmaken

3.  Vervolgens [momentopname maken van een blob](../blobs/storage-blob-snapshots.md) voor alle schijven Hallo

Sommige Windows-toepassingen zoals SQL Server bieden een gecoördineerde back-mechanisme via VSS toocreate toepassingsconsistente back-ups. Op Linux, kunt u een hulpprogramma zoals fsfreeze voor het coördineren van Hallo schijven, zodat er bestandsconsistente back-ups, maar niet toepassingsconsistente momentopnamen. Dit proces is ingewikkeld, dus en moet u overwegen [Azure Backup](../../backup/backup-azure-vms-introduction.md) of een back-upoplossing van derden die dit al te implementeren.

Hallo hierboven proces resulteert in een verzameling van gecoördineerde momentopnamen voor alle Hallo VM-schijven, voor een bepaald punt in tijd weergave van Hallo VM. Dit is een back-up herstelpunt voor Hallo VM. U kunt geplande intervallen toocreate periodiek back-ups Hallo proces herhalen. Hieronder vindt u stappen hello te[kopie Hallo back-ups tooanother regio](#copy-the-snapshots-to-another-region) voor herstel na Noodgevallen.

### <a name="creating-snapshots-while-hello-vm-is-offline"></a>Het maken van momentopnamen terwijl de Hallo is VM offline

Een andere optie toocreate consistent back-ups wordt afgesloten Hallo VM en nemen blob momentopnamen van elke schijf. Dit is eenvoudiger dan coördinerende momentopnamen van een actieve virtuele machine, maar een paar minuten uitvaltijd is vereist. Bij dit proces wordt als volgt:

1. Hallo VM afsluiten.

2. Maak een momentopname van elke VHD-blob, die slechts enkele seconden duurt.

    toocreate een momentopname, kunt u [PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blob-snapshots), Hallo [Rest-API van Azure Storage](https://msdn.microsoft.com/library/azure/ee691971.aspx), [Azure CLI](https://docs.microsoft.com/azure/xplat-cli-install), of een hello Azure Storage-clientbibliotheken zoals [ Hallo Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/hh488361.aspx).

3. Hallo VM die Hallo uitvaltijd eindigt start. Doorgaans Hallo hele proces is voltooid binnen een paar minuten.

Dit proces resulteert in een verzameling van toepassingsconsistente momentopnamen voor alle Hallo-schijven, bieden van een back-up herstelpunt voor Hallo VM. Zie hieronder voor Hallo stappen toocopy Hallo momentopnamen tooanother regio voor herstel na Noodgevallen.

### <a name="copy-hello-snapshots-tooanother-region"></a>Hallo momentopnamen tooanother regio kopiëren

Maken van momentopnamen van Hallo alleen mogelijk niet voldoende is voor herstel na Noodgevallen. U moet ook Hallo momentopname back-ups tooanother regio worden gerepliceerd.

Als u van GRS of RA-GRS voor uw schijven gebruikmaakt, klikt u vervolgens Hallo momentopnamen zijn secundaire regio gerepliceerde toohello automatisch. Kan er een paar minuten vertraging vóór Hallo replicatie en als het primaire Datacenter Hallo uitvalt voordat Hallo momentopnamen voltooien repliceren, u zich niet kunnen tooaccess Hallo momentopnamen van Hallo secundaire Datacenter. Hallo kans hiervan is klein.

> [!Note] 
> Alleen met Hallo schijven in een GRS of RA-GRS-account biedt geen bescherming tegen Hallo VM van noodsituaties. U moet ook gecoördineerde momentopnamen maken of gebruiken van Azure Backup. Dit is vereiste toorecover VM tooa consistent maken.

Als u van LRS gebruikmaakt, kopieert u Hallo momentopnamen tooa ander opslagaccount onmiddellijk na het maken van een momentopname Hallo. doel voor het kopiëren van Hallo mogelijk een LRS storage-account in een andere regio, wat resulteert in het Hallo-exemplaar wordt in een externe regio. U kunt ook Hallo momentopname tooan RA-GRS-opslagaccount in Hallo kopiëren dezelfde regio. In dit geval Hallo momentopname worden vertraagd gerepliceerde toohello externe secundaire regio. Uw back-up is beveiligd tegen rampen op de primaire site Hallo zodra de Hallo kopiëren en replicatie is voltooid.

toocopy uw incrementele momentopnamen voor herstel na Noodgevallen controleren efficiënt, Hallo-instructies in [Back-up van Azure niet-beheerde VM-schijven met incrementele momentopnamen](../../virtual-machines/windows/incremental-snapshots.md).

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-2.png)   

### <a name="recovery-from-snapshots"></a>Herstel van momentopnamen

tooretrieve een momentopname, kopieert u het toomake een nieuwe blob. Als u Hallo momentopname van Hallo primaire account kopieert, kunt u Hallo momentopname via toohello base blob van Hallo momentopname, dus omzetten Hallo schijf toohello momentopname; kopiëren Dit staat bekend als Hallo momentopname te promoveren. Als u kopieert Hallo momentopnameback-up van een secundaire account (in geval van Hallo van RA-GRS), moet dit tooa primaire account gekopieerd. U kunt een momentopname kopiëren [met behulp van PowerShell](storage-powershell-guide-full.md#how-to-copy-a-snapshot-of-a-blob) of met behulp van Hallo AzCopy hulpprogramma. Zie voor meer informatie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md).

In geval Hallo van virtuele machines met meerdere schijven, moet u kopiëren alle momentopnamen Hallo die deel uitmaken van dezelfde gecoördineerd Hallo herstelpunt. Zodra u Hallo momentopnamen toowritable VHD-blobs kopieert, kunt u Hallo blobs toorecreate uw virtuele machine met behulp van Hallo-sjabloon voor Hallo VM.

## <a name="other-options"></a>Andere opties

### <a name="sql-server"></a>SQL Server

SQL Server wordt uitgevoerd op een virtuele machine heeft een eigen toobackup ingebouwde mogelijkheden voor uw SQL Server-database tooAzure Blob-opslag of een bestandsshare. Als Hallo opslagaccount GRS of RA-GRS is, kunt u deze back-ups in de secundaire Datacenter Hallo van het opslagaccount in geval van een noodgeval Hallo openen met dezelfde beperkingen Hallo zoals eerder besproken. Zie voor meer informatie [back-up en herstel voor SQL Server in Azure Virtual Machines](../../virtual-machines/windows/sql/virtual-machines-windows-sql-backup-recovery.md). In de toevoeging toobackup and restore [SQL Server altijd op beschikbaarheidsgroepen](../../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md) secundaire replica's van databases toogreatly verkorten Hallo disaster recovery kunt onderhouden.

## <a name="other-considerations"></a>Andere overwegingen

In dit artikel is besproken hoe toobackup of nemen momentopnamen van uw virtuele machines en hun schijven toosupport-noodherstel en hoe toouse die toorecover. Met hello Azure Resource Manager-model, veel mensen gebruiken sjablonen toocreate hun virtuele machines en andere infrastructuur in Azure. U kunt een sjabloon toocreate een virtuele machine die Hallo heeft dezelfde configuratie elke keer. Als u aangepaste installatiekopieën gebruikt voor het maken van uw virtuele machines, moet u ook controleren de afbeeldingen zijn beveiligd met een account RA-GRS toostore ze.

Uw back-upproces mogelijk als gevolg daarvan kan een combinatie van twee dingen:

1. Back-up Hallo-gegevens (schijven)
2. Back-up Hallo-configuratie (sjablonen, aangepaste installatiekopieën)

Afhankelijk van de back-optie Hallo die u kiest, moet u wellicht toohandle Hallo back-up van de configuratie voor zowel Hallo gegevens als Hallo of Hallo Backup-service al die voor u kan verwerken.

## <a name="appendix---understanding-hello-impact-of-lrs-grs-and-ra-grs"></a>Bijlage - Hallo impact van LRS GRS en RA-GRS begrijpt

Voor de storage-accounts in Azure, er zijn drie typen van de redundantie van de gegevens die u met betrekking tot noodherstel – lokaal redundante (LRS) geografisch redundante (GRS overwegen moet) of geografisch redundante met lezen toegang (RA-GRS). 

Lokaal redundante opslag (LRS) drie kopieën van gegevens in Hallo Hallo behoudt hetzelfde Datacenter. Bij het schrijven van gegevens hello, worden alle drie kopieën worden bijgewerkt voordat geslaagd toohello-aanroeper wordt geretourneerd, zodat u weet dat ze identiek zijn. De schijf is beveiligd tegen lokale stroomstoringen, omdat het is zeer onwaarschijnlijk dat alle drie kopieën Hallo zou worden beïnvloed hetzelfde moment. In geval van LRS Hallo is er geen geografische redundantie, zodat Hallo schijf is niet beveiligd tegen onherstelbare fouten die invloed op een volledige data center of de opslag-eenheid hebben kunnen.

Met GRS en RA-GRS drie kopieën van uw gegevens worden bewaard in de primaire regio hello (u hebt geselecteerd) en drie extra kopieën van uw gegevens blijven behouden in een bijbehorende secundaire regio (ingesteld door Azure). Bijvoorbeeld, als u gegevens in VS-West opslaat, Hallo gegevens worden gerepliceerde tooEast VS. Dit asynchroon wordt gedaan en er is een kleine vertraging tussen updates toohello primaire en secundaire. Replica's van schijven op de secundaire site Hallo Hallo consistent op basis van per schijf (met Hallo vertraging) zijn, maar de replica's van meerdere actieve schijven mogelijk niet synchroon **met elkaar**. replica's consistent over meerdere schijven, toepassingsconsistente momentopnamen toohave nodig zijn.

Hallo belangrijkste verschil tussen GRS en RA-GRS is met RA-GRS, kunt u secundaire kopie Hallo lezen op elk gewenst moment. Als er een probleem dat Hallo-gegevens in de primaire regio Hallo niet toegankelijk samenstelt is, brengt Hallo team van Azure elke inspanning toorestore toegang. Tijdens het Hallo primaire niet beschikbaar is, hebt u RA-GRS is ingeschakeld, kunt u toegang tot Hallo-gegevens in Hallo secundaire Datacenter. Dus als u van plan tooread van Hallo replica bent als primaire Hallo niet toegankelijk is, moet klikt u vervolgens RA-GRS worden overwogen.

Als het een aanzienlijke onderbreking toobe blijkt, mag de Hallo team van Azure activeert u een geo-failover en Hallo primaire DNS-vermeldingen toopoint toosecondary opslag wijzigen. Als u beide GRS of RA-GRS ingeschakeld, kunt u op dit moment Hallo-gegevens in het Hallo-regio die toobe Hallo secundaire gebruikt openen. Met andere woorden, als uw opslagaccount GRS is en er een probleem is, u kunt toegang tot Hallo secundaire opslag alleen als er een geo-failover.

Zie voor meer informatie [welke toodo als een Azure Storage-storing optreedt,](storage-disaster-recovery-guidance.md). 

Houd er rekening mee dat Microsoft kan bepalen of er een failover plaatsvindt. Failover niet per storage-account wordt beheerd, wordt daarom niet besloten door individuele klanten. tooimplement herstel na noodgevallen voor specifieke storage-accounts of schijven op virtuele machine, moet u Hallo technieken die hierboven is beschreven in dit artikel gebruiken.
