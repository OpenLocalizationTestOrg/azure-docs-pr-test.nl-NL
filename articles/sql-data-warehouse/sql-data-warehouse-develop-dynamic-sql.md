---
title: aaaDynamic SQL in SQL Data Warehouse | Microsoft Docs
description: Tips voor het gebruik van dynamische SQL in Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: a948c2c3-3cd1-4373-90a9-79e59414b778
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 4d66eecb37621510f657d1ec9a2a935daaa16052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-sql-in-sql-data-warehouse"></a>Dynamische SQL in SQL datawarehouse
Bij het ontwikkelen van toepassingscode voor SQL Data Warehouse u mogelijk nodig toouse dynamische sql toohelp bieden flexibele, algemene en modulair oplossingen. SQL Data Warehouse biedt geen ondersteuning voor blob-gegevenstypen op dit moment. Dit beperkt mogelijk Hallo grootte van uw tekenreeksen als blob typen zowel varchar(max) en nvarchar(max) typen bevatten. Als u deze typen in uw toepassingscode gebruikt hebt bij het bouwen van zeer grote tekenreeksen, moet u toobreak Hallo code in segmenten en gebruik Hallo EXEC-instructie in plaats daarvan.

Een eenvoudig voorbeeld:

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

Als het Hallo-tekenreeks is kort kunt u [sp_executesql] [ sp_executesql] die normaal werken.

> [!NOTE]
> Instructies die worden uitgevoerd als dynamische SQL nog steeds onderwerp tooall TSQL-validatieregels.
> 
> 

## <a name="next-steps"></a>Volgende stappen
Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
