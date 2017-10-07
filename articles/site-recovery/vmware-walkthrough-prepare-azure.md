---
title: aaaPrepare Azure-resources tooreplicate lokale virtuele VMware-machines tooAzure met Azure Site Recovery | Microsoft Docs
description: Beschrijft wat u moet in de Azure voordat u begint met het repliceren van de lokale virtuele VMware-machines tooAzure met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ac72fff0593783add789408ecfeb1812d70108b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-vmware-replication-tooazure"></a>Stap 5: Azure-resources voor VMWare replicatie tooAzure voorbereiden


Volg Hallo-instructies in dit artikel tooprepare Azure resources zodat u kunt repliceren lokale machines tooAzure Hallo met [Azure Site Recovery](site-recovery-overview.md) service.

Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Voordat u begint

Zorg ervoor dat u hebt Hallo gelezen [vereisten](vmware-walkthrough-prerequisites.md)

## <a name="set-up-an-azure-account"></a>Een Azure-account instellen

- Ophalen van een [Microsoft Azure-account](http://azure.microsoft.com/).
- U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).
- Hallo ondersteunde regio's controleren voor de Site is hersteld, onder geografische beschikbaarheid in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).
- Meer informatie over [prijzen voor Site Recovery](site-recovery-faq.md#pricing), en krijgt u Hallo [prijsinformatie](https://azure.microsoft.com/pricing/details/site-recovery/).



## <a name="set-up-an-azure-network"></a>Een Azure-netwerk instellen

- Een Azure-netwerk instellen. Virtuele machines in Azure worden geplaatst in dit netwerk wanneer ze zijn gemaakt na een failover.
- Site Recovery in hello Azure-portal kunt instellen netwerken [Resource Manager](../resource-manager-deployment-model.md), of in de klassieke modus.
- Hallo-netwerk moet zich in Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis
- Meer informatie over [virtueel netwerk prijzen](https://azure.microsoft.com/pricing/details/virtual-network/).
- Meer informatie over [Azure VM-connectiviteit](site-recovery-network-design.md) na een failover.


## <a name="set-up-an-azure-storage-account"></a>Een Azure-opslagaccount instellen

- Site Recovery repliceert tooAzure opslag voor lokale machines. Virtuele machines in Azure worden gemaakt van Hallo opslag nadat de failover plaatsvindt.
- Instellen van een [Azure storage-account](../storage/common/storage-create-storage-account.md#create-a-storage-account) voor gerepliceerde gegevens.
- Site Recovery in hello Azure-portal kunt instellen in Resource Manager, of in de klassieke modus storage-accounts gebruiken.
- Hallo storage-account kan worden standaard of [premium](../storage/common/storage-premium-storage.md).
- Als u een premium-account hebt ingesteld, moet u ook een extra standaardaccount voor logboekgegevens.


## <a name="next-steps"></a>Volgende stappen

Ga te[stap 6: VMware voorbereiden resources](vmware-walkthrough-prepare-vmware.md)
