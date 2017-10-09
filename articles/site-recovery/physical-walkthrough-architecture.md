---
title: aaaReview hello architectuur voor de fysieke server replicatie tooAzure met Azure Site Recovery | Microsoft Docs
description: In dit artikel biedt een overzicht van de onderdelen en de architectuur die wordt gebruikt bij het repliceren van lokale fysieke servers tooAzure Hello Azure Site Recovery-service
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 09c9b136-35f5-465e-8d0f-f4c5d5d9f880
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 4f334c181fa6f0821adf978ebe9dbd7d36a3c753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-physical-server-replication-tooazure"></a>Stap 1: Bekijk Hallo-architectuur voor de fysieke server replicatie tooAzure

Dit artikel wordt beschreven Hallo-onderdelen en processen die worden gebruikt wanneer u lokale Windows-/ Linux fysieke servers tooAzure repliceert met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service.

Eventuele opmerkingen onder Hallo van dit artikel plaatsen of vragen in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Architectuuronderdelen

Hallo-tabel ziet u Hallo-onderdelen die u nodig hebt.

**Onderdeel** | **Vereiste** | **Details**
--- | --- | ---
**Azure** | U moet een Azure-account, een Azure storage-account en een Azure-netwerk. | Gerepliceerde gegevens worden opgeslagen in Hallo storage-account en Azure VM's worden gemaakt met Hallo gerepliceerde gegevens wanneer failover plaatsvindt. Virtuele machines in Azure verbinding toohello virtuele Azure-netwerk maken wanneer ze worden gemaakt.
**Configuratieserver** | Een enkel lokale beheerserver (fysieke server of VMware VM) die wordt uitgevoerd van alle Hallo lokale onderdelen van Site Recovery. Het gaat hierbij om een configuratieserver, de processerver, de hoofddoelserver. | Hallo configuratieserveronderdeel coördineert de communicatie tussen de on-premises en Azure en beheert gegevensreplicatie.
 **Processerver**  | Op de configuratieserver Hallo standaard geïnstalleerd. | Fungeert als replicatiegateway. Replicatiegegevens ontvangt, optimaliseert met caching, compressie en codering en verzendt het tooAzure opslag.<br/><br/> Hallo processerver tevens verwerkt push-installatie van de machines tooprotected Hallo Mobility-service.<br/><br/> U kunt aanvullende afzonderlijk toegewezen processervers, toohandle grotere hoeveelheden replicatieverkeer toevoegen.
 **Hoofddoelserver** | Standaard geïnstalleerd op Hallo lokale configuratie-server. | Hier worden de replicatiegegevens tijdens de failback vanuit Azure afgehandeld.<br/><br/> Als de hoeveelheid failbackverkeer hoog is, kunt u een afzonderlijke hoofddoelserver voor failback implementeren.
**Gerepliceerde servers** | Hallo onderdeel van de Mobility-service is geïnstalleerd op elke Windows of Linux-server die u wilt tooreplicate. Dit kan handmatig worden geïnstalleerd op elke computer of met een push-installatie van de processerver Hallo.
**Failback** | Infrastructuur is vereist voor een VMware failback. U kunt back tooa fysieke server niet afkeuren.


**Afbeelding 1: Fysieke tooAzure onderdelen**

