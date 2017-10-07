---
title: aaaScale uit een Azure SQL database | Microsoft Docs
description: Hoe toouse Hallo ShardMapManager, clientbibliotheek voor elastische database
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a>Databases met Hallo shard-toewijzing manager uitbreiden
tooeasily scale-out-databases op SQL Azure gebruiken een manager shard-toewijzing. Hallo shard-toewijzing manager is een speciale database waarin gegevens over alle shards (databases) in een set shard globale toewijzing worden bijgehouden. Hallo metagegevens kan een tooconnect toohello juiste toepassingsdatabase op basis van de waarde Hallo Hallo **sharding sleutel**. Bovendien elke shard in Hallo set bevat kaarten die Hallo lokale shard-gegevens bijhouden (ook wel **shardlets**). 

![Beheer van shard-kaart](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

Inzicht in hoe deze toewijzingen worden opgebouwd is essentieel tooshard kaart management. Dit wordt gedaan met behulp van Hallo [ShardMapManager klasse](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)vindt u in Hallo [clientbibliotheek voor elastische Database](sql-database-elastic-database-client-library.md) toomanage shard wordt toegewezen.  

## <a name="shard-maps-and-shard-mappings"></a>Shard-kaarten en shard-toewijzingen
U moet voor elke shard Hallo type shard-toewijzing toocreate selecteren. Hallo keuze is afhankelijk van Hallo database-architectuur: 

1. Één tenant per database  
2. Meerdere tenants per database (twee typen):
   1. Toewijzing van de lijst
   2. Bereik toewijzing

Voor een model voor één tenant, maakt u een **lijst toewijzing** shard-toewijzing. Hallo één tenant model wijst één database per tenant. Dit is een doeltreffend model voor SaaS-ontwikkelaars aangezien vereenvoudigt het beheer.

![Toewijzing van de lijst][1]

Hallo multitenant model wijst verschillende tenants tooa één database (en u kunt groepen van tenants verdelen over meerdere databases). Dit model gebruiken wanneer u verwacht dat elke tenant toohave kleine hoeveelheden gegevens nodig heeft. In dit model we een bereik van het gebruik van tenants tooa database toewijzen **bereik toewijzing**. 

![Bereik toewijzing][2]

Of u kunt implementeren met een multitenant database model met een *lijst toewijzing* tooassign meerdere tenants tooa één database. Bijvoorbeeld, DB1 is gebruikte toostore informatie over de tenant-id 1 en 5 en DB2 slaat gegevens voor de tenant 7- en 10. 

![Muliple tenants in één DB][3] 

### <a name="supported-net-types-for-sharding-keys"></a>Ondersteunde .net-typen voor sharding-sleutels
Elastische Scale ondersteuning Hallo volgende .net Framework-typen als sharding sleutels:

* geheel getal
* lang
* GUID
* Byte]  
* Datum/tijd
* TimeSpan
* DateTimeOffset

### <a name="list-and-range-shard-maps"></a>Lijst met en bereik shard-kaarten
Shard maps kunnen worden opgesteld met **lijsten met afzonderlijke sharding waarden sleutel**, of ze kunnen worden opgesteld met **bereiken van sharding waarden sleutel**. 

### <a name="list-shard-maps"></a>Lijst shard maps
**Shards** bevatten **shardlets** en Hallo toewijzing van shardlets tooshards wordt onderhouden door een shard-toewijzing. Een **lijst shard-toewijzing** is een koppeling tussen Hallo afzonderlijke sleutelwaarden die Hallo shardlets identificeren en Hallo-databases die als shards fungeren.  **Lijst met toewijzingen** zijn expliciete en andere sleutelwaarden kunnen worden toegewezen toohello dezelfde database. Bijvoorbeeld: sleutel 1 toegewezen tooDatabase A en sleutelwaarden 3 en 6 verwijst naar Database B.

| Sleutel | Shard-locatie |
| --- | --- |
| 1 |Database_A |
| 3 |Database_B |
| 4 |Database_C |
| 6 |Database_B |
| ... |... |

