---
title: aaaReview hello vereisten voor Hyper-V-replicatie tooAzure (zonder de System Center VMM) met Azure Site Recovery | Microsoft Docs
description: Beschrijft de vereisten voor het instellen van replicatie, failovers en herstel van lokale Hyper-V-machines tooAzure met Azure Site Recovery Hallo
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a>Stap 2: Controleer Hallo-vereisten voor Hyper-V (zonder VMM) tooAzure-replicatie

Hallo vereisten worden samengevat in de tabel Hallo.


**Vereiste** | **Details** 
--- | --- 
**Azure** | Meer informatie over [Azure-vereisten](site-recovery-prereq.md#azure-requirements).
**On-premises servers** | [Meer informatie](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) over de vereisten voor Hallo lokale Hyper-V-hosts.
**On-premises Hyper-V-VM's** | Virtuele machines die u wilt dat tooreplicate moet worden uitgevoerd een [ondersteund besturingssysteem](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), en voldoet aan de [vereisten voor Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**Azure-URL's** | Hyper-V-hosts moeten toegang tot toothese URL's:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Als u IP-adressen gebaseerde firewallregels, moet u dat ze tooAzure communicatie toestaan.<br/></br> Hallo toestaan [Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653), en Hallo HTTPS (443)-poort.<br/></br> IP-adresbereiken voor hello Azure-regio van uw abonnement en voor VS-West (gebruikt voor toegangsbeheer en identiteitsbeheer) toestaan.



## <a name="next-steps"></a>Volgende stappen

- Als u een volledige implementatie uitvoert, gaat u verder te[stap 3: plannen van capaciteit](hyper-v-site-walkthrough-capacity.md)
- Als u een eenvoudige testimplementatie uitvoert, gaat u verder te[stap 4: Plan netwerken](hyper-v-site-walkthrough-network.md).
