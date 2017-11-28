---
title: aaaIn-geheugen OLTP verbetert de prestaties van SQL-transacties | Microsoft Docs
description: Hanteer In het geheugen OLTP tooimprove transactionele prestaties in een bestaande SQL-database.
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
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a><span data-ttu-id="317fa-103">Gebruik In het geheugen OLTP tooimprove de toepassingsprestaties van uw in SQL-Database</span><span class="sxs-lookup"><span data-stu-id="317fa-103">Use In-Memory OLTP tooimprove your application performance in SQL Database</span></span>
<span data-ttu-id="317fa-104">[In het geheugen OLTP](sql-database-in-memory.md) gebruikte tooimprove Hallo prestaties van transactieverwerking gegevensopname en tijdelijke gegevens scenario's, kunnen zich in [Premium](sql-database-service-tiers.md) Azure SQL-Databases zonder te verhogen Hallo prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="317fa-104">[In-Memory OLTP](sql-database-in-memory.md) can be used tooimprove hello performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing hello pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="317fa-105">Meer informatie over hoe [Quorum wordt sleutel database werkbelasting verdubbeld tijdens DTU verlagen door 70% met SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span><span class="sxs-lookup"><span data-stu-id="317fa-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="317fa-106">Volg deze stappen tooadopt In het geheugen OLTP in uw bestaande database.</span><span class="sxs-lookup"><span data-stu-id="317fa-106">Follow these steps tooadopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="317fa-107">Stap 1: Zorg ervoor dat u gebruikt een Premium-database</span><span class="sxs-lookup"><span data-stu-id="317fa-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="317fa-108">In het geheugen OLTP wordt alleen ondersteund in Premium-databases.</span><span class="sxs-lookup"><span data-stu-id="317fa-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="317fa-109">In het geheugen wordt ondersteund als Hallo geretourneerd resultaat is 1 (niet 0):</span><span class="sxs-lookup"><span data-stu-id="317fa-109">In-Memory is supported if hello returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="317fa-110">*XTP* staat voor *Extreme transactieverwerking*</span><span class="sxs-lookup"><span data-stu-id="317fa-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a><span data-ttu-id="317fa-111">Stap 2: Identificeren objecten toomigrate tooIn-geheugen OLTP</span><span class="sxs-lookup"><span data-stu-id="317fa-111">Step 2: Identify objects toomigrate tooIn-Memory OLTP</span></span>
<span data-ttu-id="317fa-112">SSMS bevat een **transactie prestaties Analysis overzicht** rapport dat u op een database met een actieve werkbelasting uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="317fa-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="317fa-113">Hallo-rapport identificeert de tabellen en opgeslagen procedures die geschikt voor migratie zijn tooIn-geheugen OLTP.</span><span class="sxs-lookup"><span data-stu-id="317fa-113">hello report identifies tables and stored procedures that are candidates for migration tooIn-Memory OLTP.</span></span>

<span data-ttu-id="317fa-114">In SSMS, toogenerate Hallo rapport:</span><span class="sxs-lookup"><span data-stu-id="317fa-114">In SSMS, toogenerate hello report:</span></span>

* <span data-ttu-id="317fa-115">In Hallo **Objectverkenner**, met de rechtermuisknop op het databaseknooppunt van uw.</span><span class="sxs-lookup"><span data-stu-id="317fa-115">In hello **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="317fa-116">Klik op **rapporten** > **standaardrapporten** > **transactie prestaties Analysis overzicht**.</span><span class="sxs-lookup"><span data-stu-id="317fa-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="317fa-117">Zie voor meer informatie [vaststellen als een tabel of een opgeslagen Procedure moet worden overgezet tooIn-geheugen OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span><span class="sxs-lookup"><span data-stu-id="317fa-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="317fa-118">Stap 3: Een vergelijkbare testdatabase maken</span><span class="sxs-lookup"><span data-stu-id="317fa-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="317fa-119">Stel dat het Hallo-rapport geeft aan dat de database een tabel die kunnen van wordt profiteren zouden geconverteerd tooa geheugen geoptimaliseerde tabel.</span><span class="sxs-lookup"><span data-stu-id="317fa-119">Suppose hello report indicates your database has a table that would benefit from being converted tooa memory-optimized table.</span></span> <span data-ttu-id="317fa-120">U wordt aangeraden tooconfirm Hallo indicatie eerst te testen door te testen.</span><span class="sxs-lookup"><span data-stu-id="317fa-120">We recommend that you first test tooconfirm hello indication by testing.</span></span>

