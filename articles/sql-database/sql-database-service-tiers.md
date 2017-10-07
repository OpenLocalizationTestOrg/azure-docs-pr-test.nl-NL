---
title: Azure SQL Database-service en de prestaties lagen | Microsoft Docs
description: Vergelijk SQL Database Servicelagen en prestatieniveaus van individuele databases en elastische pools SQL introduceren
keywords: databaseopties, prestaties van de database
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: f5c5c596-cd1e-451f-92a7-b70d4916e974
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/30/2017
ms.author: carlrab
ms.openlocfilehash: b27b78788614d32e6c0c4267fe0ce504ebd2f444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-performance-options-are-available-for-an-azure-sql-database"></a>Welke opties voor prestaties zijn beschikbaar voor een Azure SQL Database

[Azure SQL Database](sql-database-technical-overview.md) biedt vier Servicelagen voor beide één en [gegroepeerde](sql-database-elastic-pool.md) databases. Deze Servicelagen zijn: **Basic**, **standaard**, **Premium**, en **Premium RS**. Zijn binnen elke servicelaag meerdere prestatieniveaus ([dtu's](sql-database-what-is-a-dtu.md)) en toohandle verschillende workloads en grootte van de opslagopties. Hogere prestaties bieden extra reken en opslagbronnen ontworpen toodeliver steeds hogere doorvoer en capaciteit. U kunt Servicelagen en prestatieniveaus opslag zonder uitvaltijd dynamisch wijzigen. 
- **Basic**, **standaard** en **Premium** alle Servicelagen hebben een bedrijfstijd SLA van 99.99%, flexibele opties voor bedrijfscontinuïteit, beveiligingsfuncties en facturering per uur. 
- Hallo **Premium RS** laag biedt Hallo dezelfde prestatieniveaus hello Premium-laag met een lagere SLA omdat deze wordt uitgevoerd met een lager getal van redundante exemplaren dan een database in Hallo andere Servicelagen. Dus in Hallo-gebeurtenis van een service-fout, u toorecover uw database vanuit een back-up met up tooa 5 minuten vertraging moet mogelijk.

> [!IMPORTANT]
> Een Azure SQL database een gegarandeerd aantal resources opgehaald en Hallo verwachte prestatiekenmerken van de database worden niet beïnvloed door een andere database in Azure. 

## <a name="choosing-a-service-tier"></a>Het kiezen van een servicelaag
Hallo bevat volgende tabel voorbeelden van Hallo lagen die het meest geschikt voor werklasten met verschillende groepen van toepassingen.

| Servicelaag | Beoogde workloads |
| :--- | --- |
| **Basic** | Het meest geschikt voor een kleine database, die doorgaans één actieve bewerking tegelijk ondersteunt. Voorbeelden zijn onder meer databases die worden gebruikt voor ontwikkeling of testen, of kleinschalige, onregelmatig gebruikte toepassingen. |
| **Standard** |Hallo Ga-toooption voor cloudtoepassingen met een lage toomedium i/o-prestatievereisten, ondersteunt meerdere gelijktijdige query's. Voorbeelden zijn onder meer werkgroep- of webtoepassingen. |
| **Premium** | Ontwikkeld voor gebruik bij een hoog transactievolume met hoge I/O-prestatievereisten, waarbij ondersteuning wordt geboden voor veel gelijktijdige gebruikers. Voorbeelden zijn databases die bedrijfskritieke toepassingen ondersteunen. |
| **Premium-RS** | Ontworpen voor i/o-intensieve werkbelastingen die geen hoogste beschikbaarheidsgaranties Hallo vereisen. Voorbeelden omvatten het testen van werklasten met hoge prestaties of een analytische werkbelasting Hallo-database is waar geen Hallo-systeem van record. |
|||

U kunt individuele databases maken met specifieke bronnen binnen een servicelaag met een specifieke [prestatieniveau](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) of u kunt ook maken met databases binnen een [elastische SQL-groep](sql-database-service-tiers.md#elastic-pool-service-tiers-and-performance-in-edtus). In een elastische SQL-groep worden Hallo berekenings- en bronnen gedeeld door meerdere databases binnen één logische server. 

Bronnen beschikbaar voor individuele databases worden uitgedrukt in termen van's (Database Transaction Units) en resources voor een elastische pools SQL worden uitgedrukt in termen van elastische Database Transaction Units (edtu's). Zie voor meer informatie over dtu's en edtu's [wat zijn dtu's en edtu's?](sql-database-what-is-a-dtu.md).

toodecide start op een servicelaag door vast te stellen Hallo minimale databasefuncties die u nodig hebt:

| **Functies van de service tier** | **Basic** | **Standard** | **Premium** | **Premium-RS**|
| :-- | --: | --: | --: | --: |
| Grootte van maximaal één database | 2 GB | 250 GB | 4 TB *  | 500 GB  |
| Maximumgrootte van de elastische groep | 156 GB | 2,9 TB | 4 TB * | 750 GB |
| Maximale databasegrootte in een elastische pool | 2 GB | 250 GB | 500 GB | 500 GB |
| Maximum aantal databases per groep | 500  | 500 | 100 | 100 |
| Maximale individuele database dtu 's | 5 | 100 | 4000 | 1000 |
| Maximale aantal dtu's per database in een elastische pool | 5 | 3000 | 4000 | 1000 |
| De back-up bewaarperiode database | 7 dagen | 35 dagen | 35 dagen | 35 dagen |
||||||

> [!IMPORTANT]
> Opslag van too4 TB is momenteel beschikbaar is in de volgende regio's Hallo: ons East2, VS-West, Gov ons Virginia, West-Europa, Duitsland centraal, Zuid-Oost-Azië, Japan-Oost, Australië-Oost, Canada centraal en Canada-Oost. Zie [beperkingen van de huidige 4 TB](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize)
>

Als u de juiste servicelaag Hallo hebt vastgesteld, bent u gereed toodetermine Hallo prestatieniveau (Hallo aantal dtu's) en Hallo opslaghoeveelheid voor Hallo-database. 

- S2 en S3 prestatieniveaus in Hallo Hallo **standaard** laag zijn vaak een goed uitgangspunt. 
- Hallo voor databases met hoge CPU of i/o-vereisten, prestatieniveaus in Hallo **Premium** laag zijn Hallo juiste beginpunt. 
- Hallo **Premium** laag biedt meer CPU- en begint bij 10 x meer i/o vergeleken toohello hoogste prestatieniveau in Hallo **standaard** laag.
- Hallo **PremiumRS** laag biedt Hallo prestaties Hallo **Premium** laag, tegen lagere kosten, maar met een lagere SLA.

> [!IMPORTANT]
> Bekijk Hallo [SQL elastische pools](sql-database-elastic-pool.md) onderwerp voor informatie over het groeperen van databases in SQL-elastische Hallo opslaggroepen tooshare berekenings- en resources. Hallo rest van dit onderwerp richt zich op Servicelagen en prestatieniveaus van individuele databases.
>

## <a name="single-database-service-tiers-and-performance-levels"></a>Servicelagen en prestatieniveaus van afzonderlijke databases
Voor individuele databases zijn er meerdere prestatieniveaus en opslag bedragen binnen elke servicelaag. 

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

## <a name="scaling-up-or-scaling-down-a-single-database"></a>Omhoog of omlaag schalen in een individuele database

Wanneer u een servicelaag en prestatieniveau hebt gekozen, kunt u een individuele database dynamisch omhoog of omlaag schalen op basis van het feitelijke gebruik.  

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-dynamically-scale-up-or-scale-down/player]
>

Het wijzigen van Hallo laag en/of prestaties serviceniveau van een database maakt een replica van de oorspronkelijke database Hallo op Hallo nieuwe prestatieniveau en vervolgens wordt de replica toohello overgeschakeld verbindingen. Gegevens niet verloren tijdens dit proces maar tijdens Hallo korte ogenblikken wanneer we toohello replica overgeschakeld verbindingen toohello database zijn uitgeschakeld, zodat het aantal transacties tijdens de vlucht kunnen worden teruggedraaid. Hallo tijdsduur voor de switch Hallo via verschilt, maar wordt doorgaans onder 4 seconden is minder dan 30 seconden 99% Hallo tijd. Als er een groot aantal transacties tijdens de vlucht op Hallo momenteel verbindingen zijn uitgeschakeld, hello tijdsduur voor de switch Hallo via mogelijk ook langer.  

Hallo duur Hallo volledige omhoog schalen-proces is afhankelijk van de grootte van beide Hallo en servicelaag Hallo database vóór en na Hallo wijzigen. Een 250GB-database die wordt gewijzigd naar, van of binnen een Standard-servicelaag, zou bijvoorbeeld binnen zes uur voltooid moeten zijn. Voor een database Hallo hetzelfde formaat dat veranderende prestatieniveaus binnen de Premium servicecategorie Hallo moet uitvoeren binnen drie uur.

> [!TIP]
> toocheck van de status van een doorlopende SQL-database schalen bewerking hello, kunt u Hallo query te volgen: ```select * from sys.dm_operation_status```.
>

* Als u tooa hogere laag of prestaties serviceniveau bijwerkt, wordt de maximale databasegrootte Hallo niet verhogen tenzij u expliciet een maximum groter opgeeft.
* een database toodowngrade, Hallo-database moet kleiner zijn dan Hallo maximaal toegestane grootte van de servicelaag Hallo-doel. 
* Bij een upgrade van een database met [geo-replicatie](sql-database-geo-replication-portal.md) ingeschakeld, de prestatielaag secundaire databases toohello gewenste upgraden voordat u de upgrade Hallo primaire database (algemene richtlijnen). Bij het upgraden van andere tooa is editie ugrading Hallo secundaire database eerst vereist. 
* Wanneer een database met downgraden [geo-replicatie](sql-database-geo-replication-portal.md) ingeschakeld, de prestatielaag van primaire databases toohello gewenste downgrade voor u een downgrade Hallo secundaire database (algemene richtlijnen). Wanneer downgraden tooa andere editie downgraden Hallo primaire database eerst is vereist. 

* Hallo terugzetten serviceaanbiedingen zijn verschillend voor verschillende Servicelagen Hallo. Als u toohello zijn downgraden **Basic** laag, hebt u een lagere back-up bewaarperiode - Zie [back-ups van Azure SQL Database](sql-database-automated-backups.md).
* Eigenschappen van nieuwe Hallo voor Hallo-database worden niet toegepast totdat Hallo wijzigingen voltooid zijn.


## <a name="current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize"></a>Huidige beperkingen van P11 en P15 databases met 4 TB maxsize

Een maximale grootte van 4 TB voor P11 en P15 database wordt ondersteund in sommige regio's (zoals eerder besproken). Hallo volgende overwegingen en beperkingen van toepassing tooP11 en P15 databases met 4 TB maxsize:

- Als u kiest Hallo 4 TB maxsize optie bij het maken van een database (met behulp van een waarde van 4 TB en 4096 GB), maken Hallo opdracht mislukt met een fout als Hallo-database in een niet-ondersteunde regio is ingericht.
- Voor bestaande P11 en P15 databases zich bevinden in een Hallo ondersteunde regio's, verhoogt u Hallo maxsize opslag too4 TB. Dit kan worden gecontroleerd met behulp van Hallo [DATABASEPROPERTYEX Selecteer](https://msdn.microsoft.com/library/ms186823.aspx) of door de grootte van de database in Azure-portal Hallo Hallo te bekijken. Upgraden van een bestaande P11 of P15 kan database alleen worden uitgevoerd door een principal-aanmelding op serverniveau of door leden van Hallo dbmanager-databaserol. 
- Als een upgrade bewerking wordt uitgevoerd in de configuratie van een ondersteunde regio Hallo onmiddellijk bijgewerkt. tijdens het upgradeproces Hallo blijft Hallo database online. Echter, u Hallo volledige kan niet gebruikmaken van 4 TB aan opslag totdat de werkelijke databasebestanden Hallo zijn bijgewerkt toohello nieuwe maxsize. Hallo-lengte van de tijd die nodig is afhankelijk van op grootte op Hallo van Hallo-database wordt bijgewerkt.  
- Bij het maken of bijwerken van een database P11 of P15, kunt u alleen kiezen tussen 1 TB en 4 TB maxsize. Tussenliggende opslaggrootte worden momenteel niet ondersteund. Bij het maken van een P11/P15 is Hallo standaard opslagoptie van 1 TB vooraf geselecteerd. Voor de databases zich bevinden in een Hallo ondersteunde regio's, verhoogt u Hallo opslag maximale too4TB voor één nieuwe of bestaande database. Voor alle andere regio's, kan niet maximale grootte worden verhoogd tot boven 1 TB. Hallo prijs verandert niet wanneer u opgenomen opslag van 4 TB selecteert.
- Hallo 4 TB database maxsize kan niet worden gewijzigd too1 TB zelfs als Hallo werkelijke opslag gebruikt lager dan 1 TB is. U kunt niet dus een P11 - 4 TB/P15 - 4 TB tooa P11 - 1 TB/P15 - 1 TB of een laag met lagere prestaties bijvoorbeeld tooP1 P6 downgraden) totdat er extra opslagopties voor Hallo rest Hallo prestatielagen bieden. Deze beperking geldt ook toohello terugzetten en kopiëren scenario's punt in tijd, inclusief geo-restore lange-termijn-back-up-bewaren en database-exemplaar. Wanneer een database met de optie voor Hallo 4 TB is geconfigureerd, moeten alle bewerkingen voor het herstellen van deze database worden uitgevoerd in een P11/P15 met 4 TB maxsize.
- Als maken of bijwerken van een database P11/P15 in een niet-ondersteunde regio hello maakt of upgrade is mislukt met de Hallo volgende foutbericht weergegeven: **P11 en P15-database met too4TB van opslag zijn beschikbaar in ons East2, VS-West, Gov ons-Virginia West-Europa, Duitsland centraal, Zuidoost-Azië, Japan-Oost, Australië-Oost, Canada centraal en Canada-Oost.**
- Voor scenario's van actieve geo-replicatie:
   - Instellen van een relatie geo-replicatie: als de primaire database Hallo P11 of P15, Hallo secondary(ies) ook moet P11 of P15; lagere prestatielagen worden geweigerd als de secundaire replica's omdat ze niet kunnen ondersteunen van 4 TB.
   - Upgraden Hallo primaire database in een relatie geo-replicatie: Hallo dezelfde op de secundaire database Hallo wijzigen Hallo maxsize too4 TB op een primaire database wijzigen activeert. Beide upgrades moeten zijn gelukt om de wijziging Hallo op Hallo primaire tootake kracht zijn. Beperkingen voor Hallo 4TB optie regio toepassen (Zie hierboven). Als secundaire Hallo zich in een regio die geen ondersteuning biedt voor 4 TB, is niet primair Hallo bijgewerkt.
- Gebruik Hallo Import/Export-service voor het laden van P11 - 4TB/P15 - 4TB databases wordt niet ondersteund. SqlPackage.exe te gebruiken[importeren](sql-database-import.md) en [exporteren](sql-database-export.md) gegevens.

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-portal"></a>Beheren van één database Servicelagen en prestatieniveaus met hello Azure-portal

tooset of wijzig Hallo servicelaag, prestatieniveau of opslagruimte voor een nieuwe of bestaande Azure SQL database met behulp van hello Azure-portal openen Hallo **prestaties configureren** venster voor de database door te klikken op  **Prijscategorie (schaal dtu's)** : zoals wordt weergegeven in de volgende schermafbeelding Hallo. 

- Instellen of wijzigen van de servicelaag Hallo door het selecteren van de servicelaag Hallo voor uw workload. 
- Instellen of wijzigen van het prestatieniveau hello (**dtu's**) in een servicelaag met Hallo **DTU** schuifregelaar.
- Instellen of wijzigen van Hallo opslaghoeveelheid voor prestatieniveau Hallo Hallo met **opslag** schuifregelaar. 

  ![Prijscategorie en prestatieniveau serviceniveau configureren](./media/sql-database-service-tiers/service-tier-performance-level.png)

> [!IMPORTANT]
> Bekijk [huidige beperkingen van P11 en P15 databases met 4 TB maxsize](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize) bij het selecteren van een servicelaag P11 of P15.
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-powershell"></a>Individuele database Servicelagen en prestatieniveaus met behulp van PowerShell beheren

tooset of wijzig Azure SQL-databases Servicelagen en prestatieniveaus opslaghoeveelheid met behulp van PowerShell, gebruikt Hallo volgende PowerShell-cmdlets. Als u tooinstall moet of een upgrade van PowerShell, raadpleegt u [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps). 

| Cmdlet | Beschrijving |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Maakt een database |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Een of meer databases opgehaald|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Stelt eigenschappen van een database of een bestaande database is verplaatst naar een elastische pool|


> [!TIP]
> Zie voor een PowerShell-voorbeeldscript die bewaakt Hallo maatstaven voor prestaties van een database, op schaal tooa hoger prestatieniveau en een waarschuwingsregel maakt op een van de maatstaven voor prestaties Hallo [bewaken en schalen van een enkele SQL database met PowerShell](scripts/sql-database-monitor-and-scale-database-powershell.md).

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-cli"></a>Beheren van één database Servicelagen en prestatieniveaus hello Azure CLI gebruiken

tooset of wijzig Servicelagen van Azure SQL-databases, prestatieniveaus en opslaghoeveelheid met hello Azure CLI, gebruikt u de volgende Hallo [Azure CLI SQL Database](/cli/azure/sql/db) opdrachten. Gebruik Hallo [Cloud Shell](/azure/cloud-shell/overview) toorun Hallo CLI in uw browser of [installeren](/cli/azure/install-azure-cli) op Mac OS-, Linux- of Windows. Zie voor het maken en beheren van de elastische pools SQL, [elastische pools](sql-database-elastic-pool.md).

| Cmdlet | Beschrijving |
| --- | --- |
|[AZ sql-database maken](/cli/azure/sql/db#create) |Maakt een database|
|[AZ sql db-lijst](/cli/azure/sql/db#list)|Geeft een lijst van alle databases en datawarehouses in een server of alle databases in een elastische pool|
|[AZ sql db-edities](/cli/azure/sql/db#list-editions)|Een lijst met beschikbare service doelstellingen en opslaglimieten|
|[AZ sql db lijst-gebruik](/cli/azure/sql/db#list-usages)|Retourneert het gebruik van de database|
|[AZ sql db weergeven](/cli/azure/sql/db#show)|Een database of de data warehouse opgehaald|
|[AZ sql database-update](/cli/azure/sql/db#update)|Een database bijwerkt|

> [!TIP]
> Zie voor een voorbeeldscript Azure CLI die een enkele Azure SQL database tooa verschillende prestatieniveau schaalbaar nadat het opvragen van informatie over de Hallo grootte van de database Hallo [gebruik CLI toomonitor en schaal één SQL-database](scripts/sql-database-monitor-and-scale-database-cli.md).
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-transact-sql"></a>Beheren van één database Servicelagen en prestatieniveaus met Transact-SQL

tooset of wijzig Azure SQL-databases Servicelagen en prestatieniveaus opslaghoeveelheid met Transact-SQL, gebruik Hallo T-SQL-opdrachten te volgen. U kunt deze opdrachten hello Azure-portal met de opdracht [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), of een ander programma dat kan verbinding maken met tooan Azure SQL Database-server en doorgeven Transact-SQL de opdrachten. 

| Opdracht | Beschrijving |
| --- | --- |
|[DATABASE (Azure SQL Database) maken](/sql/t-sql/statements/create-database-azure-sql-database)|Maakt een nieuwe database. U moet verbonden toohello hoofddatabase toocreate een nieuwe database.|
| [ALTER DATABASE (Azure SQL Database)](/sql/t-sql/statements/alter-database-azure-sql-database) |Hiermee wijzigt u een Azure SQL database. |
|[sys.database_service_objectives (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Retourneert Hallo edition (servicelaag), servicedoelstelling (prijscategorie) en de naam van de elastische groep, indien aanwezig, voor een Azure SQL database of een Azure SQL Data Warehouse. Als u aangemeld bent op de hoofddatabase toohello in een Azure SQL Database-server, retourneert de informatie voor alle databases. Voor Azure SQL Data Warehouse moet u verbonden toohello hoofddatabase.|
|[sys.database_usage (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-usage-azure-sql-database)|Geeft een lijst Hallo number, type en duur van de databases op een Azure SQL Database-server.|

Hallo volgende voorbeeld ziet u Hallo maxsize wordt gewijzigd met de opdracht ALTER DATABASE Hallo:

 ```sql
ALTER DATABASE <myDatabaseName> 
   MODIFY (MAXSIZE = 4096 GB);
```

## <a name="manage-single-databases-using-hello-rest-api"></a>Beheren van individuele databases met Hallo REST-API

Zie tooset of wijzig Servicelagen van Azure SQL-databases, prestatieniveaus en opslaghoeveelheid Hallo REST API, gebruik [REST-API van Azure SQL Database](/rest/api/sql/).

## <a name="next-steps"></a>Volgende stappen

* Meer informatie over [dtu's](sql-database-what-is-a-dtu.md).
* Zie toolearn over het DTU-gebruik controleren [bewaking en prestatieafstemming](sql-database-troubleshoot-performance.md).

