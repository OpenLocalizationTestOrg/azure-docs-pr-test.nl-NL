---
title: aaaHow werkt Site Recovery? | Microsoft Docs
description: In dit artikel vindt u een overzicht van de architectuur van Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-azure-to-azure-architecture
ms.openlocfilehash: ff1580d0fe294148dc0c621728491e6119c3048a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-site-recovery-work-for-on-premises-infrastructure"></a>Hoe werkt Azure Site Recovery voor een on-premises infrastructuur?

> [!div class="op_single_selector"]
> * [Virtuele Azure-machines repliceren](site-recovery-azure-to-azure-architecture.md)
> * [On-premises virtuele machines repliceren](site-recovery-components.md)

Dit artikel wordt beschreven onderliggende architectuur van Hallo [Azure Site Recovery](site-recovery-overview.md) -service en Hallo-componenten waaruit deze werken voor werkbelastingen van lokale tooAzure te repliceren.

Eventuele opmerkingen posten onderin Hallo van dit artikel of in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="replicate-tooazure"></a>TooAzure repliceren

U kunt repliceren en Hallo volgende op de lokale infrastructuur tooAzure beveiligen:

- **VMware**: on-premises virtuele VMware-machines die worden uitgevoerd op een [ondersteunde host](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). U kunt virtuele VMware-machines met een [ondersteund besturingssysteem](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) repliceren.
- **Hyper-V**: on-premises virtuele Hyper-V-machines die worden uitgevoerd op [ondersteunde hosts](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).
- **Fysieke machines**: on-premises fysieke servers waarop Windows of Linux wordt uitgevoerd, op [ondersteunde besturingssystemen](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions). U kunt virtuele Hyper-V-machines repliceren waarop gastbesturingssystemen worden uitgevoerd die [worden ondersteund door Hyper-V en Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).

## <a name="vmware-tooazure"></a>VMware tooAzure

Dit is wat u nodig hebt voor het repliceren van virtuele VMware-machines tooAzure.

Onderwerp | Onderdeel | Details
--- | --- | ---
**Configuratieserver** | Een enkele beheerserver (virtuele VMware-machine) voert alle on-premises onderdelen uit (de configuratieserver, de processerver en de hoofddoelserver) | Hallo configuratieserver coördineert de communicatie tussen de on-premises en Azure en beheert gegevensreplicatie.
 **Processerver**:  | Op de configuratieserver Hallo standaard geïnstalleerd. | Fungeert als replicatiegateway. Replicatiegegevens ontvangt, optimaliseert met caching, compressie en codering en verzendt het tooAzure opslag.<br/><br/> Hallo processerver ook push-installatie van de machines tooprotected Hallo Mobility-service verwerkt en wordt automatische detectie van virtuele VMware-machines uitgevoerd.<br/><br/> Naarmate uw implementatie groeit, kunt u extra, afzonderlijk toegewezen proces servers toohandle grotere hoeveelheden replicatieverkeer kunt toevoegen.
 **Hoofddoelserver** | Standaard geïnstalleerd op Hallo lokale configuratie-server. | Hier worden de replicatiegegevens tijdens de failback vanuit Azure afgehandeld.<br/><br/> Als de hoeveelheid failbackverkeer hoog is, kunt u een afzonderlijke hoofddoelserver voor failback implementeren.
**VMware-servers** | Virtuele VMware-machines worden gehost op vSphere ESXi-servers en het is raadzaam een vCenter server toomanage Hallo-hosts. | U toevoegen VMware servers tooyour Recovery Services-kluis.<br/><br/>
**Gerepliceerde machines** | Hallo Mobility-service wordt geïnstalleerd op elke VMware virtuele machine die u wilt dat tooreplicate. Dit kan handmatig worden geïnstalleerd op elke computer of met een push-installatie van de processerver Hallo.| -

**Afbeelding 1: VMware tooAzure onderdelen**

![Onderdelen](./media/site-recovery-components/arch-enhanced.png)

