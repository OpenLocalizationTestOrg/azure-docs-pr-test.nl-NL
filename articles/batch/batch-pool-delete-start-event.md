---
title: aaa "Azure Batch pool verwijderen start-gebeurtenis | Microsoft Docs'
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
ms.openlocfilehash: 79bb28bffc760a49cc0a95062f5086dc96c6a795
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="d3b2f-103">Gebeurtenissen voor het starten van toepassingen verwijderen</span><span class="sxs-lookup"><span data-stu-id="d3b2f-103">Pool delete start event</span></span>

 <span data-ttu-id="d3b2f-104">Deze gebeurtenis wordt verzonden wanneer een groep delete-bewerking is gestart.</span><span class="sxs-lookup"><span data-stu-id="d3b2f-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="d3b2f-105">Aangezien Hallo groep verwijderen een asynchrone gebeurtenis is, kunt u verwachten een groep verwijderen gebeurtenis toobe verzonden zodra Hallo bewerking verwijderen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="d3b2f-105">Since hello pool delete is an asynchronous event, you can expect a pool delete complete event toobe emitted once hello delete operation completes.</span></span>

 <span data-ttu-id="d3b2f-106">Hallo ziet volgende voorbeeld Hallo hoofdtekst van een groep verwijderen start-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="d3b2f-106">hello following example shows hello body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="d3b2f-107">Element</span><span class="sxs-lookup"><span data-stu-id="d3b2f-107">Element</span></span>|<span data-ttu-id="d3b2f-108">Type</span><span class="sxs-lookup"><span data-stu-id="d3b2f-108">Type</span></span>|<span data-ttu-id="d3b2f-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="d3b2f-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="d3b2f-110">id</span><span class="sxs-lookup"><span data-stu-id="d3b2f-110">id</span></span>|<span data-ttu-id="d3b2f-111">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d3b2f-111">String</span></span>|<span data-ttu-id="d3b2f-112">Hallo-id van Hallo pool.</span><span class="sxs-lookup"><span data-stu-id="d3b2f-112">hello id of hello pool.</span></span>|
