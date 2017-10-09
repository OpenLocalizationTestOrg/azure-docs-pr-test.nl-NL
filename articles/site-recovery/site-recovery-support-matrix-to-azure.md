---
title: aaaAzure Site Recovery-ondersteuningsmatrix voor het repliceren van tooAzure | Microsoft Docs
description: Geeft een overzicht van Hallo ondersteunde besturingssystemen en onderdelen voor Azure Site Recovery
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: rajanaki
ms.openlocfilehash: eae1db2ff1392d272f6b2eb0e3410da19d09da7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-on-premises-tooazure"></a>Azure Site Recovery-ondersteuningsmatrix voor het repliceren van lokale tooAzure


In dit artikel bevat een overzicht van ondersteunde configuraties en -onderdelen voor Azure Site Recovery wanneer repliceren en tooAzure herstellen. Zie voor meer informatie over de vereisten voor Azure Site Recovery Hallo [vereisten](site-recovery-prereq.md).


## <a name="support-for-deployment-options"></a>Ondersteuning voor de implementatie-opties

**Implementatie** | **VMware of fysieke server** | **Hyper-V (met/zonder Virtual Machine Manager)** |
--- | --- | ---
**Azure Portal** | Een on-premises virtuele VMware-machines tooAzure opslag, met de Azure Resource Manager of klassieke opslag en netwerken.<br/><br/> Failover tooResource Manager of klassieke VM's. | Een on-premises Hyper-V-machines tooAzure opslag met Resource Manager of klassieke opslag en netwerken.<br/><br/> Failover tooResource Manager of klassieke VM's.
**Klassieke portal** | Onderhoudsmodus bevinden. Nieuwe kluizen kunnen niet worden gemaakt. | Onderhoudsmodus bevinden.
**PowerShell** | Momenteel niet ondersteund. | Ondersteund


## <a name="support-for-datacenter-management-servers"></a>Ondersteuning voor datacenter-beheerservers

### <a name="virtualization-management-entities"></a>Virtualization management-entiteiten

**Implementatie** | **Ondersteuning**
--- | ---
**VMware-virtuele machine of fysieke server** | vCenter 6.5, 6.0 of 5.5
**Hyper-V (met Virtual Machine Manager)** | System Center Virtual Machine Manager 2016 en System Center Virtual Machine Manager 2012 R2

  >[!Note]
  > Een System Center Virtual Machine Manager 2016-cloud met een mengeling van Windows Server 2016 en 2012 R2-hosts wordt momenteel niet ondersteund.

### <a name="host-servers"></a>Host-servers

**Implementatie** | **Ondersteuning**
--- | ---
**VMware-virtuele machine of fysieke server** | vSphere 6.5 6.0, 5.5
**Hyper-V (met/zonder Virtual Machine Manager)** | Windows Server 2016, Windows Server 2012 R2 met de meest recente updates.<br></br>Als SCVMM wordt gebruikt, moeten Windows Server 2016-hosts worden beheerd door SCVMM 2016.


  >[!Note]
  >Een Hyper-V-site die combineert hosts met Windows Server 2016 en 2012 R2 wordt momenteel niet ondersteund. Tooan alternatieve herstellocatie voor virtuele machines op een host met Windows Server 2016 wordt momenteel niet ondersteund.

## <a name="support-for-replicated-machine-os-versions"></a>Ondersteuning voor gerepliceerde machine OS-versies

