---
title: aaaMigrate uw bestaande Azure-opslag toopremium datawarehouse | Microsoft Docs
description: Instructies voor het migreren van een bestaande datawarehouse toopremium gegevensopslag
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a>Uw datawarehouse toopremium opslag migreren
Azure SQL Data Warehouse onlangs geïntroduceerd [premium-opslag voor groter prestaties, voorspelbaarheid][premium storage for greater performance predictability]. Bestaande gegevens worden in datawarehouses die momenteel in de standard-opslag kunnen worden gemigreerd toopremium opslag. U kunt profiteren van de automatische migratie van of als u liever toocontrol wanneer toomigrate (waarbij uitval), kunt u doen Hallo migratie zelf.

Als u meer dan een datawarehouse hebt, gebruikt u Hallo [schema voor automatische migratie] [ automatic migration schedule] toodetermine wanneer deze ook worden gemigreerd.

## <a name="determine-storage-type"></a>Opslagtype bepalen
Als u een datawarehouse voordat Hallo datums na hebt gemaakt, gebruikt u momenteel standard-opslag.

| **Regio** | **Datawarehouse gemaakt voor deze datum** |
|:--- |:--- |
| Australië - oost |Premium-opslag is nog niet beschikbaar |
| China - oost |1 november 2016 |
| China - noord |1 november 2016 |
| Duitsland - centraal |1 november 2016 |
| Duitsland - noordoost |1 november 2016 |
| India - west |Premium-opslag is nog niet beschikbaar |
| Japan - west |Premium-opslag is nog niet beschikbaar |
| Noord-centraal VS |10 november 2016 |

## <a name="automatic-migration-details"></a>Details van de automatische migratie
Standaard gaan we uw database voor u tussen 18:00 uur en 6:00 uur in uw regio lokale tijd tijdens Hallo [schema voor automatische migratie][automatic migration schedule]. Uw bestaande datawarehouse kan niet worden gebruikt tijdens de migratie Hallo. Hallo migratie duurt ongeveer één uur per terabyte van opslag per datawarehouse. U wordt niet in rekening gebracht tijdens een gedeelte van de automatische Hallo-migratie.

> [!NOTE]
> Wanneer Hallo migratie voltooid is, wordt uw datawarehouse zich weer online is en kan worden gebruikt.
>
>

Microsoft neemt Hallo stappen toocomplete Hallo migratie (deze hoeven niet alle betrokkenheid van uw kant) te volgen. Stel in dit voorbeeld of uw bestaande datawarehouse op een standard-opslag is momenteel met de naam 'MyDW'.

1. Microsoft wijzigt de naam 'MyDW' te 'MyDW_DO_NOT_USE_ [tijdstempel]'.
2. Microsoft pauzeert 'MyDW_DO_NOT_USE_ [tijdstempel]'. Gedurende deze tijd is een back-up gemaakt. Mogelijk ziet u meerdere onderbroken en hervat als er problemen ondervindt tijdens dit proces.
3. Microsoft maakt een nieuw datawarehouse met de naam 'MyDW' op premium-opslag vanuit Hallo back-up gemaakt in stap 2. 'MyDW' worden niet weergegeven tot nadat Hallo herstellen voltooid is.
4. Nadat het Hallo herstellen is voltooid 'MyDW' toohello dezelfde gegevens datawarehouse-eenheden en -status geretourneerd (onderbroken of actieve) die deze was voordat Hallo-migratie.
5. Nadat Hallo migratie voltooid is, verwijdert Microsoft 'MyDW_DO_NOT_USE_ [tijdstempel]'.

> [!NOTE]
> Hallo uitvoeren volgende instellingen niet via als onderdeel van Hallo migratie:
>
> * Controle op databaseniveau Hallo moet toobe weer wordt ingeschakeld.
> * Firewallregels op databaseniveau Hallo moeten toobe opnieuw toegevoegd. Firewallregels op serverniveau Hallo worden niet getroffen.
>
>

### <a name="automatic-migration-schedule"></a>Planning voor automatische migratie
Automatische migraties optreden tussen 18:00 uur en 6:00 uur (lokale tijd per regio) tijdens het Hallo onderbreking schema te volgen.

| **Regio** | **Geschatte begindatum** | **Geschatte einddatum** |
|:--- |:--- |:--- |
| Australië - oost |Nog niet worden vastgesteld |Nog niet worden vastgesteld |
| China - oost |9 januari 2017 |13 januari 2017 |
| China - noord |9 januari 2017 |13 januari 2017 |
| Duitsland - centraal |9 januari 2017 |13 januari 2017 |
| Duitsland - noordoost |9 januari 2017 |13 januari 2017 |
| India - west |Nog niet worden vastgesteld |Nog niet worden vastgesteld |
| Japan - west |Nog niet worden vastgesteld |Nog niet worden vastgesteld |
| Noord-centraal VS |9 januari 2017 |13 januari 2017 |

