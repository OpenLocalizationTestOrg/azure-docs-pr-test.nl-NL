---
title: aaaPrepare Azure-resources tooreplicate Hyper-V-machines (met System Center VMM) tooAzure met Azure Site Recovery | Microsoft Docs
description: Beschrijft wat u moet in de Azure voordat u begint Hyper-V-machines (met VMM)-tooAzure repliceren met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1568bdc3-e767-477b-b040-f13699ab5644
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 86bfbab7722fe5bd5b93b92e398d1d441505d3b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-with-vmm-tooazure"></a>Stap 5: Voorbereiden op Azure-resources tooAzure voor Hyper-V-replicatie (met VMM)

Nadat u hebt gecontroleerd [vereisten voor de](vmm-to-azure-walkthrough-network.md), volg Hallo-instructies in dit artikel tooprepare Azure resources met behulp van zodat u lokale Hyper-V-machines in System Center Virtual Machine Manager (VMM) clouds tooAzure repliceren kunt, Hallo [Azure Site Recovery](site-recovery-overview.md) service.

Na het lezen van dit artikel, eventuele opmerkingen posten Hallo onderin of technische vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-an-azure-account"></a>Een Azure-account instellen

- Ophalen van een [Microsoft Azure-account](http://azure.microsoft.com/).
- U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).
- Hallo ondersteunde regio's controleren voor de Site is hersteld, onder geografische beschikbaarheid in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).
- Meer informatie over [prijzen voor Site Recovery](site-recovery-faq.md#pricing), en krijgt u Hallo [prijsinformatie](https://azure.microsoft.com/pricing/details/site-recovery/).
- Zorg ervoor dat uw Azure-account juist Hallo [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate virtuele Azure-machines. [Meer informatie](../active-directory/role-based-access-built-in-roles.md) over op rollen gebaseerd toegangsbeheer van Azure.


## <a name="set-up-an-azure-network"></a>Een Azure-netwerk instellen

- Instellen van een [Azure-netwerk](../virtual-network/virtual-network-get-started-vnet-subnet.md). Virtuele machines in Azure worden geplaatst in dit netwerk wanneer ze zijn gemaakt na een failover.
- Hallo-netwerk moet zich in Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis
- Site Recovery in hello Azure-portal kunt instellen netwerken [Resource Manager](../resource-manager-deployment-model.md), of in de klassieke modus.
- U doet er verstandig aan een netwerk in te stellen voordat u begint. Als u dat niet doet, moet u toodo tijdens de implementatie van Site Recovery.
- Meer informatie over [virtueel netwerk prijzen](https://azure.microsoft.com/pricing/details/virtual-network/).


## <a name="set-up-an-azure-storage-account"></a>Een Azure-opslagaccount instellen

- Site Recovery repliceert tooAzure opslag voor lokale machines. Virtuele machines in Azure worden gemaakt van Hallo opslag nadat de failover plaatsvindt.
- Instellen van een standaard/premium [Azure storage-account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold gegevens gerepliceerd tooAzure.
- [Premium-opslag](../storage/common/storage-premium-storage.md) wordt doorgaans gebruikt voor virtuele machines die een consistent hoge i/o-prestaties en lage latentie toohost i/o-intensieve werkbelastingen nodig.
- Als u wilt dat toouse een premium account toostore gerepliceerde gegevens, moet u ook een standard-opslag account toostore replicatielogboeken dat vastleggen lopende tooon-premises gegevens is gewijzigd.
- Afhankelijk van het resourcemodel Hallo gewenste toouse voor failover is uitgevoerd op Azure Virtual machines, instellen van een account in [modus Resource Manager](../storage/common/storage-create-storage-account.md), of [klassieke modus](../storage/common/storage-create-storage-account.md).
- Het is raadzaam dat u een opslagaccount instellen voordat u begint. U moet toodo tijdens de implementatie van Site Recovery. Hallo-accounts moeten in Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis.
- U kunt niet verplaatsen storage-accounts gebruikt door Site Recovery via resourcegroepen binnen Hallo dezelfde abonnement, of tussen verschillende abonnementen behoren.


## <a name="next-steps"></a>Volgende stappen

Ga te[stap 6: VMM voorbereiden](vmm-to-azure-walkthrough-vmm-hyper-v.md)
