---
title: aaaHow toouse batchverwerking tooimprove Azure SQL Database-toepassingsprestaties
description: Hallo onderwerp vindt u bewijs dat batchverwerking database operations aanzienlijk imroves Hallo snelheid en schaalbaarheid van uw Azure SQL Database-toepassingen. Hoewel deze batchen technieken voor elke SQL Server-database werken, Hallo Hallo artikel worden op Azure.
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a><span data-ttu-id="16670-104">Hoe toouse batchverwerking tooimprove SQL Database-toepassingsprestaties</span><span class="sxs-lookup"><span data-stu-id="16670-104">How toouse batching tooimprove SQL Database application performance</span></span>
<span data-ttu-id="16670-105">Batchverwerking van bewerkingen tooAzure SQL-Database aanzienlijk verbetert Hallo prestaties en schaalbaarheid van uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="16670-105">Batching operations tooAzure SQL Database significantly improves hello performance and scalability of your applications.</span></span> <span data-ttu-id="16670-106">In de volgorde toounderstand Hallo voordelen Hallo eerste deel van dit artikel bevat informatie over sommige voorbeeld testresultaten die sequentieel en batch aanvragen tooa SQL-Database te vergelijken.</span><span class="sxs-lookup"><span data-stu-id="16670-106">In order toounderstand hello benefits, hello first part of this article covers some sample test results that compare sequential and batched requests tooa SQL Database.</span></span> <span data-ttu-id="16670-107">Hallo rest van Hallo artikel geeft Hallo technieken, scenario's en overwegingen toohelp u toouse batchverwerking is in uw Azure-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="16670-107">hello remainder of hello article shows hello techniques, scenarios, and considerations toohelp you toouse batching successfully in your Azure applications.</span></span>

## <a name="why-is-batching-important-for-sql-database"></a><span data-ttu-id="16670-108">Waarom is batchverwerking belangrijk voor SQL-Database?</span><span class="sxs-lookup"><span data-stu-id="16670-108">Why is batching important for SQL Database?</span></span>
<span data-ttu-id="16670-109">Batchverwerking aanroepen tooa externe service is een bekende strategie voor prestaties en schaalbaarheid te verhogen.</span><span class="sxs-lookup"><span data-stu-id="16670-109">Batching calls tooa remote service is a well-known strategy for increasing performance and scalability.</span></span> <span data-ttu-id="16670-110">Er zijn vaste kosten tooany interactie met een externe service, zoals serialisatie netwerkoverdracht en deserialisatie verwerken.</span><span class="sxs-lookup"><span data-stu-id="16670-110">There are fixed processing costs tooany interactions with a remote service, such as serialization, network transfer, and deserialization.</span></span> <span data-ttu-id="16670-111">Veel afzonderlijke transacties in één batch minimaliseert deze kosten.</span><span class="sxs-lookup"><span data-stu-id="16670-111">Packaging many separate transactions into a single batch minimizes these costs.</span></span>

<span data-ttu-id="16670-112">In dit artikel willen we tooexamine verschillende scenario's en batchen strategieën SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="16670-112">In this paper, we want tooexamine various SQL Database batching strategies and scenarios.</span></span> <span data-ttu-id="16670-113">Hoewel deze strategieën ook belang voor on-premises toepassingen die gebruikmaken van SQL Server zijn, zijn er diverse redenen voor Hallo gebruik van batchverwerking voor SQL-Database te markeren:</span><span class="sxs-lookup"><span data-stu-id="16670-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting hello use of batching for SQL Database:</span></span>

* <span data-ttu-id="16670-114">Er is mogelijk groter netwerklatentie toegang tot SQL-Database, met name als u krijgt u toegang tot SQL-Database van de buitenste Hallo hetzelfde Microsoft Azure-datacenter.</span><span class="sxs-lookup"><span data-stu-id="16670-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside hello same Microsoft Azure datacenter.</span></span>
* <span data-ttu-id="16670-115">Hallo multitenant kenmerken van SQL-Database betekent dat de efficiëntie van de gegevens Hallo Hallo toegang tot laag standaarddocumentnaam toohello algehele schaalbaarheid van Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="16670-115">hello multitenant characteristics of SQL Database means that hello efficiency of hello data access layer correlates toohello overall scalability of hello database.</span></span> <span data-ttu-id="16670-116">SQL-Database moet voorkomen dat een single-tenant/gebruiker nadeel werken toohello van database-bronnen van andere tenants belasten.</span><span class="sxs-lookup"><span data-stu-id="16670-116">SQL Database must prevent any single tenant/user from monopolizing database resources toohello detriment of other tenants.</span></span> <span data-ttu-id="16670-117">In het antwoord toousage boven het vooraf gedefinieerde quota, SQL Database verminderen doorvoer of reageren met een beperking van uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="16670-117">In response toousage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span></span> <span data-ttu-id="16670-118">Efficiëntie, zoals batches, kunnen u toodo meer werk voor SQL-Database voordat deze limiet is bereikt.</span><span class="sxs-lookup"><span data-stu-id="16670-118">Efficiencies, such as batching, enable you toodo more work on SQL Database before reaching these limits.</span></span> 
* <span data-ttu-id="16670-119">Batchverwerking is ook geschikt voor architecturen die gebruikmaken van meerdere databases (sharding).</span><span class="sxs-lookup"><span data-stu-id="16670-119">Batching is also effective for architectures that use multiple databases (sharding).</span></span> <span data-ttu-id="16670-120">Hallo-efficiëntie van uw interactie met elke eenheid database nog steeds een belangrijke factor in uw algehele schaalbaarheid.</span><span class="sxs-lookup"><span data-stu-id="16670-120">hello efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span></span> 

<span data-ttu-id="16670-121">Een van de Hallo voordelen van het gebruik van SQL-Database is dat er geen toomanage Hallo servers die host Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="16670-121">One of hello benefits of using SQL Database is that you don’t have toomanage hello servers that host hello database.</span></span> <span data-ttu-id="16670-122">Deze beheerde infrastructuur ook betekent echter dat u toothink anders over optimalisaties van de database hebt.</span><span class="sxs-lookup"><span data-stu-id="16670-122">However, this managed infrastructure also means that you have toothink differently about database optimizations.</span></span> <span data-ttu-id="16670-123">U kunt niet meer tooimprove Hallo database hardware- of -infrastructuur te zoeken.</span><span class="sxs-lookup"><span data-stu-id="16670-123">You can no longer look tooimprove hello database hardware or network infrastructure.</span></span> <span data-ttu-id="16670-124">Microsoft Azure bepaalt deze omgevingen.</span><span class="sxs-lookup"><span data-stu-id="16670-124">Microsoft Azure controls those environments.</span></span> <span data-ttu-id="16670-125">Hallo gebied die u kunt beheren, is de interactie van uw toepassing met de SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="16670-125">hello main area that you can control is how your application interacts with SQL Database.</span></span> <span data-ttu-id="16670-126">Batchverwerking is een van deze optimalisaties.</span><span class="sxs-lookup"><span data-stu-id="16670-126">Batching is one of these optimizations.</span></span> 

<span data-ttu-id="16670-127">eerste deel van de Hallo Hallo papier onderzoekt verschillende batchen technieken voor .NET-toepassingen die gebruikmaken van SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="16670-127">hello first part of hello paper examines various batching techniques for .NET applications that use SQL Database.</span></span> <span data-ttu-id="16670-128">de laatste twee secties Hallo uitgelegd batchen scenario's en richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="16670-128">hello last two sections cover batching guidelines and scenarios.</span></span>

