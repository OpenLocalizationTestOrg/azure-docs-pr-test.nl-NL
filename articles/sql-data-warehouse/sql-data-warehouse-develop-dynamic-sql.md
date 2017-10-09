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
# <a name="dynamic-sql-in-sql-data-warehouse"></a><span data-ttu-id="94a64-103">Dynamische SQL in SQL datawarehouse</span><span class="sxs-lookup"><span data-stu-id="94a64-103">Dynamic SQL in SQL Data Warehouse</span></span>
<span data-ttu-id="94a64-104">Bij het ontwikkelen van toepassingscode voor SQL Data Warehouse u mogelijk nodig toouse dynamische sql toohelp bieden flexibele, algemene en modulair oplossingen.</span><span class="sxs-lookup"><span data-stu-id="94a64-104">When developing application code for SQL Data Warehouse you may need toouse dynamic sql toohelp deliver flexible, generic and modular solutions.</span></span> <span data-ttu-id="94a64-105">SQL Data Warehouse biedt geen ondersteuning voor blob-gegevenstypen op dit moment.</span><span class="sxs-lookup"><span data-stu-id="94a64-105">SQL Data Warehouse does not support blob data types at this time.</span></span> <span data-ttu-id="94a64-106">Dit beperkt mogelijk Hallo grootte van uw tekenreeksen als blob typen zowel varchar(max) en nvarchar(max) typen bevatten.</span><span class="sxs-lookup"><span data-stu-id="94a64-106">This may limit hello size of your strings as blob types include both varchar(max) and nvarchar(max) types.</span></span> <span data-ttu-id="94a64-107">Als u deze typen in uw toepassingscode gebruikt hebt bij het bouwen van zeer grote tekenreeksen, moet u toobreak Hallo code in segmenten en gebruik Hallo EXEC-instructie in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="94a64-107">If you have used these types in your application code when building very large strings, you will need toobreak hello code into chunks and use hello EXEC statement instead.</span></span>

<span data-ttu-id="94a64-108">Een eenvoudig voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="94a64-108">A simple example:</span></span>

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

<span data-ttu-id="94a64-109">Als het Hallo-tekenreeks is kort kunt u [sp_executesql] [ sp_executesql] die normaal werken.</span><span class="sxs-lookup"><span data-stu-id="94a64-109">If hello string is short you can use [sp_executesql][sp_executesql] as normal.</span></span>

> [!NOTE]
> <span data-ttu-id="94a64-110">Instructies die worden uitgevoerd als dynamische SQL nog steeds onderwerp tooall TSQL-validatieregels.</span><span class="sxs-lookup"><span data-stu-id="94a64-110">Statements executed as dynamic SQL will still be subject tooall TSQL validation rules.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="94a64-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="94a64-111">Next steps</span></span>
<span data-ttu-id="94a64-112">Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].</span><span class="sxs-lookup"><span data-stu-id="94a64-112">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
