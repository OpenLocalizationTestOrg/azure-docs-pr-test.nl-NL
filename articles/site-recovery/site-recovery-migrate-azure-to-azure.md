---
title: aaaMigrate Azure IaaS VM's tussen Azure-regio's | Microsoft Docs
description: "Azure Site Recovery toomigrate Azure IaaS virtuele machines van één Azure-regio tooanother gebruiken."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a>Migreren van Azure IaaS virtuele machines tussen Azure-regio's met Azure Site Recovery
## <a name="overview"></a>Overzicht
Welkom tooAzure Site Recovery. Gebruik dit artikel als u wilt dat toomigrate Azure VM's tussen Azure-regio's. Houd rekening met het volgende voordat u begint:

* Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: Azure Resource Manager en het klassieke model. Azure heeft bovendien twee portals: de klassieke Azure-portal die ondersteuning biedt voor het klassieke implementatiemodel Hallo Hallo en hello Azure-portal met ondersteuning voor beide implementatiemodellen. Hallo eenvoudige stappen Hallo voor migratie zijn dezelfde of van Site Recovery in de Resource Manager of in de klassieke configureren. Hallo echter UI-instructies en schermopnamen in dit artikel relevant zijn voor hello Azure-portal.
* **U kunt op dit moment alleen migreren vanaf één regio tooanother. U kunt virtuele machines failover van een Azure-regio tooanother, maar u geen failback opnieuw.**

Eventuele opmerkingen of vragen plaatsen onderin Hallo van dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Vereisten
Dit is wat u nodig hebt voor deze implementatie:

* **IaaS virtuele machines**: virtuele machines die u wilt dat toomigrate Hallo. U migreren deze virtuele machines door ze te behandelen als fysieke machines.

## <a name="deployment-steps"></a>Implementatiestappen
Deze sectie beschrijft de implementatiestappen Hallo in Hallo nieuwe Azure-portal.

1. [Maak een kluis](site-recovery-vmware-to-azure.md).
2. [Replicatie inschakelen](site-recovery-vmware-to-azure.md). Replicatie inschakelen voor Hallo VM's u wilt toomigrate en Azure als bron kiezen. 
3. [Een niet-geplande failover uitvoert](site-recovery-failover.md). Nadat de initiële replicatie is voltooid, kunt u een niet-geplande failover uitvoeren van een Azure-regio tooanother. U kunt desgewenst een herstelplan maken en uitvoeren van een niet-geplande failover, toomigrate meerdere virtuele machines tussen regio's. [Meer informatie](site-recovery-create-recovery-plans.md) over plannen voor herstel.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over andere scenario's voor replicatie in [wat is Azure Site Recovery?](site-recovery-overview.md)
