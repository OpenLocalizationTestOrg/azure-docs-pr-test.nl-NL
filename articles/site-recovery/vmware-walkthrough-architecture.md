---
title: aaaReview hello architectuur voor VMware replicatie tooAzure | Microsoft Docs
description: In dit artikel biedt een overzicht van de onderdelen en de architectuur die wordt gebruikt bij het repliceren van de lokale virtuele VMware-machines tooAzure Hello Azure Site Recovery-service
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
ms.topic: article
ms.date: 06/27.017
ms.author: raynew
ms.openlocfilehash: 7acb1d8e83a846dca79e175fd1af9324f2c31e65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-vmware-replication-tooazure"></a>Stap 1: Bekijk Hallo-architectuur voor VMware replicatie tooAzure

Dit artikel wordt beschreven Hallo-onderdelen en -processen die worden gebruikt bij het repliceren van lokale VMware virtuele machines tooAzure Hallo met [Azure Site Recovery](site-recovery-overview.md) service.

Eventuele opmerkingen onder Hallo van dit artikel plaatsen of vragen in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Architectuuronderdelen

Hallo-tabel ziet u Hallo-onderdelen die u nodig hebt.

**Onderdeel** | **Vereiste** | **Details**
--- | --- | ---
**Azure** | U moet een Azure-abonnement, Azure storage-account en een Azure-netwerk. | Gerepliceerde gegevens worden opgeslagen in Hallo storage-account. Virtuele machines in Azure worden gemaakt met de Hallo gerepliceerde gegevens bij een storing van uw on-premises site. Hallo virtuele Azure-machines verbinding toohello virtuele Azure-netwerk maken wanneer ze worden gemaakt.
**Configuratieserver** | Een enkel lokale beheerserver (VMware VM) die wordt uitgevoerd van alle Hallo lokale onderdelen van Site Recovery voor Hallo-implementatie. Het gaat hierbij om een configuratieserver, de processerver, de hoofddoelserver. | Hallo configuratieserveronderdeel coördineert de communicatie tussen de on-premises en Azure en beheert gegevensreplicatie.
 **Processerver**:  | Op de configuratieserver Hallo standaard geïnstalleerd. | Fungeert als replicatiegateway. Replicatiegegevens ontvangt, optimaliseert met caching, compressie en codering en verzendt het tooAzure opslag.<br/><br/> Hallo processerver ook push-installatie van de machines tooprotected Hallo Mobility-service verwerkt en wordt automatische detectie van virtuele VMware-machines uitgevoerd.<br/><br/> Naarmate uw implementatie groeit, kunt u extra, afzonderlijk toegewezen proces servers toohandle grotere hoeveelheden replicatieverkeer kunt toevoegen.
 **Hoofddoelserver** | Standaard geïnstalleerd op Hallo lokale configuratie-server. | Hier worden de replicatiegegevens tijdens de failback vanuit Azure afgehandeld.<br/><br/> Als de hoeveelheid failbackverkeer hoog is, kunt u een afzonderlijke hoofddoelserver voor failback implementeren.
**VMware-servers** | Virtuele VMware-machines worden gehost op vSphere ESXi-servers en het is raadzaam een vCenter server toomanage Hallo-hosts. | U toevoegen VMware servers tooyour Recovery Services-kluis.
**Gerepliceerde machines** | Hallo Mobility-service wordt geïnstalleerd op elke VMware VM die u wilt repliceren. Dit kan handmatig worden geïnstalleerd op elke computer of met een push-installatie van de processerver Hallo.

**Afbeelding 1: VMware tooAzure onderdelen**

