---
title: aaaReplicate Hyper-V-machines tooa secundaire VMM-site met Azure Site Recovery | Microsoft Docs
description: Biedt een overzicht voor het repliceren van Hyper-V-machines tooa secundaire VMM-site met behulp van hello Azure-portal.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>Hyper-V virtuele machines in VMM-clouds tooa secundaire VMM-site repliceren

> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-vmm.md)
> * [Klassieke portal](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

In dit artikel biedt een overzicht van Hallo stappen tooreplicate lokale Hyper-V virtuele machines (VM's vereist) in System Center Virtual Machine Manager (VMM)-clouds, tooa secundaire VMM locatie worden beheerd met behulp van [Azure Site Recovery](site-recovery-overview.md)in hello Azure-portal.

Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-hello-scenario-architecture"></a>Stap 1: Bekijk Hallo scenario-architectuur

Voordat de implementatie start, bekijk Hallo scenario-architectuur en zorg ervoor dat u weet dat alle Hallo onderdelen moet u toodeploy.

Ga te[stap 1: Bekijk Hallo architectuur](vmm-to-vmm-walkthrough-architecture.md).

## <a name="step-2-review-prerequisites-and-limitations"></a>Stap 2: Controleer de vereisten en beperkingen

Zorg ervoor dat u Hallo implementatievereisten en beperkingen begrijpt.

**Vereisten voor Azure**: U hebt een Microsoft Azure-abonnement en Azure Recovery Services-kluis, tooorchestrate en beheren van replicatie.
**On-premises VMM-servers en Hyper-V-hosts**: Zorg ervoor dat VMM-servers en Hyper-V-hosts compatibele en voorbereid voor implementatie van Site Recovery.

Ga te[stap 2: Controleer of de vereisten en beperkingen](vmm-to-vmm-walkthrough-prerequisites.md).

## <a name="step-3-plan-networking"></a>Stap 3: Plannen netwerken

U moet een netwerk tooensure kunt u de netwerkkoppeling tussen VMM VM-netwerken bij het implementeren van Hallo scenario configureren planning toodo.

Ga te[stap 3: plannen netwerken](vmm-to-vmm-walkthrough-network.md).


## <a name="step-4-prepare-vmm-and-hyper-v"></a>Stap 4: Voorbereiden VMM en Hyper-V

Hallo VMM-servers en Hyper-V-hosts voorbereiden voor implementatie van Site Recovery.

Ga te[stap 4: lokale servers voorbereiden](vmm-to-vmm-walkthrough-vmm-hyper-v.md).

## <a name="step-5-set-up-a-vault"></a>Stap 5: Een kluis instellen

Stel een Recovery Services-kluis. Hallo-kluis bevat configuratie-instellingen en stuurt replicatie.

[Stap 5: Instellen van een kluis](vmm-to-vmm-walkthrough-create-vault.md).

## <a name="step-6-set-up-source-and-target-settings"></a>Stap 6: Bron- en -instellingen instellen

Hallo bron- en replicatie VMM doellocaties instellen. Hallo VMM-servers toohello kluis toevoegen en downloaden Hallo-installatiebestanden voor de onderdelen van Site Recovery. Azure Site Recovery Provider setup uitvoeren op Hallo VMM-server. Setup installeert Hallo Provider op Hallo VMM-server en Hallo-server registreren in de kluis Hallo. U installeren Hallo Microsoft Recovery Services-agent op elke Hyper-V-host.

Ga te[stap 6: Hallo bron en doel-instellingen instellen](vmm-to-vmm-walkthrough-source-target.md).

## <a name="step-7-configure-network-mapping"></a>Stap 7: Netwerktoewijzing configureren

VMM VM-netwerken in de bron- en doellocaties Hallo worden toegewezen. Na een failover worden virtuele machines gemaakt in het doelnetwerk Hallo dat maps toohello bron VM-netwerk in welke Hallo bron-Hyper-V VM zich bevindt.

Ga te[stap 7: netwerktoewijzing configureren](vmm-to-vmm-walkthrough-network-mapping.md).


## <a name="step-8-set-up-a-replication-policy"></a>Stap 8: Een replicatiebeleid instellen

Geef op hoe virtuele machines worden gerepliceerd tussen VMM-locaties.

Ga te[stap 8: Stel een beleid voor wachtwoordreplicatie](vmm-to-vmm-walkthrough-replication.md).


## <a name="step-9-enable-replication-for-vms"></a>Stap 9: Replicatie voor virtuele machines inschakelen

Hallo-virtuele machines die u wilt dat tooreplicate selecteren. Als u een virtuele machine voor replicatie triggers Hallo initiële replicatie toohello secundaire site, gevolgd door lopende deltareplicatie.

Ga te[stap 9: replicatie inschakelen](vmm-to-vmm-walkthrough-enable-replication.md).


## <a name="step-10-run-a-test-failover"></a>Stap 10: Een testfailover uitvoeren

Een test failover toomake, controleren of dat alles werkt zoals verwacht worden uitgevoerd.

Ga te[stap 10: een testfailover uitvoeren](vmm-to-vmm-walkthrough-test-failover.md).
