---
title: Een virtuele machine maken met statische openbare IP-adres - Azure-portal | Microsoft Docs
description: Informatie over het maken van een virtuele machine met een statische openbare IP-adres met de Azure portal.
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
ms.openlocfilehash: 233e4eea8439320c1c7446e2c2b2e9d379351a3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-the-azure-portal"></a><span data-ttu-id="76f56-103">Een virtuele machine maken met een statische openbare IP-adres met de Azure portal</span><span class="sxs-lookup"><span data-stu-id="76f56-103">Create a VM with a static public IP address using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="76f56-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="76f56-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="76f56-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="76f56-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="76f56-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="76f56-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="76f56-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="76f56-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="76f56-108">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="76f56-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="76f56-109">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="76f56-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="76f56-110">In dit artikel wordt behandeld met het implementatiemodel van Resource Manager, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel aanbeveelt.</span><span class="sxs-lookup"><span data-stu-id="76f56-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a><span data-ttu-id="76f56-111">Een virtuele machine maken met een statische openbare IP-adres</span><span class="sxs-lookup"><span data-stu-id="76f56-111">Create a VM with a static public IP</span></span>

<span data-ttu-id="76f56-112">Als een virtuele machine maken met een statische openbare IP-adres in de Azure portal, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="76f56-112">To create a VM with a static public IP address in the Azure portal, complete the following steps:</span></span>

1. <span data-ttu-id="76f56-113">Navigeer via een browser naar de [Azure Portal](https://portal.azure.com) en log, indien nodig, in met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="76f56-113">From a browser, navigate to the [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="76f56-114">Klik op de bovenste linkerkant hoek van de portal, **nieuw**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="76f56-114">On the top left hand corner of the portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span></span>
3. <span data-ttu-id="76f56-115">In de **een implementatiemodel selecteren** Selecteer **Resource Manager** en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="76f56-115">In the **Select a deployment model** list, select **Resource Manager** and click **Create**.</span></span>
4. <span data-ttu-id="76f56-116">In de **basisbeginselen** blade, geef de VM-informatie, zoals hieronder wordt weergegeven en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="76f56-116">In the **Basics** blade, enter the VM information as shown below, and then click **OK**.</span></span>
   
    ![Azure portal - basisbeginselen](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. <span data-ttu-id="76f56-118">In de **een grootte kiezen** blade, klikt u op **A1 standaard** zoals hieronder aangegeven, en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="76f56-118">In the **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span></span>
   
    ![Azure-portal - een grootte kiezen](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. <span data-ttu-id="76f56-120">In de **instellingen** blade, klikt u op **openbaar IP-adres**, klik dan in de **openbare IP-adres maken** blade onder **toewijzing**, klikt u op **statische** zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="76f56-120">In the **Settings** blade, click **Public IP address**, then in the **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span></span> <span data-ttu-id="76f56-121">En klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="76f56-121">And then click **OK**.</span></span>
   
    ![Azure-portal - openbare IP-adres maken](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. <span data-ttu-id="76f56-123">In de **instellingen** blade, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="76f56-123">In the **Settings** blade, click **OK**.</span></span>
8. <span data-ttu-id="76f56-124">Controleer de **samenvatting** blade, zoals hieronder wordt weergegeven en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="76f56-124">Review the **Summary** blade, as shown below, and then click **OK**.</span></span>
   
    ![Azure-portal - openbare IP-adres maken](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. <span data-ttu-id="76f56-126">Let op de nieuwe tegel in uw dashboard.</span><span class="sxs-lookup"><span data-stu-id="76f56-126">Notice the new tile in your dashboard.</span></span>
   
    ![Azure-portal - openbare IP-adres maken](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. <span data-ttu-id="76f56-128">Zodra de virtuele machine is gemaakt, de **instellingen** blade wordt weergegeven zoals hieronder wordt weergegeven</span><span class="sxs-lookup"><span data-stu-id="76f56-128">Once the VM is created, the **Settings** blade will be displayed as shown below</span></span>
    
    ![Azure-portal - openbare IP-adres maken](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

