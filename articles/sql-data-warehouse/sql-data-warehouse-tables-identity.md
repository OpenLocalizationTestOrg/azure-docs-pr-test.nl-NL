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
# <a name="create-surrogate-keys-by-using-identity"></a>Vervangend sleutels maken met behulp van identiteit
> [!div class="op_single_selector"]
> * [Overzicht][Overview]
> * [Gegevenstypen][Data Types]
> * [Distribueren][Distribute]
> * [Index][Index]
> * [Partitie][Partition]
> * [Statistieken][Statistics]
> * [Tijdelijke][Temporary]
> * [Identiteit][Identity]
> 
> 

Veel gegevens modelers zoals toocreate vervangende sleutels op de tabellen bij het ontwerpen van datawarehouse-modellen. Kunt u Hallo IDENTITY-eigenschap tooachieve deze doelstelling eenvoudig en effectief zonder laadprestaties. 

## <a name="get-started-with-identity"></a>Aan de slag met de identiteit
Een tabel kunt u definiëren als Hallo IDENTITY-eigenschap hebben wanneer u eerst Hallo-tabel maken met behulp van de syntaxis die vergelijkbaar toohello-instructie is:

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

Vervolgens kunt u `INSERT..SELECT` toopopulate Hallo tabel.

## <a name="behavior"></a>Gedrag
Hallo IDENTITY-eigenschap is ontworpen tooscale uit voor alle Hallo distributies in het datawarehouse Hallo zonder laadprestaties. Hallo-implementatie van de identiteit is daarom gericht op deze doelstellingen te bereiken. In deze sectie worden Hallo nuances van Hallo implementatie toohelp u begrijpen meer volledig.  

### <a name="allocation-of-values"></a>Toewijzing van waarden
Hallo IDENTITY-eigenschap garantie geen Hallo-volgorde in welke Hallo vervangende waarden worden toegewezen, dat overeenkomt met Hallo gedrag van SQL Server en Azure SQL Database. Echter, in Azure SQL Data Warehouse Hallo afwezigheid van een garantie groter is. 

Hallo volgende voorbeeld wordt een afbeelding:

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

Twee rijen aanvoer in Hallo voorgaande voorbeeld, in distributie 1. de eerste rij Hallo Hallo vervangende waarde heeft van 1 in kolom `C1`, en de tweede rij Hallo Hallo vervangende waarde heeft van 61. Van deze waarden zijn gegenereerd door Hallo IDENTITY-eigenschap. Hallo-toewijzing van Hallo waarden is echter niet aaneengesloten. Dit gedrag is standaard.

### <a name="skewed-data"></a>Vertekende gegevens 
Hallo-bereik van waarden voor het gegevenstype Hallo gelijkmatig verdeeld over Hallo-distributies. Als een gedistribueerde tabel leidt dit tot slechtere van vertekende gegevens, Hallo vervolgens bereik van waarden beschikbaar toohello datatype kunt voortijdig worden verbruikt. Bijvoorbeeld, als alle Hallo gegevens eindigt in een enkel distributiepunt, heeft effectief Hallo tabel toegang tooonly één zestigste van waarden van het gegevenstype Hallo Hallo. Om deze reden Hallo IDENTITY-eigenschap is beperkt te`INT` en `BIGINT` alleen gegevenstypen.

### <a name="selectinto"></a>SELECTEREN... IN
Wanneer een bestaande id-kolom is geselecteerd in een nieuwe tabel, neemt de nieuwe kolom Hallo Hallo IDENTITY-eigenschap, tenzij een Hallo volgende voorwaarden voldaan wordt:
- Hallo SELECT-instructie bevat een join.
- Meerdere SELECT-instructies worden gekoppeld met behulp van de SAMENVOEGING.
- Hallo identiteitskolom is meer dan één keer in de selectielijst Hallo vermeld.
- Hallo identiteitskolom maakt deel uit van een expressie.
    
Als een van deze voorwaarden voldaan wordt, gemaakt Hallo-kolom niet NULL zijn in plaats van deze Hallo IDENTITY-eigenschap is overgenomen.

### <a name="create-table-as-select"></a>TABLE AS SELECT MAKEN
Maak tabel AS selecteren (CTAS) volgt Hallo hetzelfde gedrag van SQL Server die wordt beschreven voor SELECT... IN. U kan niet een IDENTITY-eigenschap echter opgeven in de kolomdefinitie Hallo Hallo `CREATE TABLE` deel uit van het Hallo-instructie. U niet de functie IDENTITY Hallo ook gebruiken in Hallo `SELECT` deel uit van Hallo CTAS. toopopulate een tabel, moet u toouse `CREATE TABLE` toodefine Hallo tabel gevolgd door `INSERT..SELECT` toopopulate deze.

## <a name="explicitly-insert-values-into-an-identity-column"></a>Expliciet waarden invoegen in een identiteitskolom 
Biedt ondersteuning voor SQL Data Warehouse `SET IDENTITY_INSERT <your table> ON|OFF` syntaxis. U kunt deze syntaxis tooexplicitly insert-waarden in de identiteitskolom hello gebruiken.

