---
title: Controleren van de gebruiker query's in Azure SQL Data Warehouse | Microsoft Docs
description: Overzicht van de overwegingen, best practices en taken voor het controleren van de gebruiker query's in Azure SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 1d0960db-5dcf-4a08-b1dc-6c5d3d5a616d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 65509a65c2b34553822cc02d7a7fa5a614adc57f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-user-queries-in-azure-sql-data-warehouse"></a><span data-ttu-id="5eab5-103">Monitor gebruiker query's in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5eab5-103">Monitor user queries in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="5eab5-104">Overzicht van de overwegingen, best practices en taken voor het controleren van de gebruiker query's in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5eab5-104">Overview of the considerations, best practices, and tasks for monitoring user queries in SQL Data Warehouse.</span></span>

| <span data-ttu-id="5eab5-105">Category</span><span class="sxs-lookup"><span data-stu-id="5eab5-105">Category</span></span> | <span data-ttu-id="5eab5-106">Taak of overweging</span><span class="sxs-lookup"><span data-stu-id="5eab5-106">Task or consideration</span></span> | <span data-ttu-id="5eab5-107">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5eab5-107">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="5eab5-108">Trage prestaties</span><span class="sxs-lookup"><span data-stu-id="5eab5-108">Slow performance</span></span> |<span data-ttu-id="5eab5-109">Een langlopende gebruikersquery vinden</span><span class="sxs-lookup"><span data-stu-id="5eab5-109">Find a long-running user query</span></span> |<span data-ttu-id="5eab5-110">[Langlopende query 's][Find long-running queries]</span><span class="sxs-lookup"><span data-stu-id="5eab5-110">[Find long-running queries][Find long-running queries]</span></span> |
| <span data-ttu-id="5eab5-111">Gelijktijdigheid</span><span class="sxs-lookup"><span data-stu-id="5eab5-111">Concurrency</span></span> |<span data-ttu-id="5eab5-112">Gelijktijdige bronnen toewijzen aan gebruiker query 's</span><span class="sxs-lookup"><span data-stu-id="5eab5-112">Assign concurrent resources to user queries</span></span> |<span data-ttu-id="5eab5-113">[Gelijktijdigheid van taken en de belasting van beheer][Concurrency and workload management]</span><span class="sxs-lookup"><span data-stu-id="5eab5-113">[Concurrency and workload management][Concurrency and workload management]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5eab5-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5eab5-114">Next steps</span></span>
<span data-ttu-id="5eab5-115">Voor meer tips voor het beheer, Ga naar de [Beheeroverzicht][Management overview].</span><span class="sxs-lookup"><span data-stu-id="5eab5-115">For more management tips, head over to the [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Find long-running queries]: sql-data-warehouse-manage-monitor.md
[Concurrency and workload management]: sql-data-warehouse-develop-concurrency.md
[Management overview]: sql-data-warehouse-overview-manage.md

<!--MSDN references-->


<!--Other Web references-->
