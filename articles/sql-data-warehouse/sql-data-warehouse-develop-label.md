---
title: aaaUse labels tooinstrument query's in SQL Data Warehouse | Microsoft Docs
description: Tips voor het gebruik van labels tooinstrument query's in Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 44988de8-04c1-4fed-92be-e1935661a4e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 82e7ea98e1417134227f1d7c529fdaf2f1df3853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a><span data-ttu-id="fbfc0-103">Labels tooinstrument query's in SQL Data Warehouse gebruiken</span><span class="sxs-lookup"><span data-stu-id="fbfc0-103">Use labels tooinstrument queries in SQL Data Warehouse</span></span>
<span data-ttu-id="fbfc0-104">SQL Data Warehouse ondersteunt een concept query labels genoemd.</span><span class="sxs-lookup"><span data-stu-id="fbfc0-104">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="fbfc0-105">Bekijk voordat u doorgaat naar eventuele diepte gaan we een voorbeeld van een:</span><span class="sxs-lookup"><span data-stu-id="fbfc0-105">Before going into any depth let's look at an example of one:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="fbfc0-106">Deze regel labels Hallo tekenreeks 'Mijn Query Label' toohello query.</span><span class="sxs-lookup"><span data-stu-id="fbfc0-106">This last line tags hello string 'My Query Label' toohello query.</span></span> <span data-ttu-id="fbfc0-107">Dit is vooral handig zijn omdat de query kunnen via DMV's Hallo Hallo label.</span><span class="sxs-lookup"><span data-stu-id="fbfc0-107">This is particularly helpful as hello label is query-able through hello DMVs.</span></span> <span data-ttu-id="fbfc0-108">Dit biedt ons een mechanisme tootrack omlaag probleem query's en toohelp, zien ook uitgevoerd via een ETL uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fbfc0-108">This provides us with a mechanism tootrack down problem queries and also toohelp identify progress through an ETL run.</span></span>

<span data-ttu-id="fbfc0-109">Een goede naamgevingsconventie echt helpt hier.</span><span class="sxs-lookup"><span data-stu-id="fbfc0-109">A good naming convention really helps here.</span></span> <span data-ttu-id="fbfc0-110">Bijvoorbeeld als ' PROJECT: PROCEDURE: instructie: Opmerking ' toouniquely Hallo query in onder alle Hallo-code in broncodebeheer identificeren kan helpen.</span><span class="sxs-lookup"><span data-stu-id="fbfc0-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help toouniquely identify hello query in amongst all hello code in source control.</span></span>

<span data-ttu-id="fbfc0-111">toosearch labels kunt u Hallo na query die gebruikmaakt van dynamische beheerweergaven Hallo:</span><span class="sxs-lookup"><span data-stu-id="fbfc0-111">toosearch by label you can use hello following query that uses hello dynamic management views:</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="fbfc0-112">Het is essentieel dat u vierkante haken of dubbele aanhalingstekens rond Hallo word label langs tijdens het opvragen van.</span><span class="sxs-lookup"><span data-stu-id="fbfc0-112">It is essential that you wrap square brackets or double quotes around hello word label when querying.</span></span> <span data-ttu-id="fbfc0-113">Label is een gereserveerd woord en wordt een fout veroorzaakt als deze niet zijn gescheiden.</span><span class="sxs-lookup"><span data-stu-id="fbfc0-113">Label is a reserved word and will caused an error if it has not been delimited.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="fbfc0-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fbfc0-114">Next steps</span></span>
<span data-ttu-id="fbfc0-115">Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].</span><span class="sxs-lookup"><span data-stu-id="fbfc0-115">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