### <a name="replication-process"></a>Replicatieproces

1. U instellen kunt het Hallo-implementatie, inclusief Azure onderdelen en een Recovery Services-kluis. U opgeven in de kluis Hallo Hallo replicatiebron en doel, instellen van de configuratieserver hello, VMware-servers toevoegen, maak een replicatiebeleid voor, Hallo Mobility-service implementeren, replicatie inschakelen en een testfailover uitvoeren.
2.  Machines starten in overeenstemming met het replicatiebeleid Hallo repliceren en een initiële kopie van de gegevens Hallo tooAzure gerepliceerde opslag.
4. Replicatie van verschillen wijzigingen tooAzure begint nadat Hallo initiële replicatie is voltooid. Bijgehouden wijzigingen voor een machine worden opgeslagen in een .hrl-bestand.
    - Replicerende machines communiceren met de configuratieserver Hallo op poort 443 voor HTTPS binnenkomend verkeer voor replicatiebeheer.
    - Replicerende machines verzenden replicatie gegevens toohello processerver op poort HTTPS 9443 binnenkomende (kan worden geconfigureerd).
    - Hallo configuratieserver ingedeeld replicatiebeheer met Azure via poort 443 voor HTTPS uitgaand.
    - Hallo processerver ontvangt gegevens van bronmachines, optimaliseert versleutelt en verzendt het tooAzure opslag via poort 443 uitgaand.
    - Als u de consistentie tussen meerdere VM's inschakelt, klikt u vervolgens communiceren machines in replicatiegroep Hallo met elkaar via poort 20004. Meerdere VM’s worden gebruikt als u meerdere machines groepeert in de replicatiegroepen die crashconsistent en app-consistent herstelpunten delen bij failover. Dit is handig als machines worden uitgevoerd Hallo dezelfde werkbelasting en toobe consistent nodig.
