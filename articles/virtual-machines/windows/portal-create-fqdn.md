---
title: FQDN-naam voor een virtuele machine van Windows in de Azure portal maken | Microsoft Docs
description: Informatie over het maken van een FQDN-naam of FQDN-naam voor een Resource Manager gebaseerde virtuele machine in de Azure-portal.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2d5a555cd873222efcdb29e8eb3aaf128a24414b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-qualified-domain-name-in-the-azure-portal-for-a-windows-vm"></a><span data-ttu-id="1a102-103">Een volledig gekwalificeerde domeinnaam in de Azure portal maken voor een virtuele machine van Windows</span><span class="sxs-lookup"><span data-stu-id="1a102-103">Create a fully qualified domain name in the Azure portal for a Windows VM</span></span>

<span data-ttu-id="1a102-104">Wanneer u een virtuele machine (VM) maakt in de [Azure-portal](https://portal.azure.com), een openbare IP-resource voor de virtuele machine automatisch wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1a102-104">When you create a virtual machine (VM) in the [Azure portal](https://portal.azure.com), a public IP resource for the virtual machine is automatically created.</span></span> <span data-ttu-id="1a102-105">U kunt dit IP-adres gebruiken voor externe toegang tot de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1a102-105">You use this IP address to remotely access the VM.</span></span> <span data-ttu-id="1a102-106">Hoewel de portal geen maakt een [volledig gekwalificeerde domeinnaam](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), of de FQDN-naam, kunt u een zodra de virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1a102-106">Although the portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can create one once the VM is created.</span></span> <span data-ttu-id="1a102-107">In dit artikel ziet u de stappen voor het maken van een DNS-naam of FQDN-naam.</span><span class="sxs-lookup"><span data-stu-id="1a102-107">This article demonstrates the steps to create a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="1a102-108">Maken van een FQDN-naam</span><span class="sxs-lookup"><span data-stu-id="1a102-108">Create a FQDN</span></span>
<span data-ttu-id="1a102-109">In dit artikel wordt ervan uitgegaan dat u al een virtuele machine hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1a102-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="1a102-110">Indien nodig, kunt u [maken van een virtuele machine in de portal](quick-create-portal.md) of [met Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1a102-110">If needed, you can [create a VM in the portal](quick-create-portal.md) or [with Azure PowerShell](quick-create-powershell.md).</span></span> <span data-ttu-id="1a102-111">Volg deze stappen nadat uw virtuele machine actief is:</span><span class="sxs-lookup"><span data-stu-id="1a102-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="1a102-112">U kunt nu op afstand verbinding met de virtuele machine met behulp van deze DNS-naam, zoals voor Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="1a102-112">You can now connect remotely to the VM using this DNS name such as for Remote Desktop Protocol (RDP).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a102-113">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1a102-113">Next steps</span></span>
<span data-ttu-id="1a102-114">Nu dat uw virtuele machine een openbare IP-adres en DNS-naam heeft, kunt u algemene toepassingsframeworks of services, zoals IIS, SQL en SharePoint kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="1a102-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as IIS, SQL, or SharePoint.</span></span>

<span data-ttu-id="1a102-115">U kunt ook meer informatie over [met Resource Manager](../../azure-resource-manager/resource-group-overview.md) voor tips over het bouwen van uw Azure-implementaties.</span><span class="sxs-lookup"><span data-stu-id="1a102-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

