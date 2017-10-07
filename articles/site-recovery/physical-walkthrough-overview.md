---
title: fysieke aaaReplicate lokale servers tooAzure met Azure Site Recovery | Microsoft Docs
description: Biedt een overzicht van Hallo stappen voor het repliceren van workloads die worden uitgevoerd op de lokale Windows-/ Linux fysieke servers tooAzure Hello Azure Site Recovery-service.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a>Replicatie van fysieke servers tooAzure met Site Recovery

In dit artikel biedt een overzicht van Hallo stappen vereist tooreplicate lokale Windows-/ Linux fysieke servers tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.


## <a name="step-1-review-architecture-and-prerequisites"></a>Stap 1: Bekijk de architectuur en vereisten

Voordat u de implementatie begint, Controleer Hallo scenario-architectuur en zorg ervoor dat u begrijpt dat alle benodigde tooset Hallo implementatie Hallo-onderdelen.

Ga te[stap 1: Bekijk Hallo-architectuur](physical-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Stap 2: Controleer vereisten

Zorg ervoor dat u beschikt over de Hallo vereisten voor elk onderdeel van de implementatie:

- **Vereisten voor Azure**: U moet een Microsoft Azure-account Azure-netwerken en opslagaccounts.
- **Site Recovery-onderdelen op lokale**: U moet een machine met on-premises Site Recovery-onderdelen.
- **Gerepliceerde machines**: Servers die u wilt dat tooreplicate moeten toocomply met on-premises en Azure-vereisten.

Ga te[stap 2: Controleer de vereisten en beperkingen](physical-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Stap 3: Plan capaciteit

Als u een volledige implementatie uitvoert moet u toofigure uit welke replicatie bronnen die u nodig. Als u een snelle tootest Hallo-omgeving instellen doet, kunt u deze stap overslaan.

Ga te[stap 3: plannen van capaciteit](physical-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Stap 4: Netwerken plannen

U moet een netwerk tooensure dat de virtuele Azure-machines verbonden toonetworks zijn nadat de failover plaatsvindt en dat er Hallo juiste IP-adressen plannen toodo.

Ga te[stap 4: netwerken plannen](physical-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Stap 5: Azure-resources voorbereiden

Instellen van Azure-netwerken en opslag voordat u begint. 

Ga te[stap 5: Azure voorbereiden](physical-walkthrough-prepare-azure.md)


## <a name="step-6-set-up-a-vault"></a>Stap 6: Een kluis instellen

U een Recovery Services-kluis tooorchestrate instellen en beheren van replicatie. Wanneer u Hallo kluis instelt, geeft u op wat u tooreplicate, en waar u tooreplicate naar.

Ga te[stap 6: een kluis instellen](physical-walkthrough-create-vault.md)

## <a name="step-7-configure-source-and-target-settings"></a>Stap 7: De bron en doel-instellingen configureren

Instellingen configureren voor Hallo bron en doel (Azure) site. Instellingen van de bronserver omvat Hallo on-premises Site Recovery-onderdelen voor Setup Unified tooinstall uitgevoerd.

Ga te[stap 7: Hallo bron en doel instellen](physical-walkthrough-source-target.md)

## <a name="step-8-set-up-a-replication-policy"></a>Stap 8: Een replicatiebeleid instellen

Instellen van een beleid toospecify welke fysieke servers te repliceren.

Ga te[stap 8: een replicatiebeleid instellen](physical-walkthrough-replication.md)

## <a name="step-9-install-hello-mobility-service"></a>Stap 9: Hallo Mobility-service installeren

Hallo Mobility-service moet worden geïnstalleerd op elke server die u wilt tooreplicate. Er zijn enkele manieren tooset Hallo-service met push of pull-installatie.

Ga te[stap 9: Hallo Mobility-service installeren](physical-walkthrough-install-mobility.md)

## <a name="step-10-enable-replication"></a>Stap 10: De replicatie inschakelen

Nadat het Hallo Mobility-service wordt uitgevoerd op een server, kunt u replicatie inschakelen. Na het inschakelen, initiële replicatie van Hallo VM zich voordoet.

Ga te[stap 10: replicatie inschakelen](physical-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>Stap 11: Een testfailover uitvoeren

Nadat de eerste replicatie is voltooid en de replicatie van verschillen wordt uitgevoerd, kunt u een test failover toomake, controleren of dat alles werkt zoals verwacht uitvoeren.

Ga te[stap 11: een testfailover uitvoeren](physical-walkthrough-test-failover.md)

