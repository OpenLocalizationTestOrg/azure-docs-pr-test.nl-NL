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
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a>Historische gegevens in tijdelijke tabellen met bewaarbeleid beheren
Tijdelijke tabellen wordt mogelijk uitgebreid grootte van de database meer dan gewone tabellen, met name als u historische gegevens voor een langere periode behouden. Bewaarbeleid voor historische gegevens is daarom een belangrijk aspect van het plannen en beheren van Hallo levenscyclus van elke tijdelijke tabel. Tijdelijke tabellen in Azure SQL Database worden geleverd met eenvoudig te gebruiken bewaren mechanisme waarmee u deze taak.

Bewaren van de tijdelijke geschiedenistabel kan worden geconfigureerd op Hallo afzonderlijke tabelniveau, waarmee gebruikers toocreate flexibele veroudering beleidsregels. Toepassen van de tijdelijke bewaarperiode is eenvoudig: slechts één parameter toobe ingesteld tijdens het maken of schema wijzigen van de tabel is vereist.

Nadat u een bewaarbeleid gedefinieerd, start Azure SQL Database regelmatig te controleren of er zijn historische rijen die in aanmerking voor automatische opruimen komen. Identificatie van de overeenkomende rijen en de verwijdering van Hallo geschiedenistabel optreden transparant, Hallo achtergrondtaak die is gepland en uitgevoerd door Hallo-systeem. Leeftijdsvoorwaarde voor tabelrijen Hallo-geschiedenis is ingeschakeld op basis van het einde van de SYSTEM_TIME-periode voor Hallo-kolom. Als de bewaarperiode, bijvoorbeeld toosix is ingesteld maanden, tabelrijen in aanmerking komen voor het opruimen Hallo volgende voorwaarde voldoen:

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

In Hallo voorgaande voorbeeld, wordt ervan uitgegaan dat die **ValidTo** kolom komt overeen toohello einde van de SYSTEM_TIME-periode.

## <a name="how-tooconfigure-retention-policy"></a>Hoe het bewaarbeleid tooconfigure?
Voordat u een bewaarbeleid voor een tijdelijke tabel configureert, Controleer eerst of tijdelijke historische bewaarperiode is ingeschakeld *op databaseniveau Hallo*.

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

Vlag database **is_temporal_history_retention_enabled** set tooON standaard is, maar gebruikers kunnen worden wijzigen met de instructie ALTER DATABASE. Het is ook automatisch set tooOFF na [wijst naar een bepaald tijstip](sql-database-recovery-using-backups.md) bewerking. tooenable tijdelijke geschiedenistabel bewaren opschonen voor uw database uitvoeren Hallo-instructie:

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> U kunt de bewaarperiode voor tijdelijke tabellen, zelfs als configureren **is_temporal_history_retention_enabled** is uitgeschakeld, maar automatisch opschonen voor verouderde rijen niet in dat geval wordt geactiveerd.
> 
> 

Bewaarbeleid is tijdens maken van de tabel geconfigureerd door de waarde voor Hallo HISTORY_RETENTION_PERIOD parameter:

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

Azure SQL Database kunt u de bewaarperiode toospecify met behulp van verschillende tijdseenheden: dagen, weken, maanden en jaren. Als HISTORY_RETENTION_PERIOD wordt weggelaten, wordt oneindige bewaren verondersteld. U kunt ook expliciet oneindige sleutelwoord gebruiken.

In sommige scenario's, kunt u tooconfigure retentie na het maken van de tabel of toochange eerder geconfigureerde waarde. In dat geval gebruikt u ALTER TABLE-instructie:

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> Instellen van SYSTEM_VERSIONING tooOFF *blijven niet behouden* periodewaarde bewaren. Instellen van SYSTEM_VERSIONING tooON zonder HISTORY_RETENTION_PERIOD expliciet opgegeven resultaten in Hallo oneindige bewaarperiode.
> 
> 

tooreview huidige status van het bewaarbeleid hello, gebruik Hallo volgende query die markering joins tijdelijke bewaren inschakelen op databaseniveau Hallo met bewaartermijnen voor afzonderlijke tabellen:

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


