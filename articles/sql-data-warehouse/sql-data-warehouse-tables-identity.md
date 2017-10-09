---
title: aaaCreate vervangende sleutels met identiteit | Microsoft Docs
description: Meer informatie over hoe toouse identiteit toocreate vervangende sleutels voor tabellen.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="764e7-103">Vervangend sleutels maken met behulp van identiteit</span><span class="sxs-lookup"><span data-stu-id="764e7-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="764e7-104">[Overzicht][Overview]</span><span class="sxs-lookup"><span data-stu-id="764e7-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="764e7-105">[Gegevenstypen][Data Types]</span><span class="sxs-lookup"><span data-stu-id="764e7-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="764e7-106">[Distribueren][Distribute]</span><span class="sxs-lookup"><span data-stu-id="764e7-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="764e7-107">[Index][Index]</span><span class="sxs-lookup"><span data-stu-id="764e7-107">[Index][Index]</span></span>
> * <span data-ttu-id="764e7-108">[Partitie][Partition]</span><span class="sxs-lookup"><span data-stu-id="764e7-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="764e7-109">[Statistieken][Statistics]</span><span class="sxs-lookup"><span data-stu-id="764e7-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="764e7-110">[Tijdelijke][Temporary]</span><span class="sxs-lookup"><span data-stu-id="764e7-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="764e7-111">[Identiteit][Identity]</span><span class="sxs-lookup"><span data-stu-id="764e7-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="764e7-112">Veel gegevens modelers zoals toocreate vervangende sleutels op de tabellen bij het ontwerpen van datawarehouse-modellen.</span><span class="sxs-lookup"><span data-stu-id="764e7-112">Many data modelers like toocreate surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="764e7-113">Kunt u Hallo IDENTITY-eigenschap tooachieve deze doelstelling eenvoudig en effectief zonder laadprestaties.</span><span class="sxs-lookup"><span data-stu-id="764e7-113">You can use hello IDENTITY property tooachieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="764e7-114">Aan de slag met de identiteit</span><span class="sxs-lookup"><span data-stu-id="764e7-114">Get started with IDENTITY</span></span>
<span data-ttu-id="764e7-115">Een tabel kunt u definiëren als Hallo IDENTITY-eigenschap hebben wanneer u eerst Hallo-tabel maken met behulp van de syntaxis die vergelijkbaar toohello-instructie is:</span><span class="sxs-lookup"><span data-stu-id="764e7-115">You can define a table as having hello IDENTITY property when you first create hello table by using syntax that is similar toohello following statement:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

<span data-ttu-id="764e7-116">Vervolgens kunt u `INSERT..SELECT` toopopulate Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="764e7-116">You can then use `INSERT..SELECT` toopopulate hello table.</span></span>

## <a name="behavior"></a><span data-ttu-id="764e7-117">Gedrag</span><span class="sxs-lookup"><span data-stu-id="764e7-117">Behavior</span></span>
<span data-ttu-id="764e7-118">Hallo IDENTITY-eigenschap is ontworpen tooscale uit voor alle Hallo distributies in het datawarehouse Hallo zonder laadprestaties.</span><span class="sxs-lookup"><span data-stu-id="764e7-118">hello IDENTITY property is designed tooscale out across all hello distributions in hello data warehouse without affecting load performance.</span></span> <span data-ttu-id="764e7-119">Hallo-implementatie van de identiteit is daarom gericht op deze doelstellingen te bereiken.</span><span class="sxs-lookup"><span data-stu-id="764e7-119">Therefore, hello implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="764e7-120">In deze sectie worden Hallo nuances van Hallo implementatie toohelp u begrijpen meer volledig.</span><span class="sxs-lookup"><span data-stu-id="764e7-120">This section highlights hello nuances of hello implementation toohelp you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="764e7-121">Toewijzing van waarden</span><span class="sxs-lookup"><span data-stu-id="764e7-121">Allocation of values</span></span>
<span data-ttu-id="764e7-122">Hallo IDENTITY-eigenschap garantie geen Hallo-volgorde in welke Hallo vervangende waarden worden toegewezen, dat overeenkomt met Hallo gedrag van SQL Server en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="764e7-122">hello IDENTITY property doesn't guarantee hello order in which hello surrogate values are allocated, which reflects hello behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="764e7-123">Echter, in Azure SQL Data Warehouse Hallo afwezigheid van een garantie groter is.</span><span class="sxs-lookup"><span data-stu-id="764e7-123">However, in Azure SQL Data Warehouse, hello absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="764e7-124">Hallo volgende voorbeeld wordt een afbeelding:</span><span class="sxs-lookup"><span data-stu-id="764e7-124">hello following example is an illustration:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

