---
title: aaaResources voor het ontwikkelen van een datawarehouse in Azure | Microsoft Docs
description: Concepten voor ontwikkeling, ontwerpbeslissingen, aanbevelingen en codering technieken voor SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: barbkess
editor: 
ms.assetid: 996e3afc-c21c-4e21-b9df-997f953f6dfd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: develop
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 67e3a6a3e2664919c3445ea5d5eba251054de020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a><span data-ttu-id="45d0b-103">Ontwerpbeslissingen en codering technieken voor SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="45d0b-103">Design decisions and coding techniques for SQL Data Warehouse</span></span>
<span data-ttu-id="45d0b-104">Bekijk via deze ontwikkeling artikelen toobetter begrijpen belangrijke ontwerpbeslissingen, aanbevelingen en codering technieken voor SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="45d0b-104">Take a look through these development articles toobetter understand key design decisions, recommendations and coding techniques for SQL Data Warehouse.</span></span>

## <a name="key-design-decisions"></a><span data-ttu-id="45d0b-105">Belangrijke ontwerpbeslissingen</span><span class="sxs-lookup"><span data-stu-id="45d0b-105">Key design decisions</span></span>
<span data-ttu-id="45d0b-106">Hallo markeren volgende artikelen aantal Hallo belangrijke concepten en moet u toounderstand voor ontwikkeling van uw gedistribueerde datawarehouse met behulp van SQL Data Warehouse Hallo ontwerpbeslissingen:</span><span class="sxs-lookup"><span data-stu-id="45d0b-106">hello following articles highlight some of hello key concepts and design decisions you will need toounderstand for hello development of your distributed data warehouse using SQL Data Warehouse:</span></span>

* <span data-ttu-id="45d0b-107">[verbindingen][connections]</span><span class="sxs-lookup"><span data-stu-id="45d0b-107">[connections][connections]</span></span>
* <span data-ttu-id="45d0b-108">[gelijktijdigheid van taken][concurrency]</span><span class="sxs-lookup"><span data-stu-id="45d0b-108">[concurrency][concurrency]</span></span>
* <span data-ttu-id="45d0b-109">[transacties][transactions]</span><span class="sxs-lookup"><span data-stu-id="45d0b-109">[transactions][transactions]</span></span>
* <span data-ttu-id="45d0b-110">[gebruiker gedefinieerde schema 's][user-defined schemas]</span><span class="sxs-lookup"><span data-stu-id="45d0b-110">[user-defined schemas][user-defined schemas]</span></span>
* <span data-ttu-id="45d0b-111">[tabeldistributie][table distribution]</span><span class="sxs-lookup"><span data-stu-id="45d0b-111">[table distribution][table distribution]</span></span>
* <span data-ttu-id="45d0b-112">[tabelindexen][table indexes]</span><span class="sxs-lookup"><span data-stu-id="45d0b-112">[table indexes][table indexes]</span></span>
* <span data-ttu-id="45d0b-113">[Tabelpartities][table partitions]</span><span class="sxs-lookup"><span data-stu-id="45d0b-113">[table partitions][table partitions]</span></span>
* <span data-ttu-id="45d0b-114">[CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="45d0b-114">[CTAS][CTAS]</span></span>
* <span data-ttu-id="45d0b-115">[statistieken][statistics]</span><span class="sxs-lookup"><span data-stu-id="45d0b-115">[statistics][statistics]</span></span>

## <a name="development-recommendations-and-coding-techniques"></a><span data-ttu-id="45d0b-116">Aanbevelingen voor ontwikkeling en codering technieken</span><span class="sxs-lookup"><span data-stu-id="45d0b-116">Development recommendations and coding techniques</span></span>
<span data-ttu-id="45d0b-117">Deze artikelen markeren specifieke codering technieken, tips en aanbevelingen voor het ontwikkelen van uw SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="45d0b-117">These articles highlight specific coding techniques, tips and recommendations for developing your SQL Data Warehouse:</span></span>

* <span data-ttu-id="45d0b-118">[opgeslagen procedures][stored procedures]</span><span class="sxs-lookup"><span data-stu-id="45d0b-118">[stored procedures][stored procedures]</span></span>
* <span data-ttu-id="45d0b-119">[labels][labels]</span><span class="sxs-lookup"><span data-stu-id="45d0b-119">[labels][labels]</span></span>
* <span data-ttu-id="45d0b-120">[Weergaven][views]</span><span class="sxs-lookup"><span data-stu-id="45d0b-120">[views][views]</span></span>
* <span data-ttu-id="45d0b-121">[tijdelijke tabellen][temporary tables]</span><span class="sxs-lookup"><span data-stu-id="45d0b-121">[temporary tables][temporary tables]</span></span>
* <span data-ttu-id="45d0b-122">[dynamische SQL][dynamic SQL]</span><span class="sxs-lookup"><span data-stu-id="45d0b-122">[dynamic SQL][dynamic SQL]</span></span>
* <span data-ttu-id="45d0b-123">[lussen][looping]</span><span class="sxs-lookup"><span data-stu-id="45d0b-123">[looping][looping]</span></span>
* <span data-ttu-id="45d0b-124">[Group by-opties][group by options]</span><span class="sxs-lookup"><span data-stu-id="45d0b-124">[group by options][group by options]</span></span>
* <span data-ttu-id="45d0b-125">[toewijzing van variabele][variable assignment]</span><span class="sxs-lookup"><span data-stu-id="45d0b-125">[variable assignment][variable assignment]</span></span>

## <a name="next-steps"></a><span data-ttu-id="45d0b-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="45d0b-126">Next steps</span></span>
<span data-ttu-id="45d0b-127">Wanneer u via Hallo ontwikkeling artikelen zijn kijk via Hallo [Transact-SQL-naslaginformatie] [ Transact-SQL reference] voor meer informatie over de syntaxis van de Hallo ondersteund voor SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="45d0b-127">Once you have been through hello development articles take a look through hello [Transact-SQL reference][Transact-SQL reference] page for more details on hello supported syntax for SQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[concurrency]: ./sql-data-warehouse-develop-concurrency.md
[connections]: ./sql-data-warehouse-connect-overview.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[dynamic SQL]: ./sql-data-warehouse-develop-dynamic-sql.md
[group by options]: ./sql-data-warehouse-develop-group-by-options.md
[labels]: ./sql-data-warehouse-develop-label.md
[looping]: ./sql-data-warehouse-develop-loops.md
[statistics]: ./sql-data-warehouse-tables-statistics.md
[stored procedures]: ./sql-data-warehouse-develop-stored-procedures.md
[table distribution]: ./sql-data-warehouse-tables-distribute.md
[table indexes]: ./sql-data-warehouse-tables-index.md
[table partitions]: ./sql-data-warehouse-tables-partition.md
[temporary tables]: ./sql-data-warehouse-tables-temporary.md
[transactions]: ./sql-data-warehouse-develop-transactions.md
[user-defined schemas]: ./sql-data-warehouse-develop-user-defined-schemas.md
[variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[views]: ./sql-data-warehouse-develop-views.md
[Transact-SQL reference]: ./sql-data-warehouse-overview-reference.md

<!--MSDN references-->
[renaming objects]: https://msdn.microsoft.com/library/mt631611.aspx

<!--Other Web references-->
