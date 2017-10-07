---
title: aaaReplicate virtuele VMware-machines tooAzure met Azure Site Recovery | Microsoft Docs
description: Biedt een overzicht van Hallo stappen voor het repliceren van de werkbelasting op virtuele VMware-machines tooAzure
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a>TooAzure met Site Recovery virtuele VMware-machines repliceren

In dit artikel biedt een overzicht van Hallo stappen vereist tooreplicate lokale VMware virtuele machines tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.


![Implementatieproces](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

**Afbeelding 1: Implementatieoverzicht**

## <a name="step-1-review-architecture-and-prerequisites"></a>Stap 1: Bekijk de architectuur en vereisten

Voordat u de implementatie begint, Controleer Hallo scenario-architectuur en zorg ervoor dat u begrijpt dat alle benodigde toodeploy Hallo-onderdelen

Ga te[stap 1: Bekijk Hallo-architectuur](vmware-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Stap 2: Controleer vereisten

Zorg ervoor dat u beschikt over de Hallo vereisten voor elk onderdeel van de implementatie:

- **Vereisten voor Azure**: U moet een Microsoft Azure-account Azure-netwerken en opslagaccounts.
- **Site Recovery-onderdelen op lokale**: U moet een machine met on-premises Site Recovery-onderdelen.
- **Lokale VMware vereisten**: U moet tooset accounts zodat Site Recovery toegang hebben tot VMware-servers en virtuele machines.
- **Virtuele machines gerepliceerd**: VM's u wilt tooreplicate nodig toocomply met Azure-vereisten en Hallo Mobility serviceonderdeel is geïnstalleerd.

Ga te[stap 2: Controleer de vereisten en beperkingen](vmware-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Stap 3: Plan capaciteit

Als u een volledige implementatie uitvoert moet u toofigure uit welke replicatie bronnen die u nodig. Er zijn enkele van de hulpprogramma's beschikbaar toohelp u dit doen. Ga tooStep 2. Als u een snelle tootest Hallo-omgeving instellen alleen kunt u deze stap overslaan.

Ga te[stap 3: plannen van capaciteit](vmware-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Stap 4: Netwerken plannen

U moet een netwerk tooensure dat de virtuele Azure-machines verbonden toonetworks zijn nadat de failover plaatsvindt en dat er Hallo juiste IP-adressen plannen toodo.

Ga te[stap 4: netwerken plannen](vmware-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Stap 5: Azure-resources voorbereiden

Instellen van Azure-netwerken en opslag voordat u begint. U kunt dit doen tijdens de implementatie, maar we raden dat u dit doen voordat u begint.

Ga te[stap 5: Azure voorbereiden](vmware-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-vmware"></a>Stap 6: VMware voorbereiden

U moet tooset accounts die Site Recovery gebruiken voor:

- Toegang VMware virtualisatie servers tooautomatically detecteren voor virtuele machines.
- Toegang tot virtuele machines tooinstall Hallo Mobility-service. Elke VM die u wilt dat tooreplicate moet hebben Hallo Mobility service agent is geïnstalleerd voordat u kunt replicatie inschakelen.

Ga te[stap 6: VMware voorbereiden](vmware-walkthrough-prepare-vmware.md)

## <a name="step-7-set-up-a-vault"></a>Stap 7: Een kluis instellen

U moet tooset van een Recovery Services-kluis tooorchestrate en beheren van replicatie. Wanneer u Hallo kluis instelt, geeft u op wat u tooreplicate, en waar u tooreplicate naar.

Ga te[stap 7: een kluis instellen](vmware-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Stap 8: Bron- en -instellingen configureren

Hallo-bron en doel dat wordt gebruikt voor replicatie instellen. Instellen van de instellingen van de bronserver omvat Hallo on-premises Site Recovery-onderdelen voor Setup Unified tooinstall uitgevoerd.

Ga te[stap 8: Hallo bron en doel instellen](vmware-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>Stap 9: Een replicatiebeleid instellen

U hebt ingesteld een beleid toospecify replicatie-instellingen voor virtuele VMware-machines in Hallo kluis.

Ga te[stap 9: een replicatiebeleid instellen](vmware-walkthrough-replication.md)

## <a name="step-10-install-hello-mobility-service"></a>Stap 10: Hallo Mobility-service installeren

Hallo Mobility-service moet worden geïnstalleerd op elke virtuele machine die u wilt tooreplicate. Er zijn enkele manieren tooset Hallo service push of pull-installatie.

Ga te[stap 10: Hallo Mobility-service installeren](vmware-walkthrough-install-mobility.md)

## <a name="step-11-enable-replication"></a>Stap 11: Replicatie inschakelen

U kunt replicatie inschakelen nadat Hallo Mobility-service wordt uitgevoerd op een virtuele machine. Na het inschakelen, initiële replicatie van Hallo VM zich voordoet.

Ga te[stap 11: replicatie inschakelen](vmware-walkthrough-enable-replication.md)

## <a name="step-12-run-a-test-failover"></a>Stap 12: Een testfailover uitvoeren

Nadat de eerste replicatie is voltooid en replicatie van verschillen wordt uitgevoerd, kunt u een test failover toomake, controleren of dat alles werkt zoals verwacht uitvoeren.

Ga te[stap 12: een testfailover uitvoeren](vmware-walkthrough-test-failover.md)
