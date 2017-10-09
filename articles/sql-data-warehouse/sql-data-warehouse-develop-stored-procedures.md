---
title: de procedures aaaStored in SQL Data Warehouse | Microsoft Docs
description: Tips voor het implementeren van opgeslagen procedures in Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 416252dd3dea95c66aa5e886860b933b22578002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="e927c-103">Opgeslagen procedures in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e927c-103">Stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="e927c-104">Veel van Hallo Transact-SQL-functies gevonden in SQL Server biedt ondersteuning voor SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e927c-104">SQL Data Warehouse supports many of hello Transact-SQL features found in SQL Server.</span></span> <span data-ttu-id="e927c-105">Er zijn belangrijker scale-out specifieke functies die we tooleverage toomaximize Hallo prestaties van uw oplossing wordt wilt.</span><span class="sxs-lookup"><span data-stu-id="e927c-105">More importantly there are scale out specific features that we will want tooleverage toomaximize hello performance of your solution.</span></span>

<span data-ttu-id="e927c-106">Toomaintain hello schaal en prestaties van SQL Data Warehouse zijn echter ook sommige functies en functionaliteit die u hebt doorgevoerd verschillen en anderen die niet worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="e927c-106">However, toomaintain hello scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>

<span data-ttu-id="e927c-107">Dit artikel wordt uitgelegd hoe tooimplement opgeslagen procedures in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e927c-107">This article explains how tooimplement stored procedures within SQL Data Warehouse.</span></span>

## <a name="introducing-stored-procedures"></a><span data-ttu-id="e927c-108">Introductie van opgeslagen procedures</span><span class="sxs-lookup"><span data-stu-id="e927c-108">Introducing stored procedures</span></span>
<span data-ttu-id="e927c-109">Opgeslagen procedures zijn een goede manier voor het inkapselen van uw SQL-code opslaan van het sluiten tooyour gegevens in het datawarehouse Hallo.</span><span class="sxs-lookup"><span data-stu-id="e927c-109">Stored procedures are a great way for encapsulating your SQL code; storing it close tooyour data in hello data warehouse.</span></span> <span data-ttu-id="e927c-110">Door het Hallo-code in beheerbare eenheden encapsulating opgeslagen procedures ontwikkelaars helpen bij het modularize hun oplossingen; vergemakkelijken groter herbruikbaarheid van code.</span><span class="sxs-lookup"><span data-stu-id="e927c-110">By encapsulating hello code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span></span> <span data-ttu-id="e927c-111">Elke opgeslagen procedure kan ook parameters toomake accepteren ze nog meer flexibiliteit.</span><span class="sxs-lookup"><span data-stu-id="e927c-111">Each stored procedure can also accept parameters toomake them even more flexible.</span></span>

<span data-ttu-id="e927c-112">SQL Data Warehouse biedt een vereenvoudigd en gestroomlijnd opgeslagen procedure-implementatie.</span><span class="sxs-lookup"><span data-stu-id="e927c-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="e927c-113">Hallo grootste verschil vergeleken tooSQL-Server is die Hallo opgeslagen procedure is niet vooraf gecompileerde code.</span><span class="sxs-lookup"><span data-stu-id="e927c-113">hello biggest difference compared tooSQL Server is that hello stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="e927c-114">In datawarehouses we in het algemeen minder betrokken zijn bij het Hallo-compilatietijd.</span><span class="sxs-lookup"><span data-stu-id="e927c-114">In data warehouses we are generally less concerned with hello compilation time.</span></span> <span data-ttu-id="e927c-115">Het is belangrijk dat Hallo opgeslagen procedurecode correct is geoptimaliseerd, als het wordt uitgevoerd op basis van grote hoeveelheden gegevens.</span><span class="sxs-lookup"><span data-stu-id="e927c-115">It is more important that hello stored procedure code is correctly optimised when operating against large data volumes.</span></span> <span data-ttu-id="e927c-116">Hallo-doel is toosave uren, minuten en seconden niet milliseconden.</span><span class="sxs-lookup"><span data-stu-id="e927c-116">hello goal is toosave hours, minutes and seconds not milliseconds.</span></span> <span data-ttu-id="e927c-117">Daarom is het handiger toothink van opgeslagen procedures als containers voor SQL-logica.</span><span class="sxs-lookup"><span data-stu-id="e927c-117">It is therefore more helpful toothink of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="e927c-118">Wanneer SQL Data Warehouse wordt uitgevoerd zijn de opgeslagen procedure Hallo SQL-instructies geparseerd, vertaald en geoptimaliseerd tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="e927c-118">When SQL Data Warehouse executes your stored procedure hello SQL statements are parsed, translated and optimized at run time.</span></span> <span data-ttu-id="e927c-119">Tijdens dit proces wordt elke instructie omgezet in gedistribueerde query's.</span><span class="sxs-lookup"><span data-stu-id="e927c-119">During this process each statement is converted into distributed queries.</span></span> <span data-ttu-id="e927c-120">SQL-code die daadwerkelijk wordt uitgevoerd op gegevens Hallo Hallo is verschillende toohello query verzonden.</span><span class="sxs-lookup"><span data-stu-id="e927c-120">hello SQL code that is actually executed against hello data is different toohello query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="e927c-121">Nesten van opgeslagen procedures</span><span class="sxs-lookup"><span data-stu-id="e927c-121">Nesting stored procedures</span></span>
<span data-ttu-id="e927c-122">Als opgeslagen procedures andere opgeslagen procedures aanroepen of dynamische sql uitvoeren Hallo interne opgeslagen procedure of code aanroep wordt gezegd toobe genest.</span><span class="sxs-lookup"><span data-stu-id="e927c-122">When stored procedures call other stored procedures or execute dynamic sql then hello inner stored procedure or code invocation is said toobe nested.</span></span>

