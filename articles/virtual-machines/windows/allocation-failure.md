---
title: virtuele machine van Windows-toewijzingsfouten aaaTroubleshooting | Microsoft Docs
description: Toewijzingsfouten bij het maken, opnieuw opstarten of het formaat van een Windows-VM in Azure oplossen
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resource-manager,azure-service-management
ms.assetid: bb939e23-77fc-4948-96f7-5037761c30e8
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: cjiang
ms.openlocfilehash: d0cc75ac60d952d8e4310cebc37654dc4f80857f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-windows-vms-in-azure"></a><span data-ttu-id="97a2c-103">Toewijzingsfouten bij het maken, opnieuw opstarten of vergroten of verkleinen Windows virtuele machines in Azure oplossen</span><span class="sxs-lookup"><span data-stu-id="97a2c-103">Troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure</span></span>
<span data-ttu-id="97a2c-104">Wanneer u een virtuele machine maken, gestopt (toewijzing ongedaan gemaakt) virtuele machines opnieuw opstarten of het formaat van een VM, wijst Microsoft Azure compute-bronnen tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="97a2c-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources tooyour subscription.</span></span> <span data-ttu-id="97a2c-105">Tijd tot tijd krijgt u fouten bij het uitvoeren van deze bewerkingen--zelfs voordat u hello Azure-abonnement limieten bereiken.</span><span class="sxs-lookup"><span data-stu-id="97a2c-105">You may occasionally receive errors when performing these operations -- even before you reach hello Azure subscription limits.</span></span> <span data-ttu-id="97a2c-106">In dit artikel wordt uitgelegd Hallo oorzaken van een aantal algemene toewijzingsfouten Hallo en mogelijke herstel wordt voorgesteld.</span><span class="sxs-lookup"><span data-stu-id="97a2c-106">This article explains hello causes of some of hello common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="97a2c-107">Hallo-informatie is mogelijk ook handig wanneer u van plan Hallo-implementatie van uw services bent.</span><span class="sxs-lookup"><span data-stu-id="97a2c-107">hello information may also be useful when you plan hello deployment of your services.</span></span> <span data-ttu-id="97a2c-108">U kunt ook [toewijzingsfouten bij het maken, opnieuw opstarten of vergroten of verkleinen van virtuele Linux-machines in Azure](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="97a2c-108">You can also [troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

