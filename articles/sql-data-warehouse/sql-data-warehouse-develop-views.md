---
title: aaaUsing T-SQL-weergaven in Azure SQL Data Warehouse | Microsoft Docs
description: Tips voor het gebruik van Transact-SQL-weergaven in Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: b5208f32-8f4a-4056-8788-2adbb253d9fd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 3990b133946621691bdfa4b09523d21867470c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-sql-data-warehouse"></a>Weergaven in SQL datawarehouse
Weergaven zijn vooral nuttig in SQL Data Warehouse. Ze kunnen worden gebruikt in een aantal verschillende manieren tooimprove Hallo kwaliteit van uw oplossing.  In dit artikel ziet u enkele voorbeelden van hoe tooenrich uw oplossing met weergaven, evenals Hallo-beperkingen die toobe moeten beschouwd.

> [!NOTE]
> De syntaxis voor `CREATE VIEW` niet in dit artikel wordt besproken. Raadpleeg toohello [CREATE VIEW] [ CREATE VIEW] op MSDN-artikel voor deze referentie-informatie.
> 
> 

## <a name="architectural-abstraction"></a>Architectuur abstractie
Een zeer gangbaar patroon van toepassing is toore-tabellen maken tabel AS selecteren (CTAS) gevolgd door een object patroon wijzigen tijdens het laden van gegevens maken.

Hallo in het volgende voorbeeld wordt de nieuwe records tooa datum datumdimensie toegevoegd. Houd er rekening mee hoe een nieuwe tabble, DimDate_New, het eerst wordt gemaakt en wordt de naam van tooreplace Hallo oorspronkelijke versie van de tabel Hallo gewijzigd.

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate tooDimDate_Old;
RENAME OBJECT DimDate_New tooDimDate;

```

Deze methode kan echter resulteren in tabellen die wordt weergegeven en verdwijnen uit de weergave van een gebruiker, evenals een "tabel bestaat niet" foutberichten. Weergaven kunnen gebruikers met een laag consistente presentatie gebruikte tooprovide worden terwijl de onderliggende objecten Hallo hernoemd. Door middel van gebruikers toegang betekent toohello gegevens via een weergaven gebruikers hoeven niet toohave zichtbaarheid van Hallo onderliggende tabellen. Dit biedt een consistente gebruikerservaring terwijl u ervoor zorgt dat Hallo gegevens datawarehouse ontwerpers kunnen Hallo-gegevensmodel ontwikkelen en prestaties te optimaliseren via CTAS tijdens het laadproces Hallo-gegevens.    

## <a name="performance-optimization"></a>Optimalisatie van prestaties
Weergaven kunnen ook worden gebruikte tooenforce voor optimale prestaties joins tussen de tabellen. Een weergave kan bijvoorbeeld gebruikmaken van een redundante distributiesleutel als onderdeel van Hallo criteria toominimize gegevensverplaatsing lid te worden.  Een ander voordeel van een weergave kan worden tooforce een specifieke query of gekoppelde hint. Weergaven gebruiken op deze manier wordt gegarandeerd dat joins altijd worden uitgevoerd op optimale wijze Hallo behoefte gebruikers tooremember Hallo juist construct voor hun joins te vermijden.

## <a name="limitations"></a>Beperkingen
Weergaven in SQL Data Warehouse zijn alleen metagegevens.  Als gevolg daarvan zijn Hallo volgende opties niet beschikbaar:

* Er is geen schema binding-optie
* Basistabellen kunnen niet via Hallo weergave worden bijgewerkt
* Weergaven kunnen niet worden gemaakt via tijdelijke tabellen
* Er is geen ondersteuning voor Hallo UITVOUWEN / NOEXPAND-hints
* Er zijn geen geïndexeerde weergaven in SQL Data Warehouse

## <a name="next-steps"></a>Volgende stappen
Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.
Voor `CREATE VIEW` syntaxis Raadpleeg te[CREATE VIEW][CREATE VIEW].

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
