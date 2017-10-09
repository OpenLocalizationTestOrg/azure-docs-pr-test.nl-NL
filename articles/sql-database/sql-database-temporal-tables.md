---
title: aaaGetting gestart met de tijdelijke tabellen in Azure SQL Database | Microsoft Docs
description: Meer informatie over hoe tooget gestart met het gebruik van tijdelijke tabellen in Azure SQL Database.
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: c8c0f232-0751-4a7f-a36e-67a0b29fa1b8
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 01/10/2017
ms.author: bonova
ms.openlocfilehash: 54f394b51df07aa2f9bb299f207e692171d23479
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a><span data-ttu-id="19db9-103">Aan de slag met tijdelijke tabellen in Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="19db9-103">Getting Started with Temporal Tables in Azure SQL Database</span></span>
<span data-ttu-id="19db9-104">Tijdelijke tabellen zijn een nieuwe programmeerbaarheidsfunctie van Azure SQL Database waarmee u tootrack en volledige geschiedenis van wijzigingen in uw gegevens, zonder dat nodig is voor het coderen van aangepaste Hallo Hallo analyseren.</span><span class="sxs-lookup"><span data-stu-id="19db9-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you tootrack and analyze hello full history of changes in your data, without hello need for custom coding.</span></span> <span data-ttu-id="19db9-105">Tijdelijke tabellen Houd nauw verwante tootime gegevenscontext zodat opgeslagen facts kunnen worden geïnterpreteerd als geldig alleen binnen een bepaalde periode Hallo.</span><span class="sxs-lookup"><span data-stu-id="19db9-105">Temporal Tables keep data closely related tootime context so that stored facts can be interpreted as valid only within hello specific period.</span></span> <span data-ttu-id="19db9-106">Deze eigenschap van tijdelijke tabellen maakt efficiënte analyse op basis van tijd en ophalen inzicht in gegevens ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="19db9-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span></span>

## <a name="temporal-scenario"></a><span data-ttu-id="19db9-107">Tijdelijke Scenario</span><span class="sxs-lookup"><span data-stu-id="19db9-107">Temporal Scenario</span></span>
<span data-ttu-id="19db9-108">In dit artikel ziet u Hallo stappen tooutilize tijdelijke tabellen in een toepassingsscenario.</span><span class="sxs-lookup"><span data-stu-id="19db9-108">This article illustrates hello steps tooutilize Temporal Tables in an application scenario.</span></span> <span data-ttu-id="19db9-109">Stel dat u wilt dat tootrack gebruikersactiviteit op een nieuwe website die wordt ontwikkeld vanaf het begin of op een bestaande website die u tooextend met gebruiker activiteit analytics wilt.</span><span class="sxs-lookup"><span data-stu-id="19db9-109">Suppose that you want tootrack user activity on a new website that is being developed from scratch or on an existing website that you want tooextend with user activity analytics.</span></span> <span data-ttu-id="19db9-110">In dit eenvoudige voorbeeld gaan we ervan uit dat Hallo aantal bezochte webpagina's in een periode is een indicator die behoeften toobe vastgelegd en bewaakt in Hallo website-database die wordt gehost op Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="19db9-110">In this simplified example, we assume that hello number of visited web pages during a period of time is an indicator that needs toobe captured and monitored in hello website database that is hosted on Azure SQL Database.</span></span> <span data-ttu-id="19db9-111">Hallo-doel van historische analyse van gebruikersactiviteit Hallo tooget invoer tooredesign website is en bieden betere ervaring voor Hallo bezoekers.</span><span class="sxs-lookup"><span data-stu-id="19db9-111">hello goal of hello historical analysis of user activity is tooget inputs tooredesign website and provide better experience for hello visitors.</span></span>

