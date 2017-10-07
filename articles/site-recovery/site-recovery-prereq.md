---
title: aaaPrerequisites voor replicatie tooAzure met behulp van Azure Site Recovery | Microsoft Docs
description: Meer informatie over het Hallo-vereisten voor het repliceren van virtuele machines en fysieke machines tooAzure met hello Azure Site Recovery-service.
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: rajanaki
ms.openlocfilehash: 0e32ab7cd7c65a3f67ffa2f2c15af189c15b6f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replication-from-on-premises-tooazure-by-using-site-recovery"></a>Vereisten voor replicatie van lokale tooAzure met behulp van Site Recovery

> [!div class="op_single_selector"]
> * [Repliceren vanaf Azure tooAzure](site-recovery-azure-to-azure-prereq.md)
> * [Repliceren vanaf de lokale tooAzure](site-recovery-prereq.md)

Azure Site Recovery kunt u ondersteuning van uw strategie voor zakelijke continuïteit en noodherstel herstel (BCDR) door replicatie van een virtuele Azure-machine (VM) tooanother Azure-regio te organiseren. Site Recovery repliceert ook fysieke on-premises servers en virtuele machines toohello cloud (Azure) of tooa secundair datacenter. Als er een storing optreedt op uw primaire locatie, kunt u failover-overschakeling tooa secundaire locatie tookeep toepassingen en workloads beschikbaar. U kunt back tooyour primaire locatie mislukken wanneer de primaire locatie Hallo toonormal bewerkingen retourneert. Zie voor meer informatie over Site Recovery [wat is Site Recovery?](site-recovery-overview.md).

In dit artikel samenvatten we Hallo-vereisten voor de Site Recovery de replicatie van een lokale machine tooAzure begint.

