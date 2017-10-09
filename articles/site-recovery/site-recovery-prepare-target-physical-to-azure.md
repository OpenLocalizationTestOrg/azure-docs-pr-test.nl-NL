---
title: Doel (fysieke tooAzure) voorbereiden | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooprepare uw Azure-omgeving toostart repliceren van fysieke servers met Windows of Linux-tooAzure.
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
ms.openlocfilehash: 126fb86133e1a00f5669410943565c4cd78e4369
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a>Doel (VMware tooAzure) voorbereiden
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-prepare-target-vmware-to-azure.md)
> * [Fysieke tooAzure](./site-recovery-prepare-target-physical-to-azure.md)

Dit artikel wordt beschreven hoe tooprepare uw Azure-omgeving toostart repliceren van fysieke servers (x 64), Windows of Linux die worden uitgevoerd in Azure.

## <a name="prerequisites"></a>Vereisten

Hallo artikel wordt ervan uitgegaan dat de volgende Hallo:
- U hebt een Recovery Services-kluis tooprotect uw fysieke servers gemaakt. U kunt een Recovery Services-kluis maken van Hallo [Azure-portal](http://portal.azure.com "Azure-portal").
- U hebt [instellen van uw on-premises omgeving](./site-recovery-set-up-physical-to-azure.md) tooreplicate fysieke servers tooAzure.

## <a name="prepare-target"></a>Doel voorbereiden

Na het voltooien van Hallo **stap 1: Selecteer beveiligingsdoel** en **stap 2: bereid bron**, gaat u te**stap 3: doel**

![Doel voorbereiden](./media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.png)

1. **Abonnement:** van Hallo vervolgkeuzemenu, selecteer Hallo abonnement dat u wilt dat tooreplicate uw fysieke servers naar.
2. **Implementatiemodel:** Selecteer Hallo implementatiemodel (klassiek of Resource Manager)

Op basis van Hallo implementatiemodel gekozen, wordt een validatie tooensure die u ten minste één compatibel storage-account en het virtuele netwerk in Hallo doel abonnement tooreplicate en failover uw fysieke servers naar hebt uitgevoerd.

Zodra het Hallo-validaties wordt voltooid, klikt u op OK toogo toohello volgende stap.

Als u geen compatibel Resource Manager-opslagaccount of virtueel netwerk hebt of tooadd meer wilt, kunt u doen door te klikken op Hallo **+ Opslagaccount** of **+ netwerk** knoppen in de rechterbovenhoek Hallo Hallo blade.

## <a name="next-steps"></a>Volgende stappen
[Replicatie-instellingen configureren](./site-recovery-setup-replication-settings-vmware.md).