<span data-ttu-id="19db9-112">Hallo databasemodel voor dit scenario is zeer eenvoudig - gebruiker activiteit metriek wordt weergegeven met een enkele gehele-veld **PageVisited**, en samen met basisinformatie over Hallo gebruikersprofiel wordt vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="19db9-112">hello database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on hello user profile.</span></span> <span data-ttu-id="19db9-113">Bovendien voor op basis van de analyse houdt u een reeks rijen voor elke gebruiker, waarbij elke rij Hallo-nummer van een bepaalde gebruiker binnen een bepaalde periode bezochte pagina's vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="19db9-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents hello number of pages a particular user visited within a specific period of time.</span></span>

![Schema](./media/sql-database-temporal-tables/AzureTemporal1.png)

<span data-ttu-id="19db9-115">Gelukkig hoeft u geen tooput moeite in uw app toomaintain deze activiteit informatie.</span><span class="sxs-lookup"><span data-stu-id="19db9-115">Fortunately, you do not need tooput any effort in your app toomaintain this activity information.</span></span> <span data-ttu-id="19db9-116">Dit proces is met tijdelijke tabellen geautomatiseerd - zodat u de volledige flexibiliteit tijdens het websiteontwerp en meer tijd toofocus op Hallo gegevensanalyse zelf.</span><span class="sxs-lookup"><span data-stu-id="19db9-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time toofocus on hello data analysis itself.</span></span> <span data-ttu-id="19db9-117">Hallo alleen dat u toodo hoeft tooensure is die **WebSiteInfo** tabel is geconfigureerd als [tijdelijke systeemversietabellen](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="19db9-117">hello only thing you have toodo is tooensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span></span> <span data-ttu-id="19db9-118">Hallo exacte stappen tooutilize tijdelijke tabellen in dit scenario worden hieronder beschreven.</span><span class="sxs-lookup"><span data-stu-id="19db9-118">hello exact steps tooutilize Temporal Tables in this scenario are described below.</span></span>

## <a name="step-1-configure-tables-as-temporal"></a><span data-ttu-id="19db9-119">Stap 1: Tabellen als tijdelijke configureren</span><span class="sxs-lookup"><span data-stu-id="19db9-119">Step 1: Configure tables as temporal</span></span>
<span data-ttu-id="19db9-120">Afhankelijk van of u vanaf de ontwikkeling van nieuwe of bestaande toepassing te upgraden, wordt u tijdelijke tabellen maken of bestaande wijzigen door tijdelijke kenmerken toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="19db9-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span></span> <span data-ttu-id="19db9-121">In het algemeen geval uw scenario is een combinatie van deze twee opties.</span><span class="sxs-lookup"><span data-stu-id="19db9-121">In general case, your scenario can be a mix of these two options.</span></span> <span data-ttu-id="19db9-122">Voer deze actie met behulp van [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS) [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) of een ander Transact-SQL-ontwikkeling-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="19db9-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19db9-123">Het verdient aanbeveling dat u altijd hello gebruiken meest recente versie van Management Studio tooremain gesynchroniseerd met updates tooMicrosoft Azure en SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="19db9-123">It is recommended that you always use hello latest version of Management Studio tooremain synchronized with updates tooMicrosoft Azure and SQL Database.</span></span> <span data-ttu-id="19db9-124">[SQL Server Management Studio bijwerken](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="19db9-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="create-new-table"></a><span data-ttu-id="19db9-125">Nieuwe tabel maken</span><span class="sxs-lookup"><span data-stu-id="19db9-125">Create new table</span></span>
<span data-ttu-id="19db9-126">Contextmenuoptie 'Nieuwe Systeemversietabel' in SSMS Object Explorer tooopen Hallo query-editor gebruiken met een tijdelijke tabel sjabloonscript en vervolgens 'Geef waarden voor Sjabloonparameters' (Ctrl + Shift + M) toopopulate Hallo sjabloon gebruiken:</span><span class="sxs-lookup"><span data-stu-id="19db9-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer tooopen hello query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) toopopulate hello template:</span></span>

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

