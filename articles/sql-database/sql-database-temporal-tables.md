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
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a>Aan de slag met tijdelijke tabellen in Azure SQL Database
Tijdelijke tabellen zijn een nieuwe programmeerbaarheidsfunctie van Azure SQL Database waarmee u tootrack en volledige geschiedenis van wijzigingen in uw gegevens, zonder dat nodig is voor het coderen van aangepaste Hallo Hallo analyseren. Tijdelijke tabellen Houd nauw verwante tootime gegevenscontext zodat opgeslagen facts kunnen worden geïnterpreteerd als geldig alleen binnen een bepaalde periode Hallo. Deze eigenschap van tijdelijke tabellen maakt efficiënte analyse op basis van tijd en ophalen inzicht in gegevens ontwikkeling.

## <a name="temporal-scenario"></a>Tijdelijke Scenario
In dit artikel ziet u Hallo stappen tooutilize tijdelijke tabellen in een toepassingsscenario. Stel dat u wilt dat tootrack gebruikersactiviteit op een nieuwe website die wordt ontwikkeld vanaf het begin of op een bestaande website die u tooextend met gebruiker activiteit analytics wilt. In dit eenvoudige voorbeeld gaan we ervan uit dat Hallo aantal bezochte webpagina's in een periode is een indicator die behoeften toobe vastgelegd en bewaakt in Hallo website-database die wordt gehost op Azure SQL Database. Hallo-doel van historische analyse van gebruikersactiviteit Hallo tooget invoer tooredesign website is en bieden betere ervaring voor Hallo bezoekers.

Hallo databasemodel voor dit scenario is zeer eenvoudig - gebruiker activiteit metriek wordt weergegeven met een enkele gehele-veld **PageVisited**, en samen met basisinformatie over Hallo gebruikersprofiel wordt vastgelegd. Bovendien voor op basis van de analyse houdt u een reeks rijen voor elke gebruiker, waarbij elke rij Hallo-nummer van een bepaalde gebruiker binnen een bepaalde periode bezochte pagina's vertegenwoordigt.

![Schema](./media/sql-database-temporal-tables/AzureTemporal1.png)

Gelukkig hoeft u geen tooput moeite in uw app toomaintain deze activiteit informatie. Dit proces is met tijdelijke tabellen geautomatiseerd - zodat u de volledige flexibiliteit tijdens het websiteontwerp en meer tijd toofocus op Hallo gegevensanalyse zelf. Hallo alleen dat u toodo hoeft tooensure is die **WebSiteInfo** tabel is geconfigureerd als [tijdelijke systeemversietabellen](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0). Hallo exacte stappen tooutilize tijdelijke tabellen in dit scenario worden hieronder beschreven.

## <a name="step-1-configure-tables-as-temporal"></a>Stap 1: Tabellen als tijdelijke configureren
Afhankelijk van of u vanaf de ontwikkeling van nieuwe of bestaande toepassing te upgraden, wordt u tijdelijke tabellen maken of bestaande wijzigen door tijdelijke kenmerken toe te voegen. In het algemeen geval uw scenario is een combinatie van deze twee opties. Voer deze actie met behulp van [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS) [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) of een ander Transact-SQL-ontwikkeling-hulpprogramma.

