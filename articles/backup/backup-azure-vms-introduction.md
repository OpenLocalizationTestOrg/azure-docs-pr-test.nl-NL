---
title: aaaPlanning uw back-upinfrastructuur VM in Azure | Microsoft Docs
description: Belangrijke overwegingen bij het plannen van tooback van virtuele machines in Azure
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: back-up van virtuele machines, back-up van virtuele machines
ms.assetid: 19d2cf82-1f60-43e1-b089-9238042887a9
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: d11982431610000293038ee6aa7df8e7bc2d8b70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-your-vm-backup-infrastructure-in-azure"></a>De infrastructuur voor back-ups van virtuele Azure-machines plannen
In dit artikel biedt de prestaties en resource suggesties toohelp u van plan bent uw VM-back-infrastructuur. Definieert ook belangrijke aspecten van Hallo Backup-service; deze aspecten kunnen essentieel bij het bepalen van uw architectuur zijn capaciteitsplanning en planning. Als u hebt [uw omgeving voorbereid](backup-azure-vms-prepare.md), planning Hallo volgende stap is voordat u begint met [tooback om zo VM's](backup-azure-vms.md). Als u meer informatie over virtuele machines in Azure nodig hebt, raadpleegt u Hallo [documentatie Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="how-does-azure-back-up-virtual-machines"></a>Hoe biedt Azure back-up van virtuele machines?
Wanneer een back-uptaak hello Azure Backup-service op Hallo geplande tijdstip begint, activeert het Hallo Backup-extensie tootake een momentopname van een punt in tijd. Hello Azure Backup-service gebruikt Hallo _VMSnapshot_ de extensie in de Windows- en Hallo _VMSnapshotLinux_ extensie in Linux. Hallo-extensie wordt geïnstalleerd tijdens Hallo eerste VM back-up. tooinstall Hallo-extensie, Hallo VM moet worden uitgevoerd. Als hello VM niet wordt uitgevoerd, wordt Hallo Backup-service een momentopname van Hallo onderliggende opslag (omdat er geen schrijfbewerkingen toepassing tijdens het Hallo die VM is gestopt optreden).

Bij het nemen van een momentopname van VM's van Windows coördineert hello Backup-service met Hallo Volume Shadow Copy Service (VSS) tooget een consistente momentopname te maken van schijven Hallo virtuele machine. Als u een back-up van Linux VM's, kunt u uw eigen aangepaste scripts tooensure consistentie schrijven bij het maken van een VM-momentopname. Verderop in dit artikel vindt u meer informatie over het aanroepen van deze scripts.

Zodra hello Azure Backup-service Hallo momentopname maakt, is Hallo gegevens overgedragen toohello kluis. toomaximize-efficiëntie Hallo service identificeert en alleen Hallo blokken met gegevens die zijn gewijzigd sinds de vorige back-up Hallo overdraagt.

![Virtuele machine van Azure Backup-architectuur](./media/backup-azure-vms-introduction/vmbackup-architecture.png)

Hallo-gegevensoverdracht is voltooid, Hallo momentopname wordt verwijderd als een herstelpunt wordt gemaakt.

> [!NOTE]
> 1. Tijdens de back-upproces hello bevat Azure Backup geen Hallo tijdelijke schijf is gekoppeld aan toohello virtuele machine. Zie voor meer informatie Hallo blog op [tijdelijke opslag](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/).
> 2. Omdat Azure Backup wordt een momentopname van het niveau van de opslag en overdrachten die toovault momentopname, veranderen niet Hallo opslagaccountsleutels totdat Hallo back-uptaak is voltooid.
> 3. Voor VM's voor premium kopieert u Hallo momentopname toostorage account. Dit is toomake ervoor dat Azure Backup-service voldoende IOP's voor het overbrengen van gegevens toovault opgehaald. Deze extra exemplaar van de opslag is in rekening gebracht volgens de Hallo VM toegewezen grootte. 
>

### <a name="data-consistency"></a>Gegevensconsistentie
Een back-up en herstellen van essentiële bedrijfsgegevens wordt bemoeilijkt door Hallo feit die bedrijfskritieke gegevens moet een back-up tijdens het Hallo-toepassingen die produceren Hallo gegevens worden uitgevoerd. tooaddress deze, Azure Backup ondersteunt toepassingsconsistente back-ups voor zowel Windows als een virtuele Linux-machines
#### <a name="windows-vm"></a>Windows VM
Azure Backup VSS volledige back-ups neemt op VM's van Windows (meer informatie over [VSS volledige back-up](http://blogs.technet.com/b/filecab/archive/2008/05/21/what-is-the-difference-between-vss-full-backup-and-vss-copy-backup-in-windows-server-2008.aspx)). tooenable VSS back-ups, Hallo register basisbehoeften toobe ingesteld op Hallo VM te volgen.

```
[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
"USEVSSCOPYBACKUP"="TRUE"
```

#### <a name="linux-vms"></a>Virtuele Linux-machines
Azure Backup biedt een scripting-framework. tooensure toepassing consistentie back-ups van virtuele Linux-machines, maak aangepaste scripts voor vóór en na scripts waarmee Hallo back-werkstroom en de omgeving. Azure Backup Hallo vooraf script aanroept alvorens Hallo VM-momentopname en Hallo na script wordt aangeroepen wanneer de VM-momentopnametaak Hallo is voltooid. Zie voor meer informatie [toepassing consistente VM-back-ups met behulp van script voor vóór en na](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).
> [!NOTE]
> Azure Backup alleen roept Hallo klant geschreven vóór en na-scripts. Als het Hallo-script voor vóór en na scripts probleemloos worden uitgevoerd, markeert Azure Backup Hallo herstelpunt als toepassing consistente. Hallo klant is echter die verantwoordelijk is voor Hallo toepassing consistentie bij gebruik van aangepaste scripts.
>


De volgende tabel beschrijft de consistentie en Hallo voorwaarden dat ze onder tijdens de back-up van de virtuele machine van Azure optreden- en herstelprocedures Hallo typen.

| Consistentie | Op basis van VSS | Uitleg en details |
| --- | --- | --- |
| Consistentie van toepassingen |Ja voor Windows|Consistentie van de toepassing is ideaal voor workloads zoals zorgt ervoor dat:<ol><li> Hallo VM *opgestart*. <li>Er is *geen beschadiging*. <li>Er is *zonder verlies van gegevens*.<li> Hallo-gegevens is consistent toohello-toepassing die gebruikmaakt van Hallo-gegevens met betrekking tot Hallo toepassing tijdens het Hallo van back-up--met VSS of vooraf/post-script.</ol> <li>*VM's van Windows*-meest Microsoft-werkbelastingen VSS-schrijvers die specifiek acties gerelateerde toodata consistentiecontrole hebben. Microsoft SQL Server heeft bijvoorbeeld een VSS-schrijver dat ervoor zorgt dat Hallo schrijfbewerkingen toohello transactielogbestand en Hallo database correct uitgevoerd. Voor virtuele machine van Windows Azure back-ups, toocreate een toepassingsconsistente herstelpunt moet Hallo Backup-extensie Hallo VSS workflow aanroepen en deze zijn voltooid voordat het VM-momentopname Hallo. Voor hello Azure VM-momentopname toobe nauwkeurige, moeten ook Hallo VSS-schrijvers van alle virtuele machine van Azure-toepassingen uitvoeren. (Meer informatie over Hallo [basisprincipes van VSS](http://blogs.technet.com/b/josebda/archive/2007/10/10/the-basics-of-the-volume-shadow-copy-service-vss.aspx) en duik diep in de details op Hallo van [hoe het werkt](https://technet.microsoft.com/library/cc785914%28v=ws.10%29.aspx)). </li> <li> *Virtuele Linux-machines*-klanten kunnen uitvoeren [aangepast script voor vóór en na tooensure toepassing consistentie](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent). </li> |
| Consistentie van bestandssysteem |Ja - voor Windows-computers |Er zijn twee scenario's waarbij Hallo herstelpunt kan zijn *bestandssysteem consistente*:<ul><li>Back-ups van virtuele Linux-machines in Azure, zonder pre-script/na-script of als pre-script/na-script is mislukt. <li>VSS-fout tijdens back-up voor Windows-machines in Azure.</li></ul> In beide gevallen wordt aanbevolen Hallo die kan worden uitgevoerd is tooensure die: <ol><li> Hallo VM *opgestart*. <li>Er is *geen beschadiging*.<li>Er is *zonder verlies van gegevens*.</ol> Toepassingen moeten hun eigen 'bijwerken' tooimplement mechanisme op Hallo hersteld gegevens. |
| Consistentie van de crash |Nee |Deze situatie is gelijkwaardig tooa virtuele machine 'vastlopen van een' ondervindt (via ofwel een zacht of hard reset). Consistentie van de crash gebeurt meestal wanneer hello Azure virtuele machine wordt afgesloten tijdens het Hallo van back-up. Een crashconsistent herstelpunt biedt geen garanties rond Hallo consistentie van Hallo gegevens op Hallo opslagmedium--vanuit het perspectief van Hallo-besturingssysteem of toepassing hello Hallo. Alleen Hallo-gegevens die al op de schijf Hallo toen Hallo back-up bestaat worden vastgelegd en back-up gemaakt. <br/> <br/> Hoewel er geen garanties, meestal, Hallo besturingssysteem wordt geladen, gevolgd door het controleren van de schijf procedure, zoals chkdsk toofix Beschadigingsfouten. Alle gegevens in het geheugen of schrijfbewerkingen die niet overgedragen toohello schijf zijn gaan verloren. Hallo toepassing volgt doorgaans met een eigen verificatie-mechanisme voor het geval gegevens terugdraaien toobe gedaan. <br><br>Bijvoorbeeld als transactielogboek Hallo vermeldingen die niet aanwezig in Hallo-database heeft vervolgens Hallo database-software geen terugdraaien totdat Hallo gegevens consistent is. Wanneer gegevens worden verspreid over meerdere virtuele schijven (zoals spanned volumes), biedt een crashconsistent herstelpunt geen garanties voor Hallo juistheid van Hallo-gegevens. |

## <a name="performance-and-resource-utilization"></a>Prestatie- en -gebruik
Zoals back-upsoftware die geïmplementeerde on-premises, moet u plannen voor de capaciteit en brongebruik behoeften back-ups van virtuele machines in Azure. Hallo [Azure Storage beperkt](../azure-subscription-service-limits.md#storage-limits) definiëren welke toostructure VM-implementaties tooget maximale prestaties met minimale gevolgen hebben voor toorunning werkbelastingen.

Betalen aandacht toohello die volgende Azure Storage beperkt bij het plannen van back-upprestaties:

* Maximum aantal uitgaande per storage-account
* Percentage van totaal aantal aanvragen per storage-account

### <a name="storage-account-limits"></a>Limieten voor opslagaccounts
Back-upgegevens gekopieerd van een opslagaccount, toohello i/o-bewerkingen per seconde (IOPS) en uitgaande (of doorvoer) metrieken van Hallo storage-account toegevoegd. AT Hallo dezelfde tijd, virtuele machines ook IOPS en doorvoerlimieten verbruiken. Hallo-doel is tooensure back-up en verkeer van virtuele machines niet langer zijn dan de limieten voor opslagaccounts.

### <a name="number-of-disks"></a>Aantal schijven
back-upproces Hallo probeert een back-uptaak toocomplete zo snel mogelijk. In dat geval, verbruikt deze zo veel resources geplaatst. Echter alle i/o-bewerkingen worden beperkt door Hallo *doel doorvoer voor één Blob*, die heeft een limiet van 60 MB per seconde. In een poging toomaximize snelheid van de back-upproces Hallo probeert tooback van elk van de schijven van de VM Hallo *parallel*. Als een virtuele machine vier schijven heeft, probeert Hallo service tooback van alle vier schijven parallel. Hallo **aantal schijven** Hallo belangrijkste factor bij het bepalen van de back-opslagverkeer account back-up wordt gemaakt is.

### <a name="backup-schedule"></a>Back-upschema
Een extra factor die invloed op prestaties is Hallo **back-upschema**. Als u Hallo-beleid configureren zodat alle VM's zijn een back-up op Hallo dezelfde tijd, hebt u een verkeer is vastgelopen gepland. back-upproces Hallo probeert tooback van alle schijven parallel. tooreduce hello back-upverkeer van een opslagaccount, maakt u een back-up van andere virtuele machines op verschillende tijdstip hello, zonder overlap.

## <a name="capacity-planning"></a>Capaciteitsplanning
Het samenstellen van de vorige factoren hello, moet u tooplan voor account Hallo-gebruik opslagbehoeften. Hallo downloaden [VM back-capaciteitsplanning Excel-spreadsheet](https://gallery.technet.microsoft.com/Azure-Backup-Storage-a46d7e33) toosee Hallo impact van de schijf en de back-upschema keuzes.

### <a name="backup-throughput"></a>Back-doorvoer
Voor elke schijf back-up wordt gemaakt, Azure Backup Hallo blokken op Hallo schijf leest en winkels Hallo alleen gewijzigde gegevens (incrementele back-up). Hallo toont volgende tabel Hallo gemiddelde back-up service doorvoer waarden. Hallo volgt gegevens gebruikt, kunt u schatten Hallo hoeveelheid tijd die nodig zijn tooback van een schijf van een opgegeven grootte.

| Back-upbewerking | Gunstigste doorvoer |
| --- | --- |
| Eerste back-up |160 Mbps |
| Incrementele back-up (DR) |640 Mbps <br><br> Doorvoer neerzetten aanzienlijk als Hallo gewijzigd (benodigde gegevens een back-up toobe) worden verdeeld over over Hallo schijf.|

## <a name="total-vm-backup-time"></a>Totale tijd voor VM-back-up
Hoewel de meeste van de back-uptijd Hallo is besteed aan het lezen van en kopiëren van gegevens, dragen andere bewerkingen toohello totale tijd die nodig is tooback van een virtuele machine:

* Tijd die nodig is te[installeren of bijwerken van de Backup-extensie Hallo](backup-azure-vms.md).
* Momentopname-tijd die Hallo tijd tootrigger een momentopname is. Momentopnamen zijn triggered sluiten toohello geplande back-uptijd.
* Wachttijd in. Aangezien Hallo Backup-service met het verwerken van de back-ups van meerdere klanten, kopiëren van back-upgegevens in momentopname toohello back-up of herstelservices kluis mogelijk niet onmiddellijk starten. Hallo wacht kan in tijden van piekbelasting stretch tooeight uur vanwege toohello aantal back-ups wordt verwerkt. Hallo totale VM tijdstip back-up is echter minder dan 24 uur voor dagelijkse back-upbeleid.
* Gegevens overdrachtstijd, tijd die nodig is voor back-up toocompute Hallo incrementele wijzigingen van eerdere back-up-service en de opslag van deze wijzigingen toovault overdragen.

### <a name="why-am-i-observing-longer12-hours-backup-time"></a>Waarom heb ik observeren longer(>12 hours) back-up van tijd?
Back-up bestaat uit twee fasen: maken van momentopnamen en het overdragen van Hallo momentopnamen toohello kluis. Hallo Backup-service wordt geoptimaliseerd voor opslag. Bij de overdracht van Hallo momentopname gegevens tooa kluis draagt Hallo service alleen incrementele wijzigingen van de vorige momentopname Hallo.  toodetermine hello incrementele wijzigingen, Hallo service berekent Hallo controlesom Hallo-blokken. Als een blok is gewijzigd, wordt Hallo blok geïdentificeerd als een blok toobe toohello kluis verzonden. Vervolgens vastgesteld Hallo service zoomt verder in elk van de Hallo blokken, verkoopkansen toominimize Hallo gegevens tootransfer zoekt. Na het evalueren van alle gewijzigde blokken Hallo service voegt Hallo wijzigingen samen en verzendt deze toohello kluis. Kleine, gefragmenteerde schrijfbewerkingen zijn in sommige oudere toepassingen niet optimaal is voor de opslag. Als Hallo momentopname veel kleine, gefragmenteerde schrijfbewerkingen bevat, besteedt Hallo service extra tijd Hallo gegevens geschreven door Hallo-toepassingen verwerken. Hallo toepassing schrijven blok van Azure, aanbevolen voor toepassingen die worden uitgevoerd binnen Hallo VM, is een minimum van 8 KB. Als uw toepassing gebruikmaakt van een blok van minder dan 8 KB, worden back-upprestaties gedaan. Zie voor hulp bij het afstemmen van de back-prestaties van uw toepassing tooimprove, [afstemming van toepassingen voor optimale prestaties met Azure storage](../storage/common/storage-premium-storage-performance.md). Hoewel Hallo artikel op back-upprestaties gebruikgemaakt wordt van Premium storage voorbeelden, geldt Hallo richtlijnen voor Standard-opslag-schijven.

## <a name="total-restore-time"></a>Totaal aantal terugzetten
Een herstelbewerking bestaat uit twee belangrijkste sub taken: gegevens kopiëren van Hallo kluis toohello gekozen klant storage-account en het Hallo virtuele machine maken. Kopiëren van gegevens van het Hallo-kluis, is afhankelijk van waar back-ups Hallo intern worden opgeslagen in Azure en waar Hallo klant storage-account is opgeslagen. Toocopy gegevens van de tijd is afhankelijk van:
* Wachttijd in wachtrij keer - omdat Hallo serviceprocessen hersteltaken van meerdere klanten op Hallo hetzelfde moment restore-aanvragen zijn in een wachtrij plaatsen.
* Het kopiëren van gegevens keer - gegevens van Hallo kluis toohello klant storage-account is gekopieerd. Terugzetten tijd is afhankelijk van IOPS en doorvoer Azure Backup-service opgehaald op Hallo geselecteerd klant storage-account. tooreduce Hallo tijdens het herstelproces Hallo kopiëren, selecteert u een opslagaccount die niet worden geladen met een andere toepassing geschreven en gelezen.

## <a name="best-practices"></a>Aanbevolen procedures
We raden na deze procedures bij het configureren van de back-ups voor virtuele machines:

* Niet meer dan 10 klassieke virtuele machines van dezelfde service tooback up cloud op Hallo Hallo plannen hetzelfde moment. Als u tooback van meerdere virtuele machines in dezelfde cloudservice wilt, spreiden begintijden van Hallo back-up van een uur.
* Meer dan 40 VMs tooback op Hallo niet plannen van hetzelfde moment.
* VM-back-ups plannen tijdens daluren. Deze manier Hallo Backup-service gebruikt IOP's voor het overbrengen van gegevens van Hallo klant account toohello opslagkluis.
* Zorg ervoor dat er een beleid wordt toegepast op virtuele machines die zijn verdeeld over verschillende opslagaccounts. We raden niet meer dan 20 totaal aantal schijven van een enkele storage-account worden beveiligd door Hallo dezelfde back-upschema. Als u meer dan 20 schijven in een opslagaccount verspreiden Hallo die virtuele machines over meerdere beleidsregels tooget vereist IOPS tijdens Hallo overdracht fase van de back-upproces Hallo.
* Een virtuele machine uitgevoerd op de Premium-opslag toosame storage-account niet terugzetten. Als het Hallo-herstelproces bewerking samenvalt met de back-upbewerking hello, vermindert Hallo beschikbaar IOP's voor back-up.
* Premium VM back-up, zorg ervoor dat dit opslagaccount of premium-schijven voor hosts is ten minste 50% vrije ruimte voor het Faseren van momentopname voor een goede back-up. 
* Zorg ervoor dat python-versie op de virtuele Linux-machines ingeschakeld voor back-up 2.7 is

## <a name="data-encryption"></a>Gegevensversleuteling
Azure Backup biedt gegevens als onderdeel van de back-upproces Hallo niet coderen. Echter kunt versleutelen gegevens binnen Hallo VM en maak een back-up van Hallo beveiligde gegevens naadloos (meer informatie over [back-up van de versleutelde gegevens](backup-azure-vms-encryption.md)).

## <a name="calculating-hello-cost-of-protected-instances"></a>Berekening van Hallo kosten van beveiligde instanties
Azure virtuele machines die worden ondersteund door Azure Backup te zijn onderworpen[prijzen van Azure Backup](https://azure.microsoft.com/pricing/details/backup/). Hallo beveiligd exemplaren berekening is gebaseerd op Hallo *werkelijke* grootte van Hallo virtuele machine, die Hallo som van alle Hallo-gegevens in Hallo virtuele machine is--met uitzondering van Hallo 'resource disk' genoemd.

Prijzen voor back-ups van virtuele machines is *niet* op basis van Hallo ondersteund maximale grootte voor elke virtuele machine voor gegevens schijf gekoppelde toohello. Prijzen is gebaseerd op Hallo van de werkelijke gegevens opgeslagen in de gegevensschijf Hallo. Op deze manier is Hallo back-upopslag factuur gebaseerd op Hallo hoeveelheid gegevens die is opgeslagen in Azure Backup Hallo som van Hallo werkelijke gegevens in elk herstelpunt.

Een standaard A2 grote virtuele machine die twee extra gegevensschijven met een maximale grootte van 1 TB heeft bijvoorbeeld op te halen. Hallo bevat volgende tabel Hallo actuele gegevens opgeslagen op elk van deze schijven:

| Schijftype | Maximale grootte | Werkelijke gegevens aanwezig |
| --- | --- | --- |
| Besturingssysteemschijf |1023 GB |17 GB |
| Lokale schijf / Resource-schijf |135 GB |5 GB (niet voor back-up opgenomen) |
| Gegevensschijf 1 |1023 GB |30 GB |
| Gegevensschijf 2 |1023 GB |0 GB |

Hallo *werkelijke* grootte van Hallo virtuele machine wordt in dit geval 17 GB + 30 GB + 0 GB = 47 GB. De grootte van deze beveiligde exemplaar (47 GB) wordt Hallo basis voor de maandelijkse factuur Hallo. Als Hallo groeit hoeveelheid gegevens in de virtuele machine van Hallo, Hallo beveiligd exemplaargrootte gebruikt voor facturering wijzigingen dienovereenkomstig.

Facturering start niet totdat Hallo eerste geslaagde back-up is voltooid. Op dit moment begint Hallo facturering voor zowel opslag als beveiligd exemplaren. Facturering geldt zolang er *een back-up van gegevens die zijn opgeslagen in een kluis* voor Hallo virtuele machine. Als u de beveiliging op Hallo virtuele machine stoppen, maar de back-upgegevens virtuele machine in een kluis bestaat, blijft de facturering.

Financieel voor een opgegeven virtuele machine stopt alleen als het Hallo-beveiliging is gestopt *en* alle back-gegevens worden verwijderd. Wanneer de beveiliging stopt en er zijn geen actieve taken voor de back-up, Hallo grootte van Hallo laatste geslaagde VM back-up wordt Hallo beveiligd exemplaargrootte gebruikt voor de maandelijkse factuur Hallo.

## <a name="questions"></a>Vragen?
Als u vragen hebt of als er een functie die u toosee opgenomen wilt, [Stuur ons feedback](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Volgende stappen
* [Back-up van virtuele machines](backup-azure-vms.md)
* [Back-up van virtuele machine beheren](backup-azure-manage-vms.md)
* [Virtuele machines herstellen](backup-azure-restore-vms.md)
* [VM-back-problemen](backup-azure-vms-troubleshoot.md)
