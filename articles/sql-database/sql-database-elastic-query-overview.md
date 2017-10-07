---
title: overzicht van de elastische query aaaAzure SQL Database | Microsoft Docs
description: Overzicht van Hallo elastische query functie
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: a8bf0e2c-bc74-44d0-9b1e-bcc9a6aa2e33
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: mlandzic
ms.openlocfilehash: db17f551882cfcae0da67fdda12708baeb6db81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-elastic-query-overview-preview"></a>Overzicht Azure SQL Database elastische query (preview)
Hallo elastische query-functie (in preview) kunt u toorun een verspreid over meerdere databases in Azure SQL Database Transact-SQL-query. Hiermee kunt u tooperform cross-databasequery's tooaccess externe tabellen en tooconnect Microsoft en derden hulpprogramma's (Excel, Power BI, Tableau, enz.) tooquery over gegevenslagen met meerdere databases. Met deze functie kunt u query's toolarge gegevenslagen in SQL-Database uitbreiden en visualiseren Hallo resultaten in business intelligence (BI)-rapporten.


## <a name="why-use-elastic-queries"></a>Waarom elastische query's gebruiken?

**Azure SQL Database**

Vragen over Azure SQL-databases volledig in T-SQL. Hierdoor kan alleen-lezen query's naar externe databases. Dit biedt een optie voor het huidige on-premises SQL Server toomigrate-toepassingen voor klanten met drie en vierkleuren part namen of gekoppelde server tooSQL DB.

**Beschikbaar in standard-laag**

Elastische query wordt ondersteund op Hallo standaard prestatielaag in toevoeging toohello Premium prestatielaag. Zie Hallo sectie over Preview beperkingen hieronder op prestaties beperkingen voor lagere prestatielagen.

**Push tooremote databases**

Elastische query's kunnen nu toohello externe databases van SQL-parameters voor de uitvoering van push.

**Opgeslagen procedure kan worden uitgevoerd**

