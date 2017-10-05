---
title: Azure Batch Analytics | Microsoft Docs
description: Verwijzing voor Azure Batch-analyses.
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
ms.openlocfilehash: 7d634e1bb595a84b8af339e5bc5a483a7849e7f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="0e7dc-103">Batch Analytics</span><span class="sxs-lookup"><span data-stu-id="0e7dc-103">Batch Analytics</span></span>
<span data-ttu-id="0e7dc-104">De onderwerpen in Batch Analytics bevatten informatie over de gebeurtenissen en waarschuwingen die beschikbaar zijn voor Batch-service-resources.</span><span class="sxs-lookup"><span data-stu-id="0e7dc-104">The topics in Batch Analytics contain reference information for the events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="0e7dc-105">Zie [Diagnostische logboekregistratie van Azure Batch](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) voor meer informatie over het inschakelen en gebruiken van Batch diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="0e7dc-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="0e7dc-106">Diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="0e7dc-106">Diagnostic logs</span></span>

<span data-ttu-id="0e7dc-107">De Azure Batch-service verzendt de volgende diagnostische gebeurtenissen gedurende de levensduur van bepaalde Batch-resources.</span><span class="sxs-lookup"><span data-stu-id="0e7dc-107">The Azure Batch service emits the following diagnostic log events during the lifetime of certain Batch resources.</span></span>

<span data-ttu-id="0e7dc-108">**Service-logboekgebeurtenissen**</span><span class="sxs-lookup"><span data-stu-id="0e7dc-108">**Service Log events**</span></span>
* [<span data-ttu-id="0e7dc-109">Groep maken</span><span class="sxs-lookup"><span data-stu-id="0e7dc-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="0e7dc-110">Toepassingen verwijderen starten</span><span class="sxs-lookup"><span data-stu-id="0e7dc-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="0e7dc-111">Groep verwijderen is voltooid</span><span class="sxs-lookup"><span data-stu-id="0e7dc-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="0e7dc-112">Groep formaat starten</span><span class="sxs-lookup"><span data-stu-id="0e7dc-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="0e7dc-113">Groep formaat voltooid</span><span class="sxs-lookup"><span data-stu-id="0e7dc-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="0e7dc-114">Taak starten</span><span class="sxs-lookup"><span data-stu-id="0e7dc-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="0e7dc-115">De taak is voltooid</span><span class="sxs-lookup"><span data-stu-id="0e7dc-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="0e7dc-116">Taak is mislukt</span><span class="sxs-lookup"><span data-stu-id="0e7dc-116">Task fail</span></span>](batch-task-fail-event.md)