<span data-ttu-id="19db9-128">In SSDT, gekozen voor de sjabloon 'Tijdelijke tabel (Systeemversietabellen)' wanneer nieuwe items toohello databaseproject toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="19db9-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items toohello database project.</span></span> <span data-ttu-id="19db9-129">Dat wordt geopend tabelontwerp en schakel u tooeasily opgeven Hallo tabelindeling:</span><span class="sxs-lookup"><span data-stu-id="19db9-129">That will open table designer and enable you tooeasily specify hello table layout:</span></span>

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

<span data-ttu-id="19db9-131">U kunt ook een tijdelijke tabel maken door op te geven Hallo Transact-SQL-instructies rechtstreeks, zoals weergegeven in Hallo voorbeeld hieronder.</span><span class="sxs-lookup"><span data-stu-id="19db9-131">You can also a create temporal table by specifying hello Transact-SQL statements directly, as shown in hello example below.</span></span> <span data-ttu-id="19db9-132">Houd er rekening mee dat Hallo verplichte elementen van elke tijdelijke tabel zijn Hallo periodedefinitie en Hallo SYSTEM_VERSIONING-component met een verwijzing tooanother gebruikerstabel die historische rij upversies:</span><span class="sxs-lookup"><span data-stu-id="19db9-132">Note that hello mandatory elements of every temporal table are hello PERIOD definition and hello SYSTEM_VERSIONING clause with a reference tooanother user table that will store historical row versions:</span></span>

````
CREATE TABLE WebsiteUserInfo 
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED 
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL 
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
````

<span data-ttu-id="19db9-133">Wanneer u de tijdelijke systeemversietabel maakt, wordt automatisch Hallo bijbehorende geschiedenistabel met Hallo standaardconfiguratie gemaakt.</span><span class="sxs-lookup"><span data-stu-id="19db9-133">When you create system-versioned temporal table, hello accompanying history table with hello default configuration is automatically created.</span></span> <span data-ttu-id="19db9-134">Hallo standaard geschiedenistabel bevat een geclusterde B-tree-index op Hallo periodekolommen (einde start) met pagina compressie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="19db9-134">hello default history table contains a clustered B-tree index on hello period columns (end, start) with page compression enabled.</span></span> <span data-ttu-id="19db9-135">Deze configuratie is optimaal is voor de meeste Hallo van scenario's waarin tijdelijke tabellen worden gebruikt, met name voor [gegevens controle](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="19db9-135">This configuration is optimal for hello majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span></span> 

<span data-ttu-id="19db9-136">In dit geval streven we ernaar tooperform op basis van tijd trendanalyse gedurende een langere gegevensgeschiedenis en met grotere gegevenssets, dus Hallo opslag keuze voor de geschiedenistabel Hallo een geclusterde columnstore-index is.</span><span class="sxs-lookup"><span data-stu-id="19db9-136">In this particular case, we aim tooperform time-based trend analysis over a longer data history and with bigger data sets, so hello storage choice for hello history table is a clustered columnstore index.</span></span> <span data-ttu-id="19db9-137">Een geclusterde columnstore biedt zeer goede compressie en prestaties voor analytische query's.</span><span class="sxs-lookup"><span data-stu-id="19db9-137">A clustered columnstore provides very good compression and performance for analytical queries.</span></span> <span data-ttu-id="19db9-138">Tijdelijke tabellen geven u flexibiliteit tooconfigure indexen op Hallo Hallo volledig onafhankelijk van huidige en de tijdelijke tabellen.</span><span class="sxs-lookup"><span data-stu-id="19db9-138">Temporal Tables give you hello flexibility tooconfigure indexes on hello current and temporal tables completely independently.</span></span> 

> [!NOTE]
> <span data-ttu-id="19db9-139">Columnstore-indexen zijn alleen beschikbaar in Hallo premium servicecategorie.</span><span class="sxs-lookup"><span data-stu-id="19db9-139">Columnstore indexes are only available in hello premium service tier.</span></span>
>