<span data-ttu-id="317fa-121">U moet een test-kopie van de productiedatabase.</span><span class="sxs-lookup"><span data-stu-id="317fa-121">You need a test copy of your production database.</span></span> <span data-ttu-id="317fa-122">Hallo testdatabase moet op Hallo service hetzelfde niveau als uw productiedatabase.</span><span class="sxs-lookup"><span data-stu-id="317fa-122">hello test database should be at hello same service tier level as your production database.</span></span>

<span data-ttu-id="317fa-123">tooease tests aanpassen uw testdatabase als volgt:</span><span class="sxs-lookup"><span data-stu-id="317fa-123">tooease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="317fa-124">Verbinding maken met toohello testdatabase met behulp van SSMS.</span><span class="sxs-lookup"><span data-stu-id="317fa-124">Connect toohello test database by using SSMS.</span></span>
2. <span data-ttu-id="317fa-125">tooavoid hoeven Hallo van de optie WITH (SNAPSHOT) in query's, Hallo databaseoptie ingesteld zoals wordt weergegeven in de volgende T-SQL-instructie Hallo:</span><span class="sxs-lookup"><span data-stu-id="317fa-125">tooavoid needing hello WITH (SNAPSHOT) option in queries, set hello database option as shown in hello following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="317fa-126">Stap 4: Tabellen migreren</span><span class="sxs-lookup"><span data-stu-id="317fa-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="317fa-127">U moet maken en vullen van een kopie geoptimaliseerd voor geheugen van de tabel Hallo gewenste tootest.</span><span class="sxs-lookup"><span data-stu-id="317fa-127">You must create and populate a memory-optimized copy of hello table you want tootest.</span></span> <span data-ttu-id="317fa-128">U kunt deze maken met behulp van:</span><span class="sxs-lookup"><span data-stu-id="317fa-128">You can create it by using either:</span></span>

* <span data-ttu-id="317fa-129">Hallo handige Wizard in SSMS geheugen optimalisatie.</span><span class="sxs-lookup"><span data-stu-id="317fa-129">hello handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="317fa-130">Handmatige T-SQL.</span><span class="sxs-lookup"><span data-stu-id="317fa-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="317fa-131">Wizard van geheugen optimalisatie in SSMS</span><span class="sxs-lookup"><span data-stu-id="317fa-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="317fa-132">toouse deze migratieoptie:</span><span class="sxs-lookup"><span data-stu-id="317fa-132">toouse this migration option:</span></span>

