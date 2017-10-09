---
title: aaaHow werkt op de lokale machine replicatie tooa secundaire on-premises site in de Azure Site Recovery? | Microsoft Docs
description: Dit artikel bevat een overzicht van onderdelen en -architectuur gebruikt bij het repliceren van on-premises virtuele machines en fysieke servers tooa secundaire site Hello Azure Site Recovery-service.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: raynew
ms.openlocfilehash: 097a3f43446fec69ed7f9e0b7f11e8d11f41cc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-on-premises-machine-replication-tooa-secondary-site-work-in-site-recovery"></a>Hoe lokale machine replicatie tooa secundaire site werk in Site Recovery?

Dit artikel wordt beschreven Hallo-onderdelen en processen die betrokken zijn bij het repliceren van on-premises virtuele machines en fysieke servers tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service.

U kunt de volgende tooa secundaire on-premises site Hallo repliceren:
- On-premises virtuele machines van Hyper-V, virtuele machines van Hyper-V in Hyper-V-clusters en zelfstandige hosts die worden beheerd in VMM-clouds (Virtual Machine Manager) van System Center.
- On-premises virtuele machines van VMware, en fysieke Windows- en Linux-servers. In dit scenario wordt de replicatie beheerd door Scout.

Eventuele opmerkingen posten onderin Hallo van dit artikel of in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="replicate-hyper-v-vms-tooa-secondary-on-premises-site"></a>Hyper-V-machines tooa secundaire on-premises site repliceren


### <a name="architectural-components"></a>Architectuuronderdelen

Dit is wat u nodig hebt voor het repliceren van Hyper-V-machines tooa secundaire site.

**Onderdeel** | **Locatie** | **Details**
--- | --- | ---
**Azure** | U hebt een account in Microsoft Azure nodig. |
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

**Afbeelding 1: VMM tooVMM replicatie**

![Lokale tooon-premises](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback-process"></a>Failover- en failbackproces

1. U kunt een geplande of niet-geplande [failover](site-recovery-failover.md) uitvoeren tussen on-premises sites. Als u een geplande failover uitvoert, wordt de Bronmachines tooensure worden afgesloten zonder verlies van gegevens.
2. U kunt één machine failover of maken [herstelplannen](site-recovery-create-recovery-plans.md) tooorchestrate failover van meerdere machines.
4. Als u een niet-geplande failover tooa secundaire site na Hallo failover-machines op de secundaire locatie Hallo uitvoert zijn niet ingeschakeld voor beveiliging of replicatie. Als u een geplande failover uitgevoerd na een failover hello, worden machines op de secundaire locatie Hallo beveiligd.
5. Voer vervolgens Hallo failover toostart toegang tot Hallo werkbelasting van Hallo replica-VM.
6. Als uw primaire site weer beschikbaar is, start u omgekeerde replicatie tooreplicate van Hallo secundaire site toohello primaire. Omgekeerde replicatie worden Hallo virtuele machines naar een beveiligde status, maar er is nog steeds Hallo secundair datacenter Hallo active-locatie.
7. toomake hello primaire site naar de actieve locatie Hallo opnieuw u start een geplande failover van de secundaire tooprimary, gevolgd door een andere omgekeerde replicatie.




## <a name="replicate-vmware-vmsphysical-servers-tooa-secondary-site"></a>VMware-virtuele machines/fysieke servers tooa secundaire site repliceren

U repliceren virtuele VMware-machines of fysieke servers tooa secundaire site met InMage Scout, met behulp van deze architectuur onderdelen:


### <a name="architectural-components"></a>Architectuuronderdelen

**Onderdeel** | **Locatie** | **Details**
--- | --- | ---
**Azure** | InMage Scout. | tooobtain InMage Scout, moet u een Azure-abonnement.<br/><br/> Nadat u een Recovery Services-kluis maakt, kunt u downloadt u InMage Scout en installeert het meest recente updates tooset Hallo Hallo-implementatie.
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

**Afbeelding 2: VMware tooVMware replicatie**

![VMware tooVMware](./media/site-recovery-components/vmware-to-vmware.png)


## <a name="next-steps"></a>Volgende stappen

Bekijk Hallo [ondersteuningsmatrix](site-recovery-support-matrix-to-sec-site.md)
