---
title: Eindpunten van een klassieke Linux VM instellen | Microsoft Docs
description: Informatie over het instellen van eindpunten voor een Linux-VM in de klassieke Azure portal voor de communicatie met een virtuele Linux-machine in Azure
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
ms.openlocfilehash: 4fd8b847b0f60648d1661ce5a8667c641e616ed4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="d0f85-103">Het instellen van eindpunten op een Linux klassieke virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="d0f85-103">How to set up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="d0f85-104">Alle Linux virtuele machines die u maakt in Azure met behulp van het klassieke implementatiemodel kunnen automatisch via een particulier netwerkkanaal met andere virtuele machines in dezelfde cloudservice- of virtueel netwerk communiceren.</span><span class="sxs-lookup"><span data-stu-id="d0f85-104">All Linux virtual machines that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="d0f85-105">Computers op Internet of een andere virtuele netwerken vereisen echter eindpunten het binnenkomend netwerkverkeer naar een virtuele machine wordt omgeleid.</span><span class="sxs-lookup"><span data-stu-id="d0f85-105">However, computers on the Internet or other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="d0f85-106">In dit artikel is ook beschikbaar voor [Windows virtuele machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d0f85-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d0f85-107">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d0f85-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d0f85-108">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="d0f85-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="d0f85-109">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d0f85-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="d0f85-110">In de **Resource Manager** implementatiemodel eindpunten zijn geconfigureerd met behulp van **Netwerkbeveiligingsgroepen (nsg's)**.</span><span class="sxs-lookup"><span data-stu-id="d0f85-110">In the **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="d0f85-111">Zie voor meer informatie [openen van poorten en eindpunten](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d0f85-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d0f85-112">Wanneer u een virtuele Linux-machine in de Azure portal maakt, wordt een eindpunt voor Secure Shell (SSH) doorgaans automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d0f85-112">When you create a Linux virtual machine in the Azure portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="d0f85-113">Tijdens het maken van de virtuele machine of daarna indien nodig, kunt u extra eindpunten configureren.</span><span class="sxs-lookup"><span data-stu-id="d0f85-113">You can configure additional endpoints while creating the virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="d0f85-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d0f85-114">Next steps</span></span>
* <span data-ttu-id="d0f85-115">U kunt ook een VM-eindpunt maken met behulp van de [Azure-opdrachtregelinterface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="d0f85-115">You can also create a VM endpoint by using the [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="d0f85-116">Voer de **azure vm-eindpunt maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="d0f85-116">Run the **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="d0f85-117">Als u een virtuele machine hebt gemaakt in het Resource Manager-implementatiemodel, kunt u de Azure CLI gebruiken in de modus Resource Manager voor [netwerk beveiligingsgroepen maken](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) aan verkeer voor beheer met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d0f85-117">If you created a virtual machine in the Resource Manager deployment model, you can use the Azure CLI in Resource Manager mode to [create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) to control traffic to the VM.</span></span>
