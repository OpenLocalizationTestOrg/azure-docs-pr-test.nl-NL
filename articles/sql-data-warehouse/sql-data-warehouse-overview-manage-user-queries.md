---
title: aaaMonitor gebruiker query's in Azure SQL Data Warehouse | Microsoft Docs
description: Overzicht van Hallo overwegingen, best practices en taken voor het controleren van de gebruiker query's in Azure SQL Data Warehouse
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
ms.openlocfilehash: 67639e81b04635452e1ed844fe2d7245aa96a4fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-user-queries-in-azure-sql-data-warehouse"></a><span data-ttu-id="36b9c-103">Monitor gebruiker query's in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="36b9c-103">Monitor user queries in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="36b9c-104">Overzicht van overwegingen hello, aanbevolen procedures en taken voor het controleren van de gebruiker query's in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="36b9c-104">Overview of hello considerations, best practices, and tasks for monitoring user queries in SQL Data Warehouse.</span></span>

| <span data-ttu-id="36b9c-105">Category</span><span class="sxs-lookup"><span data-stu-id="36b9c-105">Category</span></span> | <span data-ttu-id="36b9c-106">Taak of overweging</span><span class="sxs-lookup"><span data-stu-id="36b9c-106">Task or consideration</span></span> | <span data-ttu-id="36b9c-107">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="36b9c-107">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="36b9c-108">Trage prestaties</span><span class="sxs-lookup"><span data-stu-id="36b9c-108">Slow performance</span></span> |<span data-ttu-id="36b9c-109">Een langlopende gebruikersquery vinden</span><span class="sxs-lookup"><span data-stu-id="36b9c-109">Find a long-running user query</span></span> |<span data-ttu-id="36b9c-110">[Langlopende query 's][Find long-running queries]</span><span class="sxs-lookup"><span data-stu-id="36b9c-110">[Find long-running queries][Find long-running queries]</span></span> |
| <span data-ttu-id="36b9c-111">Gelijktijdigheid</span><span class="sxs-lookup"><span data-stu-id="36b9c-111">Concurrency</span></span> |<span data-ttu-id="36b9c-112">Gelijktijdige resources toouser query's toewijzen</span><span class="sxs-lookup"><span data-stu-id="36b9c-112">Assign concurrent resources toouser queries</span></span> |<span data-ttu-id="36b9c-113">[Gelijktijdigheid van taken en de belasting van beheer][Concurrency and workload management]</span><span class="sxs-lookup"><span data-stu-id="36b9c-113">[Concurrency and workload management][Concurrency and workload management]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="36b9c-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="36b9c-114">Next steps</span></span>
<span data-ttu-id="36b9c-115">Ga voor meer tips voor het beheer van toohello [Beheeroverzicht][Management overview].</span><span class="sxs-lookup"><span data-stu-id="36b9c-115">For more management tips, head over toohello [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Find long-running queries]: sql-data-warehouse-manage-monitor.md
[Concurrency and workload management]: sql-data-warehouse-develop-concurrency.md
[Management overview]: sql-data-warehouse-overview-manage.md

<!--MSDN references-->


<!--Other Web references-->