5. Verkeer tooAzure gerepliceerde opslag openbare eindpunten, is afgelopen Hallo internet. U kunt ook [openbare peering](https://docs.microsoft.com/en-us/azure/expressroute/expressroute-circuit-peerings#public-peering) van Azure ExpressRoute gebruiken. Het repliceren van verkeer via een VPN site-naar-site van een lokale site tooAzure wordt niet ondersteund.

**Afbeelding 2: VMware tooAzure replicatie**

![Verbeterd](./media/site-recovery-components/v2a-architecture-henry.png)

### <a name="failover-and-failback"></a>Failover en failback

1. Nadat u dat de testfailover werkt verifieert zoals verwacht, kunt u niet-geplande failovers tooAzure uitvoeren zoals vereist. Geplande failover wordt niet ondersteund.
2. U kunt één machine failover of maken [herstelplannen](site-recovery-create-recovery-plans.md), toofail over meerdere virtuele machines.
3. Wanneer u een failover uitvoert, worden er replica-VM's gemaakt in Azure. U doorvoeren een failover toostart toegang tot Hallo werkbelasting van Hallo replica virtuele machine van Azure.
4. Als uw primaire on-premises site weer beschikbaar is, kunt u een failback uitvoeren. U een failback-infrastructuur instellen, Hallo machine repliceren vanaf primaire Hallo secundaire site-toohello en een niet-geplande failover uitvoeren van de secundaire site Hallo. Nadat u deze failover doorvoert, gegevens worden nu back on-premises en moet u tooenable replicatie tooAzure opnieuw. [Meer informatie](site-recovery-failback-azure-to-vmware.md)

**Afbeelding 3: failback van VMware/fysieke failback**

![Failback](./media/site-recovery-components/enhanced-failback.png)

## <a name="physical-tooazure"></a>Fysieke tooAzure

Wanneer u fysieke on-premises servers tooAzure repliceert, maakt gebruik van replicatie ook Hallo dezelfde onderdelen en -processen als [VMware tooAzure](#vmware-replication-to-azure), maar houd er rekening mee deze verschillen:

- U kunt een fysieke server gebruiken voor de configuratieserver Hallo in plaats van een VMware VM
- U hebt een on-premises VMware-infrastructuur nodig voor failback. U kunt back tooa fysieke machine niet afkeuren.

## <a name="hyper-v-tooazure"></a>Hyper-V tooAzure

### <a name="replication-process"></a>Replicatieproces

1. U instellen kunt hello Azure onderdelen. Wij raden u aan om opslag- en netwerkaccounts in te stellen voordat u begint met de Site Recovery-implementatie.
2. U maakt een Replication Services-kluis voor Site Recovery en configureert de kluisinstellingen, waaronder:
    - Bron- en doelinstellingen. Als u Hyper-V-hosts in een VMM-cloud niet beheert, voor Hallo doel u een Hyper-V-site-container maken en Hyper-V-hosts tooit toevoegen. Als Hyper-V-hosts in VMM worden beheerd, is het Hallo-bron Hallo VMM-cloud. Hallo-doel is Azure.
    - Installatie van hello Azure Site Recovery Provider en Hallo Microsoft Azure Recovery Services agent. Als u VMM Hallo-Provider wordt geïnstalleerd op deze en Hallo-agent op elke Hyper-V-host. Als er geen VMM, worden zowel Hallo Provider en agent geïnstalleerd op elke host.
    - Maakt u een replicatiebeleid voor Hallo Hyper-V-site of de VMM-cloud. Hallo-beleid is toegepast tooall virtuele machines op hosts in het Hallo-site of in de cloud bevinden.
    - U schakelt replicatie voor virtuele Hyper-V-machines in. Initiële replicatie vindt plaats in overeenstemming met beleidsinstellingen Hallo-replicatie.
4. Gegevenswijzigingen worden bijgehouden en replicatie van verschillen wijzigingen tooAzure wordt gestart nadat de Hallo initiële replicatie is voltooid. Bijgehouden wijzigingen voor een item worden opgeslagen in een .hrl-bestand.
5. Uitvoeren van een test failover-toomake ervoor dat alles werkt.

### <a name="failover-and-failback-process"></a>Failover- en failbackproces

1. U kunt uitvoeren als een geplande of niet-geplande [failover](site-recovery-failover.md) van lokale Hyper-V-machines tooAzure. Als u een geplande failover uitvoert, wordt de Bronmachines tooensure worden afgesloten zonder verlies van gegevens.
2. U kunt één machine failover of maken [herstelplannen](site-recovery-create-recovery-plans.md) tooorchestrate failover van meerdere machines.
4. Nadat u Hallo failover uitvoert, moet u kunnen toosee Hallo replica virtuele machines in Azure gemaakt. U kunt een openbare IP-adres toohello VM indien nodig.
5. U doorvoert vervolgens Hallo failover toostart Hallo werkbelasting vanuit Hallo replica virtuele machine van Azure te openen.
6. Als uw primaire on-premises site weer beschikbaar is, kunt u een [failback](site-recovery-failback-from-azure-to-hyper-v.md) uitvoeren. U ere van een geplande failover van Azure toohello primaire site. Voor een geplande failover, u kunt wijzigingen selecteren toofailback toohello dezelfde virtuele machine of tooan alternatieve locatie en synchroniseren tussen Azure en lokale, tooensure zonder verlies van gegevens. Wanneer virtuele machines worden gemaakt van lokale, doorvoeren Hallo failover.

**Afbeelding 4: Hyper-V-sitereplicatie tooAzure**

![Onderdelen](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)

**Afbeelding 5: Hyper-V in de VMM-clouds tooAzure replicatie**

![Onderdelen](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png)


## <a name="replicate-tooa-secondary-site"></a>De secundaire site repliceren tooa

U kunt Hallo volgende tooyour secundaire site repliceren:

- **VMware**: on-premises virtuele VMware-machines die worden uitgevoerd op een [ondersteunde host](site-recovery-support-matrix-to-sec-site.md#on-premises-servers). U kunt virtuele VMware-machines met een [ondersteund besturingssysteem](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions) repliceren.
- **Fysieke machines**: on-premises fysieke servers waarop Windows of Linux wordt uitgevoerd, op [ondersteunde besturingssystemen](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions).
- **Hyper-V**: on-premises virtuele Hyper-V-machines die worden uitgevoerd op [ondersteunde Hyper-V-hosts](site-recovery-support-matrix-to-sec-site.md#on-premises-servers) die worden beheerd in VMM-clouds. [Ondersteunde hosts](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). U kunt virtuele Hyper-V-machines repliceren waarop gastbesturingssystemen worden uitgevoerd die [worden ondersteund door Hyper-V en Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).


## <a name="vmwarephysical-tooa-secondary-site"></a>VMware of fysieke tooa secundaire site

U repliceren virtuele VMware-machines of fysieke servers tooa secundaire site met InMage Scout.

### <a name="components"></a>Onderdelen

**Onderwerp** | **Onderdeel** | **Details**
--- | --- | ---
**Processerver** | Bevindt zich op de primaire site | U implementeert Hallo proces server toohandle caching, compressie en optimalisatie van gegevens.<br/><br/> Push-installatie van Unified Agent toomachines gewenste tooprotect Hallo ook verwerkt.
**Configuratieserver** | Bevindt zich op de secundaire site | Hallo configuratieserver beheert, configureren en bewaken van uw implementatie hetzij met behulp van de website voor groepsbeheer Hallo of Hallo vContinuum-console.
**vContinuum-server** | Optioneel. Geïnstalleerd in Hallo dezelfde locatie als de configuratieserver Hallo. | De vContinuum-server biedt een console voor het beheren en controleren van de beveiligde omgeving.
**Hoofddoelserver** | Bevindt zich in de secundaire site Hallo | Hallo hoofddoelserver bevat gerepliceerde gegevens. Deze ontvangt gegevens van de processerver hello, maakt een replicamachine op de secundaire site Hallo en bevat de gegevensretentiepunten Hallo.<br/><br/> Hallo aantal hoofddoelservers die u nodig hebt, is afhankelijk van Hallo aantal machines dat u wilt beveiligen.<br/><br/> Als u wilt dat toofail back toohello primaire site, moet u er een hoofddoelserver te. Hallo is Unified Agent geïnstalleerd op deze server.
**VMware ESX/ESXi- en vCenter-server** |  Virtuele machines worden op ESX-/ESXi-hosts gehost. Hosts worden beheerd via een vCenter-server | U moet een VMware-infrastructuur tooreplicate virtuele VMware-machines.
**VM's/fysieke servers** |  Unified Agent is geïnstalleerd op virtuele VMware-machines en fysieke servers die u wilt dat tooreplicate. | Hallo agent fungeert als communicatieprovider tussen alle Hallo-onderdelen.


### <a name="replication-process"></a>Replicatieproces

1. U Hallo onderdeelservers op elke site (configuratie, proces, hoofddoel) instellen en Hallo Unified Agent installeren op computers die u tooreplicate wilt.
2. Na de initiële replicatie verzendt Hallo-agent op elke machine delta replicatie wijzigingen toohello process-server.
3. Hallo processerver optimaliseert de Hallo gegevens en toohello hoofddoelserver op de secundaire site Hallo overdraagt. Hallo configuratieserver beheert het replicatieproces Hallo.

**Afbeelding 6: VMware tooVMware replicatie**

![VMware tooVMware](./media/site-recovery-components/vmware-to-vmware.png)



## <a name="hyper-v-tooa-secondary-site"></a>Hyper-V tooa secundaire site

Dit is wat u nodig hebt voor het repliceren van Hyper-V-machines tooa secundaire site.


**Onderwerp** | **Onderdeel** | **Details**
--- | --- | ---
**VMM-server** | Het is raadzaam een VMM-server op Hallo primaire site, en één in Hallo secundaire site | Elke VMM-server moet worden verbonden toohello internet.<br/><br/> Elke server moet ten minste één privécloud in VMM, met Hyper-V Hallo mogelijkheid profielset hebben.<br/><br/> U installeren hello Azure Site Recovery Provider op Hallo VMM-server. Hallo Provider coördineert en stuurt replicatie met Site Recovery-service Hallo via Hallo internet. De communicatie tussen Hallo Provider en Azure is beveiligd en versleuteld.
**Hyper-V-server** |  Een of meer Hyper-V-hostservers in Hallo primaire en secundaire VMM-clouds.<br/><br/> Servers moeten worden verbonden toohello internet.<br/><br/> Gegevens worden gerepliceerd tussen Hallo primaire en secundaire Hyper-V-hostservers via Hallo LAN of VPN-, Kerberos of certificaatverificatie gebruiken.  
**Virtuele Hyper-V-machines** | Bevindt zich op Hallo bron Hyper-V-hostserver. | Hallo-bronserver host moet ten minste één virtuele machine die u wilt dat tooreplicate hebben.

### <a name="replication-process"></a>Replicatieproces

1. U instellen kunt hello Azure-account.
2. U maakt een Replication Services-kluis voor Site Recovery en configureert de kluisinstellingen, waaronder:

    - Hallo replicatiebron en doel (primaire en secundaire sites).
    - Installatie van hello Azure Site Recovery Provider en Hallo Microsoft Azure Recovery Services agent. Hallo Provider is geïnstalleerd op de VMM-servers en Hallo-agent op elke Hyper-V-host.
    - U maakt een replicatiebeleid voor de bron-VMM-cloud. Hallo beleid is toegepast tooall virtuele machines op hosts in Hallo cloud bevindt.
    - U schakelt replicatie voor virtuele Hyper-V-machines in. Initiële replicatie vindt plaats in overeenstemming met beleidsinstellingen Hallo-replicatie.
4. Gegevenswijzigingen worden bijgehouden en replicatie van verschillen toobegins wordt gewijzigd nadat de initiële replicatie Hallo is voltooid. Bijgehouden wijzigingen voor een item worden opgeslagen in een .hrl-bestand.
5. Uitvoeren van een test failover-toomake ervoor dat alles werkt.

**Afbeelding 7: VMM tooVMM replicatie**

![Lokale tooon-premises](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback"></a>Failover en failback

1. U kunt een geplande of niet-geplande [failover](site-recovery-failover.md) uitvoeren tussen on-premises sites. Als u een geplande failover uitvoert, wordt de Bronmachines tooensure worden afgesloten zonder verlies van gegevens.
2. U kunt één machine failover of maken [herstelplannen](site-recovery-create-recovery-plans.md) tooorchestrate failover van meerdere machines.
4. Als u een niet-geplande failover tooa secundaire site na Hallo failover-machines op de secundaire locatie Hallo uitvoert zijn niet ingeschakeld voor beveiliging of replicatie. Als u een geplande failover uitgevoerd na een failover hello, worden machines op de secundaire locatie Hallo beveiligd.
5. Voer vervolgens Hallo failover toostart toegang tot Hallo werkbelasting van Hallo replica-VM.
6. Als uw primaire site weer beschikbaar is, start u omgekeerde replicatie tooreplicate van Hallo secundaire site toohello primaire. Omgekeerde replicatie worden Hallo virtuele machines naar een beveiligde status, maar er is nog steeds Hallo secundair datacenter Hallo active-locatie.
7. toomake hello primaire site naar de actieve locatie Hallo opnieuw u start een geplande failover van de secundaire tooprimary, gevolgd door een andere omgekeerde replicatie.


## <a name="next-steps"></a>Volgende stappen

- [Meer informatie](site-recovery-hyper-v-azure-architecture.md) over Hallo Hyper-V-replicatie-werkstroom.
- [Vereisten controleren](site-recovery-prereq.md)