### <a name="range-shard-maps"></a>Bereik shard maps
In een **bereik shard-toewijzing**, Hallo sleutel bereik is beschreven door een combinatie van **[lage waarde, hoogwaardige)** waar Hallo *lage waarde* is de minimale sleutel Hallo in Hallo bereik en Hallo *Waardevolle* Hallo eerste waarde hoger is dan Hallo bereik. 

Bijvoorbeeld: **[0, 100)** bestaat uit alle gehele getallen groter dan of gelijk 0 en kleiner dan 100. Houd er rekening mee dat meerdere adresbereiken kunnen punt toohello dezelfde database en niet-aaneengesloten bereiken wordt uitgevoerd, worden ondersteund (bijvoorbeeld [100,200) en [400,600) beide C punt tooDatabase in Hallo voorbeeld hieronder.)

| Sleutel | Shard-locatie |
| --- | --- |
| [1,50) |Database_A |
| [50,100) |Database_B |
| [100,200) |Database_C |
| [400,600) |Database_C |
| ... |... |

Hallo-tabellen die hierboven is een conceptueel voorbeeld van een **ShardMap** object. Elke rij is een eenvoudig voorbeeld van een persoon **PointMapping** (voor Hallo lijst shard-toewijzing) of **RangeMapping** (voor Hallo bereik shard-toewijzing) object.

## <a name="shard-map-manager"></a>Beheer van shard-kaart
In het Hallo-clientbibliotheek is Hallo shard-toewijzing manager een verzameling van shard-kaarten. Hallo gegevens die worden beheerd door een **ShardMapManager** exemplaar wordt opgeslagen op drie locaties: 

1. **Globale Shard-toewijzing (GSM)**: U een database tooserve opgeven als Hallo-opslagplaats voor alle shard-kaarten en toewijzingen. Speciale tabellen en opgeslagen procedures worden automatisch gemaakt voor toomanage Hallo informatie. Dit is meestal een kleine database en licht geopend en mag niet worden gebruikt voor andere behoeften van de toepassing hello. Hallo tabellen zijn in een speciale schema met de naam **__ShardManagement**. 
2. **Lokale Shard-toewijzing (LSM)**: elke database die u opgeeft toobe een shard is gewijzigd toocontain verschillende kleine tabellen en speciale opgeslagen procedures die bevatten en shard kaart informatie specifieke toothat shard beheren. Deze informatie is redundant met Hallo-informatie in Hallo GSM en kunnen Hallo toovalidate in de cache opgeslagen shard kaart toepassingsinformatie zonder belasting op Hallo GSM; worden geplaatst Hallo-toepassing gebruikt Hallo LSM toodetermine als een toewijzing in de cache nog geldig is. Hallo tabellen bijbehorende toohello LSM op elke shard bevinden zich ook in Hallo schema **__ShardManagement**.
3. **Toepassingscache**: elke toepassing exemplaar toegang tot een **ShardMapManager** object onderhoudt een lokale cache in het geheugen van de toewijzingen. Routinggegevens die onlangs zijn opgehaald worden opgeslagen. 

## <a name="constructing-a-shardmapmanager"></a>Een ShardMapManager maken
Een **ShardMapManager** -object is gemaakt met behulp van een [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) patroon. Hallo  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  methode heeft referenties (inclusief Hallo-servernaam en databasenaam houden Hallo GSM) in Hallo vorm van een  **ConnectionString** en retourneert een exemplaar van een **ShardMapManager**.  

**Opmerking:** hello **ShardMapManager** slechts één keer per app-domein, Hallo initialisatie van de code voor een toepassing moet worden gemaakt. Het maken van extra exemplaren van ShardMapManager in Hallo hetzelfde appdomain resulteert in meer geheugen en CPU-gebruik van de toepassing hello. Een **ShardMapManager** mag een onbeperkt aantal shard-kaarten. Bij een enkele shard-toewijzing is mogelijk niet voldoende is voor veel toepassingen, zijn er keer wanneer verschillende sets van databases worden gebruikt voor verschillende schema of voor unieke doeleinden; in deze gevallen mogelijk meerdere shard-kaarten beter. 

