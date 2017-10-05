---
title: Virtuele VMware-machines en fysieke servers repliceren naar Azure in de klassieke portal | Microsoft Docs
description: Dit artikel wordt beschreven hoe u Azure Site Recovery implementeert om replicatie, failovers en herstel van on-premises VMware-virtuele machines en fysieke Windows of Linux-servers naar Azure te organiseren.
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
ms.openlocfilehash: 73c3fb5cf4056ddb9554f598ec7f173d81802f17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-to-azure-with-azure-site-recovery"></a>Virtuele VMware-machines en fysieke servers repliceren naar Azure met Azure Site Recovery
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmware-to-azure.md)
> * [De klassieke portal](site-recovery-vmware-to-azure-classic.md)
> * [De klassieke portal (verouderd)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

De Azure Site Recovery-service draagt bij aan uw strategie voor zakelijke continuïteit en noodherstel herstel (BCDR) door te organiseren replicatie, failovers en herstel van virtuele machines en fysieke servers. Machines kunnen worden gerepliceerd naar Azure of een secundaire on-premises Datacenter. Zie voor een snel overzicht [wat is Azure Site Recovery?](site-recovery-overview.md).

## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven hoe:

* **Virtuele VMware-machines repliceren naar Azure**: Site Recovery implementeert voor het coördineren van replicatie, failovers en herstel van on-premises VMware-virtuele machines naar Azure storage.
* **Fysieke servers repliceren naar Azure**: Azure Site Recovery implementeert voor het coördineren van replicatie, failovers en herstel van on-premises fysieke Windows en Linux-servers naar Azure.

> [!NOTE]
> In dit artikel wordt beschreven hoe repliceren naar Azure. Als u repliceren van VMware-machines of fysieke Windows of Linux-servers naar een secundair datacenter wilt, Zie [Site Recovery VMware naar VMware](site-recovery-vmware-to-vmware.md).
>
>

Eventuele opmerkingen of vragen plaatsen aan de onderkant van dit artikel of op de [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="enhanced-deployment"></a>Verbeterde architectuur
In dit artikel bevat instructies voor een uitgebreide implementatie in de klassieke Azure portal. Het is raadzaam om gebruik te maken van deze versie voor alle nieuwe implementaties. Als u hebt al geïmplementeerd met behulp van de eerdere verouderde versie, raden wij u aan te migreren naar de nieuwe versie. Zie voor meer informatie over de migratie [Site Recovery VMware naar Azure classic legacy](site-recovery-vmware-to-azure-classic-legacy.md#migrate-to-the-enhanced-deployment).

De verbeterde architectuur is een belangrijke update. Hier volgt een samenvatting van de verbeteringen die we hebben aangebracht:

* **Er is geen virtuele machines in Azure-infrastructuur**: gegevens rechtstreeks naar een Azure storage-account worden gerepliceerd. Er is bovendien niet nodig voor het instellen van een infrastructuur VMs (zoals configuratieserver of de hoofddoelserver) voor replicatie en failover desgewenst in de verouderde implementatie.  
* **Installatie van Unified**: één installatie biedt eenvoudige instellingen en schaalbaarheid voor on-premises onderdelen.
* **Beveiligde implementatie**: alle verkeer, worden versleuteld en replicatie-management-berichten worden verzonden via HTTPS 443.
* **Herstelpunten**: ondersteuning voor crashes en toepassingsconsistent herstelpunt punten voor Windows en Linux-omgevingen en ondersteuning voor beide één virtuele machine en multi-VM consistente configuraties.
* **Failover testen**: ondersteuning voor ononderbroken testfailover naar Azure zonder de productie of onderbreken van replicatie.
* **Niet-geplande failover**: ondersteuning voor niet-geplande failover naar Azure met een verbeterde optie voor virtuele machines automatisch afgesloten voordat failover wordt uitgevoerd.
* **Failback**: geïntegreerde failback die alleen nog deltawijzigingen gerepliceerd terug naar de lokale site.
* **vSphere 6.0**: beperkte ondersteuning voor VMware vSphere 6.0 implementaties.

## <a name="how-does-site-recovery-help-protect-virtual-machines-and-physical-servers"></a>Hoe kan Site Recovery beter beveiligen van virtuele machines en fysieke servers?
* VMware-beheerders kunnen externe beveiligingen om Azure beveiligen van zakelijke workloads en toepassingen die worden uitgevoerd op virtuele VMware-machines configureren. Managers voor de server kunnen fysieke on-premises Windows en Linux-servers repliceren naar Azure.
* De Azure Site Recovery-console biedt één locatie voor eenvoudige installatie en beheer van replicatie, failover- en herstelproces.
* Als u virtuele VMware-machines die worden beheerd door een vCenter-server repliceert, kan Site Recovery de virtuele machines automatisch detecteren. Als machines op ESXi-host, detecteert Site Recovery virtuele machines op de host.
* Als u eenvoudig failovers vanuit uw on-premises infrastructuur naar Azure uitvoert, kunt u mislukken back-(herstel) van Azure naar VMware VM-servers van de lokale site.
* U kunt herstelplannen die een groep van toepassing werklast die zijn gelaagd over meerdere machines configureren. Als u niet over deze plannen, biedt Site Recovery consistentie tussen meerdere VM's, zodat de machines die de dezelfde werkbelasting samen kunnen worden hersteld naar een consistente gegevenspunt.

## <a name="supported-operating-systems"></a>Ondersteunde besturingssystemen
### <a name="windows-64-bit-only"></a>Windows (alleen 64 bits)
* Windows Server 2008 R2 SP1 +
* Windows Server 2012
* Windows Server 2012 R2

### <a name="linux-64-bit-only"></a>Linux (alleen 64 bits)
* Red Hat Enterprise Linux 6.7, 7.1 en 7.2
* CentOS 6.5, 6.6 6.7, 7.0, 7.1 en 7.2
* Oracle Enterprise Linux, 6.4 en 6.5 met Red Hat compatibel kernel of Unbreakable Enterprise Kernel versie 3 (UEK3)
* SUSE Linux Enterprise Server 11 SP3

## <a name="scenario-architecture"></a>Scenario-architectuur
Scenario-onderdelen:

* **Een on-premises management server**: de beheerserver onderdelen van Site Recovery wordt uitgevoerd:
  * **Configuratieserver**: coördineert de communicatie en processen voor replicatie en herstel van gegevens beheert.
  * **Processerver**: fungeert als replicatiegateway. Deze gegevens worden ontvangen van beveiligde bronmachines; Deze optimaliseert met caching, compressie en codering; en gegevens van replicatie verzendt naar Azure-opslag. Ook push-installatie van Mobility-service naar beveiligde computers afgehandeld en wordt automatische detectie van virtuele VMware-machines uitgevoerd.
  * **Hoofddoelserver**: hier worden de replicatiegegevens tijdens de failback vanuit Azure afgehandeld.
    U kunt ook een beheerserver die als een processerver fungeert voor het schalen van uw implementatie alleen implementeren.
* **De Mobility-service**: dit onderdeel wordt geïmplementeerd op elke machine (VM VMware of fysieke server) die u wilt repliceren naar Azure. Deze gegevens schrijfbewerkingen op de machine vastgelegd en stuurt deze door naar de processerver.
* **Azure**: U hoeft niet te maken van een Azure VM's voor het afhandelen van replicatie en failover. De Site Recovery-service verwerkt gegevensbeheer en gegevens rechtstreeks naar de Azure-opslag gerepliceerd. Gerepliceerde Azure VM's worden automatisch ingezette alleen bij een failover naar Azure. Echter, als u een failback van Azure naar de lokale site wilt, wordt moet u een Azure VM instellen om te fungeren als een processerver.

De volgende afbeelding (gemaakt door Henry Robalino) toont de wisselwerking tussen deze onderdelen:

![Componentarchitectuur](./media/site-recovery-vmware-to-azure/v2a-architecture-henry.png)

## <a name="capacity-planning"></a>Capaciteitsplanning
Wanneer u van plan bent capaciteit hier van wat u nodig hebt bij het nadenken over:

* **De bronomgeving**: capaciteitsplanning of VMware-infrastructuur en bron vereisten van de machine.
* **De beheerserver**: plannen voor de lokale management-servers met onderdelen van Site Recovery.
* **Netwerkbandbreedte van bron naar doel**: Planning voor netwerkbandbreedte nodig is voor replicatie tussen de bron- en Azure.

### <a name="source-environment-considerations"></a>Bron omgeving overwegingen
* **Maximale dagelijkse wijzigingssnelheid**: een beveiligde machine slechts één processerver kunt gebruiken. Een enkel proces-server kan maximaal 2 TB aan gegevens wijzigen per dag verwerken. 2 TB is dus dat de maximale dagelijkse gegevens wijzigen die wordt ondersteund voor een beveiligde machine.
* **Maximale doorvoer**: een gerepliceerde machine kan deel uitmaken van een opslagaccount in Azure. Standard-opslagaccount kan maximaal 20.000 aanvragen per seconde worden verwerkt en we adviseren dat u het aantal IOPS via een bronmachine tot 20.000. Bijvoorbeeld, als er een bronmachine met 5 schijven en elke schijf 120 IOPS (grootte van 8 KB) op de bron genereert, moeten in de Azure per schijf-IOPS limiet van 500. Het aantal = totale bron IOPs/20, 000 van storage-accounts die zijn vereist.

### <a name="management-server-considerations"></a>Overwegingen voor Management server
De beheerserver wordt uitgevoerd van onderdelen van Site Recovery dat optimalisatie van gegevens, replicatie en beheer verwerken. Moet overweg kan de dagelijkse snelheid capaciteit voor wijzigen voor alle werkbelastingen op beveiligde machines uitgevoerd en er voldoende bandbreedte continu om gegevens te repliceren naar Azure-opslag. Specifiek:

* De processerver ontvangt replicatiegegevens van beveiligde machines en optimaliseert met caching, compressie en codering voordat naar Azure worden verzonden. De beheerserver hebt voldoende bronnen zijn voor deze taken uitvoeren.
* Schijfcache maakt gebruik van de processerver. U wordt aangeraden een afzonderlijke cache schijf 600 GB of meer voor het afhandelen van gewijzigde gegevens opgeslagen in het geval van knelpunt netwerk of een storing. Tijdens de implementatie, kunt u de cache configureren op een station met ten minste 5 GB aan opslagruimte, maar is de minimale aanbeveling 600 GB.
* Als een best practice is het raadzaam de beheerserver bevindt zich in het hetzelfde netwerk en de LAN-segment als de machines die u wilt beveiligen. Dit kan zich bevinden op een ander netwerk, maar machines die u wilt beveiligen N3 netwerk zichtbaarheid aan moeten hebben.

Aanbevelingen voor de grootte voor de beheerserver worden samengevat in de volgende tabel:

| **CPU-beheerserver** | **Geheugen** | **Cachegrootte van de schijf** | **Snelheid van de gegevens wijzigen** | **Beveiligde machines** |
| --- | --- | --- | --- | --- |
| 8 vcpu's (2-sockets * @ 2,5 GHz-4 kernen) |16 GB |300 GB |500 GB of minder |Implementeer een beheerserver met deze instellingen minder dan 100 machines repliceren. |
| 12 vcpu's (2-sockets * @ 2,5 GHz-6 kernen) |18 GB |600 GB |500 GB tot 1 TB |Implementeer een beheerserver met deze instellingen 100 tot 150-machines repliceren. |
| 16 vcpu's (2-sockets * @ 2,5 GHz-8 kernen) |32 GB |1 TB |1 TB tot 2 TB |Implementeer een beheerserver met deze instellingen 150 tot 200-machines repliceren. |
| Een andere processerver implementeren | | |> 2 TB |Aanvullende processen servers implementeren als u meer dan 200 machines repliceert, of als de dagelijkse hoeveelheden wijzigen frequentie hoger is dan 2 TB. |

Waar:

* Elke bronmachine is geconfigureerd met 3 schijven van 100 GB.
* We gebruiken benchmarking opslag van 8 SAS-schijven van 10.000 RPM RAID 10 voor cache schijf metingen.

### <a name="network-bandwidth-from-source-to-target"></a>Netwerkbandbreedte van bron naar doel
Zorg ervoor dat u bij het berekenen van de bandbreedte die zijn vereist voor de initiële replicatie en replicatie van verschillen met behulp van de [hulpprogramma capacity planner](site-recovery-capacity-planner.md).

#### <a name="throttling-bandwidth-used-for-replication"></a>Gebruikt voor replicatie van de bandbreedte beperken
VMware-verkeer gerepliceerd naar Azure gaat via een specifiek proces-server. U kunt de bandbreedte die beschikbaar is voor replicatie van Site Recovery op die server als volgt beperken:

1. Open de Microsoft Azure Backup MMC-module op de belangrijkste management-server of op een beheerserver die met aanvullende ingericht processervers. Standaard wordt een snelkoppeling naar Microsoft Azure Backup gemaakt op het bureaublad. Of u kunt deze vinden in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Klik in de module op **Eigenschappen wijzigen**.

    ![De eigenschappen wijzigen bandbreedte beperken](./media/site-recovery-vmware-to-azure-classic/throttle1.png)
3. Op de **bandbreedtebeperking** tabblad, geeft u de bandbreedte die kan worden gebruikt voor replicatie van Site Recovery en de planning van toepassing.

    ![Replicatie van de bandbreedte beperken](./media/site-recovery-vmware-to-azure-classic/throttle2.png)

U kunt ook instellen met behulp van PowerShell beperking. Hier volgt een voorbeeld:

    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth (512*1024) -NonWorkHourBandwidth (2048*1024)

#### <a name="maximizing-bandwidth-usage"></a>Bandbreedtegebruik optimaliseren
Voor een verhoging van de bandbreedte die door Azure Site Recovery voor replicatie gebruikt, moet u een registersleutel te wijzigen.

De volgende sleutel bepaalt het aantal threads per schijf repliceren die worden gebruikt bij het repliceren:

    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication\UploadThreadsPerVM

 In een overprovisioning netwerk moet deze registersleutel worden gewijzigd van de standaardwaarden. Wij ondersteunen maximaal 32.  

Zie voor meer informatie over het plannen van capaciteit gedetailleerde [Site Recovery-Capaciteitsplanner](site-recovery-capacity-planner.md).

### <a name="additional-process-servers"></a>Aanvullende processen servers
Als u moet meer dan 200 computers beveiligen of uw dagelijkse wijzigingssnelheid groter dat 2 TB, u extra servers toevoegen kunt voor het afhandelen van de belasting. Als u wilt uitbreiden, kunt u het volgende doen:

* Verhoog het aantal beheerservers. U kunt bijvoorbeeld maximaal 400 machines met twee beheerservers beveiligen.
* Aanvullende processen servers toevoegen en deze te verwerken van het verkeer in plaats van (of als aanvulling op) gebruiken de beheerserver.

Deze tabel wordt een scenario waarin beschreven:

* U instellen de oorspronkelijke management-server om te gebruiken als een configuratieserver.
* U instellen een extra processerver.
* U configureren beveiligde virtuele machines voor het gebruik van de aanvullende processerver.
* Elke machine beveiligde bron is geconfigureerd met drie schijven van 100 GB.

| **Oorspronkelijke management server**<br/><br/>(configuratieserver) | **Aanvullende processerver** | **Cachegrootte van de schijf** | **Snelheid van de gegevens wijzigen** | **Beveiligde machines** |
| --- | --- | --- | --- | --- |
| 8 vcpu's (2-sockets * 4 kernen @ 2,5 GHz), 16 GB RAM-geheugen |4 vcpu's (2-sockets * 2 kernen @ 2,5 GHz), 8 GB RAM-geheugen |300 GB |250 GB of minder |U kunt 85 of minder machines repliceren. |
| 8 vcpu's (2-sockets * 4 kernen @ 2,5 GHz), 16 GB RAM-geheugen |8 vcpu's (2-sockets * 4 kernen @ 2,5 GHz), 12 GB RAM-geheugen |600 GB |250 GB tot 1 TB |U kunt 85 150-machines repliceren. |
| 12 vcpu's (2-sockets * 6 kernen @ 2,5 GHz), 18 GB RAM-geheugen |12 vcpu's (2-sockets * 6 kernen @ 2,5 GHz) 24 GB RAM-geheugen |1 TB |1 TB tot 2 TB |U kunt 150 225 machines repliceren. |

Hoe u de schaal van uw servers, is afhankelijk van uw voorkeur voor een model omhoog schalen of scale-out. U implementeert enkele geavanceerde management en processervers opschalen of uitbreiden door het implementeren van meerdere servers met minder bronnen. Bijvoorbeeld: als u beveiligen 220 machines wilt, kunt u een van de volgende doen:

* De oorspronkelijke management-server configureren met 12 vcpu's en 18 GB aan RAM-geheugen. Een extra processerver configureren met 12 vcpu's en 24 GB aan RAM-geheugen. Beveiligde machines voor het gebruik van de aanvullende processerver configureren.
* Configureer twee beheerservers (2 x 8 Vcpu, 16 GB RAM-geheugen) en twee extra processervers (1 x 8 vcpu's en 4vCPUs x 1 voor het afhandelen van 135 + 85 (220)-machines). Beveiligde machines voor het gebruik van alleen de aanvullende processen servers configureren.

Volg de instructies in [aanvullende processen servers implementeren](#deploy-additional-process-servers) voor het instellen van een extra process-server.

## <a name="before-you-start-deployment"></a>Voordat u implementatie begint
De volgende tabellen geven een overzicht van de vereisten voor het implementeren van dit scenario.

### <a name="azure-prerequisites"></a>Vereisten voor Azure
| **Vereiste** | **Details** |
| --- | --- |
| **Azure-account** |U hebt een [Microsoft Azure](https://azure.microsoft.com/)-account nodig. U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/). Zie voor meer informatie over prijzen voor Site Recovery [siteherstel](https://azure.microsoft.com/pricing/details/site-recovery/). |
| **Azure Storage** |U hebt een Azure Storage-account nodig om gerepliceerde gegevens op te slaan. Gerepliceerde gegevens worden opgeslagen in Azure storage en Azure VM's worden ingezet wanneer failover plaatsvindt. <br/><br/>U hebt een [standaard geografisch redundant opslagaccount](../storage/storage-redundancy.md#geo-redundant-storage) nodig. Het account moet zich in dezelfde regio bevinden als de Site Recovery-service en worden gekoppeld aan hetzelfde abonnement. Replicatie naar premium storage-accounts wordt momenteel niet ondersteund en mag niet worden gebruikt.<br/><br/>We bieden geen ondersteuning voor bewegende opslagaccounts die zijn gemaakt met behulp van de [Azure-portal](../storage/storage-create-storage-account.md) over resourcegroepen. Zie voor meer informatie [Inleiding tot Microsoft Azure Storage](../storage/storage-introduction.md).<br/><br/> |
| **Azure-netwerk** |U een Azure-netwerk nodig waarmee virtuele Azure-machines verbinding maken wanneer failover plaatsvindt. Het virtuele Azure-netwerk moet zich in dezelfde regio bevinden als de Site Recovery-kluis.<br/><br/>Als u wilt niet na de failover naar Azure, moet u een VPN-verbinding (of Azure ExpressRoute) instellen vanaf het netwerk van Azure naar de lokale site. |

### <a name="on-premises-prerequisites"></a>Vereisten voor on-premises
| **Vereiste** | **Details** |
| --- | --- |
| **Beheerserver** |U moet een on-premises Windows 2012 R2-server uitgevoerd op een virtuele machine of fysieke server. Alle van de on-premises Site Recovery-onderdelen zijn geïnstalleerd op deze beheerserver.<br/><br/> Het is raadzaam om de implementatie van de server als een maximaal beschikbare VMware-VM. Failback naar de lokale site van Azure is altijd ingesteld op virtuele VMware-machines ongeacht of u failover van virtuele machines of fysieke servers. Als de beheerserver als een VMware-VM niet is geconfigureerd, moet u een afzonderlijke hoofddoelserver instellen als een VMware-VM failbackverkeer ontvangt.<br/><br/>De server mag niet een domeincontroller zijn.<br/><br/>De server moet een statisch IP-adres hebben.<br/><br/>De hostnaam van de server moet 15 tekens of minder.<br/><br/>De landinstelling van het besturingssysteem moet alleen Engels zijn.<br/><br/>De beheerserver is internettoegang vereist.<br/><br/>Moet u uitgaand verkeer van de server als volgt: tijdelijke toegang op http-80 tijdens de installatie van de Site Recovery-onderdelen (om het downloaden van MySQL); actieve uitgaande toegang via HTTPS 443 voor het replicatiebeheer van; actieve uitgaande toegang via HTTPS 9443 voor replicatieverkeer (deze poort kan worden aangepast).<br/><br/> Zorg ervoor dat deze URL's zijn toegankelijk vanaf de beheerserver: <br/>- \*.hypervrecoverymanager.windowsazure.com<br/>- \*.accesscontrol.windows.net<br/>- \*.backup.windowsazure.com<br/>- \*.blob.core.windows.net<br/>- \*.store.core.windows.net<br/>-https://www.msftncsi.com/ncsi.txt<br/>- [https://dev.mysql.com/Get/Archives/MySQL-5.5/MySQL-5.5.37-Win32.msi](https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi")<br/><br/>Als u IP-adressen gebaseerde firewallregels op de server hebt, controleert u of de regels communicatie met Azure toestaan. Sta de IP-adresbereiken toe die worden beschreven in [Azure Datacenter IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) (Azure Datacenter IP-bereiken), evenals de poort HTTPS (443). U moet ook voor de lijst met geaccepteerde IP-adresbereiken voor de Azure-regio van uw abonnement en voor VS-West. De URL [https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi](https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi") is voor het downloaden van MySQL. |
| **VMware vCenter/ESXi-host** |U moet een of meer VMware vSphere ESX/ESXi-hypervisors beheren van uw virtuele machines van VMware, ESX/ESXi versie 6.0, 5.5 of 5.1 uitgevoerd met de meest recente updates.<br/><br/> Het is raadzaam dat u een VMware vCenter-server implementeert voor het beheren van uw ESXi-hosts. Worden moet gestart vCenter versie 6.0 of 5.5 met de nieuwste updates.<br/><br/>Houd er rekening mee dat de Site Recovery biedt geen ondersteuning voor nieuwe vCenter en vSphere 6.0 functies zoals cross vCenter vMotion, virtuele volumes en opslagruimten DRS. Site Recovery-ondersteuning is beperkt tot de functies die ook beschikbaar in versie 5.5 waren. |
| **Beveiligde machines** |**Azure**<br/><br/>Computers die u wilt beveiligen, moeten voldoen aan [vereisten voor Azure](site-recovery-prereq.md) voor het maken van virtuele Azure-machines.<br><br/>Als u verbinding maken met de Azure VM's na een failover wilt, moet u extern bureaublad-verbindingen op de lokale firewall inschakelen.<br/><br/>Op beveiligde machines mag de capaciteit per schijf niet meer dan 1023 GB bedragen. Een virtuele machine mag maximaal 64 schijven hebben (maximaal 64 TB). Als u schijven groter dan 1 TB hebt, overweeg het gebruik van databasereplicatie zoals SQL Server Always On of Oracle Data Guard.<br/><br/>Minimaal 2 GB aan beschikbare ruimte voor de installatie voor de installatie van onderdelen.<br/><br/>Gastclusters met gedeelde schijven worden niet ondersteund. Als u een geclusterde implementatie hebt, overweeg het gebruik van databasereplicatie zoals SQL Server Always On of Oracle Data Guard.<br/><br/>Unified Extensible Firmware Interface (UEFI) / Extensible Firmware Interface(EFI) wordt niet ondersteund.<br/><br/>Namen voor machines moeten tussen 1 en maximaal 63 tekens bevatten (letters, cijfers en afbreekstreepjes) bevatten. De naam moet beginnen met een letter of cijfer en eindigen met een letter of cijfer. Nadat een machine is beveiligd, kunt u de naam van Azure kunt wijzigen.<br/><br/>**Virtuele VMware-machines**<br/><br>U moet VMware vSphere PowerCLI 6.0 installeren. op de beheerserver (configuratieserver).<br/><br/>VMware-machines die u wilt beveiligen moet VMware tools geïnstalleerd en actief zijn.<br/><br/>Als de bron VM NIC-koppeling heeft, wordt deze geconverteerd naar één NIC na een failover naar Azure.<br/><br/>Als beveiligde virtuele machines hebt een iSCSI-schijf, converteert Site Recovery de beveiligde VM iSCSI-schijf naar een VHD-bestand, als de virtuele machine failover wordt uitgevoerd naar Azure. Als iSCSI-doel kan worden bereikt door de virtuele machine in Azure, wordt verbinding maken met iSCSI-doel en wordt in feite twee schijven te zien: de VHD-schijf op de virtuele machine van Azure en de bron iSCSI-schijf. In dit geval moet u Verbreek de verbinding met het iSCSI-doel die wordt weergegeven op de virtuele machine failover van Azure.<br/><br/>Voor meer informatie over de gebruikersmachtigingen VMware die Site Recovery moet, Zie [VMware toegangsmachtigingen vCenter](#vmware-permissions-for-vcenter-access).<br/><br/> **Windows Server-machines (op VMware VM of fysieke server)**<br/><br/>De server moet worden uitgevoerd op een ondersteund 64-bits besturingssysteem: Windows Server 2012 R2, Windows Server 2012 of Windows Server 2008 R2 met op minimaal SP1.<br/><br/>Het besturingssysteem moet worden geïnstalleerd op station C en de besturingssysteemschijf moet een standaardschijf van Windows. (Het besturingssysteem mag niet worden geïnstalleerd op een Windows-dynamische schijf.)<br/><br/>Voor Windows Server 2008 R2-machines moet u .NET Framework 3.5.1 geïnstalleerd hebben.<br/><br/>U moet een administrator-account opgeven (dit moet een lokale beheerder op de Windows-machine zijn) voor de pushinstallatie de Mobility-Service op Windows-servers. Als het opgegeven account een niet-domeinaccount is, moet u de gebruiker RAS-beheer op de lokale computer uitschakelen. Zie voor meer informatie [installeren van de mobility-service met push-installatie](#install-the-mobility-service-with-push-installation).<br/><br/>Site Recovery biedt ondersteuning voor virtuele machines met een RDM-schijf. Tijdens de failback, zal Site Recovery opnieuw gebruiken van de RDM-schijf als de oorspronkelijke bron-VM en RDM-schijf beschikbaar zijn. Als ze niet beschikbaar is, die tijdens de failback worden uitgevoerd, maakt Site Recovery een nieuw VMDK-bestand voor elke schijf.<br/><br/>**Linux-machines**<br/><br/>U moet een ondersteund 64-bits besturingssysteem: Red Hat Enterprise Linux 6.7; Centos 6.5, 6.6 of 6.7; Oracle Enterprise Linux, 6.4 of 6.5 met Red Hat compatibel kernel of Unbreakable Enterprise Kernel versie 3 (UEK3); SUSE Linux Enterprise Server 11 SP3.<br/><br/>/ etc/hosts bestanden op beveiligde machines moeten vermeldingen die de naam van de lokale host aan IP-adressen die zijn gekoppeld aan alle netwerkadapters toewijzen bevatten. <br/><br/>Als u wilt verbinding maken met Azure een virtuele machine met Linux na een failover via een Secure Shell-client (ssh), zorg ervoor dat de Secure Shell-service op de beveiligde computer is ingesteld op automatisch op opstarten van het systeem starten en dat firewall-regels toestaan een ssh verbinding mee.<br/><br/>Beveiliging kan alleen worden ingeschakeld voor Linux-machines met de volgende opslag: File system (EXT3, ETX4, ReiserFS, XFS); Multipath-software-apparaat toewijzen (MPIO); Volume manager (LVM2). Fysieke servers met HP CCISS controller opslag worden niet ondersteund. Het bestandssysteem ReiserFS wordt alleen ondersteund op SUSE Linux Enterprise Server 11 SP3.<br/><br/>Site Recovery biedt ondersteuning voor virtuele machines met een RDM-schijf. Tijdens de failback voor Linux Site Recovery niet opnieuw gebruiken van de RDM-schijf. In plaats daarvan wordt een nieuw VMDK-bestand voor elke overeenkomende RDM-schijf gemaakt. |

Alleen voor een Linux-VM: Zorg ervoor dat u de instelling disk.enableUUID=true ingesteld in de configuratieparameters van de virtuele machine in VMware. Als deze rij niet bestaat, moet u deze toevoegen. Dit is vereist voor een consistente UUID bieden aan de VMDK zodat deze correct koppelt. Zonder deze instelling wordt failback, wordt een volledige download zelfs als de virtuele machine beschikbaar lokaal is. Deze instelling toe te voegen, zorgt u ervoor dat alleen nog deltawijzigingen worden overgedragen tijdens de failback.

## <a name="step-1-create-a-vault"></a>Stap 1: Een kluis maken
1. Meld u aan bij [Azure Portal](https://manage.windowsazure.com/).
2. Vouw **Data Services** > **Recovery Services** en klik op **Site Recovery-kluis**.
3. Klik op **Nieuw maken** > **Snelle invoer**.
4. Voer in **Naam** een beschrijvende naam in om de kluis aan te duiden.
5. Selecteer in **Regio** de geografische regio voor de kluis. Ondersteunde regio's, Zie [Azure Site Recovery prijsinformatie](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Klik op **Kluis maken**.
    ![Kluis maken](./media/site-recovery-vmware-to-azure-classic/quick-start-create-vault.png)

Controleer de statusbalk om te bevestigen dat de kluis is gemaakt. De kluis wordt weergegeven als **Active** op de hoofdblade **Recovery Services** pagina.

## <a name="step-2-set-up-an-azure-network"></a>Stap 2: Een Azure-netwerk instellen
Een Azure-netwerk instellen zodat de virtuele Azure-machines worden verbonden met een netwerk na een failover en failback naar de lokale site kunt werken zoals verwacht.

1. Selecteer in de Azure-portal **virtueel netwerk maken** en geef de netwerknaam, IP-adresbereik en de subnetnaam van het.
2. Als u doen failback moet, voegt u VPN en ExpressRoute toe aan het netwerk. VPN en ExpressRoute kunnen worden toegevoegd aan het netwerk zelfs na een failover.

Zie voor meer informatie over Azure-netwerken, [virtuele netwerken overzicht](../virtual-network/virtual-networks-overview.md).

> [!NOTE]
> [Migratie van netwerken](../azure-resource-manager/resource-group-move-resources.md) in resourcegroepen binnen hetzelfde abonnement of tussen abonnementen wordt niet ondersteund voor netwerken die worden gebruikt voor het implementeren van Site Recovery.
>
>

## <a name="step-3-install-the-vmware-components"></a>Stap 3: De VMware-onderdelen installeren
Als u repliceren van virtuele VMware-machines wilt, als volgt op de beheerserver:

1. [Download](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1) en VMware vSphere PowerCLI 6.0 installeren.
2. De server opnieuw opstarten.

## <a name="step-4-download-a-vault-registration-key"></a>Stap 4: Een kluisregistratiesleutel downloaden
1. Open de Site Recovery-console in Azure vanaf de beheerserver. Op de **Recovery Services** pagina, klikt u op de kluis openen de **Quick Start** pagina. U kunt ook openen de **Quick Start** pagina op elk gewenst moment door te klikken op het pictogram.

    ![Pictogram Quick Start](./media/site-recovery-vmware-to-azure-classic/quick-start-icon.png)
2. Op de **Quick Start** pagina, klikt u op **Doelresources voorbereiden** > **Download een registratiesleutel**. Het registratiebestand wordt automatisch gegenereerd. Het is geldig voor vijf dagen nadat deze gegenereerd.

## <a name="step-5-install-the-management-server"></a>Stap 5: De beheerserver installeren
> [!TIP]
> Zorg ervoor dat deze URL's zijn toegankelijk vanaf de beheerserver:
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



1. Op de **Quick Start** pagina, de uniforme installatiebestand naar de server downloaden.
2. Voer het installatiebestand om setup te starten de **Unified installatie van Site Recovery** wizard.
3. Selecteer bij **Voordat u begint** de optie **De configuratieserver en processerver installeren**.

   ![Voordat u begint](./media/site-recovery-vmware-to-azure-classic/combined-wiz1.png)
4. In **van derden softwarelicentie**, klikt u op **ik ga akkoord** downloaden en installeren van MySQL.

    ![Software van derden](./media/site-recovery-vmware-to-azure-classic/combined-wiz105.PNG)
5. In **registratie**, bladeren en selecteer de registratiesleutel die u hebt gedownload van de kluis.

    ![Registratie](./media/site-recovery-vmware-to-azure-classic/combined-wiz3.png)
6. In **internetinstellingen**, opgeven hoe de provider die wordt uitgevoerd op de configuratieserver wordt verbinding met Azure Site Recovery via Internet.

   * Als u verbinding wilt maken met de proxy die momenteel op de computer is ingesteld, selecteert u **Verbinding maken met bestaande proxyinstellingen**.
   * Als u wilt dat de provider rechtstreeks verbinding maakt, selecteert u **rechtstreeks verbinden zonder een proxy**.
   * Als de bestaande proxy verificatie vereist is of als u wilt een aangepaste proxy gebruikt voor de providerverbinding, selecteer **verbinding maken met aangepaste proxyinstellingen**.
     * Als u een aangepaste proxy gebruikt, moet u het adres, poort en referenties opgeven.
     * Als u een proxy gebruikt, hebt u al mag de volgende URL's:
       * *.hypervrecoverymanager.windowsazure.com    
       * *.accesscontrol.windows.net
       * *.backup.windowsazure.com
       * *.blob.core.windows.net
       * *.store.core.windows.net

    ![Firewall](./media/site-recovery-vmware-to-azure-classic/combined-wiz4.png)

1. In **controle van vereisten**, een selectievakje om ervoor te zorgen dat de installatie kunt uitvoeren door Setup wordt uitgevoerd.

    ![Vereisten](./media/site-recovery-vmware-to-azure-classic/combined-wiz5.png)

     Als er een waarschuwing wordt weergegeven over **Synchronisatiecontrole voor algemene tijd**, moet u controleren of de tijd op de systeemklok (instellingen voor **datum en tijd**) overeenkomt met de tijdzone.

     ![Synchronisatieprobleem in de tijd](./media/site-recovery-vmware-to-azure-classic/time-sync-issue.png)

1. In **MySQL configuratie**, maken de referenties voor aanmelding bij de MySQL-server-exemplaar dat wordt geïnstalleerd.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz6.png)
2. Selecteer bij **Details van de omgeving** of u virtuele VMware-machines wilt repliceren. Als u bent, controleert het installatieprogramma dat PowerCLI 6.0 is geïnstalleerd.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz7.png)
3. Selecteer bij **Installatielocatie** waar u de binaire bestanden wilt installeren en de cache wilt opslaan. U kunt een station met ten minste 5 GB aan beschikbare schijfruimte selecteren, maar we raden een cachestation met ten minste 600 GB beschikbare schijfruimte.

   ![Installatielocatie](./media/site-recovery-vmware-to-azure-classic/combined-wiz8.png)
4. In **netwerk selecteren**, geef de listener (netwerkadapter en SSL-poort) waarop de configuratieserver verzendt en ontvangt gegevens van replicatie. U kunt de standaard poort (9443). Naast deze poort wordt poort 443 worden gebruikt door een webserver die replicatiebewerkingen ingedeeld. Gebruik geen 443 voor het ontvangen van replicatieverkeer.

    ![Netwerk selecteren](./media/site-recovery-vmware-to-azure-classic/combined-wiz9.png)



1. Lees de informatie bij **Samenvatting** en klik op **Installeren**. Wanneer de installatie is voltooid, wordt er een wachtwoordzin gegenereerd. U hebt deze nodig wanneer u replicatie inschakelt, dus kopieer deze en bewaar deze op een veilige locatie.

   ![Samenvatting](./media/site-recovery-vmware-to-azure-classic/combined-wiz10.png)


> [!WARNING]
> De Microsoft Azure Recovery Service Agent-proxy moet worden ingesteld.
> Nadat de installatie is voltooid, start u de Microsoft Azure Recovery Services-Shell vanuit het menu Start. Voer de volgende reeks opdrachten voor het instellen van de proxy-instellingen in het opdrachtvenster.
>
>
    $pwd = ConvertTo-SecureString -String ProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumb – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
>


### <a name="run-setup-from-the-command-line"></a>Voer setup uit vanaf de opdrachtregel
U kunt ook de uniforme wizard uitvoeren vanaf de opdrachtregel als volgt:

    UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]

Waar:

* /ServerMode: Verplicht. Hiermee geeft u op of de installatie, de configuratie- en -servers of alleen de processerver installeren moet (gebruikt voor het installeren van extra processervers). Invoerwaarden: CS, PS.
* InstallDrive: verplicht. Hiermee geeft u de map waar de onderdelen zijn geïnstalleerd.
* / MySQLCredFilePath. Verplicht. Hiermee geeft u het pad naar het bestand waarin de referenties van MySQL-server zijn opgeslagen. De sjabloon voor het maken van het bestand worden opgehaald.
* / VaultCredFilePath. Verplicht. Locatie van het kluisreferentiebestand.
* /EnvType. Verplicht. Type installatie. Waarden: VMware, NonVMware.
* /PSIP en /CSIP. Verplicht. IP-adres van de processerver en de configuratieserver.
* /PassphraseFilePath. Verplicht. Locatie van het bestand wachtwoordzin.
* / ByPassProxy. Optioneel. Hiermee geeft u de beheerserver die verbinding met Azure zonder een proxy maakt.
* /ProxySettingsFilePath. Optioneel. Hiermee geeft u instellingen voor een aangepaste proxy (standaardproxy op de server die moet worden geverifieerd) of aangepaste proxy.

## <a name="step-6-set-up-credentials-for-the-vcenter-server"></a>Stap 6: Referenties voor de vCenter-server instellen
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Discovery/player]
>
>

De processerver kan automatisch detecteren voor virtuele VMware-machines die worden beheerd door een vCenter-server. Voor automatische detectie moet Site Recovery een account en de referenties die toegang de vCenter-server tot. Dit is niet relevant als u alleen fysieke servers repliceert.

De serviceaccount en referenties instellen:

1. Maak een rol op de vCenter-server (**Azure_Site_Recovery**) op het niveau van de vCenter-met de [vereist machtigingen](#vmware-permissions-for-vcenter-access).
2. Wijs de **Azure_Site_Recovery** rol aan een vCenter-gebruiker.

   > [!NOTE]
   > Een vCenter-gebruikersaccount dat de rol alleen-lezen heeft kunt failover uitvoeren zonder beveiligde bronmachines afgesloten. Als u deze machines afsluiten wilt, moet u de functie Azure_Site_Recovery. Als u alleen virtuele machines van VMware naar Azure migreren bent en hoeft niet te failback, is de rol alleen-lezen is voldoende.
   >
   >
3. Om het account toevoegt, open **cspsconfigtool**. Het is beschikbaar als een snelkoppeling op het bureaublad en zich in de map van de \home\svsystems\bin [locatie installeren].
4. Klik op het tabblad **Accounts beheren** op **Account toevoegen**.

    ![Account toevoegen](./media/site-recovery-vmware-to-azure-classic/credentials1.png)
5. In **accountdetails**, referenties die kunnen worden gebruikt voor toegang tot de vCenter-server toevoegen. Het kan meer dan 15 minuten duren voordat de accountnaam moet worden weergegeven in de portal. Voor het direct bijwerken, klikt u op **vernieuwen** op de **configuratieservers** tabblad.

    ![Details](./media/site-recovery-vmware-to-azure-classic/credentials2.png)

## <a name="step-7-add-vcenter-servers-and-esxi-hosts"></a>Stap 7: VCenter server- en ESXi-hosts toevoegen
Als u virtuele VMware-machines repliceert, moet u een vCenter-server (of ESXi-host) toe te voegen.

1. Op de **Servers** > **configuratieservers** tabblad **vCenter-server toevoegen**.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter1.png)
2. De vCenter-server of details van ESXi-host, de naam van het account dat u hebt opgegeven voor toegang tot de vCenter-server in de vorige stap, en de processerver die wordt gebruikt voor het detecteren van VMware-machines die worden beheerd door de vCenter-server toevoegen. De vCenter-server of ESXi-host moet zich in hetzelfde netwerk bevindt als de server waarop de processerver is geïnstalleerd.

   > [!NOTE]
   > Als u de vCenter-server of ESXi-host met een account dat geen administrator-bevoegdheden op de server met vCenter of host toevoegt, zorg ervoor dat de vCenter of ESXi-accounts hebben deze bevoegdheden ingeschakeld: Datacenter, gegevensopslag, map, Jost, netwerk, Resource, virtuele Machine en vSphere gedistribueerde overschakelen. De vCenter-server moet de bevoegdheid opslag weergaven is ingeschakeld.
   >
   >

    ![VCenter-server toevoegen](./media/site-recovery-vmware-to-azure-classic/add-vcenter2.png)
3. Nadat de detectie is voltooid, kunt u de vCenter-server wordt weergegeven op de **configuratieservers** tabblad.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter3.png)

## <a name="step-8-create-a-protection-group"></a>Stap 8: Maak een beveiligingsgroep
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Protection/player]
>
>

Beveiligingsgroepen zijn logische groeperingen van virtuele machines of fysieke servers dat u beveiligen wilt met behulp van dezelfde beveiligingsinstellingen. U beveiligingsinstellingen toe aan een beveiligingsgroep en die instellingen worden toegepast op alle machines (virtuele of fysieke) dat u aan de groep toevoegt.

1. Ga naar **beveiligde Items** > **beveiligingsgroep** en klik op het pictogram om een beveiligingsgroep toevoegen.

    ![Beveiligingsgroep maken](./media/site-recovery-vmware-to-azure-classic/protection-groups1.png)
2. Op de **instellingen voor de beveiligingsgroep opgeven** pagina, Geef een naam voor de groep. In de **van** vervolgkeuzelijst, selecteert u de configuratieserver waarop u wilt maken van de groep. **Doel** is Microsoft Azure.

    ![Instellingen voor de beveiligingsgroep](./media/site-recovery-vmware-to-azure-classic/protection-groups2.png)
3. Op de **replicatie-instellingen opgeven** pagina, configureer de replicatie-instellingen die worden gebruikt voor alle machines in de groep.

    ![Beveiliging groep Replicatie](./media/site-recovery-vmware-to-azure-classic/protection-groups3.png)

   * **Consistentie tussen Multi-VM's**: als u dit inschakelen op, maakt het gedeelde toepassingsconsistente herstelpunten op de computers in de beveiligingsgroep. Deze instelling is de meest relevante wanneer alle machines in de beveiligingsgroep dezelfde werkbelasting worden uitgevoerd. Alle machines worden hersteld naar het hetzelfde gegevenspunt. Dit is beschikbaar of u repliceert VMware-machines of fysieke servers (Windows of Linux).
   * **Drempelwaarde voor RPO**: Hiermee stelt u de RPO. Waarschuwingen worden gegenereerd wanneer de replicatie van de beveiliging doorlopende gegevens groter is dan de geconfigureerde drempelwaarde van RPO.
   * **Herstel bewaarperiode**: Hiermee geeft u de bewaarperiode. Beveiligde machines kunnen worden hersteld naar een willekeurig punt binnen dit tijdsbestek.
   * **Toepassingsconsistente momentopnamen frequentie**: geeft aan hoe vaak de herstelpunten die toepassingsconsistente momentopnamen bevatten worden gemaakt.

Wanneer u het selectievakje selecteert, wordt een beveiligingsgroep is gemaakt met de naam die u hebt opgegeven. Bovendien een tweede beveiligingsgroep wordt gemaakt met de naam *beveiliging groepsnaam*- Failback. Deze beveiligingsgroep wordt gebruikt als u een failback naar de lokale site na een failover naar Azure. U kunt de beveiligingsgroepen bewaken zoals ze worden gemaakt op de **beveiligde Items** pagina.

## <a name="step-9-install-the-mobility-service"></a>Stap 9: Installeer de Mobility-service
De eerste stap bij het inschakelen van beveiliging voor virtuele machines en fysieke servers is het installeren van de Mobility-service. U kunt dit op twee manieren doen:

* Automatisch pushen en installeren van de service op elke machine van de processerver. Wanneer u machines aan een beveiligingsgroep toevoegen en ze een juiste versie van de Mobility-service al hebt uitgevoerd, zich push-installatie niet voor. U kunt de service automatisch ook installeren met behulp van uw onderneming push-methode, zoals WSUS of System Center Configuration Manager. Zorg ervoor dat u hebt de beheerserver ingesteld voordat u dit doen.
* De service handmatig installeren op elke machine die u wilt beveiligen. Zorg ervoor dat u hebt de beheerserver ingesteld voordat u dit doen.

### <a name="install-the-mobility-service-with-push-installation"></a>Installeer de Mobility-service met push-installatie
Wanneer u computers aan een beveiligingsgroep toevoegt, wordt de Mobility-service automatisch gepusht en geïnstalleerd op elke computer met de processerver.

#### <a name="prepare-for-automatic-push-on-windows-machines"></a>Automatische push voorbereiden op Windows-computers
Windows-machines voorbereiden zodat de Mobility-service kan automatisch worden geïnstalleerd door de processerver:

1. Maak een account die de processerver gebruiken kunt voor toegang tot de machine. Het account moet administrator-bevoegdheden (lokaal of domeinbeheerder) hebben. Deze referenties worden alleen gebruikt voor push-installatie van de Mobility-service.

   > [!NOTE]
   > Als u niet een domeinaccount, moet u beheer van de externe gebruikerstoegang op de lokale computer uitschakelen. De DWORD-vermelding LocalAccountTokenFilterPolicy met een waarde van 1 kunt u dit doen in het register onder HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System, toevoegen onder. Als het register-item van een opdracht voor het openen van CLI of met behulp van PowerShell, voer  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** .
   >
   >
2. Voor Windows Firewall op de computer die u wilt beveiligen, selecteert u **toestaan van een app of functie via Firewall**, en schakel **bestands- en printerdeling** en **Windows Management Instrumentation**. Voor de machines die deel uitmaken van een domein, kunt u de firewall-beleid configureren met een groepsbeleidsobject.

   ![Firewallinstellingen](./media/site-recovery-vmware-to-azure-classic/mobility1.png)
3. Voeg het account dat u hebt gemaakt:

   * Open **cspsconfigtool**. Het is beschikbaar als een snelkoppeling op het bureaublad en zich in de map van de \home\svsystems\bin [locatie installeren].
   * Klik op het tabblad **Accounts beheren** op **Account toevoegen**.
   * Voeg het account dat u hebt gemaakt. Nadat u het account toevoegt, moet u de referenties opgeven wanneer u een computer aan een beveiligingsgroep toevoegt.

#### <a name="prepare-for-automatic-push-on-linux-servers"></a>Automatische push voorbereiden op Linux-servers
1. Zorg ervoor dat de Linux-machine die u wilt beveiligen wordt ondersteund, zoals beschreven in [On-premises vereisten](#on-premises-prerequisites). Zorg ervoor dat er netwerkverbinding is tussen de computer die u wilt beveiligen en de beheerserver die de processerver wordt uitgevoerd.
2. Maak een account die de processerver gebruiken kunt voor toegang tot de machine. Het account moet een Hoofdgebruiker op de bronserver Linux. Deze referenties worden alleen gebruikt voor push-installatie van de Mobility-service.

   * Open **cspsconfigtool**. Het is beschikbaar als een snelkoppeling op het bureaublad en zich in de map van de \home\svsystems\bin [locatie installeren].
   * Klik op het tabblad **Accounts beheren** op **Account toevoegen**.
   * Voeg het account dat u hebt gemaakt. Nadat u het account toevoegt, moet u de referenties opgeven wanneer u een computer aan een beveiligingsgroep toevoegt.
3. Controleer of het bestand /etc/hosts op de Linux-bronserver vermeldingen bevat die de lokale hostnaam toewijzen aan IP-adressen die zijn gekoppeld aan alle netwerkadapters.
4. Installeer de meest recente openssh, openssh-server en openssl-pakketten op de computer die u wilt beveiligen.
5. Zorg ervoor dat SSH ingeschakeld en worden uitgevoerd op poort 22.
6. U kunt als volgt het SFTP-subsysteem en wachtwoordverificatie inschakelen in het bestand sshd_config:

   * Meld u aan als hoofdmap.
   * Zoek de regel die met PasswordAuthentication begint in het bestand /etc/ssh/sshd_config.
   * Verwijder opmerkingen bij de regel en wijzig de waarde van **nee** naar **ja**.
   * Zoek de regel die begint met **Subsystem** en verwijder opmerkingen bij de regel.

     ![Linux standaardinstelling van geen subsystemen negeren](./media/site-recovery-vmware-to-azure-classic/mobility2.png)

### <a name="install-the-mobility-service-manually"></a>De Mobility-service handmatig installeren
Het installatieprogramma's zijn beschikbaar in C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository.

| Bronbesturingssysteem | Installatiebestand van de Mobility-service |
| --- | --- |
| Windows Server (alleen 64-bits) |Microsoft-ASR_UA_9*.0.0_Windows_* release.exe |
| CentOS 6.4, 6.5, 6.6 (alleen 64-bits) |Microsoft-ASR_UA_9*.0.0_RHEL6-64_*release.tar.gz |
| SUSE Linux Enterprise Server 11 SP3 (alleen 64-bits) |Microsoft-ASR_UA_9*.0.0_SLES11-SP3-64_*release.tar.gz |
| Oracle Enterprise Linux 6.4, 6.5 (alleen 64-bits) |Microsoft-ASR_UA_9*.0.0_OL6-64_*release.tar.gz |

#### <a name="install-the-mobility-service-manually-on-a-windows-server"></a>De Mobility-service handmatig te installeren op een Windows-server
1. Download het relevante installatieprogramma en voer het uit.
2. Selecteer in **Voordat u begint** **Mobility-service**.

    ![De installatie van de Mobility-service](./media/site-recovery-vmware-to-azure-classic/mobility3.png)
3. In **Server configuratiedetails**, geef het IP-adres van de beheerserver en de wachtwoordzin op die is gegenereerd tijdens de installatie van de management server-onderdelen. U kunt de wachtwoordzin ophalen door het uitvoeren van  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** op de beheerserver.

    ![Mobility-service](./media/site-recovery-vmware-to-azure-classic/mobility6.png)
4. In **installatielocatie**, houdt de standaardlocatie en klikt u op **volgende** om installatie te starten.
5. In **installatievoortgang**, Controleer de installatie en start de computer desgevraagd opnieuw op.

U kunt ook installeren met het invoeren van de opdrachtregel naar de volgende tekst:

    UnifiedAgent.exe [/Role <Agent/MasterTarget>] [/InstallLocation <Installation Directory>] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>] [/LogFilePath <Log File Path>]

In de voorgaande opdracht:

* / Rol: verplicht. Hiermee geeft u op of de Mobility-service moet worden geïnstalleerd.
* / InstallLocation: verplicht. Geeft aan waar de service moet worden geïnstalleerd.
* / PassphraseFilePath: verplicht. Hiermee geeft u de wachtwoordzin voor configuratie-server.
* / LogFilePath: verplicht. Hiermee geeft u het setup-logboekbestand.

#### <a name="uninstall-the-mobility-service-manually"></a>De Mobility-service handmatig verwijderen
U kunt de Mobility-service verwijderen met behulp van **een programma verwijderen of wijzigen** in het Configuratiescherm of via de opdrachtregel.

De opdracht voor het verwijderen van de Mobility-service via de opdrachtregel is:

    MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1}

