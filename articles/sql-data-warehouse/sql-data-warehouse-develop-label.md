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
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a>Labels tooinstrument query's in SQL Data Warehouse gebruiken
SQL Data Warehouse ondersteunt een concept query labels genoemd. Bekijk voordat u doorgaat naar eventuele diepte gaan we een voorbeeld van een:

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

Deze regel labels Hallo tekenreeks 'Mijn Query Label' toohello query. Dit is vooral handig zijn omdat de query kunnen via DMV's Hallo Hallo label. Dit biedt ons een mechanisme tootrack omlaag probleem query's en toohelp, zien ook uitgevoerd via een ETL uitvoeren.

Een goede naamgevingsconventie echt helpt hier. Bijvoorbeeld als ' PROJECT: PROCEDURE: instructie: Opmerking ' toouniquely Hallo query in onder alle Hallo-code in broncodebeheer identificeren kan helpen.

toosearch labels kunt u Hallo na query die gebruikmaakt van dynamische beheerweergaven Hallo:

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> Het is essentieel dat u vierkante haken of dubbele aanhalingstekens rond Hallo word label langs tijdens het opvragen van. Label is een gereserveerd woord en wordt een fout veroorzaakt als deze niet zijn gescheiden.
> 
> 

## <a name="next-steps"></a>Volgende stappen
Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
