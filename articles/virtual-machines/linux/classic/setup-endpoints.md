---
title: aaaSet eindpunten op een klassieke Linux VM | Microsoft Docs
description: Meer informatie over tooset eindpunten voor een Linux-VM in hello Azure classic portal tooallow communicatie met een virtuele Linux-machine in Azure
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="084c2-103">Hoe tooset eindpunten op een Linux klassieke virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="084c2-103">How tooset up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="084c2-104">Alle Linux virtuele machines die u maakt in Azure met behulp van het klassieke implementatiemodel Hallo kan automatisch communiceren via een particulier netwerkkanaal met andere virtuele machines in Hallo dat dezelfde cloud service- of virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="084c2-104">All Linux virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="084c2-105">Computers op Hallo Internet of een andere virtuele netwerken vereisen echter eindpunten toodirect Hallo netwerk binnenkomend verkeer tooa virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="084c2-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="084c2-106">In dit artikel is ook beschikbaar voor [Windows virtuele machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="084c2-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="084c2-107">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="084c2-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="084c2-108">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="084c2-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="084c2-109">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="084c2-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="084c2-110">In Hallo **Resource Manager** implementatiemodel eindpunten zijn geconfigureerd met behulp van **Netwerkbeveiligingsgroepen (nsg's)**.</span><span class="sxs-lookup"><span data-stu-id="084c2-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="084c2-111">Zie voor meer informatie [openen van poorten en eindpunten](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="084c2-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="084c2-112">Wanneer u een virtuele Linux-machine in hello Azure-portal maakt, wordt een eindpunt voor Secure Shell (SSH) doorgaans automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="084c2-112">When you create a Linux virtual machine in hello Azure portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="084c2-113">Tijdens het maken van Hallo virtuele machine of daarna indien nodig, kunt u extra eindpunten configureren.</span><span class="sxs-lookup"><span data-stu-id="084c2-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="084c2-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="084c2-114">Next steps</span></span>
* <span data-ttu-id="084c2-115">U kunt ook een VM-eindpunt maken met behulp van Hallo [Azure-opdrachtregelinterface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="084c2-115">You can also create a VM endpoint by using hello [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="084c2-116">Voer Hallo **azure vm-eindpunt maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="084c2-116">Run hello **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="084c2-117">Als u een virtuele machine hebt gemaakt in Hallo Resource Manager-implementatiemodel, kunt u hello Azure CLI in de modus Resource Manager te gebruiken[netwerk beveiligingsgroepen maken](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol verkeer toohello VM.</span><span class="sxs-lookup"><span data-stu-id="084c2-117">If you created a virtual machine in hello Resource Manager deployment model, you can use hello Azure CLI in Resource Manager mode too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol traffic toohello VM.</span></span>
