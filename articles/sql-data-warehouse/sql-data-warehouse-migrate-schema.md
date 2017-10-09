---
title: aaaMigrate uw schema tooSQL Data Warehouse | Microsoft Docs
description: Tips voor het migreren van uw schema tooAzure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a><span data-ttu-id="042c7-103">Uw schema's tooSQL Data Warehouse migreren</span><span class="sxs-lookup"><span data-stu-id="042c7-103">Migrate your schemas tooSQL Data Warehouse</span></span>
<span data-ttu-id="042c7-104">Richtlijnen voor het migreren van uw SQL-schema's tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="042c7-104">Guidance for migrating your SQL schemas tooSQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="042c7-105">De schema-migratie plannen</span><span class="sxs-lookup"><span data-stu-id="042c7-105">Plan your schema migration</span></span>

<span data-ttu-id="042c7-106">Als u van plan een migratie bent, Zie Hallo [tabel overzicht] [ table overview] toobecome bekend zijn met overwegingen bij het ontwerpen van tabel zoals statistieken, distributie, partitioneren en indexeren.</span><span class="sxs-lookup"><span data-stu-id="042c7-106">As you plan a migration, see hello [table overview][table overview] toobecome familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="042c7-107">Ook worden enkele [niet-ondersteunde tabelfuncties] [ unsupported table features] en de tijdelijke oplossingen.</span><span class="sxs-lookup"><span data-stu-id="042c7-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a><span data-ttu-id="042c7-108">Databases van de gebruiker gedefinieerde schema's tooconsolidate gebruiken</span><span class="sxs-lookup"><span data-stu-id="042c7-108">Use user-defined schemas tooconsolidate databases</span></span>

<span data-ttu-id="042c7-109">De werkbelasting van uw bestaande heeft waarschijnlijk meer dan één database.</span><span class="sxs-lookup"><span data-stu-id="042c7-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="042c7-110">Een datawarehouse van SQL Server kan bijvoorbeeld een faseringsdatabase, een datawarehouse-database en sommige gegevens datamart-databases.</span><span class="sxs-lookup"><span data-stu-id="042c7-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="042c7-111">In deze topologie wordt elke database uitgevoerd als een afzonderlijke werkbelasting met afzonderlijke beveiligingsbeleid.</span><span class="sxs-lookup"><span data-stu-id="042c7-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="042c7-112">Daarentegen, voert SQL Data Warehouse Hallo gehele datawarehouse-workload binnen één database.</span><span class="sxs-lookup"><span data-stu-id="042c7-112">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="042c7-113">Joins zijn niet toegestaan cross-database.</span><span class="sxs-lookup"><span data-stu-id="042c7-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="042c7-114">SQL Data Warehouse verwacht daarom alle tabellen die worden gebruikt door Hallo datawarehouse toobe opgeslagen in één Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="042c7-114">Therefore, SQL Data Warehouse expects all tables used by hello data warehouse toobe stored within hello one database.</span></span>

<span data-ttu-id="042c7-115">Wordt u aangeraden tooconsolidate van de gebruiker gedefinieerde schema's de werkbelasting van uw bestaande in een database.</span><span class="sxs-lookup"><span data-stu-id="042c7-115">We recommend using user-defined schemas tooconsolidate your existing workload into one database.</span></span> <span data-ttu-id="042c7-116">Zie voor voorbeelden [gebruiker gedefinieerde schema's](sql-data-warehouse-develop-user-defined-schemas.md)</span><span class="sxs-lookup"><span data-stu-id="042c7-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="042c7-117">Compatibele gegevenstypen gebruiken</span><span class="sxs-lookup"><span data-stu-id="042c7-117">Use compatible data types</span></span>
<span data-ttu-id="042c7-118">Wijzigen van uw gegevens typen toobe die compatibel is met SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="042c7-118">Modify your data types toobe compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="042c7-119">Zie voor een lijst van ondersteunde en niet-ondersteunde gegevenstypen [gegevenstypen][data types].</span><span class="sxs-lookup"><span data-stu-id="042c7-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="042c7-120">Dat onderwerp biedt tijdelijke oplossingen voor Hallo niet-ondersteunde typen.</span><span class="sxs-lookup"><span data-stu-id="042c7-120">That topic gives workarounds for hello unsupported types.</span></span> <span data-ttu-id="042c7-121">Het bevat ook een query tooidentify bestaande typen die niet worden ondersteund in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="042c7-121">It also provides a query tooidentify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="042c7-122">Rijgrootte minimaliseren</span><span class="sxs-lookup"><span data-stu-id="042c7-122">Minimize row size</span></span>
<span data-ttu-id="042c7-123">Minimaliseer Hallo rijlengte van de tabellen voor de beste prestaties.</span><span class="sxs-lookup"><span data-stu-id="042c7-123">For best performance, minimize hello row length of your tables.</span></span> <span data-ttu-id="042c7-124">Aangezien korter rij lengten toobetter prestaties leiden, Hallo kleinste gegevenstypen gebruiken die werken voor uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="042c7-124">Since shorter row lengths lead toobetter performance, use hello smallest data types that work for your data.</span></span> 

