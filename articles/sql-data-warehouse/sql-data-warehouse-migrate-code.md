---
title: aaaMigrate uw code tooSQL voor SQL Data Warehouse | Microsoft Docs
description: Tips voor het migreren van uw SQL-code tooAzure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 19c252a3-0e41-4eec-9d3e-09a68c7e7add
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/23/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 7a16d579d068e9df9aba3dc61e4a09bcaa551588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-code-toosql-data-warehouse"></a><span data-ttu-id="1732f-103">Uw code tooSQL voor SQL Data Warehouse migreren</span><span class="sxs-lookup"><span data-stu-id="1732f-103">Migrate your SQL code tooSQL Data Warehouse</span></span>
<span data-ttu-id="1732f-104">Dit artikel wordt uitgelegd codewijzigingen moet u waarschijnlijk toomake bij het migreren van uw code vanaf een andere database tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1732f-104">This article explains code changes you will probably need toomake when migrating your code from another database tooSQL Data Warehouse.</span></span> <span data-ttu-id="1732f-105">Sommige functies van SQL Data Warehouse kunnen de prestaties aanzienlijk verbeteren omdat ze ontworpen toowork in een gedistribueerde wijze zijn.</span><span class="sxs-lookup"><span data-stu-id="1732f-105">Some SQL Data Warehouse features can significantly improve performance as they are designed toowork in a distributed fashion.</span></span> <span data-ttu-id="1732f-106">Echter toomaintain prestaties en schaalbaarheid, sommige functies zijn ook niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="1732f-106">However, toomaintain performance and scale, some features are also not available.</span></span>

## <a name="common-t-sql-limitations"></a><span data-ttu-id="1732f-107">Algemene T-SQL-beperkingen</span><span class="sxs-lookup"><span data-stu-id="1732f-107">Common T-SQL Limitations</span></span>
<span data-ttu-id="1732f-108">Hallo volgende lijst bevat een overzicht van de meest voorkomende Hallo-functies die biedt geen ondersteuning voor SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1732f-108">hello following list summarizes hello most common features that SQL Data Warehouse does not support.</span></span> <span data-ttu-id="1732f-109">Hallo koppelingen kunt u tooworkarounds voor Hallo niet-ondersteunde functies:</span><span class="sxs-lookup"><span data-stu-id="1732f-109">hello links take you tooworkarounds for hello unsupported features:</span></span>

