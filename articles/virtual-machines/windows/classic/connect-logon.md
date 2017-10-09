---
title: aaaLog op tooa klassieke virtuele machine in Azure | Microsoft Docs
description: Hello Azure portal toolog op tooa Windows virtuele machine gemaakt met het klassieke implementatiemodel hello gebruiken.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 3c1239ed-07dc-48b8-8b3d-dc8c5f0ab20e
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 2e32b7036c2538e73b46580e0f5f8f4979e8a685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="c7133-103">Meld u aan tooa Windows virtuele machine met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="c7133-103">Log on tooa Windows virtual machine using hello Azure portal</span></span>
<span data-ttu-id="c7133-104">In hello Azure-portal, gebruikt u Hallo **Connect** knop toostart een extern bureaublad-sessie en meld u aan tooa virtuele machine van Windows.</span><span class="sxs-lookup"><span data-stu-id="c7133-104">In hello Azure portal, you use hello **Connect** button toostart a Remote Desktop session and log on tooa Windows VM.</span></span>

<span data-ttu-id="c7133-105">Wilt u tooconnect tooa Linux VM?</span><span class="sxs-lookup"><span data-stu-id="c7133-105">Do you want tooconnect tooa Linux VM?</span></span> <span data-ttu-id="c7133-106">Zie [hoe toolog op tooa virtuele machine met Linux](../../linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="c7133-106">See [How toolog on tooa virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="c7133-107">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c7133-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c7133-108">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="c7133-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="c7133-109">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c7133-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="c7133-110">Voor informatie over hoe toolog over het gebruik van tooa VM Resource Manager Hallo model, Zie [hier](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c7133-110">For information about how toolog on tooa VM using hello Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="c7133-111">Verbinding maken met toohello virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c7133-111">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="c7133-112">Meld u aan toohello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c7133-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="c7133-113">Klik op Hallo virtuele machine die u tooaccess wilt.</span><span class="sxs-lookup"><span data-stu-id="c7133-113">Click on hello virtual machine that you want tooaccess.</span></span> <span data-ttu-id="c7133-114">Hallo-naam wordt weergegeven in Hallo **alle resources** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="c7133-114">hello name is listed in hello **All resources** pane.</span></span>

    ![Virtuele-machine-locaties](./media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="c7133-116">Klik op **Connect** op de opdrachtbalk Hallo op Hallo virtuele machine dashboard.</span><span class="sxs-lookup"><span data-stu-id="c7133-116">Click **Connect** on hello command bar atop hello virtual machine dashboard.</span></span>

    ![Pictogram voor Hallo virtuele machine verbinding maken](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="c7133-118">Meld u aan toohello virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c7133-118">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="c7133-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c7133-119">Next steps</span></span>
* <span data-ttu-id="c7133-120">Als hello **Connect** knop is niet actief of er andere problemen met extern bureaublad-verbinding hello, probeert u Hallo-configuratie wordt opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c7133-120">If hello **Connect** button is inactive or you are having other problems with hello Remote Desktop connection, try resetting hello configuration.</span></span> <span data-ttu-id="c7133-121">Klik op **externe toegang opnieuw instellen** vanuit Hallo virtuele machine dashboard.</span><span class="sxs-lookup"><span data-stu-id="c7133-121">click **Reset remote access** from hello virtual machine dashboard.</span></span>

    ![Opnieuw instellen van externe toegang](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="c7133-123">Probeer de fabrieksinstellingen voor problemen met het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="c7133-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="c7133-124">Klik op **wachtwoord opnieuw instellen** langs Hallo de linkerrand van virtuele machine dashboard onder **ondersteuning + probleemoplossing**.</span><span class="sxs-lookup"><span data-stu-id="c7133-124">Click **Reset password** along hello left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Wachtwoord opnieuw instellen](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="c7133-126">Als deze tips werken niet of niet wat u nodig hebt, gaat u naar [tooa van problemen met extern bureaublad-verbindingen op basis van Windows Azure virtuele Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c7133-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="c7133-127">Dit artikel leidt u door het opsporen en oplossen van veelvoorkomende problemen.</span><span class="sxs-lookup"><span data-stu-id="c7133-127">This article walks you through diagnosing and resolving common problems.</span></span>
