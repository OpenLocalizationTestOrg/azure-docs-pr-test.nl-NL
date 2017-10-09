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
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a>Ontwerpbeslissingen en codering technieken voor SQL Data Warehouse
Bekijk via deze ontwikkeling artikelen toobetter begrijpen belangrijke ontwerpbeslissingen, aanbevelingen en codering technieken voor SQL Data Warehouse.

## <a name="key-design-decisions"></a>Belangrijke ontwerpbeslissingen
Hallo markeren volgende artikelen aantal Hallo belangrijke concepten en moet u toounderstand voor ontwikkeling van uw gedistribueerde datawarehouse met behulp van SQL Data Warehouse Hallo ontwerpbeslissingen:

* [verbindingen][connections]
* [gelijktijdigheid van taken][concurrency]
* [transacties][transactions]
* [gebruiker gedefinieerde schema 's][user-defined schemas]
* [tabeldistributie][table distribution]
* [tabelindexen][table indexes]
* [Tabelpartities][table partitions]
* [CTAS][CTAS]
* [statistieken][statistics]

## <a name="development-recommendations-and-coding-techniques"></a>Aanbevelingen voor ontwikkeling en codering technieken
Deze artikelen markeren specifieke codering technieken, tips en aanbevelingen voor het ontwikkelen van uw SQL Data Warehouse:

* [opgeslagen procedures][stored procedures]
* [labels][labels]
* [Weergaven][views]
* [tijdelijke tabellen][temporary tables]
* [dynamische SQL][dynamic SQL]
* [lussen][looping]
* [Group by-opties][group by options]
* [toewijzing van variabele][variable assignment]

## <a name="next-steps"></a>Volgende stappen
Wanneer u via Hallo ontwikkeling artikelen zijn kijk via Hallo [Transact-SQL-naslaginformatie] [ Transact-SQL reference] voor meer informatie over de syntaxis van de Hallo ondersteund voor SQL Data Warehouse.

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
