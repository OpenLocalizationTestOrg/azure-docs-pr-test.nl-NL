---
title: aaaMap netwerken voor virtuele machine van Hyper-V-replicatie tooa secundaire site met Azure Site Recovery | Microsoft Docs
description: Hierin wordt beschreven hoe toomap netwerken bij het repliceren van Hyper-V-machines tooa secundaire VMM-site met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a>Stap 7: De netwerken voor virtuele machine van Hyper-V-replicatie tooa secundaire site toewijzen


Na het instellen van [bron en doel instellingen](vmm-to-vmm-walkthrough-source-target.md) gebruiken voor het repliceren van Hyper-V virtuele machines (VM's) tooa secundaire System Center Virtual Machine Manager (VMM)-site, in dit artikel tooconfigure netwerktoewijzing voor virtuele Hyper-V machine (VM) replicatie tooa secundaire site, met behulp van [Azure Site Recovery](site-recovery-overview.md).

Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Voordat u begint

- Meer informatie over [netwerktoewijzing](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) voordat u begint.
- Controleer of de virtuele machines op de VMM-servers zijn verbonden tooa VM-netwerk.

## <a name="configure-network-mapping"></a>Netwerktoewijzing configureren

1. In **netwerktoewijzing** > **Netwerktoewijzingen**, klikt u op **+ netwerktoewijzing**.
2. In **netwerktoewijzing toevoegen** tabblad, selecteert u Hallo bron en doel van de VMM-servers. Hallo VM-netwerken die zijn gekoppeld aan de VMM-servers Hallo worden opgehaald.
3. In **Bronnetwerk**, selecteer toouse uit Hallo lijst met VM-netwerken die zijn gekoppeld aan de primaire VMM-server Hallo gewenste Hallo-netwerk.
4. In **doelnetwerk**, selecteer Hallo netwerk gewenste toouse op Hallo secundaire VMM-server. Klik vervolgens op **OK**.

    ![Netwerktoewijzing](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

Dit is wat er gebeurt wanneer er netwerktoewijzing wordt uitgevoerd:

* Alle bestaande gerepliceerde virtuele machines die overeenkomen met toohello bron-VM-netwerk is verbonden toohello doel VM-netwerk.
* Nieuwe virtuele machines die verbonden toohello bron-VM-netwerk zijn worden toegewezen doelnetwerk verbonden toohello na de replicatie.
* Als u een bestaande toewijzing met een nieuw netwerk wijzigt, worden gerepliceerde virtuele machines verbonden met de nieuwe instellingen Hallo.
* Als Hallo doelnetwerk meerdere subnetten heeft en een van deze subnetten Hallo heeft dezelfde naam als het subnet waarop Hallo bron virtual machine zich bevindt, wordt Hallo replica virtuele machine na een failover worden verbonden toothat Doelsubnet. Als er geen Doelsubnet met een overeenkomende naam, wordt de Hallo virtuele machine verbonden toohello eerste subnet in het Hallo-netwerk zijn.



## <a name="next-steps"></a>Volgende stappen

Ga te[stap 8: Configureer een beleid voor wachtwoordreplicatie](vmm-to-vmm-walkthrough-replication.md).