1. <span data-ttu-id="317fa-133">Toohello testdatabase met SSMS verbinden.</span><span class="sxs-lookup"><span data-stu-id="317fa-133">Connect toohello test database with SSMS.</span></span>
2. <span data-ttu-id="317fa-134">In Hallo **Objectverkenner**, met de rechtermuisknop op het Hallo-tabel en klik vervolgens op **geheugen optimalisatie Advisor**.</span><span class="sxs-lookup"><span data-stu-id="317fa-134">In hello **Object Explorer**, right-click on hello table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="317fa-135">Hallo **tabel geheugen optimalisatie van Advisor** wizard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="317fa-135">hello **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="317fa-136">Klik in de wizard Hallo op **migratie validatie** (of Hallo **volgende** knop) toosee als Hallo tabel een heeft niet-ondersteunde functies die niet worden ondersteund in tabellen geoptimaliseerd voor geheugen.</span><span class="sxs-lookup"><span data-stu-id="317fa-136">In hello wizard, click **Migration validation** (or hello **Next** button) toosee if hello table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="317fa-137">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="317fa-137">For more information, see:</span></span>
   
   * <span data-ttu-id="317fa-138">Hallo *geheugen optimalisatie controlelijst* in [geheugen optimalisatie Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span><span class="sxs-lookup"><span data-stu-id="317fa-138">hello *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="317fa-139">[Transact-SQL-Constructs niet wordt ondersteund door In het geheugen OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span><span class="sxs-lookup"><span data-stu-id="317fa-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="317fa-140">[Migreren tooIn-geheugen OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span><span class="sxs-lookup"><span data-stu-id="317fa-140">[Migrating tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="317fa-141">Als Hallo tabel geen niet-ondersteunde onderdelen heeft, kunt Hallo advisor Hallo werkelijke schema en de gegevensmigratie voor u uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="317fa-141">If hello table has no unsupported features, hello advisor can perform hello actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="317fa-142">Handmatige T-SQL</span><span class="sxs-lookup"><span data-stu-id="317fa-142">Manual T-SQL</span></span>
<span data-ttu-id="317fa-143">toouse deze migratieoptie:</span><span class="sxs-lookup"><span data-stu-id="317fa-143">toouse this migration option:</span></span>

1. <span data-ttu-id="317fa-144">Verbinding tooyour testdatabase met SSMS (of een vergelijkbaar hulpprogramma).</span><span class="sxs-lookup"><span data-stu-id="317fa-144">Connect tooyour test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="317fa-145">Hallo volledige T-SQL-script voor de tabel en de indexen ervan verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="317fa-145">Obtain hello complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="317fa-146">SSMS, met de rechtermuisknop op het knooppunt van uw tabel.</span><span class="sxs-lookup"><span data-stu-id="317fa-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="317fa-147">Klik op **tabel als een Script** > **maken naar** > **nieuwe queryvenster**.</span><span class="sxs-lookup"><span data-stu-id="317fa-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="317fa-148">In de script-venster Hallo toevoegen WITH (MEMORY_OPTIMIZED = ON) toohello CREATE TABLE-instructie.</span><span class="sxs-lookup"><span data-stu-id="317fa-148">In hello script window, add WITH (MEMORY_OPTIMIZED = ON) toohello CREATE TABLE statement.</span></span>
4. <span data-ttu-id="317fa-149">Als er een GECLUSTERDE index, wijzigt u het tooNONCLUSTERED.</span><span class="sxs-lookup"><span data-stu-id="317fa-149">If there is a CLUSTERED index, change it tooNONCLUSTERED.</span></span>
5. <span data-ttu-id="317fa-150">Wijzig de naam van de bestaande tabel Hallo via SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="317fa-150">Rename hello existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="317fa-151">Hallo nieuwe geoptimaliseerd voor geheugen kopie maken van Hallo tabel uw bewerkte CREATE TABLE-script uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="317fa-151">Create hello new memory-optimized copy of hello table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="317fa-152">Hallo gegevens tooyour geheugen geoptimaliseerde tabel kopiëren met behulp van INSERT... SELECTEER * IN:</span><span class="sxs-lookup"><span data-stu-id="317fa-152">Copy hello data tooyour memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="317fa-153">Stap 5 (optioneel): opgeslagen procedures migreren</span><span class="sxs-lookup"><span data-stu-id="317fa-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="317fa-154">Hallo-In-Memory-functie kunt ook een opgeslagen procedure voor verbeterde prestaties wijzigen.</span><span class="sxs-lookup"><span data-stu-id="317fa-154">hello In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="317fa-155">Overwegingen voor systeemeigen, gecompileerde, opgeslagen procedures</span><span class="sxs-lookup"><span data-stu-id="317fa-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="317fa-156">Een systeemeigen, gecompileerde, opgeslagen procedure moet beschikken over de volgende opties in de component T-SQL met Hallo:</span><span class="sxs-lookup"><span data-stu-id="317fa-156">A natively compiled stored procedure must have hello following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="317fa-157">NATIVE_COMPILATION</span><span class="sxs-lookup"><span data-stu-id="317fa-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="317fa-158">SCHEMABINDING: betekenis tabellen die Hallo opgeslagen procedure geen hun kolomdefinities gewijzigd op een manier waardoor Hallo opgeslagen procedure, zou beïnvloeden, tenzij u Hallo opgeslagen procedure verwijderen.</span><span class="sxs-lookup"><span data-stu-id="317fa-158">SCHEMABINDING: meaning tables that hello stored procedure cannot have their column definitions changed in any way that would affect hello stored procedure, unless you drop hello stored procedure.</span></span>

<span data-ttu-id="317fa-159">Een systeemeigen module moet een gebruiken big [ATOMIC-blokken](http://msdn.microsoft.com/library/dn452281.aspx) voor het transactiebeheer van de.</span><span class="sxs-lookup"><span data-stu-id="317fa-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="317fa-160">Er is geen rol voor een expliciete BEGIN TRANSACTION of ROLLBACK TRANSACTION.</span><span class="sxs-lookup"><span data-stu-id="317fa-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="317fa-161">Als uw code een schending van een bedrijfsregel detecteert, deze beëindigen Hallo-atomic-blok met een [THROW](http://msdn.microsoft.com/library/ee677615.aspx) instructie.</span><span class="sxs-lookup"><span data-stu-id="317fa-161">If your code detects a violation of a business rule, it can terminate hello atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="317fa-162">Typische CREATE PROCEDURE voor systeemeigen, gecompileerde</span><span class="sxs-lookup"><span data-stu-id="317fa-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="317fa-163">Hallo T-SQL-toocreate een systeemeigen, gecompileerde, opgeslagen procedure is doorgaans vergelijkbare toohello sjabloon te volgen:</span><span class="sxs-lookup"><span data-stu-id="317fa-163">Typically hello T-SQL toocreate a natively compiled stored procedure is similar toohello following template:</span></span>

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

* <span data-ttu-id="317fa-164">MOMENTOPNAME is voor Hallo TRANSACTION_ISOLATION_LEVEL, Hallo meest voorkomende waarde voor Hallo systeemeigen, gecompileerde opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="317fa-164">For hello TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is hello most common value for hello natively compiled stored procedure.</span></span> <span data-ttu-id="317fa-165">Echter een subset van Hallo andere waarden worden ook ondersteund:</span><span class="sxs-lookup"><span data-stu-id="317fa-165">However,  a subset of hello other values are also supported:</span></span>
  
  * <span data-ttu-id="317fa-166">REPEATABLE READ</span><span class="sxs-lookup"><span data-stu-id="317fa-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="317fa-167">SERIALISEERBAAR</span><span class="sxs-lookup"><span data-stu-id="317fa-167">SERIALIZABLE</span></span>
* <span data-ttu-id="317fa-168">Hallo-waarde van taal moet aanwezig zijn in Hallo sys.languages weergeven.</span><span class="sxs-lookup"><span data-stu-id="317fa-168">hello LANGUAGE value must be present in hello sys.languages view.</span></span>

### <a name="how-toomigrate-a-stored-procedure"></a><span data-ttu-id="317fa-169">Hoe een opgeslagen procedure toomigrate</span><span class="sxs-lookup"><span data-stu-id="317fa-169">How toomigrate a stored procedure</span></span>
<span data-ttu-id="317fa-170">Hallo migratiestappen zijn:</span><span class="sxs-lookup"><span data-stu-id="317fa-170">hello migration steps are:</span></span>

1. <span data-ttu-id="317fa-171">Hallo CREATE PROCEDURE script toohello reguliere geïnterpreteerde opgeslagen procedure verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="317fa-171">Obtain hello CREATE PROCEDURE script toohello regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="317fa-172">Herschrijf de header toomatch Hallo vorige sjabloon.</span><span class="sxs-lookup"><span data-stu-id="317fa-172">Rewrite its header toomatch hello previous template.</span></span>
3. <span data-ttu-id="317fa-173">Nagaan of Hallo opgeslagen procedure T-SQL-code maakt gebruik van alle functies die worden niet ondersteund voor systeemeigen, gecompileerde, opgeslagen procedures.</span><span class="sxs-lookup"><span data-stu-id="317fa-173">Ascertain whether hello stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="317fa-174">Tijdelijke oplossingen implementeren indien nodig.</span><span class="sxs-lookup"><span data-stu-id="317fa-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="317fa-175">Zie voor meer informatie [migratieproblemen voor systeemeigen gecompileerde opgeslagen Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span><span class="sxs-lookup"><span data-stu-id="317fa-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="317fa-176">Wijzig de naam van de oude opgeslagen procedure Hallo via SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="317fa-176">Rename hello old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="317fa-177">Of u gewoon.</span><span class="sxs-lookup"><span data-stu-id="317fa-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="317fa-178">De bewerkte CREATE PROCEDURE T-SQL-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="317fa-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="317fa-179">Stap 6: Uw werkbelasting uitvoeren in de test</span><span class="sxs-lookup"><span data-stu-id="317fa-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="317fa-180">Voer een werkbelasting in uw testdatabase die is vergelijkbaar toohello werkbelasting die wordt uitgevoerd in de productiedatabase.</span><span class="sxs-lookup"><span data-stu-id="317fa-180">Run a workload in your test database that is similar toohello workload that runs in your production database.</span></span> <span data-ttu-id="317fa-181">Dit zou moeten uitwijzen Hallo prestatieverbetering bereikt door het gebruik van Hallo In-Memory-functie voor tabellen en opgeslagen procedures.</span><span class="sxs-lookup"><span data-stu-id="317fa-181">This should reveal hello performance gain achieved by your use of hello In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="317fa-182">Belangrijke kenmerken van de werkbelasting Hallo zijn:</span><span class="sxs-lookup"><span data-stu-id="317fa-182">Major attributes of hello workload are:</span></span>

* <span data-ttu-id="317fa-183">Het aantal gelijktijdige verbindingen.</span><span class="sxs-lookup"><span data-stu-id="317fa-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="317fa-184">Verhouding tussen lezen/schrijven.</span><span class="sxs-lookup"><span data-stu-id="317fa-184">Read/write ratio.</span></span>

<span data-ttu-id="317fa-185">tootailor en werkbelasting uitvoeren Hallo-test, kunt u overwegen Hallo handige ostress.exe hulpprogramma, geïllustreerd in [hier](sql-database-in-memory.md).</span><span class="sxs-lookup"><span data-stu-id="317fa-185">tootailor and run hello test workload, consider using hello handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="317fa-186">toominimize netwerklatentie, voert u uw test in Hallo dezelfde Azure geografische regio waar Hallo database bestaat.</span><span class="sxs-lookup"><span data-stu-id="317fa-186">toominimize network latency, run your test in hello same Azure geographic region where hello database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="317fa-187">Stap 7: Na de implementatie controleren</span><span class="sxs-lookup"><span data-stu-id="317fa-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="317fa-188">Houd rekening met bewaking Hallo prestaties gevolgen van uw implementaties In het geheugen in productie:</span><span class="sxs-lookup"><span data-stu-id="317fa-188">Consider monitoring hello performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="317fa-189">[In het geheugen, opslag bewaken](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="317fa-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="317fa-190">Bewaking van Azure SQL-database met behulp van de dynamische beheerweergave</span><span class="sxs-lookup"><span data-stu-id="317fa-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="317fa-191">Verwante koppelingen</span><span class="sxs-lookup"><span data-stu-id="317fa-191">Related links</span></span>
* [<span data-ttu-id="317fa-192">In het geheugen OLTP (optimalisatie In het geheugen)</span><span class="sxs-lookup"><span data-stu-id="317fa-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="317fa-193">Inleiding tooNatively gecompileerde opgeslagen Procedures</span><span class="sxs-lookup"><span data-stu-id="317fa-193">Introduction tooNatively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="317fa-194">Geheugen optimalisatie Advisor</span><span class="sxs-lookup"><span data-stu-id="317fa-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)