## <a name="self-migration-toopremium-storage"></a>Zelfstandige migratie toopremium opslag
Als u toocontrol wilt wanneer uw uitvaltijd wordt uitgevoerd, kunt u Hallo stappen toomigrate een bestaand datawarehouse op standaardopslag toopremium opslag te volgen. Als u deze optie kiest, moet u Hallo zelf migratie voltooien voordat Hallo automatische migratie in deze regio begint. Dit zorgt ervoor dat u het risico van Hallo automatische migratie een conflict veroorzaken vermijden (Raadpleeg toohello [schema voor automatische migratie][automatic migration schedule]).

### <a name="self-migration-instructions"></a>Zelfstandige migratie-instructies
toomigrate uw gegevens datawarehouse zelf, gebruikt u Hallo back-up en herstellen van functies. Hallo terugzetten gedeelte van de migratie Hallo is verwachte tootake ongeveer één uur per terabyte van opslag per datawarehouse. Als u wilt dat tookeep Hallo dezelfde naam nadat de migratie is voltooid, voert u de Hallo [stappen toorename tijdens de migratie][steps toorename during migration].

1. [Onderbreken] [ Pause] uw datawarehouse. Dit vindt een automatische back-up.
2. [Herstellen] [ Restore] van uw meest recente momentopname.
3. Verwijder het bestaande datawarehouse op een standard-opslag. **Als u niet in deze stap toodo, wordt in rekening gebracht voor beide datawarehouses.**

> [!NOTE]
> Hallo uitvoeren volgende instellingen niet via als onderdeel van Hallo migratie:
>
> * Controle op databaseniveau Hallo moet toobe weer wordt ingeschakeld.
> * Firewallregels op databaseniveau Hallo moeten toobe opnieuw toegevoegd. Firewallregels op serverniveau Hallo worden niet getroffen.
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a>Wijzig de naam van datawarehouse tijdens de migratie (optioneel)
Twee databases op dezelfde logische server kan geen Hallo Hallo dezelfde naam. SQL Data Warehouse ondersteunt nu Hallo mogelijkheid toorename een datawarehouse.

Stel in dit voorbeeld of uw bestaande datawarehouse op een standard-opslag is momenteel met de naam 'MyDW'.

1. Wijzig de naam 'MyDW' met behulp van Hallo na de opdracht ALTER DATABASE. (In dit voorbeeld we je Wijzig de naam 'MyDW_BeforeMigration'.)  Deze opdracht alle bestaande transacties wordt gestopt en moet worden uitgevoerd in Hallo hoofddatabase toosucceed.
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. [Onderbreken] [ Pause] 'MyDW_BeforeMigration'. Dit vindt een automatische back-up.
3. [Herstellen] [ Restore] van uw meest recente momentopname van een nieuwe database met naam Hallo deze toobe (bijvoorbeeld ' MyDW') gebruikt.
4. Verwijderen van 'MyDW_BeforeMigration'. **Als u niet in deze stap toodo, wordt in rekening gebracht voor beide datawarehouses.**


## <a name="next-steps"></a>Volgende stappen
Hello toopremium opslag wijzigen, moet u ook een toenemend aantal blob-databasebestanden in Hallo onderliggende architectuur van uw datawarehouse. toomaximize hello prestatievoordelen van deze wijziging opnieuw maken van uw geclusterde columnstore-indexen met behulp van Hallo script volgen. Hallo script werkt door af te dwingen enkele van uw bestaande gegevens toohello extra blobs. Als u geen actie onderneemt, distribueren Hallo gegevens natuurlijk gedurende een bepaalde periode, als u meer gegevens in de tabellen laden.

**Vereisten:**

- Hallo-datawarehouse moet worden uitgevoerd met 1000 datawarehouse eenheden of hoger (Zie [scale rekenkracht][scale compute power]).
- Hallo gebruiker uitvoeren van script Hallo zou in Hallo [mediumrc rol] [ mediumrc role] of hoger. een gebruikersrol toothis tooadd Hallo volgende uitvoeren:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

Als u problemen ondervindt met uw datawarehouse [Maak een ondersteuningsticket] [ create a support ticket] en verwijzen naar 'migratie toopremium opslag' als Hallo mogelijke oorzaak.

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
