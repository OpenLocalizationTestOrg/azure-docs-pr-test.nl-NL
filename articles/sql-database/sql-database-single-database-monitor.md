---
title: prestaties van de database in Azure SQL Database aaaMonitoring | Microsoft Docs
description: Meer informatie over het Hallo-opties voor het controleren van de database met Azure-hulpprogramma's en dynamische Beheerweergave.
keywords: database bewaken, prestaties van clouddatabase
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: a2e47475-c955-4a8d-a65c-cbef9a6d9b9f
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: b13771183d4ccf37f58e2fc518b9b14de38212dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-database-performance-in-azure-sql-database"></a>Databaseprestaties bewaken in Azure SQL Database
Hallo prestatiecontrole van een SQL-database in Azure begint met het bewaken van Hallo resource relatieve toohello het gebruiksniveau van databaseprestaties. Bewaking, kunt u bepalen of uw database veel capaciteit heeft of juist problemen heeft omdat resources volledig worden benut uit en vervolgens besluit of het is tijd tooadjust Hallo prestatieniveau en [servicelaag](sql-database-service-tiers.md) van uw database. U kunt een database bewaken met grafische hulpprogramma's in Hallo [Azure-portal](https://portal.azure.com) of met behulp van SQL [dynamische beheerweergaven](https://msdn.microsoft.com/library/ms188754.aspx).

