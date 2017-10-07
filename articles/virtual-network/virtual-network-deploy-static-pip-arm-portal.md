---
title: een virtuele machine met een statische openbare IP-adres - Azure-portal aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate met een statische openbare IP-adres met een virtuele machine hello Azure-portal.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74d2132785f06148757409ee0a44b98d1e4b98e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a>Een virtuele machine maken met een statische openbare IP-adres met hello Azure-portal

> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI](virtual-network-deploy-static-pip-arm-cli.md)
> * [Sjabloon](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (klassiek)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md). In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel hello aanbeveelt gebruiken.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a>Een virtuele machine maken met een statische openbare IP-adres

toocreate een virtuele machine met een statische openbare IP-adres in hello Azure-portal voltooid Hallo stappen te volgen:

1. Navigeer via een browser toohello [Azure-portal](https://portal.azure.com) en, indien nodig, meld u aan met uw Azure-account.
2. Klik op Hallo bovenste linkerkant hoek van Hallo-portal, **nieuw**>>**Compute**>**Windows Server 2012 R2 Datacenter**.
3. In Hallo **een implementatiemodel selecteren** Selecteer **Resource Manager** en klik op **maken**.
4. In Hallo **basisbeginselen** blade informatie over het Hallo VM invoeren, zoals hieronder wordt weergegeven en klik vervolgens op **OK**.
   
    ![Azure portal - basisbeginselen](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. In Hallo **een grootte kiezen** blade, klikt u op **A1 standaard** zoals hieronder aangegeven, en klik vervolgens op **Selecteer**.
   
    ![Azure-portal - een grootte kiezen](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. In Hallo **instellingen** blade, klikt u op **openbaar IP-adres**, klik dan in Hallo **openbare IP-adres maken** blade onder **toewijzing**, klikt u op **Statische** zoals hieronder wordt weergegeven. En klik vervolgens op **OK**.
   
    ![Azure-portal - openbare IP-adres maken](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. In Hallo **instellingen** blade, klikt u op **OK**.
8. Bekijk Hallo **samenvatting** blade, zoals hieronder wordt weergegeven en klik vervolgens op **OK**.
   
    ![Azure-portal - openbare IP-adres maken](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. Let op de nieuwe tegel Hallo in uw dashboard.
   
    ![Azure-portal - openbare IP-adres maken](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. Zodra Hallo VM is gemaakt, Hallo **instellingen** blade wordt weergegeven zoals hieronder wordt weergegeven
    
    ![Azure-portal - openbare IP-adres maken](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

