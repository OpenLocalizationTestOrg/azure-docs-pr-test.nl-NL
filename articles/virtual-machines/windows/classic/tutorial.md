---
title: een virtuele machine in Azure-portal Hallo aaaCreate | Microsoft Docs
description: Een virtuele Windows-machine maken in hello Azure-portal.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a>Maak een virtuele machine met Windows in hello Azure-portal
> [!div class="op_single_selector"]
> * [Azure Portal](tutorial.md)
> * [PowerShell: Klassieke implementatie](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Meer informatie over hoe te[u deze stappen uitvoert met behulp van Resource Manager-implementatiemodel Hallo](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) met Hallo **Azure-portal**.

Deze zelfstudie leert u hoe toocreate een Azure virtuele machine (VM) met Windows in hello Azure-portal. We een installatiekopie van Windows Server gebruiken als voorbeeld, maar dat is slechts een Hallo veel installatiekopieën van Azure biedt. Houd er rekening mee dat uw opties in de installatiekopie, afhankelijk van uw abonnement. Windows-bureaublad installatiekopieën is bijvoorbeeld mogelijk beschikbaar tooMSDN abonnees.

Deze sectie leest u hoe toouse hello **Dashboard** in Azure portal tooselect Hallo en maak vervolgens Hallo virtuele machine.

U kunt ook maken met virtuele machines met [uw eigen installatiekopieën](createupload-vhd.md). toolearn over deze en andere methoden, Zie [toocreate verschillende manieren een virtuele Windows-machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <a id="createvirtualmachine"></a>Hello virtuele machine maken
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[een virtuele machine maken met Resource Manager-implementatiemodel Hallo](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in hello Azure-portal.
* Meld u aan toohello virtuele machine. Zie voor instructies [tooa virtuele machine met Windows Server aanmelden](connect-logon.md).
* Voeg een schijf toostore gegevens. U kunt zowel leeg schijven en schijven met gegevens koppelen. Zie voor instructies Hallo [koppelen van een data schijf tooa Windows virtuele machine gemaakt met het klassieke implementatiemodel Hallo](attach-disk.md).