<span data-ttu-id="042c7-125">PolyBase heeft voor de breedte van de rij tabel, een limiet van 1 MB.</span><span class="sxs-lookup"><span data-stu-id="042c7-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="042c7-126">Als u van plan tooload gegevens in SQL Data Warehouse met PolyBase bent, werk de tabellen toohave maximale rij breedten van minder dan 1 MB.</span><span class="sxs-lookup"><span data-stu-id="042c7-126">If you plan tooload data into SQL Data Warehouse with PolyBase, update your tables toohave maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a><span data-ttu-id="042c7-127">Hallo distributie optie opgeven</span><span class="sxs-lookup"><span data-stu-id="042c7-127">Specify hello distribution option</span></span>
<span data-ttu-id="042c7-128">SQL Data Warehouse is een gedistribueerde database-systeem.</span><span class="sxs-lookup"><span data-stu-id="042c7-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="042c7-129">Elke tabel is gedistribueerd of gerepliceerd via Hallo rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="042c7-129">Each table is distributed or replicated across hello Compute nodes.</span></span> <span data-ttu-id="042c7-130">Er is een tabeloptie waarmee u kunt opgeven hoe toodistribute Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="042c7-130">There's a table option that lets you specify how toodistribute hello data.</span></span> <span data-ttu-id="042c7-131">Hallo zijn opties round-robin wordt gerepliceerd, of hash gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="042c7-131">hello choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="042c7-132">Elk heeft voor- en nadelen.</span><span class="sxs-lookup"><span data-stu-id="042c7-132">Each has pros and cons.</span></span> <span data-ttu-id="042c7-133">Als u geen optie voor distributie Hallo opgeeft, SQL Data Warehouse round robin Hallo standaard gebruikt.</span><span class="sxs-lookup"><span data-stu-id="042c7-133">If you don't specify hello distribution option, SQL Data Warehouse will use round-robin as hello default.</span></span>

- <span data-ttu-id="042c7-134">Round robin is Hallo standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="042c7-134">Round-robin is hello default.</span></span> <span data-ttu-id="042c7-135">Dit is de eenvoudigste toouse hello en Hallo gegevens zo snel mogelijk worden geladen, maar joins gegevensverplaatsing waardoor wordt vertraagd queryprestaties is vereist.</span><span class="sxs-lookup"><span data-stu-id="042c7-135">It is hello simplest toouse, and loads hello data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="042c7-136">Gerepliceerde winkels een kopie van de tabel Hallo op elk rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="042c7-136">Replicated stores a copy of hello table on each Compute node.</span></span> <span data-ttu-id="042c7-137">Gerepliceerde tabellen zijn zodat omdat ze geen verplaatsing van gegevens voor samenvoegingen en aggregaties behoeven.</span><span class="sxs-lookup"><span data-stu-id="042c7-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="042c7-138">Extra opslag vereist, hetgeen daarom het meest geschikt voor kleinere tabellen.</span><span class="sxs-lookup"><span data-stu-id="042c7-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="042c7-139">Hallo rijen verdeelt hash gedistribueerd over alle knooppunten van Hallo via een hash-functie.</span><span class="sxs-lookup"><span data-stu-id="042c7-139">Hash distributed distributes hello rows across all hello nodes via a hash function.</span></span> <span data-ttu-id="042c7-140">Gedistribueerd hash-tabellen zijn Hallo hart van SQL Data Warehouse omdat ze ontworpen tooprovide hoge queryprestaties op grote tabellen zijn.</span><span class="sxs-lookup"><span data-stu-id="042c7-140">Hash distributed tables are hello heart of SQL Data Warehouse since they are designed tooprovide high query performance on large tables.</span></span> <span data-ttu-id="042c7-141">Deze optie vereist een planning tooselect Hallo best van de kolommen op welke toodistribute Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="042c7-141">This option requires some planning tooselect hello best column on which toodistribute hello data.</span></span> <span data-ttu-id="042c7-142">Echter, als u niet het aanbevolen kolom Hallo Hallo eerst kiest, kunt u eenvoudig opnieuw distribueren Hallo gegevens op een andere kolom.</span><span class="sxs-lookup"><span data-stu-id="042c7-142">However, if you don't choose hello best column hello first time, you can easily re-distribute hello data on a different column.</span></span> 

<span data-ttu-id="042c7-143">Zie toochoose Hallo aanbevolen optie voor distributie voor elke tabel [tabellen gedistribueerd](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="042c7-143">toochoose hello best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="042c7-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="042c7-144">Next steps</span></span>
<span data-ttu-id="042c7-145">Nadat u uw database schema tooSQL Data Warehouse hebt gemigreerd, gaat u verder tooone Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="042c7-145">Once you have successfully migrated your database schema tooSQL Data Warehouse, proceed tooone of hello following articles:</span></span>

* <span data-ttu-id="042c7-146">[Uw gegevens migreren][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="042c7-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="042c7-147">[Uw code migreren][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="042c7-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="042c7-148">Zie voor meer informatie over best practices voor SQL Data Warehouse Hallo [aanbevolen procedures] [ best practices] artikel.</span><span class="sxs-lookup"><span data-stu-id="042c7-148">For more about SQL Data Warehouse best practices, see hello [best practices][best practices] article.</span></span>

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
