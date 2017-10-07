---
title: System Center VMM aaaPrepare voor Hyper-V-replicatie tooAzure | Microsoft Docs
description: Hierin wordt beschreven hoe tooprepare System Center VMM-server voor Hyper-V-replicatie tooAzure, met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a>Stap 6: VMM-servers en Hyper-V-hosts voor Hyper-V-replicatie tooAzure voorbereiden

Na het instellen van [Azure onderdelen](vmm-to-azure-walkthrough-prepare-azure.md) gebruiken voor de implementatie van Hallo Hallo-instructies in dit artikel tooprepare on-premises VMM-servers en Hyper-V-hosts toointeract met Azure Site Recovery.

Na het lezen van dit artikel, eventuele opmerkingen posten Hallo onderin of technische vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-vmm-servers"></a>VMM-servers voorbereiden

- U moet ten minste één VMM-server die voldoen aan vereisten voor Hallo-ondersteuning voor replicatie van Site Recovery (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).
- Zorg ervoor dat u hebt Hallo VMM-server voor voorbereid [netwerktoewijzing](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).
- Zorg ervoor dat Hallo VMM-server heeft toegang tot deze URL 's

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- Als u IP-adressen gebaseerde firewallregels, moet u dat ze tooAzure communicatie toestaan.
- Hallo toestaan [Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653), en Hallo HTTPS (443)-poort.
- IP-adresbereiken voor hello Azure-regio van uw abonnement en voor VS-West (gebruikt voor toegangsbeheer en identiteitsbeheer) toestaan.

Tijdens de implementatie van Site Recovery Hallo Site Recovery Provider downloaden en installeren op elke VMM-server. Hallo VMM-server is geregistreerd in Hallo die Recovery Services-kluis.




## <a name="next-steps"></a>Volgende stappen

Ga te[stap 7: een kluis maken](vmm-to-azure-walkthrough-create-vault.md)

