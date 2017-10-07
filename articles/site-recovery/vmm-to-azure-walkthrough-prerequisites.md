---
title: aaaReview hello vereisten voor Hyper-V-replicatie tooAzure (met System Center VMM) met Azure Site Recovery | Microsoft Docs
description: Beschrijft de vereisten voor het instellen van replicatie, failovers en herstel van lokale Hyper-V-machines in VMM-clouds tooAzure, met Azure Site Recovery Hallo
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a1c30fd5-c979-473c-af44-4f725ad3e3ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: raynew
ms.openlocfilehash: de13a2d80b1a9a5d968a180d559f661ab11e70c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-with-vmm-tooazure-replication"></a>Stap 2: Controleer Hallo-vereisten voor Hyper-V (met VMM) tooAzure-replicatie

Nadat u hebt doorgenomen Hallo [scenarioarchitectuur](vmm-to-azure-walkthrough-architecture.md), Lees dit artikel toomake dat u weet Hallo-vereisten voor implementatie. 

## <a name="prerequisites-and-limitations"></a>Vereisten en beperkingen

**Vereiste** | **Details**
--- | ---
**Azure-account** | U hebt een [Microsoft Azure-account](http://azure.microsoft.com/) nodig.
**Azure Storage** | U moet een Azure storage-account toostore gerepliceerde gegevens.<br/><br/> Hallo storage-account moet zich in Hallo dezelfde regio bevinden als hello Azure Recovery Services-kluis.<br/><br/>U kunt [geografisch redundante opslag](../storage/common/storage-redundancy.md#geo-redundant-storage) of lokaal redundante opslag gebruiken. Wij raden geografisch redundante opslag aan. Met geografisch redundante opslag is gegevens tegen als een regionale uitval of als de primaire regio Hallo kan niet worden hersteld.<br/><br/> U kunt een standaard Azure-opslagaccount gebruiken of kunt u Azure [Premium-Storage](../storage/common/storage-premium-storage.md) gebruiken. Premium Storage kan I/O-intensieve werkbelastingen hosten en wordt meestal gebruikt voor virtuele machines die consistent hoge I/O-prestaties en lage latentie nodig hebben. Als u Premium Storage gebruikt voor gerepliceerde gegevens, hebt u ook een standaardopslagaccount nodig. Standard-opslagaccount slaat replicatielogboeken die de doorlopende wijzigingen tooon-premises gegevens vastleggen.
**Azure-netwerk** | U moet een [Azure-netwerk](../virtual-network/virtual-network-get-started-vnet-subnet.md), toowhich virtuele Azure-machines verbinding maken na een failover. Hello Azure-netwerk moet Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis.
**On-premises VMM-servers** | U hebt een of meer VMM-servers nodig met System Center 2012 R2 of hoger.<br/><br/> Elke VMM-server moet een of meer privéclouds hebben. Elke cloud heeft een of meer hostgroepen nodig.<br/><br/> Hallo VMM-beheerserver moet toegang tot internet.
**On-premises Hyper-V** | Hyper-V-hostservers moeten ten minste draaien op Windows Server 2012 R2 met Hallo Hyper-V-functie ingeschakeld of Microsoft Hyper-V Server 2012 R2. de meest recente updates Hallo moeten worden geïnstalleerd.<br/><br/> Hallo Hyper-V-host moet zich bevinden in een hostgroep voor VMM (dat zich in een VMM-cloud).<br/><br/> Een host moet een of meer virtuele machines die u wilt dat tooreplicated hebben.<br/><br/> Hyper-V-hosts moeten worden verbonden toohello internet voor replicatie tooAzure, rechtstreeks of met een proxy. Hyper-V-servers moeten beschikken over Hallo oplossingen beschreven in artikel [2961977](https://support.microsoft.com/kb/2961977).
**On-premises Hyper-V-VM's** | Virtuele machines die u wilt dat tooreplicate moet worden uitgevoerd een [ondersteund besturingssysteem](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), en voldoet aan de [vereisten voor Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). Hallo VM-naam kan worden gewijzigd nadat de replicatie is ingeschakeld. 




## <a name="next-steps"></a>Volgende stappen

Ga te[stap 3: plannen van capaciteit](vmm-to-azure-walkthrough-capacity.md)