Virtuele machines die zijn beveiligd, moet voldoen aan [Azure-vereisten](#failed-over-azure-vm-requirements) bij het repliceren van tooAzure.
Hallo volgende tabel geeft een overzicht van ondersteuning voor gerepliceerde besturingssystemen in verschillende scenario's tijdens het gebruik van Azure Site Recovery. Deze ondersteuning geldt voor elke werkbelasting die wordt uitgevoerd op Hallo besturingssysteem vermeld.

 **VMware of fysieke server** | **Hyper-V (met/zonder VMM)** |
--- | --- |
64-bits Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 met op minste SP1<br/>*Windows Server 2016* : niet ondersteund op dit moment op virtuele VMware-machines en fysieke servers. <br/><br/> Red Hat Enterprise Linux: 5.2 too5.11, 6.1 too6.8, 7.0 too7.3 <br/><br/>Cent OS: 5.2 too5.11, 6.1 too6.8, 7.0 too7.3 <br/><br/>Ubuntu 14.04 TNS server[ (kernel-versies ondersteund)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Ubuntu 16.04 TNS server[ (kernel-versies ondersteund)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Oracle Enterprise Linux 6.4, 6.5 met Hallo Red Hat compatibel kernel of Unbreakable Enterprise Kernel versie 3 (UEK3) <br/><br/> SUSE Linux Enterprise Server 11 SP3 <br/><br/> SUSE Linux Enterprise Server 11 SP4 <br/>(Upgrade van de computers van SLES 11 SP3 tooSLES 11 SP4 repliceren wordt niet ondersteund. Als een gerepliceerde machine is bijgewerkt van SLES 11SP3 tooSLES 11 SP4 is geïnstalleerd, u moet toodisable replicatie en beveiligen Hallo machine opnieuw na Hallo upgrade.) | Een gastbesturingssysteem [ondersteund door Azure](https://technet.microsoft.com/library/cc794868.aspx)


>[!IMPORTANT]
>(Toepasselijke tooVMware of fysieke servers repliceren tooAzure)
>
> Kernel versie 3.10.0-514 wordt ondersteund vanaf versie 9,8 van hello Azure Site Recovery Mobility-service op Red Hat Enterprise Linux Server 7 + en CentOS 7 + servers.<br/><br/>
> Klanten op Hallo 3.10.0-514 kernel met een versie van de Mobility-service die lager is dan versie 9,8 Hallo zijn vereiste toodisable replicatie, Hallo updateversie van Hallo Mobility service tooversion 9,8 en vervolgens opnieuw replicatie inschakelen.


### <a name="supported-ubuntu-kernel-versions-for-vmwarephysical-servers"></a>Ondersteunde versies van Ubuntu kernel voor VMware/fysieke servers

**Release** | **De versie van de Mobility-service** | **Kernelversie** |
--- | --- | --- |
14.04 TNS | 9.9 | 3.13.0-24-Generic too3.13.0-117-algemene<br/>3.16.0-25-Generic too3.16.0-77-algemene<br/>3.19.0-18-Generic too3.19.0-80-algemene<br/>4.2.0-18-Generic too4.2.0-42-algemene<br/>4.4.0-21-Generic too4.4.0-75-algemene |
14.04 TNS | 9.10 | 3.13.0-24-Generic too3.13.0-121-algemene<br/>3.16.0-25-Generic too3.16.0-77-algemene<br/>3.19.0-18-Generic too3.19.0-80-algemene<br/>4.2.0-18-Generic too4.2.0-42-algemene<br/>4.4.0-21-Generic too4.4.0-81-algemene |
16.04 TNS | 9.10 | 4.4.0-21-Generic too4.4.0-81-algemene<br/>4.8.0-34-Generic too4.8.0-56-algemene<br/>4.10.0-14-Generic too4.10.0-24-algemene |


## <a name="supported-file-systems-and-guest-storage-configurations-on-linux-vmwarephysical-servers"></a>Ondersteunde bestandssystemen en Gast opslagconfiguraties op Linux (VMware of fysieke servers)

Hallo volgende bestand systemen en opslag configuratiesoftware wordt ondersteund op Linux-servers met VMware of fysieke servers:
* -Bestandssystemen: ext3, ext4, ReiserFS (Suse Linux Enterprise Server alleen), XFS
* Volumebeheer: LVM2
* Multipath-software: apparaat toewijzen

Paravirtualized-opslagapparaten (apparaten die zijn geëxporteerd door paravirtualized stuurprogramma's) worden niet ondersteund.<br/>
Meerdere wachtrij blok i/o-apparaten worden niet ondersteund.<br/>
Fysieke servers met Hallo HP CCISS opslagcontroller worden niet ondersteund.<br/>

>[!Note]
> Op Linux-servers Hallo mappen te volgen (als is ingesteld als afzonderlijke partities /-bestandssystemen) moet zijn op Hallo dezelfde schijf (schijf Hallo OS) op de bronserver Hallo: / (root), / Boot, /usr, /usr/local, /var, etc<br/><br/>
> XFSv5 functies op XFS bestandssystemen zoals metagegevens controlesom worden ondersteund vanaf versie 9.10 Hallo Mobility-service. Als u XFSv5 functies gebruikt, zorg ervoor dat u versie van de Mobility-Service uitvoert 9.10 of hoger. U kunt Hallo xfs_info hulpprogramma toocheck hello XFS superblock voor Hallo partitie gebruiken. Als ftype is too1 ingesteld, worden klikt u vervolgens XFSv5 functies gebruikt.
>


## <a name="support-for-network-configuration"></a>Ondersteuning voor netwerkconfiguratie
Hallo volgende tabellen geven een overzicht van configuratie-netwerkondersteuning in verschillende scenario's die gebruikmaken van Azure Site Recovery tooreplicate tooAzure.

### <a name="host-network-configuration"></a>Host-netwerkconfiguratie

**Configuratie** | **VMware of fysieke server** | **Hyper-V (met/zonder Virtual Machine Manager)**
--- | --- | ---
NIC-koppeling | Ja<br/><br/>Niet ondersteund wanneer fysieke machines worden gerepliceerd.| Ja
VLAN | Ja | Ja
IPv4 | Ja | Ja
IPv6 | Nee | Nee

### <a name="guest-vm-network-configuration"></a>Configuratie van Gast-VM-netwerken

**Configuratie** | **VMware of fysieke server** | **Hyper-V (met/zonder Virtual Machine Manager)**
--- | --- | ---
NIC-koppeling | Nee | Nee
IPv4 | Ja | Ja
IPv6 | Nee | Nee
Vaste IP-adres (Windows) | Ja | Ja
Vaste IP-adres (Linux) | Ja <br/><br/>Virtuele machines met gelijkmatige geconfigureerde toouse DHCP op failback  | Nee
Meerdere NIC 's | Ja | Ja

### <a name="failed-over-azure-vm-network-configuration"></a>Configuratie van failover Azure VM-netwerken

**Azure-netwerken** | **VMware of fysieke server** | **Hyper-V (met/zonder Virtual Machine Manager)**
--- | --- | ---
ExpressRoute | Ja | Ja
ILB | Ja | Ja
ELB | Ja | Ja
Traffic Manager | Ja | Ja
Meerdere NIC 's | Ja | Ja
Reserved IP | Ja | Ja
IPv4 | Ja | Ja
Behouden van de bron-IP | Ja | Ja


## <a name="support-for-storage"></a>Ondersteuning voor opslag
Hallo volgende tabellen geven een overzicht van ondersteuning voor opslag in verschillende scenario's die gebruikmaken van Azure Site Recovery tooreplicate tooAzure.

### <a name="host-storage-configuration"></a>Host-opslagconfiguratie

**Configuratie** | **VMware of fysieke server** | **Hyper-V (met/zonder Virtual Machine Manager)**
--- | --- | --- | ---
NFS | Ja voor VMware<br/><br/> Er is geen voor fysieke servers | N.v.t.
SMB 3.0 | N.v.t. | Ja
SAN (ISCSI) | Ja | Ja
Multipath (MPIO)<br></br>Getest met de: Microsoft DSM, EMC PowerPath 5.7 SP4, EMC PowerPath DSM voor CLARiiON | Ja | Ja

### <a name="guest-or-physical-server-storage-configuration"></a>Gast of fysieke server opslagconfiguratie

**Configuratie** | **VMware of fysieke server** | **Hyper-V (met/zonder Virtual Machine Manager)**
--- | --- | ---
VMDK | Ja | N.v.t.
VHD/VHDX | N.v.t. | Ja
Generatie 2 VM | N.v.t. | Ja
EFI/UEFI| Nee | Ja
Clusterschijf gedeeld | Nee | Nee
Versleutelde schijf | Nee | Nee
NFS | Nee | N.v.t.
SMB 3.0 | Nee | Nee
RDM | Ja<br/><br/> Niet van toepassing op fysieke servers | N.v.t.
Schijf > 1 TB | Ja<br/><br/>Een Resourcegroepnaam 4095 GB | Ja<br/><br/>Een Resourcegroepnaam 4095 GB
Schijf met de 4K-sectorgrootte | Ja | Ja, ondersteund voor virtuele machines van generatie 1<br/><br/>Niet ondersteund voor virtuele machines van generatie 2.
Volume met striped schijf > 1 TB<br/><br/> LVM logische volumebeheer | Ja | Ja
Opslagruimten | Nee | Ja
Schijf hot toevoegen of verwijderen | Nee | Nee
Schijf uitsluiten | Ja | Ja
Multipath (MPIO) | N.v.t. | Ja

**Azure Storage** | **VMware of fysieke server** | **Hyper-V (met/zonder Virtual Machine Manager)**
--- | --- | ---
LRS | Ja | Ja
GRS | Ja | Ja
RA-GRS | Ja | Ja
Cool storage | Nee | Nee
Hot storage| Nee | Nee
Versleuteling op rest(SSE)| Ja | Ja
Premium Storage | Ja | Ja
Service voor importeren/exporteren | Nee | Nee


## <a name="support-for-azure-compute-configuration"></a>Ondersteuning voor Azure compute-configuratie

**COMPUTE-functie** | **VMware of fysieke server** | **Hyper-V (met/zonder Virtual Machine Manager)**
--- | --- | --- 
Beschikbaarheidssets | Ja | Ja
HUB | Ja | Ja  
Managed Disks | Ja | Ja<br/><br/>Failback tooon-premises van de virtuele machine van Azure met beheerde schijven is momenteel niet ondersteund.

## <a name="failed-over-azure-vm-requirements"></a>Vereisten voor failover-virtuele machine in Azure

U kunt Site Recovery tooreplicate virtuele machines en fysieke servers met een besturingssysteem dat wordt ondersteund door Azure implementeren. Dit omvat de meeste versies van Windows en Linux. Een on-premises virtuele machines die u wilt dat tooreplicate moeten voldoen aan de volgende Azure-vereisten bij het repliceren van tooAzure Hallo.

**Entiteit** | **Vereisten** | **Details**
--- | --- | ---
**Gastbesturingssysteem** | TooAzure Hyper-V-replicatie: Site Recovery ondersteunt alle besturingssystemen die zijn [ondersteund door Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx). <br/><br/> Voor VMware en fysieke server-replicatie: Controleer Hallo Windows en Linux [vereisten](site-recovery-vmware-to-azure-classic.md) | Controle van vereisten mislukt als een niet-ondersteund.
**Architectuur van de Gast-besturingssysteem** | 64-bits | Controle van vereisten mislukt als een niet-ondersteund
**Grootte van de besturingssysteemschijf** | Too2048 GB omhoog als u repliceert **VMware-machines of fysieke servers tooAzure**.<br/><br/>Maximaal 2048 GB voor **Hyper-V Generation 1** virtuele machines.<br/><br/>Een Resourcegroepnaam 300 GB voor **Hyper-V Generation 2 virtuele machines**.  | Controle van vereisten mislukt als een niet-ondersteund
**Het aantal schijven voor besturingssysteem** | 1 | Controle van vereisten mislukt als een niet-ondersteund.
**Aantal gegevensschijven** | 64- of minder als u repliceert **virtuele VMware-machines tooAzure**; 16 of minder als u repliceert **tooAzure Hyper-V-machines** | Controle van vereisten mislukt als een niet-ondersteund
**De grootte van VHD gegevensschijf** | Up too4095 GB | Controle van vereisten mislukt als een niet-ondersteund
**Netwerkadapters** | Meerdere netwerkadapters worden ondersteund |
**Gedeelde VHD** | Niet ondersteund | Controle van vereisten mislukt als een niet-ondersteund
**FC-schijf** | Niet ondersteund | Controle van vereisten mislukt als een niet-ondersteund
**Harde schijf-indeling** | VHD <br/><br/> VHDX | Hoewel VHDX wordt momenteel niet ondersteund in Azure, converteert Site Recovery VHDX tooVHD wanneer u een failover tooAzure actief is. Wanneer u een failback uit blijven tooon-premises Hallo virtuele machines in toouse hello VHDX-indeling.
**BitLocker** | Niet ondersteund | BitLocker moet worden uitgeschakeld voordat u een virtuele machine beveiligt.
**VM-naam** | Tussen 1 en 63 tekens. Beperkte tooletters, cijfers en afbreekstreepjes. Hallo VM-naam moet beginnen en eindigen met een letter of cijfer. | Hallo-waarde in de eigenschappen van de virtuele machine Hallo in Site Recovery bijwerken.
**VM-type** | Generatie 1<br/><br/> Generatie 2--Windows | Generatie 2 virtuele machines met een type besturingssysteem schijf basic (waaronder een of twee gegevensvolumes die zijn opgemaakt als VHDX) en minder dan 300 GB aan schijfruimte worden ondersteund.<br></br>Virtuele machines Linux generatie 2 worden niet ondersteund. [Meer informatie](https://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/)|

## <a name="support-for-recovery-services-vault-actions"></a>Ondersteuning voor Recovery Services-kluis acties

**Actie** | **VMware of fysieke server** | **Hyper-V (geen Virtual Machine Manager)** | **Hyper-V (met Virtual Machine Manager)**
--- | --- | --- | ---
Kluis over brongroepen verplaatsen<br/><br/> Binnen en tussen abonnementen | Nee | Nee | Nee
Verplaats de opslag, netwerk, Azure VM's via resourcegroepen<br/><br/> Binnen en tussen abonnementen | Nee | Nee | Nee


## <a name="support-for-provider-and-agent"></a>Ondersteuning voor de Provider en Agent

**Naam** | **Beschrijving** | **Meest recente versie** | **Details**
--- | --- | --- | --- | ---
**Azure Site Recovery Provider** | Coördineert de communicatie tussen de on-premises servers en Azure <br/><br/> Op de on-premises Virtual Machine Manager-servers of op de Hyper-V-servers worden geïnstalleerd als er geen Virtual Machine Manager-server | 5.1.19 ([beschikbaar is via de portal](http://aka.ms/downloaddra)) | [Meest recente functies en oplossingen](https://support.microsoft.com/kb/3155002)
**Azure Site Recovery Unified Setup (tooAzure VMware)** | Coördineert de communicatie tussen de on-premises VMware-servers en Azure <br/><br/> Geïnstalleerd op de on-premises VMware-servers | 9.3.4246.1 (beschikbaar via de portal) | [Meest recente functies en oplossingen](https://support.microsoft.com/kb/3155002)
**Mobility-service** | Coördineert de replicatie tussen de on-premises VMware servers of fysieke servers en Azure/secundaire site<br/><br/> Geïnstalleerd op de VMware-VM of fysieke servers wilt u dat tooreplicate  | N.V.T. (beschikbaar via de portal) | N.v.t.
**Microsoft Azure Recovery Services (MARS)-agent** | Coördineert de replicatie tussen Hyper-V-machines en Azure<br/><br/> Geïnstalleerd op de on-premises Hyper-V-servers (met of zonder een Virtual Machine Manager-beheerserver) | Nieuwste agent ([beschikbaar is via de portal](http://aka.ms/latestmarsagent)) |






## <a name="next-steps"></a>Volgende stappen
[Vereisten controleren](site-recovery-prereq.md)
