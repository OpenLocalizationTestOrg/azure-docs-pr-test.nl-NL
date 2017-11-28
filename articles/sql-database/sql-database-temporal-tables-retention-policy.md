---
title: historische gegevens aaaManage in tijdelijke tabellen met bewaarbeleid | Microsoft Docs
description: Meer informatie over hoe toouse tijdelijke bewaren beleid tookeep historische gegevens onder uw beheer.
services: sql-database
documentationcenter: 
author: bonova
manager: drasumic
editor: 
ms.assetid: 76cfa06a-e758-453e-942c-9f1ed6a38c2a
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 10/12/2016
ms.author: bonova
ms.openlocfilehash: a72a6111a6cd7322d734d08bf3852e95f5ffea8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a><span data-ttu-id="a1508-103">Historische gegevens in tijdelijke tabellen met bewaarbeleid beheren</span><span class="sxs-lookup"><span data-stu-id="a1508-103">Manage historical data in Temporal Tables with retention policy</span></span>
<span data-ttu-id="a1508-104">Tijdelijke tabellen wordt mogelijk uitgebreid grootte van de database meer dan gewone tabellen, met name als u historische gegevens voor een langere periode behouden.</span><span class="sxs-lookup"><span data-stu-id="a1508-104">Temporal Tables may increase database size more than regular tables, especially if you retain historical data for a longer period of time.</span></span> <span data-ttu-id="a1508-105">Bewaarbeleid voor historische gegevens is daarom een belangrijk aspect van het plannen en beheren van Hallo levenscyclus van elke tijdelijke tabel.</span><span class="sxs-lookup"><span data-stu-id="a1508-105">Hence, retention policy for historical data is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="a1508-106">Tijdelijke tabellen in Azure SQL Database worden geleverd met eenvoudig te gebruiken bewaren mechanisme waarmee u deze taak.</span><span class="sxs-lookup"><span data-stu-id="a1508-106">Temporal Tables in Azure SQL Database come with easy-to-use retention mechanism that helps you accomplish this task.</span></span>

<span data-ttu-id="a1508-107">Bewaren van de tijdelijke geschiedenistabel kan worden geconfigureerd op Hallo afzonderlijke tabelniveau, waarmee gebruikers toocreate flexibele veroudering beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="a1508-107">Temporal history retention can be configured at hello individual table level, which allows users toocreate flexible aging polices.</span></span> <span data-ttu-id="a1508-108">Toepassen van de tijdelijke bewaarperiode is eenvoudig: slechts één parameter toobe ingesteld tijdens het maken of schema wijzigen van de tabel is vereist.</span><span class="sxs-lookup"><span data-stu-id="a1508-108">Applying temporal retention is simple: it requires only one parameter toobe set during table creation or schema change.</span></span>

<span data-ttu-id="a1508-109">Nadat u een bewaarbeleid gedefinieerd, start Azure SQL Database regelmatig te controleren of er zijn historische rijen die in aanmerking voor automatische opruimen komen.</span><span class="sxs-lookup"><span data-stu-id="a1508-109">After you define retention policy, Azure SQL Database starts checking regularly if there are historical rows that are eligible for automatic data cleanup.</span></span> <span data-ttu-id="a1508-110">Identificatie van de overeenkomende rijen en de verwijdering van Hallo geschiedenistabel optreden transparant, Hallo achtergrondtaak die is gepland en uitgevoerd door Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="a1508-110">Identification of matching rows and their removal from hello history table occur transparently, in hello background task that is scheduled and run by hello system.</span></span> <span data-ttu-id="a1508-111">Leeftijdsvoorwaarde voor tabelrijen Hallo-geschiedenis is ingeschakeld op basis van het einde van de SYSTEM_TIME-periode voor Hallo-kolom.</span><span class="sxs-lookup"><span data-stu-id="a1508-111">Age condition for hello history table rows is checked based on hello column representing end of SYSTEM_TIME period.</span></span> <span data-ttu-id="a1508-112">Als de bewaarperiode, bijvoorbeeld toosix is ingesteld maanden, tabelrijen in aanmerking komen voor het opruimen Hallo volgende voorwaarde voldoen:</span><span class="sxs-lookup"><span data-stu-id="a1508-112">If retention period, for example, is set toosix months, table rows eligible for cleanup satisfy hello following condition:</span></span>

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

