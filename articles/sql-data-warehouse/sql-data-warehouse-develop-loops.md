---
title: Gebruikmaken van T-SQL-lussen in Azure SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: 40a872ff310f48bfd543ac184fe7301b85b50258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="loops-in-sql-data-warehouse"></a><span data-ttu-id="58c8a-103">Lussen in SQL datawarehouse</span><span class="sxs-lookup"><span data-stu-id="58c8a-103">Loops in SQL Data Warehouse</span></span>
<span data-ttu-id="58c8a-104">SQL Data Warehouse ondersteunt de [terwijl][terwijl] lus voor herhaaldelijk blokken instructie uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="58c8a-104">SQL Data Warehouse supports the [WHILE][WHILE] loop for repeatedly executing statement blocks.</span></span> <span data-ttu-id="58c8a-105">Dit wordt voortgezet voor als de opgegeven voorwaarden voldaan wordt, of tot de code specifiek de lus met behulp van beëindigt de `BREAK` sleutelwoord.</span><span class="sxs-lookup"><span data-stu-id="58c8a-105">This will continue for as long as the specified conditions are true or until the code specifically terminates the loop using the `BREAK` keyword.</span></span> <span data-ttu-id="58c8a-106">Lussen zijn bijzonder nuttig voor het vervangen van cursors die zijn gedefinieerd in SQL-code.</span><span class="sxs-lookup"><span data-stu-id="58c8a-106">Loops are particularly useful for replacing cursors defined in SQL code.</span></span> <span data-ttu-id="58c8a-107">Gelukkig bijna alle cursors die zijn geschreven in SQL-code zijn van de snel vooruit-lezen alleen groot.</span><span class="sxs-lookup"><span data-stu-id="58c8a-107">Fortunately, almost all cursors that are written in SQL code are of the fast forward, read only variety.</span></span> <span data-ttu-id="58c8a-108">Daarom [terwijl] lussen vormen een geweldige alternatief als u dat merkt wilt vervangen.</span><span class="sxs-lookup"><span data-stu-id="58c8a-108">Therefore [WHILE] loops are a great alternative if you find yourself having to replace one.</span></span>

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a><span data-ttu-id="58c8a-109">Gebruik van lussen en vervangt cursors in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="58c8a-109">Leveraging loops and replacing cursors in SQL Data Warehouse</span></span>
<span data-ttu-id="58c8a-110">Echter eerst in head wilt voordat u moet zelf de volgende vraag stellen: 'Kan deze cursor worden opnieuw geschreven naar set op basis van bewerkingen gebruiken?'.</span><span class="sxs-lookup"><span data-stu-id="58c8a-110">However, before diving in head first you should ask yourself the following question: "Could this cursor be re-written to use set based operations?".</span></span> <span data-ttu-id="58c8a-111">In veel gevallen is het antwoord Ja zijn, en is vaak de aanbevolen aanpak.</span><span class="sxs-lookup"><span data-stu-id="58c8a-111">In many cases the answer will be yes and is often the best approach.</span></span> <span data-ttu-id="58c8a-112">Een set op basis van de bewerking vaak voert aanzienlijk sneller dan een benadering iteratieve, per rij.</span><span class="sxs-lookup"><span data-stu-id="58c8a-112">A set based operation often performs significantly faster than an iterative, row by row approach.</span></span>

<span data-ttu-id="58c8a-113">Vooruit cursors voor alleen-lezen kunnen eenvoudig worden vervangen door een samenvoegartikel constructie.</span><span class="sxs-lookup"><span data-stu-id="58c8a-113">Fast forward read-only cursors can be easily replaced with a looping construct.</span></span> <span data-ttu-id="58c8a-114">Hieronder vindt u een eenvoudig voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="58c8a-114">Below is a simple example.</span></span> <span data-ttu-id="58c8a-115">Dit codevoorbeeld werkt de statistieken voor elke tabel in de database.</span><span class="sxs-lookup"><span data-stu-id="58c8a-115">This code example updates the statistics for every table in the database.</span></span> <span data-ttu-id="58c8a-116">Door iteratie van de tabellen in de lus kunnen we elke opdracht wordt uitgevoerd in de reeks.</span><span class="sxs-lookup"><span data-stu-id="58c8a-116">By iterating over the tables in the loop we are able to execute each command in sequence.</span></span>

<span data-ttu-id="58c8a-117">Maak eerst een tijdelijke tabel die een unieke rij-getal gebruikt voor het identificeren van de afzonderlijke instructies:</span><span class="sxs-lookup"><span data-stu-id="58c8a-117">First, create a temporary table containing a unique row number used to identify the individual statements:</span></span>

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

<span data-ttu-id="58c8a-118">Ten tweede initialiseren van de variabelen die zijn vereist voor het uitvoeren van de lus:</span><span class="sxs-lookup"><span data-stu-id="58c8a-118">Second, initialize the variables required to perform the loop:</span></span>

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

<span data-ttu-id="58c8a-119">Nu op een uitvoeren-instructies in een lus tegelijk:</span><span class="sxs-lookup"><span data-stu-id="58c8a-119">Now loop over statements executing them one at a time:</span></span>

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

<span data-ttu-id="58c8a-120">Ten slotte de tijdelijke tabel die is gemaakt in de eerste stap verwijderen</span><span class="sxs-lookup"><span data-stu-id="58c8a-120">Finally drop the temporary table created in the first step</span></span>

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->

## <a name="next-steps"></a><span data-ttu-id="58c8a-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="58c8a-121">Next steps</span></span>
<span data-ttu-id="58c8a-122">Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].</span><span class="sxs-lookup"><span data-stu-id="58c8a-122">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
<span data-ttu-id="58c8a-123">[terwijl]: https://msdn.microsoft.com/library/ms178642.aspx</span><span class="sxs-lookup"><span data-stu-id="58c8a-123">[WHILE]: https://msdn.microsoft.com/library/ms178642.aspx</span></span>


<!--Other Web references-->
