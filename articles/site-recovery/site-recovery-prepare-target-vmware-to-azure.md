---
title: Doel (VMware tooAzure) voorbereiden | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooprepare uw Azure-omgeving toostart tooAzure voor VMware-virtuele machines repliceren.
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 5975d3c122032f92f8df370ee74fa0c7012ebe2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a>Doel (VMware tooAzure) voorbereiden
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-prepare-target-vmware-to-azure.md)
> * [Fysieke tooAzure](./site-recovery-prepare-target-physical-to-azure.md)

Dit artikel wordt beschreven hoe tooprepare uw Azure-omgeving toostart tooAzure voor VMware-virtuele machines repliceren.

## <a name="prerequisites"></a>Vereisten

Hallo artikel wordt ervan uitgegaan dat de volgende Hallo:
- Uw virtuele VMware-machines, hebt u een Recovery Services-kluis tooprotect gemaakt. U kunt een Recovery Services-kluis maken van Hallo [Azure-portal](http://portal.azure.com "Azure-portal").
- U hebt [instellen van uw on-premises omgeving](./site-recovery-set-up-vmware-to-azure.md) tooreplicate VMware-virtuele machines tooAzure.

## <a name="prepare-target"></a>Doel voorbereiden

Na het voltooien van Hallo **stap 1: Selecteer beveiligingsdoel** en **stap 2: bereid bron**, gaat u te**stap 3: doel**

![Doel voorbereiden](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. **Abonnement:** van Hallo vervolgkeuzemenu, selecteer Hallo abonnement dat u wilt dat tooreplicate uw virtuele machines.
2. **Implementatiemodel:** Selecteer Hallo implementatiemodel (klassiek of Resource Manager)

Op basis van Hallo implementatiemodel gekozen, wordt een validatie tooensure die u ten minste één compatibel storage-account en het virtuele netwerk in Hallo doel abonnement tooreplicate en failover uw virtuele machine hebt uitgevoerd.

Zodra het Hallo-validaties wordt voltooid, klikt u op OK toogo toohello volgende stap.

Als u geen compatibel Resource Manager-opslagaccount of virtueel netwerk hebt of tooadd meer wilt, kunt u doen door te klikken op Hallo **+ Opslagaccount** of **+ netwerk** knoppen in de rechterbovenhoek Hallo Hallo blade.

## <a name="next-steps"></a>Volgende stappen
[Replicatie-instellingen configureren](./site-recovery-setup-replication-settings-vmware.md).
