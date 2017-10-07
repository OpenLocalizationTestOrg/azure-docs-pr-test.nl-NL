---
title: de matrix aaaSupport voor replicatie tooa secundaire site met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo ondersteunde besturingssystemen en onderdelen voor Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: raynew
ms.openlocfilehash: 0b2bbc86aff52308d5a90a56d7a3ff4286877740
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="support-matrix-for-replication-tooa-secondary-site-with-azure-site-recovery"></a>De ondersteuningsmatrix voor replicatie tooa secundaire site met Azure Site Recovery

In dit artikel bevat een overzicht van wat wordt ondersteund wanneer u Azure Site Recovery tooreplicate tooa secundaire on-premises site gebruiken.

## <a name="deployment-options"></a>Implementatieopties

**Implementatie** | **VMware of fysieke server** | **Hyper-V (met/zonder SCVMM)**
--- | --- | --- | ---
**Azure Portal** | Een on-premises virtuele VMware-machines toosecondary VMware-site.<br/><br/> Hallo downloaden [InMage Scout gebruikershandleiding](http://download.microsoft.com/download/E/0/8/E08B3BCE-3631-4CED-8E65-E3E7D252D06D/InMage_Scout_Standard_User_Guide_8.0.1.pdf) (niet beschikbaar in hello Azure-portal). | Een on-premises Hyper-V-machines in VMM-clouds tooa secundaire VMM-cloud.<br></br> Niet ondersteund zonder VMM  <br/><br/> Standaard Hyper-V-replicatie alleen. SAN is niet ondersteund.
**Klassieke portal** | Onderhoudsmodus bevinden. Nieuwe kluizen kunnen niet worden gemaakt. | Alleen de onderhoudsmodus<br></br> Niet ondersteund zonder SCVMM
**PowerShell** | Niet ondersteund | Ondersteund<br></br> Niet ondersteund zonder SCVMM

## <a name="on-premises-servers"></a>Lokale servers

### <a name="virtualization-servers"></a>Virtualisatieservers

**Implementatie** | **Ondersteuning**
--- | ---
**VMware-virtuele machine of fysieke server** | vSphere 6.0, 5.5 of 5.1 met de meest recente update
**Hyper-V (met VMM)** | VMM 2016 en VMM 2012 R2

  >[!Note]
  > VMM 2016 clouds met een mengeling van Windows Server 2016 en 2012 R2-hosts worden momenteel niet ondersteund.

### <a name="host-servers"></a>Host-servers

**Implementatie** | **Ondersteuning**
--- | ---
**VMware-virtuele machine of fysieke server** | vCenter 5.5 of 6.0 (ondersteuning voor alleen 5.5 functies)
**Hyper-V (geen VMM)** | Geen een ondersteunde configuratie voor het repliceren van de secundaire site tooa
**Hyper-V met VMM** | Windows Server 2016 en Windows Server 2012 R2 met de nieuwste updates Hallo.<br/><br/> Windows Server 2016 hosts moeten worden beheerd door VMM 2016.

## <a name="support-for-replicated-machine-os-versions"></a>Ondersteuning voor gerepliceerde machine OS-versies
Hallo volgende tabel geeft een overzicht van ondersteuning voor besturingssystemen in verschillende scenario's met Azure Site Recovery opgetreden. Deze ondersteuning geldt voor elke werkbelasting die wordt uitgevoerd op Hallo besturingssysteem vermeld.

**VMware of fysieke server** | **Hyper-V (met VMM)**
--- | --- | ---
64-bits Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 met op minste SP1<br/><br/> Red Hat Enterprise Linux 6.7, 7.1, 7.2 <br/><br/> Centos 6.5 6.6, 6.7, 7.0, 7.1, 7.2 <br/><br/> Oracle Enterprise Linux, 6.4 of 6.5 met Hallo Red Hat compatibel kernel of Unbreakable Enterprise Kernel versie 3 (UEK3) <br/><br/> SUSE Linux Enterprise Server 11 SP3 | Een besturingssysteem Gast [ondersteund door Hyper-V](https://technet.microsoft.com/library/mt126277.aspx)

>[!Note]
>Alleen Linux-machines na opslag Hello kunnen worden gerepliceerd: File system (EXT3, ETX4, ReiserFS, XFS); Multipath-software-apparaat Mapper; Volume manager (LVM2).
>Fysieke servers met HP CCISS controller opslag worden niet ondersteund.
>Hallo ReiserFS bestandssysteem wordt alleen ondersteund op SUSE Linux Enterprise Server 11 SP3.

## <a name="network-configuration"></a>Netwerkconfiguratie

### <a name="hosts"></a>Hosts

**Configuratie** | **VMware of fysieke server** | **Hyper-V (met VMM)**
--- | --- | ---
NIC-koppeling | Ja | Ja
VLAN | Ja | Ja
IPv4 | Ja | Ja
IPv6 | Nee | Nee

### <a name="guest-vms"></a>Gast-VM 's

**Configuratie** | **VMware of fysieke server** | **Hyper-V (met VMM)**
--- | --- | ---
NIC-koppeling | Nee | Nee
IPv4 | Ja | Ja
IPv6 | Nee | Nee
Vaste IP-adres (Windows) | Ja | Ja
Vaste IP-adres (Linux) | Ja | Ja
Meerdere NIC 's | Ja | Ja


## <a name="storage"></a>Storage

### <a name="host-storage"></a>Opslag van de host

**Storage (host)** | **VMware of fysieke server** | **Hyper-V (met VMM)**
--- | --- | ---
NFS | Ja | N.v.t.
SMB 3.0 | N.v.t. | Ja
SAN (ISCSI) | Ja | Ja
Multipath (MPIO) | Ja | Ja

### <a name="guest-or-physical-server-storage"></a>Gast of opslag van de fysieke server

**Configuratie** | **VMware of fysieke server** | **Hyper-V (met VMM)**
--- | --- | ---
VMDK | Ja | N.v.t.
VHD/VHDX | N.v.t. | Ja (omhoog too16 schijven)
Generatie 2 VM | N.v.t. | Ja
Clusterschijf gedeeld | Ja  | Nee
Versleutelde schijf | Nee | Nee
UEFI| Nee | N.v.t.
NFS | Nee | Nee
SMB 3.0 | Nee | Nee
RDM | Ja | N.v.t.
Schijf > 1 TB | Nee | Ja
Volume met striped schijf > 1 TB<br/><br/> LVM | Ja | Ja
Opslagruimten | Nee | Ja
Schijf hot toevoegen of verwijderen | Nee | Nee
Schijf uitsluiten | Nee | Ja
Multipath (MPIO) | N.v.t. | Ja

## <a name="vaults"></a>Kluizen

**Actie** | **VMware of fysieke server** | **Hyper-V (met VMM)**
--- | --- | ---
Verplaatsen van kluizen naar andere resourcegroepen (binnen of tussen abonnementen) | Nee | Nee
Verplaats de opslag, netwerk, Azure VM's via resourcegroepen (binnen of tussen abonnementen) | Nee | Nee

## <a name="provider-and-agent"></a>Provider en agent

**Naam** | **Beschrijving** | **Meest recente versie** | **Details**
--- | --- | --- | --- | ---
**Azure Site Recovery Provider** | Coördineert de communicatie tussen de on-premises servers en Azure <br/><br/> Op de on-premises VMM-servers of op de Hyper-V-servers worden geïnstalleerd als er geen VMM-server | 5.1.19 ([beschikbaar is via de portal](http://aka.ms/downloaddra)) | [Meest recente functies en oplossingen](https://support.microsoft.com/kb/3155002)
**Mobility-service** | Coördineert de replicatie tussen de on-premises VMware-servers of fysieke servers en de secundaire site Hallo<br/><br/> Geïnstalleerd op de VMware-VM of fysieke servers dat u wilt dat tooreplicate  | N.V.T. (beschikbaar via de portal) | N.v.t.


## <a name="next-steps"></a>Volgende stappen

- [Virtuele Hyper-V-machines in VMM-clouds tooa secundaire site repliceren](site-recovery-vmm-to-vmm.md)
- [Virtuele VMware-machines en fysieke servers tooa secundaire site repliceren](site-recovery-vmware-to-vmware.md)
