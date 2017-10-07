---
title: aaaSet eindpunten op een klassieke Linux VM | Microsoft Docs
description: Meer informatie over tooset eindpunten voor een Linux-VM in hello Azure classic portal tooallow communicatie met een virtuele Linux-machine in Azure
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a>Hoe tooset eindpunten op een Linux klassieke virtuele machine in Azure
Alle Linux virtuele machines die u maakt in Azure met behulp van het klassieke implementatiemodel Hallo kan automatisch communiceren via een particulier netwerkkanaal met andere virtuele machines in Hallo dat dezelfde cloud service- of virtuele netwerk. Computers op Hallo Internet of een andere virtuele netwerken vereisen echter eindpunten toodirect Hallo netwerk binnenkomend verkeer tooa virtuele machine. In dit artikel is ook beschikbaar voor [Windows virtuele machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

In Hallo **Resource Manager** implementatiemodel eindpunten zijn geconfigureerd met behulp van **Netwerkbeveiligingsgroepen (nsg's)**. Zie voor meer informatie [openen van poorten en eindpunten](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Wanneer u een virtuele Linux-machine in hello Azure-portal maakt, wordt een eindpunt voor Secure Shell (SSH) doorgaans automatisch voor u gemaakt. Tijdens het maken van Hallo virtuele machine of daarna indien nodig, kunt u extra eindpunten configureren.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Volgende stappen
* U kunt ook een VM-eindpunt maken met behulp van Hallo [Azure-opdrachtregelinterface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2). Voer Hallo **azure vm-eindpunt maken** opdracht.
* Als u een virtuele machine hebt gemaakt in Hallo Resource Manager-implementatiemodel, kunt u hello Azure CLI in de modus Resource Manager te gebruiken[netwerk beveiligingsgroepen maken](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol verkeer toohello VM.