> [!IMPORTANT]
> Het verdient aanbeveling dat u altijd hello gebruiken meest recente versie van Management Studio tooremain gesynchroniseerd met updates tooMicrosoft Azure en SQL-Database. [SQL Server Management Studio bijwerken](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

### <a name="create-new-table"></a>Nieuwe tabel maken
Contextmenuoptie 'Nieuwe Systeemversietabel' in SSMS Object Explorer tooopen Hallo query-editor gebruiken met een tijdelijke tabel sjabloonscript en vervolgens 'Geef waarden voor Sjabloonparameters' (Ctrl + Shift + M) toopopulate Hallo sjabloon gebruiken:

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

In SSDT, gekozen voor de sjabloon 'Tijdelijke tabel (Systeemversietabellen)' wanneer nieuwe items toohello databaseproject toe te voegen. Dat wordt geopend tabelontwerp en schakel u tooeasily opgeven Hallo tabelindeling:

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

U kunt ook een tijdelijke tabel maken door op te geven Hallo Transact-SQL-instructies rechtstreeks, zoals weergegeven in Hallo voorbeeld hieronder. Houd er rekening mee dat Hallo verplichte elementen van elke tijdelijke tabel zijn Hallo periodedefinitie en Hallo SYSTEM_VERSIONING-component met een verwijzing tooanother gebruikerstabel die historische rij upversies:

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

Wanneer u de tijdelijke systeemversietabel maakt, wordt automatisch Hallo bijbehorende geschiedenistabel met Hallo standaardconfiguratie gemaakt. Hallo standaard geschiedenistabel bevat een geclusterde B-tree-index op Hallo periodekolommen (einde start) met pagina compressie is ingeschakeld. Deze configuratie is optimaal is voor de meeste Hallo van scenario's waarin tijdelijke tabellen worden gebruikt, met name voor [gegevens controle](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0). 

In dit geval streven we ernaar tooperform op basis van tijd trendanalyse gedurende een langere gegevensgeschiedenis en met grotere gegevenssets, dus Hallo opslag keuze voor de geschiedenistabel Hallo een geclusterde columnstore-index is. Een geclusterde columnstore biedt zeer goede compressie en prestaties voor analytische query's. Tijdelijke tabellen geven u flexibiliteit tooconfigure indexen op Hallo Hallo volledig onafhankelijk van huidige en de tijdelijke tabellen. 

> [!NOTE]
> Columnstore-indexen zijn alleen beschikbaar in Hallo premium servicecategorie.
>

Hallo script volgen ziet u hoe Standaardindex voor geschiedenistabel gewijzigde toohello geclusterde columnstore kan zijn:

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

Tijdelijke tabellen worden weergegeven in Hallo Object Explorer met de specifieke pictogram hello om gemakkelijker te identificeren, terwijl de geschiedenistabel wordt weergegeven als een onderliggend knooppunt.

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a>Bestaande tabel tootemporal wijzigen
We hebben betrekking op Hallo alternatieve scenario in welke Hallo WebsiteUserInfo tabel al bestaat, maar is niet ontworpen tookeep een geschiedenis van wijzigingen. In dit geval kunt u eenvoudig hello bestaande tabel toobecome tijdelijke, zoals weergegeven in het volgende voorbeeld Hallo uitbreiden:

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

## <a name="step-2-run-your-workload-regularly"></a>Stap 2: Uw werkbelasting regelmatig wordt uitgevoerd
Hallo belangrijkste voordeel van tijdelijke tabellen is dat u niet toochange moet of aanpassen van uw website in een manier tooperform bijhouden. Zodra gemaakt, behouden voor tijdelijke tabellen transparant eerdere versies van de rij telkens wanneer u de wijzigingen op uw gegevens uitvoeren. 

In de volgorde tooleverage automatische bijhouden voor dit scenario, gaan we zojuist bijwerken kolom **PagesVisited** telkens wanneer de gebruiker installatieserver sessie op Hallo website wordt:

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

Het is belangrijk toonotice die update query Hallo hoeft niet tooknow Hallo precieze tijd wanneer de huidige bewerking Hallo opgetreden of hoe u historische gegevens blijven behouden voor toekomstige analyse. Beide aspecten worden automatisch afgehandeld door hello Azure SQL Database. Hallo volgende diagram illustreert hoe gegevens van geschiedenis van elke update wordt gegenereerd.

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a>Stap 3: Analyse van de historische gegevens
Als tijdelijke systeemsamenstelling is ingeschakeld, is analyse van historische gegevens nu slechts één query weg van u. In dit artikel wordt we enkele voorbeelden voor het oplossen van algemene analysis scenario's - toolearn alle gegevens verstrekken, verschillende opties die zijn geïntroduceerd in Hallo verkennen [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) component.

toosee hello bovenste 10 gebruikers gesorteerd op Hallo aantal bezochte webpagina's vanaf een uur geleden, voer deze query uit:

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

U kunt eenvoudig deze query wijzigen tooanalyze Hallo site bezoeken vanaf een dag geleden, een maand geleden of op elk punt in de afgelopen Hallo die u wenst.

tooperform elementaire statistische analyse voor Hallo vorige dag, gebruikt u Hallo voorbeeld te volgen:

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

toosearch voor activiteiten van een specifieke gebruiker binnen een periode, gebruik Hallo ingesloten component:

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

Grafische visualisatie is vooral handig voor tijdelijke query's, zoals u trends en gebruikspatronen in een intuïtieve manier heel eenvoudig weergeven kunt:

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a>Zich ontwikkelende tabelschema
Normaal gesproken moet u toochange Hallo tijdelijke tabelschema terwijl u ontwikkeling van apps. Voor die, voert u eenvoudigweg reguliere ALTER TABLE-instructies en Azure SQL Database worden op de juiste wijze wijzigingen toohello geschiedenistabel doorgegeven. Hallo volgende script toont hoe u extra kenmerk voor bijhouden kunt toevoegen:

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

Op deze manier kunt u de definitie van kolom wijzigen terwijl uw werkbelasting actief is:

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

Ten slotte kunt u een kolom die u niet meer nodig hebt.

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

Of gebruik de meest recente [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange tijdelijke tabel schema terwijl u bent verbonden toohello database (onlinemodus) of als onderdeel van het databaseproject hello (offlinemodus).

## <a name="controlling-retention-of-historical-data"></a>Bewaren van historische gegevens beheren
Met tijdelijke systeemversietabellen, kan het verhogen van geschiedenistabel Hallo Hallo databasegrootte is meer dan gewone tabellen. Een grote en voortdurend groeiende geschiedenistabel kan een probleem die beide vanwege toopure opslagkosten, evenals een prestaties opleggen belasting op het tijdelijke uitvoeren van query's vormen. Daarom is ontwikkelen van een bewaarbeleid voor gegevens voor het beheren van gegevens in de geschiedenistabel Hallo een belangrijk aspect van het plannen en beheren van Hallo levenscyclus van elke tijdelijke tabel. Met Azure SQL Database hebt u de volgende methoden voor het beheren van historische gegevens in de tijdelijke tabel Hallo Hallo:

* [Partitioneren van tabel](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [Script voor aangepaste opschoning](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a>Volgende stappen
Bekijk voor meer informatie over tijdelijke tabellen [MSDN-documentatie](https://msdn.microsoft.com/library/dn935015.aspx).
Bezoek Channel 9 toohear een [echte klant tijdelijke implementatie Succesverhaal](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) en bekijk een [tijdelijke demonstratie live](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