<span data-ttu-id="764e7-125">Twee rijen aanvoer in Hallo voorgaande voorbeeld, in distributie 1.</span><span class="sxs-lookup"><span data-stu-id="764e7-125">In hello preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="764e7-126">de eerste rij Hallo Hallo vervangende waarde heeft van 1 in kolom `C1`, en de tweede rij Hallo Hallo vervangende waarde heeft van 61.</span><span class="sxs-lookup"><span data-stu-id="764e7-126">hello first row has hello surrogate value of 1 in column `C1`, and hello second row has hello surrogate value of 61.</span></span> <span data-ttu-id="764e7-127">Van deze waarden zijn gegenereerd door Hallo IDENTITY-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="764e7-127">Both of these values were generated by hello IDENTITY property.</span></span> <span data-ttu-id="764e7-128">Hallo-toewijzing van Hallo waarden is echter niet aaneengesloten.</span><span class="sxs-lookup"><span data-stu-id="764e7-128">However, hello allocation of hello values is not contiguous.</span></span> <span data-ttu-id="764e7-129">Dit gedrag is standaard.</span><span class="sxs-lookup"><span data-stu-id="764e7-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="764e7-130">Vertekende gegevens</span><span class="sxs-lookup"><span data-stu-id="764e7-130">Skewed data</span></span> 
<span data-ttu-id="764e7-131">Hallo-bereik van waarden voor het gegevenstype Hallo gelijkmatig verdeeld over Hallo-distributies.</span><span class="sxs-lookup"><span data-stu-id="764e7-131">hello range of values for hello data type are spread evenly across hello distributions.</span></span> <span data-ttu-id="764e7-132">Als een gedistribueerde tabel leidt dit tot slechtere van vertekende gegevens, Hallo vervolgens bereik van waarden beschikbaar toohello datatype kunt voortijdig worden verbruikt.</span><span class="sxs-lookup"><span data-stu-id="764e7-132">If a distributed table suffers from skewed data, then hello range of values available toohello datatype can be exhausted prematurely.</span></span> <span data-ttu-id="764e7-133">Bijvoorbeeld, als alle Hallo gegevens eindigt in een enkel distributiepunt, heeft effectief Hallo tabel toegang tooonly één zestigste van waarden van het gegevenstype Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="764e7-133">For example, if all hello data ends up in a single distribution, then effectively hello table has access tooonly one-sixtieth of hello values of hello data type.</span></span> <span data-ttu-id="764e7-134">Om deze reden Hallo IDENTITY-eigenschap is beperkt te`INT` en `BIGINT` alleen gegevenstypen.</span><span class="sxs-lookup"><span data-stu-id="764e7-134">For this reason, hello IDENTITY property is limited too`INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="764e7-135">SELECTEREN... IN</span><span class="sxs-lookup"><span data-stu-id="764e7-135">SELECT..INTO</span></span>
<span data-ttu-id="764e7-136">Wanneer een bestaande id-kolom is geselecteerd in een nieuwe tabel, neemt de nieuwe kolom Hallo Hallo IDENTITY-eigenschap, tenzij een Hallo volgende voorwaarden voldaan wordt:</span><span class="sxs-lookup"><span data-stu-id="764e7-136">When an existing IDENTITY column is selected into a new table, hello new column inherits hello IDENTITY property, unless one of hello following conditions is true:</span></span>
- <span data-ttu-id="764e7-137">Hallo SELECT-instructie bevat een join.</span><span class="sxs-lookup"><span data-stu-id="764e7-137">hello SELECT statement contains a join.</span></span>
- <span data-ttu-id="764e7-138">Meerdere SELECT-instructies worden gekoppeld met behulp van de SAMENVOEGING.</span><span class="sxs-lookup"><span data-stu-id="764e7-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="764e7-139">Hallo identiteitskolom is meer dan één keer in de selectielijst Hallo vermeld.</span><span class="sxs-lookup"><span data-stu-id="764e7-139">hello IDENTITY column is listed more than one time in hello SELECT list.</span></span>
- <span data-ttu-id="764e7-140">Hallo identiteitskolom maakt deel uit van een expressie.</span><span class="sxs-lookup"><span data-stu-id="764e7-140">hello IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="764e7-141">Als een van deze voorwaarden voldaan wordt, gemaakt Hallo-kolom niet NULL zijn in plaats van deze Hallo IDENTITY-eigenschap is overgenomen.</span><span class="sxs-lookup"><span data-stu-id="764e7-141">If any one of these conditions is true, hello column is created NOT NULL instead of inheriting hello IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="764e7-142">TABLE AS SELECT MAKEN</span><span class="sxs-lookup"><span data-stu-id="764e7-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="764e7-143">Maak tabel AS selecteren (CTAS) volgt Hallo hetzelfde gedrag van SQL Server die wordt beschreven voor SELECT... IN.</span><span class="sxs-lookup"><span data-stu-id="764e7-143">CREATE TABLE AS SELECT (CTAS) follows hello same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="764e7-144">U kan niet een IDENTITY-eigenschap echter opgeven in de kolomdefinitie Hallo Hallo `CREATE TABLE` deel uit van het Hallo-instructie.</span><span class="sxs-lookup"><span data-stu-id="764e7-144">However, you can't specify an IDENTITY property in hello column definition of hello `CREATE TABLE` part of hello statement.</span></span> <span data-ttu-id="764e7-145">U niet de functie IDENTITY Hallo ook gebruiken in Hallo `SELECT` deel uit van Hallo CTAS.</span><span class="sxs-lookup"><span data-stu-id="764e7-145">You also can't use hello IDENTITY function in hello `SELECT` part of hello CTAS.</span></span> <span data-ttu-id="764e7-146">toopopulate een tabel, moet u toouse `CREATE TABLE` toodefine Hallo tabel gevolgd door `INSERT..SELECT` toopopulate deze.</span><span class="sxs-lookup"><span data-stu-id="764e7-146">toopopulate a table, you need toouse `CREATE TABLE` toodefine hello table followed by `INSERT..SELECT` toopopulate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="764e7-147">Expliciet waarden invoegen in een identiteitskolom</span><span class="sxs-lookup"><span data-stu-id="764e7-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="764e7-148">Biedt ondersteuning voor SQL Data Warehouse `SET IDENTITY_INSERT <your table> ON|OFF` syntaxis.</span><span class="sxs-lookup"><span data-stu-id="764e7-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="764e7-149">U kunt deze syntaxis tooexplicitly insert-waarden in de identiteitskolom hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="764e7-149">You can use this syntax tooexplicitly insert values into hello IDENTITY column.</span></span>

<span data-ttu-id="764e7-150">Veel gegevens modelers zoals toouse vooraf gedefinieerde negatieve van bepaalde rijen in hun dimensies waarden.</span><span class="sxs-lookup"><span data-stu-id="764e7-150">Many data modelers like toouse predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="764e7-151">Een voorbeeld is het Hallo -1 of 'onbekend lid' rij.</span><span class="sxs-lookup"><span data-stu-id="764e7-151">An example is hello -1 or "unknown member" row.</span></span> 

<span data-ttu-id="764e7-152">Hallo volgende script toont hoe tooexplicitly deze rij toevoegen met behulp van IDENTITY_INSERT instellen:</span><span class="sxs-lookup"><span data-stu-id="764e7-152">hello next script shows how tooexplicitly add this row by using SET IDENTITY_INSERT:</span></span>

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="764e7-153">Gegevens laden in een tabel met de identiteit</span><span class="sxs-lookup"><span data-stu-id="764e7-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="764e7-154">Hallo aanwezigheid van Hallo IDENTITY-eigenschap heeft gevolgen tooyour gegevens laden code.</span><span class="sxs-lookup"><span data-stu-id="764e7-154">hello presence of hello IDENTITY property has some implications tooyour data-loading code.</span></span> <span data-ttu-id="764e7-155">Deze sectie worden enkele basispatronen die voor het laden van gegevens in tabellen met behulp van de identiteit.</span><span class="sxs-lookup"><span data-stu-id="764e7-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="764e7-156">Gegevens laden met PolyBase</span><span class="sxs-lookup"><span data-stu-id="764e7-156">Load data with PolyBase</span></span>
<span data-ttu-id="764e7-157">tooload gegevens in een tabel en een vervangend sleutel genereren met behulp van de identiteit, Hallo-tabel maken en vervolgens gebruik INSERT... Selecteer of INSERT... WAARDEN tooperform Hallo belasting.</span><span class="sxs-lookup"><span data-stu-id="764e7-157">tooload data into a table and generate a surrogate key by using IDENTITY, create hello table and then use INSERT..SELECT or INSERT..VALUES tooperform hello load.</span></span>

<span data-ttu-id="764e7-158">Hallo illustreert volgende voorbeeld Hallo basispatroon:</span><span class="sxs-lookup"><span data-stu-id="764e7-158">hello following example highlights hello basic pattern:</span></span>
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT toopopulate hello table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> <span data-ttu-id="764e7-159">Het is niet mogelijk toouse `CREATE TABLE AS SELECT` momenteel bij het laden van gegevens naar een tabel met een identiteitskolom.</span><span class="sxs-lookup"><span data-stu-id="764e7-159">It's not possible toouse `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="764e7-160">Zie voor meer informatie over het laden van gegevens met behulp van hulpprogramma voor Hallo bulksgewijs kopiëren (BCP)-programma Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="764e7-160">For more information on loading data by using hello bulk copy program (BCP) tool, see hello following articles:</span></span>

