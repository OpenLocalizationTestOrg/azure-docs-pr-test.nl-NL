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
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="b4988-103">Weergaven in SQL datawarehouse</span><span class="sxs-lookup"><span data-stu-id="b4988-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="b4988-104">Weergaven zijn vooral nuttig in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b4988-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="b4988-105">Ze kunnen worden gebruikt in een aantal verschillende manieren tooimprove Hallo kwaliteit van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="b4988-105">They can be used in a number of different ways tooimprove hello quality of your solution.</span></span>  <span data-ttu-id="b4988-106">In dit artikel ziet u enkele voorbeelden van hoe tooenrich uw oplossing met weergaven, evenals Hallo-beperkingen die toobe moeten beschouwd.</span><span class="sxs-lookup"><span data-stu-id="b4988-106">This article highlights a few examples of how tooenrich your solution with views, as well as hello limitations that need toobe considered.</span></span>

> [!NOTE]
> <span data-ttu-id="b4988-107">De syntaxis voor `CREATE VIEW` niet in dit artikel wordt besproken.</span><span class="sxs-lookup"><span data-stu-id="b4988-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="b4988-108">Raadpleeg toohello [CREATE VIEW] [ CREATE VIEW] op MSDN-artikel voor deze referentie-informatie.</span><span class="sxs-lookup"><span data-stu-id="b4988-108">Please refer toohello [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="b4988-109">Architectuur abstractie</span><span class="sxs-lookup"><span data-stu-id="b4988-109">Architectural abstraction</span></span>
<span data-ttu-id="b4988-110">Een zeer gangbaar patroon van toepassing is toore-tabellen maken tabel AS selecteren (CTAS) gevolgd door een object patroon wijzigen tijdens het laden van gegevens maken.</span><span class="sxs-lookup"><span data-stu-id="b4988-110">A very common application pattern is toore-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="b4988-111">Hallo in het volgende voorbeeld wordt de nieuwe records tooa datum datumdimensie toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b4988-111">hello example below adds new date records tooa date dimension.</span></span> <span data-ttu-id="b4988-112">Houd er rekening mee hoe een nieuwe tabble, DimDate_New, het eerst wordt gemaakt en wordt de naam van tooreplace Hallo oorspronkelijke versie van de tabel Hallo gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="b4988-112">Note how a new tabble, DimDate_New, is first created and then renamed tooreplace hello original version of hello table.</span></span>

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

<span data-ttu-id="b4988-113">Deze methode kan echter resulteren in tabellen die wordt weergegeven en verdwijnen uit de weergave van een gebruiker, evenals een "tabel bestaat niet" foutberichten.</span><span class="sxs-lookup"><span data-stu-id="b4988-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="b4988-114">Weergaven kunnen gebruikers met een laag consistente presentatie gebruikte tooprovide worden terwijl de onderliggende objecten Hallo hernoemd.</span><span class="sxs-lookup"><span data-stu-id="b4988-114">Views can be used tooprovide users with a consistent presentation layer whilst hello underlying objects are renamed.</span></span> <span data-ttu-id="b4988-115">Door middel van gebruikers toegang betekent toohello gegevens via een weergaven gebruikers hoeven niet toohave zichtbaarheid van Hallo onderliggende tabellen.</span><span class="sxs-lookup"><span data-stu-id="b4988-115">By providing users access toohello data through a views, means users don't need toohave visibility of hello underlying tables.</span></span> <span data-ttu-id="b4988-116">Dit biedt een consistente gebruikerservaring terwijl u ervoor zorgt dat Hallo gegevens datawarehouse ontwerpers kunnen Hallo-gegevensmodel ontwikkelen en prestaties te optimaliseren via CTAS tijdens het laadproces Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="b4988-116">This provides a consistent user experience while ensuring that hello data warehouse designers can evolve hello data model and maximize performance by using CTAS during hello data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="b4988-117">Optimalisatie van prestaties</span><span class="sxs-lookup"><span data-stu-id="b4988-117">Performance optimization</span></span>
<span data-ttu-id="b4988-118">Weergaven kunnen ook worden gebruikte tooenforce voor optimale prestaties joins tussen de tabellen.</span><span class="sxs-lookup"><span data-stu-id="b4988-118">Views can also be utilized tooenforce performance optimized joins between tables.</span></span> <span data-ttu-id="b4988-119">Een weergave kan bijvoorbeeld gebruikmaken van een redundante distributiesleutel als onderdeel van Hallo criteria toominimize gegevensverplaatsing lid te worden.</span><span class="sxs-lookup"><span data-stu-id="b4988-119">For example, a view can incorporate a redundant distribution key as part of hello joining criteria toominimize data movement.</span></span>  <span data-ttu-id="b4988-120">Een ander voordeel van een weergave kan worden tooforce een specifieke query of gekoppelde hint.</span><span class="sxs-lookup"><span data-stu-id="b4988-120">Another benefit of a view could be tooforce a specific query or joining hint.</span></span> <span data-ttu-id="b4988-121">Weergaven gebruiken op deze manier wordt gegarandeerd dat joins altijd worden uitgevoerd op optimale wijze Hallo behoefte gebruikers tooremember Hallo juist construct voor hun joins te vermijden.</span><span class="sxs-lookup"><span data-stu-id="b4988-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding hello need for users tooremember hello correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="b4988-122">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="b4988-122">Limitations</span></span>
<span data-ttu-id="b4988-123">Weergaven in SQL Data Warehouse zijn alleen metagegevens.</span><span class="sxs-lookup"><span data-stu-id="b4988-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="b4988-124">Als gevolg daarvan zijn Hallo volgende opties niet beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="b4988-124">Consequently hello following options are not available:</span></span>

* <span data-ttu-id="b4988-125">Er is geen schema binding-optie</span><span class="sxs-lookup"><span data-stu-id="b4988-125">There is no schema binding option</span></span>
* <span data-ttu-id="b4988-126">Basistabellen kunnen niet via Hallo weergave worden bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="b4988-126">Base tables cannot be updated through hello view</span></span>
* <span data-ttu-id="b4988-127">Weergaven kunnen niet worden gemaakt via tijdelijke tabellen</span><span class="sxs-lookup"><span data-stu-id="b4988-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="b4988-128">Er is geen ondersteuning voor Hallo UITVOUWEN / NOEXPAND-hints</span><span class="sxs-lookup"><span data-stu-id="b4988-128">There is no support for hello EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="b4988-129">Er zijn geen geïndexeerde weergaven in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b4988-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4988-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b4988-130">Next steps</span></span>
<span data-ttu-id="b4988-131">Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="b4988-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="b4988-132">Voor `CREATE VIEW` syntaxis Raadpleeg te[CREATE VIEW][CREATE VIEW].</span><span class="sxs-lookup"><span data-stu-id="b4988-132">For `CREATE VIEW` syntax please refer too[CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