<span data-ttu-id="19db9-140">Hallo script volgen ziet u hoe Standaardindex voor geschiedenistabel gewijzigde toohello geclusterde columnstore kan zijn:</span><span class="sxs-lookup"><span data-stu-id="19db9-140">hello following script shows how default index on history table can be changed toohello clustered columnstore:</span></span>

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

<span data-ttu-id="19db9-141">Tijdelijke tabellen worden weergegeven in Hallo Object Explorer met de specifieke pictogram hello om gemakkelijker te identificeren, terwijl de geschiedenistabel wordt weergegeven als een onderliggend knooppunt.</span><span class="sxs-lookup"><span data-stu-id="19db9-141">Temporal Tables are represented in hello Object Explorer with hello specific icon for easier identification, while its history table is displayed as a child node.</span></span>

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a><span data-ttu-id="19db9-143">Bestaande tabel tootemporal wijzigen</span><span class="sxs-lookup"><span data-stu-id="19db9-143">Alter existing table tootemporal</span></span>
<span data-ttu-id="19db9-144">We hebben betrekking op Hallo alternatieve scenario in welke Hallo WebsiteUserInfo tabel al bestaat, maar is niet ontworpen tookeep een geschiedenis van wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="19db9-144">Let’s cover hello alternative scenario in which hello WebsiteUserInfo table already exists, but was not designed tookeep a history of changes.</span></span> <span data-ttu-id="19db9-145">In dit geval kunt u eenvoudig hello bestaande tabel toobecome tijdelijke, zoals weergegeven in het volgende voorbeeld Hallo uitbreiden:</span><span class="sxs-lookup"><span data-stu-id="19db9-145">In this case, you can simply extend hello existing table toobecome temporal, as shown in hello following example:</span></span>

````
ALTER TABLE WebsiteUserInfo 
ADD 
    ValidFrom datetime2 (0) GENERATED ALWAYS AS ROW START HIDDEN  
        constraint DF_ValidFrom DEFAULT DATEADD(SECOND, -1, SYSUTCDATETIME())
    , ValidTo datetime2 (0)  GENERATED ALWAYS AS ROW END HIDDEN   
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo); 

ALTER TABLE WebsiteUserInfo  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

## <a name="step-2-run-your-workload-regularly"></a><span data-ttu-id="19db9-146">Stap 2: Uw werkbelasting regelmatig wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="19db9-146">Step 2: Run your workload regularly</span></span>
<span data-ttu-id="19db9-147">Hallo belangrijkste voordeel van tijdelijke tabellen is dat u niet toochange moet of aanpassen van uw website in een manier tooperform bijhouden.</span><span class="sxs-lookup"><span data-stu-id="19db9-147">hello main advantage of Temporal Tables is that you do not need toochange or adjust your website in any way tooperform change tracking.</span></span> <span data-ttu-id="19db9-148">Zodra gemaakt, behouden voor tijdelijke tabellen transparant eerdere versies van de rij telkens wanneer u de wijzigingen op uw gegevens uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="19db9-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span></span> 

<span data-ttu-id="19db9-149">In de volgorde tooleverage automatische bijhouden voor dit scenario, gaan we zojuist bijwerken kolom **PagesVisited** telkens wanneer de gebruiker installatieserver sessie op Hallo website wordt:</span><span class="sxs-lookup"><span data-stu-id="19db9-149">In order tooleverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on hello website:</span></span>

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