In deze code probeert een toepassing een bestaande tooopen **ShardMapManager** Hello [TryGetSqlShardMapManager methode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).  Als objecten die een Global **ShardMapManager** (GSM) nog niet bestaat in de database hello, Hallo-clientbibliotheek maakt ze er met Hallo [CreateSqlShardMapManager methode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

Als alternatief kunt u Powershell toocreate een nieuwe Manager van de Shard-toewijzing. Een voorbeeld is beschikbaar [hier](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="get-a-rangeshardmap-or-listshardmap"></a>Een RangeShardMap of ListShardMap ophalen
Na het maken van een shard kaart manager, kunt u krijgen Hallo [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) of [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) met Hallo [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), Hallo [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), of Hallo [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) methode.

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a>Beheerdersrechten shard-kaart
Toepassingen beheren en manipuleren van shard-kaarten zijn anders dan die Hallo shard maps tooroute verbindingen gebruiken. 

tooadminister shard-toewijzingen (toevoegen of wijzigen shards, shard-kaarten, shard-toewijzingen, enz.) moet u Hallo instantiëren **ShardMapManager** met **referenties die lezen/schrijven-bevoegdheden op beide Hallo GSM-database en op elk database die als een shard fungeert**. Hallo referenties moeten ervoor zorgen dat voor schrijfacties tegen Hallo tabellen in beide Hallo GSM en LSM shard kaart informatie wordt ingevoerd of gewijzigd, ook als voor het maken van tabellen LSM op nieuwe shards.  

Zie [referenties gebruikt tooaccess Hallo elastische Database-clientbibliotheek](sql-database-elastic-scale-manage-credentials.md).

### <a name="only-metadata-affected"></a>Alleen de metagegevens die van invloed op een
Methoden voor het invullen van of het wijzigen van Hallo **ShardMapManager** gegevens Hallo gebruikersgegevens opgeslagen in Hallo shards zelf niet wijzigen. Bijvoorbeeld, methoden zoals **CreateShard**, **DeleteShard**, **UpdateMapping**, enzovoort. invloed hebben op Hallo shard kaart bestaan alleen uit metagegevens. Ze niet verwijdert, toevoegen of wijzigen van de gebruikersgegevens in Hallo shards. In plaats daarvan deze methoden zijn ontworpen toobe gebruikt in combinatie met afzonderlijke bewerkingen u toocreate uitvoeren of werkelijke databases verwijderen of verplaatsen rijen uit één shard tooanother toorebalance een shard-omgeving.  (Hallo **gesplitste samenvoegen** hulpprogramma dat wordt geleverd met hulpprogramma's voor elastische database wordt gebruikgemaakt van deze API's samen met het organiseren van de daadwerkelijke gegevensverplaatsing tussen shards.) Zie [vergroten/verkleinen met Hallo elastische Database split-samenvoegen hulpprogramma](sql-database-elastic-scale-overview-split-and-merge.md).

## <a name="populating-a-shard-map-example"></a>Voorbeeld van een shard-toewijzing in te vullen
Een van de voorbeeldreeks bewerkingen toopopulate een specifieke shard-toewijzing wordt hieronder weergegeven. Hallo code voert de volgende stappen uit: 

1. Een nieuwe shard-toewijzing wordt gemaakt binnen een manager shard-toewijzing. 
2. Hallo-metagegevens voor twee verschillende shards toegevoegd toohello shard-toewijzing. 
3. Een aantal belangrijke bereik toewijzingen worden toegevoegd en hello algehele inhoud van Hallo shard-toewijzing wordt weergegeven. 

Hallo-code wordt geschreven, zodat het Hallo-methode kan opnieuw worden gestart als er een fout optreedt. Elke aanvraag wordt gecontroleerd of een shard of toewijzing al bestaat, voordat u probeert toocreate deze. Hallo code wordt ervan uitgegaan dat de naam van databases **sample_shard_0**, **sample_shard_1** en **sample_shard_2** al zijn gemaakt in Hallo server waarnaar wordt verwezen door de tekenreeks **shardServer**. 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List hello shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

Als alternatief kunt u PowerShell-scripts tooachieve Hallo resultaat hetzelfde. Sommige Hallo voorbeeld PowerShell-voorbeelden zijn beschikbaar [hier](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).     

Zodra de shard-kaarten zijn ingevuld, wordt data access-toepassingen kunnen worden gemaakt of aangepast toowork met Hallo maps. In te vullen of manipuleren van Hallo maps moet zich niet voor pas weer **kaart indeling** moet toochange.  

## <a name="data-dependent-routing"></a>Gegevensafhankelijke routering
Hallo shard-toewijzing manager zal meest worden gebruikt in toepassingen waarvoor verbindingen tooperform Hallo app-specifieke gegevens databasebewerkingen. Deze verbindingen moeten worden gekoppeld aan de juiste database Hallo. Dit staat bekend als **gegevensafhankelijke routering**. Exemplaar maken van een object shard kaart manager van Hallo-factory met referenties die alleen-lezen toegang op Hallo GSM database hebben voor deze toepassingen. Afzonderlijke aanvragen voor latere verbindingen Geef referenties op die nodig zijn voor het verbinden van toohello juiste shard-database.

Houd er rekening mee dat deze toepassingen (met behulp van **ShardMapManager** geopend met alleen-lezen referenties) kan geen wijzigingen aanbrengen toohello maps of toewijzingen. Maak voor die behoeften beheerdersrechten-specifieke toepassingen of PowerShell-scripts die hogere bevoegdheden referenties opgeven, zoals eerder besproken. Zie [referenties gebruikt tooaccess Hallo elastische Database-clientbibliotheek](sql-database-elastic-scale-manage-credentials.md).

Zie voor meer informatie [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md). 

## <a name="modifying-a-shard-map"></a>Wijzigen van een shard-toewijzing
Een shard-toewijzing kan op verschillende manieren worden gewijzigd. Alle van de volgende methoden Hallo Hallo metagegevens beschrijven Hallo shards en hun toewijzingen wijzigen maar ze gegevens binnen Hallo shards niet fysiek aanpassen, of komen ze maken of verwijderen van de werkelijke Hallo-databases.  Aantal Hallo-bewerkingen op Hallo shard-toewijzing die hieronder worden beschreven wellicht toobe coördinatie met beheeracties die gegevens fysiek verplaatsen of die toevoegen en verwijderen van de databases die fungeren als shards.

Deze methoden samenwerken als bouwstenen Hallo beschikbaar voor het wijzigen van Hallo algemene distributie van gegevens in uw databaseomgeving shard-.  

* tooadd of verwijder shards: Gebruik  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  en  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  Hallo [Shardmap klasse](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx). 
  
    Hallo moeten-server en database die vertegenwoordigt Hallo doel shard al bestaan voor deze bewerkingen tooexecute. Deze methoden geen invloed heeft op Hallo databases zelf, alleen op metagegevens in Hallo shard-toewijzing.
* toocreate of verwijder punten of adresbereiken die zijn toegewezen toohello shards: Gebruik  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  Hallo [RangeShardMapping klasse](https://msdn.microsoft.com/library/azure/dn807318.aspx), en  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  Hallo [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)
  
    Veel verschillende punten of adresbereiken kunnen worden toegewezen toohello dezelfde shard. Deze methoden zijn alleen van invloed op de metagegevens - ze hebben geen invloed op alle gegevens die al aanwezig in shards. Als gegevens verwijderd uit de database Hallo in volgorde toobe consistent zijn met toobe moeten **DeleteMapping** bewerkingen, moet u tooperform deze bewerkingen afzonderlijk, maar in combinatie met behulp van deze methoden.  
* de bestaande bereiken toosplit in twee of aangrenzende bereiken samenvoegen tot één: Gebruik  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  en  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.  
  
    Let op te splitsen en samenvoegen van bewerkingen **veranderen niet Hallo shard toowhich sleutel waarden worden toegewezen**. Een splitsing, een bestaand bereik opgesplitst in twee delen, maar blijft beide als toegewezen toohello dezelfde shard. Een samenvoeging is van invloed op twee aangrenzende bereiken die al toegewezen toohello zijn dezelfde shard, ze samenvoegen tot een enkel bereik.  Hallo verkeer van punten of bereiken zelf tussen shards moet toobe gecoördineerd door middel van **UpdateMapping** in combinatie met de daadwerkelijke gegevensverplaatsing.  U kunt Hallo **gesplitste/Merge** service die deel uitmaakt van de elastische database toocoordinate shard-toewijzing wijzigingen met gegevensverplaatsing, hulpprogramma's voor wanneer verkeer nodig is. 
* toore-kaart (of verplaatsen) afzonderlijke punten of bereiken toodifferent shards: Gebruik  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.  
  
    Omdat de gegevens wellicht toobe verplaatst van één shard tooanother in volgorde toobe consistent zijn met **UpdateMapping** bewerkingen, moet u tooperform beweging die afzonderlijk, maar in combinatie met behulp van deze methoden.
* tootake toewijzingen online als offline: Gebruik  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  en  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol Hallo online status van een toewijzing. 
  
    Bepaalde bewerkingen op de shard-toewijzingen zijn alleen toegestaan als een toewijzing in een 'offline' staat, met inbegrip van **UpdateMapping** en **DeleteMapping**. Als een toewijzing offline is, wordt een gegevens-afhankelijke aanvraag op basis van een sleutel die is opgenomen in de toewijzing een fout geretourneerd. Bovendien wanneer een bereik is eerst offline gehaald, wordt alle verbindingen toohello van invloed op een shard worden automatisch in volgorde tooprevent inconsistente of onvolledige resultaten voor query's die zijn gericht tegen bereiken wordt gewijzigd afgebroken. 

Toewijzingen zijn niet-wijzigbaar objecten in .net.  Alle Hallo methoden bovenstaande Wijzig toewijzingen ongeldig ook eventuele verwijzingen toothem in uw code. toomake it eenvoudiger tooperform reeksen van bewerkingen die in een statuswijziging van een toewijzing, alle Hallo-methoden die een-toewijzing gewijzigd een nieuwe retourneren toewijzing-verwijzing, zodat bewerkingen kunnen worden gekoppeld. Bijvoorbeeld, toodelete een bestaande toewijzing in shardmap sm dat Hallo sleutel 25 bevat, kunt u uitvoeren hello te volgen: 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a>Toevoegen van een shard
Toepassingen vaak moet toosimply nieuwe shards toohandle gegevens toevoegen die wordt verwacht van de nieuwe sleutels of sleutelbereiken, voor een shard-toewijzing die al bestaat. Bijvoorbeeld, een toepassing shard door Tenant-ID moet mogelijk een nieuwe shard tooprovision voor een nieuwe tenant of gegevens shard maandelijks moet mogelijk een nieuwe shard ingericht voordat Hallo begin van elke nieuwe maand. 

Als nieuw bereik Hallo sleutelwaarden nog niet is onderdeel van een bestaande toewijzing en geen gegevensverplaatsing nodig, het is zeer eenvoudig tooadd Hallo nieuwe shard en Hallo nieuwe sleutel of bereik toothat shard koppelen. Zie voor meer informatie over het toevoegen van nieuwe shards [toevoegen van een nieuwe shard](sql-database-elastic-scale-add-a-shard.md).

Voor scenario's waarvoor de verplaatsing van gegevens, is Hallo gesplitste merge tool echter benodigde tooorchestrate Hallo verplaatsing van gegevens tussen shards in combinatie met Hallo nodig shard toewijzingen worden bijgewerkt. Zie voor meer informatie over het gebruik van hello gesplitste samenvoegen yool, [overzicht van de gesplitste samenvoegen](sql-database-elastic-scale-overview-split-and-merge.md) 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
