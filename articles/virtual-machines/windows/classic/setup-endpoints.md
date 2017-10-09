---
title: aaaSet eindpunten op een klassieke Windows-VM | Microsoft Docs
description: Informatie over tooset eindpunten voor een Windows-VM in hello Azure classic portal tooallow communicatie met een virtuele Windows-machine in Azure.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="3f3ca-103">Hoe tooset eindpunten op een klassieke Windows-virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="3f3ca-103">How tooset up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="3f3ca-104">Alle Windows virtuele machines die u maakt in Azure met behulp van het klassieke implementatiemodel Hallo automatisch kan communiceren via een particulier netwerkkanaal met andere virtuele machines in Hallo dezelfde cloudservice of een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-104">All Windows virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="3f3ca-105">Computers op Hallo Internet of een andere virtuele netwerken vereisen echter eindpunten toodirect Hallo netwerk binnenkomend verkeer tooa virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="3f3ca-106">In dit artikel is ook beschikbaar voor [virtuele Linux-machines](../../linux/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="3f3ca-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f3ca-107">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3f3ca-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3f3ca-108">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="3f3ca-109">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="3f3ca-110">In Hallo **Resource Manager** implementatiemodel eindpunten zijn geconfigureerd met behulp van **Netwerkbeveiligingsgroepen (nsg's)**.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="3f3ca-111">Zie voor meer informatie [toestaan externe toegang tooyour virtuele machine met behulp van Azure-portal Hallo](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3f3ca-111">For more information, see [Allow external access tooyour VM using hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="3f3ca-112">Wanneer u een virtuele Windows-computer in hello Azure-portal maakt, worden algemene eindpunten zoals die voor extern bureaublad- en Windows PowerShell voor externe toegang doorgaans automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-112">When you create a Windows virtual machine in hello Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="3f3ca-113">Tijdens het maken van Hallo virtuele machine of daarna indien nodig, kunt u extra eindpunten configureren.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="3f3ca-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f3ca-114">Next steps</span></span>
* <span data-ttu-id="3f3ca-115">een Azure PowerShell-cmdlet tooset u een eindpunt VM toouse Zie [toevoegen AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f3ca-115">toouse an Azure PowerShell cmdlet tooset up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="3f3ca-116">een Azure PowerShell-cmdlet toomanage een ACL voor een eindpunt toouse Zie [beheren toegangsbeheerlijsten (ACL's) voor eindpunten met behulp van PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3f3ca-116">toouse an Azure PowerShell cmdlet toomanage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="3f3ca-117">Als u een virtuele machine hebt gemaakt in Hallo Resource Manager-implementatiemodel, kunt u Azure PowerShell te gebruiken[netwerk beveiligingsgroepen maken](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol verkeer toohello VM.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-117">If you created a virtual machine in hello Resource Manager deployment model, you can use Azure PowerShell too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol traffic toohello VM.</span></span>
