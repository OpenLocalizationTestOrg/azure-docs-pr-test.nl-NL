---
title: aaaCreate FQDN voor een Linux-VM in hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe toocreate een FQDN-naam of FQDN voor een Resource Manager op basis van virtuele machine in hello Azure-portal.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1494a0cb1caa62069c72096a739aee111ac8b383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-linux-vm"></a><span data-ttu-id="2b677-103">Maken van een volledig gekwalificeerde domeinnaam in hello Azure-portal voor een Linux-VM</span><span class="sxs-lookup"><span data-stu-id="2b677-103">Create a fully qualified domain name in hello Azure portal for a Linux VM</span></span>

<span data-ttu-id="2b677-104">Wanneer u een virtuele machine (VM) maakt in Hallo [Azure-portal](https://portal.azure.com), een openbare IP-resource voor Hallo virtuele machine automatisch wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2b677-104">When you create a virtual machine (VM) in hello [Azure portal](https://portal.azure.com), a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="2b677-105">U gebruikt dit IP-adres tooremotely toegang Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="2b677-105">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="2b677-106">Hoewel het Hallo-portal maakt geen een [volledig gekwalificeerde domeinnaam](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), of de FQDN-naam, kunt u een toevoegen wanneer hello VM is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2b677-106">Although hello portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can add one once hello VM is created.</span></span> <span data-ttu-id="2b677-107">Dit artikel wordt gedemonstreerd Hallo stappen toocreate een DNS-naam of FQDN-naam.</span><span class="sxs-lookup"><span data-stu-id="2b677-107">This article demonstrates hello steps toocreate a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="2b677-108">Maken van een FQDN-naam</span><span class="sxs-lookup"><span data-stu-id="2b677-108">Create a FQDN</span></span>
<span data-ttu-id="2b677-109">In dit artikel wordt ervan uitgegaan dat u al een virtuele machine hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2b677-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="2b677-110">Indien nodig, kunt u [maken van een virtuele machine in Hallo portal](quick-create-portal.md) of [Hello Azure CLI](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2b677-110">If needed, you can [create a VM in hello portal](quick-create-portal.md) or [with hello Azure CLI](quick-create-cli.md).</span></span> <span data-ttu-id="2b677-111">Volg deze stappen nadat uw virtuele machine actief is:</span><span class="sxs-lookup"><span data-stu-id="2b677-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="2b677-112">U kunt nu verbinding op afstand toohello VM die gebruikmaakt van de DNS-naam, zoals met `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="2b677-112">You can now connect remotely toohello VM using this DNS name such as with `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b677-113">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2b677-113">Next steps</span></span>
<span data-ttu-id="2b677-114">Nu dat uw virtuele machine een openbare IP-adres en DNS-naam heeft, kunt u implementeren algemene toepassingsframeworks of -services zoals nginx, MongoDB, Docker, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="2b677-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as nginx, MongoDB, Docker, etc.</span></span>

<span data-ttu-id="2b677-115">U kunt ook meer informatie over [met Resource Manager](../../azure-resource-manager/resource-group-overview.md) voor tips over het bouwen van uw Azure-implementaties.</span><span class="sxs-lookup"><span data-stu-id="2b677-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

