---
title: Eindpunten van een klassieke Windows-VM instellen | Microsoft Docs
description: Informatie over het instellen van eindpunten voor een virtuele machine van Windows in de klassieke Azure portal voor de communicatie met een virtuele Windows-machine in Azure.
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
ms.openlocfilehash: 60861819a7e437bb715b14c0e8eaf74f13b33ebf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="99cbc-103">Het instellen van de eindpunten van een klassieke Windows-virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="99cbc-103">How to set up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="99cbc-104">Alle Windows kan de virtuele machines die u maakt in Azure met behulp van het klassieke implementatiemodel automatisch communiceren via een particulier netwerkkanaal met andere virtuele machines in dezelfde cloudservice- of virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="99cbc-104">All Windows virtual machines that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="99cbc-105">Computers op Internet of een andere virtuele netwerken vereisen echter eindpunten het binnenkomend netwerkverkeer naar een virtuele machine wordt omgeleid.</span><span class="sxs-lookup"><span data-stu-id="99cbc-105">However, computers on the Internet or other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="99cbc-106">In dit artikel is ook beschikbaar voor [virtuele Linux-machines](../../linux/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="99cbc-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99cbc-107">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="99cbc-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="99cbc-108">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="99cbc-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="99cbc-109">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="99cbc-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="99cbc-110">In de **Resource Manager** implementatiemodel eindpunten zijn geconfigureerd met behulp van **Netwerkbeveiligingsgroepen (nsg's)**.</span><span class="sxs-lookup"><span data-stu-id="99cbc-110">In the **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="99cbc-111">Zie voor meer informatie [toestaan van externe toegang tot uw virtuele machine met de Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="99cbc-111">For more information, see [Allow external access to your VM using the Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="99cbc-112">Wanneer u een virtuele Windows-computer in de Azure portal maakt, worden algemene eindpunten zoals die voor extern bureaublad- en Windows PowerShell voor externe toegang doorgaans automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="99cbc-112">When you create a Windows virtual machine in the Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="99cbc-113">Tijdens het maken van de virtuele machine of daarna indien nodig, kunt u extra eindpunten configureren.</span><span class="sxs-lookup"><span data-stu-id="99cbc-113">You can configure additional endpoints while creating the virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="99cbc-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="99cbc-114">Next steps</span></span>
* <span data-ttu-id="99cbc-115">Zie voor het gebruik van een Azure PowerShell-cmdlet voor het instellen van een VM-eindpunt, [toevoegen AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="99cbc-115">To use an Azure PowerShell cmdlet to set up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="99cbc-116">Zie voor het gebruik van een Azure PowerShell-cmdlet voor het beheren van een ACL voor een eindpunt, [beheren toegangsbeheerlijsten (ACL's) voor eindpunten met behulp van PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="99cbc-116">To use an Azure PowerShell cmdlet to manage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="99cbc-117">Als u een virtuele machine hebt gemaakt in het Resource Manager-implementatiemodel, kunt u Azure PowerShell te [netwerk beveiligingsgroepen maken](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) aan verkeer voor beheer met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="99cbc-117">If you created a virtual machine in the Resource Manager deployment model, you can use Azure PowerShell to [create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) to control traffic to the VM.</span></span>