<span data-ttu-id="e927c-123">SQL Data Warehouse ondersteunt maximaal 8 geneste niveaus.</span><span class="sxs-lookup"><span data-stu-id="e927c-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span></span> <span data-ttu-id="e927c-124">Dit is een iets andere tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="e927c-124">This is slightly different tooSQL Server.</span></span> <span data-ttu-id="e927c-125">Hallo nest niveau in SQL Server is 32.</span><span class="sxs-lookup"><span data-stu-id="e927c-125">hello nest level in SQL Server is 32.</span></span>

<span data-ttu-id="e927c-126">aanroepen van de bovenste niveau opgeslagen procedure Hallo gelijkstaat toonest niveau 1</span><span class="sxs-lookup"><span data-stu-id="e927c-126">hello top level stored procedure call equates toonest level 1</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="e927c-127">Als Hallo opgeslagen procedure kan ook een andere EXEC aanroep wordt hierdoor neemt Hallo nest niveau too2</span><span class="sxs-lookup"><span data-stu-id="e927c-127">If hello stored procedure also makes another EXEC call then this will increase hello nest level too2</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="e927c-128">Als u de tweede procedure Hallo voert enkele dynamische sql vervolgens vergroten dit Hallo nest niveau too3</span><span class="sxs-lookup"><span data-stu-id="e927c-128">If hello second procedure then executes some dynamic sql then this will increase hello nest level too3</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="e927c-129">Opmerking SQL Data Warehouse ondersteunt momenteel geen@NESTLEVEL.</span><span class="sxs-lookup"><span data-stu-id="e927c-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span></span> <span data-ttu-id="e927c-130">U moet een nummer van uw niveau nest tookeep zelf.</span><span class="sxs-lookup"><span data-stu-id="e927c-130">You will need tookeep a track of your nest level yourself.</span></span> <span data-ttu-id="e927c-131">Het lijkt onwaarschijnlijk u Hallo 8 nest limiet bereikt, maar als u u wilt nodig hebt toore werk uw code en 'plat' deze zodat het past binnen deze limiet.</span><span class="sxs-lookup"><span data-stu-id="e927c-131">It is unlikely you will hit hello 8 nest level limit but if you do you will need toore-work your code and "flatten" it so that it fits within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="e927c-132">INSERT... UITVOEREN</span><span class="sxs-lookup"><span data-stu-id="e927c-132">INSERT..EXECUTE</span></span>
<span data-ttu-id="e927c-133">SQL Data Warehouse mag u geen tooconsume Hallo resultatenset van een opgeslagen procedure met een instructie INSERT.</span><span class="sxs-lookup"><span data-stu-id="e927c-133">SQL Data Warehouse does not permit you tooconsume hello result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="e927c-134">Er is echter een alternatieve methode die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e927c-134">However, there is an alternative approach you can use.</span></span>

<span data-ttu-id="e927c-135">Raadpleeg de volgende artikel op toohello [tijdelijke tabellen] voor een voorbeeld over het toodo dit.</span><span class="sxs-lookup"><span data-stu-id="e927c-135">Please refer toohello following article on [temporary tables] for an example on how toodo this.</span></span>

## <a name="limitations"></a><span data-ttu-id="e927c-136">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="e927c-136">Limitations</span></span>
<span data-ttu-id="e927c-137">Er zijn bepaalde aspecten van Transact-SQL opgeslagen procedures die niet zijn geïmplementeerd in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e927c-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="e927c-138">Ze zijn:</span><span class="sxs-lookup"><span data-stu-id="e927c-138">They are:</span></span>

* <span data-ttu-id="e927c-139">tijdelijke opgeslagen procedures</span><span class="sxs-lookup"><span data-stu-id="e927c-139">temporary stored procedures</span></span>
* <span data-ttu-id="e927c-140">genummerde opgeslagen procedures</span><span class="sxs-lookup"><span data-stu-id="e927c-140">numbered stored procedures</span></span>
* <span data-ttu-id="e927c-141">uitgebreide opgeslagen procedures</span><span class="sxs-lookup"><span data-stu-id="e927c-141">extended stored procedures</span></span>
* <span data-ttu-id="e927c-142">CLR opgeslagen procedures</span><span class="sxs-lookup"><span data-stu-id="e927c-142">CLR stored procedures</span></span>
* <span data-ttu-id="e927c-143">versleutelingsoptie</span><span class="sxs-lookup"><span data-stu-id="e927c-143">encryption option</span></span>
* <span data-ttu-id="e927c-144">replicatie-optie</span><span class="sxs-lookup"><span data-stu-id="e927c-144">replication option</span></span>
* <span data-ttu-id="e927c-145">Table-valued parameters</span><span class="sxs-lookup"><span data-stu-id="e927c-145">table-valued parameters</span></span>
* <span data-ttu-id="e927c-146">alleen-lezen parameters</span><span class="sxs-lookup"><span data-stu-id="e927c-146">read-only parameters</span></span>
* <span data-ttu-id="e927c-147">standaardparameters</span><span class="sxs-lookup"><span data-stu-id="e927c-147">default parameters</span></span>
* <span data-ttu-id="e927c-148">contexten worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="e927c-148">execution contexts</span></span>
* <span data-ttu-id="e927c-149">instructie return</span><span class="sxs-lookup"><span data-stu-id="e927c-149">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="e927c-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e927c-150">Next steps</span></span>
<span data-ttu-id="e927c-151">Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].</span><span class="sxs-lookup"><span data-stu-id="e927c-151">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[tijdelijke tabellen]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
