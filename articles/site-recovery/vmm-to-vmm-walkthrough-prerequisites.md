---
title: aaaReview hello vereisten voor Hyper-V-replicatie tooa secundaire VMM-site met Azure Site Recovery | Microsoft Docs
description: Hierin wordt beschreven Hallo-vereisten voor het repliceren van Hyper-V-machines tooa secundaire VMM-site met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 21ff0545-8be5-4495-9804-78ab6e24add6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 1bd945fdda36c3cce5d159209abbd3c98a7e3682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-and-limitations-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>Stap 2: Controleer Hallo vereisten en beperkingen voor Hyper-V VM replicatie tooa secundaire VMM-site


Nadat u hebt doorgenomen Hallo [scenarioarchitectuur](vmm-to-vmm-walkthrough-architecture.md), Lees dit artikel toomake dat u weet Hallo-vereisten voor implementatie, wanneer het repliceren van on-premises Hyper-V virtuele machines (VM's) wordt beheerd in System Center Virtual Clouds Machine Manager (VMM), tooa secundaire site met behulp van [Azure Site Recovery](site-recovery-overview.md) in hello Azure-portal.

Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites-and-limitations"></a>Vereisten en beperkingen

**Vereiste** | **Details**
--- | ---
**Azure** | Een [Microsoft Azure](http://azure.microsoft.com/) abonnement.<br/><br/> U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).<br/><br/> [Meer informatie](https://azure.microsoft.com/pricing/details/site-recovery/) over prijzen voor Site Recovery.<br/><br/> Hallo ondersteunde regio's controleren voor de Site is hersteld, onder geografische beschikbaarheid in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).
**VMM-servers** | U hebt twee VMM-servers, één in Hallo primaire site en één in Hallo secundaire wordt aangeraden.<br/><br/> Repliceren tussen clouds op één VMM-server wordt ondersteund.<br/><br/> VMM-servers waarop ten minste System Center 2012 SP1 met de nieuwste updates Hallo.<br/><br/> VMM-servers moeten toegang tot internet.
**VMM-clouds** | Elke VMM-server moet op een of meer clouds, en alle clouds Hallo Hyper-V Capaciteitsprofiel ingesteld moeten hebben. <br/><br/>Clouds moeten een of meer VMM-hostgroepen bevatten.<br/><br/> Als u slechts één VMM-server hebt, moet deze ten minste twee clouds, tooact als primaire en secundaire.
**Hyper-V** | Hyper-V-servers moeten ten minste draaien op Windows Server 2012 met Hallo Hyper-V-rol en hebben Hallo nieuwste updates zijn geïnstalleerd.<br/><br/> Een Hyper-V-server moet een of meer virtuele machines bevatten.<br/><br/>  Hyper-V-hostservers moeten zich in hostgroepen in Hallo primaire en secundaire VMM-clouds.<br/><br/> Als u op Windows Server 2012 R2 Hyper-V in een cluster uitvoert, installeert u [2961977 bijwerken](https://support.microsoft.com/kb/2961977)<br/><br/> Als u op Windows Server 2012 Hyper-V in een cluster uitvoert, wordt niet clusterbroker automatisch als u een statisch IP-adressen gebaseerde cluster hebt gemaakt. Hallo clusterbroker handmatig configureren. [Lees meer](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> Hyper-V-servers moeten toegang tot internet.




## <a name="next-steps"></a>Volgende stappen

Ga te[stap 3: plannen netwerken](vmm-to-vmm-walkthrough-network.md).
