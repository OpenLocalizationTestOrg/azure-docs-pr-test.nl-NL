---
title: aaaReplicate virtuele VMware-machines en fysieke servers tooAzure (klassieke verouderd) | Microsoft Docs
description: Hierin wordt beschreven hoe tooreplicate lokale VM's en Windows of Linux fysieke servers tooAzure met Azure Site Recovery in een oudere implementatie in de klassieke portal Hallo.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: f980fb52-8ec2-4dd9-85e2-8e52e449f1ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: raynew
ms.openlocfilehash: 64c6d906d54426fdd2b884350542a4562bb12528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery-using-hello-classic-portal-legacy"></a>Virtuele VMware-machines en fysieke servers tooAzure repliceren met Azure Site Recovery met Hallo klassieke portal (verouderd)
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmware-to-azure.md)
> * [Klassieke portal](site-recovery-vmware-to-azure-classic.md)
> * [Klassieke Portal (verouderd)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

Welkom tooAzure Site Recovery. Dit artikel wordt een oude implementatie voor het repliceren van on-premises VMware-virtuele machines of Windows of Linux fysieke servers tooAzure met Azure Site Recovery in de klassieke portal Hallo beschreven.

## <a name="overview"></a>Overzicht
Organisaties moeten een BCDR-strategie die bepaalt hoe toepassingen, workloads en gegevens beschikbaar tijdens geplande en ongeplande uitval blijven, en toonormal werkomstandigheden zo snel mogelijk te herstellen. In uw BCDR-strategie moeten bedrijfsgegevens veilig en herstelbaar blijven. Ook moet ervoor worden gezorgd dat workloads continu beschikbaar blijven wanneer zich een noodsituatie voordoet.

Site Recovery is een Azure-service die tooyour BCDR-strategie door replicatie van fysieke on-premises servers en virtuele machines toohello cloud (Azure) of tooa secundair datacenter organiseren bijdraagt. Wanneer er storingen optreden op uw primaire locatie, schakelt u over toohello secundaire locatie tookeep toepassingen en workloads beschikbaar. U mislukken back tooyour primaire locatie wanneer deze toonormal bewerkingen weer. Zie [Wat is Azure Site Recovery?](site-recovery-overview.md) voor meer informatie

> [!WARNING]
> Dit artikel bevat **verouderde instructies**. Deze niet gebruikt voor nieuwe implementaties. In plaats daarvan [Volg deze instructies](site-recovery-vmware-to-azure.md) toodeploy Site Recovery in hello Azure-portal of [Volg deze instructies](site-recovery-vmware-to-azure-classic.md) tooconfigure Hallo uitgebreide implementatie in de klassieke portal Hallo. Als u al hebt geïmplementeerd met behulp van Hallo-methode in dit artikel wordt beschreven, wordt u aangeraden toohello uitgebreide implementatie in de klassieke portal hello te migreren.
>
>

## <a name="migrate-toohello-enhanced-deployment"></a>Verbeterde toohello implementatie migreren
Deze sectie is alleen relevant als u Site Recovery met Hallo-instructies in dit artikel al hebt geïmplementeerd.

toomigrate uw bestaande implementatie u moet:

1. Implementeer de nieuwe Site Recovery-onderdelen in uw on-premises site.
2. Configureer de referenties voor automatische detectie van virtuele VMware-machines op Hallo nieuwe configuratie-server.
3. Hallo VMware-servers met de nieuwe configuratieserver Hallo detecteren.
4. Maak een nieuwe beveiligingsgroep met de nieuwe configuratieserver Hallo.

Voordat u begint:

* Het is raadzaam dat u een onderhoudsvenster voor migratie instellen.
* Hallo **Machines migreren** optie is alleen beschikbaar als u bestaande beveiligingsgroepen die zijn gemaakt tijdens de implementatie van een verouderde hebt.
* Na voltooiing van de migratiestappen Hallo kan duren 15 minuten of langer toorefresh Hallo referenties en toodiscover en vernieuwen van virtuele machines zodat u ze tooa beveiligingsgroep kunt toevoegen. U kunt handmatig vernieuwen in plaats van te wachten.

Migreren als volgt:

1. Meer informatie over [uitgebreide implementatie in de klassieke portal Hallo](site-recovery-vmware-to-azure-classic.md). Bekijk Hallo verbeterde [architectuur](site-recovery-vmware-to-azure-classic.md), en [vereisten](site-recovery-vmware-to-azure-classic.md).
2. Hallo Mobility-service verwijderen van computers die u repliceert. Een nieuwe versie van het Hallo-service wordt geïnstalleerd op Hallo machines wanneer u ze nieuwe beveiligingsgroep toohello toevoegt.
3. Download een [kluisregistratiesleutel](site-recovery-vmware-to-azure-classic.md) en [Hallo unified setup-wizard uitvoert](site-recovery-vmware-to-azure-classic.md) tooinstall Hallo configuratieserver en processerver master gericht op server-onderdelen. Lees meer over [capaciteitsplanning](site-recovery-vmware-to-azure-classic.md).
4. [Instellen van referenties](site-recovery-vmware-to-azure-classic.md) die Site Recovery kunt tooaccess VMware server tooautomatically virtuele VMware-machines detecteren. Meer informatie over [vereist machtigingen](site-recovery-vmware-to-azure-classic.md).
5. Voeg [vCenter servers of vSphere hosts](site-recovery-vmware-to-azure-classic.md). Het kan 15 minuten duren voordat informatie voor servers tooappear in Hallo Site Recovery-portal.
6. Maak een [nieuwe beveiligingsgroep](site-recovery-vmware-to-azure-classic.md). Het kan Hallo portal toorefresh too15 minuten duren zodat Hallo virtuele machines worden gedetecteerd en worden weergegeven. Als u niet toowait wilt kunt u de naam van de beheerserver Hallo markeren (Klik niet op deze) > **vernieuwen**.
7. Klik onder de nieuwe beveiligingsgroep Hallo op **Machines migreren**.

    ![Account toevoegen](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration1.png)
8. In **Machines selecteren** beveiligingsgroep selecteert Hallo u wilt toomigrate uit en computers die u wilt dat toomigrate Hallo.

    ![Account toevoegen](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration2.png)
9. In **doelinstellingen configureren** aangeven of u toouse Hallo dezelfde instellingen voor alle computers en selecteer Hallo processerver en de Azure storage-account. Als u geen afzonderlijke processerver wordt dit Hallo Hallo IP-adres van de configuratieserver server Hallo zijn.

    ![Account toevoegen](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration3.png)

    > [AZURE.NOTE] [Migratie van opslagaccounts](../resource-group-move-resources.md) via resource groepen binnen hetzelfde abonnement Hallo of voor abonnementen wordt niet ondersteund voor storage-accounts gebruikt voor de implementatie van Site Recovery.

1. In **Accounts opgeven**, u hebt gemaakt voor Hallo proces server tooaccess machine toopush Hallo nieuwe versie van de Mobility-service Hallo HALLO hallo-account selecteren.

   ![Account toevoegen](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration4.png)
2. Site Recovery worden gemigreerd van de gerepliceerde gegevens toohello Azure storage-account die u hebt opgegeven. U kunt eventueel Hallo opslagaccount die u in de verouderde implementatie Hallo gebruikt hergebruiken.
3. Na het Hallo-taak is voltooid virtuele machines automatisch gesynchroniseerd. Nadat de synchronisatie is voltooid, kunt u Hallo virtuele machines kunt verwijderen uit de oude beveiligingsgroep Hallo.
4. Als alle machines hebt gemigreerd, kunt u verouderde Hallo-beveiligingsgroep verwijderen.
5. Houd er rekening mee toospecify Hallo failover-eigenschappen voor machines en hello Azure-netwerkinstellingen nadat synchronisatie voltooid is.
6. Als u bestaande herstelplannen hebt, kunt u migreren ze toohello uitgebreide implementatie Hello **herstelplan migreren** optie. U moet dit alleen doen nadat alle beveiligde machines zijn gemigreerd.

   ![Account toevoegen](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration5.png)

> [!NOTE]
> Nadat u klaar bent met migratie doorgaan met de Hallo [verbeterde artikel](site-recovery-vmware-to-azure-classic.md). Hallo rest van dit artikel verouderde niet langer relevant en hoeft u geen toofollow ieder meer Hallo stappen wordt beschreven in it **.
>
>

## <a name="what-do-i-need"></a>Wat heb ik nodig?
Dit diagram toont Hallo-onderdelen voor implementatie.

![Nieuwe kluis](./media/site-recovery-vmware-to-azure-classic-legacy/architecture.png)

U hebt het volgende nodig:

| **Onderdeel** | **Implementatie** | **Details** |
| --- | --- | --- |
| **Configuratieserver** |Een standaard A3 virtuele machine van Azure in Hallo hetzelfde abonnement als Site Recovery. |Hallo configuratieserver coördineert de communicatie tussen de beveiligde machines processerver Hallo en hoofddoelservers in Azure. Replicatie en ingesteld coördinaten herstel in Azure wanneer failover plaatsvindt. |
| **Hoofddoelserver** |Een virtuele machine van Azure, WindowsServer op basis van een Windows Server 2012 R2 afbeelding (tooprotect Windows-machines) of als een Linux-server op basis van een afbeelding OpenLogic CentOS 6.6 (tooprotect Linux-machines).<br/><br/> Van de drie formaatopties zijn beschikbaar: standaard A4, standaard D14 en standaard DS4.<br/><br/> Hallo-server is verbonden toohello dezelfde Azure-netwerk als Hallo configuratieserver.<br/><br/> U hebt ingesteld in Hallo Site Recovery-portal |Deze ontvangt en behoudt de gerepliceerde gegevens van uw beveiligde machines met behulp van de gekoppelde virtuele harde schijven die zijn gemaakt op de blob-opslag in uw Azure storage-account.<br/><br/> Selecteer standaard DS4 specifiek voor het configureren van beveiliging voor werkbelastingen vereisen consistent hoge prestaties en lage latentie met Premium-Opslagaccount. |
| **Processerver** |Een lokale virtuele of fysieke server met Windows Server 2012 R2<br/><br/> Het is raadzaam deze heeft geplaatst op Hallo dezelfde netwerk en LAN-segment als Hallo machines dat u wilt dat tooprotect, maar kan uitgevoerd op een ander netwerk zolang beveiligde machines beschikken over N3 tooit zichtbaarheid van het netwerk.<br/><br/> U instellen en registreer de configuratieserver toohello in Hallo Site Recovery-portal. |Beveiligde machines verzenden replicatie gegevens toohello lokale processerver. Er is een schijfcache toocache replicatiegegevens die het ontvangt. Een aantal acties worden uitgevoerd op die gegevens.<br/><br/> Dit optimaliseert de gegevens met caching, compressie en codering voordat u deze op de hoofddoelserver toohello verzendt.<br/><br/> Push-installatie van Hallo Mobility-Service verwerkt.<br/><br/> Automatische detectie van virtuele VMware-machines worden uitgevoerd. |
| **Lokale computers** |Een on-premises virtuele VMware-machines of fysieke servers met Windows of Linux. |U configureren replicatie-instellingen die van toepassing zijn een of meer computers. U kunt via een afzonderlijke virtuele machine of vaker voorkomt, niet meerdere machines die u in een herstelplan verzamelen. |
| **Mobility-service** |Geïnstalleerd op elke virtuele machine of fysieke server gewenste tooprotect<br/><br/> Kan worden geïnstalleerd handmatig of gepusht en automatisch door Hallo processerver worden geïnstalleerd wanneer u replicatie voor een machine inschakelt. |Hallo Mobility-service verzendt gegevens toohello processerver tijdens de eerste replicatie (resync). Nadat het Hallo-machine bevindt zich in een beveiligde status (nadat de resync is voltooid) wordt Hallo Mobility-service worden vastgelegd schrijfbewerkingen toodisk in het geheugen en verzendt deze toohello processerver. Applicationconsistency voor Windows-servers wordt bereikt met VSS. |
| **Azure Site Recovery-kluis** |U een Site Recovery-kluis maken met een Azure-abonnement en beheerservers in Hallo kluis registreren. |Hallo kluis coördineert en stuurt replicatie, failovers en herstel tussen uw on-premises site en Azure. |
| **Replicatiemechanisme** |**Via Internet Hallo**-communicatie en repliceren gegevens uit beveiligde lokale servers tooAzure met behulp van veilige SSL/TLS-kanaal via internet Hallo. Dit is de standaardoptie Hallo.<br/><br/> **VPN en ExpressRoute**: gegevens voor communicatie en repliceren tussen on-premises servers en Azure via een VPN-verbinding. U moet tooset van een site-naar-site VPN- of een ExpressRoute-verbinding tussen uw on-premises site en Azure-netwerk.<br/><br/> Selecteert u hoe u wilt dat tooreplicate tijdens de implementatie van Site Recovery. U kunt Hallo mechanisme niet wijzigen nadat deze geconfigureerd zonder enige impact op de replicatie van bestaande machines. |Geen van beide optie moet u tooopen alle inkomende netwerkpoorten op beveiligde computers. Alle netwerkcommunicatie is vanaf Hallo lokale site gestart. |

## <a name="capacity-planning"></a>Capaciteitsplanning
Hallo-hoofdgebieden moet u tooconsider:

* **Bronomgeving**: Hallo VMware-infrastructuur, machine broninstellingen en vereisten.
* **Onderdeelservers**: Hallo processerver configuratieserver en hoofddoelserver

### <a name="considerations-for-hello-source-environment"></a>Overwegingen voor het Hallo-bronomgeving
* **Maximum schijfgrootte**: Hallo huidige maximale grootte van Hallo-schijf die aangesloten tooa virtuele machine worden kan is 1 TB. Maximale grootte van de bronschijf van een die kan worden gerepliceerd Hallo is dus ook beperkte too1 TB.
* **Maximale grootte per bron**: Hallo maximale grootte van een machine één bron wordt 31 TB (met 31 schijven) en met een D14-exemplaar dat is ingericht voor Hallo hoofddoelserver.
* **Aantal bronnen per hoofddoelserver**: meerdere bronmachines kunnen worden beveiligd met een enkele hoofddoelserver. Echter kan niet een machine één bron worden beveiligd op meerdere servers hoofddoel, omdat als schijven repliceren, een VHD die Hallo grootte van Hallo schijf weerspiegelt wordt gemaakt op Azure blob-opslag en gekoppeld als een schijf toohello hoofddoel beheerserver.  
* **Maximale dagelijkse wijzigingssnelheid per bron**: Er zijn drie factoren die toobe beschouwd als wanneer u overweegt Hallo aanbevolen moeten snelheid per bron wijzigen. Voor Hallo doel op basis van overwegingen zijn twee IOPS op Hallo doelschijf voor elke bewerking op de bron Hallo vereist. Dit is omdat het lezen van gegevens van oude en het schrijven van nieuwe gegevens Hallo op Hallo doelschijf gebeurt.
  * **Dagelijks wijzigen snelheid wordt ondersteund door de processerver Hallo**: een bronmachine kan niet meerdere processervers omvatten. Een server met een enkel proces kan van too1 TB van dagelijkse wijzigingssnelheid ondersteunen. Daarom is 1 TB Hallo maximale dagelijkse gegevens wijzigen snelheid voor een bronmachine wordt ondersteund.
  * **Maximale doorvoer wordt ondersteund door de doelschijf Hallo**: Maximum verloop per bronschijf kan niet meer dan 144 GB per dag (met de grootte van 8 kB schrijven). Zie de tabel Hallo in Hallo hoofddoel gedeelte voor het Hallo-doorvoer en IOPs van Hallo doel voor verschillende grootten voor schrijven. Dit nummer moet worden gedeeld door twee omdat elke bron IOP 2 IOPS op Hallo doelschijf genereert. Meer informatie over [Azure schaalbaarheids- en prestatiedoelen](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) bij het configureren van Hallo doel voor premium storage-accounts.
  * **Maximale doorvoer wordt ondersteund door de storage-account Hallo**: een bron kan niet meerdere opslagaccounts omvatten. Gegeven dat een opslagaccount in beslag neemt maximaal 20.000 aanvragen per seconde en dat elke bron IOP 2 IOPS op de hoofddoelserver Hallo genereert, adviseren we u Hallo aantal IOPS op Hallo bron too10, 000. Meer informatie over [Azure schaalbaarheids- en prestatiedoelen](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) bij het configureren van de bron Hallo voor premium storage-accounts.

### <a name="considerations-for-component-servers"></a>Overwegingen voor onderdeelservers
Tabel 1 bevat een overzicht van de grootte van virtuele machines Hallo voor Hallo configuratie- en hoofddoelservers.

| **Onderdeel** | **Geïmplementeerde Azure-exemplaren** | **Kernen** | **Geheugen** | **Maximum aantal schijven** | **Grootte van de schijf** |
| --- | --- | --- | --- | --- | --- |
| Configuratieserver |Standaard A3 |4 |7 GB |8 |1023 GB |
| Hoofddoelserver |Standaard A4 |8 |14 GB |16 |1023 GB |
| Standaard D14 |16 |112 GB |32 |1023 GB | |
| Standaard DS4 |8 |28 GB |16 |1023 GB | |

**Tabel 1**

#### <a name="process-server-considerations"></a>Processerver overwegingen
In het algemeen afhankelijk schaling van de hostserver proces van de dagelijkse wijzigingssnelheid Hallo op alle beveiligde werkbelastingen.

* U moet voldoende compute tooperform taken, zoals inline compressie en codering.
* Hallo processerver schijfcache gebruikt. Zorg ervoor dat Hallo cacheruimte aanbevolen en de doorvoercapaciteit van de schijf is beschikbaar toofacilitate Hallo gegevenswijzigingen zijn opgeslagen in het Hallo-gebeurtenis van knelpunt netwerk of een storing.
* Zorg ervoor dat voldoende bandbreedte zodat hello processerver Hallo gegevens toohello hoofddoel server tooprovide continue gegevensbescherming uploaden kunt.

Tabel 2 biedt een overzicht van Hallo proces server richtlijnen.

| **Snelheid van de gegevens wijzigen** | **CPU** | **Geheugen** | **Cachegrootte van de schijf** | **De doorvoercapaciteit van de cache-schijf** | **Bandbreedte inkomend en uitgaand** |
| --- | --- | --- | --- | --- | --- |
| < 300 GB |4 vcpu's (2-sockets * 2 kernen @ 2.5 GHz) |4 GB |600 GB |7 too10 MB per seconde |30 Mbps/21 Mbps |
| too600 300 GB |8 vcpu's (2-sockets * @ 2.5 GHz-4 kernen) |6 GB |600 GB |11 too15 MB per seconde |60 Mbps/42 Mbps |
| 600 GB too1 TB |12 vcpu's (2-sockets * @ 2.5 GHz-6 kernen) |8 GB |600 GB |too20 16 MB per seconde |100 Mbps/70 Mbps |
| > 1 TB |Een andere processerver implementeren | | | | |

**Tabel 2**

Waar:

* Inkomend is downloaden bandbreedte (intranet tussen de bron- en server Hallo).
* Uitgaande is het uploaden van bandbreedte (internet tussen de processerver Hallo en hoofddoelserver). Uitgaande getallen wordt ervan uitgegaan dat de gemiddelde 30% proces servercompressie.
* Voor cache wordt schijf een aparte OS-schijf van minimaal 128 GB aanbevolen voor alle processervers.
* Voor cache schijf doorvoer Hallo na opslag is gebruikt voor benchmarking: 8 SAS-schijven van 10 RPM met RAID 10-configuratie.

#### <a name="configuration-server-considerations"></a>Overwegingen voor configuratie-server
Elke configuratieserver kan ondersteunen van too100 bronmachines met 3 en 4-volumes. Als uw implementatie groter is raden wij dat u implementeert een andere configuratieserver. Zie tabel 1 voor Hallo standaardeigenschappen virtuele machine van de configuratieserver Hallo.

#### <a name="master-target-server-and-storage-account-considerations"></a>Overwegingen voor hoofddoel server en storage-account
Hallo-opslag voor elke hoofddoelserver bevat een besturingssysteemschijf, een bewaarvolume en gegevensschijven. Hallo bewaarstation onderhoudt Hallo journaal van schijfwijzigingen voor Hallo duur van de bewaarperiode Hallo gedefinieerd in Hallo Site Recovery-portal.  Raadpleeg tooTable 1 voor eigenschappen van de virtuele machine Hallo van Hallo hoofddoelserver. Tabel 3 laat zien hoe de schijven van A4 hello worden gebruikt.

| **Exemplaar** | **OS-schijf** | **Retentie** | **Gegevensschijven** |
| --- | --- | --- | --- |
| **Retentie** |**Gegevensschijven** | | |
| Standaard A4 |1 schijf (1 * 1023 GB) |1 schijf (1 * 1023 GB) |15 schijven (15 * 1023 GB) |
| Standaard D14 |1 schijf (1 * 1023 GB) |1 schijf (1 * 1023 GB) |31 schijven (15 * 1023 GB) |
| Standaard DS4 |1 schijf (1 * 1023 GB) |1 schijf (1 * 1023 GB) |15 schijven (15 * 1023 GB) |

**Tabel 3**

Afhankelijk van capaciteitsplanning voor Hallo hoofddoelserver:

* Prestaties van de Azure-opslag en beperkingen
  * Hallo maximum aantal schijven gebruikt voor een standaard laag VM maximaal, is ongeveer 40 (20.000/500 IOP's per schijf) in een enkel opslagaccount. Meer informatie over [schaalbaarheidsdoelen voor standard-opslagaccounts](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) en voor [premium storage-accounts](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
* Dagelijkse wijzigingssnelheid
* Bewaartermijn volume opslag.

Opmerking:

* Een bron kan niet meerdere opslagaccounts omvatten. Dit geldt toohello gegevensschijf die toohello storage-accounts is geselecteerd bij het configureren van beveiliging. Hallo OS en Hallo bewaren schijven gaat meestal toohello storage-account automatisch geïmplementeerd.
* Hallo opslag bewaarvolume vereist, is afhankelijk van de dagelijkse wijzigingssnelheid Hallo en Hallo aantal dagen bewaren. Hallo bewaren opslag vereist per hoofddoelserver totale verloop van bron per dag = * aantal dagen bewaren.
* Elke hoofddoelserver heeft slechts één bewaarvolume. Hallo bewaarvolume worden verdeeld over Hallo schijven gekoppelde toohello hoofddoelserver. Bijvoorbeeld:
  * Als er een bronmachine met 5 schijven en elke schijf 120 IOPS (grootte van 8 kB) op de bron hello genereert, betekent dit too240 IOP's per schijf (2 bewerkingen op Hallo doelschijf per bron i/o). 240 IOP's valt binnen hello Azure per schijf-IOPS limiet van 500.
  * Op het bewaarvolume hello, wordt dit 120 * 5 = 600 IOPS en dit kunnen een van de trechterhals bottle worden. In dit scenario zou een goede werkwijze tooadd worden meer schijven toohello-bewaarvolume en omvatten het opzij, als een RAID stripe-configuratie. Hierdoor nemen de prestaties omdat Hallo IOP's worden gedistribueerd over meerdere stations. het aantal stations toobe Hallo toegevoegd toohello bewaarvolume worden als volgt:
    * Totaal aantal IOPS van bronomgeving / 500
    * Totale verloop per dag uit bronomgeving (niet-gecomprimeerd) / 287 GB. 287 GB is de maximale doorvoer hello wordt ondersteund door een andere doelschijf per dag. Met deze metriek variëren, afhankelijk van de grootte van de Hallo schrijven met een factor van 8 kB omdat in dit geval 8 kB thee schrijven grootte wordt aangenomen. Bijvoorbeeld, als Hallo grootte geschreven is 4K wordt doorvoer 287/2. En als de grootte van Hallo schrijven 16K vervolgens doorvoer 287 * 2.
* aantal vereiste opslagaccounts voor Hallo = totale source IOPs/10000.

## <a name="before-you-start"></a>Voordat u begint
| **Onderdeel** | **Vereisten** | **Details** |
| --- | --- | --- |
| **Azure-account** |U hebt een [Microsoft Azure](https://azure.microsoft.com/)-account nodig. U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/). | |
| **Azure Storage** |U moet een Azure storage-account toostore gerepliceerde gegevens<br/><br/> Beide Hallo-account moet een [standaardaccount geografisch redundante opslag](../storage/common/storage-redundancy.md#geo-redundant-storage) of [Premium-Opslagaccount](../storage/common/storage-premium-storage.md).<br/><br/> Moet in dezelfde regio bevinden als hello Azure Site Recovery-service hello, en worden gekoppeld aan Hallo hetzelfde abonnement. We bieden geen ondersteuning voor Hallo verplaatsing van Storage-accounts die zijn gemaakt met behulp van Hallo [nieuwe Azure portal](../storage/common/storage-create-storage-account.md) over resourcegroepen.<br/><br/> Lees meer toolearn [tooMicrosoft inleiding Azure Storage](../storage/common/storage-introduction.md) | |
| **Virtuele Azure-netwerk** |U moet een Azure-netwerk op welke Hallo configuratieserver en de hoofddoelserver wordt geïmplementeerd. Deze moet Hallo hetzelfde abonnement en dezelfde regio bevinden als hello Azure Site Recovery-kluis. U kunt eventueel tooreplicate gegevens via een ExpressRoute- of VPN-verbinding hello Azure virtuele moet netwerk verbonden tooyour on-premises netwerk via een ExpressRoute-verbinding of een Site-naar-Site-VPN. | |
| **Azure-resources** |Zorg ervoor dat u hebt onvoldoende toodeploy Azure-resources van alle onderdelen. Meer informatie in [Azure-abonnementen](../azure-subscription-service-limits.md). | |
| **Virtuele machines van Azure** |Virtuele machines die u wilt dat tooprotect moet voldoen aan [vereisten voor Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).<br/><br/> **Aantal schijf**: maximaal 31 schijven kan worden ondersteund op een enkele, beveiligde server<br/><br/> **Schijf grootten**: capaciteit per schijf mag niet meer dan 1023 GB zijn<br/><br/> **Clustering**: geclusterde servers worden niet ondersteund<br/><br/> **Opstarten**: Unified Extensible Firmware Interface (UEFI) / Extensible Firmware Interface(EFI) wordt niet ondersteund<br/><br/> **Volumes**: Bitlocker versleutelde volumes worden niet ondersteund<br/><br/> **Servernamen**: namen moeten tussen 1 en maximaal 63 tekens bevatten (letters, cijfers en afbreekstreepjes) bevatten. Hallo-naam moet beginnen met een letter of cijfer en eindigen met een letter of cijfer. Nadat een machine is beveiligd, kunt u hello Azure naam wijzigen. | |
| **Configuratieserver** |Standaard A3 virtuele machine op basis van de installatiekopie van een Azure Site Recovery Windows Server 2012 R2-galerie wordt in uw abonnement voor de configuratieserver hello gemaakt. Het gemaakt als Hallo eerste instantie in een nieuwe cloudservice. Als u openbare Internet selecteert als het verbindingstype Hallo voor Hallo configuratie server Hallo cloud-service wordt gemaakt met een gereserveerde openbare IP-adres.<br/><br/> Hallo-installatiepad moet alleen Engelse tekens liggen. | |
| **Hoofddoelserver** |Virtuele machine van Azure, standaard A4, D14 of DS4.<br/><br/> Hallo-installatiepad moet alleen Engelse tekens liggen. Bijvoorbeeld Hallo-pad moet **/usr/local/ASR** voor een hoofddoelserver waarop Linux wordt uitgevoerd. | |
| **Processerver** |U kunt de processerver Hallo op fysieke of virtuele machine met Windows Server 2012 R2 met de nieuwste updates Hallo implementeren. Installeer op C: /.<br/><br/> Het is raadzaam u Hallo-server op Hallo plaatsen hetzelfde netwerk en subnet bevindt als de machines die u wilt dat tooprotect Hallo.<br/><br/> VMware vSphere CLI 5.5.0 op Hallo processerver installeren. Hallo VMware vSphere CLI onderdeel is vereist op de processerver Hallo in volgorde toodiscover virtuele machines die worden beheerd door een vCenter-server of virtuele machines op ESXi-host.<br/><br/> Hallo-installatiepad moet alleen Engelse tekens liggen.<br/><br/> ReFS-bestandssysteem wordt niet ondersteund. | |
| **VMware** |Een VMware vCenter-server uw VMware vSphere hypervisors te beheren. Worden moet gestart vCenter versie 5.1 of 5.5 met de nieuwste updates Hallo.<br/><br/> Een of meer vSphere hypervisors virtuele VMware-machines die wilt u tooprotect. Hallo hypervisor moet versie 5.1 of 5.5 ESX/ESXi worden uitgevoerd met de nieuwste updates Hallo.<br/><br/> Virtuele VMware-machines moet VMware tools geïnstalleerd en uitgevoerd. | |
| **Windows-machines** |Beveiligde fysieke servers of virtuele machines van VMware met Windows hebben een aantal vereisten.<br/><br/> Een ondersteund 64-bits besturingssysteem: **Windows Server 2012 R2**, **Windows Server 2012**, of **Windows Server 2008 R2 met op minimaal SP1**.<br/><br/> hostnaam, koppelpunten, apparaatnamen, systeempad Windows hello (bijvoorbeeld: C:\Windows) mag alleen in het Engels zijn.<br/><br/> Hallo-besturingssysteem moet worden geïnstalleerd op het station C:\.<br/><br/> Alleen standaardschijven worden ondersteund. Dynamische schijven worden niet ondersteund.<br/><br/> Firewallregels voor beveiligde machines moeten ze tooreach-Hallo configuratie en master doelservers in toestaan Azure.p ><p>U moet een administrator-account tooprovide (moet een lokale beheerder op de machine met Windows hello zijn) toopush Hallo Mobility-Service installeren op Windows-servers. Als Hallo opgegeven account een account niet tot een domein is moet u toodisable externe gebruiker toegangsbeheer op Hallo lokale machine. toodo deze Hallo toevoegen LocalAccountTokenFilterPolicy DWORD registervermelding met de waarde 1 onder HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System. tooadd hello registervermelding vanuit een CLI open cmd of powershell en voer  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** . [Meer informatie](https://msdn.microsoft.com/library/aa826699.aspx) over toegangsbeheer.<br/><br/> Als u wilt verbinding maken met tooWindows virtuele machines in Azure met extern bureaublad Zorg ervoor dat extern bureaublad is ingeschakeld voor Hallo lokale machine na een failover. Als u geen verbinding maakt via VPN, firewallregels voor extern bureaublad-verbindingen via Hallo moeten toestaan internet. | |
| **Linux-machines** |Een ondersteund 64-bits besturingssysteem: **Centos, 6.4, 6.5, 6.6**; **Oracle Enterprise Linux 6.4, 6.5 met Hallo Red Hat compatibel kernel of Unbreakable Enterprise Kernel versie 3 (UEK3)**, **SUSE Linux Enterprise Server 11 SP3**.<br/><br/> Firewallregels voor beveiligde machines mag worden ze tooreach Hallo configuratie- en hoofddoelservers in Azure.<br/><br/> de bestanden/etc/hosts op beveiligde machines moeten vermeldingen die zijn toegewezen Hallo lokale host naam tooIP adressen die zijn gekoppeld aan alle NIC's bevatten <br/><br/> Als u wilt dat tooconnect tooan Azure virtuele machine actief Linux nadat de failover via een Secure Shell-client (ssh), zorg ervoor dat Hallo Secure Shell-service op Hallo beveiligd machine toostart automatisch op opstarten van het systeem is ingesteld en dat firewall-regels toestaan een ssh verbinding tooit.<br/><br/> Hallo-hostnaam, koppelpunten, apparaat, en Linux systeempaden en bestandsnamen (bijvoorbeeld/etc /; /usr) moet in het Engels alleen.<br/><br/> Beveiliging kan worden ingeschakeld voor lokale machines Hello opslag te volgen:-<br>Bestandssysteem: EXT3, ETX4, ReiserFS, XFS<br>Multipath-software-apparaat toewijzen (MPIO)<br>Volumebeheer: LVM2<br>Fysieke servers met HP CCISS controller opslag worden niet ondersteund. | |
| **Van derden** |Sommige onderdelen voor implementatie in dit scenario is afhankelijk van software van derden toofunction goed de. Zie voor een volledige lijst [mededelingen van derden software en informatie](#third-party) | |

### <a name="network-connectivity"></a>Netwerkverbinding
U hebt twee opties bij het configureren van de netwerkverbinding tussen uw on-premises site en hello Azure-netwerk op welke Hallo infrastructuuronderdelen (configuratieserver, hoofddoelservers) zijn geïmplementeerd. U moet toodecide welke network connectivity optie toouse voordat u uw configuratieserver kunt implementeren. U moet deze instelling op moment van implementatie Hallo toochoose. Deze kan niet later worden gewijzigd.

**Internet:** communicatie en replicatie van gegevens tussen Hallo lokale servers (processerver, beveiligde machines) en hello Azure onderdeel infrastructuurservers (configuratieserver, hoofddoelserver), gebeurt via een veilige SSL / TLS-verbinding van de lokale toohello openbare eindpunten op Hallo configuratie en master doelservers. (Hallo enige uitzondering hierop is Hallo verbinding tussen de processerver Hallo en de hoofddoelserver Hallo op TCP-poort 9080 die niet versleuteld is. Alleen informatie over het beheer gerelateerde toohello replicatie protocol voor replicatie-instellingen voor deze verbinding wordt uitgewisseld.)

![Implementatie diagram internet](./media/site-recovery-vmware-to-azure-classic-legacy/internet-deployment.png)

**VPN**: communicatie en replicatie van gegevens tussen Hallo lokale servers (processerver, beveiligde machines) en hello Azure onderdeel infrastructuurservers (configuratieserver, hoofddoelserver), gebeurt via een VPN-verbinding tussen uw on-premises netwerk en hello Azure virtuele netwerk op welke Hallo configuratieserver en hoofddoelservers zijn geïmplementeerd. Zorg ervoor dat uw on-premises netwerk verbonden toohello virtuele Azure-netwerk door een ExpressRoute-verbinding of een site-naar-site VPN-verbinding.

![Diagram van de implementatie van VPN](./media/site-recovery-vmware-to-azure-classic-legacy/vpn-deployment.png)

## <a name="step-1-create-a-vault"></a>Stap 1: Een kluis maken
1. Meld u aan toohello [beheerportal](https://portal.azure.com).
2. Vouw **Data Services** > **Recovery Services** en klik op **Site Recovery-kluis**.
3. Klik op **Nieuw maken** > **Snelle invoer**.
4. In **naam**, voer een beschrijvende naam tooidentify Hallo-kluis.
5. In **regio**, selecteer de geografische regio voor de kluis Hallo Hallo. toocheck ondersteunde regio's Zie geografische beschikbaarheid in [prijsinformatie voor Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
6. Klik op **Kluis maken**.

    ![Nieuwe kluis](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-create-vault.png)

Selectievakje Hallo status balk tooconfirm die Hallo kluis is gemaakt. Hallo-kluis wordt weergegeven als **Active** op Hallo belangrijkste **Recovery Services** pagina.

## <a name="step-2-deploy-a-configuration-server"></a>Stap 2: Een configuratieserver implementeren
### <a name="configure-server-settings"></a>Server-instellingen configureren
1. In Hallo **Recovery Services** pagina, klikt u op Hallo kluis tooopen Hallo snel starten-pagina. Snel starten kan ook worden geopend op elk gewenst moment Hallo-pictogram.

    ![Pictogram Snel starten](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-icon.png)
2. Selecteer in de vervolgkeuzelijst Hallo **tussen een on-premises site met VMware of fysieke servers en Azure**.
3. In **voorbereiden Target(Azure) Resources** klikt u op **configuratieserver implementeren**.

    ![Configuratieserver implementeren](./media/site-recovery-vmware-to-azure-classic-legacy/deploy-cs2.png)
4. In **nieuwe Server configuratiedetails** opgeven:

   * Een naam voor Hallo configuratie server en referenties tooconnect tooit.
   * Vervolgkeuzelijst Hallo connectiviteit netwerktype Selecteer **openbare Internet** of **VPN**. Houd er rekening mee dat u deze instelling nadat deze toegepast niet wijzigen.
   * Selecteer hello Azure-netwerk op welke Hallo server moet zich bevinden. Als u VPN-Zorg ervoor dat is hello Azure-netwerk verbonden tooyour on-premises netwerk zoals verwacht.
   * Hallo interne IP-adres en subnet dat wordt toegewezen toohello server opgeven. Denk eraan dat de eerste vier IP-adressen in elk subnet Hallo zijn gereserveerd voor intern gebruik van Azure. Gebruik een ander beschikbaar IP-adres.

     ![Configuratieserver implementeren](./media/site-recovery-vmware-to-azure-classic-legacy/cs-details.png)
5. Wanneer u klikt op **OK** een standaard A3 virtuele machine op basis van de installatiekopie van een Azure Site Recovery Windows Server 2012 R2-galerie in uw abonnement voor de configuratieserver hello wordt gemaakt. Het gemaakt als Hallo eerste instantie in een nieuwe cloudservice. Als u tooconnect geselecteerd via Hallo internet Hallo-cloudservice wordt gemaakt met een gereserveerde openbare IP-adres. U kunt voortgang in Hallo **taken** tabblad.

    ![Voortgang van de monitor](./media/site-recovery-vmware-to-azure-classic-legacy/monitor-cs.png)
6. Als u verbinding via maakt internet, Hallo nadat Hallo configuratieserver geïmplementeerde Opmerking Hallo openbare IP-adres toegewezen tooit op Hallo is **virtuele Machines** pagina in hello Azure-portal. Klik op Hallo **eindpunten** tabblad Opmerking Hallo openbare HTTPS-poort toegewezen tooprivate poort 443. Wanneer u Hallo hoofddoel en processervers met de configuratieserver hello registreert, hebt u deze informatie later nodig. Hallo configuratieserver is geïmplementeerd met deze eindpunten:

   * HTTPS: Een openbare poort is gebruikte toocoordinate communicatie tussen onderdeelservers en Azure via internet Hallo. Particuliere poort 443 is gebruikte toocoordinate communicatie tussen onderdeelservers en Azure via VPN.
   * Aangepaste: Een openbare poort wordt gebruikt voor failback hulpprogramma communicatie via Hallo internet. Particuliere poort 9443 wordt gebruikt voor failback hulpprogramma communicatie via VPN.
   * PowerShell: Particuliere poort 5986
   * Extern bureaublad: particuliere poort 3389

   ![VM-eindpunten](./media/site-recovery-vmware-to-azure-classic-legacy/vm-endpoints.png)

   > [!WARNING]
   > Niet verwijderen of Hallo openbare of particuliere poort aantal eindpunten gemaakt tijdens de implementatie van configuratieserver wijzigen.
   >
   >

Hallo configuratieserver is geïmplementeerd in een automatisch gemaakte Azure cloudservice met een gereserveerd IP-adres. Hallo gereserveerd adres is benodigde tooensure die server cloud service IP-adres Hallo blijft Hallo dezelfde over Hallo virtuele machines (met inbegrip van de configuratieserver Hallo) op Hallo cloud-service opnieuw wordt opgestart. Hallo gereserveerde openbare IP-adres moet toobe handmatig niet-gereserveerde wanneer Hallo configuratieserver buiten werking wordt gesteld of het gereserveerde moet blijven. Er is een standaardlimiet van 20 gereserveerde openbare IP-adressen per abonnement. [Meer informatie](../virtual-network/virtual-networks-reserved-private-ip.md) over gereserveerde IP-adressen.

### <a name="register-hello-configuration-server-in-hello-vault"></a>Hallo configuratieserver in Hallo kluis registreren
1. In Hallo **Quick Start** pagina op **Doelresources voorbereiden** > **Download een registratiesleutel**. Hallo-sleutelbestand wordt automatisch gegenereerd. Het is geldig tot 5 dagen nadat deze gegenereerd. Kopieer de verbindingsreeks toohello configuratieserver.
2. In **virtuele Machines** Selecteer Hallo configuratieserver uit de lijst met virtuele machines Hallo. Open Hallo **Dashboard** tabblad en klik op **Connect**. **Open** Hallo gedownload RDP-bestand toolog op Hallo configuratieserver maken met extern bureaublad. Als u VPN, gebruikt u Hallo interne IP-adres (Hallo adres u hebt opgegeven tijdens de implementatie van configuratieserver Hallo) voor een extern bureaublad-verbinding van Hallo lokale site. Hallo Setup Wizard voor de Server van Azure Site Recovery-configuratie wordt automatisch uitgevoerd wanneer u zich aanmeldt voor Hallo eerst.

    ![Registratie](./media/site-recovery-vmware-to-azure-classic-legacy/splash.png)
3. In **installatie van de Software van derden** klikt u op **ik ga akkoord** toodownload en installeer MySQL.

    ![MySQL-installatie](./media/site-recovery-vmware-to-azure-classic-legacy/sql-eula.png)
4. In **MySQL Serverdetails** referenties toolog op Hallo MySQL server-exemplaar te maken.

    ![MySQL-referenties](./media/site-recovery-vmware-to-azure-classic-legacy/sql-password.png)
5. In **internetinstellingen** opgeven hoe de configuratieserver Hallo toohello wordt verbinding internet. Opmerking:

   * Als u wilt dat toouse een aangepaste proxy u moet instellen voordat u Hallo Provider installeert.
   * Wanneer u klikt op **volgende** wordt een test toocheck Hallo proxyverbinding uitgevoerd.
   * Als u een aangepaste proxy gebruikt, of als uw standaardproxy verificatie vereist moet u tooenter Hallo proxy-gegevens, inclusief Hallo-adres, poort en referenties.
   * Hallo volgende URL's moeten toegankelijk zijn via Hallo-proxy:
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * Als u IP-adressen gebaseerde firewallregels controleren of regels Hallo tooallow communicatie van Hallo configuratie toohello IP-adressen die worden beschreven zijn ingesteld [Azure Datacenter IP-adresbereiken](https://msdn.microsoft.com/library/azure/dn175718.aspx) en het protocol HTTPS (443). Hebt u IP-adresbereiken toowhite-lijst van hello Azure-regio die u van plan toouse en die van de VS-West bent.

     ![Registratie van proxy](./media/site-recovery-vmware-to-azure-classic-legacy/register-proxy.png)
6. In **fout bericht lokalisatie Providerinstellingen** aangeven in welke taal fout berichten tooappear.

    ![Fout bericht registratie](./media/site-recovery-vmware-to-azure-classic-legacy/register-locale.png)
7. In **Azure Site Recovery-registratie** bladeren en selecteer Hallo sleutelbestand u toohello server hebt gekopieerd.

    ![Registratie-sleutelbestand](./media/site-recovery-vmware-to-azure-classic-legacy/register-vault.png)
8. Hallo na voltooiing van de wizard Hallo deze opties selecteren:

   * Selecteer **starten Account Management dialoogvenster** toospecify die Accounts beheren dialoogvenster Hallo moet worden geopend nadat u Hallo wizard hebt voltooid.
   * Selecteer **bureaubladpictogram maken voor Cspsconfigtool** tooadd een snelkoppeling op het bureaublad op de configuratieserver Hallo zodat u Hallo openen kunt **Accounts beheren** dialoogvenster op elk gewenst moment zonder toorerun Hallo de wizard.

     ![Inschrijving voltooien](./media/site-recovery-vmware-to-azure-classic-legacy/register-final.png)
9. Klik op **voltooien** toocomplete Hallo-wizard. Een wachtwoordzin wordt gegenereerd. Kopieer de verbindingsreeks tooa veilige locatie. U moet deze tooauthenticate en Hallo-proces en hoofddoelservers registreren met de configuratieserver Hallo. Het is ook tooensure kanaal integriteit in servercommunicatie configuratie gebruikt. Hallo wachtwoordzin kan opnieuw worden gegenereerd, maar u moet toore registreren Hallo hoofddoel en processervers met de nieuwe wachtwoordzin Hallo.

    ![Wachtwoordzin](./media/site-recovery-vmware-to-azure-classic-legacy/passphrase.png)

Na de registratie Hallo configuratieserver wordt aangeboden op Hallo **configuratieservers** pagina in Hallo kluis.

### <a name="set-up-and-manage-accounts"></a>Instellen en beheren van accounts
Tijdens de implementatie van Site Recovery-referenties voor de volgende activiteiten Hallo aanvragen:

* Een VMware-account dus thatSite herstel kunnen automatisch detectie van virtuele machines op de vCenter-servers of vSphere-hosts.
* Wanneer u voor beveiliging, toevoegen zodat Site Recovery Hallo Mobility-service op deze kunt installeren.

Nadat u zich hebt ingeschreven met de configuratieserver Hallo kunt u Hallo openen **Accounts beheren** dialoogvenster tooadd en accounts beheren die moeten worden gebruikt voor deze acties. Er zijn een aantal manieren toodo dit:

* Hallo-snelkoppeling die u hebt gekozen toocreated voor Hallo dialoogvenster op de laatste pagina Hallo van setup voor de configuratieserver hello (cspsconfigtool) openen.
* Open Hallo dialoogvenster op voltooien van de server-configuratie.

1. In **Accounts beheren** klikt u op **Account toevoegen**. U kunt ook wijzigen en verwijderen van bestaande accounts.

    ![Accounts beheren](./media/site-recovery-vmware-to-azure-classic-legacy/manage-account.png)
2. In **accountdetails** opgeven van een account naam toouse in Azure en referenties (domein/gebruikersnaam).

    ![Accounts beheren](./media/site-recovery-vmware-to-azure-classic-legacy/account-details.png)

### <a name="connect-toohello-configuration-server"></a>Verbinding maken met de configuratieserver toohello
Er zijn twee manieren toohello tooconnect configuratieserver:

* Via een VPN-site-naar-site of een ExpressRoute-verbinding
* Via internet Hallo

Opmerking:

* Hallo eindpunten van Hallo virtuele machine een internetverbinding gebruikt in combinatie met Hallo openbare virtuele IP-adres van de server Hallo.
* Een VPN-verbinding maakt gebruik van interne IP-adres van de server Hallo Hallo samen met de Hallo eindpunt particuliere poorten.
* Hiermee wordt aangegeven of is een eenmalige beslissing toodecide tooconnect (beheer- en replicatie-gegevens) van uw lokale servers toohello verschillende onderdeelservers (configuratieserver, hoofddoelserver) in Azure wordt uitgevoerd via een VPN-verbinding of Hallo internet. U kan niet deze instelling daarna wijzigen. Als u dit u doet zult moet tooredeploy Hallo scenario en uw computers beveiligt.  

## <a name="step-3-deploy-hello-master-target-server"></a>Stap 3: De hoofddoelserver Hallo implementeren
1. Klik op **voorbereiden Target(Azure) Resources** > **hoofddoelserver implementeren**.
2. Hallo hoofddoel Serverdetails en referenties opgeven. Hallo-server worden geïmplementeerd in Hallo dezelfde Azure-netwerk als Hallo configuratieserver. Wanneer u klikt op toocomplete wordt Azure een virtuele machine wordt gemaakt met een installatiekopie van Windows of Linux-galerie.

    ![Doel-serverinstellingen](./media/site-recovery-vmware-to-azure-classic-legacy/target-details.png)

Denk eraan dat de eerste vier IP-adressen in elk subnet Hallo zijn gereserveerd voor intern gebruik van Azure. Geef een ander beschikbaar IP-adres.

> [!NOTE]
> Selecteer standaard DS4 bij het configureren van beveiliging voor werkbelastingen waarvoor consistent hoge i/o-prestaties en lage latentie in volgorde toohost i/o intensieve werkbelastingen met behulp van [Premium-Opslagaccount](../storage/common/storage-premium-storage.md).
>
>

1. Een Windows-master doelserver virtuele machine wordt gemaakt met deze eindpunten. Houd er rekening mee dat openbare eindpunten alleen gemaakt worden als de verbinding maken via internet Hallo.

   * Aangepaste: Openbare poort die worden gebruikt door Hallo proces toosend replicatie servergegevens via Hallo internet. Particuliere poort 9443 wordt gebruikt door Hallo proces server toosend replicatie gegevens toohello hoofddoelserver via VPN.
   * Custom1: Openbare poort die worden gebruikt door Hallo proces servermetagegevens toosend via Hallo internet. Particuliere poort 9080 wordt gebruikt door Hallo proces server toosend metagegevens toohello hoofddoelserver via VPN.
   * PowerShell: Particuliere poort 5986
   * Extern bureaublad: particuliere poort 3389
2. Een Linux hoofddoelserver VM is gemaakt met deze eindpunten. Houd er rekening mee dat openbare eindpunten alleen gemaakt worden als u verbinding via Hallo maakt internet.

   * Aangepaste: Openbare poort die worden gebruikt door het proces server toosend replicatiegegevens via Hallo internet. Particuliere poort 9443 wordt gebruikt door Hallo proces server toosend replicatie gegevens toohello hoofddoelserver via VPN.
   * Custom1: Openbare poort wordt gebruikt door Hallo proces servermetagegevens toosend via Hallo internet. Particuliere poort 9080 wordt gebruikt door Hallo proces server toosend metagegevens toohello hoofddoelserver via VPN
   * SSH: Particuliere poort 22

     > [!WARNING]
     > Geen verwijderen of wijzigen Hallo openbare of particuliere poortnummer van een Hallo eindpunten is gemaakt tijdens de implementatie van Hallo hoofddoel server.
     >
     >
3. In **virtuele Machines** Hallo virtuele machine toostart wacht.

   * Als het een Windows server Noteer Hallo remote desktop-gegevens.
   * Als een Linux-server is en u verbinding via de VPN-Opmerking Hallo interne IP-adres van Hallo virtuele machine maakt waarmee. Als u verbinding via Hallo internet Opmerking Hallo openbaar IP-adres maakt.
4. Hallo-serverinstallatie toocomplete aanmelden en registreren met de configuratieserver Hallo.
5. Als u Windows uitvoert:

   1. Een verbinding met extern bureaublad toohello virtuele machine starten. Hallo wordt eerste keer dat u zich aanmeldt een script uitgevoerd in een PowerShell-venster. Niet sluiten. Wanneer deze is voltooid Hallo Host Agent Config hulpprogramma wordt automatisch geopend tooregister Hallo-server.
   2. In **Host Agent Config** Hallo interne IP-adres van de configuratieserver Hallo en poort 443. U kunt zelfs als u geen verbinding maakt via VPN omdat Hallo virtuele machine gekoppelde toohello Hallo interne adres en particuliere poort 443 gebruiken dezelfde Azure-netwerk als Hallo configuratieserver. Laat **gebruik HTTPS** ingeschakeld. Voer Hallo wachtwoordzin voor Hallo configuratieserver die u eerder hebt genoteerd. Klik op **OK** tooregister Hallo-server. U kunt Hallo NAT opties negeren. Deze worden niet gebruikt.
   3. Als de vereiste van het systeemstation geschatte bewaarperiode meer dan 1 TB is kunt u configureren Hallo-bewaarvolume (R:) met een virtuele schijf en [opslagruimten](http://blogs.technet.com/b/askpfeplat/archive/2013/10/21/storage-spaces-how-to-configure-storage-tiers-with-windows-server-2012-r2.aspx)

   ![De hoofddoelserver Windows](./media/site-recovery-vmware-to-azure-classic-legacy/target-register.png)
6. Als u werkt met Linux:

   1. Zorg ervoor dat u hebt geïnstalleerd Hallo nieuwste Linux Integration Services (LIS) geïnstalleerd voordat u de hoofddoelserver Hallo installeren. U vindt Hallo meest recente versie van LIS samen met instructies over het tooinstall [hier](https://www.microsoft.com/download/details.aspx?id=46842). Hallo machine starten nadat Hallo LIS hebt geïnstalleerd.
   2. In **voorbereiden (Azure) Doelresources** klikt u op **downloaden en installeren van extra software (alleen voor Linux Hoofddoelserver)**. Kopiëren Hallo gedownload tar-bestand toohello virtuele machine met behulp van een client sftp. U kunt ook toohello geïmplementeerde linux hoofddoelserver aanmelden en gebruik *wget http://go.microsoft.com/fwlink/?LinkID=529757&clcid=0x409* toodownload Hallo Hallo-bestand.
   3. Meld u aan met behulp van een client Secure Shell toohello-server. Als u bent verbonden gebruiken toohello Azure-netwerk via VPN Hallo interne IP-adres. Gebruik anders Hallo externe IP-adres en Hallo SSH openbaar eindpunt.
   4. Hallo-bestanden extraheren uit Hallo gzipped installatieprogramma door te voeren: **– xvzf Microsoft tar-ASR_UA_8.4.0.0_RHEL6-64***
      ![hoofddoelserver Linux](./media/site-recovery-vmware-to-azure-classic-legacy/linux-tar.png)
   5. Zorg ervoor dat u bent klaar Hallo directory toowhich u Hallo inhoud van Hallo tar-bestand hebt uitgepakt.
   6. Hallo configuratie server wachtwoordzin tooa lokale bestand kopiëren met de opdracht Hallo **echo  *`<passphrase>`*  > passphrase.txt**
   7. Hallo-opdracht uitvoeren '**sudo. / -t installeren beide - a host -R -d /usr/local/ASR MasterTarget -i  *`<Configuration server internal IP address>`*  -p 443 -s y - c https -P passphrase.txt**'.

      ![Registreren van de doelserver](./media/site-recovery-vmware-to-azure-classic-legacy/linux-mt-install.png)
7. Wacht een paar minuten (10-15) en op Hallo pagina controleren die Hallo hoofddoelserver wordt vermeld als geregistreerd in **Servers** > **configuratieservers** **Serverdetails** tabblad. Als u Linux uitvoert en niet hebt geregistreerd Hallo host-configuratieprogramma opnieuw uitvoeren van /usr/local/ASR/Vx/bin/hostconfigcli. U moet toegangsmachtigingen tooset type chmod als hoofdmap uitvoert.

    ![Controleer of de doelserver](./media/site-recovery-vmware-to-azure-classic-legacy/target-server-list.png)

> [!NOTE]
> Het kan duren too15 minuten nadat de registratie is voltooid voor Hallo hoofddoel server toobe die worden vermeld in het Hallo-portal. tooupdate onmiddellijk, klikt u op **vernieuwen** op Hallo **configuratieservers** pagina.
>
>

## <a name="step-4-deploy-hello-on-premises-process-server"></a>Stap 4: Hallo lokale processerver implementeren
Voordat u begint met het is raadzaam een statisch IP-adres op de processerver hello te configureren zodat kan worden gegarandeerd toobe permanente meerdere opnieuw wordt opgestart.

1. Klik op Snel starten > **processerver installeren lokale** > **downloaden en installeren van de processerver Hallo**.

    ![Processerver installeren](./media/site-recovery-vmware-to-azure-classic-legacy/ps-deploy.png)
2. Kopiëren Hallo gedownload zip-bestand toohello server waarop u tooinstall Hallo processerver gaat. Hallo zip-bestand bevat twee bestanden voor installatie:

   * Microsoft-ASR_CX_TP_8.4.0.0_Windows*
   * Microsoft-ASR_CX_8.4.0.0_Windows*
3. Pak Hallo archiveren en kopieer Hallo tooa locatie van installatie op Hallo-server.
4. Voer Hallo **Microsoft-ASR_CX_TP_8.4.0.0_Windows*** installatiebestand en volg de instructies Hallo. Hiermee installeert u onderdelen van derden die nodig zijn voor het Hallo-implementatie.
5. Voer **Microsoft-ASR_CX_8.4.0.0_Windows***.
6. Op Hallo **servermodus** pagina **processerver**.
7. Op Hallo **omgeving Details** pagina Hallo te volgen:

    - Als u wilt dat tooprotect VMware-virtuele machines Klik **Ja**
    - Als u wilt dat alleen tooprotect fysieke servers en VMware vCLI geïnstalleerd op de processerver Hallo derhalve niet nodig. Klik op **Nee** en door te gaan.

1. Houd er rekening mee Hallo volgende bij het installeren van VMware vCLI:

   * **Alleen VMware vSphere CLI 5.5.0 wordt ondersteund**. Hallo processerver werkt niet met andere versies of vSphere CLI-updates.
   * Downloaden van vSphere CLI 5.5.0 van [hier.](https://my.vmware.com/web/vmware/details?downloadGroup=VCLI550&productId=352)
   * Als u vSphere CLI hebt geïnstalleerd voordat Hallo processerver installeren is gestart en setup niet worden gedetecteerd, van toofive minuten wachten voordat u setup opnieuw proberen. Dit zorgt ervoor dat alle Hallo omgevingsvariabelen die nodig zijn voor de detectie van vSphere CLI hebt juist geïnitialiseerd.
2. In **NIC selectie voor processerver** Selecteer Hallo-netwerkadapter die Hallo processerver moet gebruiken.

   ![Adapter selecteren](./media/site-recovery-vmware-to-azure-classic-legacy/ps-nic.png)
3. In **Server configuratiedetails**:

   * Geef Hallo interne IP-adres van de configuratieserver Hallo en 443 voor Hallo-poort voor Hallo IP-adres en poort, als u verbinding via VPN maakt. Anders Hallo openbare virtuele IP-adres en toegewezen openbare HTTP-eindpunt opgeven.
   * Typ in het Hallo wachtwoordzin van Hallo configuratieserver.
   * Schakel **controleren Mobility service software handtekening** als u wilt dat toodisable verificatie wanneer u automatische push tooinstall Hallo service gebruiken. Handtekeningverificatie moet een internetverbinding vanaf de processerver Hallo.
   * Klik op **Volgende**.

   ![Configuratieserver registreren](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cs.png)
4. In **Selecteer installatiestation** een cachestation te selecteren. Hallo processerver moet een cachestation met ten minste 600 GB vrije ruimte. Klik vervolgens op **Installeren**.

   ![Configuratieserver registreren](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cache.png)
5. Houd er rekening mee dat u toorestart hello toocomplete Hallo serverinstallatie wellicht. In **configuratieserver** > **Serverdetails** die Hallo processerver wordt weergegeven en is geregistreerd in kluis Hallo controleren.

> [!NOTE]
> Too15 minuten nadat de registratie is voltooid voor Hallo proces server tooappear zoals vermeld onder de configuratieserver Hallo kan duren. Hallo configuratieserver tooupdate onmiddellijk vernieuwen door te klikken op de knop Vernieuwen Hallo onder Hallo van configuratiepagina Hallo van server
>
>

![Processerver valideren](./media/site-recovery-vmware-to-azure-classic-legacy/ps-register.png)

U kunt dit als handtekeningverificatie voor Hallo Mobility-service niet is uitgeschakeld bij de registratie van de processerver hello later als volgt doen:

1. Meld u aan bij de processerver Hallo als beheerder en open Hallo bestand C:\pushinstallsvc\pushinstaller.conf voor bewerken. Onder de sectie Hallo **[PushInstaller.transport]** toevoegen van deze regel: **SignatureVerificationChecks = '0'**. Opslaan en sluiten Hallo-bestand.
2. Hallo InMage PushInstall-service opnieuw opstarten

## <a name="step-5-update-site-recovery-components"></a>Stap 5: Update Site Recovery-onderdelen
Site Recovery-onderdelen worden uit tootime tijd bijgewerkt. Wanneer nieuwe updates beschikbaar zijn moet u deze in volgorde Hallo installeren:

1. Configuratieserver
2. Processerver
3. Hoofddoelserver
4. Failback hulpprogramma (vContinuum)

### <a name="obtain-and-install-hello-updates"></a>Downloaden en installeren van updates Hallo
1. U kunt updates voor Hallo configuratie, proces- en hoofddoelservers verkrijgen van Site Recovery Hallo **Dashboard**. Voor de installatie van Linux uitpakken Hallo van Hallo gzipped installatieprogramma en Voer Hallo-opdracht ' sudo. / installeren ' tooinstall Hallo update.
2. [Download](http://go.microsoft.com/fwlink/?LinkID=533813) Hallo meest recente update voor Hallo Failback tool(vContinuum).
3. Als u virtuele machines of fysieke servers die al Hallo Mobility-service geïnstalleerd uitvoert, kunt u als volgt updates downloaden voor Hallo-service:

   * **Optie 1**: updates downloaden:
     * [Windows Server (alleen 64 bits)](http://download.microsoft.com/download/8/4/8/8487F25A-E7D9-4810-99E4-6C18DF13A6D3/Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe)
     * [CentOS 6.4,6.5,6.6 (alleen 64 bits)](http://download.microsoft.com/download/7/E/D/7ED50614-1FE1-41F8-B4D2-25D73F623E9B/Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz)
     * [Oracle Enterprise Linux 6.4,6.5 (alleen 64 bits)](http://download.microsoft.com/download/5/2/6/526AFE4B-7280-4DC6-B10B-BA3FD18B8091/Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz)
     * [SUSE Linux Enterprise Server SP3 (alleen 64 bits)](http://download.microsoft.com/download/B/4/2/B4229162-C25C-4DB2-AD40-D0AE90F92305/Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz)
     * Na het bijwerken van Hallo proces server Hallo zijn bijgewerkte versie van de Mobility-service Hallo beschikbaar in Hallo C:\pushinstallsvc\repository map op de processerver Hallo.
   * **Optie 2**: als er een machine met een oudere versie van Hallo Mobility-service is geïnstalleerd, u kunt automatisch upgraden Hallo Mobility-service op de machine Hallo Hallo-beheerportal.

     1. Zorg ervoor dat processerver hello wordt bijgewerkt.
     2. Ervoor zorgen dat de beveiligde machine Hallo voldoet aan de Hallo [vereisten](#install-the-mobility-service-automatically) voor automatisch pushen Hallo Mobility-service, zodat Hallo update werkt zoals verwacht.
     3. Selecteer Hallo beveiligingsgroep, markeer Hallo beveiligd machine en klik op **Update Mobility-service**. Deze knop is alleen beschikbaar als er een nieuwere versie van Hallo Mobility-service.

         ![Selecteer de vCenter-server](./media/site-recovery-vmware-to-azure-classic-legacy/update-mobility.png)

Geef in Select-accounts Hallo administrator-account gebruikt toobe tooupdate Hallo mobility-service op Hallo beveiligde server. Klik op OK en wachten op Hallo geactiveerd taak toocomplete.

## <a name="step-6-add-vcenter-servers-or-vsphere-hosts"></a>Stap 6: VCenter-servers of vSphere-hosts toevoegen
1. Klik op **Servers** > **configuratieservers** > configuratieserver >**vCenter-Server toevoegen** tooadd een vCenter-server of vSphere-host.

    ![Selecteer de vCenter-server](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter.png)
2. Geef details op voor het Hallo-server of de host en de processerver Selecteer Hallo die gebruikt toodiscover worden deze.

   * Geef Hallo-poortnummer op welke Hallo vCenter-server wordt uitgevoerd als Hallo vCenter-server niet wordt uitgevoerd op Hallo-standaardpoort 443.
   * Hallo-process-server moet zich op Hallo hetzelfde netwerk als Hallo vCenter server/vSphere-host en VMware vSphere CLI 5.5.0 geïnstalleerd moeten hebben.

     ![instellingen van de vCenter-server](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter4.png)
3. Nadat de detectie is voltooid wordt onder Hallo server configuratiedetails Hallo vCenter-server vermeld.

    ![instellingen van de vCenter-server](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter2.png)
4. Als u een niet-administratoraccount tooadd Hallo server of de host gebruikt, zorg er dan voor dat account Hallo heeft Hallo volgende bevoegdheden:

   * vCenter accounts hebt Datacenter, gegevensopslag, map, Host, netwerk, Resource, opslag weergaven, virtuele machine en vSphere gedistribueerd Switch bevoegdheden is ingeschakeld.
   * vSphere host accounts hebt Hallo Datacenter, gegevensopslag, map, Host, netwerk, Resource, virtuele machine en vSphere gedistribueerd Switch bevoegdheden ingeschakeld

## <a name="step-7-create-a-protection-group"></a>Stap 7: Een beveiligingsgroep maken
1. Open **beveiligde Items** > **beveiligingsgroep** > **beveiligingsgroep maken**.

    ![Beveiligingsgroep maken](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg1.png)
2. Op Hallo **instellingen voor de beveiligingsgroep opgeven** pagina voor het Hallo-groep en selecteer Hallo configuratieserver waarop u wilt dat toocreate Hallo groep een naam opgeven.

    ![Instellingen voor de beveiligingsgroep](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg2.png)
3. Op Hallo **replicatie-instellingen opgeven** pagina Hallo replicatie-instellingen die worden gebruikt voor alle Hallo-machines in de groep Hallo configureren.

    ![Beveiliging groep Replicatie](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg3.png)
4. Instellingen:

   * **Consistentie tussen Multi-VM's**: als u dit inschakelen op gedeelde toepassingsconsistente herstelpunten over Hallo-machines in de beveiligingsgroep Hallo maakt. Deze instelling is meest relevante wanneer alle machines in de beveiligingsgroep Hallo HALLO hallo dezelfde werkbelasting. Alle machines herstelde toohello worden dezelfde gegevenspunt. Alleen beschikbaar voor Windows-servers.
   * **Drempelwaarde voor RPO**: waarschuwingen worden gegenereerd wanneer het Hallo continue beveiliging gegevensreplicatie RPO Hallo geconfigureerd RPO drempelwaarde overschrijdt.
   * **Herstel bewaarperiode**: Hiermee geeft u de bewaarperiode Hallo. Beveiligde machines kunnen worden hersteld tooany punt binnen dit venster.
   * **Toepassingsconsistente momentopnamen frequentie**: geeft aan hoe vaak de herstelpunten met toepassingsconsistente momentopnamen worden gemaakt.

U kunt Hallo beveiligingsgroep controleren als ze worden gemaakt op Hallo **beveiligde Items** pagina.

## <a name="step-8-set-up-machines-you-want-tooprotect"></a>Stap 8: Computers instellen gewenste tooprotect
U moet tooinstall Hallo Mobility-service op de virtuele machines en fysieke servers die u wilt dat tooprotect. U kunt dit op twee manieren doen:

* Automatisch push en Hallo service installeren op elke machine van de processerver Hallo.
* Hallo-service handmatig te installeren.

### <a name="install-hello-mobility-service-automatically"></a>Hallo Mobility-service automatisch geïnstalleerd
Wanneer u toevoegt wordt machines tooa beveiliging groep Hallo Mobility-service automatisch gepusht en geïnstalleerd op elke machine door Hallo processerver.

**Automatisch installeren push Hallo mobility-service op Windows-servers:**

1. Meest recente updates voor de processerver Hallo Hallo installeren zoals is beschreven in [stap 5: Installeer de meest recente updates](#step-5-install-latest-updates), en zorg ervoor dat proces Hallo server beschikbaar is.
2. Zorg ervoor dat er een netwerkverbinding is tussen de bronmachine hello en hello processerver en de desbetreffende bronmachine Hallo toegankelijk is vanaf de processerver Hallo.  
3. Configureer Hallo Windows firewall tooallow **bestands- en printerdeling** en **Windows Management Instrumentation**. Onder Windows Firewall-instellingen 'Toestaan dat een app of functie via Firewall' hello optie selecteren en selecteer Hallo toepassingen zoals weergegeven in volgende Hallo-afbeelding. Voor de machines die deel uitmaken van tooa domein kunt u Hallo firewall-beleid configureren met een groepsbeleidsobject.

    ![Firewallinstellingen](./media/site-recovery-vmware-to-azure-classic-legacy/push-firewall.png)
4. Hallo-account gebruikt tooperform Hallo push-installatie moet Hallo-beheerdersgroep op Hallo machine gewenste tooprotect. Deze referenties worden alleen gebruikt voor de push-installatie van Mobility-service Hallo en u hebt deze opgeven wanneer u een machine tooa-beveiligingsgroep toevoegen.
5. Als Hallo opgegeven account een domeinaccount is niet moet u toodisable externe gebruiker toegangsbeheer op Hallo lokale machine. toodo deze Hallo toevoegen LocalAccountTokenFilterPolicy DWORD registervermelding met de waarde 1 onder HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System. tooadd hello registervermelding vanuit een CLI open cmd of powershell en voer  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** .

**Automatisch installeren push Hallo mobility-service op Linux-servers:**

1. Meest recente updates voor de processerver Hallo Hallo installeren zoals is beschreven in [stap 5: Installeer de meest recente updates](#step-5-install-latest-updates), en zorg ervoor dat proces Hallo server beschikbaar is.
2. Zorg ervoor dat er een netwerkverbinding is tussen de bronmachine hello en hello processerver en de desbetreffende bronmachine Hallo toegankelijk is vanaf de processerver Hallo.  
3. Zorg ervoor dat het Hallo-account is een Hoofdgebruiker op de bronserver Linux Hallo.
4. Zorg ervoor dat bestand Hallo/etc/hosts op de bron Hallo server bevat items die zijn toegewezen Hallo lokale host naam tooIP adressen die zijn gekoppeld aan alle NIC's Linux.
5. Installeer de meest recente openssh hello, openssh-server, openssl-pakketten op Hallo machine gewenste tooprotect.
6. Zorg ervoor dat SSH is ingeschakeld en wordt uitgevoerd op poort 22.
7. SFTP subsysteem voor verificatie en wachtwoord in Hallo sshd_config bestand als volgt inschakelen:

   * een) aanmelden als hoofdmap.
   * b) in Hallo bestand/etc/ssh/sshd_config-bestand, zoek Hallo regel die begint met **PasswordAuthentication**.
   * c) Opmerking Hallo regel verwijderen en waarde van 'no' hello te 'Ja' wijzigen.

       ![Linux-mobiliteit](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push.png)
   * d) zoeken Hallo regel die begint met het subsysteem en het commentaar verwijderen Hallo regel.

       ![Mobiliteit van Linux-push](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push2.png)    
8. Zorg ervoor dat Hallo bron machine Linux-variant wordt ondersteund.

### <a name="install-hello-mobility-service-manually"></a>Hallo Mobility-service handmatig installeren
Hallo softwarepakketten tooinstall Hallo Mobility-service op de processerver Hallo in C:\pushinstallsvc\repository worden gebruikt. Zich aanmeldt bij de processerver Hallo en kopiëren Hallo juiste installatie pakket toohello bronmachine op basis van de volgende tabel voor Hallo:-

| Bronbesturingssysteem | Pakket van de Mobility-service op de processerver |
| --- | --- |
| Windows Server (alleen 64-bits) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe` |
| CentOS 6.4, 6.5, 6.6 (alleen 64-bits) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz` |
| SUSE Linux Enterprise Server 11 SP3 (alleen 64-bits) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz` |
| Oracle Enterprise Linux 6.4, 6.5 (alleen 64-bits) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz` |

**tooinstall hello Mobility-service handmatig op een WindowsServer**, Hallo te volgen:

1. Kopiëren Hallo **Microsoft ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe** pakket van Hallo proces server mappad in bovenstaande toohello bronmachine Hallo tabel vermeld.
2. Hallo Mobility-service door te voeren uitvoerbare Hallo op de bronmachine Hallo installeren.
3. Hallo installer-instructies.
4. Selecteer **Mobility-service** als Hallo-rol en klik op **volgende**.

    ![Installeren van de mobility-service](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install.png)
5. Laat de installatiemap Hallo als standaardinstallatiepad Hallo en klik op **installeren**.
6. In **Host Agent Config** Hallo IP-adres- en HTTPS-poort van de configuratieserver Hallo opgeven.

   * Als u verbinding maakt via internet Geef Hallo Hallo openbare virtuele IP-adres en openbare HTTPS-eindpunt als Hallo-poort.
   * Als u verbinding via VPN maakt opgeven Hallo interne IP-adres en poort 443 voor Hallo-poort. Laat **gebruik HTTPS** gecontroleerd.

     ![Installeren van de mobility-service](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install2.png)
7. Hallo configuratie server wachtwoordzin opgeven en klik op **OK** tooregister Hallo Mobility-service met de configuratieserver Hallo.

**toorun vanaf de opdrachtregel Hallo:**

1. Kopieer Hallo wachtwoordzin van Hallo CX toohello bestand 'C:\connection.passphrase' op Hallo-server en voer deze opdracht. In ons voorbeeld CX i 104.40.75.37 en Hallo HTTPS-poort is 62519:

    `C:\Microsoft-ASR_UA_8.2.0.0_Windows_PREVIEW_20Mar2015_Release.exe" -ip 104.40.75.37 -port 62519 -mode UA /LOG="C:\stdout.txt" /DIR="C:\Program Files (x86)\Microsoft Azure Site Recovery" /VERYSILENT  /SUPPRESSMSGBOXES /norestart  -usesysvolumes  /CommunicationMode https /PassphrasePath "C:\connection.passphrase"`

**Hallo Mobility-service handmatig te installeren op een Linux-server**:

1. Hallo juiste tar-archief op basis van de tabel Hallo hierboven van toohello bronmachine voor Hallo proces server kopiëren.
2. Een shellprogramma openen en uitpakken van Hallo gecomprimeerde tar-archief tooa lokaal pad door te voeren`tar -xvzf Microsoft-ASR_UA_8.2.0.0*`
3. Maak een bestand passphrase.txt in Hallo lokale directory toowhich u extraheerde Hallo van Hallo tar-archief door te voeren  *`echo <passphrase> >passphrase.txt`*  vanuit shell.
4. Hallo Mobility-service installeren door te voeren  *`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`* .
5. Geef Hallo IP-adres en poort:

   * Als u de configuratieserver toohello verbinding via internet Geef Hallo server virtuele openbare IP-adres en openbare HTTPS-eindpunt in Hallo `<IP address>` en `<port>`.
   * Als u verbinding via een VPN-verbinding maakt opgeven Hallo interne IP-adres en poort 443.

**toorun vanaf de opdrachtregel Hallo**:

1. Kopieer Hallo wachtwoordzin van Hallo CX toohello bestand 'passphrase.txt' op Hallo-server en voer deze opdrachten. In ons voorbeeld CX i 104.40.75.37 en Hallo HTTPS-poort is 62519:

tooinstall op een productieserver:

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

tooinstall op Hallo-doelserver:

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

> [!NOTE]
> Wanneer u machines tooa beveiligingsgroep die al een juiste versie van Hallo Mobility-service worden uitgevoerd en vervolgens Hallo push-installatie wordt overgeslagen toevoegt.
>
>

## <a name="step-9-enable-protection"></a>Stap 9: Inschakelen van de beveiliging
tooenable beveiliging u virtuele machines en fysieke servers tooa beveiligingsgroep toevoegen. Houd rekening met het volgende voordat u begint:

* Virtuele machines om de 15 minuten worden gedetecteerd en too15 minuten voordat ze kunnen er tooappear in Azure Site Recovery na de detectie.
* Omgevingswijzigingen op Hallo virtuele machine (zoals VMware tools-installatie) kunnen de too15 minuten toobe bijgewerkt in Site Recovery ook duren.
* U kunt controleren Hallo gedetecteerd laatste tijd in Hallo **laatste CONTACT op** veld Hallo vCenter server/ESXi-host op Hallo **configuratieservers** pagina.
* Als u een beveiligingsgroep die al is gemaakt hebt en het toevoegen van een vCenter-Server of ESXi-host hierna, duurt het vijftien minuten voor hello Azure Site Recovery-portal toorefresh en toobe van virtuele machines die worden vermeld in Hallo **Add machines tooa beveiligingsgroep**  dialoogvenster.
* Als u tooproceed onmiddellijk met machines tooprotection groep toe te voegen wilt zonder te wachten Hallo geplande detectie, markeer Hallo configuratieserver (Klik niet op deze) en klik op Hallo **vernieuwen** knop.
* Wanneer u virtuele machines of fysieke machines tooa beveiligingsgroep toevoegt, Hallo processerver automatisch pushes en installeert deze Hallo Mobility-service op de bronserver Hallo als hello dit niet is gebeurd.
* Voor de automatische push-mechanisme Hallo toowork moet u hebt uw beveiligde machines ingesteld zoals beschreven in de vorige stap Hallo.

Machines als volgt toevoegen:

1. Klik op **beveiligde Items** > **beveiligingsgroep** > **Machines** > **Machines toevoegen**. Als een best practice wordt aangeraden dat beveiligingsgroepen uw werkbelastingen moeten worden gespiegeld zodat toevoegen van computers met een specifieke toepassing toohello dezelfde groep.
2. In **virtuele Machines selecteren** als u fysieke servers, op Hallo beveiligt **fysieke Machines toevoegen** wizard Hallo IP-adres en de beschrijvende naam opgeven. Selecteer vervolgens Hallo-besturingssystemen.

    ![V Center-server toevoegen](./media/site-recovery-vmware-to-azure-classic-legacy/physical-protect.png)
3. In **virtuele Machines selecteren** als u virtuele VMware-machines beveiligt, selecteert u een vCenter-server die wordt beheerd door uw virtuele machines (of Hallo EXSi host waarop ze uitvoert), en selecteer vervolgens Hallo-machines.

    ![V Center-server toevoegen](./media/site-recovery-vmware-to-azure-classic-legacy/select-vms.png)    
4. In **Doelresources opgeven** selecteert Hallo hoofddoelservers en opslag toouse voor replicatie en selecteert u of het Hallo-instellingen moeten worden gebruikt voor alle werkbelastingen. Selecteer [Premium-Opslagaccount](../storage/common/storage-premium-storage.md) tijdens het configureren van beveiliging voor werkbelastingen waarvoor consistent hoge i/o-prestaties en lage latentie in volgorde toohost i/o-intensieve werkbelastingen. Als u wilt dat toouse een Premium Storage-account voor uw werkbelastingschijven, moet u toouse Hallo hoofddoel van DS-serie. U kunt geen hoofddoel van DS reeks Premium-opslag-schijven gebruiken.

   > [!NOTE]
   > We bieden geen ondersteuning voor Hallo verplaatsing van Storage-accounts die zijn gemaakt met behulp van Hallo [nieuwe Azure portal](../storage/common/storage-create-storage-account.md) over resourcegroepen.
   >
   >

    ![vCenter-server](./media/site-recovery-vmware-to-azure-classic-legacy/machine-resources.png)
5. In **Accounts opgeven** gewenste toouse voor het installeren van de Mobility-service Hallo op beveiligde machines Hallo-account selecteren. Hallo-accountreferenties zijn nodig voor automatische installatie van Hallo Mobility-service. Als u een account Zorg ervoor dat geen selecteren instellen u een zoals beschreven in stap 2. Houd er rekening mee dat dit account kan niet worden geopend door Azure. Voor Windows hebben server Hallo account administrator-bevoegdheden op de bronserver Hallo. Voor Linux moet Hallo account hoofdmap.

    ![Linux-referenties](./media/site-recovery-vmware-to-azure-classic-legacy/mobility-account.png)
6. Klik op Hallo vinkje toofinish machines toohello beveiliging groep en toostart initiële replicatie voor elke computer toe te voegen. U kunt de status op Hallo bewaken **taken** pagina.

    ![V Center-server toevoegen](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs2.png)
7. U kunt bovendien protection-status controleren door te klikken op **beveiligde Items** > de naam van beveiligingsgroep > **virtuele Machines** . Nadat de initiële replicatie is voltooid en Hallo machines synchroniseren van gegevens worden ze weergegeven **beveiligde** status.

    ![Taken van de virtuele machine](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs.png)

### <a name="set-protected-machine-properties"></a>Eigenschappen van de machine set beveiligd
1. Nadat een machine heeft een **beveiligde** status kunt u de failover-eigenschappen configureren. In de details van groep Hallo selecteren computer en open Hallo Hallo **configureren** tabblad.
2. Hallo-naam die wordt gegeven toohello machine in Azure na failover en Hallo grootte van virtuele machine van Azure, kunt u wijzigen. U kunt ook selecteren hello Azure-netwerk toowhich Hallo machine na een failover verbonden.

   > [!NOTE]
   > [Migratie van netwerken](../resource-group-move-resources.md) via resource groepen binnen hetzelfde abonnement Hallo of voor abonnementen wordt niet ondersteund voor netwerken gebruikt voor de implementatie van Site Recovery.
   >
   >

    ![Eigenschappen van de virtuele machine instellen](./media/site-recovery-vmware-to-azure-classic-legacy/vm-props.png)

Opmerking:

* Hallo-naam van hello Azure-machine moet voldoen aan de Azure-vereisten.
* Standaard zijn gerepliceerde virtuele machines in Azure niet verbonden tooan Azure-netwerk. Als u wilt dat de gerepliceerde virtuele machines toocommunicate zorg hello tooset dezelfde Azure-netwerk voor deze.
* Als u de grootte van een volume op een virtuele VMware-machine of fysieke server gaat in een kritieke status. Als u toomodify Hallo grootte hoeft, Hallo te volgen:

  * a) wijzigen Hallo-instelling.
  * b) in Hallo **virtuele Machines** tabblad, selecteer Hallo virtuele machine en klik op **verwijderen**.
  * c) in **virtuele Machine verwijderen** Hallo optie **Schakel de beveiliging (gebruiken voor herstelanalyse en volume vergroten of verkleinen)**. Deze optie schakelt beveiliging maar handhaaft herstelpunten Hallo in Azure.

      ![Eigenschappen van de virtuele machine instellen](./media/site-recovery-vmware-to-azure-classic-legacy/remove-vm.png)
  * d) opnieuw inschakelen van beveiliging voor Hallo virtuele machine. Wanneer het inschakelen van beveiliging Hallo gegevens voor Hallo aangepast volume worden overgedragen tooAzure.

## <a name="step-10-run-a-failover"></a>Stap 10: Een failover uitvoeren
Momenteel kunt u alleen niet-geplande failovers voor beveiligde virtuele VMware-machines en fysieke servers uitvoeren. Let op Hallo volgende:

* Voordat u een failover start, zorg ervoor dat Hallo configuratie en master doelservers actief is en goed. Anders mislukt failover.
* Bronmachines zijn niet afgesloten als onderdeel van een niet-geplande failover. Een niet-geplande failover uitvoeren stopt gegevensreplicatie voor Hallo beveiligde servers. U moet beschikken over toodelete Hallo machines uit de beveiligingsgroep Hallo en deze opnieuw toevoegen in de volgorde toostart machines opnieuw beveiligen nadat hello niet-geplande failover is voltooid.
* Als u toofail wilt via zonder verlies van gegevens, zorg er dan voor dat Hallo primaire site virtuele machines zijn uitgeschakeld voordat u Hallo-failover start.

1. Op Hallo **herstelplannen** pagina en het toevoegen van een herstelplan. Geef details op voor het Hallo-abonnement en selecteer **Azure** als Hallo doel.

    ![Plan voor herstel configureren](./media/site-recovery-vmware-to-azure-classic-legacy/rplan1.png)
2. In **virtuele Machine selecteren** selecteert u een beveiligingsgroep en selecteer vervolgens machines in Hallo groep tooadd toohello-herstelplan. [Lees meer](site-recovery-create-recovery-plans.md) over plannen voor herstel.

    ![Virtuele machines toevoegen](./media/site-recovery-vmware-to-azure-classic-legacy/rplan2.png)
3. Indien nodig kunt u aanpassen Hallo plan toocreate groepen en Hallo volgorde welke computers bij het herstellen van Hallo plan worden de failover. U kunt ook wordt u gevraagd om de handmatige acties en scripts toevoegen. Hallo van scripts bij het herstellen van tooAzure kan worden toegevoegd met behulp van [Azure Automation-Runbooks](site-recovery-runbook-automation.md).
4. In Hallo **herstelplannen** Selecteer Hallo-plan en klik op pagina **niet-geplande Failover**.
5. In **bevestigen Failover** hello failoverrichting (tooAzure) controleren en Hallo herstel punt toofail via te selecteren.
6. Wacht tot Hallo failover-taak toocomplete en controleer vervolgens of failover Hallo werkte zoals verwacht en die Hallo begin van de virtuele machines in Azure is gerepliceerd.

## <a name="step-11-fail-back-failed-over-machines-from-azure"></a>Stap 11: Mislukken terug failover machines van Azure
[Meer informatie](site-recovery-failback-azure-to-vmware-classic-legacy.md) over het toobring uw mislukte via machines worden uitgevoerd in Azure terug tooyour on-premises omgeving.

## <a name="manage-your-process-servers"></a>De processervers beheren
Hallo processerver replicatie gegevens toohello hoofddoelserver verzendt in Azure, en nieuwe VMware virtuele machines toegevoegd tooa vCenter-server detecteert. In de volgende omstandigheden Hallo kunt u toochange Hallo processerver in uw implementatie:

* Als de huidige processerver Hallo uitvalt
* Als uw herstelpunt stijgingen objective (RPO) tooan onaanvaardbaar voor uw organisatie.

Indien nodig dat kunt u replicatie Hallo van sommige of alle van uw lokale VMware-virtuele verwerken machines en fysieke servers tooa verschillende server. Bijvoorbeeld:

* **Fout**— als een processerver is mislukt of is niet beschikbaar kunt u de beveiligde machine replicatie tooanother processerver verplaatsen. Metagegevens van de bronmachine hello en replica-machine worden verplaatst toohello nieuwe processerver en de gegevens opnieuw wordt gesynchroniseerd. nieuwe processerver Hello wordt automatisch verbinding toohello vCenter server tooperform automatische detectie. U kunt Hallo status van de processervers op Hallo Site Recovery dashboard bewaken.
* **Taakverdeling tooadjust RPO**, voor betere taakverdeling u kunt een andere processerver in Hallo Site Recovery-portal selecteert en verplaatst u de replicatie van een of meer machines tooit handmatige load balancing. In dit geval is de metagegevens van de geselecteerde bronsite Hallo en replica-machines verplaatste toohello nieuwe processerver. de oorspronkelijke processerver Hallo blijft verbonden toohello vCenter-server.

### <a name="monitor-hello-process-server"></a>Monitor Hallo processerver
Als een processerver een kritieke status een waarschuwing de status wordt weergegeven op Hallo Site Recovery-Dashboard is. U kunt op op Hallo status tooopen Hallo gebeurtenissen tabblad en inzoomen toospecific taken op tabblad Hallo-taken.

### <a name="modify-hello-process-server-used-for-replication"></a>Hallo processerver gebruikt voor replicatie wijzigen
1. Open **Servers** > **configuratieservers** > configuratieserver > **Serverdetails**.
2. Klik op **processervers** > **processerver wijzigen** volgende gewenste toomodify toohello-server.

    ![Processerver wijzigen 1](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps1.png)
3. In **processerver wijzigen** > **proces doelserver** Selecteer Hallo nieuwe server die u wilt toouse en selecteer vervolgens Hallo virtuele machines dat u wilt dat tooreplicate toohello nieuwe server. Klik op Hallo informatie pictogram volgende toohello servernaam voor meer informatie over de vrije ruimte en gebruikt geheugen. gemiddelde ruimte Hallo die worden vereist tooreplicate elke geselecteerde virtuele machine toohello nieuwe processerver wordt weergegeven toohelp u besluiten laden.

    ![Processerver wijzigen 2](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps2.png)
4. Klik op Hallo vinkje toobegin toohello nieuwe processerver repliceren. Opmerking: als u alle virtuele machines verwijdert uit een process-server is een kritieke het een kritieke waarschuwing niet meer in het Hallo-dashboard weergegeven moet.

## <a name="third-party-software-notices-and-information"></a>Software van derden kennisgevingen en informatie
Niet vertalen of Localize

Hallo-software en -firmware uitgevoerd in de Microsoft-product Hallo of de service is gebaseerd op of opgenomen met het materiaal van Hallo projecten onderstaande (gezamenlijk 'Code van derden').  Microsoft hello is geen oorspronkelijke auteur Hallo Code van derden.  de oorspronkelijke copyrightgegevens Hallo en licentie, waaronder Microsoft deze Code van derden ontvangen worden die hieronder ingesteld.

Hallo-informatie in de sectie A is met betrekking tot de Code van derden onderdelen van Hallo projecten hieronder vermeld. Deze licenties en informatie vindt u dient alleen ter informatie.  Deze Code van derden wordt relicensed tooyou door Microsoft onder de licentievoorwaarden voor Microsoft-product Hallo of -service van Microsoft-software.  

Hallo-informatie in de sectie B is met betrekking tot de Code van derden-onderdelen die worden aangebracht beschikbaar tooyou door Microsoft onder Hallo oorspronkelijke licentievoorwaarden.

Hallo volledige bestand kan worden gevonden op Hallo [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft behoudt alle rechten die in deze overeenkomst niet uitdrukkelijk zijn verleend, hetzij bij implicatie volgens of anderszins.
