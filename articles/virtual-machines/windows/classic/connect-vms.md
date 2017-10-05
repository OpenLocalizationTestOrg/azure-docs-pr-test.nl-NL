---
title: Verbinding maken met Windows-VM's in een cloudservice | Microsoft Docs
description: Verbinding maken met Windows virtuele machines is gemaakt met het klassieke implementatiemodel met een Azure-cloudservice of virtuele netwerk.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c1cbc802-4352-4d2e-9e49-4ccbd955324b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: 0c7a21461e5bb111c4359df8e949d48382b591c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-windows-virtual-machines-created-with-the-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a><span data-ttu-id="e9cbb-103">Verbinding maken met Windows virtuele machines is gemaakt met het klassieke implementatiemodel met een virtueel netwerk of cloud-service</span><span class="sxs-lookup"><span data-stu-id="e9cbb-103">Connect Windows virtual machines created with the classic deployment model with a virtual network or cloud service</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e9cbb-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e9cbb-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e9cbb-105">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="e9cbb-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="e9cbb-106">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e9cbb-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="e9cbb-107">Windows virtuele machines is gemaakt met het klassieke implementatiemodel worden altijd geplaatst in een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="e9cbb-107">Windows virtual machines created with the classic deployment model are always placed in a cloud service.</span></span> <span data-ttu-id="e9cbb-108">De cloudservice fungeert als een container en biedt een unieke openbare DNS-naam, een openbare IP-adres en een set eindpunten voor toegang tot de virtuele machine via het Internet.</span><span class="sxs-lookup"><span data-stu-id="e9cbb-108">The cloud service acts as a container and provides a unique public DNS name, a public IP address, and a set of endpoints to access the virtual machine over the Internet.</span></span> <span data-ttu-id="e9cbb-109">De cloudservice kan zich in een virtueel netwerk, maar is geen vereiste.</span><span class="sxs-lookup"><span data-stu-id="e9cbb-109">The cloud service can be in a virtual network, but that's not a requirement.</span></span> <span data-ttu-id="e9cbb-110">U kunt ook [virtuele Linux-machines verbinding met een virtueel netwerk of cloud service](../../linux/classic/connect-vms.md).</span><span class="sxs-lookup"><span data-stu-id="e9cbb-110">You can also [connect Linux virtual machines with a virtual network or cloud service](../../linux/classic/connect-vms.md).</span></span>

<span data-ttu-id="e9cbb-111">Als een cloudservice niet in een virtueel netwerk, er sprake een *zelfstandige* cloudservice.</span><span class="sxs-lookup"><span data-stu-id="e9cbb-111">If a cloud service isn't in a virtual network, it's called a *standalone* cloud service.</span></span> <span data-ttu-id="e9cbb-112">De virtuele machines in een zelfstandige cloudservice communiceren met andere virtuele machines met behulp van de andere virtuele machines de openbare DNS-namen, en het verkeer wordt verzonden via Internet.</span><span class="sxs-lookup"><span data-stu-id="e9cbb-112">The virtual machines in a standalone cloud service communicate with other virtual machines by using the other virtual machines’ public DNS names, and the traffic travels over the Internet.</span></span> <span data-ttu-id="e9cbb-113">Als een service in de cloud zich in een virtueel netwerk, kan de virtuele machines in de cloudservice zonder verkeer verzenden via Internet communiceren met andere virtuele machines in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="e9cbb-113">If a cloud service is in a virtual network, the virtual machines in that cloud service can communicate with all other virtual machines in the virtual network without sending any traffic over the Internet.</span></span>

<span data-ttu-id="e9cbb-114">Als u uw virtuele machines in dezelfde zelfstandige cloudservice plaatst, kunt u nog steeds gebruiken voor taakverdeling en beschikbaarheidssets.</span><span class="sxs-lookup"><span data-stu-id="e9cbb-114">If you place your virtual machines in the same standalone cloud service, you can still use load balancing and availability sets.</span></span> <span data-ttu-id="e9cbb-115">Zie voor meer informatie [taakverdeling van virtuele machines](../../virtual-machines-windows-load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en [de beschikbaarheid van virtuele machines beheren](../../virtual-machines-windows-manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e9cbb-115">For details, see [Load balancing virtual machines](../../virtual-machines-windows-load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Manage the availability of virtual machines](../../virtual-machines-windows-manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="e9cbb-116">U kan echter ordenen van de virtuele machines op subnetten of een zelfstandige cloudservice verbinding met uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="e9cbb-116">However, you can't organize the virtual machines on subnets or connect a standalone cloud service to your on-premises network.</span></span> <span data-ttu-id="e9cbb-117">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e9cbb-117">Here's an example:</span></span>

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a><span data-ttu-id="e9cbb-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e9cbb-118">Next steps</span></span>
<span data-ttu-id="e9cbb-119">Nadat u een virtuele machine maakt, is het een goed idee om [een gegevensschijf toevoegen](attach-disk.md) zodat uw services en werkbelastingen hebt een locatie voor het opslaan van gegevens.</span><span class="sxs-lookup"><span data-stu-id="e9cbb-119">After you create a virtual machine, it's a good idea to [add a data disk](attach-disk.md) so your services and workloads have a location to store data.</span></span>
