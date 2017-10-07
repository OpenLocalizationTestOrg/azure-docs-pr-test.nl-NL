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
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a>Windows virtuele machine toonew Azure knooppunt opnieuw implementeren
Als u problemen zijn gericht probleemoplossing Remote Desktop (RDP) verbinding of de toepassing toegang tot tooWindows Azure virtuele machine (VM) opnieuw distribueren Hallo VM kan helpen. Wanneer u een virtuele machine opnieuw implementeert, wordt verplaatst Hallo VM tooa nieuw knooppunt binnen hello Azure-infrastructuur en vervolgens wordt het weer ingeschakeld, alle configuratieopties en bijbehorende bronnen behouden. Dit artikel ziet u hoe tooredeploy een VM die gebruikmaakt van Azure PowerShell of hello Azure-portal.

> [!NOTE]
> Nadat u een virtuele machine opnieuw implementeren, is Hallo tijdelijke schijf verloren en dynamische IP-adressen die zijn gekoppeld aan virtuele netwerkinterface worden bijgewerkt. 


## <a name="using-azure-powershell"></a>Azure PowerShell gebruiken
Zorg ervoor dat u hebt de nieuwste Azure PowerShell Hallo 1.x op deze computer geïnstalleerd. Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

Hallo volgende voorbeeld implementeert Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Volgende stappen
Als u verbinding maken met tooyour VM problemen ondervindt, kunt u Help-informatie vinden op [probleemoplossing RDP-verbindingen](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) of [gedetailleerde stappen voor probleemoplossing RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Als u geen toegang een toepassing die wordt uitgevoerd op de virtuele machine tot, kunt u ook lezen [toepassing het oplossen van problemen](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