U kunt eventuele opmerkingen onder Hallo van Hallo artikel boeken. Kunt u ook technische vragen in Hallo vragen [Azure Recovery Services-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="azure-requirements"></a>Azure-vereisten

**Vereiste** | **Details**
--- | ---
**Azure-account** | Een [Microsoft Azure-account](http://azure.microsoft.com/). U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).
**Site Recovery-service** | Zie voor meer informatie over prijzen voor Azure Site Recovery-service Hallo [prijzen voor Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). |
**Azure Storage** | U moet een Azure Storage-account toostore gerepliceerde gegevens. Hallo storage-account moet zich in Hallo dezelfde regio bevinden als hello Azure Recovery Services-kluis. Virtuele machines in Azure worden gemaakt wanneer failover plaatsvindt.<br/><br/> Afhankelijk van het resourcemodel Hallo gewenste toouse voor Azure VM-failover, kunt u een account instellen met behulp van Hallo [Azure Resource Manager-implementatiemodel](../storage/common/storage-create-storage-account.md) of Hallo [klassieke implementatiemodel](../storage/common/storage-create-storage-account.md).<br/><br/>U kunt [geografisch redundante opslag](../storage/common/storage-redundancy.md#geo-redundant-storage) of lokaal redundante opslag gebruiken. Wij raden geografisch redundante opslag aan. Met geografisch redundante opslag is gegevens tegen als een regionale uitval of als de primaire regio Hallo kan niet worden hersteld.<br/><br/> U kunt een standaard Azure-opslagaccount gebruiken of kunt u Azure Premium-opslag. [Premium-opslag](https://docs.microsoft.com/azure/storage/storage-premium-storage) wordt meestal gebruikt voor virtuele machines die u een consistent hoge i/o-prestaties en lage latentie moeten. Een virtuele machine kunt I/O-intensieve werkbelastingen hosten met premium-opslag. Als u Premium Storage gebruikt voor gerepliceerde gegevens, hebt u ook een standaardopslagaccount nodig. Standard-opslagaccount slaat replicatielogboeken die de doorlopende wijzigingen tooon-premises gegevens vastleggen.<br/><br/>
**Beperkingen voor opslag** | Storage-accounts die u in Site Recovery tooa andere resourcegroep gebruikt verplaatsen, of is niet verplaatsen tooor gebruik met een ander abonnement.<br/><br/> Op dit moment toopremium storage-accounts in Centraal, India en India Zuid repliceren is niet beschikbaar.
**Azure-netwerk** | U hebt een Azure-netwerk, toowhich virtuele Azure-machines verbinding maken na een failover. Hello Azure-netwerk moet Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis.<br/><br/> In hello Azure-portal, kunt u een Azure-netwerk maken met behulp van Hallo [Resource Manager-implementatiemodel](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) of Hallo [klassieke implementatiemodel](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).<br/><br/> Als u van System Center Virtual Machine Manager (VMM) tooAzure repliceert, moet u netwerktoewijzing tussen VMM VM-netwerken en Azure-netwerken instellen. Dit zorgt ervoor dat de virtuele Azure-machines verbinding tooappropriate netwerken na een failover maken.
**Beperkingen op het netwerk** | U kan de netwerkaccounts die u in Site Recovery tooa andere resourcegroep gebruikt verplaatsen of verplaatsen tooor gebruik met een ander abonnement.
**Netwerktoewijzing** | Als u Microsoft Hyper-V-machines in VMM-clouds repliceren, moet u netwerktoewijzing instellen. Dit zorgt ervoor dat tooappropriate netwerken in Azure Virtual machines verbinding maken wanneer ze zijn gemaakt na een failover.

> [!NOTE]
> Hallo beschrijven volgende secties Hallo-vereisten voor de verschillende onderdelen van Hallo klant-omgeving. Zie voor meer informatie over ondersteuning voor specifieke configuraties Hallo [ondersteuningsmatrix](site-recovery-support-matrix.md).
>

## <a name="disaster-recovery-of-vmware-vms-or-physical-windows-or-linux-servers-tooazure"></a>Herstel na noodgevallen van virtuele VMware-machines of fysieke tooAzure voor Windows of Linux-servers
Hallo volgende onderdelen zijn vereist voor herstel na noodgevallen van virtuele VMware-machines of fysieke Windows of Linux-servers. Dit zijn bovendien toohello zijn beschreven in [Azure-vereisten](#azure-requirements).


### <a name="configuration-server-or-additional-process-server"></a>Configuratieserver of extra processerver

Een lokale machine instellen als Hallo configuratie tooorchestrate servercommunicatie tussen Hallo on-premises site en Azure. Hallo lokale machine beheert ook gegevensreplicatie. <br/></br>

*   **VMware vCenter of vSphere host-vereisten**

    | **Onderdeel** | **Vereisten** |
    | --- | --- |
    | **vSphere** | U moet een of meer VMware vSphere hypervisors hebben.<br/><br/>Hypervisors moet worden uitgevoerd vSphere versie 6.0, 5.5 of 5.1 Hello meest recente updates.<br/><br/>We raden aan dat vSphere-hosts en vCenter-servers in Hallo zijn netwerk als processerver Hallo. Tenzij u een speciale processerver hebt ingesteld, is dit Hallo-netwerk waarin Hallo configuratieserver zich bevindt. |
    | **vCenter** | Het is raadzaam dat u een VMware vCenter server toomanage uw vSphere-hosts implementeert. Worden moet het vCenter versie 6.0 of 5.5, met de nieuwste updates Hallo uitgevoerd.<br/><br/>**Beperking**: Site Recovery biedt geen ondersteuning voor replicatie tussen de exemplaren van vCenter vMotion. DRS-opslag- en Storage vMotion worden ook niet ondersteund op een hoofddoel VM nadat een beveiligt.||

* **Vereisten voor gerepliceerde machines**

    | **Onderdeel** | **Vereisten** |
    | --- | --- |
    | **Lokale machines** (VMware-machines) | Gerepliceerde virtuele machines moet VMware tools geïnstalleerd en uitgevoerd.<br/><br/> Virtuele machines moeten voldoen aan [vereisten voor Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) voor het maken van een virtuele machine in Azure.<br/><br/>Schijfcapaciteit op elke beveiligde computer niet meer dan 1023 GB. <br/><br/>Een minimaal 2 GB aan beschikbare ruimte op het Hallo-installatiestation is vereist voor de installatie van onderdelen.<br/><br/>Als u meerdere VM-consistentie tooenable wilt, moet poort 20004 worden geopend op Hallo VM lokale firewall.<br/><br/>Namen voor machines moeten liggen tussen 1 en maximaal 63 tekens bevatten (u kunt gebruiken letters, cijfers en afbreekstreepjes). Hallo-naam moet beginnen met een letter of cijfer en eindigen met een letter of cijfer. <br/><br/>Nadat u replicatie voor een machine hebt ingeschakeld, kunt u hello Azure naam wijzigen.<br/><br/> |
    | **Windows-machines** (fysieke of VMware) | Hallo machine moet worden uitgevoerd Hallo volgende ondersteund 64-bits besturingssystemen: <br/>-Windows Server 2012 R2<br/>-Windows Server 2012<br/>-Windows Server 2008 R2 met SP1 of hoger<br/><br/> Hallo besturingssysteem moet worden geïnstalleerd op station C. Hallo OS-schijf moet een standaardschijf zijn Windows, en niet als dynamische. Hallo gegevensschijf kan niet dynamisch zijn.<br/><br/>|
    | **Linux-machines** (fysieke of VMware) | Hallo machine moet worden uitgevoerd Hallo volgende ondersteund 64-bits besturingssystemen: <br/>-Red Hat Enterprise Linux 7.2, 7.1, 6,8 of 6.7<br/>-Centos 7.2, 7.1, 7.0, 6,8, 6.7, 6.6 of 6.5<br/>-Server Ubuntu 14.04 TNS (Zie voor een lijst van ondersteunde kernel-versies voor Ubuntu [ondersteunde besturingssystemen](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions))<br/>-Oracle compatibel is met Enterprise Linux 6.5 of 6.4, uitvoeren van beide Hallo Red Hat kernel of Unbreakable Enterprise Kernel versie 3 (UEK3)<br/>-SUSE Linux Enterprise Server 11 SP4 of SUSE Linux Enterprise Server 11 SP3<br/><br/>Uw bestanden/etc/hosts op beveiligde machines moeten vermeldingen die zijn toegewezen Hallo lokale host naam tooIP adressen die zijn gekoppeld aan alle netwerkadapters hebben.<br/><br/>Na een failover als u wilt tooconnect tooan virtuele Azure-machine waarop Linux wordt uitgevoerd met behulp van een client Secure Shell (SSH), zorg ervoor dat Hallo SSH-service op Hallo beveiligde computer is ingesteld toostart automatisch op opstarten van het systeem. Zorg ook dat firewall-regels toestaan dat een SSH-verbinding toohello beveiligde virtuele machine.<br/><br/>Hallo-hostnaam, koppelpunten, apparaat, en Linux systeempaden en bestandsnamen (bijvoorbeeld /etc/ bevinden en /usr) moeten alleen in het Engels zijn.<br/><br/>Hallo volgende mappen (als ingesteld als afzonderlijke partities of -bestandssystemen) moet zijn op Hallo dezelfde schijf (schijf Hallo OS) op de bronserver Hallo:<br/>- / (root)<br/>- / opstarten<br/>-/usr<br/>-/ usr/lokaal<br/>-/var<br/>- / enzovoort<br/><br/>XFS v5 functies, zoals metagegevens controlesom, worden momenteel niet ondersteund door Site Recovery op XFS-bestandssystemen. Zorg ervoor dat uw bestandssystemen XFS eventuele v5-functies niet gebruiken. U kunt Hallo xfs_info hulpprogramma toocheck hello XFS superblock voor Hallo partitie gebruiken. Als **ftype** te is ingesteld,**1**, XFS v5 functies worden gebruikt.<br/><br/>Hallo lsof hulpprogramma moet op Red Hat Enterprise Linux 7 en CentOS 7-servers zijn geïnstalleerd en beschikbaar.<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-tooazure-no-vmm"></a>Herstel na noodgevallen van Hyper-V-machines tooAzure (niets VMM)

Hallo volgende onderdelen zijn vereist voor herstel na noodgevallen van Hyper-V-machines in VMM-clouds. Dit zijn bovendien toohello zijn beschreven in [Azure-vereisten](#azure-requirements).

| **Vereiste** | **Details** |
| --- | --- |
| **Hyper-V-host** |Een of meer lokale servers moeten Windows Server 2012 R2 worden uitgevoerd met de meest recente updates Hallo en Hallo Hyper-V-functie is ingeschakeld of Microsoft Hyper-V Server 2012 R2.<br/><br/>Hyper-V-servers moeten een of meer virtuele machines hebben.<br/><br/>Hyper-V-servers zijn verbonden toohello Internet, rechtstreeks of via een proxyserver.<br/><br/>Hyper-V-servers moeten beschikken over Hallo oplossingen beschreven in Knowledge Base-artikel Hallo [2961977](https://support.microsoft.com/kb/2961977) geïnstalleerd.
|**Provider en agent**| Tijdens de implementatie van Site Recovery kunt u hello Azure Site Recovery provider installeren. installatie van de provider Hallo ook hello Azure Recovery Services-agent geïnstalleerd op elke Hyper-V-server met virtuele machines die u wilt dat tooprotect. <br/><br/>Alle Hyper-V-servers in een kluis moet hebben siteherstel Hallo dezelfde versie van de provider Hallo en Hallo-agent.<br/><br/>Hallo-provider moet tooconnect tooSite herstel via Hallo Internet. Verkeer kan worden verzonden, rechtstreeks of via een proxy. HTTPS gebaseerde proxy wordt niet ondersteund. Hallo-proxyserver moet toegang toohello volgende URL's toestaan:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/>Als u IP-adressen gebaseerde firewallregels op Hallo-server hebt, zorg ervoor dat Hallo regels communicatie tooAzure toestaan.<br/><br/> Hallo toestaan [Azure datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653),- en HTTPS (poort 443).<br/><br/> IP-adresbereiken voor hello Azure-regio van uw abonnement en voor Hallo westen van de VS (gebruikt voor beheer en de identiteit van toegangsbeheer) toestaan.


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooazure"></a>Herstel na noodgevallen van Hyper-V-machines in VMM-clouds tooAzure

Hallo volgende onderdelen zijn vereist voor herstel na noodgevallen van Hyper-V-machines in VMM-clouds. Dit zijn bovendien toohello zijn beschreven in [Azure-vereisten](#azure-requirements).

| **Vereiste** | **Details** |
| --- | --- |
| **Virtual Machine Manager** |U moet een of meer VMM-servers met System Center 2012 R2 of hoger hebben. Elke VMM-server moet een of meer clouds zijn geconfigureerd. <br/><br/>Een cloud moet hebben:<br/>-Een of meer VMM-hostgroepen.<br/>-Een of meer Hyper-V-hostservers of -clusters in elke hostgroep.<br/><br/>Zie voor meer informatie over het instellen van VMM-clouds [hoe toocreate een cloud in Virtual Machine Manager 2012](http://social.technet.microsoft.com/wiki/contents/articles/2729.how-to-create-a-cloud-in-vmm-2012.aspx). |
| **Hyper-V** |Hyper-V-hostservers moeten ten minste draaien op Windows Server 2012 R2 met Hallo Hyper-V-functie ingeschakeld of Microsoft Hyper-V Server 2012 R2. de meest recente updates Hallo moeten worden geïnstalleerd.<br/><br/> Een Hyper-V-server moet een of meer virtuele machines hebben.<br/><br/> Een Hyper-V-hostserver of het cluster met virtuele machines die u wilt dat tooreplicate moet worden beheerd in een VMM-cloud.<br/><br/>Hyper-V-servers zijn verbonden toohello Internet, rechtstreeks of via een proxyserver.<br/><br/>Hyper-V-servers moeten beschikken over Hallo oplossingen beschreven in Knowledge Base-artikel Hallo [2961977](https://support.microsoft.com/kb/2961977) geïnstalleerd.<br/><br/>Hyper-V-hostservers moeten toegang tot Internet voor gegevens replicatie tooAzure. |
| **Provider en agent** |Installeer de Azure Site Recovery Provider op Hallo VMM-server tijdens de implementatie van Azure Site Recovery. Recovery Services-Agent installeren op Hyper-V-hosts. Hallo-provider en agent tooconnect tooAzure rechtstreeks via Internet Hallo of nodig via een proxy. Op HTTPS gebaseerde proxy wordt niet ondersteund. Hallo-proxyserver op Hallo VMM-server en Hyper-V-hosts moet toegang tot toestaan: <br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>Als u IP-adressen gebaseerde firewallregels op Hallo VMM-server hebt, zorg ervoor dat Hallo regels communicatie tooAzure toestaan.<br/><br/> Hallo toestaan [Azure datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653) - en HTTPS (poort 443).<br/><br/>IP-adresbereiken voor hello Azure-regio voor uw abonnement en voor Hallo westen van de VS (gebruikt voor beheer en de identiteit van toegangsbeheer) toestaan.<br/><br/> |

### <a name="replicated-machine-prerequisites"></a>Vereisten voor gerepliceerde machines

| **Onderdeel** | **Details** |
| --- | --- |
| **Beveiligde virtuele machines** | Ondersteunt alle besturingssystemen die worden ondersteund door site Recovery [Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx).<br/><br/>Virtuele machines moeten voldoen aan Hallo [vereisten voor Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) voor het maken van een virtuele machine in Azure. Namen voor machines moeten liggen tussen 1 en maximaal 63 tekens bevatten (u kunt gebruiken letters, cijfers en afbreekstreepjes). Hallo-naam moet beginnen met een letter of cijfer en eindigen met een letter of cijfer. <br/><br/>Nadat u replicatie voor Hallo VM hebt ingeschakeld, kunt u de naam van de VM Hallo wijzigen. <br/><br/> Schijfcapaciteit voor elke beveiligde computer niet meer dan 1023 GB. Een virtuele machine kan hebben up too16-schijven (omhoog too16 TB).<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooa-customer-owned-site"></a>Herstel na noodgevallen van Hyper-V-machines in VMM-clouds tooa klant die eigendom zijn van site

Hallo volgende onderdelen zijn vereist voor herstel na noodgevallen van Hyper-V-machines in VMM-clouds tooa klant die eigendom zijn van site. Dit zijn bovendien toohello zijn beschreven in [Azure-vereisten](#azure-requirements).

| **Onderdeel** | **Details** |
| --- | --- |
| **Virtual Machine Manager** |  Het is raadzaam dat u een VMM-server op Hallo primaire site en de secundaire site Hallo implementeert.<br/><br/> U kunt [repliceren tussen clouds op één VMM-server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment). tooreplicate tussen clouds op één VMM-server, moet u ten minste twee clouds die zijn geconfigureerd op Hallo VMM-server.<br/><br/> VMM-servers moeten ten minste draaien op System Center 2012 SP1 met de nieuwste updates Hallo.<br/><br/> Elke VMM-server moet een of meer clouds hebben. Alle clouds moeten Hallo profiel voor Hyper-V-capaciteit hebben. <br/><br/>Clouds moeten een of meer VMM-hostgroepen hebben. Zie voor meer informatie over het instellen van VMM-clouds [voorbereiden voor Azure Site Recovery-implementatie](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric). |
| **Hyper-V** | Hyper-V-servers moeten ten minste draaien op Windows Server 2012 met Hallo Hyper-V-functie ingeschakeld en hebben Hallo nieuwste updates zijn geïnstalleerd.<br/><br/> Een Hyper-V-server moet een of meer virtuele machines hebben.<br/><br/>  Hyper-V-host-servers moeten zich in hostgroepen in Hallo primaire en secundaire VMM-clouds.<br/><br/> Als u op Windows Server 2012 R2 Hyper-V in een cluster uitvoert, raden wij aan dat u Hallo-update die wordt beschreven in Knowledge Base-artikel installeert [2961977](https://support.microsoft.com/kb/2961977).<br/><br/> Als u Hyper-V wordt uitgevoerd in een cluster op Windows Server 2012 en een statische IP-adressen gebaseerde cluster hebt, wordt niet automatisch een clusterbroker gemaakt. U moet Hallo clusterbroker handmatig configureren. Zie voor meer informatie over de clusterbroker hello [configureren Hallo replica broker-functie voor replicatie van cluster naar cluster](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **Provider** | Tijdens de implementatie van Site Recovery hello Azure Site Recovery provider op VMM-servers te installeren. Hallo provider communiceert met Site Recovery via HTTPS (poort 443) tooorchestrate replicatie. Gegevensreplicatie plaatsvindt tussen Hallo primaire en secundaire Hyper-V-servers via Hallo LAN of via een VPN-verbinding.<br/><br/> Hallo-provider die wordt uitgevoerd op Hallo VMM-beheerserver moet toegang tot toohello volgende URL's:<br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>Hallo Site Recovery provider moet de firewall-communicatie van Hallo VMM-servers toohello toestaan [Azure datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653), waardoor Hallo HTTPS (poort 443)-protocol. |


## <a name="url-access"></a>URL-toegang
Deze URL's moeten beschikbaar zijn vanuit VMware, VMM en Hyper-V-hostservers zijn:

|**URL** | **VMM tooVMM** | **VMM tooAzure** | **Hyper-V tooAzure** | **VMware tooAzure** |
|--- | --- | --- | --- | --- |
|``*.accesscontrol.windows.net`` | Toestaan | Toestaan | Toestaan | Toestaan |
|``*.backup.windowsazure.com`` | Niet vereist | Toestaan | Toestaan | Toestaan |
|``*.hypervrecoverymanager.windowsazure.com`` | Toestaan | Toestaan | Toestaan | Toestaan |
|``*.store.core.windows.net`` | Toestaan | Toestaan | Toestaan | Toestaan |
|``*.blob.core.windows.net`` | Niet vereist | Toestaan | Toestaan | Toestaan |
|``https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi`` | Niet vereist | Niet vereist | Niet vereist | Toestaan dat SQL downloaden |
|``time.windows.com`` | Toestaan | Toestaan | Toestaan | Toestaan|
|``time.nist.gov`` | Toestaan | Toestaan | Toestaan | Toestaan |