* <span data-ttu-id="1732f-110">[ANSI joins op updates][ANSI joins on updates]</span><span class="sxs-lookup"><span data-stu-id="1732f-110">[ANSI joins on updates][ANSI joins on updates]</span></span>
* <span data-ttu-id="1732f-111">[ANSI-verbindingen in verwijderen][ANSI joins on deletes]</span><span class="sxs-lookup"><span data-stu-id="1732f-111">[ANSI joins on deletes][ANSI joins on deletes]</span></span>
* <span data-ttu-id="1732f-112">[Merge-instructie][merge statement]</span><span class="sxs-lookup"><span data-stu-id="1732f-112">[merge statement][merge statement]</span></span>
* <span data-ttu-id="1732f-113">meerdere databases joins</span><span class="sxs-lookup"><span data-stu-id="1732f-113">cross-database joins</span></span>
* <span data-ttu-id="1732f-114">[cursors][cursors]</span><span class="sxs-lookup"><span data-stu-id="1732f-114">[cursors][cursors]</span></span>
* <span data-ttu-id="1732f-115">[INSERT... EXEC][INSERT..EXEC]</span><span class="sxs-lookup"><span data-stu-id="1732f-115">[INSERT..EXEC][INSERT..EXEC]</span></span>
* <span data-ttu-id="1732f-116">OUTPUT-component</span><span class="sxs-lookup"><span data-stu-id="1732f-116">output clause</span></span>
* <span data-ttu-id="1732f-117">de gebruiker gedefinieerde inlinefuncties</span><span class="sxs-lookup"><span data-stu-id="1732f-117">inline user-defined functions</span></span>
* <span data-ttu-id="1732f-118">meerdere instructies functies</span><span class="sxs-lookup"><span data-stu-id="1732f-118">multi-statement functions</span></span>
* [<span data-ttu-id="1732f-119">algemene tabelexpressies</span><span class="sxs-lookup"><span data-stu-id="1732f-119">common table expressions</span></span>](#Common-table-expressions)
* <span data-ttu-id="1732f-120">[recursieve algemene tabelexpressies (CTE)] (#Recursive-common-table-expressions-(CTE)</span><span class="sxs-lookup"><span data-stu-id="1732f-120">[recursive common table expressions (CTE)](#Recursive-common-table-expressions-(CTE)</span></span>
* <span data-ttu-id="1732f-121">CLR-functies en procedures</span><span class="sxs-lookup"><span data-stu-id="1732f-121">CLR functions and procedures</span></span>
* <span data-ttu-id="1732f-122">de functie $partition</span><span class="sxs-lookup"><span data-stu-id="1732f-122">$partition function</span></span>
* <span data-ttu-id="1732f-123">tabelvariabelen voor de</span><span class="sxs-lookup"><span data-stu-id="1732f-123">table variables</span></span>
* <span data-ttu-id="1732f-124">de parameters voor waarde</span><span class="sxs-lookup"><span data-stu-id="1732f-124">table value parameters</span></span>
* <span data-ttu-id="1732f-125">gedistribueerde transacties</span><span class="sxs-lookup"><span data-stu-id="1732f-125">distributed transactions</span></span>
* <span data-ttu-id="1732f-126">Commit / rollback werken</span><span class="sxs-lookup"><span data-stu-id="1732f-126">commit / rollback work</span></span>
* <span data-ttu-id="1732f-127">transactie opslaan</span><span class="sxs-lookup"><span data-stu-id="1732f-127">save transaction</span></span>
* <span data-ttu-id="1732f-128">uitvoering contexten (EXECUTE AS)</span><span class="sxs-lookup"><span data-stu-id="1732f-128">execution contexts (EXECUTE AS)</span></span>
* <span data-ttu-id="1732f-129">[Group by, component met rollup / kubus / sets opties voor groeperen][group by clause with rollup / cube / grouping sets options]</span><span class="sxs-lookup"><span data-stu-id="1732f-129">[group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options]</span></span>
* <span data-ttu-id="1732f-130">[geneste niveaus dan 8][nesting levels beyond 8]</span><span class="sxs-lookup"><span data-stu-id="1732f-130">[nesting levels beyond 8][nesting levels beyond 8]</span></span>
* <span data-ttu-id="1732f-131">[door weergaven bijwerken][updating through views]</span><span class="sxs-lookup"><span data-stu-id="1732f-131">[updating through views][updating through views]</span></span>
* <span data-ttu-id="1732f-132">[gebruik van selecteren voor de toewijzing van variabele][use of select for variable assignment]</span><span class="sxs-lookup"><span data-stu-id="1732f-132">[use of select for variable assignment][use of select for variable assignment]</span></span>
* <span data-ttu-id="1732f-133">[Er is geen MAX-gegevenstype voor dynamische SQL-tekenreeksen][no MAX data type for dynamic SQL strings]</span><span class="sxs-lookup"><span data-stu-id="1732f-133">[no MAX data type for dynamic SQL strings][no MAX data type for dynamic SQL strings]</span></span>

<span data-ttu-id="1732f-134">De meeste van deze beperkingen kunt gelukkig rond worden gewerkt.</span><span class="sxs-lookup"><span data-stu-id="1732f-134">Fortunately most of these limitations can be worked around.</span></span> <span data-ttu-id="1732f-135">Uitleg vindt u in Hallo relevante ontwikkeling artikelen waarnaar wordt verwezen hierboven.</span><span class="sxs-lookup"><span data-stu-id="1732f-135">Explanations are provided in hello relevant development articles referenced above.</span></span>

## <a name="supported-cte-features"></a><span data-ttu-id="1732f-136">Ondersteunde CTE-functies</span><span class="sxs-lookup"><span data-stu-id="1732f-136">Supported CTE features</span></span>
<span data-ttu-id="1732f-137">Algemene tabelexpressies (CTE's) worden gedeeltelijk ondersteund in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1732f-137">Common table expressions (CTEs) are partially supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="1732f-138">Hallo volgende CTE kenmerken worden momenteel ondersteund:</span><span class="sxs-lookup"><span data-stu-id="1732f-138">hello following CTE features are currently supported:</span></span>

* <span data-ttu-id="1732f-139">Een CTE kan worden opgegeven in een SELECT-instructie.</span><span class="sxs-lookup"><span data-stu-id="1732f-139">A CTE can be specified in a SELECT statement.</span></span>
* <span data-ttu-id="1732f-140">Een CTE kan worden opgegeven in een instructie CREATE VIEW.</span><span class="sxs-lookup"><span data-stu-id="1732f-140">A CTE can be specified in a CREATE VIEW statement.</span></span>
* <span data-ttu-id="1732f-141">Een CTE kan worden opgegeven in een instructie maken tabel AS selecteren (CTAS).</span><span class="sxs-lookup"><span data-stu-id="1732f-141">A CTE can be specified in a CREATE TABLE AS SELECT (CTAS) statement.</span></span>
* <span data-ttu-id="1732f-142">Een CTE kan worden opgegeven in een instructie maken externe tabel AS selecteren (CRTAS).</span><span class="sxs-lookup"><span data-stu-id="1732f-142">A CTE can be specified in a CREATE REMOTE TABLE AS SELECT (CRTAS) statement.</span></span>
* <span data-ttu-id="1732f-143">Een CTE kan worden opgegeven in een instructie maken externe tabel AS selecteren (CETAS).</span><span class="sxs-lookup"><span data-stu-id="1732f-143">A CTE can be specified in a CREATE EXTERNAL TABLE AS SELECT (CETAS) statement.</span></span>
* <span data-ttu-id="1732f-144">Een externe tabel kan worden verwezen vanuit een CTE.</span><span class="sxs-lookup"><span data-stu-id="1732f-144">A remote table can be referenced from a CTE.</span></span>
* <span data-ttu-id="1732f-145">Een externe tabel kan worden verwezen vanuit een CTE.</span><span class="sxs-lookup"><span data-stu-id="1732f-145">An external table can be referenced from a CTE.</span></span>
* <span data-ttu-id="1732f-146">Meerdere definities voor CTE-query kunnen worden gedefinieerd in een CTE.</span><span class="sxs-lookup"><span data-stu-id="1732f-146">Multiple CTE query definitions can be defined in a CTE.</span></span>

## <a name="cte-limitations"></a><span data-ttu-id="1732f-147">CTE-beperkingen</span><span class="sxs-lookup"><span data-stu-id="1732f-147">CTE Limitations</span></span>
<span data-ttu-id="1732f-148">Algemene tabelexpressies hebben enkele beperkingen in SQL Data Warehouse, waaronder:</span><span class="sxs-lookup"><span data-stu-id="1732f-148">Common table expressions have some limitations in SQL Data Warehouse including:</span></span>

* <span data-ttu-id="1732f-149">Een CTE moet worden gevolgd door één SELECT-instructie.</span><span class="sxs-lookup"><span data-stu-id="1732f-149">A CTE must be followed by a single SELECT statement.</span></span> <span data-ttu-id="1732f-150">INSERT, UPDATE, DELETE, en MERGE-instructies worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="1732f-150">INSERT, UPDATE, DELETE, and MERGE statements are not supported.</span></span>
* <span data-ttu-id="1732f-151">Een algemene tabelexpressie met verwijzingen tooitself (een recursieve algemene tabelexpressie) wordt niet ondersteund (Zie onderstaande sectie).</span><span class="sxs-lookup"><span data-stu-id="1732f-151">A common table expression that includes references tooitself (a recursive common table expression) is not supported (see below section).</span></span>
* <span data-ttu-id="1732f-152">Het opgeven van meer dan één met de component in een CTE is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="1732f-152">Specifying more than one WITH clause in a CTE is not allowed.</span></span> <span data-ttu-id="1732f-153">Bijvoorbeeld, als een CTE_query_definition een subquery bevat, kan geen die subquery bevatten een geneste met component die een andere CTE definieert.</span><span class="sxs-lookup"><span data-stu-id="1732f-153">For example, if a CTE_query_definition contains a subquery, that subquery cannot contain a nested WITH clause that defines another CTE.</span></span>
* <span data-ttu-id="1732f-154">Een component ORDER BY kan niet worden gebruikt in Hallo CTE_query_definition, behalve wanneer de component TOP is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="1732f-154">An ORDER BY clause cannot be used in hello CTE_query_definition, except when a TOP clause is specified.</span></span>
* <span data-ttu-id="1732f-155">Wanneer een CTE wordt gebruikt in een instructie die deel uitmaakt van een batch, worden Hallo-instructie in voordat deze gevolgd door een puntkomma.</span><span class="sxs-lookup"><span data-stu-id="1732f-155">When a CTE is used in a statement that is part of a batch, hello statement before it must be followed by a semicolon.</span></span>
* <span data-ttu-id="1732f-156">Wanneer gebruikt in instructies sp_prepare voorbereid, CTE's gedragen Hallo dezelfde manier als andere SELECT-instructies in PDW.</span><span class="sxs-lookup"><span data-stu-id="1732f-156">When used in statements prepared by sp_prepare, CTEs will behave hello same way as other SELECT statements in PDW.</span></span> <span data-ttu-id="1732f-157">Echter als CTE's worden gebruikt als onderdeel van CETAS sp_prepare voorbereid, kunt Hallo gedrag uitstellen van SQL Server en andere instructies PDW vanwege Hallo manier binding voor sp_prepare is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="1732f-157">However, if CTEs are used as part of CETAS prepared by sp_prepare, hello behavior can defer from SQL Server and other PDW statements because of hello way binding is implemented for sp_prepare.</span></span> <span data-ttu-id="1732f-158">Als SELECT verwijzingen die CTE met behulp van een verkeerde kolom niet in CTE bestaat Hallo sp_prepare inactiviteit Hallo fout detecteren, maar Hallo fout gegenereerd tijdens sp_execute in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="1732f-158">If SELECT that references CTE is using a wrong column that does not exist in CTE, hello sp_prepare will pass without detecting hello error, but hello error will be thrown during sp_execute instead.</span></span>

## <a name="recursive-ctes"></a><span data-ttu-id="1732f-159">Recursieve CTE 's</span><span class="sxs-lookup"><span data-stu-id="1732f-159">Recursive CTEs</span></span>
<span data-ttu-id="1732f-160">Recursieve CTE's worden niet ondersteund in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1732f-160">Recursive CTEs are not supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="1732f-161">Hallo-migratie van recursieve CTE kan erg complex en beste Hallo-proces is toobreak in meerdere stappen.</span><span class="sxs-lookup"><span data-stu-id="1732f-161">hello migration of recursive CTE can be somewhat complex and hello best process is toobreak it into multiple steps.</span></span> <span data-ttu-id="1732f-162">U kunt gewoonlijk een lus gebruiken en een tijdelijke tabel invullen zoals doorlopen van tussentijdse Hallo recursieve query's.</span><span class="sxs-lookup"><span data-stu-id="1732f-162">You can typically use a loop and populate a temporary table as you iterate over hello recursive interim queries.</span></span> <span data-ttu-id="1732f-163">Zodra de tijdelijke tabel hello wordt ingevuld kunt u vervolgens Hallo gegevens als een resultaatset één retourneren.</span><span class="sxs-lookup"><span data-stu-id="1732f-163">Once hello temporary table is populated you can then return hello data as a single result set.</span></span> <span data-ttu-id="1732f-164">Een soortgelijke benadering is gebruikte toosolve `GROUP BY WITH CUBE` in Hallo [group by, component met rollup / kubus / sets opties voor groeperen] [ group by clause with rollup / cube / grouping sets options] artikel.</span><span class="sxs-lookup"><span data-stu-id="1732f-164">A similar approach has been used toosolve `GROUP BY WITH CUBE` in hello [group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options] article.</span></span>

## <a name="unsupported-system-functions"></a><span data-ttu-id="1732f-165">Niet-ondersteunde systeemfuncties</span><span class="sxs-lookup"><span data-stu-id="1732f-165">Unsupported system functions</span></span>
<span data-ttu-id="1732f-166">Er zijn ook enkele systeemfuncties die worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="1732f-166">There are also some system functions that are not supported.</span></span> <span data-ttu-id="1732f-167">Enkele van Hallo belangrijkste die u doorgaans wellicht gebruikt in de gegevensopslag zijn:</span><span class="sxs-lookup"><span data-stu-id="1732f-167">Some of hello main ones you might typically find used in data warehousing are:</span></span>

* <span data-ttu-id="1732f-168">NEWSEQUENTIALID()</span><span class="sxs-lookup"><span data-stu-id="1732f-168">NEWSEQUENTIALID()</span></span>
* <span data-ttu-id="1732f-169">@@NESTLEVEL()</span><span class="sxs-lookup"><span data-stu-id="1732f-169">@@NESTLEVEL()</span></span>
* <span data-ttu-id="1732f-170">@@IDENTITY()</span><span class="sxs-lookup"><span data-stu-id="1732f-170">@@IDENTITY()</span></span>
* <span data-ttu-id="1732f-171">@@ROWCOUNT()</span><span class="sxs-lookup"><span data-stu-id="1732f-171">@@ROWCOUNT()</span></span>
* <span data-ttu-id="1732f-172">ROWCOUNT_BIG</span><span class="sxs-lookup"><span data-stu-id="1732f-172">ROWCOUNT_BIG</span></span>
* <span data-ttu-id="1732f-173">ERROR_LINE()</span><span class="sxs-lookup"><span data-stu-id="1732f-173">ERROR_LINE()</span></span>

<span data-ttu-id="1732f-174">Sommige van deze problemen kunnen worden uitgevoerd om.</span><span class="sxs-lookup"><span data-stu-id="1732f-174">Some of these issues can be worked around.</span></span>

## <a name="rowcount-workaround"></a><span data-ttu-id="1732f-175">@@ROWCOUNT tijdelijke oplossing</span><span class="sxs-lookup"><span data-stu-id="1732f-175">@@ROWCOUNT workaround</span></span>
<span data-ttu-id="1732f-176">toowork rond onvoldoende ondersteuning voor @@ROWCOUNT, maakt u een opgeslagen procedure die de laatste rijtelling Hallo ophalen uit sys.dm_pdw_request_steps en vervolgens uitgevoerd `EXEC LastRowCount` na een DML-instructie.</span><span class="sxs-lookup"><span data-stu-id="1732f-176">toowork around lack of support for @@ROWCOUNT, create a stored procedure that will retrieve hello last row count from sys.dm_pdw_request_steps and then execute `EXEC LastRowCount` after a DML statement.</span></span>

```sql
CREATE PROCEDURE LastRowCount AS
WITH LastRequest as 
(   SELECT TOP 1    request_id
    FROM            sys.dm_pdw_exec_requests
    WHERE           session_id = SESSION_ID()
    AND             resource_class IS NOT NULL
    ORDER BY end_time DESC
),
LastRequestRowCounts as
(
    SELECT  step_index, row_count
    FROM    sys.dm_pdw_request_steps
    WHERE   row_count >= 0
    AND     request_id IN (SELECT request_id from LastRequest)
)
SELECT TOP 1 row_count FROM LastRequestRowCounts ORDER BY step_index DESC
;
```

## <a name="next-steps"></a><span data-ttu-id="1732f-177">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1732f-177">Next steps</span></span>
<span data-ttu-id="1732f-178">Zie voor een volledige lijst met alle ondersteunde T-SQL-instructies, [Transact-SQL-onderwerpen][Transact-SQL topics].</span><span class="sxs-lookup"><span data-stu-id="1732f-178">For a complete list of all supported T-SQL statements, see [Transact-SQL topics][Transact-SQL topics].</span></span>

<!--Image references-->

<!--Article references-->
[ANSI joins on updates]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[ANSI joins on deletes]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[merge statement]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[INSERT..EXEC]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[Transact-SQL topics]: ./sql-data-warehouse-reference-tsql-statements.md

[cursors]: ./sql-data-warehouse-develop-loops.md
[group by clause with rollup / cube / grouping sets options]: ./sql-data-warehouse-develop-group-by-options.md
[nesting levels beyond 8]: ./sql-data-warehouse-develop-transactions.md
[updating through views]: ./sql-data-warehouse-develop-views.md
[use of select for variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[no MAX data type for dynamic SQL strings]: ./sql-data-warehouse-develop-dynamic-sql.md

<!--MSDN references-->

<!--Other Web references-->
