---
title: aaaReplicate virtuele VMware-machines en fysieke servers tooAzure in de klassieke portal Hallo | Microsoft Docs
description: Dit artikel wordt beschreven hoe toodeploy Azure Site Recovery tooorchestrate replicatie, failovers en herstel van on-premises virtuele VMware-machines en fysieke servers tooAzure van Windows of Linux.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a9022c1f-43c1-4d38-841f-52540025fb46
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-vmware-to-azure
ms.openlocfilehash: f85e4139ad45552ce963072e14d71d279bb7dac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery"></a>Virtuele VMware-machines en fysieke servers tooAzure met Azure Site Recovery repliceren
> [!div class="op_single_selector"]
> * [Hello Azure-portal](site-recovery-vmware-to-azure.md)
> * [Hallo klassieke portal](site-recovery-vmware-to-azure-classic.md)
> * [Hallo klassieke portal (verouderd)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

Hello Azure Site Recovery-service draagt bij aan tooyour zakelijke continuïteit en noodherstelplan (BCDR) door te organiseren replicatie, failovers en herstel van virtuele machines en fysieke servers. Machines kunnen gerepliceerde tooAzure of tooa secundaire on-premises datacenter zijn. Zie voor een snel overzicht [wat is Azure Site Recovery?](site-recovery-overview.md).

## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven hoe:

* **TooAzure voor VMware-virtuele machines repliceren**: Site Recovery implementeert toocoordinate replicatie, failovers en herstel van tooAzure opslag voor lokale VMware virtuele machines.
* **Replicatie van fysieke servers tooAzure**: Azure Site Recovery implementeert toocoordinate replicatie, failovers en herstel van lokale fysieke Windows- en Linux-servers tooAzure.

> [!NOTE]
> Dit artikel wordt beschreven hoe tooreplicate tooAzure. Als u tooreplicate VMware-machines of Windows of Linux fysieke servers tooa secundair datacenter wilt, Zie [Site Recovery VMware tooVMware](site-recovery-vmware-to-vmware.md).
>
>

Eventuele opmerkingen of vragen plaatsen op Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="enhanced-deployment"></a>Verbeterde architectuur
In dit artikel bevat instructies voor de implementatie van een verbeterde in Hallo klassieke Azure-portal. Het is raadzaam om gebruik te maken van deze versie voor alle nieuwe implementaties. Als u al hebt geïmplementeerd door met behulp van Hallo eerdere verouderde versie, is het raadzaam dat u de nieuwe versie toohello migreren. Zie voor meer informatie over de migratie [Site Recovery VMware tooAzure klassieke verouderde](site-recovery-vmware-to-azure-classic-legacy.md#migrate-to-the-enhanced-deployment).

Hallo uitgebreide implementatie is een belangrijke update. Hier volgt een samenvatting van Hallo verbeteringen die we hebben aangebracht:

* **Er is geen virtuele machines in Azure-infrastructuur**: gegevens repliceert rechtstreeks tooan Azure storage-account. Er is bovendien geen tooset nodig om een infrastructuur VMs (zoals configuratieserver of de hoofddoelserver) voor replicatie en failover desgewenst in oudere Hallo-implementatie.  
* **Installatie van Unified**: één installatie biedt eenvoudige instellingen en schaalbaarheid voor on-premises onderdelen.
* **Beveiligde implementatie**: alle verkeer, worden versleuteld en replicatie-management-berichten worden verzonden via HTTPS 443.
* **Herstelpunten**: ondersteuning voor crashes en toepassingsconsistent herstelpunt punten voor Windows en Linux-omgevingen en ondersteuning voor beide één virtuele machine en multi-VM consistente configuraties.
* **Failover testen**: ondersteuning voor ononderbroken test failover tooAzure zonder de productie of onderbreken van replicatie.
* **Niet-geplande failover**: ondersteuning voor niet-geplande failover tooAzure met een uitgebreide optie tooautomatically virtuele machines afsluiten voordat de failover.
* **Failback**: geïntegreerde failback die alleen nog deltawijzigingen back toohello repliceert lokale site.
* **vSphere 6.0**: beperkte ondersteuning voor VMware vSphere 6.0 implementaties.

## <a name="how-does-site-recovery-help-protect-virtual-machines-and-physical-servers"></a>Hoe kan Site Recovery beter beveiligen van virtuele machines en fysieke servers?
* VMware-beheerders kunnen externe veiligheidsmaatregelen tooprotect Azure van zakelijke workloads en toepassingen die worden uitgevoerd op virtuele VMware-machines configureren. Managers voor de server kunnen tooAzure van fysieke on-premises Windows en Linux-servers worden gerepliceerd.
* Hallo Azure Site Recovery-console biedt één locatie voor eenvoudige installatie en beheer van replicatie, failover- en herstelproces.
* Als u virtuele VMware-machines die worden beheerd door een vCenter-server repliceert, kan Site Recovery de virtuele machines automatisch detecteren. Als machines op ESXi-host, detecteert Site Recovery virtuele machines op Hallo host.
* Als u eenvoudig failovers vanuit uw lokale infrastructuur tooAzure uitvoert, kunt u mislukken back-(herstel) van Azure tooVMware VM servers in Hallo on-premises-site.
* U kunt herstelplannen die een groep van toepassing werklast die zijn gelaagd over meerdere machines configureren. Als u niet over deze plannen, biedt Site Recovery consistentie tussen meerdere VM's, zodat computers waarop een Hallo dezelfde werkbelastingen kunnen worden hersteld samen tooa consistent gegevenspunt.

## <a name="supported-operating-systems"></a>Ondersteunde besturingssystemen
### <a name="windows-64-bit-only"></a>Windows (alleen 64 bits)
* Windows Server 2008 R2 SP1 +
* Windows Server 2012
* Windows Server 2012 R2

### <a name="linux-64-bit-only"></a>Linux (alleen 64 bits)
* Red Hat Enterprise Linux 6.7, 7.1 en 7.2
* CentOS 6.5, 6.6 6.7, 7.0, 7.1 en 7.2
* Oracle Enterprise Linux, 6.4 en 6.5 met beide Hallo Red Hat compatibel kernel of Unbreakable Enterprise Kernel versie 3 (UEK3)
* SUSE Linux Enterprise Server 11 SP3

## <a name="scenario-architecture"></a>Scenario-architectuur
Scenario-onderdelen:

* **Een on-premises management server**: Hallo beheerserver onderdelen van Site Recovery wordt uitgevoerd:
  * **Configuratieserver**: coördineert de communicatie en processen voor replicatie en herstel van gegevens beheert.
  * **Processerver**: fungeert als replicatiegateway. Deze gegevens worden ontvangen van beveiligde bronmachines; Deze optimaliseert met caching, compressie en codering; en stuurt replicatie tooAzure gegevensopslag. Ook push-installatie van Mobility-service tooprotected machines afgehandeld en wordt automatische detectie van virtuele VMware-machines uitgevoerd.
  * **Hoofddoelserver**: hier worden de replicatiegegevens tijdens de failback vanuit Azure afgehandeld.
    U kunt ook implementeren op een beheerserver die alleen als een proces server tooscale uw implementatie fungeert.
* **Hallo van de Mobility-service**: dit onderdeel wordt geïmplementeerd op elke machine (VM VMware of fysieke server) die u wilt dat tooreplicate tooAzure. Deze gegevens schrijfbewerkingen op Hallo machine vastgelegd en stuurt ze toohello processerver.
* **Azure**: U hoeft niet toocreate Azure VM's toohandle replicatie en failover. Hallo Site Recovery-service verwerkt gegevensbeheer en gegevens repliceert rechtstreeks tooAzure opslag. Gerepliceerde Azure VM's worden automatisch ingezette alleen wanneer tooAzure failover plaatsvindt. Echter, als u toofail door Azure toohello lokale site wilt, moet u tooset van een virtuele machine van Azure tooact als processerver.

Hallo afbeelding (gemaakt door Henry Robalino) na toont de wisselwerking tussen deze onderdelen:

![Componentarchitectuur](./media/site-recovery-vmware-to-azure/v2a-architecture-henry.png)

## <a name="capacity-planning"></a>Capaciteitsplanning
Wanneer u van plan bent capaciteit, is dit wat u moet toothink over:

* **Hallo bronomgeving**: plannen of Hallo VMware-infrastructuur en bron machine capaciteitsvereisten.
* **Hallo-beheerserver**: plannen voor Hallo on-premises beheerservers die onderdelen van Site Recovery uitvoeren.
* **Netwerkbandbreedte vanaf bron tootarget**: Planning voor netwerkbandbreedte nodig is voor replicatie tussen Hallo bron- en Azure.

### <a name="source-environment-considerations"></a>Bron omgeving overwegingen
* **Maximale dagelijkse wijzigingssnelheid**: een beveiligde machine slechts één processerver kunt gebruiken. Een enkel proces-server kan verwerken van too2 TB aan gegevens per dag wijzigen. 2 TB is dus Hallo maximale dagelijkse gegevens wijzigen die wordt ondersteund voor een beveiligde machine.
* **Maximale doorvoer**: een gerepliceerde machine kan deel uitmaken van tooone storage-account in Azure. Standard-opslagaccount kan maximaal 20.000 aanvragen per seconde worden verwerkt en we adviseren dat u Hallo aantal IOPS over een bron machine too20, 000. Bijvoorbeeld, als er een bronmachine met 5 schijven en elke schijf 120 IOPS (grootte van 8 KB) op de bron hello genereert, moeten binnen hello Azure per schijf-IOPS limiet van 500. aantal vereiste opslagaccounts voor Hallo totale bron IOPs/20, 000 =.

### <a name="management-server-considerations"></a>Overwegingen voor Management server
Hallo-beheerserver wordt uitgevoerd van onderdelen van Site Recovery dat optimalisatie van gegevens, replicatie en beheer verwerken. Deze moet kunnen toohandle Hallo dagelijkse wijziging snelheid capaciteit voor alle werkbelastingen op beveiligde machines uitgevoerd en er voldoende bandbreedte toocontinuously tooAzure gegevensopslag repliceren. Specifiek:

* Hallo processerver ontvangt replicatiegegevens van beveiligde machines en optimaliseert met caching, compressie en codering voordat u deze tooAzure verzendt. Hallo-beheerserver moet voldoende bronnen tooperform hebben deze taken.
* Hallo processerver schijfcache gebruikt. U wordt aangeraden een afzonderlijke cache schijf 600 GB of meer toohandle gegevenswijzigingen opgeslagen in het Hallo-gebeurtenis van knelpunt netwerk of een storing. Tijdens de implementatie, kunt u Hallo-cache configureren op een station met ten minste 5 GB aan opslagruimte, maar 600 GB Hallo minimale aanbeveling is.
* Als een best practice zich het beste die Hallo-beheerserver op Hallo hetzelfde netwerk en LAN-segment als Hallo machines gewenste tooprotect. Dit kan zich bevinden op een ander netwerk, maar de machines die u wilt dat tooprotect N3 netwerk zichtbaarheid tooit moet hebben.

Aanbevelingen voor de grootte voor de beheerserver Hallo worden samengevat in de volgende tabel Hallo:

| **CPU-beheerserver** | **Geheugen** | **Cachegrootte van de schijf** | **Snelheid van de gegevens wijzigen** | **Beveiligde machines** |
| --- | --- | --- | --- | --- |
| 8 vcpu's (2-sockets * @ 2,5 GHz-4 kernen) |16 GB |300 GB |500 GB of minder |Een beheerserver met deze instellingen tooreplicate minder dan 100 computers implementeren. |
| 12 vcpu's (2-sockets * @ 2,5 GHz-6 kernen) |18 GB |600 GB |500 GB too1 TB |Implementeer een beheerserver met deze instellingen tooreplicate 100 tot 150-machines. |
| 16 vcpu's (2-sockets * @ 2,5 GHz-8 kernen) |32 GB |1 TB |1 TB too2 TB |Implementeer een beheerserver met deze instellingen tooreplicate 150 tot 200-machines. |
| Een andere processerver implementeren | | |> 2 TB |Aanvullende processen servers implementeren als u meer dan 200 machines repliceert, of als Hallo dagelijkse gegevens wijzigen frequentie hoger is dan 2 TB. |

Waar:

* Elke bronmachine is geconfigureerd met 3 schijven van 100 GB.
* We gebruiken benchmarking opslag van 8 SAS-schijven van 10.000 RPM RAID 10 voor cache schijf metingen.

### <a name="network-bandwidth-from-source-tootarget"></a>Netwerkbandbreedte vanaf bron tootarget
Zorg ervoor dat u Hallo-bandbreedte die vereist voor de initiële replicatie en replicatie van verschillen zijn met behulp van Hallo berekenen [hulpprogramma capacity planner](site-recovery-capacity-planner.md).

#### <a name="throttling-bandwidth-used-for-replication"></a>Gebruikt voor replicatie van de bandbreedte beperken
VMware verkeer gerepliceerd tooAzure gaat via een specifiek proces-server. U kunt de Hallo-bandbreedte die beschikbaar is voor replicatie van Site Recovery op die server als volgt beperken:

1. Hallo Microsoft Azure Backup MMC-module op de belangrijkste beheerserver Hallo openen of op een beheerserver processervers uitgevoerd aanvullende ingericht. Standaard wordt een snelkoppeling naar Microsoft Azure Backup op Hallo bureaublad gemaakt. Of u kunt deze vinden in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Klik in het Hallo-module op **eigenschappen wijzigen**.

    ![De eigenschappen wijzigen bandbreedte beperken](./media/site-recovery-vmware-to-azure-classic/throttle1.png)
3. Op Hallo **bandbreedtebeperking** tabblad, Hallo-bandbreedte die kan worden gebruikt voor replicatie van Site Recovery en Hallo toepasselijke planning opgeven.

    ![Replicatie van de bandbreedte beperken](./media/site-recovery-vmware-to-azure-classic/throttle2.png)

U kunt ook instellen met behulp van PowerShell beperking. Hier volgt een voorbeeld:

    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth (512*1024) -NonWorkHourBandwidth (2048*1024)

#### <a name="maximizing-bandwidth-usage"></a>Bandbreedtegebruik optimaliseren
tooincrease hello bandbreedte door Azure Site Recovery voor replicatie gebruikt, moet u een registersleutel toochange.

Hallo Hallo volgende sleutel besturingselementen aantal threads per schijf repliceren die worden gebruikt bij het repliceren:

    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication\UploadThreadsPerVM

 In een overprovisioning netwerk moet deze registersleutel toobe gewijzigd van de standaardwaarden. Wij ondersteunen maximaal 32.  

Zie voor meer informatie over het plannen van capaciteit gedetailleerde [Site Recovery-Capaciteitsplanner](site-recovery-capacity-planner.md).

### <a name="additional-process-servers"></a>Aanvullende processen servers
Als u nodig hebt tooprotect is meer dan 200 machines of uw dagelijkse wijzigingssnelheid groter 2 TB, kunt u toevoegen extra servers toohandle Hallo laden. tooscale out, kunt u:

* Het aantal beheerservers Hallo verhogen. U kunt bijvoorbeeld beveiligen van too400 machines met twee beheerservers.
* Aanvullende processen servers toevoegen en gebruiken van deze toohandle verkeer in plaats van (of als aanvulling op) Hallo-beheerserver.

Deze tabel wordt een scenario waarin beschreven:

* U instellen Hallo oorspronkelijke management server toouse als een configuratieserver.
* U instellen een extra processerver.
* U configureren beveiligde virtuele machines toouse Hallo aanvullende processerver.
* Elke machine beveiligde bron is geconfigureerd met drie schijven van 100 GB.

| **Oorspronkelijke management server**<br/><br/>(configuratieserver) | **Aanvullende processerver** | **Cachegrootte van de schijf** | **Snelheid van de gegevens wijzigen** | **Beveiligde machines** |
| --- | --- | --- | --- | --- |
| 8 vcpu's (2-sockets * 4 kernen @ 2,5 GHz), 16 GB RAM-geheugen |4 vcpu's (2-sockets * 2 kernen @ 2,5 GHz), 8 GB RAM-geheugen |300 GB |250 GB of minder |U kunt 85 of minder machines repliceren. |
| 8 vcpu's (2-sockets * 4 kernen @ 2,5 GHz), 16 GB RAM-geheugen |8 vcpu's (2-sockets * 4 kernen @ 2,5 GHz), 12 GB RAM-geheugen |600 GB |250 GB too1 TB |U kunt 85 150-machines repliceren. |
| 12 vcpu's (2-sockets * 6 kernen @ 2,5 GHz), 18 GB RAM-geheugen |12 vcpu's (2-sockets * 6 kernen @ 2,5 GHz) 24 GB RAM-geheugen |1 TB |1 TB too2 TB |U kunt 150 225 machines repliceren. |

Hoe u de schaal van uw servers, is afhankelijk van uw voorkeur voor een model omhoog schalen of scale-out. U implementeert enkele geavanceerde management en processervers opschalen of uitbreiden door het implementeren van meerdere servers met minder bronnen. Bijvoorbeeld: als u tooprotect 220 machines nodig hebt, kunt u een van de volgende Hallo doen:

* Hallo oorspronkelijke management-server configureren met 12 vcpu's en 18 GB aan RAM-geheugen. Een extra processerver configureren met 12 vcpu's en 24 GB aan RAM-geheugen. Beveiligde machines toouse alleen Hallo aanvullende processen server configureren.
* Configureer twee beheerservers (2 x 8 Vcpu, 16 GB RAM-geheugen) en twee extra processervers (1 x 8 vcpu's en 4vCPUs x 1 toohandle 135 + 85 (220)-machines). Beveiligde machines toouse alleen Hallo proces extra servers te configureren.

Volg de instructies in Hallo [aanvullende processen servers implementeren](#deploy-additional-process-servers) tooset van een extra processerver.

## <a name="before-you-start-deployment"></a>Voordat u implementatie begint
Hallo volgende tabellen geven een overzicht Hallo-vereisten voor het implementeren van dit scenario.

### <a name="azure-prerequisites"></a>Vereisten voor Azure
| **Vereiste** | **Details** |
| --- | --- |
| **Azure-account** |U hebt een [Microsoft Azure](https://azure.microsoft.com/)-account nodig. U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/). Zie voor meer informatie over prijzen voor Site Recovery [siteherstel](https://azure.microsoft.com/pricing/details/site-recovery/). |
| **Azure Storage** |U moet een Azure storage-account toostore gerepliceerde gegevens. Gerepliceerde gegevens worden opgeslagen in Azure storage en Azure VM's worden ingezet wanneer failover plaatsvindt. <br/><br/>U hebt een [standaard geografisch redundant opslagaccount](../storage/storage-redundancy.md#geo-redundant-storage) nodig. Hallo-account moet zich in dezelfde regio bevinden als de Site Recovery-service Hallo Hallo en worden gekoppeld aan Hallo hetzelfde abonnement. Replicatie toopremium storage-accounts wordt momenteel niet ondersteund en mag niet worden gebruikt.<br/><br/>We bieden geen ondersteuning voor bewegende opslagaccounts die zijn gemaakt met behulp van Hallo [Azure-portal](../storage/storage-create-storage-account.md) over resourcegroepen. Zie voor meer informatie [tooMicrosoft inleiding Azure Storage](../storage/storage-introduction.md).<br/><br/> |
| **Azure-netwerk** |U moet een Azure-netwerk waarmee virtuele Azure-machines verbinding maken toowhen failover plaatsvindt. Hello Azure virtuele netwerk moet zich in Hallo dezelfde regio bevinden als Hallo Site Recovery-kluis.<br/><br/>toofail na de failover-tooAzure, moet u een VPN-verbinding (of Azure ExpressRoute) instellen uit hello Azure toohello lokale netwerksite. |

### <a name="on-premises-prerequisites"></a>Vereisten voor on-premises
| **Vereiste** | **Details** |
| --- | --- |
| **Beheerserver** |U moet een on-premises Windows 2012 R2-server uitgevoerd op een virtuele machine of fysieke server. Alle Hallo on-premises Site Recovery-onderdelen zijn geïnstalleerd op deze beheerserver.<br/><br/> U wordt aangeraden dat u Hallo-server als een maximaal beschikbare VMware VM implementeren. Failback toohello lokale site van Azure is altijd tooVMware VMs ongeacht of u failover van virtuele machines of fysieke servers. Als u geen Hallo-beheerserver als een VM VMware configureren, moet u tooset van een afzonderlijke hoofddoelserver als een VMware VM tooreceive failback-verkeer.<br/><br/>Hallo-server mag niet een domeincontroller zijn.<br/><br/>Hallo-server moet een statisch IP-adres hebben.<br/><br/>Hallo-hostnaam van Hallo-server moet 15 tekens of minder.<br/><br/>Hallo besturingssysteem landinstellingen moet alleen Engels zijn.<br/><br/>Hallo-beheerserver is internettoegang vereist.<br/><br/>Moet u uitgaand verkeer van Hallo-server als volgt: tijdelijke toegang op http-80 tijdens de installatie van onderdelen van de Site Recovery hello (toodownload MySQL); actieve uitgaande toegang via HTTPS 443 voor het replicatiebeheer van; actieve uitgaande toegang via HTTPS 9443 voor replicatieverkeer (deze poort kan worden aangepast).<br/><br/> Controleer of dat deze URL's zijn toegankelijk vanaf Hallo-beheerserver: <br/>- \*.hypervrecoverymanager.windowsazure.com<br/>- \*.accesscontrol.windows.net<br/>- \*.backup.windowsazure.com<br/>- \*.blob.core.windows.net<br/>- \*.store.core.windows.net<br/>-https://www.msftncsi.com/ncsi.txt<br/>- [https://dev.mysql.com/Get/Archives/MySQL-5.5/MySQL-5.5.37-Win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi")<br/><br/>Als u IP-adressen gebaseerde firewallregels op Hallo-server hebt, controleert u dat Hallo regels communicatie tooAzure toestaan. U moet tooallow hello [Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/details.aspx?id=41653) en Hallo HTTPS (443)-poort. U moet ook toowhitelist IP-adresbereiken voor hello Azure-regio van uw abonnement en voor VS-West. Hallo URL [https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi") is voor het downloaden van MySQL. |
| **VMware vCenter/ESXi-host** |U moet een of meer VMware vSphere ESX/ESXi-hypervisors beheren van uw virtuele machines van VMware, ESX/ESXi versie 6.0, 5.5 of 5.1 uitgevoerd met de meest recente updates Hallo.<br/><br/> Het is raadzaam dat u een VMware vCenter server toomanage ESXi-hosts implementeert. Worden moet gestart vCenter versie 6.0 of 5.5 met de nieuwste updates Hallo.<br/><br/>Houd er rekening mee dat de Site Recovery biedt geen ondersteuning voor nieuwe vCenter en vSphere 6.0 functies zoals cross vCenter vMotion, virtuele volumes en opslagruimten DRS. Site Recovery-ondersteuning is beperkt toofeatures die ook beschikbaar in versie 5.5 waren. |
| **Beveiligde machines** |**Azure**<br/><br/>Computers die u wilt dat tooprotect moet voldoen aan [vereisten voor Azure](site-recovery-prereq.md) voor het maken van virtuele Azure-machines.<br><br/>Als u tooconnect toohello virtuele Azure-machines na een failover wilt, moet u extern bureaublad-verbindingen op de lokale firewall Hallo tooenable.<br/><br/>Op beveiligde machines mag de capaciteit per schijf niet meer dan 1023 GB bedragen. Een virtuele machine kan hebben up too64-schijven (dus van too64 TB). Als u schijven groter dan 1 TB hebt, overweeg het gebruik van databasereplicatie zoals SQL Server Always On of Oracle Data Guard.<br/><br/>Minimaal 2 GB aan beschikbare ruimte op het Hallo-installatiestation voor de installatie van onderdelen.<br/><br/>Gastclusters met gedeelde schijven worden niet ondersteund. Als u een geclusterde implementatie hebt, overweeg het gebruik van databasereplicatie zoals SQL Server Always On of Oracle Data Guard.<br/><br/>Unified Extensible Firmware Interface (UEFI) / Extensible Firmware Interface(EFI) wordt niet ondersteund.<br/><br/>Namen voor machines moeten tussen 1 en maximaal 63 tekens bevatten (letters, cijfers en afbreekstreepjes) bevatten. Hallo-naam moet beginnen met een letter of cijfer en eindigen met een letter of cijfer. Nadat een machine is beveiligd, kunt u hello Azure naam wijzigen.<br/><br/>**Virtuele VMware-machines**<br/><br>U moet tooinstall VMware vSphere PowerCLI 6.0. op Hallo-beheerserver (configuratieserver).<br/><br/>VMware-machines gewenste tooprotect moet VMware tools geïnstalleerd en uitgevoerd.<br/><br/>Als de bron-Hallo VM heeft NIC-koppeling, wordt deze geconverteerd tooa enkel NIC na failover tooAzure.<br/><br/>Als beveiligde virtuele machines hebt een iSCSI-schijf, Site Recovery converteert Hallo VM iSCSI-schijf in een VHD-bestand beveiligd als Hallo VM failover tooAzure wordt uitgevoerd. Als iSCSI-doel kan worden bereikt door hello Azure VM, wordt verbinding tooiSCSI doel en wordt in feite twee schijven te zien: Hallo VHD schijf op Hallo Azure virtuele machine en Hallo bron iSCSI-schijf. In dit geval moet u toodisconnect Hallo iSCSI-doel dat wordt weergegeven op Hallo failover Azure VM.<br/><br/>Voor meer informatie over Hallo VMware gebruikersmachtigingen die Site Recovery moet, Zie [VMware toegangsmachtigingen vCenter](#vmware-permissions-for-vcenter-access).<br/><br/> **Windows Server-machines (op VMware VM of fysieke server)**<br/><br/>Hallo-server moet worden uitgevoerd op een ondersteund 64-bits besturingssysteem: Windows Server 2012 R2, Windows Server 2012 of Windows Server 2008 R2 met op minimaal SP1.<br/><br/>Hallo-besturingssysteem moet worden geïnstalleerd op station C en Hallo besturingssysteemschijf moet een standaardschijf van Windows. (Hallo OS mag niet worden geïnstalleerd op een Windows-dynamische schijf.)<br/><br/>Voor Windows Server 2008 R2-machines moet u toohave .NET Framework 3.5.1 geïnstalleerd.<br/><br/>U moet een administrator-account tooprovide (moet een lokale beheerder op de machine met Windows hello zijn) voor Hallo push-installatie Hallo Mobility-Service op Windows-servers. Als Hallo account is een account niet tot een domein opgegeven, moet u toodisable externe gebruiker toegangsbeheer op Hallo lokale machine. Zie voor meer informatie [Hallo mobility-service installeren met push-installatie](#install-the-mobility-service-with-push-installation).<br/><br/>Site Recovery biedt ondersteuning voor virtuele machines met een RDM-schijf. Tijdens de failback hergebruiken Site Recovery van Hallo RDM-schijf als Hallo oorspronkelijke bron-VM en RDM-schijf beschikbaar zijn. Als ze niet beschikbaar is, die tijdens de failback worden uitgevoerd, maakt Site Recovery een nieuw VMDK-bestand voor elke schijf.<br/><br/>**Linux-machines**<br/><br/>U moet een ondersteund 64-bits besturingssysteem: Red Hat Enterprise Linux 6.7; Centos 6.5, 6.6 of 6.7; Oracle Enterprise Linux, 6.4 of 6.5 met Hallo Red Hat compatibel kernel of Unbreakable Enterprise Kernel versie 3 (UEK3); SUSE Linux Enterprise Server 11 SP3.<br/><br/>/ etc/hosts bestanden op beveiligde machines moeten vermeldingen die zijn toegewezen Hallo lokale host naam tooIP adressen die zijn gekoppeld aan alle netwerkadapters bevatten. <br/><br/>Als u wilt dat tooconnect tooan Azure virtuele machine met Linux na een failover via een Secure Shell-client (ssh), zorg ervoor dat Hallo Secure Shell-service op de machine Hallo beveiligd toostart automatisch op opstarten van het systeem is ingesteld en dat firewall-regels toestaan een ssh verbinding tooit.<br/><br/>Beveiliging kan alleen worden ingeschakeld voor Linux-machines Hello opslag te volgen: File system (EXT3, ETX4, ReiserFS, XFS); Multipath-software-apparaat toewijzen (MPIO); Volume manager (LVM2). Fysieke servers met HP CCISS controller opslag worden niet ondersteund. Hallo ReiserFS bestandssysteem wordt alleen ondersteund op SUSE Linux Enterprise Server 11 SP3.<br/><br/>Site Recovery biedt ondersteuning voor virtuele machines met een RDM-schijf. Tijdens de failback voor Linux Site Recovery niet opnieuw gebruiken van Hallo RDM-schijf. In plaats daarvan wordt een nieuw VMDK-bestand voor elke overeenkomende RDM-schijf gemaakt. |

Alleen voor een Linux-VM: Zorg ervoor dat u Hallo disk.enableUUID=true in Hallo configuratieparameters Hallo virtuele machine in VMware instelt. Als deze rij niet bestaat, moet u deze toevoegen. Dit is vereiste tooprovide een consistente UUID toohello VMDK zodat deze correct koppelt. Zonder deze instelling wordt failback, wordt een volledige download als Hallo VM beschikbaar lokaal. Deze instelling toe te voegen, zorgt u ervoor dat alleen nog deltawijzigingen worden overgedragen tijdens de failback.

## <a name="step-1-create-a-vault"></a>Stap 1: Een kluis maken
1. Meld u aan toohello [Azure-portal](https://manage.windowsazure.com/).
2. Vouw **Data Services** > **Recovery Services** en klik op **Site Recovery-kluis**.
3. Klik op **Nieuw maken** > **Snelle invoer**.
4. In **naam**, voer een beschrijvende naam tooidentify Hallo-kluis.
5. In **regio**, selecteer de geografische regio voor de kluis Hallo Hallo. toocheck ondersteunde regio's, Zie [Azure Site Recovery prijsinformatie](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Klik op **Kluis maken**.
    ![Kluis maken](./media/site-recovery-vmware-to-azure-classic/quick-start-create-vault.png)

Selectievakje Hallo status balk tooconfirm die Hallo kluis is gemaakt. Hallo-kluis wordt weergegeven als **Active** op Hallo belangrijkste **Recovery Services** pagina.

## <a name="step-2-set-up-an-azure-network"></a>Stap 2: Een Azure-netwerk instellen
Een Azure-netwerk zo instellen dat virtuele Azure-machines na een failover verbonden tooa netwerk worden en zodat failback toohello lokale site werken kunt zoals verwacht.

1. Selecteer in de Azure-portal hello, **virtueel netwerk maken** en geef Hallo netwerknaam, IP-adresbereik en de subnetnaam van het.
2. Als u failback toodo nodig hebt, kunt u VPN-en ExpressRoute toohello netwerk toevoegen. VPN en ExpressRoute kunnen toohello netwerk zelfs na een failover worden toegevoegd.

Zie voor meer informatie over Azure-netwerken, [virtuele netwerken overzicht](../virtual-network/virtual-networks-overview.md).

> [!NOTE]
> [Migratie van netwerken](../azure-resource-manager/resource-group-move-resources.md) via resource groepen binnen hetzelfde abonnement Hallo of voor abonnementen wordt niet ondersteund voor netwerken gebruikt voor de implementatie van Site Recovery.
>
>

## <a name="step-3-install-hello-vmware-components"></a>Stap 3: Hallo VMware-onderdelen installeren
Als u tooreplicate virtuele VMware-machines wilt, volg deze stappen op Hallo-beheerserver:

1. [Download](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1) en VMware vSphere PowerCLI 6.0 installeren.
2. Hallo-server opnieuw opstarten.

## <a name="step-4-download-a-vault-registration-key"></a>Stap 4: Een kluisregistratiesleutel downloaden
1. Open in Hallo-beheerserver, Hallo Site Recovery-console in Azure. Op Hallo **Recovery Services** pagina, klikt u op Hallo kluis tooopen hello **Quick Start** pagina. U kunt ook openen Hallo **Quick Start** pagina op elk gewenst moment door te klikken op Hallo-pictogram.

    ![Pictogram Quick Start](./media/site-recovery-vmware-to-azure-classic/quick-start-icon.png)
2. Op Hallo **Quick Start** pagina, klikt u op **Doelresources voorbereiden** > **Download een registratiesleutel**. Hallo registratiebestand wordt automatisch gegenereerd. Het is geldig voor vijf dagen nadat deze gegenereerd.

## <a name="step-5-install-hello-management-server"></a>Stap 5: Hallo-beheerserver installeren
> [!TIP]
> Controleer of dat deze URL's zijn toegankelijk vanaf Hallo-beheerserver:
>
> * *.hypervrecoverymanager.windowsazure.com
> * *.accesscontrol.windows.net
> * *.backup.windowsazure.com
> * *.blob.core.windows.net
> * *.store.core.windows.net
> * https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi
> * https://www.msftncsi.com/ncsi.txt
>
>



>[!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Setup-Registration/player]



1. Op Hallo **Quick Start** pagina, Hallo unified installatie bestandsserver toohello downloaden.
2. Bestand Hallo-toostart installatie uitvoeren in Hallo **Unified installatie van Site Recovery** wizard.
3. In **voordat u begint met**, selecteer **installeren Hallo configuratieserver en de processerver**.

   ![Voordat u begint](./media/site-recovery-vmware-to-azure-classic/combined-wiz1.png)
4. In **van derden softwarelicentie**, klikt u op **ik ga akkoord** toodownload en installeer MySQL.

    ![Software van derden](./media/site-recovery-vmware-to-azure-classic/combined-wiz105.PNG)
5. In **registratie**, bladeren en selecteer Hallo registratiesleutel die u hebt gedownload van Hallo kluis.

    ![Registratie](./media/site-recovery-vmware-to-azure-classic/combined-wiz3.png)
6. In **internetinstellingen**, opgeven hoe Hallo-provider die wordt uitgevoerd op de configuratieserver Hallo tooAzure Site Recovery via Internet hello wordt verbinding.

   * Als u tooconnect met Hallo-proxy die momenteel ingesteld op de machine hello wilt, selecteer **verbinding maken met bestaande proxyinstellingen**.
   * Als u rechtstreeks Hallo provider tooconnect wilt, schakelt **rechtstreeks verbinden zonder een proxy**.
   * Als Hallo bestaande proxy verificatie is vereist als u een aangepaste proxy toouse voor Hallo providerverbinding wilt, schakelt u **verbinding maken met aangepaste proxyinstellingen**.
     * Als u een aangepaste proxy gebruikt, moet u toospecify Hallo adres, poort en referenties.
     * Als u een proxy gebruikt, moet u hebben al toegestaan Hallo volgende URL's:
       * *.hypervrecoverymanager.windowsazure.com    
       * *.accesscontrol.windows.net
       * *.backup.windowsazure.com
       * *.blob.core.windows.net
       * *.store.core.windows.net

    ![Firewall](./media/site-recovery-vmware-to-azure-classic/combined-wiz4.png)

1. In **controle van vereisten**, een selectievakje toomake zorgen dat Hallo installatie kunt uitvoeren door Setup wordt uitgevoerd.

    ![Vereisten](./media/site-recovery-vmware-to-azure-classic/combined-wiz5.png)

     Als er een waarschuwing wordt weergegeven over Hallo **globale tijd sync selectievakje**, controleren die tijd Hallo op Hallo systeemklok (**datum en tijd** instellingen) is dezelfde als de tijdzone Hallo Hallo.

     ![Synchronisatieprobleem in de tijd](./media/site-recovery-vmware-to-azure-classic/time-sync-issue.png)

1. In **MySQL configuratie**, maken de referenties voor het aanmelden toohello MySQL server-exemplaar dat wordt geïnstalleerd.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz6.png)
2. In **omgeving Details**Selecteer of u tooreplicate virtuele VMware-machines gaat. Als u bent, controleert het installatieprogramma dat PowerCLI 6.0 is geïnstalleerd.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz7.png)
3. In **installatielocatie**, selecteer waar u tooinstall Hallo binaire bestanden wilt en Hallo cache opslaan. U kunt een station met ten minste 5 GB aan beschikbare schijfruimte selecteren, maar we raden een cachestation met ten minste 600 GB beschikbare schijfruimte.

   ![Installatielocatie](./media/site-recovery-vmware-to-azure-classic/combined-wiz8.png)
4. In **netwerk selecteren**, Hallo listener (netwerkadapter en SSL-poort) op welke Hallo configuratieserver verzendt en ontvangt replicatiegegevens opgeven. Kunt u Hallo standaard poort (9443). Bij toevoeging toothis poort wordt poort 443 gebruikt door een webserver die replicatiebewerkingen ingedeeld. Gebruik geen 443 voor het ontvangen van replicatieverkeer.

    ![Netwerk selecteren](./media/site-recovery-vmware-to-azure-classic/combined-wiz9.png)



1. In **samenvatting**bekijkt hello informatie en op **installeren**. Wanneer de installatie is voltooid, wordt er een wachtwoordzin gegenereerd. U hebt deze nodig wanneer u replicatie inschakelt, dus kopieer deze en bewaar deze op een veilige locatie.

   ![Samenvatting](./media/site-recovery-vmware-to-azure-classic/combined-wiz10.png)


> [!WARNING]
> Hallo Microsoft Azure Recovery Service Agent-proxy moet worden ingesteld.
> Nadat het Hallo-installatie is voltooid, start u Hallo Microsoft Azure Recovery Services-Shell vanuit de menu Start van Windows hello. In opdrachtvenster Hallo dat wordt geopend, Hallo volgende reeks opdrachten tooset up Hallo proxyserverinstellingen worden uitgevoerd.
>
>
    $pwd = ConvertTo-SecureString -String ProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumb – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
>


### <a name="run-setup-from-hello-command-line"></a>Het installatieprogramma uitvoeren vanaf de opdrachtregel Hallo
U kunt ook Hallo unified wizard uitvoeren vanaf de opdrachtregel hello, als volgt:

    UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]

Waar:

* /ServerMode: Verplicht. Hiermee geeft u op of Hallo installatie Hallo-configuratie en het proces servers of Hallo processerver alleen (gebruikte tooinstall aanvullende processen servers installeren moet). Invoerwaarden: CS, PS.
* InstallDrive: verplicht. Hiermee geeft u Hallo map waarop Hallo-onderdelen zijn geïnstalleerd.
* / MySQLCredFilePath. Verplicht. Hiermee geeft u Hallo pad tooa bestand waar de referenties voor de MySQL Hallo worden opgeslagen. Hallo sjabloon toocreate Hallo bestand ophalen.
* / VaultCredFilePath. Verplicht. Locatie van het kluisreferentiebestand Hallo.
* /EnvType. Verplicht. Type installatie. Waarden: VMware, NonVMware.
* /PSIP en /CSIP. Verplicht. IP-adres van de processerver Hallo en de configuratieserver.
* /PassphraseFilePath. Verplicht. Locatie van Hallo wachtwoordzin bestand.
* / ByPassProxy. Optioneel. Hiermee geeft u een beheerserver Hallo die verbinding tooAzure zonder een proxy maakt.
* /ProxySettingsFilePath. Optioneel. Hiermee geeft u instellingen voor een aangepaste proxy (standaardproxy op Hallo-server die moet worden geverifieerd) of aangepaste proxy.

## <a name="step-6-set-up-credentials-for-hello-vcenter-server"></a>Stap 6: Referenties voor Hallo vCenter-server instellen
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Discovery/player]
>
>

Hallo processerver kan automatisch detecteren voor virtuele VMware-machines die worden beheerd door een vCenter-server. Voor automatische detectie moet Site Recovery een account en de referenties die toegang de Hallo vCenter server tot. Dit is niet relevant als u alleen fysieke servers repliceert.

tooset hello serviceaccount en referenties:

1. Hallo vCenter server, maakt u een rol (**Azure_Site_Recovery**) op Hallo vCenter niveau Hello [vereist machtigingen](#vmware-permissions-for-vcenter-access).
2. Hallo toewijzen **Azure_Site_Recovery** rol tooa vCenter gebruiker.

   > [!NOTE]
   > Een vCenter-gebruikersaccount dat de rol alleen-lezen Hallo is kunt failover uitvoeren zonder beveiligde bronmachines afgesloten. Als u tooshut omlaag deze machines wilt, moet u Hallo Azure_Site_Recovery rol. Als u alleen van virtuele machines van VMware tooAzure migreren bent en toofail terug hoeft niet, is de rol alleen-lezen Hallo voldoende.
   >
   >
3. tooadd Hallo-account openen **cspsconfigtool**. Het zich beschikbaar als een snelkoppeling op Hallo bureaublad en bevindt in Hallo [locatie installeren] \home\svsystems\bin map.
4. Op Hallo **Accounts beheren** tabblad **Account toevoegen**.

    ![Account toevoegen](./media/site-recovery-vmware-to-azure-classic/credentials1.png)
5. In **accountdetails**, referenties die gebruikt tooaccess worden kunnen Hallo vCenter-server toevoegen. Het kan meer dan 15 minuten duren voordat Hallo account naam tooappear in Hallo-portal. tooupdate onmiddellijk, klikt u op **vernieuwen** op Hallo **configuratieservers** tabblad.

    ![Details](./media/site-recovery-vmware-to-azure-classic/credentials2.png)

## <a name="step-7-add-vcenter-servers-and-esxi-hosts"></a>Stap 7: VCenter server- en ESXi-hosts toevoegen
Als u virtuele VMware-machines repliceert, moet u een vCenter-server tooadd (of ESXi-host).

1. Op Hallo **Servers** > **configuratieservers** tabblad **vCenter-server toevoegen**.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter1.png)
2. Hallo vCenter-server of details van ESXi-host, Hallo-naam van het Hallo-account die u hebt opgegeven tooaccess Hallo vCenter-server in de vorige stap Hallo en Hallo processerver die worden gebruikt toodiscover virtuele VMware-machines die worden beheerd door Hallo vCenter-server toevoegen. Hallo vCenter-server of ESXi-host moet zich bevinden in Hallo netwerk als het Hallo-server op welke Hallo process-server is geïnstalleerd.

   > [!NOTE]
   > Als u Hallo vCenter-server of ESXi-host met een account dat geen administrator-bevoegdheden op Hallo vCenter of host-server toevoegt, controleert u of Hallo vCenter of ESXi-accounts hebt deze bevoegdheden ingeschakeld: Datacenter, gegevensopslag, map, Jost, netwerk, Resource, virtuele Machine en vSphere gedistribueerde Switch. Hallo vCenter-server moet Hallo opslag weergaven bevoegdheid ingeschakeld.
   >
   >

    ![VCenter-server toevoegen](./media/site-recovery-vmware-to-azure-classic/add-vcenter2.png)
3. Nadat de detectie is voltooid, Hallo vCenter-server wordt aangeboden op Hallo **configuratieservers** tabblad.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter3.png)

## <a name="step-8-create-a-protection-group"></a>Stap 8: Maak een beveiligingsgroep
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Protection/player]
>
>

Beveiligingsgroepen zijn logische groeperingen van virtuele machines of fysieke servers dat u tooprotect met behulp van wilt dezelfde beveiligingsinstellingen Hallo. U beveiligingsgroep instellingen tooa beveiliging toepassen en deze instellingen zijn toegepast tooall machines (virtuele of fysieke) dat u toohello groep toevoegen.

1. Ga te**beveiligde Items** > **beveiligingsgroep** en klik op Hallo pictogram tooadd een beveiligingsgroep.

    ![Beveiligingsgroep maken](./media/site-recovery-vmware-to-azure-classic/protection-groups1.png)
2. Op Hallo **instellingen voor de beveiligingsgroep opgeven** pagina, Geef een naam voor het Hallo-groep. In Hallo **van** vervolgkeuzelijst, selecteer Hallo configuratieserver waarop u wilt dat toocreate Hallo groep. **Doel** is Microsoft Azure.

    ![Instellingen voor de beveiligingsgroep](./media/site-recovery-vmware-to-azure-classic/protection-groups2.png)
3. Op Hallo **replicatie-instellingen opgeven** pagina, Hallo replicatie-instellingen die worden gebruikt voor alle Hallo-machines in de groep Hallo configureren.

    ![Beveiliging groep Replicatie](./media/site-recovery-vmware-to-azure-classic/protection-groups3.png)

   * **Consistentie tussen Multi-VM's**: als u dit inschakelen op gedeelde toepassingsconsistente herstelpunten over Hallo-machines in de beveiligingsgroep Hallo maakt. Deze instelling is meest relevante bij het uitvoeren van alle machines in de beveiligingsgroep Hallo Hallo dezelfde werkbelasting. Alle machines herstelde toohello worden dezelfde gegevenspunt. Dit is beschikbaar of u repliceert VMware-machines of fysieke servers (Windows of Linux).
   * **Drempelwaarde voor RPO**: Sets Hallo RPO. Waarschuwingen worden gegenereerd wanneer continue gegevensreplicatie beveiliging Hallo Hallo geconfigureerd RPO drempelwaarde overschrijdt.
   * **Herstel bewaarperiode**: Hiermee geeft u de bewaarperiode Hallo. Beveiligde machines kunnen worden hersteld tooany punt binnen dit venster.
   * **Toepassingsconsistente momentopnamen frequentie**: geeft aan hoe vaak de herstelpunten die toepassingsconsistente momentopnamen bevatten worden gemaakt.

Wanneer u een vinkje Hallo selecteert, wordt een beveiligingsgroep is gemaakt met Hallo-naam die u hebt opgegeven. Bovendien een tweede beveiligingsgroep is gemaakt met de naam van de Hallo *beveiliging groepsnaam*- Failback. Deze beveiligingsgroep wordt gebruikt als u back-toohello lokale site na failover tooAzure mislukken. U kunt beveiligingsgroepen Hallo bewaken zoals ze worden gemaakt op Hallo **beveiligde Items** pagina.

## <a name="step-9-install-hello-mobility-service"></a>Stap 9: Hallo Mobility-service installeren
Hallo eerste stap bij het inschakelen van beveiliging voor virtuele machines en fysieke servers is tooinstall Hallo Mobility-service. U kunt dit op twee manieren doen:

* Automatisch push en Hallo service installeren op elke machine van de processerver Hallo. Wanneer u machines tooa beveiligingsgroep toevoegen en ze een juiste versie van de Mobility-service Hallo al uitvoert, zich push-installatie niet voor. U kunt ook automatisch Hallo service installeren met behulp van uw onderneming push-methode, zoals WSUS of System Center Configuration Manager. Zorg ervoor dat u hebt de beheerserver Hallo ingesteld voordat u dit doen.
* Hallo-service handmatig installeren op elke machine die u tooprotect wilt. Zorg ervoor dat u hebt de beheerserver Hallo ingesteld voordat u dit doen.

### <a name="install-hello-mobility-service-with-push-installation"></a>Hallo Mobility-service installeren met push-installatie
Wanneer u machines tooa beveiligingsgroep toevoegt, wordt de Hallo Mobility-service automatisch gepusht en geïnstalleerd op elke machine door Hallo processerver.

#### <a name="prepare-for-automatic-push-on-windows-machines"></a>Automatische push voorbereiden op Windows-computers
tooprepare Windows-machines zodanig dat de Mobility-service Hallo kunnen automatisch door Hallo processerver worden geïnstalleerd:

1. Maak een account dat processerver Hallo tooaccess Hallo machine kunt gebruiken. Hallo-account moet administratorbevoegdheden (lokaal of domeinbeheerder) hebben. Deze referenties worden alleen gebruikt voor push-installatie van Hallo Mobility-service.

   > [!NOTE]
   > Als u niet een domeinaccount gebruikt, moet u toodisable externe gebruiker toegangsbeheer op Hallo lokale machine. toodo, in het register onder HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System, Hallo Hallo DWORD-vermelding LocalAccountTokenFilterPolicy met een waarde van 1 toevoegen onder. tooadd hello registervermelding vanuit een CLI opdracht openen of met behulp van PowerShell, voer  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** .
   >
   >
2. Voor Windows Firewall op de gewenste tooprotect Hallo-machine, selecteert u **toestaan van een app of functie via Firewall**, en schakel **bestands- en printerdeling** en **Windows-beheer Instrumentation**. Voor de machines die deel uitmaken van tooa domein, kunt u Hallo firewall-beleid configureren met een groepsbeleidsobject.

   ![Firewallinstellingen](./media/site-recovery-vmware-to-azure-classic/mobility1.png)
3. Hallo-account dat u hebt gemaakt toevoegen:

   * Open **cspsconfigtool**. Het zich beschikbaar als een snelkoppeling op Hallo bureaublad en bevindt in Hallo [locatie installeren] \home\svsystems\bin map.
   * Op Hallo **Accounts beheren** tabblad **Account toevoegen**.
   * Hallo-account dat u hebt gemaakt toevoegen. Nadat u Hallo account toevoegt, moet u tooprovide Hallo referenties wanneer u een machine tooa-beveiligingsgroep toevoegen.

#### <a name="prepare-for-automatic-push-on-linux-servers"></a>Automatische push voorbereiden op Linux-servers
1. Zorg ervoor dat u wilt dat tooprotect wordt ondersteund, zoals beschreven in de Hallo Linux machine [On-premises vereisten](#on-premises-prerequisites). Zorg ervoor dat er een netwerkverbinding is tussen Hallo machine gewenste tooprotect en Hallo beheerserver die de processerver hello wordt uitgevoerd.
2. Maak een account dat processerver Hallo tooaccess Hallo machine kunt gebruiken. Hallo-account moet een Hoofdgebruiker op de bronserver Linux Hallo. Deze referenties worden alleen gebruikt voor push-installatie van Hallo Mobility-service.

   * Open **cspsconfigtool**. Het zich beschikbaar als een snelkoppeling op Hallo bureaublad en bevindt in Hallo [locatie installeren] \home\svsystems\bin map.
   * Op Hallo **Accounts beheren** tabblad **Account toevoegen**.
   * Hallo-account dat u hebt gemaakt toevoegen. Nadat u Hallo account toevoegt, moet u tooprovide Hallo referenties wanneer u een machine tooa-beveiligingsgroep toevoegen.
3. Controleer dat bestand Hallo/etc/hosts op de bron Hallo Linux-server bevat items die zijn toegewezen Hallo lokale hostnaam tooIP adressen die zijn gekoppeld aan alle netwerkadapters.
4. Hallo nieuwste openssh, openssh-server en openssl-pakketten installeren op de gewenste tooprotect Hallo-machine.
5. Zorg ervoor dat SSH ingeschakeld en worden uitgevoerd op poort 22.
6. SFTP subsysteem voor verificatie en wachtwoord in Hallo sshd_config bestand als volgt inschakelen:

   * Meld u aan als hoofdmap.
   * Zoek in Hallo /etc/ssh/sshd_config bestand Hallo-regel die met PasswordAuthentication begint.
   * Opmerking verwijderen Hallo regel en wijzig Hallo-waarde van **geen** te**Ja**.
   * Zoeken naar Hallo regel die met begint **subsysteem** en verwijder het commentaarteken Hallo regel.

     ![Linux standaardinstelling van geen subsystemen negeren](./media/site-recovery-vmware-to-azure-classic/mobility2.png)

### <a name="install-hello-mobility-service-manually"></a>Hallo Mobility-service handmatig installeren
Hallo-installatieprogramma's zijn beschikbaar in C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository.

| Bronbesturingssysteem | Installatiebestand van de Mobility-service |
| --- | --- |
| Windows Server (alleen 64-bits) |Microsoft-ASR_UA_9*.0.0_Windows_* release.exe |
| CentOS 6.4, 6.5, 6.6 (alleen 64-bits) |Microsoft-ASR_UA_9*.0.0_RHEL6-64_*release.tar.gz |
| SUSE Linux Enterprise Server 11 SP3 (alleen 64-bits) |Microsoft-ASR_UA_9*.0.0_SLES11-SP3-64_*release.tar.gz |
| Oracle Enterprise Linux 6.4, 6.5 (alleen 64-bits) |Microsoft-ASR_UA_9*.0.0_OL6-64_*release.tar.gz |

#### <a name="install-hello-mobility-service-manually-on-a-windows-server"></a>Hallo Mobility-service handmatig te installeren op een Windows-server
1. Downloaden en uitvoeren van de relevante Hallo-installatieprogramma.
2. Selecteer in **Voordat u begint** **Mobility-service**.

    ![De installatie van de Mobility-service](./media/site-recovery-vmware-to-azure-classic/mobility3.png)
3. In **Server configuratiedetails**, Hallo IP-adres van beheerserver Hallo opgeven en Hallo wachtwoordzin die is gegenereerd toen u Hallo management server-onderdelen geïnstalleerd. U kunt Hallo wachtwoordzin ophalen door het uitvoeren van  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** op Hallo-beheerserver.

    ![Mobility-service](./media/site-recovery-vmware-to-azure-classic/mobility6.png)
4. In **installatielocatie**, houdt de standaardlocatie Hallo en klikt u op **volgende** toobegin-installatie.
5. In **installatievoortgang**, Controleer de installatie en start Hallo computer desgevraagd opnieuw op.

U kunt ook installeren door te voeren Hallo na de tekst hello vanaf de opdrachtregel:

    UnifiedAgent.exe [/Role <Agent/MasterTarget>] [/InstallLocation <Installation Directory>] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>] [/LogFilePath <Log File Path>]

In de Hallo voorafgaand aan de opdracht:

* / Rol: verplicht. Hiermee geeft u op of Hallo Mobility-service moet worden geïnstalleerd.
* / InstallLocation: verplicht. Hiermee geeft u op waar tooinstall Hallo service.
* / PassphraseFilePath: verplicht. Hiermee geeft u Hallo configuratie server wachtwoordzin.
* / LogFilePath: verplicht. Hiermee geeft u Hallo setup logboekbestand.

#### <a name="uninstall-hello-mobility-service-manually"></a>Hallo Mobility-service handmatig verwijderen
U kunt de Mobility-service Hallo verwijderen met behulp van **een programma verwijderen of wijzigen** in het Configuratiescherm of via de opdrachtregel Hallo.

Hallo opdracht toouninstall Mobility-service via de opdrachtregel Hallo is:

    MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1}

