---
title: aaaSet van VMM en Hyper-V voor replicatie tooa secundaire site met Azure Site Recovery | Microsoft Docs
description: Hierin wordt beschreven hoe tooset van System Center VMM-servers en Hyper-V-hosts voor replicatie tooa secundaire VMM-site.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d0389e3b-3737-496c-bda6-77152264dd98
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 677bf6d38328ccc425e3b0f056d03159a52da428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-vmm-and-hyper-v-for-hyper-v-vm-replication-tooa-secondary-site"></a>Stap 4: Instellen van VMM en Hyper-V voor Hyper-V VM replicatie tooa secundaire site 

Nadat u hebt voorbereid voor netwerken, instellen van System Center Virtual Machine Manager (VMM)-servers en Hyper-V-hosts voor Hyper-V virtuele machine (VM) replicatie tooa secundaire site met behulp van [Azure Site Recovery](site-recovery-overview.md) in hello Azure-portal. 

Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="prepare-vmm-servers"></a>VMM-servers voorbereiden 

tooprepare voor implementatie:


1. Zorg ervoor dat de VMM-servers voldoen aan Hallo [ondersteuningsvereisten](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), en [implementatievereisten](vmm-to-vmm-walkthrough-prerequisites.md).
2. Zorg ervoor dat de VMM-servers zijn verbonden toohello internet en toegang toothese URL's hebben.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - Als u IP-adressen gebaseerde firewallregels, moet u dat ze tooAzure communicatie toestaan.
    - Hallo toestaan [Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653), en Hallo HTTPS (443)-poort.
    - IP-adresbereiken voor hello Azure-regio van uw abonnement en voor VS-West (gebruikt voor toegangsbeheer en identiteitsbeheer) toestaan.
