---
title: aaa "Azure Batch-pool verwijderen gebeurtenis | Microsoft Docs'
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
ms.openlocfilehash: 494c371e48ebfb1bf3d2973a7401829a939ba141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="9292c-103">Gebeurtenis groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="9292c-103">Pool delete complete event</span></span>

 <span data-ttu-id="9292c-104">Deze gebeurtenis wordt verzonden wanneer een groep delete-bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9292c-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="9292c-105">Hallo ziet volgende voorbeeld Hallo hoofdtekst van een groep verwijderingsgebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="9292c-105">hello following example shows hello body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="9292c-106">Element</span><span class="sxs-lookup"><span data-stu-id="9292c-106">Element</span></span>|<span data-ttu-id="9292c-107">Type</span><span class="sxs-lookup"><span data-stu-id="9292c-107">Type</span></span>|<span data-ttu-id="9292c-108">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9292c-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="9292c-109">id</span><span class="sxs-lookup"><span data-stu-id="9292c-109">id</span></span>|<span data-ttu-id="9292c-110">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9292c-110">String</span></span>|<span data-ttu-id="9292c-111">Hallo-id van Hallo pool.</span><span class="sxs-lookup"><span data-stu-id="9292c-111">hello id of hello pool.</span></span>|
|<span data-ttu-id="9292c-112">startTime</span><span class="sxs-lookup"><span data-stu-id="9292c-112">startTime</span></span>|<span data-ttu-id="9292c-113">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="9292c-113">DateTime</span></span>|<span data-ttu-id="9292c-114">Hallo tijd Hallo-groep verwijderen is gestart.</span><span class="sxs-lookup"><span data-stu-id="9292c-114">hello time hello pool delete started.</span></span>|
|<span data-ttu-id="9292c-115">endTime</span><span class="sxs-lookup"><span data-stu-id="9292c-115">endTime</span></span>|<span data-ttu-id="9292c-116">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="9292c-116">DateTime</span></span>|<span data-ttu-id="9292c-117">Hallo tijd Hallo-groep verwijderen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9292c-117">hello time hello pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="9292c-118">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9292c-118">Remarks</span></span>
<span data-ttu-id="9292c-119">Zie voor meer informatie over statussen en foutcodes voor de bewerking formaat wijzigen van toepassingen [een adresgroep verwijderen van een account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span><span class="sxs-lookup"><span data-stu-id="9292c-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>