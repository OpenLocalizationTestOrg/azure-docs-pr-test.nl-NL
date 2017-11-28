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
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a><span data-ttu-id="7f32b-103">Een virtuele machine maken met een statische openbare IP-adres met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="7f32b-103">Create a VM with a static public IP address using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f32b-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7f32b-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="7f32b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f32b-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="7f32b-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7f32b-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="7f32b-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="7f32b-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="7f32b-108">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="7f32b-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="7f32b-109">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7f32b-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7f32b-110">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel hello aanbeveelt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7f32b-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a><span data-ttu-id="7f32b-111">Een virtuele machine maken met een statische openbare IP-adres</span><span class="sxs-lookup"><span data-stu-id="7f32b-111">Create a VM with a static public IP</span></span>

<span data-ttu-id="7f32b-112">toocreate een virtuele machine met een statische openbare IP-adres in hello Azure-portal voltooid Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7f32b-112">toocreate a VM with a static public IP address in hello Azure portal, complete hello following steps:</span></span>

1. <span data-ttu-id="7f32b-113">Navigeer via een browser toohello [Azure-portal](https://portal.azure.com) en, indien nodig, meld u aan met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="7f32b-113">From a browser, navigate toohello [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="7f32b-114">Klik op Hallo bovenste linkerkant hoek van Hallo-portal, **nieuw**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="7f32b-114">On hello top left hand corner of hello portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span></span>
3. <span data-ttu-id="7f32b-115">In Hallo **een implementatiemodel selecteren** Selecteer **Resource Manager** en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="7f32b-115">In hello **Select a deployment model** list, select **Resource Manager** and click **Create**.</span></span>
4. <span data-ttu-id="7f32b-116">In Hallo **basisbeginselen** blade informatie over het Hallo VM invoeren, zoals hieronder wordt weergegeven en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7f32b-116">In hello **Basics** blade, enter hello VM information as shown below, and then click **OK**.</span></span>
   
    ![Azure portal - basisbeginselen](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. <span data-ttu-id="7f32b-118">In Hallo **een grootte kiezen** blade, klikt u op **A1 standaard** zoals hieronder aangegeven, en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="7f32b-118">In hello **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span></span>
   
    ![Azure-portal - een grootte kiezen](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. <span data-ttu-id="7f32b-120">In Hallo **instellingen** blade, klikt u op **openbaar IP-adres**, klik dan in Hallo **openbare IP-adres maken** blade onder **toewijzing**, klikt u op **Statische** zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7f32b-120">In hello **Settings** blade, click **Public IP address**, then in hello **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span></span> <span data-ttu-id="7f32b-121">En klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7f32b-121">And then click **OK**.</span></span>
   
    ![Azure-portal - openbare IP-adres maken](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. <span data-ttu-id="7f32b-123">In Hallo **instellingen** blade, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7f32b-123">In hello **Settings** blade, click **OK**.</span></span>
8. <span data-ttu-id="7f32b-124">Bekijk Hallo **samenvatting** blade, zoals hieronder wordt weergegeven en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7f32b-124">Review hello **Summary** blade, as shown below, and then click **OK**.</span></span>
   
    ![Azure-portal - openbare IP-adres maken](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. <span data-ttu-id="7f32b-126">Let op de nieuwe tegel Hallo in uw dashboard.</span><span class="sxs-lookup"><span data-stu-id="7f32b-126">Notice hello new tile in your dashboard.</span></span>
   
    ![Azure-portal - openbare IP-adres maken](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. <span data-ttu-id="7f32b-128">Zodra Hallo VM is gemaakt, Hallo **instellingen** blade wordt weergegeven zoals hieronder wordt weergegeven</span><span class="sxs-lookup"><span data-stu-id="7f32b-128">Once hello VM is created, hello **Settings** blade will be displayed as shown below</span></span>
    
    ![Azure-portal - openbare IP-adres maken](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

