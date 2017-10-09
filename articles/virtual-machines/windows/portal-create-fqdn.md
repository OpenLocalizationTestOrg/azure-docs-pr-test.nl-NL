---
title: aaaCreate FQDN-naam voor een virtuele machine van Windows in hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe toocreate een FQDN-naam of FQDN voor een Resource Manager op basis van virtuele machine in hello Azure-portal.
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
ms.openlocfilehash: 67c817ec97073803e513bc41ebde67b75ced565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-windows-vm"></a><span data-ttu-id="93c5f-103">Maken van een volledig gekwalificeerde domeinnaam in hello Azure-portal voor een virtuele machine van Windows</span><span class="sxs-lookup"><span data-stu-id="93c5f-103">Create a fully qualified domain name in hello Azure portal for a Windows VM</span></span>

<span data-ttu-id="93c5f-104">Wanneer u een virtuele machine (VM) maakt in Hallo [Azure-portal](https://portal.azure.com), een openbare IP-resource voor Hallo virtuele machine automatisch wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="93c5f-104">When you create a virtual machine (VM) in hello [Azure portal](https://portal.azure.com), a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="93c5f-105">U gebruikt dit IP-adres tooremotely toegang Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="93c5f-105">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="93c5f-106">Hoewel het Hallo-portal maakt geen een [volledig gekwalificeerde domeinnaam](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), of de FQDN-naam, kunt u een zodra hello VM is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="93c5f-106">Although hello portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can create one once hello VM is created.</span></span> <span data-ttu-id="93c5f-107">Dit artikel wordt gedemonstreerd Hallo stappen toocreate een DNS-naam of FQDN-naam.</span><span class="sxs-lookup"><span data-stu-id="93c5f-107">This article demonstrates hello steps toocreate a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="93c5f-108">Maken van een FQDN-naam</span><span class="sxs-lookup"><span data-stu-id="93c5f-108">Create a FQDN</span></span>
<span data-ttu-id="93c5f-109">In dit artikel wordt ervan uitgegaan dat u al een virtuele machine hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="93c5f-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="93c5f-110">Indien nodig, kunt u [maken van een virtuele machine in Hallo portal](quick-create-portal.md) of [met Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="93c5f-110">If needed, you can [create a VM in hello portal](quick-create-portal.md) or [with Azure PowerShell](quick-create-powershell.md).</span></span> <span data-ttu-id="93c5f-111">Volg deze stappen nadat uw virtuele machine actief is:</span><span class="sxs-lookup"><span data-stu-id="93c5f-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="93c5f-112">U kunt nu verbinding op afstand toohello VM die gebruikmaakt van deze DNS-naam, zoals voor Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="93c5f-112">You can now connect remotely toohello VM using this DNS name such as for Remote Desktop Protocol (RDP).</span></span>

## <a name="next-steps"></a><span data-ttu-id="93c5f-113">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="93c5f-113">Next steps</span></span>
<span data-ttu-id="93c5f-114">Nu dat uw virtuele machine een openbare IP-adres en DNS-naam heeft, kunt u algemene toepassingsframeworks of services, zoals IIS, SQL en SharePoint kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="93c5f-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as IIS, SQL, or SharePoint.</span></span>

<span data-ttu-id="93c5f-115">U kunt ook meer informatie over [met Resource Manager](../../azure-resource-manager/resource-group-overview.md) voor tips over het bouwen van uw Azure-implementaties.</span><span class="sxs-lookup"><span data-stu-id="93c5f-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