<span data-ttu-id="a1508-113">In Hallo voorgaande voorbeeld, wordt ervan uitgegaan dat die **ValidTo** kolom komt overeen toohello einde van de SYSTEM_TIME-periode.</span><span class="sxs-lookup"><span data-stu-id="a1508-113">In hello preceding example, we assumed that **ValidTo** column corresponds toohello end of SYSTEM_TIME period.</span></span>

## <a name="how-tooconfigure-retention-policy"></a><span data-ttu-id="a1508-114">Hoe het bewaarbeleid tooconfigure?</span><span class="sxs-lookup"><span data-stu-id="a1508-114">How tooconfigure retention policy?</span></span>
<span data-ttu-id="a1508-115">Voordat u een bewaarbeleid voor een tijdelijke tabel configureert, Controleer eerst of tijdelijke historische bewaarperiode is ingeschakeld *op databaseniveau Hallo*.</span><span class="sxs-lookup"><span data-stu-id="a1508-115">Before you configure retention policy for a temporal table, check first whether temporal historical retention is enabled *at hello database level*.</span></span>

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

<span data-ttu-id="a1508-116">Vlag database **is_temporal_history_retention_enabled** set tooON standaard is, maar gebruikers kunnen worden wijzigen met de instructie ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="a1508-116">Database flag **is_temporal_history_retention_enabled** is set tooON by default, but users can change it with ALTER DATABASE statement.</span></span> <span data-ttu-id="a1508-117">Het is ook automatisch set tooOFF na [wijst naar een bepaald tijstip](sql-database-recovery-using-backups.md) bewerking.</span><span class="sxs-lookup"><span data-stu-id="a1508-117">It is also automatically set tooOFF after [point in time restore](sql-database-recovery-using-backups.md) operation.</span></span> <span data-ttu-id="a1508-118">tooenable tijdelijke geschiedenistabel bewaren opschonen voor uw database uitvoeren Hallo-instructie:</span><span class="sxs-lookup"><span data-stu-id="a1508-118">tooenable temporal history retention cleanup for your database, execute hello following statement:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> <span data-ttu-id="a1508-119">U kunt de bewaarperiode voor tijdelijke tabellen, zelfs als configureren **is_temporal_history_retention_enabled** is uitgeschakeld, maar automatisch opschonen voor verouderde rijen niet in dat geval wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="a1508-119">You can configure retention for temporal tables even if **is_temporal_history_retention_enabled** is OFF, but automatic cleanup for aged rows is not triggered in that case.</span></span>
> 
> 

<span data-ttu-id="a1508-120">Bewaarbeleid is tijdens maken van de tabel geconfigureerd door de waarde voor Hallo HISTORY_RETENTION_PERIOD parameter:</span><span class="sxs-lookup"><span data-stu-id="a1508-120">Retention policy is configured during table creation by specifying value for hello HISTORY_RETENTION_PERIOD parameter:</span></span>

````
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
````

<span data-ttu-id="a1508-121">Azure SQL Database kunt u de bewaarperiode toospecify met behulp van verschillende tijdseenheden: dagen, weken, maanden en jaren.</span><span class="sxs-lookup"><span data-stu-id="a1508-121">Azure SQL Database allows you toospecify retention period by using different time units: DAYS, WEEKS, MONTHS, and YEARS.</span></span> <span data-ttu-id="a1508-122">Als HISTORY_RETENTION_PERIOD wordt weggelaten, wordt oneindige bewaren verondersteld.</span><span class="sxs-lookup"><span data-stu-id="a1508-122">If HISTORY_RETENTION_PERIOD is omitted, INFINITE retention is assumed.</span></span> <span data-ttu-id="a1508-123">U kunt ook expliciet oneindige sleutelwoord gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a1508-123">You can also use INFINITE keyword explicitly.</span></span>