## <a name="batching-strategies"></a><span data-ttu-id="16670-129">Batchverwerking strategieën</span><span class="sxs-lookup"><span data-stu-id="16670-129">Batching strategies</span></span>
### <a name="note-about-timing-results-in-this-topic"></a><span data-ttu-id="16670-130">Houd er rekening mee over timing resultaten in dit onderwerp</span><span class="sxs-lookup"><span data-stu-id="16670-130">Note about timing results in this topic</span></span>
> [!NOTE]
> <span data-ttu-id="16670-131">Resultaten niet benchmarks, maar zijn bedoeld tooshow **relatieve prestaties**.</span><span class="sxs-lookup"><span data-stu-id="16670-131">Results are not benchmarks but are meant tooshow **relative performance**.</span></span> <span data-ttu-id="16670-132">Tijdsinstellingen zijn gebaseerd op een gemiddelde van ten minste 10 test wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="16670-132">Timings are based on an average of at least 10 test runs.</span></span> <span data-ttu-id="16670-133">Bewerkingen worden ingevoegd in een lege tabel.</span><span class="sxs-lookup"><span data-stu-id="16670-133">Operations are inserts into an empty table.</span></span> <span data-ttu-id="16670-134">Deze tests zijn gemeten pre-V12 en ze niet per se toothroughput die mogelijk optreden in een V12-database met Hallo nieuwe overeenkomen [Servicelagen](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="16670-134">These tests were measured pre-V12, and they do not necessarily correspond toothroughput that you might experience in a V12 database using hello new [service tiers](sql-database-service-tiers.md).</span></span> <span data-ttu-id="16670-135">Hallo relatieve voordeel van het Hallo batchverwerking techniek moet vergelijkbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="16670-135">hello relative benefit of hello batching technique should be similar.</span></span>
> 
> 

### <a name="transactions"></a><span data-ttu-id="16670-136">Transacties</span><span class="sxs-lookup"><span data-stu-id="16670-136">Transactions</span></span>
<span data-ttu-id="16670-137">Het lijkt erop vreemd toobegin een overzicht van batchverwerking door het bespreken van transacties.</span><span class="sxs-lookup"><span data-stu-id="16670-137">It seems strange toobegin a review of batching by discussing transactions.</span></span> <span data-ttu-id="16670-138">Maar gebruik Hallo van client-side transacties heeft een subtiele serverzijde batchen-effect dat zorgt voor betere prestaties.</span><span class="sxs-lookup"><span data-stu-id="16670-138">But hello use of client-side transactions has a subtle server-side batching effect that improves performance.</span></span> <span data-ttu-id="16670-139">En transacties kunnen worden toegevoegd met slechts een paar regels code, zodat ze een snelle manier tooimprove prestaties van opeenvolgende bewerkingen bieden.</span><span class="sxs-lookup"><span data-stu-id="16670-139">And transactions can be added with only a few lines of code, so they provide a fast way tooimprove performance of sequential operations.</span></span>

<span data-ttu-id="16670-140">Overweeg het volgende C#-code die een reeks van insert bevat Hallo en bewerkingen op een eenvoudige tabel bijwerken.</span><span class="sxs-lookup"><span data-stu-id="16670-140">Consider hello following C# code that contains a sequence of insert and update operations on a simple table.</span></span>

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

<span data-ttu-id="16670-141">Hallo ADO.NET code sequentieel na voert deze bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="16670-141">hello following ADO.NET code sequentially performs these operations.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

<span data-ttu-id="16670-142">Hallo de beste manier toooptimize deze code tooimplement is een vorm van client-side batchverwerking van deze aanroepen.</span><span class="sxs-lookup"><span data-stu-id="16670-142">hello best way toooptimize this code is tooimplement some form of client-side batching of these calls.</span></span> <span data-ttu-id="16670-143">Maar er is een eenvoudige manier tooincrease Hallo prestaties van deze code door gewoon Hallo reeks aanroepen in een transactie.</span><span class="sxs-lookup"><span data-stu-id="16670-143">But there is a simple way tooincrease hello performance of this code by simply wrapping hello sequence of calls in a transaction.</span></span> <span data-ttu-id="16670-144">Hier volgt Hallo dezelfde code die gebruikmaakt van een transactie.</span><span class="sxs-lookup"><span data-stu-id="16670-144">Here is hello same code that uses a transaction.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

<span data-ttu-id="16670-145">In beide voorbeelden worden daadwerkelijk transacties gebruikt.</span><span class="sxs-lookup"><span data-stu-id="16670-145">Transactions are actually being used in both of these examples.</span></span> <span data-ttu-id="16670-146">In het eerste voorbeeld hello is elke aanroep van afzonderlijke een impliciete transactie.</span><span class="sxs-lookup"><span data-stu-id="16670-146">In hello first example, each individual call is an implicit transaction.</span></span> <span data-ttu-id="16670-147">Een expliciete transactie verpakt in het tweede voorbeeld hello, alle Hallo aanroepen.</span><span class="sxs-lookup"><span data-stu-id="16670-147">In hello second example, an explicit transaction wraps all of hello calls.</span></span> <span data-ttu-id="16670-148">Per Hallo-documentatie voor Hallo [vooraf geschreven transactielogboek](https://msdn.microsoft.com/library/ms186259.aspx), logboekrecords worden leeggemaakt toohello schijf wanneer Hallo transactie wordt doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="16670-148">Per hello documentation for hello [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed toohello disk when hello transaction commits.</span></span> <span data-ttu-id="16670-149">Dus door meer aanroepen in een transactie, kan hello schrijven toohello transactielogboek stellen tot Hallo transactie doorgevoerd is.</span><span class="sxs-lookup"><span data-stu-id="16670-149">So by including more calls in a transaction, hello write toohello transaction log can delay until hello transaction is committed.</span></span> <span data-ttu-id="16670-150">In feite inschakelt u voor Hallo schrijfbewerkingen toohello van server-transactielogboek batchverwerking.</span><span class="sxs-lookup"><span data-stu-id="16670-150">In effect, you are enabling batching for hello writes toohello server’s transaction log.</span></span>

<span data-ttu-id="16670-151">Hallo volgende tabel ziet u enkele ad-hoc-testresultaten.</span><span class="sxs-lookup"><span data-stu-id="16670-151">hello following table shows some ad-hoc testing results.</span></span> <span data-ttu-id="16670-152">Hallo tests uitgevoerd Hallo die dezelfde sequentiële met en zonder transacties voegt.</span><span class="sxs-lookup"><span data-stu-id="16670-152">hello tests performed hello same sequential inserts with and without transactions.</span></span> <span data-ttu-id="16670-153">Voor meer perspectief Hallo eerste reeks tests op afstand vanaf uitgevoerd een laptop toohello-database in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="16670-153">For more perspective, hello first set of tests ran remotely from a laptop toohello database in Microsoft Azure.</span></span> <span data-ttu-id="16670-154">Hallo tweede reeks tests uitgevoerd vanuit een cloudservice en de database dat beide zich bevond in Hallo dezelfde Microsoft Azure-datacenter (VS-West).</span><span class="sxs-lookup"><span data-stu-id="16670-154">hello second set of tests ran from a cloud service and database that both resided within hello same Microsoft Azure datacenter (West US).</span></span> <span data-ttu-id="16670-155">Hallo volgende tabel toont Hallo duur in milliseconden van opeenvolgende voegt met en zonder transacties.</span><span class="sxs-lookup"><span data-stu-id="16670-155">hello following table shows hello duration in milliseconds of sequential inserts with and without transactions.</span></span>

<span data-ttu-id="16670-156">**On-Premises tooAzure**:</span><span class="sxs-lookup"><span data-stu-id="16670-156">**On-Premises tooAzure**:</span></span>

| <span data-ttu-id="16670-157">Bewerkingen</span><span class="sxs-lookup"><span data-stu-id="16670-157">Operations</span></span> | <span data-ttu-id="16670-158">Er is geen transactie (ms)</span><span class="sxs-lookup"><span data-stu-id="16670-158">No Transaction (ms)</span></span> | <span data-ttu-id="16670-159">Transactie (ms)</span><span class="sxs-lookup"><span data-stu-id="16670-159">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="16670-160">1</span><span class="sxs-lookup"><span data-stu-id="16670-160">1</span></span> |<span data-ttu-id="16670-161">130</span><span class="sxs-lookup"><span data-stu-id="16670-161">130</span></span> |<span data-ttu-id="16670-162">402</span><span class="sxs-lookup"><span data-stu-id="16670-162">402</span></span> |
| <span data-ttu-id="16670-163">10</span><span class="sxs-lookup"><span data-stu-id="16670-163">10</span></span> |<span data-ttu-id="16670-164">1208</span><span class="sxs-lookup"><span data-stu-id="16670-164">1208</span></span> |<span data-ttu-id="16670-165">1226</span><span class="sxs-lookup"><span data-stu-id="16670-165">1226</span></span> |
| <span data-ttu-id="16670-166">100</span><span class="sxs-lookup"><span data-stu-id="16670-166">100</span></span> |<span data-ttu-id="16670-167">12662</span><span class="sxs-lookup"><span data-stu-id="16670-167">12662</span></span> |<span data-ttu-id="16670-168">10395</span><span class="sxs-lookup"><span data-stu-id="16670-168">10395</span></span> |
| <span data-ttu-id="16670-169">1000</span><span class="sxs-lookup"><span data-stu-id="16670-169">1000</span></span> |<span data-ttu-id="16670-170">128852</span><span class="sxs-lookup"><span data-stu-id="16670-170">128852</span></span> |<span data-ttu-id="16670-171">102917</span><span class="sxs-lookup"><span data-stu-id="16670-171">102917</span></span> |

<span data-ttu-id="16670-172">**Azure tooAzure (hetzelfde datacenter)**:</span><span class="sxs-lookup"><span data-stu-id="16670-172">**Azure tooAzure (same datacenter)**:</span></span>

| <span data-ttu-id="16670-173">Bewerkingen</span><span class="sxs-lookup"><span data-stu-id="16670-173">Operations</span></span> | <span data-ttu-id="16670-174">Er is geen transactie (ms)</span><span class="sxs-lookup"><span data-stu-id="16670-174">No Transaction (ms)</span></span> | <span data-ttu-id="16670-175">Transactie (ms)</span><span class="sxs-lookup"><span data-stu-id="16670-175">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="16670-176">1</span><span class="sxs-lookup"><span data-stu-id="16670-176">1</span></span> |<span data-ttu-id="16670-177">21</span><span class="sxs-lookup"><span data-stu-id="16670-177">21</span></span> |<span data-ttu-id="16670-178">26</span><span class="sxs-lookup"><span data-stu-id="16670-178">26</span></span> |
| <span data-ttu-id="16670-179">10</span><span class="sxs-lookup"><span data-stu-id="16670-179">10</span></span> |<span data-ttu-id="16670-180">220</span><span class="sxs-lookup"><span data-stu-id="16670-180">220</span></span> |<span data-ttu-id="16670-181">56</span><span class="sxs-lookup"><span data-stu-id="16670-181">56</span></span> |
| <span data-ttu-id="16670-182">100</span><span class="sxs-lookup"><span data-stu-id="16670-182">100</span></span> |<span data-ttu-id="16670-183">2145</span><span class="sxs-lookup"><span data-stu-id="16670-183">2145</span></span> |<span data-ttu-id="16670-184">341</span><span class="sxs-lookup"><span data-stu-id="16670-184">341</span></span> |
| <span data-ttu-id="16670-185">1000</span><span class="sxs-lookup"><span data-stu-id="16670-185">1000</span></span> |<span data-ttu-id="16670-186">21479</span><span class="sxs-lookup"><span data-stu-id="16670-186">21479</span></span> |<span data-ttu-id="16670-187">2756</span><span class="sxs-lookup"><span data-stu-id="16670-187">2756</span></span> |

> [!NOTE]
> <span data-ttu-id="16670-188">Geen zijn resultaten benchmarks.</span><span class="sxs-lookup"><span data-stu-id="16670-188">Results are not benchmarks.</span></span> <span data-ttu-id="16670-189">Zie Hallo [opmerking over timing resultaten in dit onderwerp](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="16670-189">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="16670-190">Op basis van de vorige testresultaten hello, één bewerking in een transactie wrapping neemt af prestaties.</span><span class="sxs-lookup"><span data-stu-id="16670-190">Based on hello previous test results, wrapping a single operation in a transaction actually decreases performance.</span></span> <span data-ttu-id="16670-191">Maar als u het aantal bewerkingen binnen een enkele transactie Hallo verhoogt, Hallo prestatieverbeteringen meer wordt gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="16670-191">But as you increase hello number of operations within a single transaction, hello performance improvement becomes more marked.</span></span> <span data-ttu-id="16670-192">Hallo prestatieverschil is ook meer merkbare bij alle bewerkingen binnen Hallo Microsoft Azure-datacenter plaatsvinden.</span><span class="sxs-lookup"><span data-stu-id="16670-192">hello performance difference is also more noticeable when all operations occur within hello Microsoft Azure datacenter.</span></span> <span data-ttu-id="16670-193">Hallo overshadows langere latentie van het gebruik van SQL-Database van Microsoft Azure-datacenter buiten Hallo Hallo prestatieverbetering te bereiken van het gebruik van transacties.</span><span class="sxs-lookup"><span data-stu-id="16670-193">hello increased latency of using SQL Database from outside hello Microsoft Azure datacenter overshadows hello performance gain of using transactions.</span></span>

<span data-ttu-id="16670-194">Hoewel het gebruik van transacties Hallo van de prestaties verhogen kunt te blijven[observeren best practices voor transacties en verbindingen](https://msdn.microsoft.com/library/ms187484.aspx).</span><span class="sxs-lookup"><span data-stu-id="16670-194">Although hello use of transactions can increase performance, continue too[observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span></span> <span data-ttu-id="16670-195">Hallo-transactie zo kort mogelijk en sluiten Hallo databaseverbinding behouden nadat Hallo werk is voltooid.</span><span class="sxs-lookup"><span data-stu-id="16670-195">Keep hello transaction as short as possible, and close hello database connection after hello work completes.</span></span> <span data-ttu-id="16670-196">met de instructie in het vorige voorbeeld Hallo Hallo zorgt ervoor dat de Hallo verbinding wordt gesloten wanneer het volgende codeblok Hallo is voltooid.</span><span class="sxs-lookup"><span data-stu-id="16670-196">hello using statement in hello previous example assures that hello connection is closed when hello subsequent code block completes.</span></span>

<span data-ttu-id="16670-197">Hallo vorige voorbeeld laat zien dat u een lokale transactie tooany ADO.NET code met twee regels kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="16670-197">hello previous example demonstrates that you can add a local transaction tooany ADO.NET code with two lines.</span></span> <span data-ttu-id="16670-198">Transacties bieden een snelle manier tooimprove Hallo prestaties van code waarmee u opeenvolgende invoegen, bijwerken en verwijderen van bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="16670-198">Transactions offer a quick way tooimprove hello performance of code that makes sequential insert, update, and delete operations.</span></span> <span data-ttu-id="16670-199">Echter kunt wijzigen in Hallo code verdere tootake profiteren van de client-side batches, zoals table-valued parameters voor de snelste Hallo prestaties.</span><span class="sxs-lookup"><span data-stu-id="16670-199">However, for hello fastest performance, consider changing hello code further tootake advantage of client-side batching, such as table-valued parameters.</span></span>

<span data-ttu-id="16670-200">Zie voor meer informatie over transacties in ADO.NET [lokale transacties in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span><span class="sxs-lookup"><span data-stu-id="16670-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span></span>

### <a name="table-valued-parameters"></a><span data-ttu-id="16670-201">Table-valued parameters</span><span class="sxs-lookup"><span data-stu-id="16670-201">Table-valued parameters</span></span>
<span data-ttu-id="16670-202">Tabeltypen die door de gebruiker gedefinieerde ondersteunen table-valued parameters als parameters in de Transact-SQL-instructies, opgeslagen procedures en functies.</span><span class="sxs-lookup"><span data-stu-id="16670-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span></span> <span data-ttu-id="16670-203">Deze client-side batchen techniek kunt u toosend meerdere rijen van gegevens binnen Hallo tabelwaardeparameter.</span><span class="sxs-lookup"><span data-stu-id="16670-203">This client-side batching technique allows you toosend multiple rows of data within hello table-valued parameter.</span></span> <span data-ttu-id="16670-204">toouse table-valued parameters definiëren eerst een tabeltype.</span><span class="sxs-lookup"><span data-stu-id="16670-204">toouse table-valued parameters, first define a table type.</span></span> <span data-ttu-id="16670-205">Hallo volgende Transact-SQL-instructie maakt een tabeltype met de naam **MyTableType**.</span><span class="sxs-lookup"><span data-stu-id="16670-205">hello following Transact-SQL statement creates a table type named **MyTableType**.</span></span>

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


<span data-ttu-id="16670-206">In de code, maakt u een **DataTable** Hello exact dezelfde namen en typen van Hallo tabeltype.</span><span class="sxs-lookup"><span data-stu-id="16670-206">In code, you create a **DataTable** with hello exact same names and types of hello table type.</span></span> <span data-ttu-id="16670-207">Dit geeft **DataTable** aanroepen in een parameter van een tekstquery of een opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="16670-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span></span> <span data-ttu-id="16670-208">Hallo volgende voorbeeld ziet u deze techniek:</span><span class="sxs-lookup"><span data-stu-id="16670-208">hello following example shows this technique:</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

<span data-ttu-id="16670-209">In het vorige voorbeeld Hallo Hallo **SqlCommand** object voegt rijen uit een tabelwaardeparameter  **@TestTvp** .</span><span class="sxs-lookup"><span data-stu-id="16670-209">In hello previous example, hello **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span></span> <span data-ttu-id="16670-210">Hallo eerder gemaakte **DataTable** -object toegewezen toothis parameter Hello **SqlCommand.Parameters.Add** methode.</span><span class="sxs-lookup"><span data-stu-id="16670-210">hello previously created **DataTable** object is assigned toothis parameter with hello **SqlCommand.Parameters.Add** method.</span></span> <span data-ttu-id="16670-211">Batchen Hallo invoegen in een aanroep aanzienlijk toeneemt Hallo prestaties via sequentiële ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="16670-211">Batching hello inserts in one call significantly increases hello performance over sequential inserts.</span></span>

<span data-ttu-id="16670-212">een opgeslagen procedure tooimprove Hallo vorige voorbeeld bovendien gebruiken in plaats van een opdracht op basis van tekst.</span><span class="sxs-lookup"><span data-stu-id="16670-212">tooimprove hello previous example further, use a stored procedure instead of a text-based command.</span></span> <span data-ttu-id="16670-213">Hallo volgende Transact-SQL-opdracht maakt een opgeslagen procedure waarmee Hallo **SimpleTestTableType** tabelwaardeparameter.</span><span class="sxs-lookup"><span data-stu-id="16670-213">hello following Transact-SQL command creates a stored procedure that takes hello **SimpleTestTableType** table-valued parameter.</span></span>

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

<span data-ttu-id="16670-214">Wijzig de Hallo **SqlCommand** declaratie in Hallo vorige code voorbeeld toohello volgende object.</span><span class="sxs-lookup"><span data-stu-id="16670-214">Then change hello **SqlCommand** object declaration in hello previous code example toohello following.</span></span>

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

<span data-ttu-id="16670-215">In de meeste gevallen hebben table-valued parameters gelijkwaardige of betere prestaties dan andere batchen technieken.</span><span class="sxs-lookup"><span data-stu-id="16670-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span></span> <span data-ttu-id="16670-216">Table-valued parameters zijn vaak beter, omdat ze meer flexibiliteit dan andere opties.</span><span class="sxs-lookup"><span data-stu-id="16670-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span></span> <span data-ttu-id="16670-217">Bijvoorbeeld, staan andere technieken, zoals SQL bulksgewijs kopiëren, alleen de Hallo invoegen van nieuwe rijen.</span><span class="sxs-lookup"><span data-stu-id="16670-217">For example, other techniques, such as SQL bulk copy, only permit hello insertion of new rows.</span></span> <span data-ttu-id="16670-218">Maar met tabelwaarden parameters, kunt u logica in Hallo opgeslagen procedure toodetermine welke rijen updates zijn en die zijn ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="16670-218">But with table-valued parameters, you can use logic in hello stored procedure toodetermine which rows are updates and which are inserts.</span></span> <span data-ttu-id="16670-219">Hallo tabeltype kan ook worden gewijzigd toocontain een 'Bewerking'-kolom waarin wordt aangegeven of Hallo opgegeven rij moet worden ingevoegd, bijgewerkt of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="16670-219">hello table type can also be modified toocontain an “Operation” column that indicates whether hello specified row should be inserted, updated, or deleted.</span></span>

<span data-ttu-id="16670-220">Hallo volgende tabel ziet u de testresultaten ad-hoc voor gebruik van parameters tabelwaarden Hallo in milliseconden.</span><span class="sxs-lookup"><span data-stu-id="16670-220">hello following table shows ad-hoc test results for hello use of table-valued parameters in milliseconds.</span></span>

| <span data-ttu-id="16670-221">Bewerkingen</span><span class="sxs-lookup"><span data-stu-id="16670-221">Operations</span></span> | <span data-ttu-id="16670-222">On-Premises tooAzure (ms)</span><span class="sxs-lookup"><span data-stu-id="16670-222">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="16670-223">Azure hetzelfde datacenter (ms)</span><span class="sxs-lookup"><span data-stu-id="16670-223">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="16670-224">1</span><span class="sxs-lookup"><span data-stu-id="16670-224">1</span></span> |<span data-ttu-id="16670-225">124</span><span class="sxs-lookup"><span data-stu-id="16670-225">124</span></span> |<span data-ttu-id="16670-226">32</span><span class="sxs-lookup"><span data-stu-id="16670-226">32</span></span> |
| <span data-ttu-id="16670-227">10</span><span class="sxs-lookup"><span data-stu-id="16670-227">10</span></span> |<span data-ttu-id="16670-228">131</span><span class="sxs-lookup"><span data-stu-id="16670-228">131</span></span> |<span data-ttu-id="16670-229">25</span><span class="sxs-lookup"><span data-stu-id="16670-229">25</span></span> |
| <span data-ttu-id="16670-230">100</span><span class="sxs-lookup"><span data-stu-id="16670-230">100</span></span> |<span data-ttu-id="16670-231">338</span><span class="sxs-lookup"><span data-stu-id="16670-231">338</span></span> |<span data-ttu-id="16670-232">51</span><span class="sxs-lookup"><span data-stu-id="16670-232">51</span></span> |
| <span data-ttu-id="16670-233">1000</span><span class="sxs-lookup"><span data-stu-id="16670-233">1000</span></span> |<span data-ttu-id="16670-234">2615</span><span class="sxs-lookup"><span data-stu-id="16670-234">2615</span></span> |<span data-ttu-id="16670-235">382</span><span class="sxs-lookup"><span data-stu-id="16670-235">382</span></span> |
| <span data-ttu-id="16670-236">10.000</span><span class="sxs-lookup"><span data-stu-id="16670-236">10000</span></span> |<span data-ttu-id="16670-237">23830</span><span class="sxs-lookup"><span data-stu-id="16670-237">23830</span></span> |<span data-ttu-id="16670-238">3586</span><span class="sxs-lookup"><span data-stu-id="16670-238">3586</span></span> |

> [!NOTE]
> <span data-ttu-id="16670-239">Geen zijn resultaten benchmarks.</span><span class="sxs-lookup"><span data-stu-id="16670-239">Results are not benchmarks.</span></span> <span data-ttu-id="16670-240">Zie Hallo [opmerking over timing resultaten in dit onderwerp](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="16670-240">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="16670-241">Hallo prestatieverbetering van batchverwerking is onmiddellijk zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="16670-241">hello performance gain from batching is immediately apparent.</span></span> <span data-ttu-id="16670-242">In vorige sequentiële test hello, 1000 bewerkingen zijn in 129 seconden buiten Hallo datacenter en 21 seconden uit binnen Hallo datacenter.</span><span class="sxs-lookup"><span data-stu-id="16670-242">In hello previous sequential test, 1000 operations took 129 seconds outside hello datacenter and 21 seconds from within hello datacenter.</span></span> <span data-ttu-id="16670-243">Maar met tabelwaarden parameters 1000 operations alleen 2.6 buiten Hallo datacenter en 0,4 seconden binnen Hallo datacenter.</span><span class="sxs-lookup"><span data-stu-id="16670-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside hello datacenter and 0.4 seconds within hello datacenter.</span></span>

<span data-ttu-id="16670-244">Zie voor meer informatie over table-valued parameters [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="16670-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

### <a name="sql-bulk-copy"></a><span data-ttu-id="16670-245">SQL bulksgewijs kopiëren</span><span class="sxs-lookup"><span data-stu-id="16670-245">SQL bulk copy</span></span>
<span data-ttu-id="16670-246">SQL bulksgewijs kopiëren is een andere manier tooinsert grote hoeveelheden gegevens in een doeldatabase.</span><span class="sxs-lookup"><span data-stu-id="16670-246">SQL bulk copy is another way tooinsert large amounts of data into a target database.</span></span> <span data-ttu-id="16670-247">.NET-toepassingen kunnen gebruikmaken van Hallo **SqlBulkCopy** bewerkingen klasse tooperform bulksgewijs invoegen.</span><span class="sxs-lookup"><span data-stu-id="16670-247">.NET applications can use hello **SqlBulkCopy** class tooperform bulk insert operations.</span></span> <span data-ttu-id="16670-248">**SqlBulkCopy** lijkt in functie toohello opdrachtregelprogramma **Bcp.exe**, of Hallo Transact-SQL-instructie **BULK INSERT**.</span><span class="sxs-lookup"><span data-stu-id="16670-248">**SqlBulkCopy** is similar in function toohello command-line tool, **Bcp.exe**, or hello Transact-SQL statement, **BULK INSERT**.</span></span> <span data-ttu-id="16670-249">Hallo volgende voorbeeldcode laat zien hoe toobulk kopie Hallo rijen in de bron Hallo **DataTable**, tabel, toohello doeltabel in SQL Server, MyTable.</span><span class="sxs-lookup"><span data-stu-id="16670-249">hello following code example shows how toobulk copy hello rows in hello source **DataTable**, table, toohello destination table in SQL Server, MyTable.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

<span data-ttu-id="16670-250">Er zijn enkele gevallen waarbij bulksgewijs kopiëren heeft de voorkeur boven table-valued parameters.</span><span class="sxs-lookup"><span data-stu-id="16670-250">There are some cases where bulk copy is preferred over table-valued parameters.</span></span> <span data-ttu-id="16670-251">Zie Hallo Vergelijkingstabel Table-Valued parameters versus BULK INSERT-bewerkingen in Hallo onderwerp [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="16670-251">See hello comparison table of Table-Valued parameters versus BULK INSERT operations in hello topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

<span data-ttu-id="16670-252">Hallo volgende ad-hoc testresultaten geven Hallo prestaties van batchverwerking met **SqlBulkCopy** in milliseconden.</span><span class="sxs-lookup"><span data-stu-id="16670-252">hello following ad-hoc test results show hello performance of batching with **SqlBulkCopy** in milliseconds.</span></span>

| <span data-ttu-id="16670-253">Bewerkingen</span><span class="sxs-lookup"><span data-stu-id="16670-253">Operations</span></span> | <span data-ttu-id="16670-254">On-Premises tooAzure (ms)</span><span class="sxs-lookup"><span data-stu-id="16670-254">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="16670-255">Azure hetzelfde datacenter (ms)</span><span class="sxs-lookup"><span data-stu-id="16670-255">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="16670-256">1</span><span class="sxs-lookup"><span data-stu-id="16670-256">1</span></span> |<span data-ttu-id="16670-257">433</span><span class="sxs-lookup"><span data-stu-id="16670-257">433</span></span> |<span data-ttu-id="16670-258">57</span><span class="sxs-lookup"><span data-stu-id="16670-258">57</span></span> |
| <span data-ttu-id="16670-259">10</span><span class="sxs-lookup"><span data-stu-id="16670-259">10</span></span> |<span data-ttu-id="16670-260">441</span><span class="sxs-lookup"><span data-stu-id="16670-260">441</span></span> |<span data-ttu-id="16670-261">32</span><span class="sxs-lookup"><span data-stu-id="16670-261">32</span></span> |
| <span data-ttu-id="16670-262">100</span><span class="sxs-lookup"><span data-stu-id="16670-262">100</span></span> |<span data-ttu-id="16670-263">636</span><span class="sxs-lookup"><span data-stu-id="16670-263">636</span></span> |<span data-ttu-id="16670-264">53</span><span class="sxs-lookup"><span data-stu-id="16670-264">53</span></span> |
| <span data-ttu-id="16670-265">1000</span><span class="sxs-lookup"><span data-stu-id="16670-265">1000</span></span> |<span data-ttu-id="16670-266">2535</span><span class="sxs-lookup"><span data-stu-id="16670-266">2535</span></span> |<span data-ttu-id="16670-267">341</span><span class="sxs-lookup"><span data-stu-id="16670-267">341</span></span> |
| <span data-ttu-id="16670-268">10.000</span><span class="sxs-lookup"><span data-stu-id="16670-268">10000</span></span> |<span data-ttu-id="16670-269">21605</span><span class="sxs-lookup"><span data-stu-id="16670-269">21605</span></span> |<span data-ttu-id="16670-270">2737</span><span class="sxs-lookup"><span data-stu-id="16670-270">2737</span></span> |

> [!NOTE]
> <span data-ttu-id="16670-271">Geen zijn resultaten benchmarks.</span><span class="sxs-lookup"><span data-stu-id="16670-271">Results are not benchmarks.</span></span> <span data-ttu-id="16670-272">Zie Hallo [opmerking over timing resultaten in dit onderwerp](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="16670-272">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="16670-273">In kleinere batch Hallo gebruik table-valued parameters ver-loop Hallo **SqlBulkCopy** klasse.</span><span class="sxs-lookup"><span data-stu-id="16670-273">In smaller batch sizes, hello use table-valued parameters outperformed hello **SqlBulkCopy** class.</span></span> <span data-ttu-id="16670-274">Echter, **SqlBulkCopy** 12-31% sneller dan table-valued parameters uitgevoerd voor de tests Hallo van 1000 en 10.000 rijen.</span><span class="sxs-lookup"><span data-stu-id="16670-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for hello tests of 1,000 and 10,000 rows.</span></span> <span data-ttu-id="16670-275">Table-valued parameters, zoals **SqlBulkCopy** is een goede optie voor batch ingevoegd, vooral wanneer vergeleken toohello prestatie van bewerkingen niet batch verwerkt.</span><span class="sxs-lookup"><span data-stu-id="16670-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared toohello performance of non-batched operations.</span></span>

<span data-ttu-id="16670-276">Zie voor meer informatie over bulksgewijs kopiëren in ADO.NET [Bulksgewijze kopieerbewerkingen in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span><span class="sxs-lookup"><span data-stu-id="16670-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span></span>

### <a name="multiple-row-parameterized-insert-statements"></a><span data-ttu-id="16670-277">Meerdere rij geparametriseerde INSERT-instructies</span><span class="sxs-lookup"><span data-stu-id="16670-277">Multiple-row Parameterized INSERT statements</span></span>
<span data-ttu-id="16670-278">Een alternatief voor kleine batches is een grote tooconstruct geparametriseerde INSERT-instructie die meerdere rijen worden ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="16670-278">One alternative for small batches is tooconstruct a large parameterized INSERT statement that inserts multiple rows.</span></span> <span data-ttu-id="16670-279">Hallo volgende codevoorbeeld ziet u deze methode.</span><span class="sxs-lookup"><span data-stu-id="16670-279">hello following code example demonstrates this technique.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


<span data-ttu-id="16670-280">In dit voorbeeld is tooshow hello basisconcept bedoeld.</span><span class="sxs-lookup"><span data-stu-id="16670-280">This example is meant tooshow hello basic concept.</span></span> <span data-ttu-id="16670-281">Een meer realistische scenario zou doorlopen Hallo vereist entiteiten tooconstruct Hallo-queryreeks en Hallo opdrachtparameters tegelijkertijd.</span><span class="sxs-lookup"><span data-stu-id="16670-281">A more realistic scenario would loop through hello required entities tooconstruct hello query string and hello command parameters simultaneously.</span></span> <span data-ttu-id="16670-282">Bent u beperkt tooa totaal van 2100 queryparameters bevatten, zodat dit Hallo kunt u het totale aantal rijen dat kan worden verwerkt op deze manier beperkt.</span><span class="sxs-lookup"><span data-stu-id="16670-282">You are limited tooa total of 2100 query parameters, so this limits hello total number of rows that can be processed in this manner.</span></span>

<span data-ttu-id="16670-283">Hallo na ad-hoc resultaten weergeven Hallo prestaties testen van dit type van de instructie insert in milliseconden.</span><span class="sxs-lookup"><span data-stu-id="16670-283">hello following ad-hoc test results show hello performance of this type of insert statement in milliseconds.</span></span>

| <span data-ttu-id="16670-284">Bewerkingen</span><span class="sxs-lookup"><span data-stu-id="16670-284">Operations</span></span> | <span data-ttu-id="16670-285">Table-valued parameters (ms)</span><span class="sxs-lookup"><span data-stu-id="16670-285">Table-valued parameters (ms)</span></span> | <span data-ttu-id="16670-286">Één instructie INSERT (ms)</span><span class="sxs-lookup"><span data-stu-id="16670-286">Single-statement INSERT (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="16670-287">1</span><span class="sxs-lookup"><span data-stu-id="16670-287">1</span></span> |<span data-ttu-id="16670-288">32</span><span class="sxs-lookup"><span data-stu-id="16670-288">32</span></span> |<span data-ttu-id="16670-289">20</span><span class="sxs-lookup"><span data-stu-id="16670-289">20</span></span> |
| <span data-ttu-id="16670-290">10</span><span class="sxs-lookup"><span data-stu-id="16670-290">10</span></span> |<span data-ttu-id="16670-291">30</span><span class="sxs-lookup"><span data-stu-id="16670-291">30</span></span> |<span data-ttu-id="16670-292">25</span><span class="sxs-lookup"><span data-stu-id="16670-292">25</span></span> |
| <span data-ttu-id="16670-293">100</span><span class="sxs-lookup"><span data-stu-id="16670-293">100</span></span> |<span data-ttu-id="16670-294">33</span><span class="sxs-lookup"><span data-stu-id="16670-294">33</span></span> |<span data-ttu-id="16670-295">51</span><span class="sxs-lookup"><span data-stu-id="16670-295">51</span></span> |

> [!NOTE]
> <span data-ttu-id="16670-296">Geen zijn resultaten benchmarks.</span><span class="sxs-lookup"><span data-stu-id="16670-296">Results are not benchmarks.</span></span> <span data-ttu-id="16670-297">Zie Hallo [opmerking over timing resultaten in dit onderwerp](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="16670-297">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="16670-298">Deze methode kan worden iets snellere voor batches die minder dan 100 rijen zijn.</span><span class="sxs-lookup"><span data-stu-id="16670-298">This approach can be slightly faster for batches that are less than 100 rows.</span></span> <span data-ttu-id="16670-299">Hoewel Hallo verbetering klein is, is deze techniek een andere optie die goed in uw scenario specifieke toepassing werkt mogelijk.</span><span class="sxs-lookup"><span data-stu-id="16670-299">Although hello improvement is small, this technique is another option that might work well in your specific application scenario.</span></span>

### <a name="dataadapter"></a><span data-ttu-id="16670-300">DataAdapter</span><span class="sxs-lookup"><span data-stu-id="16670-300">DataAdapter</span></span>
<span data-ttu-id="16670-301">Hallo **DataAdapter** klasse kunt u toomodify een **gegevensset** object en vervolgens dient Hallo wijzigingen Als INSERT, UPDATE en DELETE-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="16670-301">hello **DataAdapter** class allows you toomodify a **DataSet** object and then submit hello changes as INSERT, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="16670-302">Als u van Hallo gebruikmaakt **DataAdapter** op deze manier is het belangrijk toonote die scheiden oproepen worden gedaan voor elke afzonderlijke bewerking.</span><span class="sxs-lookup"><span data-stu-id="16670-302">If you are using hello **DataAdapter** in this manner, it is important toonote that separate calls are made for each distinct operation.</span></span> <span data-ttu-id="16670-303">tooimprove prestaties, gebruik Hallo **UpdateBatchSize** eigenschap toohello aantal bewerkingen tegelijk in batch moet worden opgenomen.</span><span class="sxs-lookup"><span data-stu-id="16670-303">tooimprove performance, use hello **UpdateBatchSize** property toohello number of operations that should be batched at a time.</span></span> <span data-ttu-id="16670-304">Zie voor meer informatie [uitvoeren van Batch bewerkingen met behulp van DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span><span class="sxs-lookup"><span data-stu-id="16670-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span></span>

### <a name="entity-framework"></a><span data-ttu-id="16670-305">Entity framework</span><span class="sxs-lookup"><span data-stu-id="16670-305">Entity framework</span></span>
<span data-ttu-id="16670-306">Entity Framework ondersteunt momenteel geen batchverwerking.</span><span class="sxs-lookup"><span data-stu-id="16670-306">Entity Framework does not currently support batching.</span></span> <span data-ttu-id="16670-307">Andere ontwikkelaars in Hallo community toodemonstrate oplossingen, zoals een onderdrukking Hallo hebt geprobeerd **SaveChanges** methode.</span><span class="sxs-lookup"><span data-stu-id="16670-307">Different developers in hello community have attempted toodemonstrate workarounds, such as override hello **SaveChanges** method.</span></span> <span data-ttu-id="16670-308">Maar Hallo oplossingen zijn meestal complexe en aangepaste toohello toepassing en gegevensmodel.</span><span class="sxs-lookup"><span data-stu-id="16670-308">But hello solutions are typically complex and customized toohello application and data model.</span></span> <span data-ttu-id="16670-309">Hallo Entity Framework codeplex project heeft momenteel een bespreking van de pagina voor deze functie-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="16670-309">hello Entity Framework codeplex project currently has a discussion page on this feature request.</span></span> <span data-ttu-id="16670-310">tooview deze discussie Zie [ontwerp notulen - 2 augustus 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span><span class="sxs-lookup"><span data-stu-id="16670-310">tooview this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span></span>

### <a name="xml"></a><span data-ttu-id="16670-311">XML</span><span class="sxs-lookup"><span data-stu-id="16670-311">XML</span></span>
<span data-ttu-id="16670-312">Voor de volledigheid, we van mening bent dat deze belangrijk tootalk XML als een batchen strategie.</span><span class="sxs-lookup"><span data-stu-id="16670-312">For completeness, we feel that it is important tootalk about XML as a batching strategy.</span></span> <span data-ttu-id="16670-313">Hallo-gebruik van XML heeft echter geen voordelen ten opzichte van andere methoden en enkele nadelen.</span><span class="sxs-lookup"><span data-stu-id="16670-313">However, hello use of XML has no advantages over other methods and several disadvantages.</span></span> <span data-ttu-id="16670-314">Hallo aanpak is vergelijkbaar tootable-valued parameters, maar een XML-bestand of de tekenreeks wordt doorgegeven tooa opgeslagen procedure in plaats van een gebruiker gedefinieerde tabel.</span><span class="sxs-lookup"><span data-stu-id="16670-314">hello approach is similar tootable-valued parameters, but an XML file or string is passed tooa stored procedure instead of a user-defined table.</span></span> <span data-ttu-id="16670-315">Hallo opgeslagen procedure parseert Hallo opdrachten in Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="16670-315">hello stored procedure parses hello commands in hello stored procedure.</span></span>

<span data-ttu-id="16670-316">Er zijn enkele nadelen toothis benadering:</span><span class="sxs-lookup"><span data-stu-id="16670-316">There are several disadvantages toothis approach:</span></span>

* <span data-ttu-id="16670-317">Werken met XML kan lastig zijn en foutgevoelig.</span><span class="sxs-lookup"><span data-stu-id="16670-317">Working with XML can be cumbersome and error prone.</span></span>
* <span data-ttu-id="16670-318">Bij het parseren Hallo XML op Hallo-database kan CPU-intensief zijn.</span><span class="sxs-lookup"><span data-stu-id="16670-318">Parsing hello XML on hello database can be CPU-intensive.</span></span>
* <span data-ttu-id="16670-319">Deze methode is langzamer dan table-valued parameters in de meeste gevallen.</span><span class="sxs-lookup"><span data-stu-id="16670-319">In most cases, this method is slower than table-valued parameters.</span></span>

<span data-ttu-id="16670-320">Hallo gebruik van XML voor batch-query's is daarom niet aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="16670-320">For these reasons, hello use of XML for batch queries is not recommended.</span></span>

## <a name="batching-considerations"></a><span data-ttu-id="16670-321">Batchverwerking overwegingen</span><span class="sxs-lookup"><span data-stu-id="16670-321">Batching considerations</span></span>
<span data-ttu-id="16670-322">Hallo uit te voeren meer richtlijnen voor het gebruik van de Hallo van batchverwerking in SQL-Database-toepassingen te bieden.</span><span class="sxs-lookup"><span data-stu-id="16670-322">hello following sections provide more guidance for hello use of batching in SQL Database applications.</span></span>

### <a name="tradeoffs"></a><span data-ttu-id="16670-323">Voor-en nadelen</span><span class="sxs-lookup"><span data-stu-id="16670-323">Tradeoffs</span></span>
<span data-ttu-id="16670-324">Afhankelijk van uw architectuur batchverwerking kan betrekking hebben op een afweging tussen de prestaties en tolerantie.</span><span class="sxs-lookup"><span data-stu-id="16670-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span></span> <span data-ttu-id="16670-325">Denk bijvoorbeeld Hallo scenario waar uw rol onverwacht uitvalt.</span><span class="sxs-lookup"><span data-stu-id="16670-325">For example, consider hello scenario where your role unexpectedly goes down.</span></span> <span data-ttu-id="16670-326">Als u één rij met gegevens verliest, is Hallo impact kleiner dan Hallo gevolgen van het verlies van een grote batch van niet-verzonden rijen.</span><span class="sxs-lookup"><span data-stu-id="16670-326">If you lose one row of data, hello impact is smaller than hello impact of losing a large batch of unsubmitted rows.</span></span> <span data-ttu-id="16670-327">Er is een groter risico wanneer u rijen worden gebufferd voordat ze worden verzonden toohello database in een opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="16670-327">There is a greater risk when you buffer rows before sending them toohello database in a specified time window.</span></span>

<span data-ttu-id="16670-328">Vanwege deze afweging evalueren Hallo-type van bewerkingen die u batch.</span><span class="sxs-lookup"><span data-stu-id="16670-328">Because of this tradeoff, evaluate hello type of operations that you batch.</span></span> <span data-ttu-id="16670-329">Batch-agressiever (grotere batches en langer tijdvensters) met gegevens die minder kritiek is.</span><span class="sxs-lookup"><span data-stu-id="16670-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span></span>

### <a name="batch-size"></a><span data-ttu-id="16670-330">Batchgrootte</span><span class="sxs-lookup"><span data-stu-id="16670-330">Batch size</span></span>
<span data-ttu-id="16670-331">In onze tests is er meestal geen voordeel toobreaking grote batches in kleinere reeksen.</span><span class="sxs-lookup"><span data-stu-id="16670-331">In our tests, there was typically no advantage toobreaking large batches into smaller chunks.</span></span> <span data-ttu-id="16670-332">Deze onderverdeling vaak resulteerde in feite in trager dan één grote batch wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="16670-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span></span> <span data-ttu-id="16670-333">Neem bijvoorbeeld een scenario waar u tooinsert 1000 rijen.</span><span class="sxs-lookup"><span data-stu-id="16670-333">For example, consider a scenario where you want tooinsert 1000 rows.</span></span> <span data-ttu-id="16670-334">Hallo volgende tabel ziet u hoe lang duurt het toouse table-valued parameters tooinsert 1000 rijen wanneer onderverdeeld in kleinere batches.</span><span class="sxs-lookup"><span data-stu-id="16670-334">hello following table shows how long it takes toouse table-valued parameters tooinsert 1000 rows when divided into smaller batches.</span></span>

| <span data-ttu-id="16670-335">Batchgrootte</span><span class="sxs-lookup"><span data-stu-id="16670-335">Batch size</span></span> | <span data-ttu-id="16670-336">Herhalingen</span><span class="sxs-lookup"><span data-stu-id="16670-336">Iterations</span></span> | <span data-ttu-id="16670-337">Table-valued parameters (ms)</span><span class="sxs-lookup"><span data-stu-id="16670-337">Table-valued parameters (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="16670-338">1000</span><span class="sxs-lookup"><span data-stu-id="16670-338">1000</span></span> |<span data-ttu-id="16670-339">1</span><span class="sxs-lookup"><span data-stu-id="16670-339">1</span></span> |<span data-ttu-id="16670-340">347</span><span class="sxs-lookup"><span data-stu-id="16670-340">347</span></span> |
| <span data-ttu-id="16670-341">500</span><span class="sxs-lookup"><span data-stu-id="16670-341">500</span></span> |<span data-ttu-id="16670-342">2</span><span class="sxs-lookup"><span data-stu-id="16670-342">2</span></span> |<span data-ttu-id="16670-343">355</span><span class="sxs-lookup"><span data-stu-id="16670-343">355</span></span> |
| <span data-ttu-id="16670-344">100</span><span class="sxs-lookup"><span data-stu-id="16670-344">100</span></span> |<span data-ttu-id="16670-345">10</span><span class="sxs-lookup"><span data-stu-id="16670-345">10</span></span> |<span data-ttu-id="16670-346">465</span><span class="sxs-lookup"><span data-stu-id="16670-346">465</span></span> |
| <span data-ttu-id="16670-347">50</span><span class="sxs-lookup"><span data-stu-id="16670-347">50</span></span> |<span data-ttu-id="16670-348">20</span><span class="sxs-lookup"><span data-stu-id="16670-348">20</span></span> |<span data-ttu-id="16670-349">630</span><span class="sxs-lookup"><span data-stu-id="16670-349">630</span></span> |

> [!NOTE]
> <span data-ttu-id="16670-350">Geen zijn resultaten benchmarks.</span><span class="sxs-lookup"><span data-stu-id="16670-350">Results are not benchmarks.</span></span> <span data-ttu-id="16670-351">Zie Hallo [opmerking over timing resultaten in dit onderwerp](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="16670-351">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="16670-352">U ziet dat de beste prestaties Hallo voor 1000 rijen toosubmit ze in één keer.</span><span class="sxs-lookup"><span data-stu-id="16670-352">You can see that hello best performance for 1000 rows is toosubmit them all at once.</span></span> <span data-ttu-id="16670-353">In andere tests (hier niet weergegeven) is er een kleine prestaties voordeel toobreak een batch 10000 rij in twee batches van 5000.</span><span class="sxs-lookup"><span data-stu-id="16670-353">In other tests (not shown here) there was a small performance gain toobreak a 10000 row batch into two batches of 5000.</span></span> <span data-ttu-id="16670-354">Maar Hallo tabelschema voor deze tests is relatief eenvoudige, dus u moet uitvoeren op getest uw specifieke gegevens en de batch grootten tooverify deze bevindingen.</span><span class="sxs-lookup"><span data-stu-id="16670-354">But hello table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes tooverify these findings.</span></span>

<span data-ttu-id="16670-355">Een andere factor tooconsider is dat als de totale batch Hallo te groot wordt, SQL Database mogelijk beperken en toocommit Hallo batch weigeren.</span><span class="sxs-lookup"><span data-stu-id="16670-355">Another factor tooconsider is that if hello total batch becomes too large, SQL Database might throttle and refuse toocommit hello batch.</span></span> <span data-ttu-id="16670-356">Test voor de beste resultaten Hallo uw specifieke scenario toodetermine als er een ideaal batchgrootte.</span><span class="sxs-lookup"><span data-stu-id="16670-356">For hello best results, test your specific scenario toodetermine if there is an ideal batch size.</span></span> <span data-ttu-id="16670-357">Hallo batchgrootte configureerbaar maken op runtime tooenable snel aanpassingen op basis van prestaties of fouten.</span><span class="sxs-lookup"><span data-stu-id="16670-357">Make hello batch size configurable at runtime tooenable quick adjustments based on performance or errors.</span></span>

<span data-ttu-id="16670-358">Ten slotte Hallo grootte van Hallo batch worden verdeeld met Hallo risico's van batchverwerking.</span><span class="sxs-lookup"><span data-stu-id="16670-358">Finally, balance hello size of hello batch with hello risks associated with batching.</span></span> <span data-ttu-id="16670-359">Als er tijdelijke fouten of Hallo-rol is mislukt, kunt u de Hallo gevolgen van het Hallo opnieuw te proberen of verlies van gegevens in een batch Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="16670-359">If there are transient errors or hello role fails, consider hello consequences of retrying hello operation or of losing hello data in hello batch.</span></span>

### <a name="parallel-processing"></a><span data-ttu-id="16670-360">Parallelle verwerking</span><span class="sxs-lookup"><span data-stu-id="16670-360">Parallel processing</span></span>
<span data-ttu-id="16670-361">Wat gebeurt er als u duurde Hallo benadering Hallo batchgrootte vermindering van maar meerdere threads tooexecute Hallo werk gebruikt?</span><span class="sxs-lookup"><span data-stu-id="16670-361">What if you took hello approach of reducing hello batch size but used multiple threads tooexecute hello work?</span></span> <span data-ttu-id="16670-362">Onze tests bleek opnieuw, of meerdere kleinere multithreaded batches doorgaans uitgevoerd slechter dan één groter batch.</span><span class="sxs-lookup"><span data-stu-id="16670-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span></span> <span data-ttu-id="16670-363">Hallo probeert volgende test tooinsert 1000 rijen in een of meer parallelle batches.</span><span class="sxs-lookup"><span data-stu-id="16670-363">hello following test attempts tooinsert 1000 rows in one or more parallel batches.</span></span> <span data-ttu-id="16670-364">Deze test toont hoe meer gelijktijdige batches daadwerkelijk prestaties verlaagd.</span><span class="sxs-lookup"><span data-stu-id="16670-364">This test shows how more simultaneous batches actually decreased performance.</span></span>

| <span data-ttu-id="16670-365">Batchgrootte [iteraties]</span><span class="sxs-lookup"><span data-stu-id="16670-365">Batch size [Iterations]</span></span> | <span data-ttu-id="16670-366">Twee threads (ms)</span><span class="sxs-lookup"><span data-stu-id="16670-366">Two threads (ms)</span></span> | <span data-ttu-id="16670-367">Vier threads (ms)</span><span class="sxs-lookup"><span data-stu-id="16670-367">Four threads (ms)</span></span> | <span data-ttu-id="16670-368">Zes threads (ms)</span><span class="sxs-lookup"><span data-stu-id="16670-368">Six threads (ms)</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="16670-369">1000 [1]</span><span class="sxs-lookup"><span data-stu-id="16670-369">1000 [1]</span></span> |<span data-ttu-id="16670-370">277</span><span class="sxs-lookup"><span data-stu-id="16670-370">277</span></span> |<span data-ttu-id="16670-371">315</span><span class="sxs-lookup"><span data-stu-id="16670-371">315</span></span> |<span data-ttu-id="16670-372">266</span><span class="sxs-lookup"><span data-stu-id="16670-372">266</span></span> |
| <span data-ttu-id="16670-373">500 [2]</span><span class="sxs-lookup"><span data-stu-id="16670-373">500 [2]</span></span> |<span data-ttu-id="16670-374">548</span><span class="sxs-lookup"><span data-stu-id="16670-374">548</span></span> |<span data-ttu-id="16670-375">278</span><span class="sxs-lookup"><span data-stu-id="16670-375">278</span></span> |<span data-ttu-id="16670-376">256</span><span class="sxs-lookup"><span data-stu-id="16670-376">256</span></span> |
| <span data-ttu-id="16670-377">250 [4]</span><span class="sxs-lookup"><span data-stu-id="16670-377">250 [4]</span></span> |<span data-ttu-id="16670-378">405</span><span class="sxs-lookup"><span data-stu-id="16670-378">405</span></span> |<span data-ttu-id="16670-379">329</span><span class="sxs-lookup"><span data-stu-id="16670-379">329</span></span> |<span data-ttu-id="16670-380">265</span><span class="sxs-lookup"><span data-stu-id="16670-380">265</span></span> |
| <span data-ttu-id="16670-381">100 [10]</span><span class="sxs-lookup"><span data-stu-id="16670-381">100 [10]</span></span> |<span data-ttu-id="16670-382">488</span><span class="sxs-lookup"><span data-stu-id="16670-382">488</span></span> |<span data-ttu-id="16670-383">439</span><span class="sxs-lookup"><span data-stu-id="16670-383">439</span></span> |<span data-ttu-id="16670-384">391</span><span class="sxs-lookup"><span data-stu-id="16670-384">391</span></span> |

> [!NOTE]
> <span data-ttu-id="16670-385">Geen zijn resultaten benchmarks.</span><span class="sxs-lookup"><span data-stu-id="16670-385">Results are not benchmarks.</span></span> <span data-ttu-id="16670-386">Zie Hallo [opmerking over timing resultaten in dit onderwerp](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="16670-386">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="16670-387">Er zijn verschillende mogelijke oorzaken voor Hallo vermindering in prestaties vanwege tooparallelism:</span><span class="sxs-lookup"><span data-stu-id="16670-387">There are several potential reasons for hello degradation in performance due tooparallelism:</span></span>

* <span data-ttu-id="16670-388">Er zijn meerdere gelijktijdige netwerk aanroepen in plaats van een.</span><span class="sxs-lookup"><span data-stu-id="16670-388">There are multiple simultaneous network calls instead of one.</span></span>
* <span data-ttu-id="16670-389">Meerdere bewerkingen op één tabel kunnen leiden tot conflicten en blokkeren.</span><span class="sxs-lookup"><span data-stu-id="16670-389">Multiple operations against a single table can result in contention and blocking.</span></span>
* <span data-ttu-id="16670-390">Er zijn overhead die is gekoppeld aan multithreading.</span><span class="sxs-lookup"><span data-stu-id="16670-390">There are overheads associated with multithreading.</span></span>
* <span data-ttu-id="16670-391">Hallo kosten van meerdere verbindingen belangrijker is dan Hallo voordeel van parallelle verwerking.</span><span class="sxs-lookup"><span data-stu-id="16670-391">hello expense of opening multiple connections outweighs hello benefit of parallel processing.</span></span>

<span data-ttu-id="16670-392">Als u verschillende tabellen of databases als doel, is het mogelijk toosee prestaties krijgen met deze strategie.</span><span class="sxs-lookup"><span data-stu-id="16670-392">If you target different tables or databases, it is possible toosee some performance gain with this strategy.</span></span> <span data-ttu-id="16670-393">Database-sharding of federaties zou een scenario voor deze benadering zijn.</span><span class="sxs-lookup"><span data-stu-id="16670-393">Database sharding or federations would be a scenario for this approach.</span></span> <span data-ttu-id="16670-394">Sharding maakt gebruik van meerdere databases en de andere database tooeach routes.</span><span class="sxs-lookup"><span data-stu-id="16670-394">Sharding uses multiple databases and routes different data tooeach database.</span></span> <span data-ttu-id="16670-395">Als er elke kleine batch tooa andere database, kan vervolgens Hallo bewerkingen uit te voeren parallel efficiënter zijn.</span><span class="sxs-lookup"><span data-stu-id="16670-395">If each small batch is going tooa different database, then performing hello operations in parallel can be more efficient.</span></span> <span data-ttu-id="16670-396">Hallo prestatieverbetering te bereiken is echter niet groot genoeg toouse als Hallo basis voor een sharding besluit toouse database in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="16670-396">However, hello performance gain is not significant enough toouse as hello basis for a decision toouse database sharding in your solution.</span></span>

<span data-ttu-id="16670-397">Parallelle uitvoering van kleinere batches kan in sommige ontwerpen resulteren in betere doorvoer van aanvragen in een systeem wordt belast.</span><span class="sxs-lookup"><span data-stu-id="16670-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span></span> <span data-ttu-id="16670-398">In dit geval, zelfs als het sneller tooprocess één groter batch, verwerking van meerdere batches parallel mogelijk efficiënter.</span><span class="sxs-lookup"><span data-stu-id="16670-398">In this case, even though it is quicker tooprocess a single larger batch, processing multiple batches in parallel might be more efficient.</span></span>

<span data-ttu-id="16670-399">Als u parallelle uitvoering gebruikt, kunt u beheren Hallo maximum aantal werkthreads.</span><span class="sxs-lookup"><span data-stu-id="16670-399">If you do use parallel execution, consider controlling hello maximum number of worker threads.</span></span> <span data-ttu-id="16670-400">Een kleiner getal kan leiden tot minder conflicten en een sneller worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="16670-400">A smaller number might result in less contention and a faster execution time.</span></span> <span data-ttu-id="16670-401">Houd ook rekening met Hallo extra belasting die door dit op Hallo doeldatabase in verbindingen en transacties geplaatst.</span><span class="sxs-lookup"><span data-stu-id="16670-401">Also, consider hello additional load that this places on hello target database both in connections and transactions.</span></span>

### <a name="related-performance-factors"></a><span data-ttu-id="16670-402">Prestaties gerelateerd aan factoren</span><span class="sxs-lookup"><span data-stu-id="16670-402">Related performance factors</span></span>
<span data-ttu-id="16670-403">Typische richtlijnen op de prestaties van de database is ook van invloed op de batchverwerking.</span><span class="sxs-lookup"><span data-stu-id="16670-403">Typical guidance on database performance also affects batching.</span></span> <span data-ttu-id="16670-404">Voeg bijvoorbeeld presteert voor tabellen die een primaire sleutel voor grote of veel niet-geclusterde indexen.</span><span class="sxs-lookup"><span data-stu-id="16670-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span></span>

<span data-ttu-id="16670-405">Als het table-valued parameters een opgeslagen procedure gebruikt, kunt u opdracht Hallo **SET NOCOUNT ON** aan Hallo begin van Hallo procedure.</span><span class="sxs-lookup"><span data-stu-id="16670-405">If table-valued parameters use a stored procedure, you can use hello command **SET NOCOUNT ON** at hello beginning of hello procedure.</span></span> <span data-ttu-id="16670-406">Deze instructie onderdrukt return van het aantal Hallo van invloed op rijen in de procedure Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="16670-406">This statement suppresses hello return of hello count of hello affected rows in hello procedure.</span></span> <span data-ttu-id="16670-407">Hallo echter in onze tests gebruik van **SET NOCOUNT ON** geen invloed heeft ofwel nemen de prestaties af.</span><span class="sxs-lookup"><span data-stu-id="16670-407">However, in our tests, hello use of **SET NOCOUNT ON** either had no effect or decreased performance.</span></span> <span data-ttu-id="16670-408">Hallo opgeslagen testprocedure is heel eenvoudig met één **invoegen** opdracht Hallo tabelwaardeparameter.</span><span class="sxs-lookup"><span data-stu-id="16670-408">hello test stored procedure was simple with a single **INSERT** command from hello table-valued parameter.</span></span> <span data-ttu-id="16670-409">Het is mogelijk dat de complexere opgeslagen procedures van deze instructie profiteren wilt.</span><span class="sxs-lookup"><span data-stu-id="16670-409">It is possible that more complex stored procedures would benefit from this statement.</span></span> <span data-ttu-id="16670-410">Maar niet wordt ervan uitgegaan dat toe te voegen **SET NOCOUNT ON** tooyour opgeslagen procedure automatisch verbetert de prestaties.</span><span class="sxs-lookup"><span data-stu-id="16670-410">But don’t assume that adding **SET NOCOUNT ON** tooyour stored procedure automatically improves performance.</span></span> <span data-ttu-id="16670-411">toounderstand Hallo effect, testen van de opgeslagen procedure met en zonder Hallo **SET NOCOUNT ON** instructie.</span><span class="sxs-lookup"><span data-stu-id="16670-411">toounderstand hello effect, test your stored procedure with and without hello **SET NOCOUNT ON** statement.</span></span>

## <a name="batching-scenarios"></a><span data-ttu-id="16670-412">Batchverwerking scenario 's</span><span class="sxs-lookup"><span data-stu-id="16670-412">Batching scenarios</span></span>
<span data-ttu-id="16670-413">Hallo volgende secties wordt beschreven hoe toouse table-valued parameters in drie scenario's van toepassing.</span><span class="sxs-lookup"><span data-stu-id="16670-413">hello following sections describe how toouse table-valued parameters in three application scenarios.</span></span> <span data-ttu-id="16670-414">Hallo eerste scenario ziet u hoe buffer en batches kunnen samenwerken.</span><span class="sxs-lookup"><span data-stu-id="16670-414">hello first scenario shows how buffering and batching can work together.</span></span> <span data-ttu-id="16670-415">het tweede scenario Hallo verbetert de prestaties door het uitvoeren van de operations master-details in een aanroep van één opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="16670-415">hello second scenario improves performance by performing master-detail operations in a single stored procedure call.</span></span> <span data-ttu-id="16670-416">Hallo laatste scenario toont hoe toouse table-valued parameters in een "UPSERT"-bewerking.</span><span class="sxs-lookup"><span data-stu-id="16670-416">hello final scenario shows how toouse table-valued parameters in an “UPSERT” operation.</span></span>

### <a name="buffering"></a><span data-ttu-id="16670-417">Buffer</span><span class="sxs-lookup"><span data-stu-id="16670-417">Buffering</span></span>
<span data-ttu-id="16670-418">Er zijn enkele scenario's die voor de hand liggende kandidaat voor batchverwerking, zijn er veel scenario's die gebruikmaken van batchverwerking door vertraagde verwerking kunnen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="16670-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span></span> <span data-ttu-id="16670-419">Vertraagde verwerking ook wordt echter een groter risico dat Hallo gegevens gaan in de gebeurtenis Hallo van een onverwachte fout verloren.</span><span class="sxs-lookup"><span data-stu-id="16670-419">However, delayed processing also carries a greater risk that hello data is lost in hello event of an unexpected failure.</span></span> <span data-ttu-id="16670-420">Het is belangrijk toounderstand dit risico en overweeg Hallo gevolgen.</span><span class="sxs-lookup"><span data-stu-id="16670-420">It is important toounderstand this risk and consider hello consequences.</span></span>

<span data-ttu-id="16670-421">Neem bijvoorbeeld een webtoepassing waarmee wordt bijgehouden Hallo navigatiegeschiedenis van elke gebruiker.</span><span class="sxs-lookup"><span data-stu-id="16670-421">For example, consider a web application that tracks hello navigation history of each user.</span></span> <span data-ttu-id="16670-422">Op elke pagina-aanvraag kan de toepassing hello paginaweergave database aanroep toorecord Hallo van een gebruiker maken.</span><span class="sxs-lookup"><span data-stu-id="16670-422">On each page request, hello application could make a database call toorecord hello user’s page view.</span></span> <span data-ttu-id="16670-423">Maar hogere prestaties en schaalbaarheid kunnen worden bereikt door het bufferen Hallo gebruikers navigatie activiteiten en vervolgens deze gegevens toohello database in batches wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="16670-423">But higher performance and scalability can be achieved by buffering hello users’ navigation activities and then sending this data toohello database in batches.</span></span> <span data-ttu-id="16670-424">U kunt Hallo database bijwerken door de verstreken tijd en/of buffergrootte activeren.</span><span class="sxs-lookup"><span data-stu-id="16670-424">You can trigger hello database update by elapsed time and/or buffer size.</span></span> <span data-ttu-id="16670-425">Een regel kan bijvoorbeeld opgeven dat Hallo batch moet worden verwerkt na 20 seconden of wanneer Hallo buffer 1000 objecten bereikt.</span><span class="sxs-lookup"><span data-stu-id="16670-425">For example, a rule could specify that hello batch should be processed after 20 seconds or when hello buffer reaches 1000 items.</span></span>

<span data-ttu-id="16670-426">Hallo volgende codevoorbeeld wordt [reactieve extensies - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess buffer opgeslagen gebeurtenissen die worden gegenereerd door een controleprogramma klasse.</span><span class="sxs-lookup"><span data-stu-id="16670-426">hello following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess buffered events raised by a monitoring class.</span></span> <span data-ttu-id="16670-427">Wanneer Hallo buffer opvulling of er is een time-out is bereikt, Hallo batch van gebruikersgegevens toohello database met een tabelwaardeparameter is verzonden.</span><span class="sxs-lookup"><span data-stu-id="16670-427">When hello buffer fills or a timeout is reached, hello batch of user data is sent toohello database with a table-valued parameter.</span></span>

<span data-ttu-id="16670-428">Hallo volgende NavHistoryData klasse modellen Hallo gebruiker navigatie details.</span><span class="sxs-lookup"><span data-stu-id="16670-428">hello following NavHistoryData class models hello user navigation details.</span></span> <span data-ttu-id="16670-429">Deze bevat algemene informatie, zoals gebruikers-id hello, Hallo URL geopend en Hallo tijd toegang.</span><span class="sxs-lookup"><span data-stu-id="16670-429">It contains basic information such as hello user identifier, hello URL accessed, and hello access time.</span></span>

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

<span data-ttu-id="16670-430">Hallo NavHistoryDataMonitor klasse is verantwoordelijk voor het bufferen Hallo navigatie gegevens toohello gebruikersdatabase.</span><span class="sxs-lookup"><span data-stu-id="16670-430">hello NavHistoryDataMonitor class is responsible for buffering hello user navigation data toohello database.</span></span> <span data-ttu-id="16670-431">Het bevat een methode, RecordUserNavigationEntry die antwoordt door een **OnAdded** gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="16670-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span></span> <span data-ttu-id="16670-432">Hallo volgende code toont Hallo constructor logica die gebruikmaakt van Rx toocreate een waarneembare verzameling op basis van Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="16670-432">hello following code shows hello constructor logic that uses Rx toocreate an observable collection based on hello event.</span></span> <span data-ttu-id="16670-433">Vervolgens worden toothis waarneembare verzameling bijgehouden met Hallo Buffer methode.</span><span class="sxs-lookup"><span data-stu-id="16670-433">It then subscribes toothis observable collection with hello Buffer method.</span></span> <span data-ttu-id="16670-434">Hallo overbelasting geeft dat die buffer Hallo elke 20 seconden of 1000 vermeldingen moet worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="16670-434">hello overload specifies that hello buffer should be sent every 20 seconds or 1000 entries.</span></span>

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

<span data-ttu-id="16670-435">Hallo-handler alle items in de buffer opgeslagen Hallo converteert naar een type tabelwaarden en stuurt vervolgens deze type tooa opgeslagen procedure die processen Hallo batch.</span><span class="sxs-lookup"><span data-stu-id="16670-435">hello handler converts all of hello buffered items into a table-valued type and then passes this type tooa stored procedure that processes hello batch.</span></span> <span data-ttu-id="16670-436">Hallo toont volgende code Hallo volledige definitie voor zowel Hallo NavHistoryDataEventArgs en Hallo NavHistoryDataMonitor klassen.</span><span class="sxs-lookup"><span data-stu-id="16670-436">hello following code shows hello complete definition for both hello NavHistoryDataEventArgs and hello NavHistoryDataMonitor classes.</span></span>

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

<span data-ttu-id="16670-437">toouse deze buffer klasse, Hallo-toepassing maakt een statische NavHistoryDataMonitor-object.</span><span class="sxs-lookup"><span data-stu-id="16670-437">toouse this buffering class, hello application creates a static NavHistoryDataMonitor object.</span></span> <span data-ttu-id="16670-438">Telkens wanneer die een gebruiker toegang krijgt een pagina tot roept Hallo toepassing hello NavHistoryDataMonitor.RecordUserNavigationEntry methode.</span><span class="sxs-lookup"><span data-stu-id="16670-438">Each time a user accesses a page, hello application calls hello NavHistoryDataMonitor.RecordUserNavigationEntry method.</span></span> <span data-ttu-id="16670-439">Hallo buffer logica voortgezet tootake antwoord verzenden van de database van deze vermeldingen toohello in batches.</span><span class="sxs-lookup"><span data-stu-id="16670-439">hello buffering logic proceeds tootake care of sending these entries toohello database in batches.</span></span>

### <a name="master-detail"></a><span data-ttu-id="16670-440">Details van basispagina</span><span class="sxs-lookup"><span data-stu-id="16670-440">Master detail</span></span>
<span data-ttu-id="16670-441">Table-valued parameters zijn handig voor eenvoudige INSERT-scenario's.</span><span class="sxs-lookup"><span data-stu-id="16670-441">Table-valued parameters are useful for simple INSERT scenarios.</span></span> <span data-ttu-id="16670-442">Het kan echter meer lastig toobatch voegt die betrekking hebben op meer dan één tabel zijn.</span><span class="sxs-lookup"><span data-stu-id="16670-442">However, it can be more challenging toobatch inserts that involve more than one table.</span></span> <span data-ttu-id="16670-443">Hallo ' master/detail'-scenario is een goed voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="16670-443">hello “master/detail” scenario is a good example.</span></span> <span data-ttu-id="16670-444">Hallo hoofdtabel identificeert Hallo primaire entiteit.</span><span class="sxs-lookup"><span data-stu-id="16670-444">hello master table identifies hello primary entity.</span></span> <span data-ttu-id="16670-445">Een of meer detailtabellen opslaan meer gegevens over Hallo entiteit.</span><span class="sxs-lookup"><span data-stu-id="16670-445">One or more detail tables store more data about hello entity.</span></span> <span data-ttu-id="16670-446">In dit scenario afdwingen refererende-sleutelrelaties Hallo van details tooa unieke master entiteit.</span><span class="sxs-lookup"><span data-stu-id="16670-446">In this scenario, foreign key relationships enforce hello relationship of details tooa unique master entity.</span></span> <span data-ttu-id="16670-447">U kunt een vereenvoudigde versie van een tabel PurchaseOrder en de bijbehorende OrderDetail-tabel.</span><span class="sxs-lookup"><span data-stu-id="16670-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span></span> <span data-ttu-id="16670-448">Hallo volgende Transact-SQL maakt Hallo PurchaseOrder tabel met vier kolommen: OrderID, OrderDate CustomerID en Status.</span><span class="sxs-lookup"><span data-stu-id="16670-448">hello following Transact-SQL creates hello PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span></span>

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

<span data-ttu-id="16670-449">Elke order bevat een of meer kopen van een product.</span><span class="sxs-lookup"><span data-stu-id="16670-449">Each order contains one or more product purchases.</span></span> <span data-ttu-id="16670-450">Deze informatie wordt vastgelegd in Hallo PurchaseOrderDetail tabel.</span><span class="sxs-lookup"><span data-stu-id="16670-450">This information is captured in hello PurchaseOrderDetail table.</span></span> <span data-ttu-id="16670-451">Hallo volgende Transact-SQL maakt Hallo PurchaseOrderDetail tabel met vijf kolommen: OrderID, OrderDetailID ProductID, UnitPrice en OrderQty.</span><span class="sxs-lookup"><span data-stu-id="16670-451">hello following Transact-SQL creates hello PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span></span>

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

<span data-ttu-id="16670-452">Hallo OrderID kolom in Hallo PurchaseOrderDetail tabel moet verwijzen naar een order uit Hallo PurchaseOrder tabel.</span><span class="sxs-lookup"><span data-stu-id="16670-452">hello OrderID column in hello PurchaseOrderDetail table must reference an order from hello PurchaseOrder table.</span></span> <span data-ttu-id="16670-453">na de definitie van een refererende sleutel Hallo dwingt deze beperking af.</span><span class="sxs-lookup"><span data-stu-id="16670-453">hello following definition of a foreign key enforces this constraint.</span></span>

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

<span data-ttu-id="16670-454">In de volgorde toouse table-valued parameters, moet u een gebruiker gedefinieerde tabeltype voor elke doeltabel hebben.</span><span class="sxs-lookup"><span data-stu-id="16670-454">In order toouse table-valued parameters, you must have one user-defined table type for each target table.</span></span>

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

<span data-ttu-id="16670-455">Vervolgens definieert u een opgeslagen procedure die tabellen van de volgende typen accepteert.</span><span class="sxs-lookup"><span data-stu-id="16670-455">Then define a stored procedure that accepts tables of these types.</span></span> <span data-ttu-id="16670-456">Deze procedure kunt een toepassing toolocally batch de een reeks orders en orderdetails in één aanroep.</span><span class="sxs-lookup"><span data-stu-id="16670-456">This procedure allows an application toolocally batch a set of orders and order details in a single call.</span></span> <span data-ttu-id="16670-457">Hallo biedt volgende Transact-SQL Hallo voltooid opgeslagen procedure-declaratie voor deze aankoop voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="16670-457">hello following Transact-SQL provides hello complete stored procedure declaration for this purchase order example.</span></span>

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

<span data-ttu-id="16670-458">In dit voorbeeld Hallo lokaal gedefinieerde @IdentityLink tabel Hallo werkelijke OrderID waarden uit Hallo zojuist ingevoegd rijen bevat.</span><span class="sxs-lookup"><span data-stu-id="16670-458">In this example, hello locally defined @IdentityLink table stores hello actual OrderID values from hello newly inserted rows.</span></span> <span data-ttu-id="16670-459">Deze volgorde-id's zijn anders dan Hallo tijdelijke OrderID waarden in Hallo @orders en @details table-valued parameters.</span><span class="sxs-lookup"><span data-stu-id="16670-459">These order identifiers are different from hello temporary OrderID values in hello @orders and @details table-valued parameters.</span></span> <span data-ttu-id="16670-460">Om deze reden Hallo @IdentityLink tabel verbindt vervolgens Hallo OrderID waarden uit Hallo @orders toohello echte OrderID parameterwaarden voor nieuwe rijen Hallo in Hallo PurchaseOrder tabel.</span><span class="sxs-lookup"><span data-stu-id="16670-460">For this reason, hello @IdentityLink table then connects hello OrderID values from hello @orders parameter toohello real OrderID values for hello new rows in hello PurchaseOrder table.</span></span> <span data-ttu-id="16670-461">Na deze stap Hallo @IdentityLink tabel invoegen Hallo volgorde details Hello kunt vergemakkelijken werkelijke OrderID die voldoet aan de Hallo foreign key-beperking.</span><span class="sxs-lookup"><span data-stu-id="16670-461">After this step, hello @IdentityLink table can facilitate inserting hello order details with hello actual OrderID that satisfies hello foreign key constraint.</span></span>

<span data-ttu-id="16670-462">Deze opgeslagen procedure kan worden gebruikt vanuit code of van andere Transact-SQL-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="16670-462">This stored procedure can be used from code or from other Transact-SQL calls.</span></span> <span data-ttu-id="16670-463">Zie Hallo table-valued parameters sectie van dit artikel voor een codevoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="16670-463">See hello table-valued parameters section of this paper for a code example.</span></span> <span data-ttu-id="16670-464">Hallo volgende Transact-SQL ziet u hoe toocall sp_InsertOrdersBatch Hallo.</span><span class="sxs-lookup"><span data-stu-id="16670-464">hello following Transact-SQL shows how toocall hello sp_InsertOrdersBatch.</span></span>

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

<span data-ttu-id="16670-465">Deze oplossing kunt elke batch toouse een set waarden OrderID die bij 1 beginnen.</span><span class="sxs-lookup"><span data-stu-id="16670-465">This solution allows each batch toouse a set of OrderID values that begin at 1.</span></span> <span data-ttu-id="16670-466">Deze tijdelijke OrderID waarden Hallo relaties in batch Hallo beschreven, maar Hallo werkelijke OrderID waarden worden bepaald bij Hallo Hallo insert-bewerking.</span><span class="sxs-lookup"><span data-stu-id="16670-466">These temporary OrderID values describe hello relationships in hello batch, but hello actual OrderID values are determined at hello time of hello insert operation.</span></span> <span data-ttu-id="16670-467">U kunt Hallo dezelfde instructies in het vorige voorbeeld Hallo meerdere keren worden uitgevoerd en unieke orders genereren in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="16670-467">You can run hello same statements in hello previous example repeatedly and generate unique orders in hello database.</span></span> <span data-ttu-id="16670-468">Overweeg meer code of database logica waarmee wordt voorkomen dubbele orders dat bij het gebruik van deze techniek batchverwerking om deze reden.</span><span class="sxs-lookup"><span data-stu-id="16670-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span></span>

<span data-ttu-id="16670-469">In dit voorbeeld laat zien dat zelfs complexere databasebewerkingen, zoals operations master-details, kunnen in batch worden opgenomen met tabelwaarden parameters.</span><span class="sxs-lookup"><span data-stu-id="16670-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span></span>

### <a name="upsert"></a><span data-ttu-id="16670-470">UPSERT</span><span class="sxs-lookup"><span data-stu-id="16670-470">UPSERT</span></span>
<span data-ttu-id="16670-471">Een ander batchen scenario omvat het gelijktijdig bijwerken van bestaande rijen en nieuwe rijen invoegen.</span><span class="sxs-lookup"><span data-stu-id="16670-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span></span> <span data-ttu-id="16670-472">Deze bewerking is het soms waarnaar wordt verwezen tooas een "UPSERT" (update + insert)-bewerking.</span><span class="sxs-lookup"><span data-stu-id="16670-472">This operation is sometimes referred tooas an “UPSERT” (update + insert) operation.</span></span> <span data-ttu-id="16670-473">In plaats van afzonderlijke oproepen tooINSERT en bij te werken, is de instructie MERGE Hallo beste geschikt toothis taak.</span><span class="sxs-lookup"><span data-stu-id="16670-473">Rather than making separate calls tooINSERT and UPDATE, hello MERGE statement is best suited toothis task.</span></span> <span data-ttu-id="16670-474">Hallo MERGE-instructie kunt uitvoeren van beide invoegen en updatebewerkingen in één aanroep.</span><span class="sxs-lookup"><span data-stu-id="16670-474">hello MERGE statement can perform both insert and update operations in a single call.</span></span>

<span data-ttu-id="16670-475">Table-valued parameters kunnen worden gebruikt met Hallo MERGE-instructie tooperform updates en toevoegingen.</span><span class="sxs-lookup"><span data-stu-id="16670-475">Table-valued parameters can be used with hello MERGE statement tooperform updates and inserts.</span></span> <span data-ttu-id="16670-476">Neem bijvoorbeeld een vereenvoudigde werknemerstabel met Hallo volgende kolommen: werknemer-id, FirstName, LastName, SocialSecurityNumber:</span><span class="sxs-lookup"><span data-stu-id="16670-476">For example, consider a simplified Employee table that contains hello following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span></span>

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

<span data-ttu-id="16670-477">In dit voorbeeld kunt u Hallo feit die Hallo SocialSecurityNumber unieke tooperform een SAMENVOEGING van meerdere werknemers.</span><span class="sxs-lookup"><span data-stu-id="16670-477">In this example, you can use hello fact that hello SocialSecurityNumber is unique tooperform a MERGE of multiple employees.</span></span> <span data-ttu-id="16670-478">Maak eerst Hallo gebruiker gedefinieerde tabeltype:</span><span class="sxs-lookup"><span data-stu-id="16670-478">First, create hello user-defined table type:</span></span>

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

<span data-ttu-id="16670-479">Vervolgens maakt u een opgeslagen procedure of code schrijven dat maakt gebruik van MERGE-instructie tooperform Hallo update hello en in te voegen.</span><span class="sxs-lookup"><span data-stu-id="16670-479">Next, create a stored procedure or write code that uses hello MERGE statement tooperform hello update and insert.</span></span> <span data-ttu-id="16670-480">Hallo volgende voorbeeld wordt Hallo MERGE-instructie op een tabelwaardeparameter @employees, van het type EmployeeTableType.</span><span class="sxs-lookup"><span data-stu-id="16670-480">hello following example uses hello MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span></span> <span data-ttu-id="16670-481">inhoud van Hallo Hallo @employees tabel worden hier niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="16670-481">hello contents of hello @employees table are not shown here.</span></span>

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

<span data-ttu-id="16670-482">Zie voor meer informatie Hallo documentatie en voorbeelden voor het Hallo MERGE-instructie.</span><span class="sxs-lookup"><span data-stu-id="16670-482">For more information, see hello documentation and examples for hello MERGE statement.</span></span> <span data-ttu-id="16670-483">Hoewel Hallo hetzelfde werk kan worden uitgevoerd in meerdere stappen procedureaanroep met afzonderlijke INSERT- en UPDATE-bewerkingen opgeslagen, is het efficiënter Hallo MERGE-instructie.</span><span class="sxs-lookup"><span data-stu-id="16670-483">Although hello same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, hello MERGE statement is more efficient.</span></span> <span data-ttu-id="16670-484">Databasecode kunt Transact-SQL-aanroepen die gebruikmaken van de instructie MERGE Hallo rechtstreeks zonder twee databaseaanroepen voor INSERT en UPDATE ook opstellen.</span><span class="sxs-lookup"><span data-stu-id="16670-484">Database code can also construct Transact-SQL calls that use hello MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span></span>

## <a name="recommendation-summary"></a><span data-ttu-id="16670-485">Aanbeveling samenvatting</span><span class="sxs-lookup"><span data-stu-id="16670-485">Recommendation summary</span></span>
<span data-ttu-id="16670-486">Hallo bevat volgende lijst een samenvatting van Hallo batchverwerking aanbevelingen in dit onderwerp wordt beschreven:</span><span class="sxs-lookup"><span data-stu-id="16670-486">hello following list provides a summary of hello batching recommendations discussed in this topic:</span></span>

* <span data-ttu-id="16670-487">Buffer en batchverwerking tooincrease Hallo prestaties en schaalbaarheid van SQL Database-toepassingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="16670-487">Use buffering and batching tooincrease hello performance and scalability of SQL Database applications.</span></span>
* <span data-ttu-id="16670-488">Begrijpen Hallo balans vinden tussen batchverwerking/buffer en tolerantie.</span><span class="sxs-lookup"><span data-stu-id="16670-488">Understand hello tradeoffs between batching/buffering and resiliency.</span></span> <span data-ttu-id="16670-489">Tijdens een storing rol Hallo risico van het verlies van een niet-verwerkte batch van essentiële bedrijfsgegevens mogelijk bieden, opwegen tegen Hallo prestatievoordelen van batchverwerking.</span><span class="sxs-lookup"><span data-stu-id="16670-489">During a role failure, hello risk of losing an unprocessed batch of business-critical data might outweigh hello performance benefit of batching.</span></span>
* <span data-ttu-id="16670-490">Poging tookeep alle aanroepen toohello database binnen één datacenter tooreduce latentie.</span><span class="sxs-lookup"><span data-stu-id="16670-490">Attempt tookeep all calls toohello database within a single datacenter tooreduce latency.</span></span>
* <span data-ttu-id="16670-491">Als u een bepaalde batchen techniek, bieden table-valued parameters Hallo optimale prestaties en flexibiliteit.</span><span class="sxs-lookup"><span data-stu-id="16670-491">If you choose a single batching technique, table-valued parameters offer hello best performance and flexibility.</span></span>
* <span data-ttu-id="16670-492">Invoegen van de prestaties voor Hallo snelste, volg deze algemene richtlijnen maar testen van uw scenario:</span><span class="sxs-lookup"><span data-stu-id="16670-492">For hello fastest insert performance, follow these general guidelines but test your scenario:</span></span>
  * <span data-ttu-id="16670-493">Voor < 100 rijen geparametriseerde gebruik één opdracht invoegen.</span><span class="sxs-lookup"><span data-stu-id="16670-493">For < 100 rows, use a single parameterized INSERT command.</span></span>
  * <span data-ttu-id="16670-494">Voor < 1000 rijen, table-valued parameters te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="16670-494">For < 1000 rows, use table-valued parameters.</span></span>
  * <span data-ttu-id="16670-495">Voor > = 1000 rijen, SqlBulkCopy gebruiken.</span><span class="sxs-lookup"><span data-stu-id="16670-495">For >= 1000 rows, use SqlBulkCopy.</span></span>
* <span data-ttu-id="16670-496">Voor bijwerken en verwijderen van bewerkingen, table-valued parameters gebruiken met opgeslagen procedure logica die de juiste werking Hallo voor elke rij in de Hallo tabel parameter bepaalt.</span><span class="sxs-lookup"><span data-stu-id="16670-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines hello correct operation on each row in hello table parameter.</span></span>
* <span data-ttu-id="16670-497">Richtlijnen voor batch grootte:</span><span class="sxs-lookup"><span data-stu-id="16670-497">Batch size guidelines:</span></span>
  * <span data-ttu-id="16670-498">Gebruik het grootste batch grootten hello, die geschikt zijn voor uw toepassing en de zakelijke vereisten.</span><span class="sxs-lookup"><span data-stu-id="16670-498">Use hello largest batch sizes that make sense for your application and business requirements.</span></span>
  * <span data-ttu-id="16670-499">Saldo Hallo prestaties krijgen van grote batches met Hallo risico's van tijdelijke of onherstelbare fouten.</span><span class="sxs-lookup"><span data-stu-id="16670-499">Balance hello performance gain of large batches with hello risks of temporary or catastrophic failures.</span></span> <span data-ttu-id="16670-500">Wat is Hallo gevolg pogingen of verlies van gegevens in een batch Hallo Hallo?</span><span class="sxs-lookup"><span data-stu-id="16670-500">What is hello consequence of retries or loss of hello data in hello batch?</span></span> 
  * <span data-ttu-id="16670-501">Test Hallo grootste batch grootte tooverify dat SQL-Database komt niet afwijzen.</span><span class="sxs-lookup"><span data-stu-id="16670-501">Test hello largest batch size tooverify that SQL Database does not reject it.</span></span>
  * <span data-ttu-id="16670-502">Configuratie-instellingen maken dat beheer batches, zoals batchgrootte Hallo of Hallo buffering tijdvenster.</span><span class="sxs-lookup"><span data-stu-id="16670-502">Create configuration settings that control batching, such as hello batch size or hello buffering time window.</span></span> <span data-ttu-id="16670-503">Deze instellingen bieden flexibiliteit.</span><span class="sxs-lookup"><span data-stu-id="16670-503">These settings provide flexibility.</span></span> <span data-ttu-id="16670-504">Hallo gedrag in productie batchverwerking zonder Hallo cloud-service opnieuw te implementeren, kunt u wijzigen.</span><span class="sxs-lookup"><span data-stu-id="16670-504">You can change hello batching behavior in production without redeploying hello cloud service.</span></span>
* <span data-ttu-id="16670-505">Vermijd parallelle uitvoering van batches die worden uitgevoerd op één tabel in een database.</span><span class="sxs-lookup"><span data-stu-id="16670-505">Avoid parallel execution of batches that operate on a single table in one database.</span></span> <span data-ttu-id="16670-506">Als u toodivide één batch tussen meerdere worker threads kiest, voert u tests toodetermine Hallo ideaal aantal threads.</span><span class="sxs-lookup"><span data-stu-id="16670-506">If you do choose toodivide a single batch across multiple worker threads, run tests toodetermine hello ideal number of threads.</span></span> <span data-ttu-id="16670-507">Na een niet-opgegeven drempelwaarde meer threads worden de prestaties verminderen, in plaats van verhogen.</span><span class="sxs-lookup"><span data-stu-id="16670-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span></span>
* <span data-ttu-id="16670-508">Overweeg het bufferen van grootte en de tijd bij wijze van het implementeren van batchverwerking voor scenario's met meer.</span><span class="sxs-lookup"><span data-stu-id="16670-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16670-509">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="16670-509">Next steps</span></span>
<span data-ttu-id="16670-510">In dit artikel gericht op het ontwerpen van databases en het coderen van technieken relatie toobatching kunt verbeteren de prestaties en schaalbaarheid.</span><span class="sxs-lookup"><span data-stu-id="16670-510">This article focused on how database design and coding techniques related toobatching can improve your application performance and scalability.</span></span> <span data-ttu-id="16670-511">Maar dit is slechts één factor in uw algehele beveiligingsstrategie.</span><span class="sxs-lookup"><span data-stu-id="16670-511">But this is just one factor in your overall strategy.</span></span> <span data-ttu-id="16670-512">Zie voor meer manieren tooimprove prestaties en schaalbaarheid [richtlijnen voor Azure SQL Database-prestaties voor individuele databases](sql-database-performance-guidance.md) en [prijs- en Prestatieoverwegingen voor een elastische pool](sql-database-elastic-pool-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="16670-512">For more ways tooimprove performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool-guidance.md).</span></span>

