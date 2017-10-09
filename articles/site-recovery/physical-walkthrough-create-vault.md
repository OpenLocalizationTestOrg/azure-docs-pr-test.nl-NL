---
title: aaaSet van een fysieke server replicatie tooAzure met Azure Site Recovery-kluis | Microsoft Docs
description: Geeft een overzicht van Hallo stappen u moet tooset van een kluis tooreplicate fysieke servers tooAzure met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 988928e3ece31116823f132cc39223fe44443468
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a>Stap 6: Een kluis voor de fysieke server replicatie tooAzure instellen


Dit artikel wordt beschreven hoe tooset van een kluis. Hallo-kluis maken en geef op wat u wilt tooreplicate vanuit uw lokale locatie tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.


Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="create-a-recovery-services-vault"></a>Een Recovery Services-kluis maken

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a>Selecteer een beveiligingsdoel

Selecteer wat u tooreplicate, en waar u tooreplicate aan.

1. Klik op **Recovery Services-kluizen** > kluis.
2. In Hallo Resource Menu, klikt u op **siteherstel** > **infrastructuur voorbereiden** > **beveiligingsdoel**.
3. In **beveiligingsdoel**, selecteer **tooAzure** > **niet gevirtualiseerde/andere**.


## <a name="next-steps"></a>Volgende stappen

Ga te[stap 7: bron- en doel instellen](physical-walkthrough-source-target.md)