#### <a name="change-the-ip-address-of-the-management-server"></a>Wijzig de IP-adres van de beheerserver
Nadat u de wizard uitvoert, kunt u het IP-adres van de beheerserver als volgt wijzigen:

1. Open het bestand hostconfig.exe (te vinden op het bureaublad).
2. Op de **Global** en wijzig het IP-adres van de beheerserver.

   > [!NOTE]
   > Alleen het IP-adres van de beheerserver wijzigen. Het poortnummer voor communicatie van de management-server moet poort 443, en **gebruik HTTPS** moet worden ingeschakeld blijft. De wachtwoordzin niet wijzigen.
   >
   >

    ![IP-adres van Management server](./media/site-recovery-vmware-to-azure-classic/host-config.png)

#### <a name="install-the-mobility-service-manually-on-a-linux-server"></a>De Mobility-service handmatig te installeren op een Linux-server
1. Kopieer de juiste tar-archief voor de Linux-machine die u wilt beveiligen. Zie de tabel onder [handmatig installeren van de Mobility-service](#install-the-mobility-service-manually) om te bepalen welke tar archiveert u moeten gebruiken.
2. Open een shellprogramma en pak de gecomprimeerde tar-archief op een lokaal pad door te voeren:`tar -xvzf Microsoft-ASR_UA_8.5.0.0*`
3. Maak een bestand met de naam passphrase.txt in de lokale map waarnaar u de inhoud van het tar-archief hebt uitgepakt. U doet dit door de wachtwoordzin van C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase op de beheerserver kopiëren en opslaan in passphrase.txt door te voeren  *`echo <passphrase> >passphrase.txt`*  in de shell.
4. Installeer de Mobility-service met de volgende opdracht:*`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`*
5. Geef het interne IP-adres van de beheerserver en controleer of poort 443 is geselecteerd.

#### <a name="install-the-mobility-service-from-the-command-line"></a>De Mobility-service installeren vanaf de opdrachtregel

Kopieer de wachtwoordzin van C:\Program Files (x86) \InMage Systems\private\connection op de beheerserver en deze opslaan als 'passphrase.txt' op de beheerserver. Voer de volgende opdrachten. Het IP-adres van de management-server is 104.40.75.37 en de HTTPS-poort is 443 in ons voorbeeld:

Installeren op een productieserver:

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt

Installeren op een hoofddoelserver:

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt


## <a name="step-10-enable-protection-for-a-machine"></a>Stap 10: Beveiliging voor een machine inschakelen
Als beveiliging wilt inschakelen, virtuele machines en fysieke servers aan een beveiligingsgroep toevoegen. Voordat u begint, Let op het volgende als u virtuele VMware-machines beveiligt:

* Virtuele VMware-machines om de 15 minuten worden gedetecteerd, en het kan meer dan 15 minuten duren voordat ze worden weergegeven in de Site Recovery-portal na de detectie.
* Omgevingswijzigingen op de virtuele machine (zoals VMware tools-installatie) mogelijk ook rekening houden met meer dan 15 minuten worden bijgewerkt in Site Recovery.
* U kunt de laatste keer dat gedetecteerde controleren op virtuele VMware-machines in de **laatste Contact op** veld voor de vCenter-server/ESXi-host op de **configuratieservers** tabblad.
* Als u een vCenter-Server of ESXi-host na het maken van een beveiligingsgroep toevoegt, duurt het mogelijk meer dan 15 minuten voor de Azure Site Recovery-portal om te vernieuwen en voor virtuele machines te worden vermeld in de **machines toevoegen aan een beveiligingsgroep** in het dialoogvenster.
* Als u wilt onmiddellijk en machines toevoegen aan een beveiligingsgroep zonder te wachten op de geplande detectie, markeer de configuratieserver (Klik niet op deze) en klik op **vernieuwen**.

Daarnaast doet u het volgende:

* Het is raadzaam om uw beveiligingsgroepen te bouwen, zodat ze uw werkbelastingen. Bijvoorbeeld, machines met een specifieke toepassing tot dezelfde groep toevoegen.
* Wanneer u computers aan een beveiligingsgroep toevoegt, wordt de processerver automatisch pushes en installeert de Mobility-service als dit niet is gebeurd. U moet de push-mechanisme voorbereid, zoals beschreven in de vorige stap.

### <a name="add-machines-to-a-protection-group"></a>Machines toevoegen aan een beveiligingsgroep

1. Ga naar **beveiligde Items** > **beveiligingsgroep** > **Machines** > **Machines toevoegen**.
2. Als u virtuele VMware-machines, beveiligt **virtuele Machines selecteren**, selecteert u een vCenter-server die wordt beheerd door uw virtuele machines (of de EXSi host waarop ze uitvoert) en selecteer vervolgens de machines.

    ![Schakel de beveiliging voor virtuele machines](./media/site-recovery-vmware-to-azure-classic/enable-protection2.png)
3. Als u fysieke servers beveiligt **virtuele Machines selecteren**, open de **fysieke Machines toevoegen** wizard en geef de IP-adres en de beschrijvende naam. Selecteer vervolgens de besturingssysteemgroep.

   ![Schakel de beveiliging voor fysieke servers](./media/site-recovery-vmware-to-azure-classic/enable-protection1.png)
4. In **Doelresources opgeven**, selecteer het opslagaccount dat u voor replicatie gebruikt en selecteert u of de instellingen moeten worden gebruikt voor alle werkbelastingen. Premium-opslagaccounts worden momenteel niet ondersteund.

   > [!NOTE]
   > We bieden geen ondersteuning voor bewegende opslagaccounts die zijn gemaakt met behulp van de [Azure-portal](../storage/storage-create-storage-account.md) over resourcegroepen.                           
   > [Migratie van opslagaccounts](../azure-resource-manager/resource-group-move-resources.md) in resourcegroepen binnen hetzelfde abonnement of tussen abonnementen wordt niet ondersteund voor opslagaccounts die worden gebruikt voor het implementeren van Site Recovery.
   >
   >

    ![Doelinstellingen configureren](./media/site-recovery-vmware-to-azure-classic/enable-protection3.png)
5. In **Accounts opgeven**, selecteert u het account dat u [instellen](#install-the-mobility-service-with-push-installation) moet worden gebruikt voor automatische installatie van de Mobility-service.

    ![Accounts opgeven](./media/site-recovery-vmware-to-azure-classic/enable-protection4.png)
6. Klik op het vinkje om te voltooien machines toe te voegen aan de beveiligingsgroep en initiële replicatie voor elke computer te starten.

   > [!NOTE]
   > Als u push-installatie is voorbereid, wordt de Mobility-service automatisch geïnstalleerd op computers die niet hebt wanneer deze wordt toegevoegd aan de beveiligingsgroep. Nadat de service is geïnstalleerd, wordt een beveiligingstaak wordt gestart en is mislukt. Na de fout moet u handmatig opnieuw op elke computer waarop eerder de Mobility-service geïnstalleerd. Na het opnieuw opstarten wordt de beveiligingstaak opnieuw begint en initiële replicatie plaatsvindt.
   >
   >

U kunt de status controleren op de **taken** pagina.

![Status op de pagina taken controleren](./media/site-recovery-vmware-to-azure-classic/enable-protection5.png)

Beveiligingsstatus kan ook worden bewaakt in **beveiligde Items** > *naam beveiligingsgroep* > **virtuele Machines**. Nadat de eerste replicatie is voltooid en gegevens worden gesynchroniseerd, machine-status gewijzigd in **beveiligde**.

![Status van de monitor in beveiligde Items](./media/site-recovery-vmware-to-azure-classic/enable-protection6.png)

## <a name="step-11-set-protected-machine-properties"></a>Stap 11: Beveiligde computereigenschappen
1. Nadat een machine heeft een **beveiligde** status, kunt u de failover-eigenschappen configureren. In de gegevens van de beveiliging, selecteer de computer en open de **configureren** tabblad.
2. Site Recovery automatisch wordt voorgesteld eigenschappen voor de virtuele machine van Azure en detecteert dat de on-premises netwerk-instellingen.

    ![Eigenschappen van de virtuele machine instellen](./media/site-recovery-vmware-to-azure-classic/vm-properties1.png)
3. U kunt deze instellingen wijzigen:

   * **Naam van de Azure VM**: dit is de naam die na een failover zal worden gegeven aan de machine in Azure. De naam moet voldoen aan de Azure-vereisten.
   * **Azure VM-grootte**: het aantal netwerkadapters wordt bepaald door de grootte dat u voor de virtuele doelmachine opgeeft. Zie voor meer informatie over grootten en netwerkadapters, de [tabellen grootte](../virtual-machines/linux/sizes.md). Opmerking:

     * Wanneer u de grootte van een virtuele machine wijzigen en de instellingen opslaan, het aantal netwerkadapters wordt gewijzigd wanneer u opent de **configureren** tabblad van de volgende keer. Het minimum aantal netwerkadapters op de virtuele doelmachines is gelijk aan het minimum aantal netwerkadapters op een virtuele bronmachine. Het maximum aantal netwerkadapters wordt bepaald door de grootte van de virtuele machine.
       * Als het aantal netwerkadapters op de bronmachine kleiner dan of gelijk zijn aan het aantal adapters dat is toegestaan voor de grootte van de doelmachine is, wordt het doel hetzelfde aantal adapters hebben als de bron.
       * Als het aantal adapters voor de virtuele bronmachine groter is dan het aantal dat is toegestaan voor de doelgrootte, wordt het maximum wordt gebruikt.
        Als een bronmachine bijvoorbeeld twee netwerkadapters heeft en met de grootte van de doelmachine vier netwerkadapters worden ondersteund, heeft de doelcomputer twee adapters. Als de bronmachine twee adapters heeft, maar de ondersteunde doelgrootte slechts één ondersteunt, wordt de doelmachine slechts één adapter hebben.
     * Als de virtuele machine meerdere netwerkadapters heeft, moeten alle netwerkadapters zijn verbonden met hetzelfde Azure-netwerk.
   * **Azure-netwerk**: U moet een Azure-netwerk dat virtuele Azure-machines na een failover naar verbonden opgeven. Als u niet opgeeft, wordt de Azure VM's niet verbonden met een netwerk. Bovendien moet u een Azure-netwerk opgeven als u failback vanuit Azure naar de lokale site wilt. Failback vereist een VPN-verbinding tussen een Azure-netwerk en een on-premises netwerk.
   * **Azure IP-adres/subnet**: Selecteer het subnet waarop de Azure VM verbinding moet maken voor elke netwerkadapter. Houd er rekening mee dat als de netwerkadapter van de bronmachine is geconfigureerd voor het gebruik van een statisch IP-adres, kunt u een statisch IP-adres voor de virtuele machine in Azure. Als u een statisch IP-adres niet opgeeft, wordt een beschikbaar IP-adres worden toegewezen. Als het doel-IP-adres is opgegeven, maar al gebruikt door een andere virtuele machine in Azure wordt, mislukt de failover. Als de netwerkadapter van de bronmachine is geconfigureerd voor gebruik van DHCP, hebt u DHCP als de instelling voor Azure.      

## <a name="step-12-create-a-recovery-plan-and-run-a-failover"></a>Stap 12: Een herstelplan maken en een failover uitvoeren
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failover/player]
>
>

U kunt een failover voor een enkele computer uitvoeren of kunt u meerdere virtuele machines die dezelfde taak uitvoeren of uit te voeren dezelfde werkbelasting failover. Voor meerdere machines failover op hetzelfde moment, toevoegt u ze aan een plan voor herstel.

Een herstelplan maken:

1. Op de **herstelplannen** pagina, klikt u op **herstelplan toevoegen** en toevoegen van een herstelplan. Geef details op voor het abonnement en selecteer **Azure** als doel.

 ![Plan voor herstel configureren](./media/site-recovery-vmware-to-azure-classic/recovery-plan1.png)
2. In **virtuele Machine selecteren**, selecteert u een beveiligingsgroep en selecteer vervolgens de machines in de groep toevoegen aan het herstelplan.

 ![Virtuele machines toevoegen](./media/site-recovery-vmware-to-azure-classic/recovery-plan2.png)

U kunt het plan voor het maken van groepen en volgorde de volgorde waarin machines in het herstelplan wordt een failover uitgevoerd. U kunt ook scripts en wordt u gevraagd om de handmatige acties toevoegen. Scripts kunnen worden gemaakt, handmatig of via [Azure Automation-Runbooks](site-recovery-runbook-automation.md). Zie voor meer informatie over het aanpassen van herstelplannen [herstelplannen maken](site-recovery-create-recovery-plans.md).

## <a name="run-a-failover"></a>Een failover uitvoeren
Voordat u een failover uitvoert:

* Zorg ervoor dat de beheerserver uitgevoerd en beschikbaar wordt. Als dit niet het geval is, mislukt de failover.
* Als u een niet-geplande failover uitvoert:

  * Schakel primaire machines zo mogelijk uit voordat u een ongeplande failover uitvoert. Zo zorgt u ervoor dat niet tegelijkertijd zowel de bronmachines als de gerepliceerde machines worden uitgevoerd. Als u virtuele VMware-machines repliceert wanneer u een niet-geplande failover uitvoert, kunt u opgeven dat Site Recovery proberen moet de bronmachines afgesloten. Afhankelijk van de status van de primaire site, mogelijk of werkt mogelijk niet. Als u fysieke servers repliceert, kan Site Recovery niet met deze optie biedt.
  * Een niet-geplande failover stopt gerepliceerd van primaire machines, zodat eventuele verschillen gegevens won't worden overgedragen nadat een ongeplande failover is gestart.
  * Als u verbinding maken met de replica virtuele machine in Azure na een failover wilt, moet u verbinding met extern bureaublad inschakelen op de bronmachine voordat u de failover uitvoert. Vervolgens kunt u RDP-verbinding via de firewall. U moet ook RDP toestaan op het openbare-eindpunt van de Azure virtuele machine na een failover. Ga als volgt [aanbevolen procedures](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) om ervoor te zorgen dat RDP na een failover werkt.

> [!NOTE]
> Als u de beste prestaties als u een failover naar Azure doet, zorg ervoor dat u de Azure-Agent hebt geïnstalleerd op de beveiligde machine. Dit helpt het opstarten van de machine sneller en helpt bij het vaststellen van problemen. De Azure-Agent is beschikbaar voor [Linux](https://github.com/Azure/WALinuxAgent) en [Windows](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

### <a name="run-a-test-failover"></a>Een testfailover uitvoeren
Een testfailover als u wilt uw failover simuleren uitvoeren en herstelprocessen in een geïsoleerd netwerk dat niet van invloed op uw productieomgeving en kunt normale replicatie normaal gaan. Testfailover initiatd op de bron is en kunt u deze in een aantal manieren uitvoeren:

* **Een Azure-netwerk niet opgeeft**: als u een testfailover zonder een netwerk uitvoert, controleert de test dat virtuele machines starten en goed worden weergegeven in Azure. Virtuele machines niet verbonden met een Azure-netwerk na een failover.
* **Geef een Azure-netwerk**: dit type failover controleert of de volledige replicatieomgeving naar verwachting en dat de virtuele machines in Azure met het opgegeven netwerk verbonden bent.

Een testfailover uitvoeren:

1. Op de **herstelplannen** pagina, selecteer het plan en klik op **Testfailover**.

 ![Selecteer het plan](./media/site-recovery-vmware-to-azure-classic/test-failover1.png)
2. In **Testfailover bevestigen**, selecteer **geen** om aan te geven dat u niet wilt gebruiken van een Azure-netwerk voor de testfailover of Selecteer het netwerk waarmee de test-virtuele machines na een failover worden verbonden. Klik op het vinkje om de failover start.

 ![Maak een keuze](./media/site-recovery-vmware-to-azure-classic/test-failover2.png)
3. Voortgang van failover op de **taken** tabblad.

 ![Voortgang van de monitor](./media/site-recovery-vmware-to-azure-classic/test-failover3.png)
4. Nadat de failover is voltooid, kunt u moet ook de gerepliceerde Azure Zie machine worden weergegeven in **virtuele Machines** in de Azure portal. Als u een RDP-verbinding naar de Azure VM starten wilt, moet u poort 3389 op de VM-eindpunt te openen.
5. Nadat u hebt voltooid, wanneer failover bereikt de **Complete** testfase, klikt u op **volledige Test** te voltooien. In **notities**, vastleggen en opslaan van eventuele opmerkingen die zijn gekoppeld aan de testfailover.
6. Klik op **de testfailover is voltooid** automatisch opschonen van de testomgeving. Nadat dit is gebeurd, de testfailover wordt weergegeven een **Complete** status. Alle elementen of virtuele machines automatisch gemaakt tijdens de testfailover worden verwijderd. Als u een testfailover langer dan twee weken duurt, is het geforceerd te voltooien.

### <a name="run-an-unplanned-failover"></a>Een niet-geplande failover uitvoeren
Niet-geplande failover van Azure wordt gestart en kan worden uitgevoerd, zelfs als de primaire site niet beschikbaar.

1. Op de **herstelplannen** pagina, selecteer het plan en klik op **Failover** > **niet-geplande Failover**.

 ![Selecteer het plan](./media/site-recovery-vmware-to-azure-classic/unplanned-failover1.png)
2. Als u virtuele VMware-machines repliceert, kunt u proberen de lokale virtuele machines af te sluiten. Dit is een actie best-effort en failover blijft of de moeite of niet lukt. Als dit niet lukt, details van fouten wordt weergegeven op de **taken** tabblad onder **niet-geplande Failover taken**.

 ![Optie voor lokale virtuele machines afsluiten](./media/site-recovery-vmware-to-azure-classic/unplanned-failover2.png)

 > [!NOTE]
 > Deze optie niet beschikbaar als u fysieke servers repliceert. U moet probeert af te sluiten die handmatig, indien mogelijk.
 >
 >

3. In **bevestigen Failover**, controleert u de failoverrichting (naar Azure) en selecteer het herstelpunt dat u wilt gebruiken voor de failover. Als u meerdere VM ingeschakeld wanneer u replicatie-eigenschappen hebt geconfigureerd, kunt u herstellen naar de meest recente herstelpunt voor een toepassing of crashconsistent. U kunt ook selecteren **aangepaste herstelpunt** naar een eerder tijdstip herstellen. Klik op het vinkje om de failover start.

 ![Failoverrichting bevestigen](./media/site-recovery-vmware-to-azure-classic/unplanned-failover3.png)
4. Wacht totdat de taak niet-geplande failover is voltooid. U kunt voortgang failover op de **taken** tabblad. Zelfs als er fouten optreden tijdens de niet-geplande failover het herstelplan wordt uitgevoerd totdat deze voltooid is. U moet ook de gerepliceerde Azure Zie machine worden weergegeven in **virtuele Machines** in de Azure portal.

### <a name="connect-to-replicated-azure-virtual-machines-after-failover"></a>Verbinding maken met virtuele Azure-machines na een failover gerepliceerd
Voor verbinding met virtuele machines in Azure gerepliceerd na een failover, hebt u het volgende nodig:

- Een extern bureaublad-verbinding is ingeschakeld op de primaire machine.
- Windows Firewall op de primaire machine ingesteld op RDP toestaan.
- RDP toegevoegd aan het openbaar eindpunt voor de virtuele machine van Azure.

Zie voor meer informatie over om in te stellen, [probleemoplossing van extern bureaublad-verbinding na een failover met ASR](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

## <a name="deploy-additional-process-servers"></a>Aanvullende processen servers implementeren
Als u uw implementatie dan 200 bronmachines moet uitbreiden of als de totale dagelijkse verloop groter is dan 2 TB, moet u extra processervers voor de verwerking van het netwerkverkeer. Als u een extra processerver instelt, Controleer u de vereisten in [extra processervers](#additional-process-servers), en stel de processerver volgens de volgende instructies. Nadat u de server hebt ingesteld, kunt u bronmachines om dit te gebruiken.

### <a name="set-up-an-additional-process-server"></a>Een extra processerver instellen
Een extra processerver instellen als volgt:

* De uniforme wizard voor een beheerserver configureren als een processerver uitvoeren.
* Als u repliceren wilt met behulp van de nieuwe processerver beheren, moet u uw beveiligde machines migreren.

### <a name="install-the-process-server"></a>De processerver installeren
1. Op de **Quick Start** pagina, downloaden van het geïntegreerde installatiebestand voor de installatie van de Site Recovery-componenten. Voer de installatie.
2. In **Voordat u begint** selecteert u **Add additional process servers to scale out deployment** (Extra processervers toevoegen om implementatie uit te schalen).

 ![Processerver toevoegen](./media/site-recovery-vmware-to-azure-classic/add-ps1.png)
3. Voltooi de wizard net als wanneer u [instellen](#step-5-install-the-management-server) de eerste beheerserver.
4. In **Server configuratiedetails**, geef het IP-adres van de oorspronkelijke beheerserver waarop u de configuratieserver hebt geïnstalleerd en voer vervolgens de wachtwoordzin. Als u de wachtwoordzin niet hebt, voert u  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** op de oorspronkelijke management server op te halen.

 ![Configuratiedetails van server](./media/site-recovery-vmware-to-azure-classic/add-ps2.png)

### <a name="migrate-machines-to-use-the-new-process-server"></a>Machines voor het gebruik van de nieuwe processerver migreren
1. Open **configuratieservers** > **Server** > *naam van de oorspronkelijke beheerserver* > **Serverdetails**.

 ![Details van server](./media/site-recovery-vmware-to-azure-classic/update-process-server1.png)
2. In de **processervers** selecteert **processerver wijzigen** naast de server die u wilt wijzigen.

 ![De processerver bijwerken](./media/site-recovery-vmware-to-azure-classic/update-process-server2.png)
3. Selecteer **processerver wijzigen**, selecteer **proces doelserver**, en selecteer vervolgens de nieuwe beheerserver. Selecteer vervolgens de virtuele machines die de nieuwe processerver wordt afgehandeld. Klik op het informatiepictogram voor informatie over de server. De gemiddelde ruimte die nodig is om elke geselecteerde virtuele machine worden gerepliceerd naar de nieuwe processerver wordt te maken met het laden van de beslissingen die weergegeven. Klik op het vinkje om te repliceren naar de nieuwe processerver.

 ![De processerver wijzigen](./media/site-recovery-vmware-to-azure-classic/update-process-server3.png)

## <a name="vmware-permissions-for-vcenter-access"></a>VMware-machtigingen voor de vCenter-toegang
De processerver kan automatisch detecteren voor virtuele machines op een vCenter-server. Voor automatische detectie, moet u voor het definiëren van een rol (Azure_Site_Recovery) op het niveau van de vCenter om toe te staan van Site Recovery voor toegang tot de vCenter-server. Als u alleen hoeft voor VMware-machines migreren naar Azure en geen failback vanuit Azure wilt, kunt u een alleen-lezen-rol die is voldoende. De machtigingen instellen, zoals beschreven in [stap 6: instellen van referenties voor de vCenter-server](#step-6-set-up-credentials-for-the-vcenter-server). De rolmachtigingen worden samengevat in de volgende tabel:

| **Rol** | **Details** | **Machtigingen** |
| --- | --- | --- |
| Azure_Site_Recovery rol |Detectie van VMware VM |Deze rechten voor de v Center-server toewijzen:<br/><br/>Gegevensopslag: Toewijzen van ruimte, bladeren gegevensopslag, bestandsbewerkingen op laag niveau, bestand, updatebestanden voor de virtuele machine verwijderen<br/><br/>Netwerk: Netwerk toewijzen<br/><br/>Bron: Virtuele machine toewijzen aan de resourcegroep, migreren van stroom voorzien uitschakelen virtuele machine, migreren ingeschakeld op virtuele machine<br/><br/>Taken: De taak, Update-taak maken<br/><br/>Virtuele machine > configuratie<br/><br/>Virtuele machine > Interact > beantwoorden van vraag, apparaatverbinding, configureer CD's, diskettes configureren, uitschakelen, inschakelen, VMware-hulpprogramma's installeren<br/><br/>Virtuele machine > voorraad > maken, registreren, Unregister<br/><br/>Virtuele machine > inrichten > downloaden van de virtuele machine toestaan, toestaan virtuele machine bestanden uploaden<br/><br/>Virtuele machine > momentopnamen > momentopnamen verwijderen |
| vCenter gebruikersrol |VMware VM detectie/Failover zonder afsluiten van de bron-VM |Deze rechten voor de v Center-server toewijzen:<br/><br/>Data Center object > doorgeven aan het onderliggende Object rol = alleen-lezen <br/><br/>De gebruiker is toegewezen op het niveau van het datacenter en dus toegang heeft tot alle objecten in het datacenter. Als u wilt dat de toegang te beperken, wijst de **geen toegang** rol met de **doorgeven dat onderliggende** -object op voor de onderliggende objecten (ESX-hosts, datastores, VM's en -netwerken). |
| vCenter gebruikersrol |Failover en failback |Deze rechten voor de v Center-server toewijzen:<br/><br/>Datacenter-object doorgeven aan het onderliggende object rol Azure_Site_Recovery =<br/><br/>De gebruiker is toegewezen op niveau van het datacenter en dus toegang heeft tot alle objecten in het datacenter.  Als u wilt dat de toegang te beperken, wijst de ** geen toegang ** rol met de **doorgeven aan het onderliggende object** op het onderliggende object (ESX-hosts, datastores, VM's en -netwerken). |

## <a name="third-party-software-notices-and-information"></a>Software van derden kennisgevingen en informatie
<!--Do Not Translate or Localize-->

De software en firmware die wordt uitgevoerd in de Microsoft-product of de service is gebaseerd op of opgenomen met het materiaal uit de onderstaande projecten (gezamenlijk ' Code van derden').  Microsoft is niet de oorspronkelijke auteur van de Code van derden.  Het oorspronkelijke copyrightinformatie en de licentie, waaronder Microsoft deze Code van derden ontvangen worden die hieronder ingesteld.

De informatie in een sectie betrekking heeft op de Code van derden onderdelen uit de onderstaande projecten. Deze licenties en informatie vindt u dient alleen ter informatie.  Deze Code van derden is aan u wordt relicensed door Microsoft onder de licentievoorwaarden voor Microsoft software voor de Microsoft-product of service.  

De informatie in de sectie B betrekking heeft op de Code van derden-onderdelen die worden beschikbaar gesteld aan u door Microsoft onder de oorspronkelijke licentievoorwaarden.

Het volledige bestand kan worden gevonden op de [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft behoudt alle rechten die in deze overeenkomst niet uitdrukkelijk zijn verleend, hetzij bij implicatie volgens of anderszins.

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over failback](site-recovery-failback-azure-to-vmware-classic.md) brengt uw failover-machines worden uitgevoerd in Azure weer naar uw on-premises omgeving.