## <a name="monitor-databases-using-hello-azure-portal"></a>Databases bewaken via hello Azure-portal
In Hallo [Azure-portal](https://portal.azure.com/), kunt u gebruik van een individuele database bewaken door uw database selecteren en te klikken op Hallo **bewaking** grafiek. Hiermee wordt een **metriek** venster die u wijzigen kunt door te klikken op Hallo **grafiek bewerken** knop. Voeg Hallo metrische gegevens te volgen:

* CPU-percentage
* DTU-percentage
* Gegevens-I/O-percentage
* Databaseomvangpercentage

Nadat u deze metrische gegevens hebt toegevoegd, kunt u tooview blijven ze in Hallo **bewaking** grafiek met meer informatie over Hallo **metriek** venster. Alle vier metrische gegevens tonen Hallo Gemiddeld gebruik percentage relatieve toohello **DTU** van uw database. Zie Hallo [Servicelagen](sql-database-service-tiers.md) voor meer informatie over dtu's.

![Servicelaagbewaking van databaseprestaties.](./media/sql-database-service-tiers/sqldb_service_tier_monitoring.png)

U kunt ook waarschuwingen configureren op Hallo-maatstaven voor prestaties. Klik op Hallo **waarschuwing toevoegen** knop in Hallo **metriek** venster. Ga als volgt Hallo wizard tooconfigure de waarschuwing. U hebt Hallo optie tooalert als Hallo metrische gegevens een bepaalde drempelwaarde overschrijden of als Hallo onder een bepaalde drempelwaarde komt meetpunt.

Bijvoorbeeld, als u Hallo werkbelasting op uw database toogrow verwacht, kunt u tooconfigure een e-mailmelding telkens wanneer uw database 80% van een Hallo prestatiewaarden heeft bereikt. U kunt dit gebruiken als een vroegtijdige waarschuwing toofigure uit wanneer u tooswitch toohello hoger prestatieniveau wellicht.

Hallo-maatstaven voor prestaties kunt u bepalen of u kunt toodowngrade tooa lager prestatieniveau. Stel dat u gebruikmaakt van een Standard S2-database en alle prestaties metrische gegevens weergeven die database gemiddeld Hallo gebruikt niet meer dan 10% op elk moment. Is het waarschijnlijk dat Hallo-database in Standard S1 goed werkt. Echter wel rekening met workloads die pieken of fluctueren, voordat u Hallo besluit toomove tooa lager prestatieniveau.

## <a name="monitor-databases-using-dmvs"></a>Databases bewaken via DMV's
Hallo dezelfde metrische gegevens die beschikbaar zijn in de portal Hallo zijn ook beschikbaar via systeemweergaven: [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) in logische Hallo **master** database van de server en [sys.dm_db_ resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) in Hallo-gebruikersdatabase. Gebruik **sys.resource_stats** desgewenst toomonitor minder gedetailleerde gegevens over een langere periode. Gebruik **sys.dm_db_resource_stats** als u toomonitor moet meer gedetailleerde gegevens binnen een kleinere tijdsbestek. Zie [Richtlijnen voor Azure SQL Database-prestaties](sql-database-single-database-monitor.md#monitor-resource-use) voor meer informatie.

> [!NOTE]
> **sys.dm_db_resource_stats** retourneert een lege resultatenset als deze wordt gebruikt voor de buiten gebruik gestelde Web en Business Edition-databases.
>
>

### <a name="monitor-resource-use"></a>Brongebruik controleren

U kunt controleren met resource-gebruik [SQL Database Query Performance Insight](sql-database-query-performance.md) en [Query Store](https://msdn.microsoft.com/library/dn817826.aspx).

U kunt ook gebruik van deze twee weergaven met bewaken:

* [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)
* [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx)

#### <a name="sysdmdbresourcestats"></a>sys.dm_db_resource_stats
U kunt Hallo [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) weergave in elke SQL-database. Hallo **sys.dm_db_resource_stats** weergave toont recente resource Gebruik relatieve toohello service gegevenslaag. Gemiddelde percentages voor CPU, i/o-gegevens, logboekschrijfbewerkingen en geheugen elke 15 seconden worden vastgelegd en worden bewaard 1 uur.

Omdat deze weergave een meer gedetailleerd blik op gebruik van bronnen biedt, gebruikt u **sys.dm_db_resource_stats** eerste voor een analyse van de huidige status of het oplossen van problemen. Deze query geeft bijvoorbeeld Hallo gemiddelde en maximale gebruiken voor de huidige database Hallo over Hallo afgelopen uur:

    SELECT  
        AVG(avg_cpu_percent) AS 'Average CPU use in percent',
        MAX(avg_cpu_percent) AS 'Maximum CPU use in percent',
        AVG(avg_data_io_percent) AS 'Average data I/O in percent',
        MAX(avg_data_io_percent) AS 'Maximum data I/O in percent',
        AVG(avg_log_write_percent) AS 'Average log write use in percent',
        MAX(avg_log_write_percent) AS 'Maximum log write use in percent',
        AVG(avg_memory_usage_percent) AS 'Average memory use in percent',
        MAX(avg_memory_usage_percent) AS 'Maximum memory use in percent'
    FROM sys.dm_db_resource_stats;  

Zie voor andere query's, Hallo voorbeelden in [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx).

#### <a name="sysresourcestats"></a>sys.resource_stats
Hallo [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) weergave in Hallo **master** database bevat extra informatie kunt u Hallo prestaties van uw SQL-database op het niveau van prijscategorie en prestatieniveau specifieke service bewaken . Hallo-gegevens worden verzameld om de 5 minuten en ongeveer 35 dagen wordt bijgehouden. Deze weergave is handig voor een langere historische analyse van hoe uw SQL-database maakt gebruik van bronnen.

Hallo volgende grafiek ziet Hallo CPU gebruik van bronnen voor een Premium-database met Hallo P2 prestatieniveau voor elk uur in een week. Deze grafiek begint op een maandag, ziet u 5 werkdagen en geeft vervolgens een weekend, als er veel minder gebeurt op Hallo-toepassing.

![Gebruik van SQL database-bronnen](./media/sql-database-performance-guidance/sql_db_resource_utilization.png)

Vanuit de Hallo gegevens, is deze database momenteel een piek CPU-belasting van iets meer dan 50 procent CPU-gebruik relatieve toohello P2 prestatieniveau (middaguur op dinsdag). Als CPU Hallo verwerkingsflexibiliteit factor in resource-profiel van de toepassing hello, kunt vervolgens u besluiten dat P2 is Hallo rechts prestaties niveau tooguarantee die Hallo werkbelasting altijd past. Als u een toepassing toogrow na verloop van tijd verwacht, is een goed idee toohave een buffer extra bron zodat de toepassing hello niet ooit Hallo prestatieniveau limiet bereikt. Als u het prestatieniveau Hallo verhoogt, kunt u helpen te voorkomen dat zichtbaar is voor een klant fouten die optreden mogelijk wanneer een database geen voldoende power tooprocess aanvragen effectief, met name in omgevingen latentie gevoelig. Een voorbeeld is een database die een toepassing die worden getekend door webpagina's op basis van Hallo resultaten van de database-aanroepen ondersteunt.

Andere soorten toepassingen mogelijk dezelfde anders graph Hallo interpreteren. Bijvoorbeeld, als een toepassing tooprocess salarissen gegevens per dag probeert en Hallo heeft kunt dezelfde grafiek die dit kind van 'batchverwerking' model doen goed op prestatieniveau P1. Hallo prestatieniveau P1 heeft 100 dtu's vergeleken too200 dtu's op Hallo P2 prestatieniveau. Hallo prestatieniveau P1 biedt half Hallo prestaties van Hallo P2 prestatieniveau. Dus 50 procent van de CPU-gebruik in P2 is gelijk aan 100 procent CPU-gebruik in P1. Als de toepassing hello geen time-outs, maakt het niet uit als een taak 2 uur of 2,5 uur toofinish duurt, als het vandaag wordt voltooid. Een toepassing in deze categorie kunt waarschijnlijk prestatieniveau P1 gebruiken. U kunt profiteren van Hallo feit dat er perioden tijdens Hallo dag wanneer bronnengebruik ligt, zodat eventuele 'big piek' kan worden gelekt via in één Hallo holten later op Hallo dag zijn. Hallo prestatieniveau P1 mogelijk geschikt voor dit soort van toepassing (en geld besparen), zolang Hallo taken op tijd per dag voltooien kunnen.

Azure SQL Database worden verbruikt resourcegegevens voor elke actieve database in Hallo **sys.resource_stats** weergave Hallo **master** database op elke server. Hallo-gegevens in de tabel Hallo worden samengevoegd voor 5 minuten durende intervallen. Met Hallo Basic, Standard en Premium Servicelagen, kunnen Hallo gegevens worden meer dan 5 minuten tooappear in tabel hello, betekent dat deze gegevens nuttiger voor historische analyse in plaats van in de buurt van de realtime-analyse. Query Hallo **sys.resource_stats** weergave toosee Hallo recente geschiedenis van een database en toovalidate Hallo reservering gekozen bezorgd Hallo prestaties die u wilt zien wanneer nodig.

> [!NOTE]
> U moet verbonden toohello **master** database van de logische SQL database-server tooquery **sys.resource_stats** in Hallo volgen voorbeelden.
> 
> 

Dit voorbeeld ziet u hoe Hallo-gegevens in deze weergave wordt weergegeven:

    SELECT TOP 10 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![Hallo sys.resource_stats catalogusweergave](./media/sql-database-performance-guidance/sys_resource_stats.png)

Hallo volgende voorbeeld ziet u verschillende manieren waarmee u Hallo kunt **sys.resource_stats** catalogus tooget-informatie over hoe uw SQL-database maakt gebruik van bronnen weergeven:

1. toolook op Hallo voorbij de bron van de week voor Hallo database userdb1 gebruiken, kunt u deze query uitvoeren:
   
        SELECT *
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND
              start_time > DATEADD(day, -7, GETDATE())
        ORDER BY start_time DESC;
2. hoe goed uw werkbelasting past Hallo prestatieniveau tooevaluate, moet u toodrill omlaag in elk aspect van Hallo resource metrische gegevens: CPU, lezen, schrijven, aantal werknemers en aantal sessies. Hier volgt een herziene query met **sys.resource_stats** tooreport Hallo gemiddelde en maximale waarden van deze resource metrische gegevens:
   
        SELECT
            avg(avg_cpu_percent) AS 'Average CPU use in percent',
            max(avg_cpu_percent) AS 'Maximum CPU use in percent',
            avg(avg_data_io_percent) AS 'Average physical data I/O use in percent',
            max(avg_data_io_percent) AS 'Maximum physical data I/O use in percent',
            avg(avg_log_write_percent) AS 'Average log write use in percent',
            max(avg_log_write_percent) AS 'Maximum log write use in percent',
            avg(max_session_percent) AS 'Average % of sessions',
            max(max_session_percent) AS 'Maximum % of sessions',
            avg(max_worker_percent) AS 'Average % of workers',
            max(max_worker_percent) AS 'Maximum % of workers'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
3. U kunt met deze informatie over Hallo gemiddelde en maximale waarden van elke resource metrische gegevens kunt beoordelen hoe goed uw werkbelasting in Hallo prestatieniveau die u hebt gekozen past. Normaal gesproken gemiddelde waarden van **sys.resource_stats** bieden u een goede basis toouse tegen Hallo doelgrootte. Moet uw primaire meting stick. Voor een voorbeeld mogelijk Hallo standaard servicelaag wordt gebruikt met S2 prestatieniveau. Hallo gemiddelde gebruik percentages voor CPU- en i/o-leesbewerkingen en schrijfbewerkingen zijn dan 40 procent en gemiddelde aantal werknemers Hallo lager is dan 50 Hallo gemiddeld aantal sessies lager is dan 200. Uw werkbelasting mogelijk in Hallo prestatieniveau S1 past. Het is gemakkelijk toosee of geschikt is voor uw database in Hallo worker en sessielimieten. toosee tooCPU, lees- en schrijfbewerkingen, of een database in een lager prestatieniveau met past beschouwt Hallo DTU aantal Hallo lager prestatieniveau delen door Hallo DTU-nummer van uw huidige prestatieniveau en vervolgens Hallo resultaat vermenigvuldigd met 100:
   
    **S1 DTU / S2 DTU * 100 = 20 / 50 * 100 = 40**
   
    Hallo-resultaat is Hallo relatieve prestatieverschil tussen twee prestatieniveaus Hallo in een percentage. Als uw gebruik van de resource niet groter zijn dan deze hoeveelheid, kan uw werkbelasting past in Hallo lager prestatieniveau. Echter u moet toolook op alle bereiken van waarden voor het gebruik van resources en vastgesteld door percentage, hoe vaak de werkbelasting van uw database valt in Hallo lager prestatieniveau. Hallo levert volgende query Hallo past percentage per resourcedimensie, op basis van Hallo drempelwaarde van 40 procent die in dit voorbeeld is berekend:
   
        SELECT
            (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log Write Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical Data IO Fit Percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    Op basis van uw database serviceniveaudoelstelling (SLO), kunt u beslissen of uw werkbelasting in Hallo lager prestatieniveau past. Als de werkbelasting van uw database SLO 99,9 procent en hello voorgaande query waarden groter dan 99,9% voor alle drie resourcedimensies retourneert, wordt uw workload waarschijnlijk in Hallo lager prestatieniveau past.
   
    Bekijkt hello past percentage biedt ook inzicht in of u niveau prestaties toomeet van toohello volgende hogere uw SLO overstappen moet. Userdb1 ziet u bijvoorbeeld Hallo CPU-gebruik voor Hallo afgelopen week te volgen:
   
   | Gemiddelde CPU-percentage | Maximale CPU-percentage |
   | --- | --- |
   | 24.5 |100.00 |
   
    gemiddelde CPU Hallo is over een kwartaal van het Hallo-limiet van Hallo prestatieniveau, zijn voor Hallo prestatieniveau van Hallo-database geschikt zou. Maar Hallo maximale waarde bevat dat die database Hallo Hallo bereikt van het prestatieniveau Hallo. Wilt u toomove toohello hoger prestatieniveau hebben? Kijken hoe vaak uw werkbelasting bereikt 100 procent en vergelijk dit tooyour database werkbelasting SLO.
   
        SELECT
        (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log write fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical data I/O fit percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    Als u deze query retourneert een waarde minder dan 99,9 procent voor een van drie Hallo resourcedimensies, houd rekening met beide bewegende toohello hoger prestatieniveau of technieken tooreduce Hallo load afstemming van toepassingen op Hallo SQL-database.
4. In deze oefening tevens rekening gehouden met de verwachte werkbelasting toename Hallo toekomstige.

Voor elastische pools, kunt u afzonderlijke databases in de groep Hallo bewaken met Hallo technieken die in deze sectie beschreven. Maar u kunt ook Hallo pool als geheel bewaken. Zie [Een elastische pool bewaken en beheren](sql-database-elastic-pool-manage-portal.md) voor meer informatie.


### <a name="maximum-concurrent-requests"></a>Maximum aantal gelijktijdige aanvragen
toosee Hallo aantal gelijktijdige aanvragen, wordt deze Transact-SQL-query uitvoeren op de SQL-database:

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R

tooanalyze hello werkbelasting van een lokale SQL Server-database wijzigen deze query toofilter op Hallo specifieke database die u wilt tooanalyze. Bijvoorbeeld, als er een lokale database met de naam MijnDatabase, retourneert deze Transact-SQL-query Hallo aantal gelijktijdige aanvragen in de database:

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R
    INNER JOIN sys.databases D ON D.database_id = R.database_id
    AND D.name = 'MyDatabase'

Dit is slechts een momentopname op één punt in tijd. tooget een beter inzicht in uw werkbelasting en de vereisten voor gelijktijdige aanvragen, moet u toocollect veel voorbeelden gedurende een bepaalde periode.

### <a name="maximum-concurrent-logins"></a>Maximum aantal gelijktijdige aanmeldingen
U kunt uw gebruikers- en patronen tooget een idee van de frequentie van aanmeldingen Hallo analyseren. U kunt ook werkelijke hoeveelheden uitvoeren in een omgeving toomake voor test zeker dat u bent niet kunt u door deze of andere limieten in dit artikel besproken. Er is een enkele query of de dynamische beheerweergave (DMV) die u kunt u zien gelijktijdige aanmelding telt of de geschiedenis niet.

Als meerdere clients gebruik Hallo dezelfde verbindingsreeks hello service verifieert voor elke aanmelding. Als 10 gebruikers tegelijk verbinding maken met database met behulp van tooa Hallo dezelfde gebruikersnaam en wachtwoord, zou er 10 gelijktijdige aanmeldingen. Deze beperking geldt alleen toohello duur van het Hallo-aanmelding en verificatie. Als Hallo dezelfde 10 gebruikers verbinding sequentieel toohello database maakt, zou het aantal gelijktijdige aanmeldingen Hallo niet groter dan 1.

> [!NOTE]
> Op dit moment is deze limiet niet van toepassing toodatabases in elastische pools.
> 
> 

### <a name="maximum-sessions"></a>Maximum aantal sessies
toosee hello aantal huidige actieve sessies, wordt deze Transact-SQL-query uitvoeren op de SQL-database:

    SELECT COUNT(*) AS [Sessions]
    FROM sys.dm_exec_connections

Als u van een lokale SQL Server-werkbelasting analyseren bent, wijzigt u Hallo query toofocus op een specifieke database. Deze query kunt u beter bepalen mogelijke sessie behoeften voor Hallo database als u overweegt tooAzure SQL-Database te verplaatsen.

    SELECT COUNT(*)  AS [Sessions]
    FROM sys.dm_exec_connections C
    INNER JOIN sys.dm_exec_sessions S ON (S.session_id = C.session_id)
    INNER JOIN sys.databases D ON (D.database_id = S.database_id)
    WHERE D.name = 'MyDatabase'

Deze query's retourneren opnieuw een punt in tijd telling. Als u meerdere steekproeven gedurende een bepaalde periode verzamelt, hebt u Hallo best inzicht in uw sessie gebruiken.

Voor analyse van de SQL-Database, kunt u historische statistieken opvragen op sessies door het uitvoeren van query's Hallo [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) weergeven en beoordelen van Hallo **active_session_count** kolom. 