<span data-ttu-id="a1508-124">In sommige scenario's, kunt u tooconfigure retentie na het maken van de tabel of toochange eerder geconfigureerde waarde.</span><span class="sxs-lookup"><span data-stu-id="a1508-124">In some scenarios, you may want tooconfigure retention after table creation, or toochange previously configured value.</span></span> <span data-ttu-id="a1508-125">In dat geval gebruikt u ALTER TABLE-instructie:</span><span class="sxs-lookup"><span data-stu-id="a1508-125">In that case use ALTER TABLE statement:</span></span>

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> <span data-ttu-id="a1508-126">Instellen van SYSTEM_VERSIONING tooOFF *blijven niet behouden* periodewaarde bewaren.</span><span class="sxs-lookup"><span data-stu-id="a1508-126">Setting SYSTEM_VERSIONING tooOFF *does not preserve* retention period value.</span></span> <span data-ttu-id="a1508-127">Instellen van SYSTEM_VERSIONING tooON zonder HISTORY_RETENTION_PERIOD expliciet opgegeven resultaten in Hallo oneindige bewaarperiode.</span><span class="sxs-lookup"><span data-stu-id="a1508-127">Setting SYSTEM_VERSIONING tooON without HISTORY_RETENTION_PERIOD specified explicitly results in hello INFINITE retention period.</span></span>
> 
> 

<span data-ttu-id="a1508-128">tooreview huidige status van het bewaarbeleid hello, gebruik Hallo volgende query die markering joins tijdelijke bewaren inschakelen op databaseniveau Hallo met bewaartermijnen voor afzonderlijke tabellen:</span><span class="sxs-lookup"><span data-stu-id="a1508-128">tooreview current state of hello retention policy, use hello following query that joins temporal retention enablement flag at hello database level with retention periods for individual tables:</span></span>

````
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
````


## <a name="how-sql-database-deletes-aged-rows"></a><span data-ttu-id="a1508-129">Hoe SQL-Database worden verwijderd, verouderde rijen?</span><span class="sxs-lookup"><span data-stu-id="a1508-129">How SQL Database deletes aged rows?</span></span>
<span data-ttu-id="a1508-130">Hallo opruimproces is afhankelijk van Hallo index lay-out van Hallo geschiedenistabel.</span><span class="sxs-lookup"><span data-stu-id="a1508-130">hello cleanup process depends on hello index layout of hello history table.</span></span> <span data-ttu-id="a1508-131">Het is belangrijk toonotice die *slechts geschiedenis tabellen met een geclusterde index (B-tree of columnstore) kunnen niet-oneindig bewaarbeleid geconfigureerd*.</span><span class="sxs-lookup"><span data-stu-id="a1508-131">It is important toonotice that *only history tables with a clustered index (B-tree or columnstore) can have finite retention policy configured*.</span></span> <span data-ttu-id="a1508-132">Een achtergrondtaak tooperform verouderde gegevens wissen voor alle tijdelijke tabellen met beperkte bewaarperiode gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a1508-132">A background task is created tooperform aged data cleanup for all temporal tables with finite retention period.</span></span>
<span data-ttu-id="a1508-133">Opschonen logica voor Hallo rowstore (B-tree) geclusterde index verwijdert de verouderde rij in kleinere reeksen (omhoog too10K) voor het minimaliseren van zware belasting op het databaselogboek en i/o-subsysteem.</span><span class="sxs-lookup"><span data-stu-id="a1508-133">Cleanup logic for hello rowstore (B-tree) clustered index deletes aged row in smaller chunks (up too10K) minimizing pressure on database log and I/O subsystem.</span></span> <span data-ttu-id="a1508-134">Hoewel maakt gebruik van opschonen logica vereist B-tree-index, ordenen van verwijderingen voor Hallo rijen die ouder zijn dan de bewaarperiode kan niet goed kan worden gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="a1508-134">Although cleanup logic utilizes required B-tree index, order of deletions for hello rows older than retention period cannot be firmly guaranteed.</span></span> <span data-ttu-id="a1508-135">Daarom *eventuele afhankelijkheden worden pas van kracht op Hallo opschonen volgorde in uw toepassingen*.</span><span class="sxs-lookup"><span data-stu-id="a1508-135">Hence, *do not take any dependency on hello cleanup order in your applications*.</span></span>

