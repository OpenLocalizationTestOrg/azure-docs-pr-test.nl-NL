---
title: aanbevolen procedures voor aaaAzure siteherstel | Microsoft Docs
description: In dit artikel worden de aanbevolen procedures beschreven voor het implementeren van Azure Site Recovery
services: site-recovery
documentationCenter: 
author: rayne-wiselman"
manager: cfreeman
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-support-matrix-to-azure
ms.openlocfilehash: 288df858a0e1c1f5ad96dbe8b9dd0dc69d8f56ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-ready-toodeploy-azure-site-recovery"></a>Gereed toodeploy Azure Site Recovery ophalen

Dit artikel wordt beschreven hoe tooprepare voor Azure Site Recovery-implementatie.

## <a name="protecting-hyper-v-virtual-machines"></a>Virtuele Hyper-V-machines beveiligen

U hebt een aantal implementatieopties voor het beveiligen van virtuele Hyper-V-machines. U kunt lokale Hyper-VMs tooAzure of tooa secundair datacenter repliceren. Er zijn verschillende vereisten voor elke implementatie.

**Vereiste** | **TooAzure (met VMM) repliceren** | **Hyper-V-machines tooAzure (niets VMM) repliceren** | **Hyper-V-machines toosecondary site (met VMM) repliceren** | **Details**
---|---|---|---|---
**VMM** | VMM die wordt uitgevoerd op System Center 2012 R2 <br/><br/>Ten minste één VMM-cloud met één of meer VMM-hostgroepen. | N.v.t. | VMM-servers in Hallo primaire en secundaire sites op ten minste System Center 2012 SP1 met de meest recente updates. <br/><br/> Ten minste één cloud op elke VMM-server. Clouds hebben Hallo Hyper-V capaciteitsprofiel instellen.<br/><br/> Hallo-broncloud moet ten minste één VMM-hostgroep hebben. | Optioneel. U hoeft niet toohave die System Center VMM in volgorde tooreplicate Hyper-V virtuele machines tooAzure geïmplementeerd, maar als u dit moet u toomake of Hallo VMM-server juist is ingesteld. Dat betekent onder meer ervoor te zorgen dat u uitvoert Hallo juist VMM-versies en clouds zijn ingesteld.
**Hyper-V** | Ten minste één Hyper-V-hostserver in Hallo lokale site met Windows Server 2012 R2 of hoger | Ten minste één Hyper-V-server op Hallo bron en doel sites waarop minimaal Windows Server 2012 met de nieuwste updates Hallo geïnstalleerd en verbonden toohello internet.<br/><br/> Hallo Hyper-V-servers moeten zich in een hostgroep in een VMM-cloud. | Ten minste één Hyper-V-server op Hallo bron en doel sites waarop minimaal Windows Server 2012 met de nieuwste updates Hallo geïnstalleerd en verbonden toohello internet.<br/><br/> Hallo Hyper-V-servers moeten zich bevinden in een hostgroep in een VMM-cloud. |
**Virtuele machines** | Ten minste één virtuele machine op Hallo bron Hyper-V-hostserver | Ten minste één virtuele machine op Hallo Hyper-V-hostserver in de bron Hallo VMM-cloud | Ten minste één virtuele machine op Hallo Hyper-V-hostserver in de bron Hallo VMM-cloud. |  Virtuele machines repliceren tooAzure moeten voldoen aan de vereisten van de virtuele machine van Azure
**Azure-account** | U moet een Azure-account en een abonnement toohello Site Recovery-service. | U moet een Azure-account en een abonnement toohello Site Recovery-service. | N.v.t. | Als u geen account hebt, gaat u aan de slag met een gratis proefversie.
**Azure Storage** | U hebt een abonnement nodig op een Azure Storage-account waarvoor geo-replicatie is ingeschakeld. | U hebt een abonnement nodig op een Azure Storage-account waarvoor geo-replicatie is ingeschakeld. | N.v.t. | Hallo-account moet zich dezelfde regio als de Azure Site Recovery-kluis Hallo Hallo en worden gekoppeld aan Hallo hetzelfde abonnement.
**Netwerken** | Instellen van de netwerk-toewijzing tooensure dat alle machines met failover op Hallo van dezelfde Azure-netwerk verbinding kan maken tooeach andere, ongeacht welk herstelplan ze zich in. Als een netwerkgateway is geconfigureerd op het Hallo-doel Azure-netwerk, kunnen virtuele machines bovendien tooother on-premises virtuele machines verbinding. Als u niet ingesteld op het netwerk toewijzen alleen machines met failover in Hallo hetzelfde herstelplan verbinding kan maken. | N.v.t. |  <br/><br/>Stel netwerk toewijzing tooensure dat virtuele machines zijn verbonden tooappropriate netwerken na een failover en virtuele replicamachines optimaal op Hyper-V-hostservers worden geplaatst. Als u geen netwerk configureert de VM-netwerk verbonden tooany gerepliceerde machines toewijzing niet na een failover. |  tooset up netwerktoewijzing met VMM moet u toomake of VMM logische en VM-netwerken correct zijn geconfigureerd.
**Providers en agents** | Tijdens de implementatie installeert u hello Azure Site Recovery Provider op de VMM-servers. U hebt hello Azure Recovery Services-agent installeren op Hyper-V-servers in de VMM-clouds. | Tijdens de implementatie installeert u zowel hello Azure Site Recovery Provider- en hello Azure Recovery Services-agent op Hallo Hyper-V-hostserver of het cluster| Tijdens de implementatie installeert u hello Azure Site Recovery Provider op de VMM-servers. U hebt hello Azure Recovery Services-agent installeren op Hyper-V-servers in de VMM-clouds. | Providers en agents verbinding tooSite herstel via Hallo internet via een versleutelde HTTPS-verbinding. U niet nodig hebt tooadd firewalluitzonderingen of een specifieke proxy voor Hallo providerverbinding te maken.
**Verbinding met internet** | Alleen Hallo VMM-servers hebt een internetverbinding nodig. | Alleen Hallo Hyper-V-hostservers moeten een internetverbinding | Alleen voor VMM-servers is een internetverbinding nodig | Virtuele machines niet hoeft daarop geïnstalleerd en geen verbinding maken met rechtstreeks toohello internet.