Uitvoeren van extern opgeslagen procedureaanroepen of externe functies met [sp\_uitvoeren \_externe](https://msdn.microsoft.com/library/mt703714).

**Flexibiliteit**

Externe tabellen met elastische query kunnen nu tooremote tabellen met een ander schema of de tabelnaam verwijzen.

## <a name="elastic-query-scenarios"></a>Elastische query scenario 's

Hallo-doel is toofacilitate scenario's waarbij meerdere databases rijen in een enkel algehele resultaat bijdragen opvragen. Hallo query kan ofwel worden samengesteld door Hallo gebruiker of toepassing rechtstreeks of indirect via hulpprogramma's die verbonden toohello database zijn. Dit is vooral nuttig bij het maken van rapporten met commerciële BI of gegevens integratie-hulpprogramma's, of een toepassing die niet kan worden gewijzigd. U kunt met een elastische query opvragen via verschillende databases met Hallo vertrouwde SQL Server-connectiviteit ervaring in hulpprogramma's zoals Excel, Power BI, Tableau of Hiermee.
Een elastische query kunt eenvoudig toegang tooan hele verzameling-databases via query's die zijn uitgegeven door SQL Server Management Studio of Visual Studio en vereenvoudigt tussen meerdere databases opvragen van Entity Framework of andere ORM-omgevingen. Afbeelding 1 toont een scenario waarbij een bestaande cloud toepassing (waarin Hallo [clientbibliotheek voor elastische database](sql-database-elastic-database-client-library.md)) bouwt voort op de gegevens van een uitgebreide laag en een elastische query wordt gebruikt voor het melden van meerdere databases.

**Afbeelding 1** elastische query gebruikt op de uitgebreide gegevenslaag

![Elastische query gebruikt op de uitgebreide gegevenslaag][1]

Klant-scenario's voor de elastische query worden gekenmerkt door Hallo topologieën te volgen:

* **Verticale partities - query's voor meerdere databases** (topologie 1): Hallo gegevens verticaal is gepartitioneerd tussen een aantal databases in een gegevenslaag. Normaal gesproken zich verschillende sets van tabellen op verschillende databases. Dat betekent dat Hallo-schema verschilt van andere databases. Alle tabellen voor inventarisatie zijn bijvoorbeeld op de ene database terwijl alle accounting-gerelateerde tabellen op een tweede database zijn. Algemene gebruiksvoorbeelden met deze topologie vereisen een tooquery via of toocompile rapporten tussen tabellen in verschillende databases.
* **Horizontale partitionering - Sharding** (topologie 2): de gegevens zijn gepartitioneerd horizontaal toodistribute rijen in een uitgebreid uit gegevens laag. Met deze methode is Hallo schema identiek zijn op alle deelnemende databases. Deze aanpak wordt ook 'sharding' genoemd. Sharding kan worden uitgevoerd en beheerd via (1) Hallo elastische database extra bibliotheken of (2) self-sharding. Een elastische query is gebruikt tooquery of compileren rapporten over veel shards.

> [!NOTE]
> Elastische query werkt het beste voor incidentele reporting scenario's waar de meeste Hallo verwerking kan worden uitgevoerd op Hallo gegevenslaag. Voor zware reporting werklasten of datawarehousescenario's met meer complexe query's ook overwegen [Azure SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
>  

## <a name="vertical-partitioning---cross-database-queries"></a>Verticale partities - query's met meerdere databases

toobegin coderen, Zie [aan de slag met cross-databasequery (verticale partities)](sql-database-elastic-query-getting-started-vertical.md).

Een elastische query kan worden gebruikt toomake gegevens in een SQL-database beschikbaar tooother SQL-databases. Hierdoor kunnen query's van één database toorefer tootables in een andere externe SQL-database. de eerste stap Hallo is toodefine een externe gegevensbron voor elke externe database. Hallo externe gegevensbron is gedefinieerd in de lokale database Hallo van waaruit u toogain toegang tootables zich op de externe database hello wilt. Er zijn geen wijzigingen nodig op Hallo externe database. Voor typische verticale partities scenario's waarbij verschillende databases verschillende schema's, elastische query's worden gebruikt tooimplement algemene gebruiksvoorbeelden zoals toegang tot tooreference gegevens en uitvoeren van query's voor meerdere databases.

> [!IMPORTANT]
> U moet beschikken over een externe gegevensbron ALTER machtiging. Deze machtiging is opgenomen in de machtiging ALTER DATABASE Hallo. EEN externe gegevensbron ALTER machtigingen zijn vereist toorefer toohello onderliggende gegevensbron.
>

**Referentiegegevens**: Hallo-topologie wordt gebruikt voor gegevensbeheer verwijzing. In Hallo afbeelding hieronder, twee tabellen (T1 en T2) referentiegegevens worden bewaard op een specifieke database. Met een elastische query, u kunt nu toegang tot tabellen T1 en T2 op afstand uit andere databases, zoals weergegeven in afbeelding Hallo. Topologie gebruik 1 als verwijzingsdimensies kleine of externe query's in de verwijzingstabel zijn hebben selectief predicaten.

**Afbeelding 2** verticale partitioneren: gebruik elastische query tooquery referentiegegevens

![Verticale partities - elastische query tooquery referentiegegevens gebruiken][3]

**Opvragen van meerdere databases**: elastische query inschakelen gebruiksvoorbeelden waarvoor het uitvoeren van query's in verschillende SQL-databases. Afbeelding 3 ziet u vier verschillende databases: CRM, inventaris, HR en producten. Query's uitgevoerd in een van de databases Hallo moeten ook een toegang tot tooone of alle andere databases Hallo. Een elastische query kunt u de database voor deze aanvraag configureren door het uitvoeren van een paar eenvoudige DDL-componenten op elk van de vier databases Hallo. Toegang tooa externe tabel is na deze eenmalige configuratie net zo eenvoudig als het lokale tabel tooa verwijst van T-SQL-query's of van uw BI-hulpprogramma's. Deze aanpak wordt aanbevolen als Hallo externe query's niet veel resultaten retourneren.

**Afbeelding 3** verticale partities: met elastische query tooquery via verschillende databases

![Verticale partities: met elastische query tooquery via verschillende databases][4]

Hallo volgt configureren elastische databasequery's voor verticale partities scenario's waarvoor toegang tooa tabel zich bevindt op externe SQL-databases met Hallo dezelfde schema:

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) mymasterkey
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) mycredential
* [CREATE/DROP EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx) mydatasource van het type **RDBMS**
* [CREATE/DROP externe tabel](https://msdn.microsoft.com/library/dn935021.aspx) mytable

U kunt na het uitvoeren van Hallo DDL-componenten Hallo externe tabel "MijnTabel" openen alsof het een lokale tabel. Azure SQL Database automatisch Hiermee opent u een externe verbinding toohello-database, verwerkt uw aanvraag op de externe database Hallo en Hallo als resultaat gegeven.

## <a name="horizontal-partitioning---sharding"></a>Horizontale partitioneren - sharding
Het gebruik van elastische query tooperform rapportagetaken via een shard, dat wil zeggen, horizontaal is gepartitioneerd, gegevenslaag vereist een [elastische database shard-toewijzing](sql-database-elastic-scale-shard-map-management.md) toorepresent Hallo databases van Hallo gegevenslaag. Normaal gesproken alleen een enkele shard-toewijzing in dit scenario wordt gebruikt en een specifieke database met elastische querymogelijkheden (hoofdknooppunt) fungeert als Hallo toegangspunt voor het melden van query's. Alleen deze specifieke database moet toegang toohello shard-toewijzing. Afbeelding 4 ziet u deze topologie en de configuratie met Hallo elastische query database en shard-toewijzing. Hallo-databases in de gegevenslaag Hallo kunnen zijn van een Azure SQL Database versie of editie. Zie voor meer informatie over Hallo-clientbibliotheek voor elastische database en het maken van kaarten shard [Shard kaart management](sql-database-elastic-scale-shard-map-management.md).

**Afbeelding 4** horizontale partitioneren - elastische query gebruiken voor rapportage over de lagen van de gedeelde gegevens

![Horizontale partitioneren - elastische query gebruiken voor rapportage over de lagen van de gedeelde gegevens][5]

> [!NOTE]
> Elastische query uitvoeren op Database (hoofdknooppunt) kan afzonderlijke database of het Hallo kan ook dezelfde database die hosts Hallo shard-toewijzing. Welke configuratie u kiest, zorg ervoor dat die laag service en de prestaties van de database is hoog genoeg toohandle Hallo verwacht hoeveelheid aanmelding/queryaanvragen.

Hallo configureren volgt elastische databasequery's voor horizontale partitionering scenario's waarvoor toegang tooa set van de tabel die zich bevinden op (meestal) verschillende externe SQL-databases:

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) mymasterkey
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) mycredential
* Maak een [shard-toewijzing](sql-database-elastic-scale-shard-map-management.md) die de gegevenslaag Hallo-clientbibliotheek voor elastische database gebruiken.   
* [CREATE/DROP EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx) mydatasource van het type **SHARD_MAP_MANAGER**
* [CREATE/DROP externe tabel](https://msdn.microsoft.com/library/dn935021.aspx) mytable

Wanneer u deze stappen hebt uitgevoerd, kunt u Hallo horizontaal gepartitioneerde tabel "MijnTabel" openen alsof het een lokale tabel. Azure SQL Database automatisch wordt geopend meerdere parallelle verbindingen toohello externe databases waar Hallo tabellen fysiek zijn opgeslagen, verwerkt aanvragen voor externe databases Hallo Hallo en Hallo als resultaat gegeven.
Meer informatie over het Hallo-stappen die nodig zijn voor Hallo horizontale partitionering scenario vindt u [elastische query voor het partitioneren van de horizontale](sql-database-elastic-query-horizontal-partitioning.md).

toobegin coderen, Zie [aan de slag met elastische query voor horizontale partitioneren (sharding)](sql-database-elastic-query-getting-started.md).

## <a name="t-sql-querying"></a>T-SQL-query
Als u uw externe gegevensbronnen en uw externe tabellen hebt gedefinieerd, kunt u gewone SQL Server-verbinding tekenreeksen tooconnect toohello databases waar u uw externe tabellen gedefinieerd. Vervolgens kunt u uitvoeren T-SQL-instructies over de externe tabellen voor die verbinding met Hallo beperkingen die hieronder worden beschreven. U vindt meer informatie over en voorbeelden van T-SQL-query's in Hallo documentatie onderwerpen voor [horizontaal partitioneren](sql-database-elastic-query-horizontal-partitioning.md) en [verticale partities](sql-database-elastic-query-vertical-partitioning.md).

## <a name="connectivity-for-tools"></a>Connectiviteit voor hulpprogramma 's
U kunt reguliere tekenreeksen tooconnect van de SQL Server-verbinding gebruiken uw toepassingen en gegevens of BI integratie extra toodatabases waarvoor externe tabellen. Zorg ervoor dat SQL Server wordt ondersteund als een gegevensbron voor het hulpprogramma. Eenmaal zijn verbonden, raadpleegt u toohello elastische database en Hallo externe querytabellen in de database, net zoals u met een andere SQL Server-database doen zou dat u verbinding toowith uw hulpprogramma maakt.

> [!IMPORTANT]
> Verificatie met behulp van Azure Active Directory met elastische query's is momenteel niet ondersteund.
> 
> 

## <a name="cost"></a>Kosten
Elastische query is opgenomen in Hallo kosten van Azure SQL Database-databases. Denk eraan dat waar uw externe databases zich bevindt in een andere Datacenter dan Hallo elastische query endpoint-topologieën worden ondersteund, maar de uitgaande gegevens uit externe databases worden in rekening gebracht regular [Azure tarieven](https://azure.microsoft.com/pricing/details/data-transfers/).

## <a name="preview-limitations"></a>Preview-beperkingen
* Uw eerste elastische query uit te voeren kan duren tooa enkele minuten op Hallo standaard prestatielaag. Deze tijd is nodig tooload Hallo elastische queryfunctionaliteit; laden van de prestaties worden verbeterd met hogere prestatielagen.
* Scripts van externe gegevensbronnen of externe tabellen van SSMS of SSDT is nog niet ondersteund.
* Importeren/exporteren voor SQL database ondersteunt nog geen externe gegevensbronnen en externe tabellen. Als u toouse voor importeren/exporteren moet, deze objecten verwijderen voordat u exporteert en vervolgens opnieuw maken na het importeren.
* Elastische query ondersteunt momenteel alleen-lezentoegang tooexternal tabellen. U kunt alle functies van T-SQL echter gebruiken op Hallo database waarvoor Hallo externe tabel is gedefinieerd. Dit is handig in, bijvoorbeeld tijdelijke resultaten stand te houden met behulp van bijvoorbeeld selecteert < column_list > in < local_table > of toodefine opgeslagen procedures op Hallo elastische query uitvoeren op database die tooexternal tabellen verwijzen.
* Met uitzondering van nvarchar(max), worden LOB-typen niet ondersteund in definities van de externe tabel. Als tijdelijke oplossing kunt u een weergave op Hallo externe database die in nvarchar(max) Hallo LOB-typen cast maken, uw externe tabel via Hallo weergeven in plaats van de basistabel Hallo definiëren en vervolgens geconverteerd naar het oorspronkelijke LOB type Hallo in uw query's.
* Kolom statistieken over externe tabellen worden momenteel niet ondersteund. Tabellen statistieken worden ondersteund, maar moeten toobe die handmatig zijn gemaakt.

## <a name="feedback"></a>Feedback
Neem delen feedback over uw ervaringen met elastische query's met ons op de onderstaande Disqus Hallo MSDN-forums, of op Stackoverflow. We zijn geïnteresseerd in alle soorten feedback over Hallo-service (defecte producten, ruwe randen, functie hiaten).

## <a name="next-steps"></a>Volgende stappen

* Zie voor een verticale partitie zelfstudie [aan de slag met cross-databasequery (verticale partities)](sql-database-elastic-query-getting-started-vertical.md).
* Zie voor de syntaxis en voorbeelden query's voor verticaal gepartitioneerde gegevens [gegevens opvragen verticaal gepartitioneerd)](sql-database-elastic-query-vertical-partitioning.md)
* Zie voor een zelfstudie horizontaal partitioneren (sharding) [aan de slag met elastische query voor horizontale partitioneren (sharding)](sql-database-elastic-query-getting-started.md).
* Zie voor de syntaxis en voorbeelden query's voor horizontaal gepartitioneerde gegevens [gegevens opvragen horizontaal gepartitioneerd)](sql-database-elastic-query-horizontal-partitioning.md)
* Zie [sp\_uitvoeren \_externe](https://msdn.microsoft.com/library/mt703714) voor een opgeslagen procedure die een Transact-SQL-instructie op een enkele externe Azure SQL Database of een set van databases die fungeren als shards in een horizontale partitieschema wordt uitgevoerd.

<!--Image references-->
[1]: ./media/sql-database-elastic-query-overview/overview.png
[2]: ./media/sql-database-elastic-query-overview/topology1.png
[3]: ./media/sql-database-elastic-query-overview/vertpartrrefdata.png
[4]: ./media/sql-database-elastic-query-overview/verticalpartitioning.png
[5]: ./media/sql-database-elastic-query-overview/horizontalpartitioning.png

<!--anchors-->