![Onderdelen](./media/vmware-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>Replicatieproces

1. U instellen kunt het Hallo-implementatie, met inbegrip van on-premises en Azure onderdelen. In de Recovery Services-kluis hello geeft u Hallo replicatiebron en doel, instellen van de configuratieserver hello, maak een replicatiebeleid voor, Hallo Mobility-service implementeren, replicatie inschakelen en een testfailover uitvoeren.
2. Machines repliceren volgens de Hallo replicatiebeleid en een initiële kopie van het Hallo-gegevens is tooAzure gerepliceerde opslag.
3. Nadat de initiële replicatie is voltooid, begint de replicatie van verschillen wijzigingen tooAzure. Bijgehouden wijzigingen voor een machine worden opgeslagen in een .hrl-bestand.
    - Replicerende machines communiceren met de configuratieserver Hallo op poort 443 voor HTTPS binnenkomend verkeer voor replicatiebeheer.
    - Replicerende machines verzenden replicatie gegevens toohello processerver op poort HTTPS 9443 binnenkomende (kan worden aangepast).
    - Hallo configuratieserver ingedeeld replicatiebeheer met Azure via poort 443 voor HTTPS uitgaand.
    - Hallo processerver ontvangt gegevens van bronmachines, optimaliseert versleutelt en verzendt het tooAzure opslag via poort 443 uitgaand.
    - Als u de consistentie tussen meerdere VM's inschakelt, klikt u vervolgens communiceren machines in replicatiegroep Hallo met elkaar via poort 20004. Meerdere VM’s worden gebruikt als u meerdere machines groepeert in de replicatiegroepen die crashconsistent en app-consistent herstelpunten delen bij failover. Dit is handig als machines worden uitgevoerd Hallo dezelfde werkbelasting en toobe consistent nodig.
4. Verkeer tooAzure gerepliceerde opslag openbare eindpunten, is afgelopen Hallo internet. U kunt ook [openbare peering](../expressroute/expressroute-circuit-peerings.md#public-peering) van Azure ExpressRoute gebruiken. Het repliceren van verkeer via een VPN site-naar-site van een lokale site tooAzure wordt niet ondersteund.


**Afbeelding 2: VMware tooAzure replicatie**

![Verbeterd](./media/vmware-walkthrough-architecture/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Failover- en failbackproces

1. Nadat u dat de testfailover werkt verifieert zoals verwacht, kunt u niet-geplande failovers tooAzure uitvoeren zoals vereist. Geplande failover wordt niet ondersteund.
2. U kunt één machine failover of maken [herstelplannen](site-recovery-create-recovery-plans.md), toofail over meerdere virtuele machines.
3. Wanneer u een failover uitvoert, worden er replica-VM's gemaakt in Azure. U doorvoeren een failover toostart toegang tot Hallo werkbelasting van Hallo replica virtuele machine van Azure.
4. Als uw primaire on-premises site weer beschikbaar is, kunt u een failback uitvoeren. U een failback-infrastructuur instellen, Hallo machine repliceren vanaf primaire Hallo secundaire site-toohello en een niet-geplande failover uitvoeren van de secundaire site Hallo. Nadat u deze failover doorvoert, gegevens worden nu back on-premises en moet u tooenable replicatie tooAzure opnieuw. [Meer informatie](site-recovery-failback-azure-to-vmware.md)

Er zijn enkele vereisten voor een failback:


- **Tijdelijke processerver in Azure**: als u wilt dat toofail failback vanuit Azure na een failover moet u tooset van een Azure-VM die is geconfigureerd als processerver, toohandle replicatie van Azure. U kunt deze virtuele machine verwijderen wanneer de failback is voltooid.
- **VPN-verbinding**: voor failback u moet een VPN-verbinding (of Azure ExpressRoute) instellen uit hello Azure toohello lokale netwerksite.
- **Afzonderlijke on-premises hoofddoelserver**: Hallo lokale hoofddoelserver wordt de failback afgehandeld. Hallo hoofddoelserver wordt standaard op Hallo-beheerserver geïnstalleerd, maar als u failback van grotere hoeveelheden verkeer bent mislukken moet u instellen een afzonderlijke on-premises hoofddoelserver voor dit doel.
- **Beleid voor failback**: tooreplicate back tooyour lokale site, moet u een beleid voor failback. Dit wordt automatisch gemaakt wanneer u uw replicatiebeleid maakt.
- **VMware-infrastructuur**: U moet een failback uit op tooan lokale VMware VM. Dit betekent dat u moet een on-premises VMware-infrastructuur, zelfs als u lokale fysieke servers tooAzure repliceert.

**Afbeelding 3: failback van VMware/fysieke failback**

![Failback](./media/vmware-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>Volgende stappen

Ga te[stap 2: Controleer of de vereisten en beperkingen](vmware-walkthrough-prerequisites.md)
