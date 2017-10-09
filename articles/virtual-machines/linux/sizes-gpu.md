---
title: aaaAzure Linux VM-groottes - GPU | Microsoft Docs
description: Geeft een lijst Hallo verschillende GPU geoptimaliseerd grootten beschikbaar voor virtuele Linux-machines in Azure.
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: e98f720499be37df4048aeb513aa4f6b187b7335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="gpu-linux-vm-sizes"></a><span data-ttu-id="b9ed8-103">GPU Linux VM-grootten</span><span class="sxs-lookup"><span data-stu-id="b9ed8-103">GPU Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

<span data-ttu-id="b9ed8-104">Zie voor stuurprogramma-installatie- en verificatiestappen stappen [N-reeks stuurprogramma-instellingen voor Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="b9ed8-104">For driver installation and verification steps, see [N-series driver setup for Linux](n-series-driver-setup.md).</span></span>

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* <span data-ttu-id="b9ed8-105">We adviseren niet te installeren X server of andere systemen die gebruikmaken van Hallo nouveau stuurprogramma op Ubuntu NC-virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b9ed8-105">We don't recommend installing X server or other systems that use hello nouveau driver on Ubuntu NC VMs.</span></span> <span data-ttu-id="b9ed8-106">Voordat u NVIDIA GPU-stuurprogramma's installeert, moet u toodisable hello nouveau stuurprogramma.</span><span class="sxs-lookup"><span data-stu-id="b9ed8-106">Before installing NVIDIA GPU drivers, you need toodisable hello nouveau driver.</span></span>  

## <a name="other-sizes"></a><span data-ttu-id="b9ed8-107">Andere grootten</span><span class="sxs-lookup"><span data-stu-id="b9ed8-107">Other sizes</span></span>
- [<span data-ttu-id="b9ed8-108">Algemeen doel</span><span class="sxs-lookup"><span data-stu-id="b9ed8-108">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="b9ed8-109">Geoptimaliseerde rekenkracht</span><span class="sxs-lookup"><span data-stu-id="b9ed8-109">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="b9ed8-110">Geoptimaliseerd geheugen</span><span class="sxs-lookup"><span data-stu-id="b9ed8-110">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="b9ed8-111">Geoptimaliseerde opslag</span><span class="sxs-lookup"><span data-stu-id="b9ed8-111">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="b9ed8-112">Krachtig rekenvermogen</span><span class="sxs-lookup"><span data-stu-id="b9ed8-112">High performance compute</span></span>](sizes-hpc.md)

## <a name="next-steps"></a><span data-ttu-id="b9ed8-113">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b9ed8-113">Next steps</span></span>
<span data-ttu-id="b9ed8-114">Meer informatie over het [Azure compute-eenheden (ACU)](acu.md) kunt u de prestaties van Azure-SKU's met elkaar vergelijken.</span><span class="sxs-lookup"><span data-stu-id="b9ed8-114">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>