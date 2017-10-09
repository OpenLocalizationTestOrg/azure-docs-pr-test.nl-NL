---
title: aaaLeverage T-SQL-lus in Azure SQL Data Warehouse | Microsoft Docs
description: Tips voor de Transact-SQL-lussen en vervang cursors in Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f3384b81-b943-431b-bc73-90e47e4c195f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c7e8f71b910d00d0dfc30f6e5eba190fd05014b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="loops-in-sql-data-warehouse"></a><span data-ttu-id="3f118-103">Lussen in SQL datawarehouse</span><span class="sxs-lookup"><span data-stu-id="3f118-103">Loops in SQL Data Warehouse</span></span>
<span data-ttu-id="3f118-104">SQL Data Warehouse ondersteunt Hallo [terwijl][terwijl] lus voor herhaaldelijk blokken instructie uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3f118-104">SQL Data Warehouse supports hello [WHILE][WHILE] loop for repeatedly executing statement blocks.</span></span> <span data-ttu-id="3f118-105">Deze blijven voor zolang Hallo opgegeven voorwaarden wordt voldaan, of tot Hallo code specifiek Hallo lus met Hallo beëindigt `BREAK` sleutelwoord.</span><span class="sxs-lookup"><span data-stu-id="3f118-105">This will continue for as long as hello specified conditions are true or until hello code specifically terminates hello loop using hello `BREAK` keyword.</span></span> <span data-ttu-id="3f118-106">Lussen zijn bijzonder nuttig voor het vervangen van cursors die zijn gedefinieerd in SQL-code.</span><span class="sxs-lookup"><span data-stu-id="3f118-106">Loops are particularly useful for replacing cursors defined in SQL code.</span></span> <span data-ttu-id="3f118-107">Gelukkig zijn bijna alle cursors die zijn geschreven in SQL-code Hallo snelle doorsturen, lezen alleen groot.</span><span class="sxs-lookup"><span data-stu-id="3f118-107">Fortunately, almost all cursors that are written in SQL code are of hello fast forward, read only variety.</span></span> <span data-ttu-id="3f118-108">Daarom [terwijl] lussen vormen een geweldige alternatief als u merkt dat tooreplace een.</span><span class="sxs-lookup"><span data-stu-id="3f118-108">Therefore [WHILE] loops are a great alternative if you find yourself having tooreplace one.</span></span>

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a><span data-ttu-id="3f118-109">Gebruik van lussen en vervangt cursors in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3f118-109">Leveraging loops and replacing cursors in SQL Data Warehouse</span></span>
<span data-ttu-id="3f118-110">Echter eerst in head wilt voordat u zichzelf moet stellen Hallo volgende vraag: 'kan deze cursor worden opnieuw geschreven toouse set op basis van operations?'.</span><span class="sxs-lookup"><span data-stu-id="3f118-110">However, before diving in head first you should ask yourself hello following question: "Could this cursor be re-written toouse set based operations?".</span></span> <span data-ttu-id="3f118-111">In veel gevallen Hallo antwoord Ja is en is vaak de beste aanpak Hallo.</span><span class="sxs-lookup"><span data-stu-id="3f118-111">In many cases hello answer will be yes and is often hello best approach.</span></span> <span data-ttu-id="3f118-112">Een set op basis van de bewerking vaak voert aanzienlijk sneller dan een benadering iteratieve, per rij.</span><span class="sxs-lookup"><span data-stu-id="3f118-112">A set based operation often performs significantly faster than an iterative, row by row approach.</span></span>

<span data-ttu-id="3f118-113">Vooruit cursors voor alleen-lezen kunnen eenvoudig worden vervangen door een samenvoegartikel constructie.</span><span class="sxs-lookup"><span data-stu-id="3f118-113">Fast forward read-only cursors can be easily replaced with a looping construct.</span></span> <span data-ttu-id="3f118-114">Hieronder vindt u een eenvoudig voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="3f118-114">Below is a simple example.</span></span> <span data-ttu-id="3f118-115">Dit codevoorbeeld Hallo statistieken voor elke tabel in de database Hallo-updates.</span><span class="sxs-lookup"><span data-stu-id="3f118-115">This code example updates hello statistics for every table in hello database.</span></span> <span data-ttu-id="3f118-116">Door iteratie van tabellen in de lus Hallo Hallo we kunnen tooexecute elke opdracht in de reeks zijn.</span><span class="sxs-lookup"><span data-stu-id="3f118-116">By iterating over hello tables in hello loop we are able tooexecute each command in sequence.</span></span>

<span data-ttu-id="3f118-117">Maak eerst een tijdelijke tabel die een afzonderlijke instructies voor unieke rij aantal gebruikte tooidentify Hallo bevat:</span><span class="sxs-lookup"><span data-stu-id="3f118-117">First, create a temporary table containing a unique row number used tooidentify hello individual statements:</span></span>

```
CREATE TABLE #tbl
WITH
( DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS Sequence
,       [name]
,       'UPDATE STATISTICS '+QUOTENAME([name]) AS sql_code
FROM    sys.tables
;
```

<span data-ttu-id="3f118-118">Ten tweede initialiseren Hallo variabelen vereist tooperform Hallo lus:</span><span class="sxs-lookup"><span data-stu-id="3f118-118">Second, initialize hello variables required tooperform hello loop:</span></span>

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

<span data-ttu-id="3f118-119">Nu op een uitvoeren-instructies in een lus tegelijk:</span><span class="sxs-lookup"><span data-stu-id="3f118-119">Now loop over statements executing them one at a time:</span></span>

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

<span data-ttu-id="3f118-120">Ten slotte Hallo tijdelijke tabel gemaakt in de eerste stap Hallo verwijderen</span><span class="sxs-lookup"><span data-stu-id="3f118-120">Finally drop hello temporary table created in hello first step</span></span>

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a><span data-ttu-id="3f118-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f118-121">Next steps</span></span>
<span data-ttu-id="3f118-122">Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].</span><span class="sxs-lookup"><span data-stu-id="3f118-122">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[terwijl]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
