---
title: Het Linux-VM toewijzingsfouten oplossen | Microsoft Docs
description: Toewijzingsfouten bij het maken, opnieuw opstarten of het formaat van een Linux VM in Azure oplossen
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resourece-manager,azure-service-management
ms.assetid: 1ef41144-6dd6-4a56-b180-9d8b3d05eae7
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cjiang
ms.openlocfilehash: c65ede134971c034006781e058c05a82ffb68a19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-linux-vms-in-azure"></a><span data-ttu-id="e2136-103">Toewijzingsfouten bij het maken, opnieuw opstarten of het formaat van Linux virtuele machines in Azure oplossen</span><span class="sxs-lookup"><span data-stu-id="e2136-103">Troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure</span></span>
<span data-ttu-id="e2136-104">Wanneer u een virtuele machine maken, gestopt (toewijzing ongedaan gemaakt) virtuele machines opnieuw opstarten of het formaat van een VM, wijst Microsoft Azure compute-bronnen aan uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="e2136-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources to your subscription.</span></span> <span data-ttu-id="e2136-105">Tijd tot tijd krijgt u fouten bij het uitvoeren van deze bewerkingen--zelfs voordat u de Azure-abonnement limieten bereiken.</span><span class="sxs-lookup"><span data-stu-id="e2136-105">You may occasionally receive errors when performing these operations -- even before you reach the Azure subscription limits.</span></span> <span data-ttu-id="e2136-106">Dit artikel wordt uitgelegd van de oorzaken van een deel van de algemene toewijzingsfouten en mogelijk doorvoeren wordt voorgesteld.</span><span class="sxs-lookup"><span data-stu-id="e2136-106">This article explains the causes of some of the common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="e2136-107">De gegevens zijn mogelijk ook nuttig bij het plannen van de implementatie van uw services.</span><span class="sxs-lookup"><span data-stu-id="e2136-107">The information may also be useful when you plan the deployment of your services.</span></span> <span data-ttu-id="e2136-108">U kunt ook [toewijzingsfouten bij het maken, opnieuw opstarten of vergroten of verkleinen Windows virtuele machines in Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e2136-108">You can also [troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

