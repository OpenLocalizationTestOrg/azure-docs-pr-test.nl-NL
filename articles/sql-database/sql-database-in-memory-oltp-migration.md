---
title: In het geheugen OLTP verbetert de prestaties van SQL-transacties | Microsoft Docs
description: Hanteer In het geheugen OLTP transactionele prestaties in een bestaande SQL-database te verbeteren.
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 50eed9aed417778bd497f55e20c8e732fdae9cf9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-in-memory-oltp-to-improve-your-application-performance-in-sql-database"></a><span data-ttu-id="596ab-103">Gebruik In het geheugen OLTP voor het verbeteren van de toepassingsprestaties van uw in SQL-Database</span><span class="sxs-lookup"><span data-stu-id="596ab-103">Use In-Memory OLTP to improve your application performance in SQL Database</span></span>
<span data-ttu-id="596ab-104">[In het geheugen OLTP](sql-database-in-memory.md) kan worden gebruikt voor het verbeteren van de prestaties van transactieverwerking gegevensopname en tijdelijke gegevensscenario, in [Premium](sql-database-service-tiers.md) Azure SQL-Databases zonder te verhogen van de prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="596ab-104">[In-Memory OLTP](sql-database-in-memory.md) can be used to improve the performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing the pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="596ab-105">Meer informatie over hoe [Quorum wordt sleutel database werkbelasting verdubbeld tijdens DTU verlagen door 70% met SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span><span class="sxs-lookup"><span data-stu-id="596ab-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="596ab-106">Volg deze stappen vast te stellen In het geheugen OLTP in uw bestaande database.</span><span class="sxs-lookup"><span data-stu-id="596ab-106">Follow these steps to adopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="596ab-107">Stap 1: Zorg ervoor dat u gebruikt een Premium-database</span><span class="sxs-lookup"><span data-stu-id="596ab-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="596ab-108">In het geheugen OLTP wordt alleen ondersteund in Premium-databases.</span><span class="sxs-lookup"><span data-stu-id="596ab-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="596ab-109">In het geheugen wordt ondersteund als het geretourneerde resultaat 1 (niet 0):</span><span class="sxs-lookup"><span data-stu-id="596ab-109">In-Memory is supported if the returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="596ab-110">*XTP* staat voor *Extreme transactieverwerking*</span><span class="sxs-lookup"><span data-stu-id="596ab-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-to-migrate-to-in-memory-oltp"></a><span data-ttu-id="596ab-111">Stap 2: Migreren naar een In-geheugen OLTP-objecten identificeren</span><span class="sxs-lookup"><span data-stu-id="596ab-111">Step 2: Identify objects to migrate to In-Memory OLTP</span></span>
<span data-ttu-id="596ab-112">SSMS bevat een **transactie prestaties Analysis overzicht** rapport dat u op een database met een actieve werkbelasting uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="596ab-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="596ab-113">Het rapport identificeert de tabellen en opgeslagen procedures die geschikt voor migratie naar de In-geheugen OLTP zijn.</span><span class="sxs-lookup"><span data-stu-id="596ab-113">The report identifies tables and stored procedures that are candidates for migration to In-Memory OLTP.</span></span>

<span data-ttu-id="596ab-114">In SSMS om het rapport te genereren:</span><span class="sxs-lookup"><span data-stu-id="596ab-114">In SSMS, to generate the report:</span></span>

* <span data-ttu-id="596ab-115">In de **Objectverkenner**, met de rechtermuisknop op het databaseknooppunt van uw.</span><span class="sxs-lookup"><span data-stu-id="596ab-115">In the **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="596ab-116">Klik op **rapporten** > **standaardrapporten** > **transactie prestaties Analysis overzicht**.</span><span class="sxs-lookup"><span data-stu-id="596ab-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="596ab-117">Zie voor meer informatie [vaststellen als een tabel of een opgeslagen Procedure moet worden overgezet naar de In-geheugen OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span><span class="sxs-lookup"><span data-stu-id="596ab-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported to In-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="596ab-118">Stap 3: Een vergelijkbare testdatabase maken</span><span class="sxs-lookup"><span data-stu-id="596ab-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="596ab-119">Stel dat het rapport geeft aan dat de database bevat een tabel die kunnen profiteren zouden van wordt geconverteerd naar een tabel geoptimaliseerd voor geheugen.</span><span class="sxs-lookup"><span data-stu-id="596ab-119">Suppose the report indicates your database has a table that would benefit from being converted to a memory-optimized table.</span></span> <span data-ttu-id="596ab-120">Het is raadzaam dat u eerst testen om te controleren van de vermelding door te testen.</span><span class="sxs-lookup"><span data-stu-id="596ab-120">We recommend that you first test to confirm the indication by testing.</span></span>

<span data-ttu-id="596ab-121">U moet een test-kopie van de productiedatabase.</span><span class="sxs-lookup"><span data-stu-id="596ab-121">You need a test copy of your production database.</span></span> <span data-ttu-id="596ab-122">De testdatabase moet op dezelfde service laag niveau als uw productiedatabase.</span><span class="sxs-lookup"><span data-stu-id="596ab-122">The test database should be at the same service tier level as your production database.</span></span>

<span data-ttu-id="596ab-123">Om te vereenvoudigen testen, moet u uw testdatabase als volgt aanpassen:</span><span class="sxs-lookup"><span data-stu-id="596ab-123">To ease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="596ab-124">Verbinding maken met de testdatabase met behulp van SSMS.</span><span class="sxs-lookup"><span data-stu-id="596ab-124">Connect to the test database by using SSMS.</span></span>
2. <span data-ttu-id="596ab-125">Om te voorkomen dat de optie WITH (SNAPSHOT) in query's, stelt u de databaseoptie zoals aangegeven in de volgende T-SQL-instructie:</span><span class="sxs-lookup"><span data-stu-id="596ab-125">To avoid needing the WITH (SNAPSHOT) option in queries, set the database option as shown in the following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="596ab-126">Stap 4: Tabellen migreren</span><span class="sxs-lookup"><span data-stu-id="596ab-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="596ab-127">U moet maken en vullen van een kopie geoptimaliseerd voor geheugen van de tabel die u wilt testen.</span><span class="sxs-lookup"><span data-stu-id="596ab-127">You must create and populate a memory-optimized copy of the table you want to test.</span></span> <span data-ttu-id="596ab-128">U kunt deze maken met behulp van:</span><span class="sxs-lookup"><span data-stu-id="596ab-128">You can create it by using either:</span></span>

* <span data-ttu-id="596ab-129">De handige geheugen Wizard optimalisatie in SSMS.</span><span class="sxs-lookup"><span data-stu-id="596ab-129">The handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="596ab-130">Handmatige T-SQL.</span><span class="sxs-lookup"><span data-stu-id="596ab-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="596ab-131">Wizard van geheugen optimalisatie in SSMS</span><span class="sxs-lookup"><span data-stu-id="596ab-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="596ab-132">Deze migratieoptie wilt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="596ab-132">To use this migration option:</span></span>

1. <span data-ttu-id="596ab-133">Verbinding maken met de testdatabase met SSMS.</span><span class="sxs-lookup"><span data-stu-id="596ab-133">Connect to the test database with SSMS.</span></span>
2. <span data-ttu-id="596ab-134">In de **Objectverkenner**, met de rechtermuisknop op de tabel en klik vervolgens op **geheugen optimalisatie Advisor**.</span><span class="sxs-lookup"><span data-stu-id="596ab-134">In the **Object Explorer**, right-click on the table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="596ab-135">De **tabel geheugen optimalisatie van Advisor** wizard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="596ab-135">The **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="596ab-136">Klik in de wizard op **migratie validatie** (of de **volgende** knop) om te zien als de tabel heeft een niet-ondersteunde functies die niet worden ondersteund in tabellen geoptimaliseerd voor geheugen.</span><span class="sxs-lookup"><span data-stu-id="596ab-136">In the wizard, click **Migration validation** (or the **Next** button) to see if the table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="596ab-137">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="596ab-137">For more information, see:</span></span>
   
   * <span data-ttu-id="596ab-138">De *geheugen optimalisatie controlelijst* in [geheugen optimalisatie Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span><span class="sxs-lookup"><span data-stu-id="596ab-138">The *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="596ab-139">[Transact-SQL-Constructs niet wordt ondersteund door In het geheugen OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span><span class="sxs-lookup"><span data-stu-id="596ab-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="596ab-140">[Migreren naar een In-geheugen OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span><span class="sxs-lookup"><span data-stu-id="596ab-140">[Migrating to In-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="596ab-141">Als de tabel geen niet-ondersteunde onderdelen heeft, kan de advisor de werkelijke schema en de gegevensmigratie voor u uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="596ab-141">If the table has no unsupported features, the advisor can perform the actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="596ab-142">Handmatige T-SQL</span><span class="sxs-lookup"><span data-stu-id="596ab-142">Manual T-SQL</span></span>
<span data-ttu-id="596ab-143">Deze migratieoptie wilt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="596ab-143">To use this migration option:</span></span>

1. <span data-ttu-id="596ab-144">Verbinding maken met uw testdatabase met behulp van SSMS (of een vergelijkbaar hulpprogramma).</span><span class="sxs-lookup"><span data-stu-id="596ab-144">Connect to your test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="596ab-145">Het volledige T-SQL-script voor de tabel en de bijbehorende indexen verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="596ab-145">Obtain the complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="596ab-146">SSMS, met de rechtermuisknop op het knooppunt van uw tabel.</span><span class="sxs-lookup"><span data-stu-id="596ab-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="596ab-147">Klik op **tabel als een Script** > **maken naar** > **nieuwe queryvenster**.</span><span class="sxs-lookup"><span data-stu-id="596ab-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="596ab-148">Voeg in het scriptvenster WITH (MEMORY_OPTIMIZED = ON) in de instructie CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="596ab-148">In the script window, add WITH (MEMORY_OPTIMIZED = ON) to the CREATE TABLE statement.</span></span>
4. <span data-ttu-id="596ab-149">Als er een GECLUSTERDE index, wijzigen in NONCLUSTERED.</span><span class="sxs-lookup"><span data-stu-id="596ab-149">If there is a CLUSTERED index, change it to NONCLUSTERED.</span></span>
5. <span data-ttu-id="596ab-150">Wijzig de naam van de bestaande tabel met behulp van SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="596ab-150">Rename the existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="596ab-151">Maak de nieuwe kopie geoptimaliseerd voor geheugen van de tabel de bewerkte CREATE TABLE-script uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="596ab-151">Create the new memory-optimized copy of the table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="596ab-152">Kopieer de gegevens naar de tabel geoptimaliseerd voor geheugen met behulp van INSERT... SELECTEER * IN:</span><span class="sxs-lookup"><span data-stu-id="596ab-152">Copy the data to your memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="596ab-153">Stap 5 (optioneel): opgeslagen procedures migreren</span><span class="sxs-lookup"><span data-stu-id="596ab-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="596ab-154">De In-Memory-functie kunt ook een opgeslagen procedure voor verbeterde prestaties wijzigen.</span><span class="sxs-lookup"><span data-stu-id="596ab-154">The In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="596ab-155">Overwegingen voor systeemeigen, gecompileerde, opgeslagen procedures</span><span class="sxs-lookup"><span data-stu-id="596ab-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="596ab-156">Een systeemeigen, gecompileerde, opgeslagen procedure moet hebben op de component T-SQL met de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="596ab-156">A natively compiled stored procedure must have the following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="596ab-157">NATIVE_COMPILATION</span><span class="sxs-lookup"><span data-stu-id="596ab-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="596ab-158">SCHEMABINDING: wat betekent dat tabellen die de opgeslagen procedure hun kolomdefinities gewijzigd op een manier waardoor beïnvloedt de opgeslagen procedure hebben kan, tenzij u de opgeslagen procedure verwijderen.</span><span class="sxs-lookup"><span data-stu-id="596ab-158">SCHEMABINDING: meaning tables that the stored procedure cannot have their column definitions changed in any way that would affect the stored procedure, unless you drop the stored procedure.</span></span>

<span data-ttu-id="596ab-159">Een systeemeigen module moet een gebruiken big [ATOMIC-blokken](http://msdn.microsoft.com/library/dn452281.aspx) voor het transactiebeheer van de.</span><span class="sxs-lookup"><span data-stu-id="596ab-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="596ab-160">Er is geen rol voor een expliciete BEGIN TRANSACTION of ROLLBACK TRANSACTION.</span><span class="sxs-lookup"><span data-stu-id="596ab-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="596ab-161">Als uw code een schending van een bedrijfsregel detecteert, deze beëindigen atomic-blok met een [THROW](http://msdn.microsoft.com/library/ee677615.aspx) instructie.</span><span class="sxs-lookup"><span data-stu-id="596ab-161">If your code detects a violation of a business rule, it can terminate the atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="596ab-162">Typische CREATE PROCEDURE voor systeemeigen, gecompileerde</span><span class="sxs-lookup"><span data-stu-id="596ab-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="596ab-163">De T-SQL te maken van een systeemeigen, gecompileerde, opgeslagen procedure is normaal gesproken vergelijkbaar met de volgende sjabloon:</span><span class="sxs-lookup"><span data-stu-id="596ab-163">Typically the T-SQL to create a natively compiled stored procedure is similar to the following template:</span></span>

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* <span data-ttu-id="596ab-164">Voor de TRANSACTION_ISOLATION_LEVEL is MOMENTOPNAME de meest voorkomende waarde voor de systeemeigen, gecompileerde, opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="596ab-164">For the TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is the most common value for the natively compiled stored procedure.</span></span> <span data-ttu-id="596ab-165">Een subset van de andere waarden zijn, worden ook ondersteund:</span><span class="sxs-lookup"><span data-stu-id="596ab-165">However,  a subset of the other values are also supported:</span></span>
  
  * <span data-ttu-id="596ab-166">REPEATABLE READ</span><span class="sxs-lookup"><span data-stu-id="596ab-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="596ab-167">SERIALISEERBAAR</span><span class="sxs-lookup"><span data-stu-id="596ab-167">SERIALIZABLE</span></span>
* <span data-ttu-id="596ab-168">Waarde van de taal zijn in de weergave sys.languages aanwezig.</span><span class="sxs-lookup"><span data-stu-id="596ab-168">The LANGUAGE value must be present in the sys.languages view.</span></span>

### <a name="how-to-migrate-a-stored-procedure"></a><span data-ttu-id="596ab-169">Het migreren van een opgeslagen procedure</span><span class="sxs-lookup"><span data-stu-id="596ab-169">How to migrate a stored procedure</span></span>
<span data-ttu-id="596ab-170">Migratiestappen zijn:</span><span class="sxs-lookup"><span data-stu-id="596ab-170">The migration steps are:</span></span>

1. <span data-ttu-id="596ab-171">Haal het script CREATE PROCEDURE aan de reguliere geïnterpreteerde opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="596ab-171">Obtain the CREATE PROCEDURE script to the regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="596ab-172">Herschrijf de header zodat deze overeenkomen met de vorige sjabloon.</span><span class="sxs-lookup"><span data-stu-id="596ab-172">Rewrite its header to match the previous template.</span></span>
3. <span data-ttu-id="596ab-173">Controleren of de opgeslagen procedure T-SQL-code alle functies die worden niet ondersteund voor systeemeigen, gecompileerde, opgeslagen procedures gebruikt.</span><span class="sxs-lookup"><span data-stu-id="596ab-173">Ascertain whether the stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="596ab-174">Tijdelijke oplossingen implementeren indien nodig.</span><span class="sxs-lookup"><span data-stu-id="596ab-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="596ab-175">Zie voor meer informatie [migratieproblemen voor systeemeigen gecompileerde opgeslagen Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span><span class="sxs-lookup"><span data-stu-id="596ab-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="596ab-176">Wijzig de naam van de oude opgeslagen procedure met behulp van SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="596ab-176">Rename the old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="596ab-177">Of u gewoon.</span><span class="sxs-lookup"><span data-stu-id="596ab-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="596ab-178">De bewerkte CREATE PROCEDURE T-SQL-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="596ab-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="596ab-179">Stap 6: Uw werkbelasting uitvoeren in de test</span><span class="sxs-lookup"><span data-stu-id="596ab-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="596ab-180">Voer een werkbelasting in uw testdatabase die vergelijkbaar is met de werkbelasting die wordt uitgevoerd in de productiedatabase.</span><span class="sxs-lookup"><span data-stu-id="596ab-180">Run a workload in your test database that is similar to the workload that runs in your production database.</span></span> <span data-ttu-id="596ab-181">Dit zou moeten uitwijzen de prestatieverbetering bereikt door uw gebruik van de In-Memory-functie voor tabellen en opgeslagen procedures.</span><span class="sxs-lookup"><span data-stu-id="596ab-181">This should reveal the performance gain achieved by your use of the In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="596ab-182">Belangrijke kenmerken van de werkbelasting zijn:</span><span class="sxs-lookup"><span data-stu-id="596ab-182">Major attributes of the workload are:</span></span>

* <span data-ttu-id="596ab-183">Het aantal gelijktijdige verbindingen.</span><span class="sxs-lookup"><span data-stu-id="596ab-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="596ab-184">Verhouding tussen lezen/schrijven.</span><span class="sxs-lookup"><span data-stu-id="596ab-184">Read/write ratio.</span></span>

<span data-ttu-id="596ab-185">Als u wilt aanpassen en de werkbelasting van de test uitvoert, kunt u overwegen het hulpprogramma handige ostress.exe geïllustreerd in [hier](sql-database-in-memory.md).</span><span class="sxs-lookup"><span data-stu-id="596ab-185">To tailor and run the test workload, consider using the handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="596ab-186">Om te beperken netwerklatentie, uw test worden uitgevoerd in dezelfde Azure geografische regio waar de database bestaat.</span><span class="sxs-lookup"><span data-stu-id="596ab-186">To minimize network latency, run your test in the same Azure geographic region where the database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="596ab-187">Stap 7: Na de implementatie controleren</span><span class="sxs-lookup"><span data-stu-id="596ab-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="596ab-188">Houd rekening met controle van de gevolgen van de prestaties van uw implementaties In het geheugen in productie:</span><span class="sxs-lookup"><span data-stu-id="596ab-188">Consider monitoring the performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="596ab-189">[In het geheugen, opslag bewaken](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="596ab-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="596ab-190">Bewaking van Azure SQL-database met behulp van de dynamische beheerweergave</span><span class="sxs-lookup"><span data-stu-id="596ab-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="596ab-191">Verwante koppelingen</span><span class="sxs-lookup"><span data-stu-id="596ab-191">Related links</span></span>
* [<span data-ttu-id="596ab-192">In het geheugen OLTP (optimalisatie In het geheugen)</span><span class="sxs-lookup"><span data-stu-id="596ab-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="596ab-193">Inleiding tot systeemeigen, gecompileerde, opgeslagen Procedures</span><span class="sxs-lookup"><span data-stu-id="596ab-193">Introduction to Natively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="596ab-194">Geheugen optimalisatie Advisor</span><span class="sxs-lookup"><span data-stu-id="596ab-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)

