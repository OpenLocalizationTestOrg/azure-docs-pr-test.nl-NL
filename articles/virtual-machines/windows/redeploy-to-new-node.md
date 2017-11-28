---
title: aaaRedeploy Windows virtuele machines in Azure | Microsoft Docs
description: Hoe problemen die tooredeploy Windows virtuele machines in Azure toomitigate RDP-verbinding.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: genlin
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: 0ee456ee-4595-4a14-8916-72c9110fc8bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 903d9d5bf241075931ee4b746690c553d808a58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a><span data-ttu-id="a02b2-103">Windows virtuele machine toonew Azure knooppunt opnieuw implementeren</span><span class="sxs-lookup"><span data-stu-id="a02b2-103">Redeploy Windows virtual machine toonew Azure node</span></span>
<span data-ttu-id="a02b2-104">Als u problemen zijn gericht probleemoplossing Remote Desktop (RDP) verbinding of de toepassing toegang tot tooWindows Azure virtuele machine (VM) opnieuw distribueren Hallo VM kan helpen.</span><span class="sxs-lookup"><span data-stu-id="a02b2-104">If you have been facing difficulties troubleshooting Remote Desktop (RDP) connection or application access tooWindows-based Azure virtual machine (VM), redeploying hello VM may help.</span></span> <span data-ttu-id="a02b2-105">Wanneer u een virtuele machine opnieuw implementeert, wordt verplaatst Hallo VM tooa nieuw knooppunt binnen hello Azure-infrastructuur en vervolgens wordt het weer ingeschakeld, alle configuratieopties en bijbehorende bronnen behouden.</span><span class="sxs-lookup"><span data-stu-id="a02b2-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="a02b2-106">Dit artikel ziet u hoe tooredeploy een VM die gebruikmaakt van Azure PowerShell of hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a02b2-106">This article shows you how tooredeploy a VM using Azure PowerShell or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="a02b2-107">Nadat u een virtuele machine opnieuw implementeren, is Hallo tijdelijke schijf verloren en dynamische IP-adressen die zijn gekoppeld aan virtuele netwerkinterface worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="a02b2-107">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 


## <a name="using-azure-powershell"></a><span data-ttu-id="a02b2-108">Azure PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="a02b2-108">Using Azure PowerShell</span></span>
<span data-ttu-id="a02b2-109">Zorg ervoor dat u hebt de nieuwste Azure PowerShell Hallo 1.x op deze computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a02b2-109">Make sure you have hello latest Azure PowerShell 1.x installed on your machine.</span></span> <span data-ttu-id="a02b2-110">Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a02b2-110">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="a02b2-111">Hallo volgende voorbeeld implementeert Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="a02b2-111">hello following example deploys hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="a02b2-112">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a02b2-112">Next steps</span></span>
<span data-ttu-id="a02b2-113">Als u verbinding maken met tooyour VM problemen ondervindt, kunt u Help-informatie vinden op [probleemoplossing RDP-verbindingen](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) of [gedetailleerde stappen voor probleemoplossing RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a02b2-113">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting RDP connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [detailed RDP troubleshooting steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="a02b2-114">Als u geen toegang een toepassing die wordt uitgevoerd op de virtuele machine tot, kunt u ook lezen [toepassing het oplossen van problemen](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a02b2-114">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

