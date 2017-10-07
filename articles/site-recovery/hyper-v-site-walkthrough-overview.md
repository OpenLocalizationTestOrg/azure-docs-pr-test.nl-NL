---
title: aaaReplicate Hyper-V-machines tooAzure met Azure Site Recovery | Microsoft Docs
description: Hierin wordt beschreven hoe tooorchestrate replicatie, failover en herstel van on-premises Hyper-V-machines tooAzure
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a>Hyper-V virtuele machines (zonder VMM) tooAzure repliceren 

> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-hyper-v-site-to-azure.md)
> * [Klassieke Azure Portal](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell - Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

In dit artikel biedt een overzicht van Hallo stappen die nodig zijn tooreplicate lokale Hyper-V virtuele machines tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) in hello Azure-portal. In deze implementatie van Hyper-V-machines worden niet beheerd door System Center Virtual Machine Manager (VMM).


Na het lezen van dit artikel, eventuele opmerkingen posten Hallo onderin of technische vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-architecture-and-prerequisites"></a>Stap 1: Bekijk de architectuur en vereisten

Voordat u de implementatie begint, Controleer Hallo scenario-architectuur en zorg ervoor dat u begrijpt dat alle benodigde toodeploy Hallo-onderdelen

Ga te[stap 1: Bekijk Hallo-architectuur](hyper-v-site-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Stap 2: Controleer vereisten

Zorg ervoor dat u beschikt over de Hallo vereisten voor elk onderdeel van de implementatie:

- **Vereisten voor Azure**: U moet een Microsoft Azure-account Azure-netwerken en opslagaccounts.
- **Lokale Hyper-V-vereisten**: Zorg ervoor dat Hyper-V-hosts zijn voorbereid voor implementatie van Site Recovery.
- **Virtuele machines gerepliceerd**: virtuele machines die u wilt dat tooreplicate moet toocomply met Azure-vereisten.

Ga te[stap 2: Controleer of de vereisten en beperkingen](hyper-v-site-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Stap 3: Plan capaciteit

Als u een volledige implementatie uitvoert moet u toofigure uit welke replicatie bronnen die u nodig. Er zijn enkele van de hulpprogramma's beschikbaar toohelp u dit doen. Ga tooStep 2. Als u een snelle tootest Hallo-omgeving instellen alleen kunt u deze stap overslaan.

Ga te[stap 3: plannen van capaciteit](hyper-v-site-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Stap 4: Netwerken plannen

U moet een netwerk tooensure dat de virtuele Azure-machines verbonden toonetworks zijn nadat de failover plaatsvindt en dat er Hallo juiste IP-adressen plannen toodo.

Ga te[stap 4: netwerken plannen](hyper-v-site-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Stap 5: Azure-resources voorbereiden

Instellen van Azure-netwerken en opslag voordat u begint. U kunt dit doen tijdens de implementatie, maar we raden dat u dit doen voordat u begint.

Ga te[stap 5: Azure voorbereiden](hyper-v-site-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-hyper-v"></a>Stap 6: Hyper-V voorbereiden

Zorg ervoor dat Hyper-V-servers voldoen aan vereisten voor implementatie van Site Recovery.

Ga te[stap 6: Hyper-V voorbereiden](hyper-v-site-walkthrough-prepare-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>Stap 7: Een kluis instellen

U moet tooset van een Recovery Services-kluis tooorchestrate en beheren van replicatie. Wanneer u Hallo kluis instelt, geeft u op wat u tooreplicate, en waar u tooreplicate naar.

Ga te[stap 7: een kluis maken](hyper-v-site-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Stap 8: Bron- en -instellingen configureren

Hallo-bron en doel dat wordt gebruikt voor replicatie instellen. Instellen van de instellingen van de bronserver houdt het toevoegen van Hyper-V-hosts tooa Hyper-V-site, Hallo Site Recovery Provider en de Recovery Services-agent installeren op elke Hyper-V-host en Hallo site registreren op Hallo die Recovery Services-kluis.

Ga te[stap 8: Hallo bron en doel instellen](hyper-v-site-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>Stap 9: Een replicatiebeleid instellen

U hebt ingesteld een beleid toospecify replicatie-instellingen voor Hyper-V-machines in Hallo kluis.

Ga te[stap 9: een replicatiebeleid instellen](hyper-v-site-walkthrough-replication.md)


## <a name="step-10-enable-replication"></a>Stap 10: De replicatie inschakelen

Nadat u een beleid voor wachtwoordreplicatie aanwezig is, na het inschakelen van hebt, vindt initiële replicatie Hallo VM plaats.

Ga te[stap 10: replicatie inschakelen](hyper-v-site-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>Stap 11: Een testfailover uitvoeren

Nadat de eerste replicatie is voltooid en replicatie van verschillen wordt uitgevoerd, kunt u een test failover toomake, controleren of dat alles werkt zoals verwacht uitvoeren.

Ga te[stap 11: een testfailover uitvoeren](hyper-v-site-walkthrough-test-failover.md)