3. Zorg ervoor dat de VMM-server Hallo [voorbereid voor netwerktoewijzing](vmm-to-vmm-walkthrough-network.md#prepare-for-network-mapping)


## <a name="prepare-hyper-v-hostsclusters"></a>Hyper-V-hosts/clusters voorbereiden

1. Zorg ervoor dat Hyper-V-hosts/clusters voldoen Hallo [ondersteuningsvereisten](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), en [implementatievereisten](vmm-to-vmm-walkthrough-prerequisites.md).
2. Controleren van vereisten voor Hallo [Hyper-V-machines](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)
3. Controleer of [netwerk](site-recovery-support-matrix-to-sec-site.md#network-configuration) en [opslag](site-recovery-support-matrix-to-sec-site.md#storage) vereisten.
4. Zorg ervoor dat Hyper-V-hosts zijn verbonden toohello internet en toegang toothese URL's hebben.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - Als u IP-adressen gebaseerde firewallregels, moet u dat ze tooAzure communicatie toestaan.
    - Hallo toestaan [Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653), en Hallo HTTPS (443)-poort.
    - IP-adresbereiken voor hello Azure-regio van uw abonnement en voor VS-West (gebruikt voor toegangsbeheer en identiteitsbeheer) toestaan.

## <a name="prepare-for-single-server-deployment"></a>Voorbereiden voor implementatie met één server


Als u slechts één VMM-server hebt, kunt u virtuele machines te repliceren in Hyper-V-hosts in VMM-cloud Hallo[Azure](hyper-v-site-walkthrough-overview.md) of tooa secundaire VMM-cloud, zoals beschreven in dit document. De eerste optie hello wordt aangeraden omdat repliceren tussen clouds niet naadloos.

Als u tooreplicate tussen clouds wilt, kunt u met een enkele zelfstandige VMM-server of met één VMM-server geïmplementeerd in een Windows-cluster gespreide repliceren

### <a name="replicate-with-a-standalone-vmm-server"></a>Repliceren met een zelfstandige VMM-server

In dit scenario kunt u Hallo één VMM-server implementeren als een virtuele machine in de primaire site Hallo en repliceren van deze VM tooa secundaire site met Site Recovery en Hyper-V Replica.

1. **Instellen van VMM op een Hyper-V-virtuele machine**. We raden aan dat u Hallo SQL Server-exemplaar dat door VMM gebruikt op Hallo plaatsen dezelfde virtuele machine. Dit bespaart tijd als slechts één VM toobe gemaakt heeft. Als u wilt dat toouse extern exemplaar van SQL Server en een storing optreedt, moet u toorecover dat exemplaar voordat u VMM kunt herstellen.
2. **Controleer Hallo VMM-beheerserver is ten minste twee clouds die zijn geconfigureerd**. Één cloud bevat virtuele machines u wilt tooreplicate en andere cloud Hallo als de secundaire locatie Hallo fungeert Hallo. Hallo van cloud met Hallo virtuele machines die u wilt dat tooprotect moeten voldoen aan [vereisten](#prerequisites).
3. Site Recovery ingesteld zoals beschreven in dit artikel. Maken en Hallo VMM-server geregistreerd in een kluis, instellen van een beleid voor wachtwoordreplicatie en replicatie inschakelen. namen van Hallo bron en doel-VMM wordt dezelfde Hallo. Geef op dat de initiële replicatie vindt plaats via Hallo-netwerk.
4. Wanneer u netwerktoewijzing instellen kunt u VM-netwerk voor de primaire cloud toohello VM-netwerk voor de secundaire cloud Hallo HALLO hallo toewijzen.
5. Hyper-V Replica hebt ingeschakeld op Hallo Hyper-V-host met Hallo VMM VM in Hallo Hyper-V Manager-console en replicatie inschakelen voor Hallo VM. Zorg ervoor dat u Hallo VMM virtuele machine tooclouds die zijn beveiligd door Site Recovery, tooensure dat Hyper-V Replica-instellingen worden niet door Site Recovery overschreven niet toevoegen.
6. Als u herstelplannen voor failover die u maakt Hallo dezelfde VMM-server voor de bron en doel.
7. In een volledige onderbreking failover en als volgt herstellen:

   1. Een niet-geplande failover worden uitgevoerd in Hallo Hyper-V Manager-console in Hallo secundaire site toofail via Hallo primaire VMM VM toohello secundaire site.
   2. Controleer of dat Hallo die VMM VM is en actief en in de kluis hello, worden uitgevoerd een niet-geplande failover toofail via Hallo virtuele machines van primaire toosecondary clouds. Hallo failover doorvoeren en selecteert u een alternatief herstelpunt indien nodig.
   3. Nadat hello niet-geplande failover voltooid is, zijn alle resources toegankelijk vanaf de primaire site Hallo opnieuw.
   4. Te Hallo primaire site opnieuw in Hallo Hyper-V Manager-console op de secundaire site Hallo beschikbaar is, kunt u omgekeerde replicatie voor Hallo VMM VM. Hiermee start u replicatie voor virtuele machine Hallo van secundaire tooprimary.
   5. Een geplande failover uitvoeren in Hallo Hyper-V Manager-console in Hallo secundaire site, toofail via Hallo VMM VM toohello primaire site. Hallo failover doorvoeren. Omgekeerde replicatie activeert zodat hello VMM VM wordt opnieuw gerepliceerd van primaire toosecondary.
   6. In de Recovery Services-kluis Hallo, schakelt u omgekeerde replicatie voor de Hallo werkbelasting van virtuele machines, toostart ze van secundaire tooprimary te repliceren.
   7. In Hallo Recovery Services-kluis, voer een geplande failover toofail back Hallo werkbelasting VMs toohello primaire site. Hallo failover toocomplete doorvoeren deze. Omgekeerde replicatie toostart replicerende Hallo werkbelasting van virtuele machines van primaire toosecondary activeert.

### <a name="replicate-with-a-stretched-vmm-cluster"></a>Repliceren met een gespreide VMM-cluster

In plaats van een zelfstandige VMM-server implementeren als een virtuele machine die wordt gerepliceerd tooa secundaire site, kunt u VMM maximaal beschikbaar maken door deze te implementeren als een virtuele machine in een Windows-failovercluster. Dit biedt veerkracht werkbelasting en bescherming tegen hardwarefouten. toodeploy met Site Recovery Hallo VMM VM moet worden geïmplementeerd in een cluster stretch geografisch afzonderlijke sites. toodo dit:

1. Installeer VMM op een virtuele machine in een Windows-failovercluster en selecteer Hallo optie toorun Hallo server als maximaal beschikbaar tijdens de installatie.
2. Hallo SQL Server-exemplaar dat wordt gebruikt door VMM moet worden gerepliceerd met SQL Server AlwaysOn-beschikbaarheidsgroepen, zodat er een replica van de database Hallo in Hallo secundaire site is.
3. Hallo-instructies in dit artikel toocreate een kluis, Hallo-server registreren en de beveiliging instelt. U moet tooregister elke VMM-server in het Hallo-cluster in Hallo Recovery Services-kluis. toodo dit Hallo Provider te installeren op een actief knooppunt en Hallo VMM-server geregistreerd. U kunt vervolgens Hallo Provider installeren op andere knooppunten.
4. Wanneer er een storing optreedt, worden Hallo VMM-server en de bijbehorende SQL Server-database failover, en toegankelijk vanuit Hallo secundaire site.



## <a name="next-steps"></a>Volgende stappen

Ga te[stap 5: een kluis instellen](vmm-to-vmm-walkthrough-create-vault.md).