#### <a name="change-hello-ip-address-of-hello-management-server"></a>Hallo IP-adres van beheerserver Hallo wijzigen
Nadat u Hallo-wizard uitvoert, kunt u Hallo IP-adres van beheerserver Hallo als volgt wijzigen:

1. Open Hallo bestand hostconfig.exe (te vinden op Hallo bureaublad).
2. Op Hallo **Global** en wijzig Hallo IP-adres van het Hallo-beheerserver.

   > [!NOTE]
   > Alleen Hallo IP-adres van beheerserver Hallo wijzigen. Hallo-poortnummer voor communicatie van de management-server moet poort 443, en **gebruik HTTPS** moet worden ingeschakeld blijft. Hallo wachtwoordzin niet wijzigen.
   >
   >

    ![IP-adres van Management server](./media/site-recovery-vmware-to-azure-classic/host-config.png)

#### <a name="install-hello-mobility-service-manually-on-a-linux-server"></a>Hallo Mobility-service handmatig te installeren op een Linux-server
1. Hallo juiste tar archief toohello Linux-machine die u wilt dat tooprotect kopiëren. Zie de tabel Hallo onder [handmatig installeren van de Mobility-service Hallo](#install-the-mobility-service-manually) toodetermine welke tar archiveert u moet gebruiken.
2. Open een shellprogramma en pak Hallo gecomprimeerde tar-archief tooa lokaal pad door te voeren:`tar -xvzf Microsoft-ASR_UA_8.5.0.0*`
3. Maak een bestand met de naam passphrase.txt in Hallo lokale directory toowhich u extraheerde Hallo van Hallo tar-archief. toodo, kopie Hallo wachtwoordzin van C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase op Hallo-beheerserver en sla in passphrase.txt door te voeren  *`echo <passphrase> >passphrase.txt`*  Hallo shell.
4. Hallo Mobility-service installeren door te voeren Hallo volgende opdracht:*`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`*
5. Hallo interne IP-adres van beheerserver Hallo opgeven en controleer of poort 443 is geselecteerd.

#### <a name="install-hello-mobility-service-from-hello-command-line"></a>Hallo Mobility-service installeren vanaf de opdrachtregel Hallo

Hallo wachtwoordzin van C:\Program Files (x86) \InMage Systems\private\connection op Hallo-beheerserver te kopiëren en opslaan als 'passphrase.txt' op Hallo-beheerserver. Voer Hallo opdrachten te volgen. In ons voorbeeld Hallo management server IP-adres is 104.40.75.37 en Hallo HTTPS-poort is 443:

tooinstall op een productieserver:

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt

tooinstall op de hoofddoelserver Hallo:

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt


## <a name="step-10-enable-protection-for-a-machine"></a>Stap 10: Beveiliging voor een machine inschakelen
tooenable beveiliging, virtuele machines en fysieke servers tooa beveiligingsgroep toevoegen. Voordat u begint, Let op Hallo volgende als u virtuele VMware-machines beveiligt:

* Virtuele VMware-machines om de 15 minuten worden gedetecteerd en deze mogelijk meer dan 15 minuten duren voordat ze tooappear in Site Recovery-portal Hallo na de detectie.
* Omgevingswijzigingen op Hallo virtuele machine (zoals VMware tools-installatie) mogelijk ook rekening houden met meer dan 15 minuten toobe bijgewerkt in Site Recovery.
* U kunt controleren tijd voor virtuele VMware-machines in Hallo Hallo laatste gedetecteerd **laatste Contact op** veld Hallo vCenter server/ESXi-host op Hallo **configuratieservers** tabblad.
* Als u een vCenter-Server of ESXi-host na het maken van een beveiligingsgroep toevoegt, duurt het mogelijk meer dan 15 minuten voor hello Azure Site Recovery-portal toorefresh en toobe van virtuele machines die worden vermeld in Hallo **Add machines tooa beveiligingsgroep**in het dialoogvenster.
* Als u tooproceed onmiddellijk wilt en machines tooa beveiligingsgroep toevoegen zonder te wachten Hallo geplande detectie, markeer de configuratieserver hello (Klik niet op deze) en klik op **vernieuwen**.

Daarnaast doet u het volgende:

* Het is raadzaam om uw beveiligingsgroepen te bouwen, zodat ze uw werkbelastingen. Bijvoorbeeld, voeg machines met een specifieke toepassing toohello dezelfde groep.
* Wanneer u machines tooa beveiligingsgroep toevoegt, wordt de processerver Hallo automatisch pushes en Hallo Mobility-service wordt geïnstalleerd als deze niet is geïnstalleerd. U hebt voorbereid, zoals beschreven in de vorige stap Hallo van toohave Hallo push-mechanisme nodig.

### <a name="add-machines-tooa-protection-group"></a>Machines tooa beveiligingsgroep toevoegen

1. Ga te**beveiligde Items** > **beveiligingsgroep** > **Machines** > **Machines toevoegen** .
2. Als u virtuele VMware-machines, beveiligt **virtuele Machines selecteren**, selecteert u een vCenter-server die wordt beheerd door uw virtuele machines (of Hallo EXSi host waarop ze uitvoert) en selecteer Hallo-machines.

    ![Schakel de beveiliging voor virtuele machines](./media/site-recovery-vmware-to-azure-classic/enable-protection2.png)
3. Als u fysieke servers beveiligt **virtuele Machines selecteren**Open Hallo **fysieke Machines toevoegen** wizard en geef Hallo IP-adres en de beschrijvende naam. Selecteer vervolgens Hallo-besturingssystemen.

   ![Schakel de beveiliging voor fysieke servers](./media/site-recovery-vmware-to-azure-classic/enable-protection1.png)
4. In **Doelresources opgeven**, selecteer Hallo storage-account dat u voor replicatie gebruikt en selecteer of Hallo instellingen moeten worden gebruikt voor alle werkbelastingen. Premium-opslagaccounts worden momenteel niet ondersteund.

   > [!NOTE]
   > We bieden geen ondersteuning voor bewegende opslagaccounts die zijn gemaakt met behulp van Hallo [Azure-portal](../storage/storage-create-storage-account.md) over resourcegroepen.                           
   > [Migratie van opslagaccounts](../azure-resource-manager/resource-group-move-resources.md) via resource groepen binnen hetzelfde abonnement Hallo of voor abonnementen wordt niet ondersteund voor storage-accounts gebruikt voor de implementatie van Site Recovery.
   >
   >

    ![Doelinstellingen configureren](./media/site-recovery-vmware-to-azure-classic/enable-protection3.png)
5. In **Accounts opgeven**, selecteer Hallo account dat u [instellen](#install-the-mobility-service-with-push-installation) toouse voor automatische installatie van Hallo Mobility-service.

    ![Accounts opgeven](./media/site-recovery-vmware-to-azure-classic/enable-protection4.png)
6. Klik op Hallo vinkje toofinish machines toohello beveiliging groep en toostart initiële replicatie voor elke computer toe te voegen.

   > [!NOTE]
   > Als u push-installatie is voorbereid, wordt Hallo Mobility-service wordt automatisch geïnstalleerd op computers die geen wanneer je deze toohello beveiligingsgroep toegevoegd. Nadat het Hallo-service is geïnstalleerd, wordt een beveiligingstaak wordt gestart en is mislukt. Na een storing hello moet u toomanually herstart elke computer waarop eerder Hallo Mobility-service is geïnstalleerd. Hallo beveiligingstaak opnieuw wordt gestart na opnieuw opstarten hello, en vindt initiële replicatie plaats.
   >
   >

U kunt de status op Hallo bewaken **taken** pagina.

![Status op Hallo taken pagina bewaken](./media/site-recovery-vmware-to-azure-classic/enable-protection5.png)

Beveiligingsstatus kan ook worden bewaakt in **beveiligde Items** > *naam beveiligingsgroep* > **virtuele Machines**. Nadat de eerste replicatie is voltooid en gegevens worden gesynchroniseerd, van de computer statuswijzigingen te**beveiligde**.

![Status van de monitor in beveiligde Items](./media/site-recovery-vmware-to-azure-classic/enable-protection6.png)

## <a name="step-11-set-protected-machine-properties"></a>Stap 11: Beveiligde computereigenschappen
1. Nadat een machine heeft een **beveiligde** status, kunt u de failover-eigenschappen configureren. In de details van groep Hallo, selecteer computer en open Hallo Hallo **configureren** tabblad.
2. Site Recovery automatisch wordt voorgesteld eigenschappen voor hello Azure VM en detecteert Hallo lokale netwerkinstellingen.

    ![Eigenschappen van de virtuele machine instellen](./media/site-recovery-vmware-to-azure-classic/vm-properties1.png)
3. U kunt deze instellingen wijzigen:

   * **Naam van de Azure VM**: dit is Hallo-naam die wordt gegeven toohello machine in Azure na een failover. Hallo-naam moet voldoen aan de Azure-vereisten.
   * **Azure VM-grootte**: Hallo aantal netwerkadapters wordt bepaald door de grootte Hallo dat u voor de virtuele doelmachine Hallo opgeeft. Zie voor meer informatie over grootten en adapters Hallo [tabellen grootte](../virtual-machines/linux/sizes.md). Opmerking:

     * Wanneer u Hallo grootte van een virtuele machine wijzigen en het Hallo-instellingen opslaan, het aantal netwerkadapters Hallo wordt gewijzigd wanneer u Hallo opent **configureren** tabblad Hallo volgende keer. minimum aantal netwerkadapters op de virtuele doelmachines Hallo is gelijk toohello minimum aantal netwerkadapters op een virtuele bronmachine. Hallo kunt u het maximale aantal netwerkadapters wordt bepaald door de grootte Hallo van Hallo virtuele machine.
       * Als het aantal netwerkadapters op de bronmachine Hallo Hallo kleiner is dan of gelijk aantal adapters toohello toegestaan voor Hallo-doelgrootte machine Hallo doel hetzelfde aantal adapters als bron Hallo Hallo.
       * Als het aantal adapters voor de virtuele bronmachine Hallo HALLO hallo dat is toegestaan voor de doelgrootte Hallo overschrijdt, wordt maximaal Hallo doel gebruikt.
        Als een bronmachine twee netwerkadapters heeft en de grootte van Hallo doelmachine vier ondersteunt, wordt Hallo doelmachine twee adapters hebben. Als Hallo-bronmachine twee adapters heeft, maar de doelgrootte Hallo ondersteund slechts één ondersteunt, wordt Hallo doelmachine slechts één adapter hebben.
     * Als Hallo virtuele machine meerdere netwerkadapters heeft, verbonden toohello op alle netwerkadapters moet dezelfde Azure-netwerk.
   * **Azure-netwerk**: U moet een Azure-netwerk dat de virtuele Azure-machines verbonden tooafter failover worden opgeven. Als u niet opgeeft, niet hello Azure Virtual machines tooany verbonden netwerk. Bovendien moet u een Azure-netwerk toospecify als u wilt dat toofailback van Azure toohello lokale site. Failback vereist een VPN-verbinding tussen een Azure-netwerk en een on-premises netwerk.
   * **Azure IP-adres/subnet**: Selecteer Hallo subnet toowhich hello Azure VM verbinding moet maken voor elke netwerkadapter. Houd er rekening mee dat als Hallo-netwerkadapter van de bronmachine Hallo geconfigureerde toouse een statisch IP-adres is, kunt u een statisch IP-adres voor hello Azure VM. Als u een statisch IP-adres niet opgeeft, wordt een beschikbaar IP-adres worden toegewezen. Als Hallo doel-IP-adres is opgegeven, maar al gebruikt door een andere virtuele machine in Azure wordt, mislukt de failover. Als Hallo-netwerkadapter van de bronmachine Hallo geconfigureerde toouse DHCP, hebt u DHCP als Hallo-instelling voor Azure.      

## <a name="step-12-create-a-recovery-plan-and-run-a-failover"></a>Stap 12: Een herstelplan maken en een failover uitvoeren
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failover/player]
>
>

U kunt een failover voor een enkele computer uitvoeren of kunt u meerdere virtuele machines die uitvoeren Hallo dezelfde taak of Voer Hallo failover dezelfde werkbelasting. toofail via meerdere machines op Hallo dezelfde tijd, u ze tooa herstelplan toevoegen.

een herstelplan toocreate:

1. Op Hallo **herstelplannen** pagina, klikt u op **herstelplan toevoegen** en toevoegen van een herstelplan. Geef details op voor het Hallo-abonnement en selecteer **Azure** als Hallo doel.

 ![Plan voor herstel configureren](./media/site-recovery-vmware-to-azure-classic/recovery-plan1.png)
2. In **virtuele Machine selecteren**, selecteert u een beveiligingsgroep en selecteer machines in Hallo groep tooadd toohello-herstelplan.

 ![Virtuele machines toevoegen](./media/site-recovery-vmware-to-azure-classic/recovery-plan2.png)

U kunt aanpassen Hallo plan toocreate groepen en Hallo volgorde op waarin computers in het herstelplan hello wordt een failover uitgevoerd. U kunt ook scripts en wordt u gevraagd om de handmatige acties toevoegen. Scripts kunnen worden gemaakt, handmatig of via [Azure Automation-Runbooks](site-recovery-runbook-automation.md). Zie voor meer informatie over het aanpassen van herstelplannen [herstelplannen maken](site-recovery-create-recovery-plans.md).

## <a name="run-a-failover"></a>Een failover uitvoeren
Voordat u een failover uitvoert:

* Zorg ervoor dat die Hallo-beheerserver wordt uitgevoerd en beschikbaar. Als dit niet het geval is, mislukt de failover.
* Als u een niet-geplande failover uitvoert:

  * Schakel primaire machines zo mogelijk uit voordat u een ongeplande failover uitvoert. Dit zorgt ervoor dat er geen beide Hallo-bron- en replica-machines uitgevoerd op Hallo hetzelfde moment. Als u virtuele VMware-machines repliceert wanneer u een niet-geplande failover uitvoert, kunt u opgeven dat Site Recovery tooshut omlaag Hallo bronmachines moet proberen. Afhankelijk van de status van de Hallo van Hallo primaire site, mogelijk of werkt mogelijk niet. Als u fysieke servers repliceert, kan Site Recovery niet met deze optie biedt.
  * Een niet-geplande failover stopt gerepliceerd van primaire machines, zodat eventuele verschillen gegevens won't worden overgedragen nadat een ongeplande failover is gestart.
  * Als u tooconnect toohello replica virtuele machine in Azure na een failover wilt, schakelt u verbinding met extern bureaublad op de bronmachine Hallo voordat u Hallo failover uitvoert. Vervolgens kunt u RDP-verbinding via Hallo firewall. U moet ook tooallow RDP op Hallo openbaar eindpunt Hallo Azure virtuele machine na een failover. Ga als volgt [aanbevolen procedures](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) tooensure die RDP na een failover werkt.

> [!NOTE]
> tooget hello beste prestaties als u een failover-tooAzure doet, zorg ervoor dat u hello Azure-Agent op Hallo beveiligde computer hebt geïnstalleerd. Dit vermindert het opstarten van de machine Hallo sneller en helpt bij het vaststellen van problemen. Hello Azure-Agent is beschikbaar voor [Linux](https://github.com/Azure/WALinuxAgent) en [Windows](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

### <a name="run-a-test-failover"></a>Een testfailover uitvoeren
Een test failover toosimulate uw failover uitvoert en herstelprocessen zijn in een geïsoleerd netwerk dat niet van invloed op uw productieomgeving en kunt normale replicatie normaal gaan. Testfailover initiatd op Hallo-bron is en kunt u deze in een aantal manieren uitvoeren:

* **Een Azure-netwerk niet opgeeft**: als u een testfailover zonder een netwerk uitvoert, Hallo test controleert dat de virtuele machines starten en goed worden weergegeven in Azure. Virtuele machines zijn niet verbonden tooan Azure-netwerk na een failover.
* **Geef een Azure-netwerk**: dit type failover controleert of de volledige replicatieomgeving hello wordt weergegeven zoals verwacht en netwerk dat Azure virtuele machines verbonden toohello zijn opgegeven.

een testfailover toorun:

1. Op Hallo **herstelplannen** pagina, selecteer Hallo-plan en klik op **Testfailover**.

 ![Hallo-abonnement selecteren](./media/site-recovery-vmware-to-azure-classic/test-failover1.png)
2. In **Testfailover bevestigen**, selecteer **geen** tooindicate dat u niet dat toouse een Azure-netwerk voor de testfailover Hallo wilt of selecteer Hallo toowhich Hallo Netwerktest VM's na een failover worden verbonden. Klik op Hallo vinkje toostart Hallo failover.

 ![Maak een keuze](./media/site-recovery-vmware-to-azure-classic/test-failover2.png)
3. Failover-voortgang controleren op Hallo **taken** tabblad.

 ![Voortgang van de monitor](./media/site-recovery-vmware-to-azure-classic/test-failover3.png)
4. Nadat de failover Hallo is voltooid, dient u zich kunt toosee Hallo replica machine van Azure worden weergegeven in **virtuele Machines** in hello Azure-portal. Als u een RDP-verbinding toohello Azure VM tooinitiate wilt, moet u tooopen poort 3389 op Hallo VM-eindpunt.
5. Nadat u hebt voltooid, wanneer failover bereikt Hallo **Complete** testfase, klikt u op **volledige Test** toofinish. In **notities**, vastleggen en opslaan van eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo.
6. Klik op **Hallo testfailover is voltooid** tooautomatically Hallo-testomgeving opruimen. Nadat dit is gebeurd, Hallo testfailover wordt weergegeven een **Complete** status. Alle elementen of virtuele machines automatisch gemaakt tijdens de testfailover Hallo worden verwijderd. Als u een testfailover langer dan twee weken duurt, wordt deze geforceerd toofinish.

### <a name="run-an-unplanned-failover"></a>Een niet-geplande failover uitvoeren
Niet-geplande failover van Azure wordt gestart en kan worden uitgevoerd, zelfs als de primaire site Hallo niet beschikbaar.

1. Op Hallo **herstelplannen** pagina, selecteer Hallo-plan en klik op **Failover** > **niet-geplande Failover**.

 ![Hallo-abonnement selecteren](./media/site-recovery-vmware-to-azure-classic/unplanned-failover1.png)
2. Als u virtuele VMware-machines repliceert, kunt u proberen tooshut omlaag lokale virtuele machines. Dit is een actie best-effort en failover blijft of Hallo inspanning of niet lukt. Als dit niet lukt, details van fouten wordt weergegeven op Hallo **taken** tabblad onder **niet-geplande Failover taken**.

 ![Optie voor lokale virtuele machines afsluiten](./media/site-recovery-vmware-to-azure-classic/unplanned-failover2.png)

 > [!NOTE]
 > Deze optie niet beschikbaar als u fysieke servers repliceert. U moet tootry tooshut die u handmatig indien mogelijk.
 >
 >

3. In **bevestigen Failover**, controleert u Hallo failoverrichting (tooAzure) en selecteer Hallo herstelpunt dat u toouse Hallo failover wenst. Als u meerdere VM ingeschakeld wanneer u replicatie-eigenschappen hebt geconfigureerd, kunt u toohello meest recente toepassing of crashconsistent herstelpunt herstellen. U kunt ook selecteren **aangepaste herstelpunt** toorecover tooan eerder tijdstip. Klik op Hallo vinkje toostart Hallo failover.

 ![Failoverrichting bevestigen](./media/site-recovery-vmware-to-azure-classic/unplanned-failover3.png)
4. Wachten op Hallo toofinish voor niet-geplande failover-taak. U kunt de voortgang van de failover op Hallo controleren **taken** tabblad. Zelfs als er fouten optreden tijdens de niet-geplande failover van herstelplan hello wordt uitgevoerd totdat deze voltooid is. Ook moet u kunnen toosee Hallo replica machine van Azure worden weergegeven in **virtuele Machines** in hello Azure-portal.

### <a name="connect-tooreplicated-azure-virtual-machines-after-failover"></a>Verbinding maken met tooreplicated Azure virtuele machines na een failover
tooconnect tooreplicated virtuele machines in Azure na een failover, moet u de:

- Een extern bureaublad-verbinding is ingeschakeld op de primaire machine Hallo.
- Windows Firewall op de primaire machine Hallo tooallow RDP ingesteld.
- RDP toohello openbaar eindpunt voor hello Azure virtuele machine toegevoegd.

Zie voor meer informatie over om in te stellen, [probleemoplossing van extern bureaublad-verbinding na een failover met ASR](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

## <a name="deploy-additional-process-servers"></a>Aanvullende processen servers implementeren
Als u uw implementatie dan 200 bronmachines moet uitbreiden of als de totale dagelijkse verloop groter is dan 2 TB, moet u extra proces servers toohandle Hallo-netwerkverkeer. tooset van een extra processerver selectievakje Hallo vereisten op [extra processervers](#additional-process-servers), en stel vervolgens Hallo processerver toohello volgens instructies te volgen. Nadat u Hallo-server hebt ingesteld, kunt u configureren bron machines toouse deze.

### <a name="set-up-an-additional-process-server"></a>Een extra processerver instellen
Een extra processerver instellen als volgt:

* Hallo unified wizard tooconfigure een beheerserver als een processerver uitvoeren.
* Als u wilt dat de gegevensreplicatie toomanage met behulp van alleen Hallo nieuwe processerver, moet u toomigrate uw beveiligde machines.

### <a name="install-hello-process-server"></a>Hallo processerver installeren
1. Op Hallo **Quick Start** pagina, download Hallo unified installatiebestand voor Hallo installatie van de Site Recovery-onderdelen. Voer de installatie.
2. In **voordat u begint met**, selecteer **toevoegen van extra proces servers tooscale uit implementatie**.

 ![Processerver toevoegen](./media/site-recovery-vmware-to-azure-classic/add-ps1.png)
3. Hallo-wizard hebt voltooid zoals u deed wanneer u [instellen](#step-5-install-the-management-server) Hallo eerste beheerserver.
4. In **Server configuratiedetails**, Voer Hallo IP-adres van Hallo oorspronkelijke management server waarop u de configuratieserver Hallo hebt geïnstalleerd en voer vervolgens Hallo wachtwoordzin. Als u geen Hallo wachtwoordzin, voert u  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** op Hallo oorspronkelijke management server tooretrieve deze.

 ![Configuratiedetails van server](./media/site-recovery-vmware-to-azure-classic/add-ps2.png)

### <a name="migrate-machines-toouse-hello-new-process-server"></a>Machines toouse Hallo nieuwe processerver migreren
1. Open **configuratieservers** > **Server** > *naam van het oorspronkelijke beheerserver Hallo*  >   **Serverdetails**.

 ![Details van server](./media/site-recovery-vmware-to-azure-classic/update-process-server1.png)
2. In Hallo **processervers** selecteert **processerver wijzigen** volgende toohello-server die u wilt dat toochange.

 ![Hallo processerver bijwerken](./media/site-recovery-vmware-to-azure-classic/update-process-server2.png)
3. Selecteer **processerver wijzigen**, selecteer **proces doelserver**, en vervolgens selecteert de nieuwe beheerserver Hallo. Vervolgens wordt selecteert Hallo virtuele machines die nieuwe processerver Hallo afgehandeld. Klik op Hallo informatie pictogram tooget informatie over het Hallo-server. Hallo gemiddelde ruimte die nodig is tooreplicate elke geselecteerde virtuele machine toohello nieuwe processerver wordt weergegeven toohelp u besluiten laden. Klik op Hallo vinkje toostart toohello nieuwe processerver repliceren.

 ![Hallo-processerver wijzigen](./media/site-recovery-vmware-to-azure-classic/update-process-server3.png)

## <a name="vmware-permissions-for-vcenter-access"></a>VMware-machtigingen voor de vCenter-toegang
Hallo processerver kan automatisch detecteren van virtuele machines op een vCenter-server. Automatische detectie van tooperform, moet u een rol (Azure_Site_Recovery) toodefine op Hallo vCenter niveau tooallow siteherstel tooaccess hello vCenter-server. Als u alleen toomigrate VMware-machines tooAzure nodig en niet toofailback van Azure hoeft, kunt u een alleen-lezen-rol die is voldoende definiëren. Hallo machtigingen ingesteld zoals beschreven [stap 6: instellen van referenties voor de vCenter-server Hallo](#step-6-set-up-credentials-for-the-vcenter-server). Hallo-rolmachtigingen worden samengevat in de volgende tabel Hallo:

| **Rol** | **Details** | **Machtigingen** |
| --- | --- | --- |
| Azure_Site_Recovery rol |Detectie van VMware VM |Deze rechten voor Hallo v Center-server toewijzen:<br/><br/>Gegevensopslag: Toewijzen van ruimte, bladeren gegevensopslag, bestandsbewerkingen op laag niveau, bestand, updatebestanden voor de virtuele machine verwijderen<br/><br/>Netwerk: Netwerk toewijzen<br/><br/>Bron: Tooresource groep van virtuele machines, migreren van stroom voorzien uitschakelen virtuele machine, migreren ingeschakeld op virtuele machine toewijzen<br/><br/>Taken: De taak, Update-taak maken<br/><br/>Virtuele machine > configuratie<br/><br/>Virtuele machine > Interact > beantwoorden van vraag, apparaatverbinding, configureer CD's, diskettes configureren, uitschakelen, inschakelen, VMware-hulpprogramma's installeren<br/><br/>Virtuele machine > voorraad > maken, registreren, Unregister<br/><br/>Virtuele machine > inrichten > downloaden van de virtuele machine toestaan, toestaan virtuele machine bestanden uploaden<br/><br/>Virtuele machine > momentopnamen > momentopnamen verwijderen |
| vCenter gebruikersrol |VMware VM detectie/Failover zonder afsluiten van de bron-VM |Deze rechten voor Hallo v Center-server toewijzen:<br/><br/>Data Center object > doorgeven tooChild Object, de functie = alleen-lezen <br/><br/>Hallo-gebruiker is toegewezen op Hallo datacenter niveau en dus toegang tooall Hallo objecten heeft in Hallo datacenter. Als u toorestrict Hallo toegang wilt, toewijzen Hallo **geen toegang** rol met Hallo **toochild doorgegeven** object toohello onderliggende objecten (ESX-hosts, datastores, VM's en -netwerken). |
| vCenter gebruikersrol |Failover en failback |Deze rechten voor Hallo v Center-server toewijzen:<br/><br/>Object voor Datacenter-doorgeven toochild object, de functie Azure_Site_Recovery =<br/><br/>Hallo-gebruiker is toegewezen op niveau van het datacenter en dus toegang tooall Hallo objecten heeft in Hallo datacenter.  Als u toorestrict Hallo toegang wilt, toewijzen Hallo ** geen toegang ** rol met Hallo **doorgeven toochild object** toohello onderliggend object (ESX-hosts, datastores, VM's en -netwerken). |

## <a name="third-party-software-notices-and-information"></a>Software van derden kennisgevingen en informatie
<!--Do Not Translate or Localize-->

Hallo-software en -firmware uitgevoerd in de Microsoft-product Hallo of de service is gebaseerd op of opgenomen met het materiaal van Hallo projecten onderstaande (gezamenlijk 'Code van derden').  Microsoft hello is geen oorspronkelijke auteur Hallo Code van derden.  de oorspronkelijke copyrightgegevens Hallo en licentie, waaronder Microsoft deze Code van derden ontvangen worden die hieronder ingesteld.

Hallo-informatie in de sectie A is met betrekking tot de Code van derden onderdelen van Hallo projecten hieronder vermeld. Deze licenties en informatie vindt u dient alleen ter informatie.  Deze Code van derden wordt relicensed tooyou door Microsoft onder de licentievoorwaarden voor Microsoft-product Hallo of -service van Microsoft-software.  

Hallo-informatie in de sectie B is met betrekking tot de Code van derden-onderdelen die worden aangebracht beschikbaar tooyou door Microsoft onder Hallo oorspronkelijke licentievoorwaarden.

Hallo volledige bestand kan worden gevonden op Hallo [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft behoudt alle rechten die in deze overeenkomst niet uitdrukkelijk zijn verleend, hetzij bij implicatie volgens of anderszins.

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over failback](site-recovery-failback-azure-to-vmware-classic.md) toobring uw failover-machines worden uitgevoerd in Azure back-tooyour on-premises omgeving.
