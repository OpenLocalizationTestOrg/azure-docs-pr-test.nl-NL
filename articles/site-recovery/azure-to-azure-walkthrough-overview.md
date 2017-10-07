---
title: aaaReplicate Azure VM's tussen Azure-regio's | Microsoft-Docs
description: Geeft een overzicht van Hallo stappen vereist tooreplicate Azure VM's tussen Azure-regio's hello Azure Site Recovery-service in hello Azure-portal
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>Virtuele Azure-machines repliceren tussen regio's met Azure Site Recovery

>Dit artikel bevat een overzicht van Hallo stappen vereist tooreplicate Azure virtuele machines (VM's) in een Azure-regio tooAzure virtuele machines in een andere regio. 

>[!NOTE]
>
> Replicatie van Azure VM is momenteel in preview.

Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="step-1-review-architecture"></a>Stap 1: Bekijk architectuur

Voordat u een implementatie, Hallo scenario-architectuur en Hallo onderdelen moet u toodeploy bekijken.

Ga te[stap 1: Bekijk Hallo-architectuur](azure-to-azure-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Stap 2: Controleer vereisten

Controleer dat u Azure-vereisten op plaatsen, met inbegrip van een abonnement, virtuele netwerken, opslagaccounts en VM-vereisten hebben Hallo.

Ga te[stap 2: Controleer of de vereisten en beperkingen](azure-to-azure-walkthrough-prerequisites.md)


## <a name="step-3-plan-networking"></a>Stap 3: Plannen netwerken

Controleer of uitgaande verbinding is ingesteld op Azure Virtual machines die u wilt tooreplicate, en dat de verbindingen van on-premises zijn ingesteld.

Ga te[stap 4: netwerken plannen](azure-to-azure-walkthrough-network.md)



## <a name="step-4-create-a-vault"></a>Stap 4: Een kluis maken 

U moet tooset van een Recovery Services-kluis tooorchestrate en replicatie beheren en Hallo bron regio opgeven.

Ga te[stap 4: een kluis maken](azure-to-azure-walkthrough-vault.md)


## <a name="step-5-enable-replication"></a>Stap 5: Replicatie inschakelen


replicatie tooenable target-locatie-instellingen configureren, instellen van een beleid voor wachtwoordreplicatie en hello Azure VM's die u tooreplicate wilt selecteren. Na het inschakelen, initiële replicatie van Hallo VM zich voordoet.

Ga te[stap 5: replicatie inschakelen](azure-to-azure-walkthrough-enable-replication.md)


## <a name="step-6-run-a-test-failover"></a>Stap 6: Een testfailover uitvoeren

Nadat de eerste replicatie is voltooid en replicatie van verschillen wordt uitgevoerd, kunt u een test failover toomake, controleren of dat alles werkt zoals verwacht uitvoeren.

Ga te[stap 6: een testfailover uitvoeren](azure-to-azure-walkthrough-test-failover.md)


