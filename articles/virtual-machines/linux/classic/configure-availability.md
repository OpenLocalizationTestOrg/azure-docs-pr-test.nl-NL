---
title: Hiermee stelt u aaaAvailability voor klassieke virtuele Linux-machines | Microsoft Docs
description: Configureer de beschikbaarheidsset voor een nieuwe of bestaande Linux virtuele machine in het klassieke implementatiemodel Hallo met hello Azure-portal en Azure PowerShell.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b8624315-beca-4ec7-8441-2e98b166b548
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2016
ms.author: cynthn
ms.openlocfilehash: 8d8d041e3540e42a1921f5665469a2fdcaa30a29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-availability-set-for-linux-virtual-machines-in-hello-classic-deployment-model"></a><span data-ttu-id="087c7-103">Hoe tooconfigure een beschikbaarheidsset voor virtuele Linux-machines in het klassieke implementatiemodel Hallo</span><span class="sxs-lookup"><span data-stu-id="087c7-103">How tooconfigure an availability set for Linux virtual machines in hello classic deployment model</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="087c7-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="087c7-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="087c7-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="087c7-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="087c7-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="087c7-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="087c7-107">U kunt ook [beschikbaarheidssets configureren](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) in implementaties van Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="087c7-107">You can also [configure availability sets](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) in Resource Manager deployments.</span></span>

[!INCLUDE [virtual-machines-common-classic-configure-availability](../../../../includes/virtual-machines-common-classic-configure-availability.md)]