<span data-ttu-id="19db9-150">Het is belangrijk toonotice die update query Hallo hoeft niet tooknow Hallo precieze tijd wanneer de huidige bewerking Hallo opgetreden of hoe u historische gegevens blijven behouden voor toekomstige analyse.</span><span class="sxs-lookup"><span data-stu-id="19db9-150">It is important toonotice that hello update query doesn’t need tooknow hello exact time when hello actual operation occurred nor how historical data will be preserved for future analysis.</span></span> <span data-ttu-id="19db9-151">Beide aspecten worden automatisch afgehandeld door hello Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="19db9-151">Both aspects are automatically handled by hello Azure SQL Database.</span></span> <span data-ttu-id="19db9-152">Hallo volgende diagram illustreert hoe gegevens van geschiedenis van elke update wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="19db9-152">hello following diagram illustrates how history data is being generated on every update.</span></span>

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a><span data-ttu-id="19db9-154">Stap 3: Analyse van de historische gegevens</span><span class="sxs-lookup"><span data-stu-id="19db9-154">Step 3: Perform historical data analysis</span></span>
<span data-ttu-id="19db9-155">Als tijdelijke systeemsamenstelling is ingeschakeld, is analyse van historische gegevens nu slechts één query weg van u.</span><span class="sxs-lookup"><span data-stu-id="19db9-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span></span> <span data-ttu-id="19db9-156">In dit artikel wordt we enkele voorbeelden voor het oplossen van algemene analysis scenario's - toolearn alle gegevens verstrekken, verschillende opties die zijn geïntroduceerd in Hallo verkennen [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) component.</span><span class="sxs-lookup"><span data-stu-id="19db9-156">In this article, we will provide a few examples that address common analysis scenarios - toolearn all details, explore various options introduced with hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span></span>

<span data-ttu-id="19db9-157">toosee hello bovenste 10 gebruikers gesorteerd op Hallo aantal bezochte webpagina's vanaf een uur geleden, voer deze query uit:</span><span class="sxs-lookup"><span data-stu-id="19db9-157">toosee hello top 10 users ordered by hello number of visited web pages as of an hour ago, run this query:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

<span data-ttu-id="19db9-158">U kunt eenvoudig deze query wijzigen tooanalyze Hallo site bezoeken vanaf een dag geleden, een maand geleden of op elk punt in de afgelopen Hallo die u wenst.</span><span class="sxs-lookup"><span data-stu-id="19db9-158">You can easily modify this query tooanalyze hello site visits as of a day ago, a month ago or at any point in hello past you wish.</span></span>

<span data-ttu-id="19db9-159">tooperform elementaire statistische analyse voor Hallo vorige dag, gebruikt u Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="19db9-159">tooperform basic statistical analysis for hello previous day, use hello following example:</span></span>

````
DECLARE @twoDaysAgo datetime2 = DATEADD(DAY, -2, SYSUTCDATETIME());
DECLARE @aDayAgo datetime2 = DATEADD(DAY, -1, SYSUTCDATETIME());

SELECT UserID, SUM (PagesVisited) as TotalVisitedPages, AVG (PagesVisited) as AverageVisitedPages,
MAX (PagesVisited) AS MaxVisitedPages, MIN (PagesVisited) AS MinVisitedPages,
STDEV (PagesVisited) as StDevViistedPages
FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME BETWEEN @twoDaysAgo AND @aDayAgo
GROUP BY UserId
````

<span data-ttu-id="19db9-160">toosearch voor activiteiten van een specifieke gebruiker binnen een periode, gebruik Hallo ingesloten component:</span><span class="sxs-lookup"><span data-stu-id="19db9-160">toosearch for activities of a specific user, within a period of time, use hello CONTAINED IN clause:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

<span data-ttu-id="19db9-161">Grafische visualisatie is vooral handig voor tijdelijke query's, zoals u trends en gebruikspatronen in een intuïtieve manier heel eenvoudig weergeven kunt:</span><span class="sxs-lookup"><span data-stu-id="19db9-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span></span>

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a><span data-ttu-id="19db9-163">Zich ontwikkelende tabelschema</span><span class="sxs-lookup"><span data-stu-id="19db9-163">Evolving table schema</span></span>
<span data-ttu-id="19db9-164">Normaal gesproken moet u toochange Hallo tijdelijke tabelschema terwijl u ontwikkeling van apps.</span><span class="sxs-lookup"><span data-stu-id="19db9-164">Typically, you will need toochange hello temporal table schema while you are doing app development.</span></span> <span data-ttu-id="19db9-165">Voor die, voert u eenvoudigweg reguliere ALTER TABLE-instructies en Azure SQL Database worden op de juiste wijze wijzigingen toohello geschiedenistabel doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="19db9-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes toohello history table.</span></span> <span data-ttu-id="19db9-166">Hallo volgende script toont hoe u extra kenmerk voor bijhouden kunt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="19db9-166">hello following script shows how you can add additional attribute for tracking:</span></span>

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

