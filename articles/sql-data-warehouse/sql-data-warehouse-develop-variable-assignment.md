---
title: aaaAssign variabelen in SQL Data Warehouse | Microsoft Docs
description: Tips voor het toewijzen van Transact-SQL-variabelen in Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9de48739bb0af80ff2a117704b31512c680f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a>Variabelen in SQL Data Warehouse toewijzen
Variabelen in SQL Data Warehouse worden ingesteld met de Hallo `DECLARE` instructie of Hallo `SET` instructie.

Hallo volgende zijn geldige manieren tooset waarde van een variabele:

## <a name="setting-variables-with-declare"></a>Variabelen met DECLARE instellen
Tijdens de initialisatie van variabelen met DECLARE, is een van de Hallo meest flexibele manieren tooset de waarde van een variabele in SQL Data Warehouse.

```sql
DECLARE @v  int = 0
;
```

U kunt ook DECLARE tooset meer dan één variabele tegelijk gebruiken. U kunt geen gebruiken `SELECT` of `UPDATE` toodo dit:

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

U kunt geen initialiseren of een variabele gebruiken in Hallo dezelfde DECLARE-instructie. tooillustrate hello punt Hallo onderstaande voorbeeld is **niet** toegestaan als @p1 is geïnitialiseerd en gebruikt in Hallo dezelfde DECLARE-instructie. Dit leidt tot een fout opgetreden.

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a>Waarden van instellingen is ingesteld
Is een veelgebruikte manier voor het instellen van een enkele variabele ingesteld.

Hallo in de volgende voorbeelden zijn geldige manieren voor het instellen van een variabele is ingesteld:

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

U kunt alleen een variabele instellen op een tijdstip is ingesteld. Zoals hierboven beschreven zijn samengestelde operators toegestane.

## <a name="limitations"></a>Beperkingen
U kunt selecteren of UPDATE niet gebruiken voor variabele toewijzing.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
