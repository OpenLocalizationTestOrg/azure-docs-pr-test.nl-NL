---
title: aaaReplicate Hyper-V-machines in VMM-clouds tooAzure met Azure Site Recovery | Microsoft Docs
description: Biedt een overzicht voor het repliceren van Hyper-V-machines in VMM-clouds tooAzure hello Azure Site Recovery-service gebruiken
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>Hyper-V virtuele machines in VMM-clouds tooAzure met Site Recovery in hello Azure-portal repliceren
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-azure.md)
> * [Klassieke Azure Portal](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell klassiek](site-recovery-deploy-with-powershell.md)


In dit artikel biedt een overzicht van Hallo stappen vereist tooreplicate lokale Hyper-V virtuele machines (VM's) in System Center Virtual Machine Manager (VMM) clouds tooAzure, met behulp van Hallo beheerd [Azure Site Recovery](site-recovery-overview.md) service in Hello Azure-portal.

Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-hello-scenario-architecture"></a>Stap 1: Bekijk Hallo scenario-architectuur

Voordat de implementatie start, bekijk Hallo scenario-architectuur en zorg ervoor dat u weet dat alle Hallo onderdelen moet u toodeploy.

Ga te[stap 1: Bekijk Hallo-architectuur](vmm-to-azure-walkthrough-architecture.md)

## <a name="step-2-review-prerequisites-and-limitations"></a>Stap 2: Controleer de vereisten en beperkingen

Zorg ervoor dat u Hallo implementatievereisten en beperkingen begrijpt.

**Vereisten voor Azure**: U moet een Microsoft Azure-account Azure-netwerken en opslagaccounts.
**On-premises VMM-servers en Hyper-V-hosts**: Zorg ervoor dat VMM-servers en Hyper-V-hosts compatibele en voorbereid voor implementatie van Site Recovery.
**Virtuele machines gerepliceerd**: Controleer of de virtuele machines die u wilt dat tooreplicate Azure-vereisten voldoen.

Ga te[stap 2: Controleer of de vereisten en beperkingen](vmm-to-azure-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Stap 3: Plan capaciteit

Als u een volledige implementatie uitvoert, moet u toofigure welke replicatie bronnen die u nodig hebt. Er zijn enkele van de hulpprogramma's beschikbaar toohelp u dit doen. Als u een snelle tootest Hallo-omgeving instellen doet, kunt u deze stap overslaan.

Ga te[stap 3: plannen van capaciteit](vmm-to-azure-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Stap 4: Netwerken plannen

Moet u toodo sommige netwerk planning tooensure die u bij het implementeren van Hallo scenario netwerktoewijzing kunt configureren dat virtuele Azure-machines verbonden tooAzure virtuele netwerken zijn nadat de failover wordt uitgevoerd en die dat ze zijn toegewezen aan geschikte IP-adressen.

Ga te[stap 4: netwerken plannen](vmm-to-azure-walkthrough-network.md)


## <a name="step-5-prepare-azure-resources"></a>Stap 5: Azure-resources voorbereiden

Instellen van een Azure-account, netwerken en opslag. U kunt dit doen tijdens de implementatie, maar we raden dat u dit doen voordat u begint.

Ga te[stap 5: Azure voorbereiden](vmm-to-azure-walkthrough-prepare-azure.md)

## <a name="step-6-prepare-vmm-and-hyper-v"></a>Stap 6: Voorbereiden VMM en Hyper-V

Hallo lokale VMM-servers en Hyper-V-hosts voorbereiden voor implementatie van Site Recovery.

Ga te[stap 6: lokale servers voorbereiden](vmm-to-azure-walkthrough-vmm-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>Stap 7: Een kluis instellen

Stel een Recovery Services-kluis. Hallo-kluis bevat configuratie-instellingen en stuurt replicatie.

[Stap 7: Een kluis instellen](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Stap 8: Bron- en -instellingen configureren

Hallo bron- en replicatie doellocaties instellen. Hallo VMM server toohello kluis toevoegen en downloaden Hallo-installatiebestanden voor de onderdelen van Site Recovery. Azure Site Recovery Provider setup uitvoeren op Hallo VMM-server. Setup installeert Hallo Provider op Hallo VMM-server en Hallo-server registreren in de kluis Hallo. U installeren Hallo Microsoft Recovery Services-agent op elke Hyper-V-host.

Ga te[stap 8: bron- en -instellingen configureren](vmm-to-azure-walkthrough-source-target.md)

## <a name="step-9-configure-network-mapping"></a>Stap 9: Netwerktoewijzing configureren

Kaart een on-premises VMM VM-netwerken tooAzure virtuele netwerken. Na een failover worden Azure VM's gemaakt in hello Azure-netwerk dat is toegewezen toohello on-premises VM-netwerk in welke Hallo Hyper-V-bron zich bevindt.

Ga te[stap 9: netwerktoewijzing configureren](vmm-to-azure-walkthrough-network-mapping.md)


## <a name="step-10-set-up-a-replication-policy"></a>Stap 10: Een replicatiebeleid instellen

Opgeven hoe lokale VMs gerepliceerde tooAzure.

Ga te[stap 10: een replicatiebeleid instellen](vmm-to-azure-walkthrough-replication.md)


## <a name="step-11-enable-replication-for-vms"></a>Stap 11: Replicatie voor virtuele machines inschakelen

Hallo-virtuele machines die u wilt dat tooreplicate selecteren. Als u een VM voor replicatie triggers Hallo initiële replicatie tooAzure, gevolgd door lopende deltareplicatie.

Ga te[stap 11: replicatie inschakelen](vmm-to-azure-walkthrough-enable-replication.md)


## <a name="step-12-run-a-test-failover"></a>Stap 12: Een testfailover uitvoeren

Een test failover toomake, controleren of dat alles werkt zoals verwacht worden uitgevoerd.

Ga te[stap 12: een testfailover uitvoeren](vmm-to-azure-walkthrough-test-failover.md)


