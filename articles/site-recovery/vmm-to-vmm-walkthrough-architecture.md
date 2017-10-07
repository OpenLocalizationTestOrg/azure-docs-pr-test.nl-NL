---
title: Hallo-architectuur voor Hyper-V-replicatie tooa secundaire site met Azure Site Recovery aaaReview | Microsoft Docs
description: Dit artikel bevat een overzicht van Hallo-architectuur voor het repliceren van lokale Hyper-V-machines tooa secundaire System Center VMM-site met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a>Stap 1: Bekijk Hallo-architectuur voor Hyper-V-replicatie tooa secundaire site

Dit artikel wordt beschreven Hallo-onderdelen en processen die betrokken zijn bij het repliceren van on-premises Hyper-V virtuele machines (VM's) in System Center Virtual Machine Manager (VMM) clouds, tooa secundaire VMM-site met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md)service in hello Azure-portal.

Eventuele opmerkingen posten onderin Hallo van dit artikel of in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="architectural-components"></a>Architectuuronderdelen

Dit is wat u nodig hebt voor het repliceren van Hyper-V-machines tooa secundaire VMM-site.

**Onderdeel** | **Locatie** | **Details**
--- | --- | ---
**Azure** | Abonnement in Azure. | Een Recovery Services-kluis in hello Azure-abonnement, tooorchestrate maken en beheren van replicatie tussen de VMM-locaties.
**VMM-server** | U hebt een primaire en secundaire VMM-locatie nodig. | Het is raadzaam een VMM-server op Hallo primaire site, en één in Hallo secundaire site 
**Hyper-V-server** |  Een of meer Hyper-V-hostservers in Hallo primaire en secundaire VMM-clouds. | Gegevens worden gerepliceerd tussen Hallo primaire en secundaire Hyper-V-hostservers via Hallo LAN of VPN-, Kerberos of certificaatverificatie gebruiken.  
**Virtuele Hyper-V-machines** | Op Hyper-V-hostserver. | Hallo-bronserver host moet ten minste één virtuele machine die u wilt dat tooreplicate hebben.

## <a name="replication-process"></a>Replicatieproces

1. Hello Azure-account instellen, een Recovery Services-kluis maken en geef op wat u wilt tooreplicate.
2. U Hallo bron- en replicatie-instellingen configureren, waaronder het hello Azure Site Recovery Provider installeren op de VMM-servers en Hallo Microsoft Azure Recovery Services agent op elke Hyper-V-host.
3. Maakt u een replicatiebeleid voor de gegevensbron Hallo VMM-cloud. Hallo beleid is toegepast tooall virtuele machines op hosts in Hallo cloud bevindt.
4. U replicatie voor elke VMM inschakelen en initiële replicatie van een virtuele machine plaats in overeenstemming met Hallo instellingen die u kiest.
5. Na de initiële replicatie begint de replicatie van deltawijzigingen. Bijgehouden wijzigingen voor een item worden opgeslagen in een .hrl-bestand.


![Lokale tooon-premises](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a>Failover- en failbackproces

1. U kunt een geplande of niet-geplande [failover](site-recovery-failover.md) uitvoeren tussen on-premises sites. Als u een geplande failover uitvoert, wordt de Bronmachines tooensure worden afgesloten zonder verlies van gegevens.
2. U kunt één machine failover of maken [herstelplannen](site-recovery-create-recovery-plans.md) tooorchestrate failover van meerdere machines.
4. Als u een niet-geplande failover tooa secundaire site na Hallo failover-machines op de secundaire locatie Hallo uitvoert zijn niet ingeschakeld voor beveiliging of replicatie. Als u een geplande failover uitgevoerd na een failover hello, worden machines op de secundaire locatie Hallo beveiligd.
5. Voer vervolgens Hallo failover toostart toegang tot Hallo werkbelasting van Hallo replica-VM.
6. Als uw primaire site weer beschikbaar is, start u omgekeerde replicatie tooreplicate van Hallo secundaire site toohello primaire. Omgekeerde replicatie worden Hallo virtuele machines naar een beveiligde status, maar er is nog steeds Hallo secundair datacenter Hallo active-locatie.
7. toomake hello primaire site naar de actieve locatie Hallo opnieuw u start een geplande failover van de secundaire tooprimary, gevolgd door een andere omgekeerde replicatie.



## <a name="next-steps"></a>Volgende stappen

Ga te[stap 2: Controleer Hallo vereisten en beperkingen](vmm-to-vmm-walkthrough-prerequisites.md).
