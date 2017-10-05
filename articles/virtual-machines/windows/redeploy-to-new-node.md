---
title: Windows virtuele machines in Azure implementeren | Microsoft Docs
description: Klik hier voor meer informatie over het implementeren van Windows virtuele machines in Azure te verhelpen RDP-verbindingsproblemen.
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
ms.openlocfilehash: a607d0747f64ee6b224d300113905f54e003aef0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="redeploy-windows-virtual-machine-to-new-azure-node"></a><span data-ttu-id="ec376-103">Windows virtuele machine naar de nieuwe Azure knooppunt opnieuw implementeren</span><span class="sxs-lookup"><span data-stu-id="ec376-103">Redeploy Windows virtual machine to new Azure node</span></span>
<span data-ttu-id="ec376-104">Als u problemen zijn gericht kan probleemoplossing Remote Desktop (RDP) verbinding of de toepassing toegang tot Windows Azure virtuele machine (VM) opnieuw distribueren van de virtuele machine helpen.</span><span class="sxs-lookup"><span data-stu-id="ec376-104">If you have been facing difficulties troubleshooting Remote Desktop (RDP) connection or application access to Windows-based Azure virtual machine (VM), redeploying the VM may help.</span></span> <span data-ttu-id="ec376-105">Wanneer u een virtuele machine opnieuw implementeert, wordt de virtuele machine verplaatst naar een nieuw knooppunt in de Azure-infrastructuur en vervolgens wordt het weer ingeschakeld, alle configuratieopties en bijbehorende bronnen behouden.</span><span class="sxs-lookup"><span data-stu-id="ec376-105">When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="ec376-106">In dit artikel leest u hoe een virtuele machine met Azure PowerShell of de Azure-portal opnieuw implementeren.</span><span class="sxs-lookup"><span data-stu-id="ec376-106">This article shows you how to redeploy a VM using Azure PowerShell or the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="ec376-107">Nadat u een virtuele machine opnieuw implementeren, is de tijdelijke schijf verloren en dynamische IP-adressen die zijn gekoppeld aan virtuele netwerkinterface worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="ec376-107">After you redeploy a VM, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 


## <a name="using-azure-powershell"></a><span data-ttu-id="ec376-108">Azure PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="ec376-108">Using Azure PowerShell</span></span>
<span data-ttu-id="ec376-109">Zorg ervoor dat de nieuwste Azure PowerShell 1.x op deze computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ec376-109">Make sure you have the latest Azure PowerShell 1.x installed on your machine.</span></span> <span data-ttu-id="ec376-110">Zie [Azure PowerShell installeren en configureren](/powershell/azure/overview) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ec376-110">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="ec376-111">Het volgende voorbeeld wordt geïmplementeerd voor de virtuele machine met de naam `myVM` in de resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ec376-111">The following example deploys the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="ec376-112">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ec376-112">Next steps</span></span>
<span data-ttu-id="ec376-113">Als u verbinding maakt met uw virtuele machine problemen ondervindt, kunt u Help-informatie vinden op [probleemoplossing RDP-verbindingen](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) of [gedetailleerde stappen voor probleemoplossing RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ec376-113">If you are having issues connecting to your VM, you can find specific help on [troubleshooting RDP connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [detailed RDP troubleshooting steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="ec376-114">Als u geen toegang een toepassing die wordt uitgevoerd op de virtuele machine tot, kunt u ook lezen [toepassing het oplossen van problemen](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ec376-114">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

