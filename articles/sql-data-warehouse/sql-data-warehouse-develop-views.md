---
title: T-SQL-weergaven gebruiken in Azure SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: d2a03be810bd7f792876607ec735eb578b65a3b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="1c9bd-103">Weergaven in SQL datawarehouse</span><span class="sxs-lookup"><span data-stu-id="1c9bd-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="1c9bd-104">Weergaven zijn vooral nuttig in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="1c9bd-105">Ze kunnen worden gebruikt in een aantal verschillende manieren om de kwaliteit van uw oplossing te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-105">They can be used in a number of different ways to improve the quality of your solution.</span></span>  <span data-ttu-id="1c9bd-106">In dit artikel worden enkele voorbeelden van hoe uw oplossing met weergaven, evenals de beperkingen die moeten worden overwogen verrijken gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-106">This article highlights a few examples of how to enrich your solution with views, as well as the limitations that need to be considered.</span></span>

> [!NOTE]
> <span data-ttu-id="1c9bd-107">De syntaxis voor `CREATE VIEW` niet in dit artikel wordt besproken.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="1c9bd-108">Raadpleeg de [CREATE VIEW] [ CREATE VIEW] op MSDN-artikel voor deze referentie-informatie.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-108">Please refer to the [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="1c9bd-109">Architectuur abstractie</span><span class="sxs-lookup"><span data-stu-id="1c9bd-109">Architectural abstraction</span></span>
<span data-ttu-id="1c9bd-110">Een zeer gangbaar patroon van toepassing is opnieuw om tabellen te maken met behulp van maken tabel AS selecteren (CTAS) gevolgd door een object patroon wijzigen tijdens het laden van gegevens.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-110">A very common application pattern is to re-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="1c9bd-111">Het volgende voorbeeld voegt nieuwe datum records naar een datumdimensie.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-111">The example below adds new date records to a date dimension.</span></span> <span data-ttu-id="1c9bd-112">Houd er rekening mee hoe een nieuwe tabble, DimDate_New, is het eerst hebt gemaakt en wordt de naam gewijzigd ter vervanging van de oorspronkelijke versie van de tabel.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-112">Note how a new tabble, DimDate_New, is first created and then renamed to replace the original version of the table.</span></span>

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

RENAME OBJECT DimDate TO DimDate_Old;
RENAME OBJECT DimDate_New TO DimDate;

```

<span data-ttu-id="1c9bd-113">Deze methode kan echter resulteren in tabellen die wordt weergegeven en verdwijnen uit de weergave van een gebruiker, evenals een "tabel bestaat niet" foutberichten.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="1c9bd-114">Weergaven kunnen worden gebruikt om gebruikers te geven met een laag consistente presentatie terwijl de onderliggende objecten worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-114">Views can be used to provide users with a consistent presentation layer whilst the underlying objects are renamed.</span></span> <span data-ttu-id="1c9bd-115">Dankzij de gebruikers toegang tot de gegevens via een weergaven, betekent dat gebruikers hoeven niet te hebben zichtbaarheid van de onderliggende tabellen.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-115">By providing users access to the data through a views, means users don't need to have visibility of the underlying tables.</span></span> <span data-ttu-id="1c9bd-116">Dit biedt een consistente gebruikerservaring tijdens ervoor te zorgen dat de datawarehouse-designers kunt ontwikkelen van het gegevensmodel en prestaties te optimaliseren via CTAS tijdens het laden van gegevens.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-116">This provides a consistent user experience while ensuring that the data warehouse designers can evolve the data model and maximize performance by using CTAS during the data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="1c9bd-117">Optimalisatie van prestaties</span><span class="sxs-lookup"><span data-stu-id="1c9bd-117">Performance optimization</span></span>
<span data-ttu-id="1c9bd-118">Weergaven kunnen ook worden gebruikt om af te dwingen voor optimale prestaties joins tussen de tabellen.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-118">Views can also be utilized to enforce performance optimized joins between tables.</span></span> <span data-ttu-id="1c9bd-119">Een weergave kunt bijvoorbeeld een redundante distributiesleutel opnemen als onderdeel van de gekoppelde criteria voor het beperken van gegevensverplaatsing.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-119">For example, a view can incorporate a redundant distribution key as part of the joining criteria to minimize data movement.</span></span>  <span data-ttu-id="1c9bd-120">Een ander voordeel van een weergave kan worden om af te dwingen een specifieke query of gekoppelde hint.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-120">Another benefit of a view could be to force a specific query or joining hint.</span></span> <span data-ttu-id="1c9bd-121">Weergaven gebruiken op deze manier wordt gegarandeerd dat joins altijd worden uitgevoerd op optimale wijze de noodzaak van gebruikers te onthouden van de juiste construct voor hun joins te vermijden.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding the need for users to remember the correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="1c9bd-122">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="1c9bd-122">Limitations</span></span>
<span data-ttu-id="1c9bd-123">Weergaven in SQL Data Warehouse zijn alleen metagegevens.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="1c9bd-124">Als gevolg daarvan is de volgende opties zijn niet beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="1c9bd-124">Consequently the following options are not available:</span></span>

* <span data-ttu-id="1c9bd-125">Er is geen schema binding-optie</span><span class="sxs-lookup"><span data-stu-id="1c9bd-125">There is no schema binding option</span></span>
* <span data-ttu-id="1c9bd-126">Basistabellen kunnen niet via de weergave worden bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="1c9bd-126">Base tables cannot be updated through the view</span></span>
* <span data-ttu-id="1c9bd-127">Weergaven kunnen niet worden gemaakt via tijdelijke tabellen</span><span class="sxs-lookup"><span data-stu-id="1c9bd-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="1c9bd-128">Er is geen ondersteuning voor UITVOUWEN / NOEXPAND-hints</span><span class="sxs-lookup"><span data-stu-id="1c9bd-128">There is no support for the EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="1c9bd-129">Er zijn geen geïndexeerde weergaven in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1c9bd-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c9bd-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1c9bd-130">Next steps</span></span>
<span data-ttu-id="1c9bd-131">Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="1c9bd-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="1c9bd-132">Voor `CREATE VIEW` syntaxis Raadpleeg [CREATE VIEW][CREATE VIEW].</span><span class="sxs-lookup"><span data-stu-id="1c9bd-132">For `CREATE VIEW` syntax please refer to [CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
