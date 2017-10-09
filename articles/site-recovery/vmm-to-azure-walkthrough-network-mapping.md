---
title: de netwerktoewijzing aaaConfigure voor het repliceren van Hyper-V-machines in VMM-clouds tooAzure met Azure Site Recovery | Microsoft Docs
description: Hierin wordt beschreven hoe netwerktoewijzing tooconfigure bij het repliceren van Hyper-V-machines in VMM tooAzure met Azure Site Recovery clouds
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a>Stap 9: Netwerktoewijzing voor Hyper-V-replicatie (met VMM) tooAzure configureren

Na het instellen van Hallo [bron- en replicatie-instellingen](vmm-to-azure-walkthrough-source-target.md), in dit artikel tooconfigure netwerk toewijzing toomap tussen on-premises VMM VM-netwerken en Azure-netwerken gebruiken.

Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Voordat u begint

- Meer informatie over [netwerktoewijzing](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).
- [VMM voorbereiden op netwerktoewijzing](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping). 
- Verifieer dat de virtuele machines op Hallo VMM-server verbonden tooa VM-netwerk zijn en dat u ten minste één virtuele Azure-netwerk hebt gemaakt. Meerdere VM-netwerken kunnen worden toegewezen tooa één Azure-netwerk.

## <a name="configure-mapping"></a>Toewijzing configureren

Configureer het toewijzen als volgt:

1. In **Site Recovery-infrastructuur** > **Netwerktoewijzingen** > **netwerktoewijzing**, klikt u op Hallo **+ netwerktoewijzing**  pictogram.

    ![Netwerktoewijzing](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. In **netwerktoewijzing toevoegen**, selecteer Hallo bron-VMM-server, en **Azure** als Hallo doel.
3. Controleer of u Hallo-abonnement en Hallo implementatiemodel na een failover.
4. In **Bronnetwerk**, selecteer Hallo bron on-premises VM-netwerk gewenste toomap uit die zijn gekoppeld aan de VMM-server Hallo Hallo-lijst.
5. In **doelnetwerk**, selecteer hello Azure-netwerk in welke replica virtuele Azure-machines geplaatst worden moeten nadat ze zijn gemaakt. Klik vervolgens op **OK**.

    ![Netwerktoewijzing](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

Dit is wat er gebeurt wanneer er netwerktoewijzing wordt uitgevoerd:

* Bestaande virtuele machines op Hallo bron VM-netwerk zijn verbonden toohello doelnetwerk bij toewijzing begint. Nieuwe virtuele machines verbonden toohello bron VM-netwerk zijn verbonden toohello toegewezen Azure-netwerk wanneer er replicatie plaatsvindt.
* Als u een bestaande netwerktoewijzing wijzigt, gerepliceerde virtuele machines verbinding maken met behulp van de nieuwe instellingen Hallo.
* Als Hallo doelnetwerk meerdere subnetten heeft en een van deze subnetten Hallo heeft dezelfde naam als het subnet waarop Hallo bron virtuele machine zich bevindt en vervolgens Hallo replica virtuele machine verbindt toothat Doelsubnet na een failover.
* Als er geen Doelsubnet met een overeenkomende naam, verbindt Hallo virtuele machine toohello eerste subnet in het Hallo-netwerk.



## <a name="next-steps"></a>Volgende stappen

Ga te[stap 10: een replicatiebeleid maken](vmm-to-azure-walkthrough-replication.md)