- <span data-ttu-id="764e7-161">[Laden met PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="764e7-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="764e7-162">[Aanbevolen procedures van PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="764e7-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="764e7-163">Gegevens laden met BCP</span><span class="sxs-lookup"><span data-stu-id="764e7-163">Load data with BCP</span></span>
<span data-ttu-id="764e7-164">BCP is een opdrachtregelprogramma waarmee u gegevens tooload in SQL Data Warehouse kunt.</span><span class="sxs-lookup"><span data-stu-id="764e7-164">BCP is a command-line tool that you can use tooload data into SQL Data Warehouse.</span></span> <span data-ttu-id="764e7-165">Een van de parameters (-E) besturingselementen Hallo gedrag van BCP bij het laden van gegevens naar een tabel met een identiteitskolom.</span><span class="sxs-lookup"><span data-stu-id="764e7-165">One of its parameters (-E) controls hello behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="764e7-166">Wanneer -E wordt opgegeven, worden ondergebracht in Hallo invoerbestand voor Hallo kolom met de identiteit Hallo-waarden worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="764e7-166">When -E is specified, hello values held in hello input file for hello column with IDENTITY are retained.</span></span> <span data-ttu-id="764e7-167">Als E - *niet* opgegeven, wordt het Hallo-waarden in deze kolom worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="764e7-167">If -E is *not* specified, then hello values in this column are ignored.</span></span> <span data-ttu-id="764e7-168">Als de identiteitskolom Hallo niet opgenomen is, is Hallo gegevens normaal geladen.</span><span class="sxs-lookup"><span data-stu-id="764e7-168">If hello identity column is not included, then hello data is loaded as normal.</span></span> <span data-ttu-id="764e7-169">Hallo-waarden worden gegenereerd op basis van toohello increment- en seed-beleid van Hallo-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="764e7-169">hello values are generated according toohello increment and seed policy of hello property.</span></span>

<span data-ttu-id="764e7-170">Zie voor meer informatie over het laden van gegevens met behulp van BCP Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="764e7-170">For more information on loading data by using BCP, see hello following articles:</span></span>

- <span data-ttu-id="764e7-171">[Laden met BCP][]</span><span class="sxs-lookup"><span data-stu-id="764e7-171">[Load with BCP][]</span></span>
- <span data-ttu-id="764e7-172">[BCP in MSDN][]</span><span class="sxs-lookup"><span data-stu-id="764e7-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="764e7-173">Catalogusweergaven</span><span class="sxs-lookup"><span data-stu-id="764e7-173">Catalog views</span></span>
<span data-ttu-id="764e7-174">SQL Data Warehouse ondersteunt Hallo `sys.identity_columns` catalogusweergave.</span><span class="sxs-lookup"><span data-stu-id="764e7-174">SQL Data Warehouse supports hello `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="764e7-175">Deze weergave kan worden gebruikt tooidentify een kolom met Hallo IDENTITY-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="764e7-175">This view can be used tooidentify a column that has hello IDENTITY property.</span></span>

<span data-ttu-id="764e7-176">dit voorbeeld ziet u toohelp Hallo-databaseschema beter te begrijpen, hoe toointegrate `sys.identity_columns` met andere weergaven van de catalogus system:</span><span class="sxs-lookup"><span data-stu-id="764e7-176">toohelp you better understand hello database schema, this example shows how toointegrate `sys.identity_columns` with other system catalog views:</span></span>

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a><span data-ttu-id="764e7-177">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="764e7-177">Limitations</span></span>
<span data-ttu-id="764e7-178">Hallo IDENTITY-eigenschap kan niet worden gebruikt in Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="764e7-178">hello IDENTITY property can't be used in hello following scenarios:</span></span>
- <span data-ttu-id="764e7-179">Waar Hallo kolomgegevenstype is niet INT of BIGINT</span><span class="sxs-lookup"><span data-stu-id="764e7-179">Where hello column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="764e7-180">Hallo-kolom is waar ook Hallo distributiesleutel</span><span class="sxs-lookup"><span data-stu-id="764e7-180">Where hello column is also hello distribution key</span></span>
- <span data-ttu-id="764e7-181">Waar Hallo-tabel is een externe tabel</span><span class="sxs-lookup"><span data-stu-id="764e7-181">Where hello table is an external table</span></span> 

<span data-ttu-id="764e7-182">Hallo verwante functies te volgen, worden niet ondersteund in SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="764e7-182">hello following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="764e7-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="764e7-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="764e7-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="764e7-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="764e7-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="764e7-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="764e7-186">[IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="764e7-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="764e7-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="764e7-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="764e7-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="764e7-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="764e7-189">[DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="764e7-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="764e7-190">Taken</span><span class="sxs-lookup"><span data-stu-id="764e7-190">Tasks</span></span>

<span data-ttu-id="764e7-191">Deze sectie vindt u enkele voorbeelden van code kunt u algemene taken tooperform wanneer u met de id-kolommen werkt.</span><span class="sxs-lookup"><span data-stu-id="764e7-191">This section provides some sample code you can use tooperform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="764e7-192">Kolom C1 is Hallo identiteit in alle Hallo taken te volgen.</span><span class="sxs-lookup"><span data-stu-id="764e7-192">Column C1 is hello IDENTITY in all hello following tasks.</span></span>
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a><span data-ttu-id="764e7-193">Hallo hoogste toegewezen waarde vinden voor een tabel</span><span class="sxs-lookup"><span data-stu-id="764e7-193">Find hello highest allocated value for a table</span></span>
<span data-ttu-id="764e7-194">Gebruik Hallo `MAX()` toodetermine Hallo hoogste toegewezen waarde voor een gedistribueerde tabel werken:</span><span class="sxs-lookup"><span data-stu-id="764e7-194">Use hello `MAX()` function toodetermine hello highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a><span data-ttu-id="764e7-195">Hallo seed- en increment vinden voor Hallo IDENTITY-eigenschap</span><span class="sxs-lookup"><span data-stu-id="764e7-195">Find hello seed and increment for hello IDENTITY property</span></span>
<span data-ttu-id="764e7-196">U kunt Hallo catalogus weergaven toodiscover Hallo increment- en seed configuratie identiteitswaarden gebruiken voor een tabel met behulp van de volgende query Hallo:</span><span class="sxs-lookup"><span data-stu-id="764e7-196">You can use hello catalog views toodiscover hello identity increment and seed configuration values for a table by using hello following query:</span></span> 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a><span data-ttu-id="764e7-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="764e7-197">Next steps</span></span>

* <span data-ttu-id="764e7-198">toolearn meer informatie over het ontwikkelen van tabellen, Zie [tabel overzicht][Overview], [tabel gegevenstypen][Data Types], [een tabeldistribueren] [ Distribute], [Indexeren van een tabel][Index], [partitie van een tabel][Partition], en [ Tijdelijke tabellen][Temporary].</span><span class="sxs-lookup"><span data-stu-id="764e7-198">toolearn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="764e7-199">Zie voor meer informatie over best practices [aanbevolen procedures voor SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="764e7-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

[Laden met bcp]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[Laden met PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[Aanbevolen procedures van PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[BCP in MSDN]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
