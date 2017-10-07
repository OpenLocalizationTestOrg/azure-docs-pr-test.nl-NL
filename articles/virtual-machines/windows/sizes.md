---
title: aaaWindows VM-groottes in Azure | Microsoft Docs
description: Geeft een lijst Hallo verschillende grootten beschikbaar voor Windows virtuele machines in Azure.
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: aabf0d30-04eb-4d34-b44a-69f8bfb84f22
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 80bd8241b134031c41b56224e841c7557c4845cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a>Grootten voor Windows virtuele machines in Azure

Dit artikel beschrijft de beschikbare grootten Hallo en opties voor hello Azure virtuele machines kunt u toorun uw Windows-apps en werkbelastingen. Het bevat ook toobe voor overwegingen met betrekking tot implementatie op de hoogte van wanneer u van plan bent toouse deze resources.  In dit artikel is ook beschikbaar voor [virtuele Linux-machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


| Type                     | Grootten           |    Beschrijving       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Algemeen doel](sizes-general.md)          | Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0 7 | Evenwichtige CPU-geheugenverhouding. Ideaal voor testen en ontwikkeling, kleine toomedium databases en lage toomedium verkeer webservers. |
| [Geoptimaliseerde rekenkracht](sizes-compute.md)        | FS, F             | Hoge CPU-geheugenverhouding. Goed voor webservers met gemiddeld verkeer, netwerkapparatuur, batchprocessen en toepassingsservers.        |
| [Geoptimaliseerd geheugen](../virtual-machines-windows-sizes-memory.md)         | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Verhouding tussen het hoge geheugen aan CPU. Ideaal voor relationele database-servers, gemiddeld toolarge caches en in het geheugen analytics.                 |
| [Geoptimaliseerde opslag](../virtual-machines-windows-sizes-storage.md)        | Ls                | Snelle doorvoer van schijfgegevens en IO. Ideaal voor big data-, SQL- en NoSQL-databases.                                                         |
| [GPU](sizes-gpu.md)            | NV, NC            | Gespecialiseerde virtuele machines gericht voor zware grafische weergave en het bewerken van video's. Beschikbaar met één of meerdere GPU's.       |
| [Krachtig rekenvermogen](sizes-hpc.md) | H, A8 11          | Onze snelste en krachtigste CPU-virtuele machines met optionele netwerkinterfaces (RDMA) voor hoge doorvoer. 

<br> 

- Zie voor meer informatie over prijzen Hallo verschillende grootten [prijzen van virtuele Machines](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows). 
- algemene beperkingen toosee op Azure Virtual machines, Zie [Azure-abonnement en Servicelimieten, quota's en beperkingen](../../azure-subscription-service-limits.md).
- Opslagkosten zijn berekend afzonderlijk op basis van de gebruikte pagina's in Hallo storage-account. Voor meer informatie [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/).
- Meer informatie over het [Azure compute-eenheden (ACU)](acu.md) kunt u de prestaties van Azure-SKU's met elkaar vergelijken.



## <a name="rest-api"></a>Rest-API

Zie voor informatie over het gebruik van Hallo REST-API tooquery voor VM-groottes Hallo volgende:

- [Lijst met beschikbare virtuele machine grootten voor het vergroten of verkleinen](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [Lijst met beschikbare virtuele machine grootten voor een abonnement](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [Grootte van de lijst met beschikbare virtuele machines in een beschikbaarheidsset](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a>ACU

Meer informatie over het [Azure compute-eenheden (ACU)](acu.md) kunt u de prestaties van Azure-SKU's met elkaar vergelijken.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over Hallo andere VM-grootten die beschikbaar zijn:
- [Algemeen doel](sizes-general.md)
- [Geoptimaliseerde rekenkracht](sizes-compute.md)
- [Geoptimaliseerd geheugen](../virtual-machines-windows-sizes-memory.md)
- [Geoptimaliseerde opslag](../virtual-machines-windows-sizes-storage.md)
- [Geoptimaliseerde GPU](sizes-gpu.md)
- [Krachtig rekenvermogen](sizes-hpc.md)



