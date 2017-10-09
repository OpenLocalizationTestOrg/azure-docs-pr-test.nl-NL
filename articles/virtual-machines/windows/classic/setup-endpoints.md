---
title: aaaSet eindpunten op een klassieke Windows-VM | Microsoft Docs
description: Informatie over tooset eindpunten voor een Windows-VM in hello Azure classic portal tooallow communicatie met een virtuele Windows-machine in Azure.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a>Hoe tooset eindpunten op een klassieke Windows-virtuele machine in Azure
Alle Windows virtuele machines die u maakt in Azure met behulp van het klassieke implementatiemodel Hallo automatisch kan communiceren via een particulier netwerkkanaal met andere virtuele machines in Hallo dezelfde cloudservice of een virtueel netwerk. Computers op Hallo Internet of een andere virtuele netwerken vereisen echter eindpunten toodirect Hallo netwerk binnenkomend verkeer tooa virtuele machine. In dit artikel is ook beschikbaar voor [virtuele Linux-machines](../../linux/classic/setup-endpoints.md).

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

In Hallo **Resource Manager** implementatiemodel eindpunten zijn geconfigureerd met behulp van **Netwerkbeveiligingsgroepen (nsg's)**. Zie voor meer informatie [toestaan externe toegang tooyour virtuele machine met behulp van Azure-portal Hallo](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Wanneer u een virtuele Windows-computer in hello Azure-portal maakt, worden algemene eindpunten zoals die voor extern bureaublad- en Windows PowerShell voor externe toegang doorgaans automatisch voor u gemaakt. Tijdens het maken van Hallo virtuele machine of daarna indien nodig, kunt u extra eindpunten configureren.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Volgende stappen
* een Azure PowerShell-cmdlet tooset u een eindpunt VM toouse Zie [toevoegen AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).
* een Azure PowerShell-cmdlet toomanage een ACL voor een eindpunt toouse Zie [beheren toegangsbeheerlijsten (ACL's) voor eindpunten met behulp van PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).
* Als u een virtuele machine hebt gemaakt in Hallo Resource Manager-implementatiemodel, kunt u Azure PowerShell te gebruiken[netwerk beveiligingsgroepen maken](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol verkeer toohello VM.
