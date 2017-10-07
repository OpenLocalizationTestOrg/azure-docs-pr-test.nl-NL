---
title: aaaWhat is Azure Backup? | Microsoft Docs
description: Gebruik Azure Backup tooback en herstellen van gegevens en werkbelastingen van Windows-Servers, Windows-werkstations, System Center DPM-servers en virtuele machines in Azure.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: back-up en herstel; Recovery Services; back-upoplossingen
ms.assetid: 0d2a7f08-8ade-443a-93af-440cbf7c36c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/11/2017
ms.author: markgal;trinadhk;anuragm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 953a19600f67a6b7451f71b1e3234d913816d18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-features-in-azure-backup"></a>Overzicht van Hallo-functies in Azure Backup
Azure Backup is Hallo op basis van een Azure-service u kunt tooback gebruikt (of beveiligen) en het herstellen van uw gegevens in Hallo Microsoft cloud. Met Azure Backup vervangt u uw bestaande on-premises of off-site back-upoplossing door een betrouwbare, veilige en kostenbesparende cloudoplossing. Azure Backup biedt meerdere onderdelen die u downloadt en implementeert op de desbetreffende computer hello, server of in de cloud Hallo. Hallo-onderdeel of agent, die u implementeert, is afhankelijk van wat u wilt tooprotect. Alle Azure Backup-onderdelen (ongeacht of u gegevens die lokaal beveiligen wilt of in de cloud Hallo) kunnen worden gebruikt tooback up gegevens tooa Recovery Services-kluis in Azure. Zie Hallo [Azure Backup-onderdelen tabel](backup-introduction-to-azure-backup.md#which-azure-backup-components-should-i-use) (verderop in dit artikel) voor meer informatie over welke specifieke gegevens van onderdeel toouse tooprotect, toepassingen of werkbelastingen.

[Een video-overzicht van Azure Backup bekijken](https://azure.microsoft.com/documentation/videos/what-is-azure-backup/)

## <a name="why-use-azure-backup"></a>Waarom Azure Backup gebruiken?
Traditionele back-upoplossingen hebt ontwikkeld tootreat Hallo cloud als een eindpunt of statische opslaglocatie soortgelijke toodisks of tape. Terwijl deze benadering is een eenvoudige is beperkt en niet profiteren van een onderliggend cloudplatform die tooan dure, inefficiënt oplossing omzet. Andere oplossingen zijn dure omdat u uiteindelijk betaalt voor Hallo verkeerd type opslag of opslag die u niet nodig. Andere oplossingen zijn vaak inefficiënt omdat ze niet u Hallo type of de hoeveelheid opslagruimte die u moet aanbieden of te veel tijd in beslag nemen administratieve taken. Azure Backup biedt daarentegen deze belangrijke voordelen:

**Automatische opslagbeheer** - hybride omgevingen vereisen vaak heterogene opslag - sommige lokale en andere in een cloud Hallo. Met Azure Backup zijn er geen kosten voor het gebruik van on-premises opslagapparaten. De back-upopslag wordt automatisch door Azure Backup toegewezen en beheerd en u betaalt naar gebruik. Betalen-als-gebruik betekent dat u betaalt alleen voor Hallo opslag die u wilt gebruiken. Zie voor meer informatie, Hallo [Azure prijzen artikel](https://azure.microsoft.com/pricing/details/backup).

**Onbeperkt schalen** - Hallo onderliggende power maakt gebruik van Azure Backup en onbeperkt schalen van hello Azure cloud toodeliver hoge beschikbaarheid - met geen onderhoud of bewaking overhead. U kunt waarschuwingen tooprovide informatie over gebeurtenissen instellen, maar u hoeft niet tooworry over hoge beschikbaarheid voor uw gegevens in de cloud Hallo.

**Meerdere opslagopties**: een aspect van hoge beschikbaarheid is opslagreplicatie. Azure Backup biedt twee typen replicatie: [lokaal redundante opslag](../storage/common/storage-redundancy.md#locally-redundant-storage) en [geografisch redundante opslag](../storage/common/storage-redundancy.md#geo-redundant-storage). Optie Hallo back-upopslag op basis van behoeften:

* Uw gegevens driemaal (deze maakt drie kopieën van uw gegevens) in een gekoppeld datacenter in Hallo lokaal redundante opslag (LRS) gerepliceerd dezelfde regio. LRS is een goedkope optie voor het beschermen van uw gegevens tegen lokale hardwarefouten.

* Geografisch redundante opslag (GRS) repliceert uw gegevens tooa secundaire regio (honderden mijl weg van de primaire locatie Hallo Hallo brongegevens). GRS is duurder dan LRS, maar biedt een hoger duurzaamheidsniveau voor uw gegevens, zelfs in geval van een regionale onderbreking.

**Onbeperkte gegevensoverdracht** : Azure Backup brengt geen beperking op Hallo hoeveelheid binnenkomende of uitgaande gegevens u overdraagt. Azure Backup ook rekening geen voor Hallo-gegevens die worden overgedragen. Als u hello Azure Import/Export-service tooimport grote hoeveelheden gegevens, er is echter een kosten in verband met binnenkomende gegevens. Zie [Offline back-upworkflow in Azure Backup](backup-azure-backup-import-export.md) (Offline back-upwerkstroom in Azure Backup) voor meer informatie over deze kosten. Uitgaande gegevens verwijst toodata van een Recovery Services-kluis overgedragen tijdens een terugzetbewerking.

**Gegevensversleuteling** -gegevensversleuteling zorgt voor beveiligde overdracht en opslag van uw gegevens in de openbare cloud Hallo. Hallo opgegeven wachtwoordzin voor versleuteling lokaal op te slaan en dit wordt nooit verzonden naar of opgeslagen in Azure. Als het benodigde toorestore ieder Hallo-gegevens alleen u hebt opgegeven wachtwoordzin voor versleuteling of sleutel.

**Toepassingsconsistente back-up** -back-up van gegevens toorestore hello of een back-up van een bestandsserver, de virtuele machine of de SQL-database, moet u een herstelpunt heeft alle tooknow vereist. Azure Backup biedt toepassingsconsistente back-ups ervoor gezorgd dat aanvullende correcties zijn niet nodig toorestore Hallo gegevens. Herstellen van de toepassing consistente gegevens vermindert Hallo hersteltijd, zodat u tooquickly return tooa actief is.

**Lange bewaartermijn** -in plaats van overschakelt naar de back-ups van schijf tootape en zwevend Hallo tape tooan externe locatie, kunt u Azure voor het bewaren van korte en lange termijn. Azure biedt geen Hallo tijdsduur gegevens in een back-up of Recovery Services-kluis blijven beperkt. U kunt gegevens zo lang als u wilt in een kluis bewaren. Azure Backup heeft een limiet van 9999 herstelpunten per beveiligd exemplaar. Zie Hallo [back-up en retentie](backup-introduction-to-azure-backup.md#backup-and-retention) sectie in dit artikel voor meer informatie over hoe de behoeften van uw back-ups mogelijk van invloed op deze limiet.  

## <a name="which-azure-backup-components-should-i-use"></a>Welke Azure Backup-onderdelen moet ik gebruiken?
Als u niet zeker weet welk onderdeel Azure Backup werkt voor uw behoeften, Zie de volgende tabel voor informatie over wat u met elk onderdeel beveiligen kunt Hallo. Hello Azure-portal biedt een wizard, die is ingebouwd in Hallo portal tooguide u bij het kiezen van onderdeel toodownload Hallo en implementeert. Hallo-wizard, die deel van Hallo Recovery Services-kluis maken uitmaakt, leidt u door Hallo stappen voor het selecteren van een back-doel en de gegevens of toepassing tooprotect Hallo kiezen.

| Onderdeel | Voordelen | Limieten | Wat wordt er beveiligd? | Waar worden de back-ups opgeslagen? |
| --- | --- | --- | --- | --- |
| Azure Backup-agent (MARS) |<li>Back-ups maken van bestanden en mappen op een fysiek of virtueel Windows-besturingssysteem (VM's kunnen zich on-premises of in Azure bevinden)<li>Geen afzonderlijk back-upserver vereist. |<li>Drie keer per dag een back-up maken <li>Niet toepassingsbewust; alleen herstelbewerkingen op bestands-, map- of volumeniveau, <li>  Geen ondersteuning voor Linux. |<li>Bestanden, <li>Mappen |Recovery Services-kluis |
| System Center DPM |<li>App-gerichte momentopnamen (VSS)<li>Volledige flexibiliteit voor wanneer tootake back-ups<li>Herstelgranulariteit (alles)<li>Kan Recovery Services-kluis gebruiken<li>Linux Support op virtuele Hyper-V- en VMware-machines <li>Back-ups maken van virtuele VMware-machines en deze herstellen met DPM 2012 R2 |Kan geen back-up maken van Oracle-workload.|<li>Bestanden, <li>Mappen,<li> Volumes, <li>VM's,<li> Toepassingen,<li> Workloads |<li>Recovery Services-kluis,<li> Lokaal gekoppelde schijf,<li>  Tape (alleen on-premises) |
| Azure Backup-server |<li>App-gerichte momentopnamen (VSS)<li>Volledige flexibiliteit voor wanneer tootake back-ups<li>Herstelgranulariteit (alles)<li>Kan Recovery Services-kluis gebruiken<li>Linux Support op virtuele Hyper-V- en VMware-machines<li>Back-ups maken van virtuele VMware-machines en deze herstellen <li>Vereist geen System Center-licentie |<li>Kan geen back-up maken van Oracle-workload.<li>Altijd een live Azure-abonnement nodig<li>Geen ondersteuning voor tape met back-up |<li>Bestanden, <li>Mappen,<li> Volumes, <li>VM's,<li> Toepassingen,<li> Workloads |<li>Recovery Services-kluis,<li> Lokaal gekoppelde schijf |
| Back-up van virtuele machines van Azure IaaS |<li>Systeemeigen back-ups voor Windows/Linux<li>Er zijn geen specifieke agentinstallatie vereist<li>Back-ups op infrastructuurniveau zonder dat er een back-upinfrastructuur nodig is |<li>Eens per dag back-ups maken van VM's <li>VM's alleen op schijfniveau herstellen<li>Geen back-up on-premises |<li>VM's, <li>Alle schijven (met PowerShell) |<p>Recovery Services-kluis</p> |

## <a name="what-are-hello-deployment-scenarios-for-each-component"></a>Wat zijn Hallo implementatiescenario's voor elk onderdeel?
| Onderdeel | Kan worden geïmplementeerd in Azure? | Kan on-premises worden geïmplementeerd? | Doelopslag ondersteund |
| --- | --- | --- | --- |
| Azure Backup-agent (MARS) |<p>**Ja**</p> <p>Hello Azure backup-agent kan worden geïmplementeerd op een Windows Server-VM wordt uitgevoerd in Azure.</p> |<p>**Ja**</p> <p>Hallo backup-agent kan worden geïmplementeerd op elke Windows Server-VM of fysieke machine.</p> |<p>Recovery Services-kluis</p> |
| System Center DPM |<p>**Ja**</p><p>Meer informatie over [hoe tooprotect werkbelastingen in Azure met behulp van System Center DPM](backup-azure-dpm-introduction.md).</p> |<p>**Ja**</p> <p>Meer informatie over [hoe tooprotect workloads en VM's in uw datacenter](https://technet.microsoft.com/system-center-docs/dpm/data-protection-manager).</p> |<p>Lokaal gekoppelde schijf,</p> <p>Recovery Services-kluis,</p> <p>tape (alleen on-premises)</p> |
| Azure Backup-server |<p>**Ja**</p><p>Meer informatie over [hoe tooprotect werkbelastingen in Azure met behulp van Azure Backup-Server](backup-azure-microsoft-azure-backup.md).</p> |<p>**Ja**</p> <p>Meer informatie over [hoe tooprotect werkbelastingen in Azure met behulp van Azure Backup-Server](backup-azure-microsoft-azure-backup.md).</p> |<p>Lokaal gekoppelde schijf,</p> <p>Recovery Services-kluis</p> |
| Back-up van virtuele machines van Azure IaaS |<p>**Ja**</p><p>Onderdeel van de Azure-infrastructuur</p><p>Speciaal voor [back-ups van de virtuele machines van Azure IaaS (Infrastructure as a Service)](backup-azure-vms-introduction.md).</p> |<p>**Nee**</p> <p>Gebruik System Center DPM tooback van virtuele machines in uw datacenter.</p> |<p>Recovery Services-kluis</p> |

## <a name="which-applications-and-workloads-can-be-backed-up"></a>Van welke toepassingen en workloads kan een back-up worden gemaakt?
Hallo volgende tabel bevat een matrix met Hallo gegevens en werkbelastingen die kunnen worden beveiligd met Azure Backup. Hello Azure Backup-oplossing kolom heeft koppelingen toohello Implementatiedocumentatie voor deze oplossing. Elk onderdeel van Azure Backup kan worden geïmplementeerd in een Klassieke (Service Manager-implementatie) of Resource Manager-implementatiemodelomgeving.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

| Gegevens of workload | Bronomgeving | Azure Backup-oplossing |
| --- | --- | --- |
| Bestanden en mappen |Windows Server |<p>[Azure Backup-agent](backup-configure-vault.md),</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) (+ hello Azure backup-agent)</p> <p>[Azure Backup-Server](backup-azure-microsoft-azure-backup.md) (inclusief hello Azure backup-agent)</p> |
| Bestanden en mappen |Windows-computer |<p>[Azure Backup-agent](backup-configure-vault.md),</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) (+ hello Azure backup-agent)</p> <p>[Azure Backup-Server](backup-azure-microsoft-azure-backup.md) (inclusief hello Azure backup-agent)</p> |
| Virtuele Hyper-V-machine (Windows) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure backup-agent)</p> <p>[Azure Backup-Server](backup-azure-microsoft-azure-backup.md) (inclusief hello Azure backup-agent)</p> |
| Virtuele Hyper-V-machine (Linux) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure backup-agent)</p> <p>[Azure Backup-Server](backup-azure-microsoft-azure-backup.md) (inclusief hello Azure backup-agent)</p> |
| Microsoft SQL Server |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure backup-agent)</p> <p>[Azure Backup-Server](backup-azure-microsoft-azure-backup.md) (inclusief hello Azure backup-agent)</p> |
| Microsoft SharePoint |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure backup-agent)</p> <p>[Azure Backup-Server](backup-azure-microsoft-azure-backup.md) (inclusief hello Azure backup-agent)</p> |
| Microsoft Exchange |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure backup-agent)</p> <p>[Azure Backup-Server](backup-azure-microsoft-azure-backup.md) (inclusief hello Azure backup-agent)</p> |
| Virtuele machines van Azure IaaS (Windows) |uitgevoerd in Azure |[Azure Backup (VM-extensie)](backup-azure-vms-introduction.md) |
| Virtuele machines van Azure IaaS (Linux) |uitgevoerd in Azure |[Azure Backup (VM-extensie)](backup-azure-vms-introduction.md) |

