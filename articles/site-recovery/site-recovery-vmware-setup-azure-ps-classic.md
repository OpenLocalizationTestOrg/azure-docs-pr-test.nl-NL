---
title: " Beheren van een proces-Server die in Azure(Classic) | Microsoft Docs"
description: Dit artikel wordt beschreven hoe tooset van een failback proces Server(Classic) In Azure.
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: eadcc0236c77c9ebbbc885c4a7ee81098f1f4e72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a>Een proces-Server worden uitgevoerd in Azure (klassiek) beheren
> [!div class="op_single_selector"]
> * [Klassieke Azure Portal](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [Resource Manager](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

Tijdens de failback, wordt aangeraden toodeploy processerver in Azure als er hoge latentie tussen hello Azure Virtual Network- en uw on-premises netwerk. Dit artikel wordt beschreven hoe u kunt instellen, configureren en beheren Hallo processervers worden uitgevoerd in Azure.

> [!NOTE]
> Dit artikel is toobe gebruikt als u klassiek als Hallo implementatiemodel voor Hallo virtuele machines tijdens de failover gebruikt. Als u Resource Manager gebruikt als model Volg Hallo implementatiestappen in Hallo [hoe tooset omhoog & Failback processerver (Resource Manager) configureren](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

## <a name="prerequisites"></a>Vereisten

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Processerver op Azure implementeren

1. In Azure Marketplace maakt een virtuele machine met Hallo **Microsoft Azure Site Recovery proces Server V2** </br>
    ![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)
2. Zorg ervoor dat u het implementatiemodel Hallo als selecteert **klassieke** </br>
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)
3. In de wizard Hallo maken van virtuele machine > basisinstellingen, zorg ervoor dat u selecteert Hallo-abonnement en de locatie toowhere failover Hallo virtuele machines.</br>
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)
4. Zorg ervoor dat de virtuele machine Hallo is verbonden toohello Azure Virtual Network toowhich Hallo failover van virtuele machine is verbonden.</br>
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)
5. Zodra Hallo processerver virtuele machine is geconfigureerd, kunt u toolog in nodig en bij Hallo configuratieserver registreren.

> [!NOTE]
> toobe kunnen toouse deze processerver voor failback, moet u tooregister met Hallo lokale configuratie-server.

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>Hallo processerver (uitgevoerd in Azure) tooa configuratieserver (met lokale) registreren

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>Hallo processerver toolatest versie upgraden.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>Registratie Hallo processerver (uitgevoerd in Azure) van een configuratie-Server (lokaal worden uitgevoerd)

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