<span data-ttu-id="a1508-136">Hallo Hallo geclusterde columnstore-opschoontaak verwijdert gehele [rij groepen](https://msdn.microsoft.com/library/gg492088.aspx) tegelijk (doorgaans bevatten 1 miljoen rijen elke), die zeer efficiënte, vooral wanneer u historische gegevens in een hoog tempo wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="a1508-136">hello cleanup task for hello clustered columnstore removes entire [row groups](https://msdn.microsoft.com/library/gg492088.aspx) at once (typically contain 1 million of rows each), which is very efficient, especially when historical data is generated at a high pace.</span></span>

![De geclusterde columnstore-bewaren](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

<span data-ttu-id="a1508-138">Uitstekend gegevenscompressie en efficiënte bewaren opschonen wordt geclusterde columnstore-index een ideale keuze voor scenario's wanneer uw werkbelasting snel hoge mate van historische gegevens genereert.</span><span class="sxs-lookup"><span data-stu-id="a1508-138">Excellent data compression and efficient retention cleanup makes clustered columnstore index a perfect choice for scenarios when your workload rapidly generates high amount of historical data.</span></span> <span data-ttu-id="a1508-139">Dit patroon is Typerend voor intensieve [transactionele verwerking werkbelastingen die gebruikmaken van tijdelijke tabellen](https://msdn.microsoft.com/library/mt631669.aspx) voor wijzigingen bijhouden en controle, trendanalyse of IoT gegevensopname.</span><span class="sxs-lookup"><span data-stu-id="a1508-139">That pattern is typical for intensive [transactional processing workloads that use temporal tables](https://msdn.microsoft.com/library/mt631669.aspx) for change tracking and auditing, trend analysis, or IoT data ingestion.</span></span>

## <a name="index-considerations"></a><span data-ttu-id="a1508-140">Overwegingen voor index</span><span class="sxs-lookup"><span data-stu-id="a1508-140">Index considerations</span></span>
<span data-ttu-id="a1508-141">Hallo-opschoontaak voor tabellen met de geclusterde index rowstore vereist index toostart met Hallo kolom bijbehorende Hallo einde van de SYSTEM_TIME-periode.</span><span class="sxs-lookup"><span data-stu-id="a1508-141">hello cleanup task for tables with rowstore clustered index requires index toostart with hello column corresponding hello end of SYSTEM_TIME period.</span></span> <span data-ttu-id="a1508-142">Als de index niet bestaat, kunt u een eindige bewaarperiode niet configureren:</span><span class="sxs-lookup"><span data-stu-id="a1508-142">If such index doesn't exist, you cannot configure a finite retention period:</span></span>

<span data-ttu-id="a1508-143">*Bericht 13765, 16 niveau 1 staat <br> </br> op de tijdelijke systeemversietabel 'temporalstagetestdb.dbo.WebsiteUserInfo' eindig bewaarperiode instellen is mislukt omdat de geschiedenistabel Hallo ' temporalstagetestdb.dbo.WebsiteUserInfoHistory' bevat geen vereiste geclusterde index. Houd rekening met het maken van een geclusterde columnstore of B-tree-index die begint met Hallo-kolom die overeenkomt met het einde van de SYSTEM_TIME period op Hallo geschiedenistabel.*</span><span class="sxs-lookup"><span data-stu-id="a1508-143">*Msg 13765, Level 16, State 1 <br></br> Setting finite retention period failed on system-versioned temporal table 'temporalstagetestdb.dbo.WebsiteUserInfo' because hello history table 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' does not contain required clustered index. Consider creating a clustered columnstore or B-tree index starting with hello column that matches end of SYSTEM_TIME period, on hello history table.*</span></span>

<span data-ttu-id="a1508-144">Het is belangrijk toonotice die standaard geschiedenistabel gemaakt met Azure SQL Database al Hallo bevat geclusterde index, die voldoen aan de voorwaarden bewaarbeleid.</span><span class="sxs-lookup"><span data-stu-id="a1508-144">It is important toonotice that hello default history table created by Azure SQL Database already has clustered index, which is compliant for retention policy.</span></span> <span data-ttu-id="a1508-145">Als u tooremove die index in een tabel met beperkte bewaarperiode probeert, mislukt de bewerking met de volgende fout Hallo:</span><span class="sxs-lookup"><span data-stu-id="a1508-145">If you try tooremove that index on a table with finite retention period, operation fails with hello following error:</span></span>

<span data-ttu-id="a1508-146">*Bericht 13766, 16 niveau 1 staat <br> </br> kan Hallo geclusterde index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' niet verwijderen omdat deze wordt gebruikt voor het automatisch opschonen van verouderde gegevens. Overweeg instelling HISTORY_RETENTION_PERIOD tooINFINITE op Hallo overeenkomstige tijdelijke systeemversietabel als u deze index toodrop nodig.*</span><span class="sxs-lookup"><span data-stu-id="a1508-146">*Msg 13766, Level 16, State 1 <br></br> Cannot drop hello clustered index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' because it is being used for automatic cleanup of aged data. Consider setting HISTORY_RETENTION_PERIOD tooINFINITE on hello corresponding system-versioned temporal table if you need toodrop this index.*</span></span>

<span data-ttu-id="a1508-147">Opruimen op Hallo geclusterde columnstore-index werkt optimaal als historische rijen worden ingevoegd in oplopende volgorde (geordend door Hallo van periodekolom), die altijd Hallo geval is wanneer Hallo geschiedenistabel is gevuld uitsluitend door Hallo SYSTEM_ Hallo VERSIONIOING-mechanisme.</span><span class="sxs-lookup"><span data-stu-id="a1508-147">Cleanup on hello clustered columnstore index works optimally if historical rows are inserted in hello ascending order (ordered by hello end of period column), which is always hello case when hello history table is populated exclusively by hello SYSTEM_VERSIONIOING mechanism.</span></span> <span data-ttu-id="a1508-148">Als de rijen in de geschiedenistabel Hallo niet besteld door het einde van de periodekolom (die mogelijk Hallo geval als u bestaande historische gegevens hebt gemigreerd), moet u opnieuw boven op B-tree rowstore-index die is goed besteld tooachieve optimale geclusterde columnstore-index maken de prestaties.</span><span class="sxs-lookup"><span data-stu-id="a1508-148">If rows in hello history table are not ordered by end of period column (which may be hello case if you migrated existing historical data), you should re-create clustered columnstore index on top of B-tree rowstore index that is properly ordered, tooachieve optimal performance.</span></span>

<span data-ttu-id="a1508-149">Vermijd opnieuw opbouwen van de geclusterde columnstore-index in de geschiedenistabel Hallo met Hallo eindig bewaarperiode, omdat het mogelijk gewijzigd bestellen in Rijgroepen Hallo natuurlijk die zijn opgelegd door Hallo versiebeheer door het systeem bewerking.</span><span class="sxs-lookup"><span data-stu-id="a1508-149">Avoid rebuilding clustered columnstore index on hello history table with hello finite retention period, because it may change ordering in hello row groups naturally imposed by hello system-versioning operation.</span></span> <span data-ttu-id="a1508-150">Als u nodig hebt toorebuild geclusterde columnstore-index in de geschiedenistabel Hallo, dit doen door opnieuw boven op compatibele B-tree-index, behouden in Hallo rowgroups nodig zijn voor reguliere opruimen ordening te maken.</span><span class="sxs-lookup"><span data-stu-id="a1508-150">If you need toorebuild clustered columnstore index on hello history table, do that by re-creating it on top of compliant B-tree index, preserving ordering in hello rowgroups necessary for regular data cleanup.</span></span> <span data-ttu-id="a1508-151">Hallo dezelfde manier moet worden uitgevoerd als u de tijdelijke tabel maken met bestaande geschiedenistabel die kolomindex zonder gegarandeerde gegevensvolgorde geclusterde bevat:</span><span class="sxs-lookup"><span data-stu-id="a1508-151">hello same approach should be taken if you create temporal table with existing history table that has clustered column index without guaranteed data order:</span></span>

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

<span data-ttu-id="a1508-152">Wanneer beperkte bewaarperiode is geconfigureerd voor de geschiedenistabel Hallo met Hallo geclusterde columnstore-index, kunt u geen extra niet-geclusterde B-tree indexen op tabel maken:</span><span class="sxs-lookup"><span data-stu-id="a1508-152">When finite retention period is configured for hello history table with hello clustered columnstore index, you cannot create additional non-clustered B-tree indexes on that table:</span></span>

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

<span data-ttu-id="a1508-153">Een poging tooexecute boven de instructie is mislukt met de volgende fout Hallo:</span><span class="sxs-lookup"><span data-stu-id="a1508-153">An attempt tooexecute above statement fails with hello following error:</span></span>

<span data-ttu-id="a1508-154">*Bericht 13772, 16 niveau 1 staat <br> </br> kan niet-geclusterde index maken op een tijdelijke geschiedenistabel 'WebsiteUserInfoHistory' omdat er beperkte bewaarperiode en de geclusterde columnstore-index die zijn gedefinieerd.*</span><span class="sxs-lookup"><span data-stu-id="a1508-154">*Msg 13772, Level 16, State 1 <br></br> Cannot create non-clustered index on a temporal history table 'WebsiteUserInfoHistory' since it has finite retention period and clustered columnstore index defined.*</span></span>

## <a name="querying-tables-with-retention-policy"></a><span data-ttu-id="a1508-155">Opvragen van tabellen met bewaarbeleid</span><span class="sxs-lookup"><span data-stu-id="a1508-155">Querying tables with retention policy</span></span>
<span data-ttu-id="a1508-156">Alle query's op de tijdelijke tabel Hallo automatisch historische rijen die overeenkomt met beperkte bewaarbeleid, tooavoid onvoorspelbare en inconsistente resultaten omdat verouderde rijen kunnen worden verwijderd door het Hallo-opschoontaak filteren *op elk punt in tijd en in willekeurige volgorde*.</span><span class="sxs-lookup"><span data-stu-id="a1508-156">All queries on hello temporal table automatically filter out historical rows matching finite retention policy, tooavoid unpredictable and inconsistent results, since aged rows can be deleted by hello cleanup task, *at any point in time and in arbitrary order*.</span></span>

<span data-ttu-id="a1508-157">Hallo volgende afbeelding ziet u het queryplan Hallo voor een eenvoudige query:</span><span class="sxs-lookup"><span data-stu-id="a1508-157">hello following picture shows hello query plan for a simple query:</span></span>

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

<span data-ttu-id="a1508-158">Hallo query plan omvat extra filter toegepast tooend van periodekolom (ValidTo) in de geclusterde Index scannen operator Hallo op Hallo geschiedenistabel (gemarkeerd).</span><span class="sxs-lookup"><span data-stu-id="a1508-158">hello query plan includes additional filter applied tooend of period column (ValidTo) in hello Clustered Index Scan operator on hello history table (highlighted).</span></span> <span data-ttu-id="a1508-159">In dit voorbeeld wordt ervan uitgegaan dat één maand bewaarperiode is ingesteld op WebsiteUserInfo tabel.</span><span class="sxs-lookup"><span data-stu-id="a1508-159">This example assumes that one MONTH retention period was set on WebsiteUserInfo table.</span></span>

![Queryfilter bewaren](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

<span data-ttu-id="a1508-161">Echter, als u rechtstreeks query geschiedenistabel uitvoert, ziet u mogelijk rijen die ouder dan de opgegeven bewaartermijn tijdsperiode, maar zonder een garantie voor herhaalbare queryresultaten zijn.</span><span class="sxs-lookup"><span data-stu-id="a1508-161">However, if you query history table directly, you may see rows that are older than specified retention period, but without any guarantee for repeatable query results.</span></span> <span data-ttu-id="a1508-162">Hallo volgende afbeelding ziet u query uitvoeringsplan voor Hallo query op Hallo geschiedenistabel zonder aanvullende filters zijn toegepast:</span><span class="sxs-lookup"><span data-stu-id="a1508-162">hello following picture shows query execution plan for hello query on hello history table without additional filters applied:</span></span>

![Geschiedenis zonder bewaren filter opvragen](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

<span data-ttu-id="a1508-164">Vertrouw niet uw bedrijfslogica op de geschiedenistabel buiten de bewaarperiode lezen als u krijgt u mogelijk inconsistente of onverwachte resultaten.</span><span class="sxs-lookup"><span data-stu-id="a1508-164">Do not rely your business logic on reading history table beyond retention period as you may get inconsistent or unexpected results.</span></span> <span data-ttu-id="a1508-165">U wordt aangeraden tijdelijke query's te gebruiken met FOR SYSTEM_TIME-component voor het analyseren van gegevens in tijdelijke tabellen.</span><span class="sxs-lookup"><span data-stu-id="a1508-165">We recommend that you use temporal queries with FOR SYSTEM_TIME clause for analyzing data in temporal tables.</span></span>

## <a name="point-in-time-restore-considerations"></a><span data-ttu-id="a1508-166">Punt in tijd terugzetten overwegingen</span><span class="sxs-lookup"><span data-stu-id="a1508-166">Point in time restore considerations</span></span>
<span data-ttu-id="a1508-167">Wanneer u een nieuwe database door maakt [herstellen van de bestaande database tooa bepaald punt in tijd](sql-database-recovery-using-backups.md), heeft tijdelijke bewaren op databaseniveau Hallo uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a1508-167">When you create new database by [restoring existing database tooa specific point in time](sql-database-recovery-using-backups.md), it has temporal retention disabled at hello database level.</span></span> <span data-ttu-id="a1508-168">(**is_temporal_history_retention_enabled** vlag ingesteld tooOFF).</span><span class="sxs-lookup"><span data-stu-id="a1508-168">(**is_temporal_history_retention_enabled** flag set tooOFF).</span></span> <span data-ttu-id="a1508-169">Deze functie kunt u alle historische rijen bij het herstellen zonder dat u die rijen verouderde worden verwijderd voordat u een tooquery tooexamine ze.</span><span class="sxs-lookup"><span data-stu-id="a1508-169">This functionality allows you tooexamine all historical rows upon restore, without worrying that aged rows are removed before you get tooquery them.</span></span> <span data-ttu-id="a1508-170">U kunt deze ook gebruiken*inspecteren van historische gegevens buiten de geconfigureerde bewaarperiode*.</span><span class="sxs-lookup"><span data-stu-id="a1508-170">You can use it too*inspect historical data beyond configured retention period*.</span></span>

<span data-ttu-id="a1508-171">Stel dat een tijdelijke tabel die een maand bewaren opgegeven tijdsperiode heeft.</span><span class="sxs-lookup"><span data-stu-id="a1508-171">Say that a temporal table has one MONTH retention period specified.</span></span> <span data-ttu-id="a1508-172">Als uw database is gemaakt in de laag Premium-Service, zou u kunnen toocreate databasekopie met Hallo databasestatus too35 dagen terug in de afgelopen Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="a1508-172">If your database was created in Premium Service tier, you would be able toocreate database copy with hello database state up too35 days back in hello past.</span></span> <span data-ttu-id="a1508-173">Die effectief kunt u tooanalyze historische rijen die actief too65 dagen oud zijn rechtstreeks een query uitgevoerd op Hallo geschiedenistabel.</span><span class="sxs-lookup"><span data-stu-id="a1508-173">That effectively would allow you tooanalyze historical rows that are up too65 days old by querying hello history table directly.</span></span>

<span data-ttu-id="a1508-174">Als u opruimen van de tijdelijke bewaren tooactivate wilt, Voer Hallo volgende Transact-SQL-instructie na punt naar een bepaald tijstip:</span><span class="sxs-lookup"><span data-stu-id="a1508-174">If you want tooactivate temporal retention cleanup, run hello following Transact-SQL statement after point in time restore:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a><span data-ttu-id="a1508-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a1508-175">Next steps</span></span>
<span data-ttu-id="a1508-176">hoe toouse tijdelijke tabellen in uw toepassingen uitchecken toolearn [aan de slag met tijdelijke tabellen in Azure SQL Database](sql-database-temporal-tables.md).</span><span class="sxs-lookup"><span data-stu-id="a1508-176">toolearn how toouse Temporal Tables in your applications, check out [Getting Started with Temporal Tables in Azure SQL Database](sql-database-temporal-tables.md).</span></span>

<span data-ttu-id="a1508-177">Bezoek Channel 9 toohear een [echte klant tijdelijke implementatie Succesverhaal](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) en bekijk een [tijdelijke demonstratie live](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="a1508-177">Visit Channel 9 toohear a [real customer temporal implementation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

<span data-ttu-id="a1508-178">Raadpleeg voor gedetailleerde informatie over tijdelijke tabellen [MSDN-documentatie](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="a1508-178">For detailed information about Temporal Tables, review [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>

