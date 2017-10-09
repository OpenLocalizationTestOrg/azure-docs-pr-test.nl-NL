---
title: aaaUsing beheerd schijven met Azure Virtual Machine-Schaalsets | Microsoft Docs
description: Meer informatie over waarom en hoe toouse beheerd schijven met virtuele-machineschaalsets
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a>Virtuele-machineschaalsets in Azure en beheerde schijven

[Virtuele-machineschaalsets](/azure/virtual-machine-scale-sets/) in Azure ondersteunen virtuele machines met beheerde schijven. Het gebruik van beheerde schijven met schaalsets heeft een aantal voordelen, waaronder:

* U hoeft niet meer toopre-maken en beheren van accounts toostore Hallo OS opslagschijven voor Hallo virtuele machines schaalset.

* U kunt beheerde gegevens schijven toohello scale set toevoegen.

* Met een beheerde schijf kan een schaalset een capaciteit van wel 1000 virtuele machines hebben als deze is gebaseerd op een platforminstallatiekopie, of 100 virtuele machines als deze is gebaseerd op een aangepaste installatiekopie.

## <a name="get-started"></a>Aan de slag

Een eenvoudige manier tooget gestart met beheerde schijf-schaalsets is toodeploy van hello Azure-portal. Raadpleeg [dit artikel](./virtual-machine-scale-sets-portal-create.md) voor meer informatie. Een andere eenvoudige manier tooget gestart is toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy een schaalset. Hallo volgende voorbeeld ziet u hoe scale 10 virtuele machines, elk met een gegevensschijf van 50- en 100 GB in te stellen op basis van een Ubuntu toocreate:

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

U kunt ook zoeken in Hallo [Azure Quick Start-sjablonen GitHub-repo-](https://github.com/Azure/azure-quickstart-templates) voor mappen met `vmss` toosee vooraf gemaakte voorbeelden van sjablonen die schaalsets implementeren. tootell welke sjablonen al beheerde schijven gebruikt, kunt u verwijzen te[deze lijst](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).

## <a name="next-steps"></a>Volgende stappen

In [dit artikel](../virtual-machines/windows/managed-disks-overview.md) vindt u meer informatie over beheerde schijven in het algemeen.

toosee de wijze waarop een schaal van Resource Manager sjabloon tooprovision ingesteld met tooconvert beheerd schijven, Zie [in dit artikel](./virtual-machine-scale-sets-convert-template-to-md.md). Hallo toepassen dezelfde wijzigingen toohello Resource Manager-sjablonen ook toohello REST API van Azure.

toolearn meer informatie over het gebruik van beheerde gegevensschijven met schaalsets, Zie [in dit artikel](./virtual-machine-scale-sets-attached-disks.md).

werken met grote schaalsets, toobegin te verwijzen[in dit artikel](./virtual-machine-scale-sets-placement-groups.md).


