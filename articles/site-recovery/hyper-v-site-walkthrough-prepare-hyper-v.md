---
title: aaaPrepare Hyper-V host (zonder de System Center VMM) voor replicatie tooAzure | Microsoft Docs
description: Hierin wordt beschreven hoe tooprepare Hyper-V host is voor replicatie tooAzure met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a>Stap 6: Hyper-V-hosts voor replicatie tooAzure voorbereiden

Hallo-instructies in dit artikel tooprepare lokale Hyper-V-hosts toointeract met Azure Site Recovery gebruiken.

Na het lezen van dit artikel, eventuele opmerkingen posten Hallo onderin of technische vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-hosts"></a>Hosts voorbereiden

- Zorg ervoor dat Hallo Hyper-V-hosts voldoen aan Hallo [vereisten](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).
- Zorg ervoor dat de Hallo hosts toegang hebben tot Hallo vereist URL's:

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- Als u IP-adressen gebaseerde firewallregels, moet u dat ze tooAzure communicatie toestaan.
- Hallo toestaan [Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653), en Hallo HTTPS (443)-poort.
- IP-adresbereiken voor hello Azure-regio van uw abonnement en voor VS-West (gebruikt voor toegangsbeheer en identiteitsbeheer) toestaan.

Tijdens de implementatie van Site Recovery kunt u Hyper-V-hosts met virtuele machines die u tooreplicate tooa Hyper-V-site wilt toevoegen. Hallo Site Recovery Provider en de Recovery Services-agent zijn geïnstalleerd op elke host. Hallo Hyper-V-site is geregistreerd in Hallo die Recovery Services-kluis.

## <a name="next-steps"></a>Volgende stappen

Ga te[stap 7: een kluis maken](hyper-v-site-walkthrough-create-vault.md)

