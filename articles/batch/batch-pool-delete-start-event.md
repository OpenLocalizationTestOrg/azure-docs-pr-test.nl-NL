---
title: Azure Batch pool verwijderen start-gebeurtenis | Microsoft Docs
description: Verwijzing voor Batch-pool verwijderen start-gebeurtenis.
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: f8a5241dce422e5c826ab428da6d7bc93284a1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="999a8-103">Gebeurtenissen voor het starten van toepassingen verwijderen</span><span class="sxs-lookup"><span data-stu-id="999a8-103">Pool delete start event</span></span>

 <span data-ttu-id="999a8-104">Deze gebeurtenis wordt verzonden wanneer een groep delete-bewerking is gestart.</span><span class="sxs-lookup"><span data-stu-id="999a8-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="999a8-105">Aangezien het verwijderen van toepassingen een asynchrone gebeurtenis is, kunt u verwachten groep complete verwijderingsgebeurtenis om te worden verzonden nadat de delete-bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="999a8-105">Since the pool delete is an asynchronous event, you can expect a pool delete complete event to be emitted once the delete operation completes.</span></span>

 <span data-ttu-id="999a8-106">Het volgende voorbeeld ziet de hoofdtekst van een groep verwijderen start-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="999a8-106">The following example shows the body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="999a8-107">Element</span><span class="sxs-lookup"><span data-stu-id="999a8-107">Element</span></span>|<span data-ttu-id="999a8-108">Type</span><span class="sxs-lookup"><span data-stu-id="999a8-108">Type</span></span>|<span data-ttu-id="999a8-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="999a8-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="999a8-110">id</span><span class="sxs-lookup"><span data-stu-id="999a8-110">id</span></span>|<span data-ttu-id="999a8-111">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="999a8-111">String</span></span>|<span data-ttu-id="999a8-112">De id van de groep.</span><span class="sxs-lookup"><span data-stu-id="999a8-112">The id of the pool.</span></span>|