## <a name="protect-vmware-virtual-machines-or-physical-servers"></a>Virtuele VMware-machines of fysieke servers beveiligen

U hebt een aantal implementatieopties voor het beveiligen van virtuele VMware-machines of fysieke Windows-/Linux-servers. U kunt ze tooAzure of tooa secundair datacenter repliceren. Er zijn verschillende vereisten voor elke implementatie.

**Vereiste** | **Repliceren VMware virtuele machines/fysieke servers tooAzure)** | * **VMware-virtuele machines/fysieke servers toosecondary site repliceren**  
---|---|---
**Primaire site** | **Processerver**: een speciale Windows-server (fysiek of virtueel) | **Processerver**: een speciale Windows-server (fysiek of een virtuele VMware-machine)<br/><br/>  
**Secundaire on-premises site** | N.v.t. | **Configuratieserver**: een speciale Windows-server (fysiek of virtueel) <br/><br/> **Hoofddoelserver**: een speciale server (fysiek of virtueel). Configureren met Windows tooprotect Windows-computers of Linux-tooprotect Linux.
**Azure** | **Abonnement**: U hebt een abonnement nodig voor Hallo Site Recovery-service. <br/><br/> **Opslagaccount**: u hebt een opslagaccount nodig waarvoor geo-replicatie is ingeschakeld. Hallo-account moet zich dezelfde regio bevinden als de Site Recovery-kluis Hallo Hallo en worden gekoppeld aan Hallo hetzelfde abonnement. <br/><br/> **Configuratieserver**: U moet tooset Hallo configuratie server als een virtuele machine in Azure <br/><br/> **Hoofddoelserver**: U moet tooset Hallo hoofddoel server als een virtuele machine in Azure <br/><br/> Configureren met Windows tooprotect Windows-computers of Linux-tooprotect Linux.<br/><br/> **Virtuele Azure-netwerk**: U moet een Azure-netwerk op welke Hallo configuratieserver en de hoofddoelserver wordt geïmplementeerd. Deze moet Hallo hetzelfde abonnement en dezelfde regio bevinden als hello Azure Site Recovery-kluis | N.v.t.  
**Virtuele machines/fysieke servers** | Ten minste één virtuele VMware-machine of fysieke Windows-/Linux-server.<br/><br/>Tijdens de implementatie van wordt Hallo Mobility-service geïnstalleerd op elke machine| Ten minste één virtuele VMware-machine of fysieke Windows-/Linux-server.<br/><br/> Tijdens de implementatie wordt Hallo Unified agent geïnstalleerd op elke machine.