Veel gegevens modelers zoals toouse vooraf gedefinieerde negatieve van bepaalde rijen in hun dimensies waarden. Een voorbeeld is het Hallo -1 of 'onbekend lid' rij. 

Hallo volgende script toont hoe tooexplicitly deze rij toevoegen met behulp van IDENTITY_INSERT instellen:

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

## <a name="load-data-into-a-table-with-identity"></a>Gegevens laden in een tabel met de identiteit

Hallo aanwezigheid van Hallo IDENTITY-eigenschap heeft gevolgen tooyour gegevens laden code. Deze sectie worden enkele basispatronen die voor het laden van gegevens in tabellen met behulp van de identiteit. 

### <a name="load-data-with-polybase"></a>Gegevens laden met PolyBase
tooload gegevens in een tabel en een vervangend sleutel genereren met behulp van de identiteit, Hallo-tabel maken en vervolgens gebruik INSERT... Selecteer of INSERT... WAARDEN tooperform Hallo belasting.

Hallo illustreert volgende voorbeeld Hallo basispatroon:
 
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
> Het is niet mogelijk toouse `CREATE TABLE AS SELECT` momenteel bij het laden van gegevens naar een tabel met een identiteitskolom.
> 

Zie voor meer informatie over het laden van gegevens met behulp van hulpprogramma voor Hallo bulksgewijs kopiëren (BCP)-programma Hallo artikelen te volgen:

- [Laden met PolyBase][]
- [Aanbevolen procedures van PolyBase][]

### <a name="load-data-with-bcp"></a>Gegevens laden met BCP
BCP is een opdrachtregelprogramma waarmee u gegevens tooload in SQL Data Warehouse kunt. Een van de parameters (-E) besturingselementen Hallo gedrag van BCP bij het laden van gegevens naar een tabel met een identiteitskolom. 

Wanneer -E wordt opgegeven, worden ondergebracht in Hallo invoerbestand voor Hallo kolom met de identiteit Hallo-waarden worden bewaard. Als E - *niet* opgegeven, wordt het Hallo-waarden in deze kolom worden genegeerd. Als de identiteitskolom Hallo niet opgenomen is, is Hallo gegevens normaal geladen. Hallo-waarden worden gegenereerd op basis van toohello increment- en seed-beleid van Hallo-eigenschap.

Zie voor meer informatie over het laden van gegevens met behulp van BCP Hallo artikelen te volgen:

- [Laden met BCP][]
- [BCP in MSDN][]

## <a name="catalog-views"></a>Catalogusweergaven
SQL Data Warehouse ondersteunt Hallo `sys.identity_columns` catalogusweergave. Deze weergave kan worden gebruikt tooidentify een kolom met Hallo IDENTITY-eigenschap.

dit voorbeeld ziet u toohelp Hallo-databaseschema beter te begrijpen, hoe toointegrate `sys.identity_columns` met andere weergaven van de catalogus system:

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

## <a name="limitations"></a>Beperkingen
Hallo IDENTITY-eigenschap kan niet worden gebruikt in Hallo volgen scenario's:
- Waar Hallo kolomgegevenstype is niet INT of BIGINT
- Hallo-kolom is waar ook Hallo distributiesleutel
- Waar Hallo-tabel is een externe tabel 

Hallo verwante functies te volgen, worden niet ondersteund in SQL Data Warehouse:

- [IDENTITY()][]
- [@@IDENTITY][]
- [SCOPE_IDENTITY][]
- [IDENT_CURRENT][]
- [IDENT_INCR][]
- [IDENT_SEED][]
- [DBCC CHECK_IDENT()][]

## <a name="tasks"></a>Taken

Deze sectie vindt u enkele voorbeelden van code kunt u algemene taken tooperform wanneer u met de id-kolommen werkt.

> [!NOTE] 
> Kolom C1 is Hallo identiteit in alle Hallo taken te volgen.
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a>Hallo hoogste toegewezen waarde vinden voor een tabel
Gebruik Hallo `MAX()` toodetermine Hallo hoogste toegewezen waarde voor een gedistribueerde tabel werken:

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a>Hallo seed- en increment vinden voor Hallo IDENTITY-eigenschap
U kunt Hallo catalogus weergaven toodiscover Hallo increment- en seed configuratie identiteitswaarden gebruiken voor een tabel met behulp van de volgende query Hallo: 

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

## <a name="next-steps"></a>Volgende stappen

* toolearn meer informatie over het ontwikkelen van tabellen, Zie [tabel overzicht][Overview], [tabel gegevenstypen][Data Types], [een tabeldistribueren] [ Distribute], [Indexeren van een tabel][Index], [partitie van een tabel][Partition], en [ Tijdelijke tabellen][Temporary]. 
* Zie voor meer informatie over best practices [aanbevolen procedures voor SQL Data Warehouse][SQL Data Warehouse Best Practices].  

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
