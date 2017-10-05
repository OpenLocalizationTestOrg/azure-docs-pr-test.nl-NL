---
title: Bekijk de architectuur voor VMware-replicatie naar Azure | Microsoft Docs
description: In dit artikel biedt een overzicht van de onderdelen en de architectuur die wordt gebruikt voor het lokale virtuele VMware-machines repliceren naar Azure met de Azure Site Recovery-service
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
ms.openlocfilehash: 4aae04a793bab11562c20ceec0e1ae8f1a035a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="step-1-review-the-architecture-for-vmware-replication-to-azure"></a>Stap 1: Bekijk de architectuur voor VMware-replicatie naar Azure

Dit artikel wordt beschreven voor de onderdelen en processen die worden gebruikt bij het on-premises VMware-virtuele machines repliceren naar Azure worden verkregen met de [Azure Site Recovery](site-recovery-overview.md) service.

Eventuele opmerkingen kunt u onderaan dit artikel plaatsen of vragen stellen op het [Azure Recovery Services-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Architectuuronderdelen

De tabel bevat een overzicht van de onderdelen die u nodig hebt.

**Onderdeel** | **Vereiste** | **Details**
--- | --- | ---
**Azure** | U moet een Azure-abonnement, Azure storage-account en een Azure-netwerk. | Gerepliceerde gegevens worden opgeslagen in het opslagaccount. Virtuele machines in Azure worden gemaakt met de gerepliceerde gegevens bij een storing van uw on-premises site. De Azure-VM's maken verbinding met het virtuele Azure-netwerk wanneer ze worden gemaakt.
**Configuratieserver** | Een enkel lokale beheerserver (VMware VM) die wordt uitgevoerd van alle de on-premises Site Recovery-onderdelen voor de implementatie. Het gaat hierbij om een configuratieserver, de processerver, de hoofddoelserver. | Het configuratieserveronderdeel coördineert de communicatie tussen on-premises en Azure, en beheert de gegevensreplicatie.
 **Processerver**:  | standaard geïnstalleerd op de configuratieserver. | Fungeert als replicatiegateway. Dit onderdeel ontvangt replicatiegegevens, optimaliseert de gegevens met caching, compressie en codering, en verzendt ze naar de Azure-opslag.<br/><br/> De processerver verwerkt ook de push-installatie van de Mobility-service naar beveiligde computers en voert automatische detectie van virtuele VMware-machines uit.<br/><br/> Naarmate uw implementatie groeit, kunt u extra, afzonderlijk toegewezen processervers toevoegen om het toenemende replicatieverkeer af te handelen.
 **Hoofddoelserver** | Standaard geïnstalleerd op de on-premises configuratieserver. | Hier worden de replicatiegegevens tijdens de failback vanuit Azure afgehandeld.<br/><br/> Als de hoeveelheid failbackverkeer hoog is, kunt u een afzonderlijke hoofddoelserver voor failback implementeren.
**VMware-servers** | Virtuele VMware-machines worden gehost op vSphere ESXi-servers. Het wordt aangeraden om een vCenter-server te gebruiken om de hosts te beheren. | U voegt VMware-servers toe aan uw Recovery Services-kluis.
**Gerepliceerde machines** | De Mobility-service wordt geïnstalleerd op elke VMware VM die u wilt repliceren. Deze kan handmatig worden geïnstalleerd op elke computer, of met een push-installatie van de processerver.

**Afbeelding 1: onderdelen van VMware naar Azure**

![Onderdelen](./media/vmware-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>Replicatieproces

1. U instellen kunt de implementatie, met inbegrip van on-premises en Azure onderdelen. In de Recovery Services-kluis geeft u de replicatiebron en doel, instellen van de configuratieserver een replicatiebeleid maken, implementeren van de Mobility-service, replicatie inschakelen en een testfailover uitvoeren.
2. Machines repliceren in overeenstemming met het replicatiebeleid en een initiële kopie van de gegevens worden gerepliceerd naar Azure-opslag.
3. Nadat de initiële replicatie is voltooid, begint de replicatie van wijzigingen naar Azure. Bijgehouden wijzigingen voor een machine worden opgeslagen in een .hrl-bestand.
    - Replicerende machines communiceren met de configuratieserver op inkomende HTTPS-poort 443 voor replicatie.
    - Replicerende machines replicatiegegevens verzenden naar de processerver op poort HTTPS 9443 binnenkomende (kan worden aangepast).
    - De configuratieserver coördineert het replicatiebeheer met Azure via de uitgaande HTTPS-poort 443.
    - De processerver ontvangt gegevens van de bronmachines, optimaliseert en versleutelt deze gegevens en verzendt ze naar Azure Storage via de uitgaande poort 443.
    - Als u consistentie tussen meerdere VM's inschakelt, communiceren machines in de replicatiegroep met elkaar via poort 20004. Meerdere VM’s worden gebruikt als u meerdere machines groepeert in de replicatiegroepen die crashconsistent en app-consistent herstelpunten delen bij failover. Dit is handig als machines dezelfde workload gebruiken en consistent moeten zijn.
4. Verkeer wordt via internet gerepliceerd naar de openbare eindpunten van Azure Storage. U kunt ook [openbare peering](../expressroute/expressroute-circuit-peerings.md#public-peering) van Azure ExpressRoute gebruiken. Het repliceren van verkeer via een site-naar-site-VPN van een on-premises site naar Azure wordt niet ondersteund.


**Afbeelding 2: replicatie van VMware naar Azure**

![Verbeterd](./media/vmware-walkthrough-architecture/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Failover- en failbackproces

1. Wanneer u hebt gecontroleerd of de testfailover is geslaagd, kunt u naar behoefte niet-geplande failovers naar Azure uitvoeren. Geplande failover wordt niet ondersteund.
2. U kunt een failover van één machine uitvoeren of [herstelplannen](site-recovery-create-recovery-plans.md) maken om failovers van meerdere virtuele machines uit te voeren.
3. Wanneer u een failover uitvoert, worden er replica-VM's gemaakt in Azure. U geeft een failover toegang tot de workload via de replica van de Azure-VM.
4. Als uw primaire on-premises site weer beschikbaar is, kunt u een failback uitvoeren. U stelt een infrastructuur voor failback in, start de replicatie van de machine vanaf de secundaire site naar de primaire site en voert een niet-geplande failover uit vanaf de secundaire site. Nadat u deze failover doorvoert, worden de gegevens teruggeplaatst op de on-premises site en moet u de replicatie naar Azure opnieuw inschakelen. [Meer informatie](site-recovery-failback-azure-to-vmware.md)

Er zijn enkele vereisten voor een failback:


- **Tijdelijke processerver in Azure**: als u na een failover een failback vanuit Azure wilt uitvoeren, moet u een virtuele Azure-machine hebben geconfigureerd als processerver, om de replicatie vanuit Azure af te handelen. U kunt deze virtuele machine verwijderen wanneer de failback is voltooid.
- **VPN-verbinding**: voor de failback moet u een VPN-verbinding (of Azure ExpressRoute) hebben ingesteld van het Azure-netwerk naar de on-premises site.
- **Afzonderlijke on-premises hoofddoelserver**: op de on-premises hoofddoelserver wordt de failback afgehandeld. De hoofddoelserver wordt standaard op de beheerserver geïnstalleerd, maar als u een failback van grotere hoeveelheden verkeer uitvoert, kunt u voor dit doel beter een afzonderlijke on-premises hoofddoelserver instellen.
- **Failbackbeleid**: als u wilt repliceren naar de on-premises site, hebt u een failbackbeleid nodig. Dit wordt automatisch gemaakt wanneer u uw replicatiebeleid maakt.
- **VMware-infrastructuur**: u moet een failback uitvoeren naar een lokale virtuele VMware-machine. Dit betekent dat u een on-premises VMware-infrastructuur nodig hebt, zelfs als u fysieke on-premises servers naar Azure repliceert.

**Afbeelding 3: failback van VMware/fysieke failback**

![Failback](./media/vmware-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>Volgende stappen

Ga naar [stap 2: Controleer of de vereisten en beperkingen](vmware-walkthrough-prerequisites.md)
