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
# <a name="loops-in-sql-data-warehouse"></a>Lussen in SQL datawarehouse
SQL Data Warehouse ondersteunt Hallo [terwijl][terwijl] lus voor herhaaldelijk blokken instructie uitvoeren. Deze blijven voor zolang Hallo opgegeven voorwaarden wordt voldaan, of tot Hallo code specifiek Hallo lus met Hallo beëindigt `BREAK` sleutelwoord. Lussen zijn bijzonder nuttig voor het vervangen van cursors die zijn gedefinieerd in SQL-code. Gelukkig zijn bijna alle cursors die zijn geschreven in SQL-code Hallo snelle doorsturen, lezen alleen groot. Daarom [terwijl] lussen vormen een geweldige alternatief als u merkt dat tooreplace een.

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a>Gebruik van lussen en vervangt cursors in SQL Data Warehouse
Echter eerst in head wilt voordat u zichzelf moet stellen Hallo volgende vraag: 'kan deze cursor worden opnieuw geschreven toouse set op basis van operations?'. In veel gevallen Hallo antwoord Ja is en is vaak de beste aanpak Hallo. Een set op basis van de bewerking vaak voert aanzienlijk sneller dan een benadering iteratieve, per rij.

Vooruit cursors voor alleen-lezen kunnen eenvoudig worden vervangen door een samenvoegartikel constructie. Hieronder vindt u een eenvoudig voorbeeld. Dit codevoorbeeld Hallo statistieken voor elke tabel in de database Hallo-updates. Door iteratie van tabellen in de lus Hallo Hallo we kunnen tooexecute elke opdracht in de reeks zijn.

Maak eerst een tijdelijke tabel die een afzonderlijke instructies voor unieke rij aantal gebruikte tooidentify Hallo bevat:

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

Ten tweede initialiseren Hallo variabelen vereist tooperform Hallo lus:

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

Nu op een uitvoeren-instructies in een lus tegelijk:

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

Ten slotte Hallo tijdelijke tabel gemaakt in de eerste stap Hallo verwijderen

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Volgende stappen
Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[terwijl]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