## <a name="how-sql-database-deletes-aged-rows"></a>Hoe SQL-Database worden verwijderd, verouderde rijen?
Hallo opruimproces is afhankelijk van Hallo index lay-out van Hallo geschiedenistabel. Het is belangrijk toonotice die *slechts geschiedenis tabellen met een geclusterde index (B-tree of columnstore) kunnen niet-oneindig bewaarbeleid geconfigureerd*. Een achtergrondtaak tooperform verouderde gegevens wissen voor alle tijdelijke tabellen met beperkte bewaarperiode gemaakt.
Opschonen logica voor Hallo rowstore (B-tree) geclusterde index verwijdert de verouderde rij in kleinere reeksen (omhoog too10K) voor het minimaliseren van zware belasting op het databaselogboek en i/o-subsysteem. Hoewel maakt gebruik van opschonen logica vereist B-tree-index, ordenen van verwijderingen voor Hallo rijen die ouder zijn dan de bewaarperiode kan niet goed kan worden gegarandeerd. Daarom *eventuele afhankelijkheden worden pas van kracht op Hallo opschonen volgorde in uw toepassingen*.

Hallo Hallo geclusterde columnstore-opschoontaak verwijdert gehele [rij groepen](https://msdn.microsoft.com/library/gg492088.aspx) tegelijk (doorgaans bevatten 1 miljoen rijen elke), die zeer efficiënte, vooral wanneer u historische gegevens in een hoog tempo wordt gegenereerd.

![De geclusterde columnstore-bewaren](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

Uitstekend gegevenscompressie en efficiënte bewaren opschonen wordt geclusterde columnstore-index een ideale keuze voor scenario's wanneer uw werkbelasting snel hoge mate van historische gegevens genereert. Dit patroon is Typerend voor intensieve [transactionele verwerking werkbelastingen die gebruikmaken van tijdelijke tabellen](https://msdn.microsoft.com/library/mt631669.aspx) voor wijzigingen bijhouden en controle, trendanalyse of IoT gegevensopname.

## <a name="index-considerations"></a>Overwegingen voor index
Hallo-opschoontaak voor tabellen met de geclusterde index rowstore vereist index toostart met Hallo kolom bijbehorende Hallo einde van de SYSTEM_TIME-periode. Als de index niet bestaat, kunt u een eindige bewaarperiode niet configureren:

*Bericht 13765, 16 niveau 1 staat <br> </br> op de tijdelijke systeemversietabel 'temporalstagetestdb.dbo.WebsiteUserInfo' eindig bewaarperiode instellen is mislukt omdat de geschiedenistabel Hallo ' temporalstagetestdb.dbo.WebsiteUserInfoHistory' bevat geen vereiste geclusterde index. Houd rekening met het maken van een geclusterde columnstore of B-tree-index die begint met Hallo-kolom die overeenkomt met het einde van de SYSTEM_TIME period op Hallo geschiedenistabel.*

Het is belangrijk toonotice die standaard geschiedenistabel gemaakt met Azure SQL Database al Hallo bevat geclusterde index, die voldoen aan de voorwaarden bewaarbeleid. Als u tooremove die index in een tabel met beperkte bewaarperiode probeert, mislukt de bewerking met de volgende fout Hallo:

*Bericht 13766, 16 niveau 1 staat <br> </br> kan Hallo geclusterde index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' niet verwijderen omdat deze wordt gebruikt voor het automatisch opschonen van verouderde gegevens. Overweeg instelling HISTORY_RETENTION_PERIOD tooINFINITE op Hallo overeenkomstige tijdelijke systeemversietabel als u deze index toodrop nodig.*

Opruimen op Hallo geclusterde columnstore-index werkt optimaal als historische rijen worden ingevoegd in oplopende volgorde (geordend door Hallo van periodekolom), die altijd Hallo geval is wanneer Hallo geschiedenistabel is gevuld uitsluitend door Hallo SYSTEM_ Hallo VERSIONIOING-mechanisme. Als de rijen in de geschiedenistabel Hallo niet besteld door het einde van de periodekolom (die mogelijk Hallo geval als u bestaande historische gegevens hebt gemigreerd), moet u opnieuw boven op B-tree rowstore-index die is goed besteld tooachieve optimale geclusterde columnstore-index maken de prestaties.

Vermijd opnieuw opbouwen van de geclusterde columnstore-index in de geschiedenistabel Hallo met Hallo eindig bewaarperiode, omdat het mogelijk gewijzigd bestellen in Rijgroepen Hallo natuurlijk die zijn opgelegd door Hallo versiebeheer door het systeem bewerking. Als u nodig hebt toorebuild geclusterde columnstore-index in de geschiedenistabel Hallo, dit doen door opnieuw boven op compatibele B-tree-index, behouden in Hallo rowgroups nodig zijn voor reguliere opruimen ordening te maken. Hallo dezelfde manier moet worden uitgevoerd als u de tijdelijke tabel maken met bestaande geschiedenistabel die kolomindex zonder gegarandeerde gegevensvolgorde geclusterde bevat:

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

Wanneer beperkte bewaarperiode is geconfigureerd voor de geschiedenistabel Hallo met Hallo geclusterde columnstore-index, kunt u geen extra niet-geclusterde B-tree indexen op tabel maken:

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

Een poging tooexecute boven de instructie is mislukt met de volgende fout Hallo:

*Bericht 13772, 16 niveau 1 staat <br> </br> kan niet-geclusterde index maken op een tijdelijke geschiedenistabel 'WebsiteUserInfoHistory' omdat er beperkte bewaarperiode en de geclusterde columnstore-index die zijn gedefinieerd.*

## <a name="querying-tables-with-retention-policy"></a>Opvragen van tabellen met bewaarbeleid
Alle query's op de tijdelijke tabel Hallo automatisch historische rijen die overeenkomt met beperkte bewaarbeleid, tooavoid onvoorspelbare en inconsistente resultaten omdat verouderde rijen kunnen worden verwijderd door het Hallo-opschoontaak filteren *op elk punt in tijd en in willekeurige volgorde*.

Hallo volgende afbeelding ziet u het queryplan Hallo voor een eenvoudige query:

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

Hallo query plan omvat extra filter toegepast tooend van periodekolom (ValidTo) in de geclusterde Index scannen operator Hallo op Hallo geschiedenistabel (gemarkeerd). In dit voorbeeld wordt ervan uitgegaan dat één maand bewaarperiode is ingesteld op WebsiteUserInfo tabel.

![Queryfilter bewaren](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

Echter, als u rechtstreeks query geschiedenistabel uitvoert, ziet u mogelijk rijen die ouder dan de opgegeven bewaartermijn tijdsperiode, maar zonder een garantie voor herhaalbare queryresultaten zijn. Hallo volgende afbeelding ziet u query uitvoeringsplan voor Hallo query op Hallo geschiedenistabel zonder aanvullende filters zijn toegepast:

![Geschiedenis zonder bewaren filter opvragen](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

Vertrouw niet uw bedrijfslogica op de geschiedenistabel buiten de bewaarperiode lezen als u krijgt u mogelijk inconsistente of onverwachte resultaten. U wordt aangeraden tijdelijke query's te gebruiken met FOR SYSTEM_TIME-component voor het analyseren van gegevens in tijdelijke tabellen.

## <a name="point-in-time-restore-considerations"></a>Punt in tijd terugzetten overwegingen
Wanneer u een nieuwe database door maakt [herstellen van de bestaande database tooa bepaald punt in tijd](sql-database-recovery-using-backups.md), heeft tijdelijke bewaren op databaseniveau Hallo uitgeschakeld. (**is_temporal_history_retention_enabled** vlag ingesteld tooOFF). Deze functie kunt u alle historische rijen bij het herstellen zonder dat u die rijen verouderde worden verwijderd voordat u een tooquery tooexamine ze. U kunt deze ook gebruiken*inspecteren van historische gegevens buiten de geconfigureerde bewaarperiode*.

Stel dat een tijdelijke tabel die een maand bewaren opgegeven tijdsperiode heeft. Als uw database is gemaakt in de laag Premium-Service, zou u kunnen toocreate databasekopie met Hallo databasestatus too35 dagen terug in de afgelopen Hallo zijn. Die effectief kunt u tooanalyze historische rijen die actief too65 dagen oud zijn rechtstreeks een query uitgevoerd op Hallo geschiedenistabel.

Als u opruimen van de tijdelijke bewaren tooactivate wilt, Voer Hallo volgende Transact-SQL-instructie na punt naar een bepaald tijstip:

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a>Volgende stappen
hoe toouse tijdelijke tabellen in uw toepassingen uitchecken toolearn [aan de slag met tijdelijke tabellen in Azure SQL Database](sql-database-temporal-tables.md).

Bezoek Channel 9 toohear een [echte klant tijdelijke implementatie Succesverhaal](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) en bekijk een [tijdelijke demonstratie live](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

Raadpleeg voor gedetailleerde informatie over tijdelijke tabellen [MSDN-documentatie](https://msdn.microsoft.com/library/dn935015.aspx).