<span data-ttu-id="19db9-167">Op deze manier kunt u de definitie van kolom wijzigen terwijl uw werkbelasting actief is:</span><span class="sxs-lookup"><span data-stu-id="19db9-167">Similarly, you can change column definition while your workload is active:</span></span>

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

<span data-ttu-id="19db9-168">Ten slotte kunt u een kolom die u niet meer nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="19db9-168">Finally, you can remove a column that you do not need anymore.</span></span>

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

<span data-ttu-id="19db9-169">Of gebruik de meest recente [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange tijdelijke tabel schema terwijl u bent verbonden toohello database (onlinemodus) of als onderdeel van het databaseproject hello (offlinemodus).</span><span class="sxs-lookup"><span data-stu-id="19db9-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange temporal table schema while you are connected toohello database (online mode) or as part of hello database project (offline mode).</span></span>

## <a name="controlling-retention-of-historical-data"></a><span data-ttu-id="19db9-170">Bewaren van historische gegevens beheren</span><span class="sxs-lookup"><span data-stu-id="19db9-170">Controlling retention of historical data</span></span>
<span data-ttu-id="19db9-171">Met tijdelijke systeemversietabellen, kan het verhogen van geschiedenistabel Hallo Hallo databasegrootte is meer dan gewone tabellen.</span><span class="sxs-lookup"><span data-stu-id="19db9-171">With system-versioned temporal tables, hello history table may increase hello database size more than regular tables.</span></span> <span data-ttu-id="19db9-172">Een grote en voortdurend groeiende geschiedenistabel kan een probleem die beide vanwege toopure opslagkosten, evenals een prestaties opleggen belasting op het tijdelijke uitvoeren van query's vormen.</span><span class="sxs-lookup"><span data-stu-id="19db9-172">A large and ever-growing history table can become an issue both due toopure storage costs as well as imposing a performance tax on temporal querying.</span></span> <span data-ttu-id="19db9-173">Daarom is ontwikkelen van een bewaarbeleid voor gegevens voor het beheren van gegevens in de geschiedenistabel Hallo een belangrijk aspect van het plannen en beheren van Hallo levenscyclus van elke tijdelijke tabel.</span><span class="sxs-lookup"><span data-stu-id="19db9-173">Hence, developing a data retention policy for managing data in hello history table is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="19db9-174">Met Azure SQL Database hebt u de volgende methoden voor het beheren van historische gegevens in de tijdelijke tabel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="19db9-174">With Azure SQL Database, you have hello following approaches for managing historical data in hello temporal table:</span></span>

* [<span data-ttu-id="19db9-175">Partitioneren van tabel</span><span class="sxs-lookup"><span data-stu-id="19db9-175">Table Partitioning</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [<span data-ttu-id="19db9-176">Script voor aangepaste opschoning</span><span class="sxs-lookup"><span data-stu-id="19db9-176">Custom Cleanup Script</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a><span data-ttu-id="19db9-177">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="19db9-177">Next steps</span></span>
<span data-ttu-id="19db9-178">Bekijk voor meer informatie over tijdelijke tabellen [MSDN-documentatie](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="19db9-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>
<span data-ttu-id="19db9-179">Bezoek Channel 9 toohear een [echte klant tijdelijke implementatie Succesverhaal](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) en bekijk een [tijdelijke demonstratie live](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="19db9-179">Visit Channel 9 toohear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