## <a name="azure-virtual-machine-requirements"></a>Vereisten voor virtuele Azure-machines

U kunt Site Recovery tooreplicate virtuele machines en fysieke servers met een besturingssysteem dat wordt ondersteund door Azure implementeren. Dit omvat de meeste versies van Windows en Linux. U moet toomake zeker die lokale virtuele machines die u wilt dat tooprotect voldoet aan de Azure-vereisten.


## <a name="optimizing-your-deployment"></a>Uw implementatie optimaliseren

Gebruik Hallo tips toohelp u optimaliseren en schalen van uw implementatie te volgen.

- **Besturingssysteem volumegrootte**: wanneer u een virtuele machine tooAzure Hallo besturingssysteem systeemvolume repliceren moet minder dan 1 TB. Als u hebt meer volumes dan dit u handmatig kunt verplaatsen tooa andere schijf voordat u implementatie begint.
- **Gegevens schijfgrootte**: als u repliceert tooAzure u up too32 gegevensschijven op een virtuele machine, elk met een maximum van 1 TB kan hebben. U kunt virtuele machines tot ~32 TB effectief repliceren en er effectief failovers voor uitvoeren.
- **Herstel plan limieten**: Site Recovery toothousands van virtuele machines kunnen worden geschaald. Plannen voor herstel zijn bedoeld als een model voor toepassingen die een failover samen uitvoeren moet zodat we het aantal computers in een plan herstel too50 Hallo beperken.
- **Azure-servicelimieten**: elk Azure-abonnement wordt geleverd met een reeks standaardlimieten voor kerngeheugens, cloudservices enz. Het is raadzaam om een test failover toovalidate Hallo beschikbaarheid van resources in uw abonnement uit te voeren. U kunt de limieten wijzigen via de ondersteuning van Azure.
- **Capaciteitsplanning**: maak een planning voor het schalen en de prestaties.
- **Replicatiebandbreedte**: als u te weinig replicatiebandbreedte hebt, let u hierop:
    - **ExpressRoute**: Site Recovery werkt met Azure ExpressRoute en WAN-optimalisatie, bijvoorbeeld middels Riverbed.
    - **Replicatieverkeer**: Site Recovery wordt gebruikt een smartcard initiële replicatie met alleen gegevensblokken uitvoert en niet Hallo volledige VHD. Bij doorlopende replicatie worden alleen wijzigingen gerepliceerd.
    - **Netwerkverkeer**: U kunt netwerkverkeer voor replicatie wordt gebruikt door het instellen van Windows QoS met een beleid op basis van Hallo doel-IP-adres en poort beheren.  Bovendien, als u repliceert tooAzure Site Recovery met hello Azure backup-agent. U kunt voor die agent beperkingen configureren.
- **RTO**: als u wilt dat toomeasure Hallo beoogde hersteltijd (RTO) u met Site Recovery verwachten kunt we raden u een testfailover uitvoeren en weergave Hallo Site Recovery-taken tooanalyze hoeveel tijd het duurt toocomplete Hallo-bewerkingen. Als u bent tooAzure failover, voor Hallo's best RTO het is raadzaam dat u alle handmatige acties automatiseren, door te integreren met Azure automation en herstel.
- **RPO**: Site Recovery biedt ondersteuning voor een bijna-synchrone beoogd herstelpunt (RPO) wanneer u tooAzure repliceren. Hiervoor wordt aangenomen dat er voldoende bandbreedte beschikbaar is tussen uw datacenter en Azure.
