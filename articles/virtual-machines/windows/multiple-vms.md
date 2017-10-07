---
title: aaaCreate meerdere virtuele machines | Microsoft Docs
description: Opties voor het maken van meerdere virtuele machines in Windows
services: virtual-machines-windows
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dfc1d1bb-a47d-4d7c-9fd2-f12050baacab
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: guybo
ms.openlocfilehash: 37729fabd91049744f6bd94c55221f5c1c65d527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-multiple-azure-virtual-machines"></a>Meerdere virtuele Azure-machines maken
Er zijn veel scenario's waarbij u toocreate een groot aantal soortgelijke virtuele machines (VM's moet). Voorbeelden zijn high-performance computing (HPC), grootschalige data-analyse, schaalbare en vaak staatloze middelste laag of back-end servers (zoals endwebservers servers) en gedistribueerde databases.

Dit artikel wordt Hallo beschikbare opties toocreate meerdere virtuele machines in Azure. Deze opties verder dan Hallo eenvoudige gevallen waarin u een reeks van virtuele machines handmatig maken. toocreate veel virtuele machines, Hallo processen die u doorgaans niet schalen goed als u toocreate meer dan een aantal virtuele machines nodig.

Eenzijdige toocreate veel vergelijkbare VM's is toouse hello Azure Resource Manager constructie van *resource lussen*.

## <a name="resource-loops"></a>Resource lussen
Resource lussen zijn een syntactische steno in Azure Resource Manager-sjablonen. Resource lussen kunnen maken van een set op vergelijkbare wijze geconfigureerde resources in een lus. U kunt resource lussen toocreate meerdere storage-accounts, netwerkinterfaces of virtuele machines. Voor meer informatie over lussen resource verwijzen te[virtuele machines maken in beschikbaarheidssets voor resource lussen](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/).

## <a name="challenges-of-scale"></a>Uitdagingen van schaal
Hoewel resource lussen het gemakkelijker toobuild uit een cloudinfrastructuur op grote schaal maken en meer beknopte sjablonen produceren, blijven bepaalde uitdagingen. Als u een resource lus toocreate 100 virtuele machines gebruikt, moet u bijvoorbeeld toocorrelate network interface controller (NIC's) met de bijbehorende virtuele machines en opslagaccounts. Omdat Hallo aantal virtuele machines waarschijnlijk toobe verschilt van het aantal opslagaccounts hello is, hebt u toodeal met andere resource lus grootten, te. Dit zijn problemen opgelost, maar Hallo complexiteit aanzienlijk kan binnen de schaal.

Een andere uitdaging treedt op wanneer u moet een infrastructuur die elastisch schalen. U kunt bijvoorbeeld een infrastructuur voor automatisch schalen die automatisch verhoogt of verlaagt Hallo aantal VM's in het antwoord tooworkload. Virtuele machines bieden niet een mechanisme voor geïntegreerde toovary aantal (scale-out en schaal). Als u schaalt door het verwijderen van virtuele machines, is het moeilijk tooguarantee hoge beschikbaarheid door ervoor te zorgen dat virtuele machines zijn verdeeld zijn over domeinen update en fouttolerantie.

Wanneer u een resource-lus gebruikt, gaan meerdere aanroepen toocreate resources ten slotte toohello onderliggende infrastructuur. Wanneer meerdere aanroepen vergelijkbare bronnen maakt, wordt Azure is een impliciete kans tooimprove bij dit ontwerp en implementatie betrouwbaarheid en prestaties te optimaliseren. Dit is wanneer *virtuele-machineschaalsets* in komen.

## <a name="virtual-machine-scale-sets"></a>Virtuele-machineschaalsets
Virtuele-machineschaalsets zijn van een resource Azure Compute toodeploy en beheren van een set van identieke virtuele machines. Met alle virtuele machines die zijn geconfigureerd dezelfde hello, VM-schaalsets eenvoudig tooscale in en scale-out. U eenvoudigweg wijzigen Hallo aantal VM's in Hallo set. U kunt ook VM scale sets tooautoscale op basis van Hallo eisen van Hallo werkbelasting configureren.

Voor toepassingen die tooscale rekenresources uit- en scale moeten worden operations impliciet gelijkmatig over probleem- en -domeinen.

In plaats van het correleren van meerdere resources, zoals NIC's en virtuele machines, heeft een VM-schaalset netwerk, opslag, virtuele machine en extensie-eigenschappen die u centraal kunt configureren.

Voor een inleiding tooVM schaal wordt ingesteld, Raadpleeg toohello [virtuele-machineschaalsets productpagina](https://azure.microsoft.com/services/virtual-machine-scale-sets/). Voor meer informatie gedetailleerde, gaat u toohello [virtuele machines scale ingesteld documentatie](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/).