## <a name="linux-support"></a>Linux Support
Hallo toont volgende tabel hello Azure Backup-onderdelen die ondersteuning bieden voor Linux.  

| Onderdeel | Ondersteuning voor Linux (goedgekeurd door Azure) |
| --- | --- |
| Azure Backup-agent (MARS) |Nee (alleen Windows-agent) |
| System Center DPM |<li> Bestandsconsistente back-up van Linux-gast-VM's op Hyper-V en VMware<br/> <li> Linux-gast-VM's herstellen op Hyper-V- en VMware </br> </br>  *Bestandsconsistente back-up is niet beschikbaar voor virtuele Azure-machines* <br/> |
| Azure Backup-server |<li>Bestandsconsistente back-up van Linux-gast-VM's op Hyper-V en VMware<br/> <li> Linux-gast-VM's herstellen op Hyper-V- en VMware </br></br> *Bestandsconsistente back-up is niet beschikbaar voor virtuele Azure-machines*  |
| Back-up van virtuele machines van Azure IaaS |Toepassingsconsistente back-up met [prescript en postscript framework](backup-azure-linux-app-consistent.md)<br/> [Gedetailleerd bestandsherstel](backup-azure-restore-files-from-vm.md)<br/> [Alle VM-schijven herstellen](backup-azure-arm-restore-vms.md#restore-backed-up-disks)<br/> [VM herstellen](backup-azure-arm-restore-vms.md#create-a-new-vm-from-restore-point) |

## <a name="using-premium-storage-vms-with-azure-backup"></a>VM's voor Premium Storage met Azure Backup gebruiken
Azure Backup beschermt VM's voor Premium Storage. Azure Premium-opslag is (SSD) de SSD-opslag ontworpen toosupport I/O-intensieve werkbelastingen op basis van. Premium Storage is uitermate geschikt voor VM-workloads (virtuele machine). Zie voor meer informatie over Premium-opslag Hallo artikel [Premium-opslag: krachtige opslag voor Azure Virtual Machine-werkbelasting](../storage/common/storage-premium-storage.md).

### <a name="back-up-premium-storage-vms"></a>Een back-up van VM's voor Premium-opslag maken
Bij het maken van back-ups van virtuele machines Premium-opslag, Hallo Backup-service is een tijdelijke faseringslocatie, met de naam 'AzureBackup-' in hello Premium Storage-account. Hallo is Hallo tijdelijke locatie gelijk toohello groot Hallo recovery point momentopname. Zorg ervoor dat Hallo Premium Storage-account heeft voldoende vrije ruimte tooaccommodate Hallo tijdelijke faseringslocatie. Zie voor meer informatie Hallo artikel [premium storage beperkingen](../storage/common/storage-premium-storage.md#scalability-and-performance-targets). Als Hallo back-uptaak is voltooid, wordt Hallo faseringslocatie verwijderd. Hallo prijs opslag gebruikt voor Hallo faseringslocatie zijn consistent met de [prijzen van Premium storage](../storage/common/storage-premium-storage.md#pricing-and-billing).

> [!NOTE]
> Niet te wijzigen of Hallo faseringslocatie bewerken.
>
>

### <a name="restore-premium-storage-vms"></a>VM's voor Premium-opslag herstellen
VM's voor Premium-opslag kan herstelde tooeither Premium-opslag of toonormal opslag zijn. Herstellen van een VM voor Premium-opslag recovery point back tooPremium opslag is Hallo typische proces van herstel. Het kan echter rendabel toorestore een VM voor Premium-opslag herstelpunt toostandard opslag zijn. Dit type herstel kan worden gebruikt als u een subset van bestanden van Hallo VM nodig.

## <a name="using-managed-disk-vms-with-azure-backup"></a>Virtuele machines op beheerde schijven gebruiken met Azure Backup
Met Azure Backup beveiligt u virtuele machines op beheerde schijven. Dankzij beheerde schijven hoeft u opslagaccounts van virtuele machines niet te beheren en wordt de VM-inrichting sterk vereenvoudigd.

### <a name="back-up-managed-disk-vms"></a>Back-up maken van virtuele machines op beheerde schijven
Het maken van een back-up van virtuele machines op beheerde schijven en in Resource Manager gebeurt op dezelfde manier. In hello Azure-portal, kunt u back-uptaak rechtstreeks vanuit de weergave van de virtuele Machine Hallo Hallo configureren of weergave van Hallo Recovery Services-kluis. U kunt back-ups maken van virtuele machines op beheerde schijven via RestorePoint-verzamelingen die zijn gebouwd boven op beheerde schijven. Azure Backup biedt ook ondersteuning voor het maken van back-ups van virtuele machines op beheerde schijven die zijn versleuteld met Azure Disk Encryption (ADE).

### <a name="restore-managed-disk-vms"></a>Virtuele machines op beheerde schijven terugzetten
Azure Backup kunt u een volledige virtuele machine met beheerde schijven toorestore of terugzetten beheerde schijven tooa storage-account. Azure beheert Hallo beheerd schijven tijdens het terugzetten van een Hallo. U (Hallo klant) beheren Hallo storage-account is gemaakt als onderdeel van het herstelproces Hallo. Wanneer terugzetten versleutelde virtuele machines worden beheerd, moeten hello de sleutels en geheimen van de virtuele machine bestaan in Hallo sleutelkluis voorafgaande toostarting Hallo restore-bewerking.

## <a name="what-are-hello-features-of-each-backup-component"></a>Wat zijn de functies Hallo van elk onderdeel van de back-up
Hallo volgende secties vindt u tabellen om samen te vatten Hallo beschikbaarheid of ondersteuning van verschillende functies in elk onderdeel van de Azure Backup. Zie Hallo na elke tabel voor aanvullende ondersteuning of details.

### <a name="storage"></a>Storage
| Functie | Azure Backup-agent | System Center DPM | Azure Backup-server | Back-up van virtuele machines van Azure IaaS |
| --- | --- | --- | --- | --- |
| Recovery Services-kluis |![Ja][green] |![Ja][green] |![Ja][green] |![Ja][green] |
| File Storage | |![Ja][green] |![Ja][green] | |
| Bandgeheugen | |![Ja][green] | | |
| Compressie <br/>(in Recovery Services-kluis) |![Ja][green] |![Ja][green] |![Ja][green] | |
| Incrementele back-up |![Ja][green] |![Ja][green] |![Ja][green] |![Ja][green] |
| Schijfontdubbeling | |![Gedeeltelijk][yellow] |![Gedeeltelijk][yellow] | | |

![tabelsleutel](./media/backup-introduction-to-azure-backup/table-key.png)

Hallo Recovery Services-kluis is Hallo gewenste doelopslag voor alle onderdelen. System Center DPM en Azure Backup-Server bieden ook Hallo optie toohave kopiëren van een lokale schijf. Alleen System Center DPM biedt echter Hallo optie toowrite tooa tapeapparaat voor gegevensopslag.

#### <a name="compression"></a>Compressie
Back-ups worden gecomprimeerd tooreduce Hallo opslagruimte vereist. Hallo enige onderdeel dat u geen compressie gebruikt is Hallo VM-extensie. Hallo VM-extensie kopieën die alle back-upgegevens van uw storage-account toohello Recovery Services-kluis in dezelfde regio Hallo. Geen compressie wordt gebruikt bij de overdracht van gegevens Hallo. Gegevensoverdracht Hallo zonder compressie iets meer Hallo opslag gebruikt. Hallo-gegevens worden opgeslagen zonder compressie kan voor sneller herstellen, moet u moet echter dat herstelpunt.


#### <a name="disk-deduplication"></a>Schijfontdubbeling
U kunt profiteren van ontdubbeling wanneer u System Center DPM of Azure Backup Server implementeert [op een virtuele Hyper-V-machine](http://blogs.technet.com/b/dpm/archive/2015/01/06/deduplication-of-dpm-storage-reduce-dpm-storage-consumption.aspx). Windows Server voert gegevensontdubbeling (op hostniveau Hallo) op virtuele harde schijven (VHD's) die aangesloten toohello virtuele machine als back-upopslag zijn.

> [!NOTE]
> Ontdubbeling is niet beschikbaar in Azure voor Backup-onderdelen. Wanneer u System Center DPM en de back-upserver zijn geïmplementeerd in Azure, gekoppeld Hallo opslagschijven toohello die VM kan niet worden ontdubbeld.
>
>

### <a name="incremental-backup-explained"></a>Incrementele back-up uitgelegd
Elk onderdeel van de Azure Backup biedt ondersteuning voor incrementele back-up ongeacht Hallo doelopslag (schijf, tape, Recovery Services-kluis). Incrementele back-up zorgt ervoor dat back-ups opslag- en tijdsefficiënt zijn door alleen de wijzigingen sinds de laatste back-up Hallo over te brengen.

#### <a name="comparing-full-differential-and-incremental-backup"></a>Vergelijking tussen Volledige, Differentiële en Incrementele back-ups

Opslagverbruik, Beoogde hersteltijd (RTO) en netwerkverbruik varieert voor elke back-upmethode. tookeep hello back-totale eigendomskosten (TCO) omlaag, moet u toounderstand hoe toochoose Hallo aanbevolen back-upoplossing. Hallo installatiekopie na vergelijkt volledige back-up, differentiële back-up en incrementele back-up. In afbeelding Hallo blokkeert gegevensbron die a uit 10 opslag bestaat A1-A10, waarvan een back-up maandelijks. Blokken A2, A3, A4 en A9 wijzigen in Hallo eerste maand en blokkeren van A5 wijzigingen in Hallo volgende maand.

![afbeelding met vergelijkingen van back-upmethoden](./media/backup-introduction-to-azure-backup/backup-method-comparison.png)

Met **volledige back-up**, elke back-up Hallo gehele gegevensbron bevat. Bij Volledige back-up wordt een grote hoeveelheid netwerkbandbreedte en -opslag verbruikt telkens wanneer een back-upexemplaar wordt overgedragen.

**Differentiële back-up** slaat alleen Hallo blokkeert die gewijzigd zijn sinds Hallo eerste volledige back-up, wat in een kleinere hoeveelheid netwerk- en verbruik resulteert. Bij differentiële back-ups worden geen redundante exemplaren met ongewijzigde gegevens bewaard. Differentiële back-ups zijn echter inefficiënt omdat Hallo-gegevensblokken die onveranderd te laten tussen de volgende back-ups worden overgedragen en opgeslagen. In Hallo zijn tweede maand gewijzigde blokken A2, A3, A4 en A9 back-up. In Hallo worden derde maand deze dezelfde blokken back-up opnieuw samen met de gewijzigde blok A5. Hallo gewijzigd blokken blijven toobe totdat Hallo volgende volledige back-ups worden ondersteund.

**Incrementele back-up** hoge efficiëntie voor opslag en het netwerk door op te slaan alleen Hallo blokken met gegevens die gewijzigd sinds de vorige back-up Hallo bereikt. Met incrementele back-up hoeft niet tootake reguliere volledige back-ups. In voorbeeld Hallo nadat Hallo volledige back-up wordt genomen voor Hallo eerste maand gewijzigde blokken A2, A3, A4 en A9 zijn gemarkeerd als gewijzigd en overgedragen voor Hallo tweede maand. Derde maand in Hallo alleen blok A5 is gemarkeerd en overgedragen gewijzigd. Door minder gegevens te verplaatsen worden opslag- en netwerkresources bespaard, waardoor de totale eigendomskosten worden verlaagd.   

### <a name="security"></a>Beveiliging
| Functie | Azure Backup-agent | System Center DPM | Azure Backup-server | Back-up van virtuele machines van Azure IaaS |
| --- | --- | --- | --- | --- |
| Netwerkbeveiliging<br/> (tooAzure) |![Ja][green] |![Ja][green] |![Ja][green] |![Gedeeltelijk][yellow] |
| Gegevensbeveiliging<br/> (in Azure) |![Ja][green] |![Ja][green] |![Ja][green] |![Gedeeltelijk][yellow] |

![tabelsleutel](./media/backup-introduction-to-azure-backup/table-key.png)

#### <a name="network-security"></a>Netwerkbeveiliging
Alle back-upverkeer van uw servers toohello die Recovery Services-kluis wordt versleuteld met Advanced Encryption Standard 256. back-upgegevens Hello wordt verzonden via een beveiligde HTTPS-koppeling. back-upgegevens Hello wordt ook opgeslagen in Hallo Recovery Services-kluis in een versleutelde vorm. Alleen hebt u hello Azure klant Hallo wachtwoordzin toounlock deze gegevens. Microsoft hello back-upgegevens op elk moment kan niet ontsleutelen.

> [!WARNING]
> Nadat u Hallo Recovery Services-kluis maken, alleen hebt u toegang toohello versleutelingssleutel. Microsoft nooit wordt een kopie van de versleutelingssleutel en heeft geen toegang tot toohello sleutel. Als het Hallo-sleutel is verkeerd wordt geplaatst, kan Microsoft hello back-upgegevens niet herstellen.
>
>

#### <a name="data-security"></a>Gegevensbeveiliging
Back-ups van virtuele Azure-machines vereist het instellen van versleuteling *binnen* Hallo virtuele machine. Gebruik BitLocker voor virtuele machines van Windows en **dm-crypt** voor virtuele machines van Linux. De gegevens die via dit pad worden verzonden, worden niet automatisch door Azure Backup versleuteld.

### <a name="network"></a>Netwerk
| Functie | Azure Backup-agent | System Center DPM | Azure Backup-server | Back-up van virtuele machines van Azure IaaS |
| --- | --- | --- | --- | --- |
| Netwerkcompressie <br/>(te**back-upserver**) | |![Ja][green] |![Ja][green] | |
| Netwerkcompressie <br/>(te**Recovery Services-kluis**) |![Ja][green] |![Ja][green] |![Ja][green] | |
| Netwerkprotocol <br/>(te**back-upserver**) | |TCP |TCP | |
| Netwerkprotocol <br/>(te**Recovery Services-kluis**) |HTTPS |HTTPS |HTTPS |HTTPS |

![tabelsleutel](./media/backup-introduction-to-azure-backup/table-key-2.png)

Hallo VM-extensie (op Hallo IaaS VM) leest de Hallo gegevens rechtstreeks vanuit hello Azure storage-account via het opslagnetwerk hello, zodat het niet nodig toocompress dit verkeer.

Als u een System Center DPM-server of Azure Backup-Server als een secundaire server back-up, gegevenscompressie Hallo van Hallo primaire server toohello back-upserver. Comprimeren van gegevens voordat de back-up tooDPM of Azure Backup-Server, bespaart bandbreedte.

#### <a name="network-throttling"></a>Netwerkbeperking
Hello Azure backup-agent biedt netwerkbeperking, waarmee u toocontrol hoe netwerkbandbreedte wordt gebruikt tijdens de gegevensoverdracht. Beperking kan handig zijn als u tooback van gegevens tijdens werkuren nodig maar niet dat Hallo back-upproces toointerfere met andere internetverkeer wilt. De beperking voor de overdracht van toepassing is tooback up en herstelbewerkingen.

## <a name="backup-and-retention"></a>Back-up en retentie

Azure Backup heeft een limiet van 9999 herstelpunten, ook wel back-ups of momentopnamen genoemd, *per beveiligd exemplaar*. Een beveiligde exemplaar is een computer, de server (fysiek of virtueel) of de werkbelasting geconfigureerd tooback up tooAzure gegevens. Zie voor meer informatie, Hallo sectie [wat is er een beveiligde exemplaar](backup-introduction-to-azure-backup.md#what-is-a-protected-instance). Een exemplaar is beveiligd zodra er een back-up van de gegevens is opgeslagen. Hallo back-up van gegevens is Hallo-beveiliging. Als Hallo brongegevens verloren gegaan is of beschadigd is geworden, kan back-up Hallo Hallo brongegevens herstellen. Hallo toont volgende tabel Hallo maximale back-upfrequentie voor elk onderdeel. De configuratie van uw back-upbeleid bepaalt hoe snel u herstelpunten Hallo verbruiken. Als u bijvoorbeeld één herstelpunt per dag maakt, kunt u 27 jaar gebruikmaken van herstelpunten voordat ze opraken. Als u een maandelijkse herstelpunt, kunt u de herstelpunten 833 jaar u behouden. Hallo Backup-service wordt een tijdslimiet verloopt niet ingesteld voor een herstelpunt.

|  | Azure Backup-agent | System Center DPM | Azure Backup-server | Back-up van virtuele machines van Azure IaaS |
| --- | --- | --- | --- | --- |
| Back-upfrequentie<br/> (tooRecovery Services-kluis) |Drie back-ups per dag |Twee back-ups per dag |Twee back-ups per dag |Eén back-up per dag |
| Back-upfrequentie<br/> (toodisk) |Niet van toepassing |<li>Om de 15 minuten voor SQL Server <li>Elk uur voor andere workloads |<li>Om de 15 minuten voor SQL Server <li>Elk uur voor andere workloads</p> |Niet van toepassing |
| Bewaaropties |Dagelijks, wekelijks, maandelijks, jaarlijks |Dagelijks, wekelijks, maandelijks, jaarlijks |Dagelijks, wekelijks, maandelijks, jaarlijks |Dagelijks, wekelijks, maandelijks, jaarlijks |
| Maximumaantal herstelpunten per beveiligd exemplaar |9999|9999|9999|9999|
| Maximale bewaarperiode |Afhankelijk van back-upfrequentie |Afhankelijk van back-upfrequentie |Afhankelijk van back-upfrequentie |Afhankelijk van back-upfrequentie |
| Herstelpunten op lokale schijf |Niet van toepassing |<li>64 voor bestandsservers,<li>448 voor toepassingsservers |<li>64 voor bestandsservers,<li>448 voor toepassingsservers |Niet van toepassing |
| Herstelpunten op tape |Niet van toepassing |Onbeperkt |Niet van toepassing |Niet van toepassing |

## <a name="what-is-a-protected-instance"></a>Wat is een beveiligd exemplaar?
Een beveiligde exemplaar is een algemene verwijzing tooa Windows-computer, een server (fysiek of virtueel) of SQL-database die geconfigureerd tooback up tooAzure is. Een exemplaar is beveiligd wanneer u een back-upbeleid voor Hallo computer, server of database configureren en een back-up van gegevens Hallo maken. Daaropvolgende kopieën van de back-upgegevens Hallo voor het beveiligde exemplaar (die herstelpunten worden genoemd), vergroot u Hallo hoeveelheid opslag verbruikt. U kunt maken van too9999 herstelpunten voor een beveiligde sessie. Als u een herstelpunt uit de opslag verwijderen, komt het Hallo 9999 recovery point totaal niet meegeteld.
Enkele algemene voorbeelden van beveiligde instanties zijn virtuele machines, toepassingsservers, databases en pc's met Hallo Windows-besturingssysteem. Bijvoorbeeld:

* Een virtuele machine uitgevoerd Hallo Hyper-V- of Azure IaaS hypervisor fabric. Hallo-gastbesturingssystemen voor Hallo virtuele machine kan worden Windows Server of Linux.
* Een toepassingsserver: Hallo-toepassingsserver mag een fysieke of virtuele machine met Windows Server en werkbelastingen met gegevens die moeten worden toobe back-up gemaakt. Gangbare werkbelastingen zijn Microsoft SQL Server, Microsoft Exchange-server, Microsoft SharePoint server en Hallo bestandsserverrol voor Windows Server. tooback van deze werkbelastingen moet u de System Center Data Protection Manager (DPM) of Azure Backup-Server.
* Een pc, werkstation of laptop met Hallo Windows-besturingssysteem.


## <a name="what-is-a-recovery-services-vault"></a>Wat is een Recovery Services-kluis?
Een Recovery Services-kluis is dat een entiteit online opslag in Azure gebruikt toohold gegevens zoals back-ups en herstelpunten back-upbeleid. U kunt de Recovery Services-kluizen toohold back-upgegevens gebruiken voor Azure-services en on-premises servers en werkstations. Recovery Services-kluizen maken het gemakkelijk tooorganize uw back-upgegevens, terwijl de beheeroverhead minimaliseert. U kunt binnen een abonnement zoveel Recovery Services-kluizen maken als u wilt.

Back-upkluizen die gebaseerd zijn op Azure Service Manager, zijn de eerste versie Hallo van Hallo kluis. Recovery Services-kluizen, die hello Azure Resource Manager-model functies toevoegen, zijn de tweede versie Hallo van Hallo kluis. Zie Hallo [Recovery Services-kluis overzichtsartikel](backup-azure-recovery-services-vault-overview.md) voor een volledige beschrijving van Hallo Functieverschillen. U kunt gebruik Hallo portal toocreate Backup-kluizen niet langer maken, maar Backup-kluizen worden nog steeds ondersteund.

> [!IMPORTANT]
> U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden. Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.<br/> **15 oktober 2017**, u niet langer kunnen toouse PowerShell toocreate Backup-kluizen. <br/> **Per 1 november 2017**:
>- Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.
>- U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo. In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.
>

## <a name="how-does-azure-backup-differ-from-azure-site-recovery"></a>Wat is het verschil tussen Azure Backup en Azure Site Recovery?
Azure Backup en Azure Site Recovery lijken in die zin op elkaar dat u met beide services back-ups kunt maken en gegevens kunt herstellen. Deze services worden echter voor verschillende doeleinden gebruikt bij het bieden van zakelijke continuïteit en herstel na noodgevallen voor uw bedrijf. Gebruik van Azure Backup tooprotect en herstellen van gegevens op een meer gedetailleerd niveau. Als een presentatie op een laptop beschadigd geraakte, gebruikt u bijvoorbeeld Azure Backup toorestore Hallo presentatie. Als u tooreplicate Hallo configuratie en gegevens op een virtuele machine in een ander datacenter wilde, gebruikt u Azure Site Recovery.

Azure Backup beveiligt de gegevens die lokaal en in de cloud Hallo. Azure Site Recovery coördineert de replicatie, failover en failback van virtuele machines en fysieke servers. Beide services zijn belangrijk omdat uw noodherstel tookeep uw gegevens veilig en herstelbaar (back-up moet) *en* houden van uw workloads beschikbaar (Site Recovery) wanneer er storingen optreden.

Hallo volgende concepten kunt u belangrijke beslissingen te nemen om back-up en herstel na noodgevallen.

| Concept | Details | Back-up | Herstel na noodgeval (DR; disaster recovery) |
| --- | --- | --- | --- |
| Recovery Point Objective (RPO) |Hallo hoeveelheid acceptabele gegevens verloren gaan als een herstelbewerking toobe gedaan moet. |Back-oplossingen hebben grote variabiliteit met betrekking tot hun acceptabele RPO. Back-ups van virtuele machines hebben doorgaans een RPO van één dag, terwijl de RPO bij databaseback-up soms maar vijftien minuten is. |Oplossingen voor herstel na noodgevallen hebben lage RPO's. Hallo DR-kopie kan door een paar seconden of paar minuten achter zijn. |
| Beoogde hersteltijd (RTO) |Hallo hoeveelheid tijd die nodig is toocomplete herstel of herstellen. |Vanwege Hallo grotere RPO is de hoeveelheid gegevens dat er een back-upoplossing tooprocess moet Hallo is doorgaans veel grote, wat resulteert toolonger RTO's. Bijvoorbeeld: kan duren dagen toorestore gegevens vanaf tapes, afhankelijk van Hallo duurt tootransport Hallo tape vanaf een externe locatie. |Noodhersteloplossingen hebben kleinere RTO's omdat ze beter gesynchroniseerd met Hallo-bron zijn. Er hoeven minder wijzigingen toobe verwerkt. |
| Bewaartermijn |Hoe lang gegevens moeten toobe opgeslagen |Voor scenario's waarvoor een operationele herstelbewerking is vereist (beschadigde gegevens, onbedoeld verwijderen van bestanden, OS-fouten), moeten de back-upgegevens doorgaans 30 dagen of korter worden bewaard.<br>Uit oogpunt van de naleving mogelijk gegevens toobe maanden of zelfs jaren voor opgeslagen. In dergelijke gevallen kunnen de back-upgegevens het beste worden gearchiveerd. |Herstel na noodgevallen moet alleen operationele herstelgegevens, die doorgaans een paar uur of up tooa dag. Vanwege Hallo fijnmazig gegevensregistratie noodhersteloplossingen, wordt kunt u de gegevens op lange termijn niet aanbevolen. |

## <a name="next-steps"></a>Volgende stappen
Gebruik een van de volgende zelfstudies voor gedetailleerde, stapsgewijze, instructies voor het beveiligen van gegevens op Windows Server, of als u een virtuele machine (VM) beveiligt Hallo in Azure:

* [Een back-up maken van bestanden en mappen](backup-try-azure-backup-in-10-mins.md)
* [Een back-up maken van Azure Virtual Machines](backup-azure-vms-first-look-arm.md)

Lees een van de volgende artikelen voor meer informatie over het beschermen van andere workloads:

* [Een back-up maken van uw Windows Server](backup-configure-vault.md)
* [Een back up maken van uw toepassingsworkloads](backup-azure-microsoft-azure-backup.md)
* [Een back-up maken van Azure IaaS VM's](backup-azure-vms-prepare.md)

[green]: ./media/backup-introduction-to-azure-backup/green.png
[yellow]: ./media/backup-introduction-to-azure-backup/yellow.png
[red]: ./media/backup-introduction-to-azure-backup/red.png