![Onderdelen](./media/physical-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>Replicatieproces

1. U instellen kunt het Hallo-implementatie, met inbegrip van on-premises en Azure onderdelen. In de Recovery Services-kluis hello geeft u Hallo replicatiebron en doel, instellen van de configuratieserver hello, maak een replicatiebeleid voor, Hallo Mobility-service implementeren, replicatie inschakelen en een testfailover uitvoeren.
2.  Machines repliceren volgens de Hallo replicatiebeleid en een initiële kopie van het Hallo-gegevens is tooAzure gerepliceerde opslag.
4. Nadat de initiële replicatie is voltooid, begint de replicatie van verschillen wijzigingen tooAzure. Bijgehouden wijzigingen voor een machine worden opgeslagen in een .hrl-bestand.
    - Replicerende machines communiceren met de configuratieserver Hallo op poort 443 voor HTTPS binnenkomend verkeer voor replicatiebeheer.
    - Replicerende machines verzenden replicatie gegevens toohello processerver op poort HTTPS 9443 binnenkomende (kan worden aangepast).
    - Hallo configuratieserver ingedeeld replicatiebeheer met Azure via poort 443 voor HTTPS uitgaand.
    - Hallo processerver ontvangt gegevens van bronmachines, optimaliseert versleutelt en verzendt het tooAzure opslag via poort 443 uitgaand.
    - Als u de consistentie tussen meerdere VM's inschakelt, klikt u vervolgens communiceren machines in replicatiegroep Hallo met elkaar via poort 20004. Meerdere VM’s worden gebruikt als u meerdere machines groepeert in de replicatiegroepen die crashconsistent en app-consistent herstelpunten delen bij failover. Dit is handig als machines worden uitgevoerd Hallo dezelfde werkbelasting en toobe consistent nodig.
5. Verkeer tooAzure gerepliceerde opslag openbare eindpunten, is afgelopen Hallo internet. U kunt ook [openbare peering](../expressroute/expressroute-circuit-peerings.md#public-peering) van Azure ExpressRoute gebruiken. Het repliceren van verkeer via een VPN site-naar-site van een lokale site tooAzure wordt niet ondersteund.

**Afbeelding 2: Fysieke tooAzure replicatie**

![Verbeterd](./media/physical-walkthrough-architecture/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Failover- en failbackproces

Nadat u dat de testfailover werkt verifieert zoals verwacht, kunt u niet-geplande failovers tooAzure uitvoeren zoals vereist. Wanneer u een failover uitvoert, worden virtuele Azure-machines worden gemaakt van gerepliceerde gegevens. Klik, als uw primaire on-premises site weer beschikbaar is, u kunt een failback uit. Opmerking:

- Geplande failover wordt niet ondersteund.
- U kunt één machine failover of maken [herstelplannen](site-recovery-create-recovery-plans.md), toofail via meerdere machines samen.
- U doorvoeren een failover toostart toegang tot Hallo werkbelasting van Hallo replica virtuele machine van Azure.
- Wanneer de primaire site Hallo weer beschikbaar is, wordt het Hallo-machine repliceren van Hallo secundaire toohello primaire site. Voer vervolgens een niet-geplande failover van de secundaire site Hallo. Nadat u deze failover doorvoert, gegevens worden nu back on-premises en moet u tooenable replicatie tooAzure opnieuw.

Failback-onderdelen zijn:

- **Tijdelijke processerver in Azure**: U moet tooset van een virtuele machine van Azure tooact als processerver, toohandle replicatie van Azure. U kunt deze virtuele machine verwijderen wanneer de failback is voltooid.
- **VPN-verbinding**: U moet een VPN-verbinding (of Azure ExpressRoute) uit hello Azure toohello lokale netwerksite.
- **Afzonderlijke on-premises hoofddoelserver**: Hallo lokale hoofddoelserver (standaard geïnstalleerd op de configuratieserver Hallo) wordt de failback afgehandeld. Als u niet terug grote hoeveelheden verkeer, moet u een afzonderlijke on-premises hoofddoelserver instellen voor dit doel.
- **Beleid voor failback**: U moet een beleid voor failback. Dit wordt automatisch gemaakt wanneer u uw replicatiebeleid maakt.
- **VMware-infrastructuur**: U moet een failback uit op tooan lokale VMware VM. Dit betekent dat u moet een on-premises VMware-infrastructuur, zelfs als u lokale fysieke servers tooAzure repliceert.

**Afbeelding 3: Fysieke server failback**

![Failback](./media/physical-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>Volgende stappen

Ga te[stap 2: Controleer of de vereisten en beperkingen](physical-walkthrough-prerequisites.md)
