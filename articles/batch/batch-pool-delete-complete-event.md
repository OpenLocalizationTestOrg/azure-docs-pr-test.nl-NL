---
title: Azure Batch-pool verwijderen gebeurtenis | Microsoft Docs
description: Naslaginformatie voor Batch-pool gebeurtenis verwijderen.
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
ms.openlocfilehash: 890f2ba7fda37060c56177868d6214d517d91831
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="ad401-103">Gebeurtenis groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="ad401-103">Pool delete complete event</span></span>

 <span data-ttu-id="ad401-104">Deze gebeurtenis wordt verzonden wanneer een groep delete-bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ad401-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="ad401-105">Het volgende voorbeeld ziet de hoofdtekst van een groep verwijderingsgebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="ad401-105">The following example shows the body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="ad401-106">Element</span><span class="sxs-lookup"><span data-stu-id="ad401-106">Element</span></span>|<span data-ttu-id="ad401-107">Type</span><span class="sxs-lookup"><span data-stu-id="ad401-107">Type</span></span>|<span data-ttu-id="ad401-108">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="ad401-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="ad401-109">id</span><span class="sxs-lookup"><span data-stu-id="ad401-109">id</span></span>|<span data-ttu-id="ad401-110">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ad401-110">String</span></span>|<span data-ttu-id="ad401-111">De id van de groep.</span><span class="sxs-lookup"><span data-stu-id="ad401-111">The id of the pool.</span></span>|
|<span data-ttu-id="ad401-112">startTime</span><span class="sxs-lookup"><span data-stu-id="ad401-112">startTime</span></span>|<span data-ttu-id="ad401-113">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="ad401-113">DateTime</span></span>|<span data-ttu-id="ad401-114">De tijd dat de groep verwijderen is gestart.</span><span class="sxs-lookup"><span data-stu-id="ad401-114">The time the pool delete started.</span></span>|
|<span data-ttu-id="ad401-115">Eindtijd</span><span class="sxs-lookup"><span data-stu-id="ad401-115">endTime</span></span>|<span data-ttu-id="ad401-116">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="ad401-116">DateTime</span></span>|<span data-ttu-id="ad401-117">De tijd de groep verwijderen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ad401-117">The time the pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="ad401-118">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="ad401-118">Remarks</span></span>
<span data-ttu-id="ad401-119">Zie voor meer informatie over statussen en foutcodes voor de bewerking formaat wijzigen van toepassingen [een adresgroep verwijderen van een account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span><span class="sxs-lookup"><span data-stu-id="ad401-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>