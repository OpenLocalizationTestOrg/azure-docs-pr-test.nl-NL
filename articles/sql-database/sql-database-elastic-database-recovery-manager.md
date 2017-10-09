---
title: aaaUsing Recovery Manager toofix shard wijzen problemen | Microsoft Docs
description: Hallo RecoveryManager klasse toosolve problemen met de shard-kaarten gebruiken
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 45520ca3-6903-4b39-88ba-1d41b22da9fe
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: ddove
ms.openlocfilehash: 2218fb15122f1df466e65483480461e366317f2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-recoverymanager-class-toofix-shard-map-problems"></a>Met behulp van Hallo RecoveryManager klasse toofix shard kaart problemen
Hallo [RecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.aspx) klasse biedt ADO.Net toepassingen Hallo mogelijkheid tooeasily detecteren en los eventuele inconsistenties tussen Hallo globale shard-toewijzing (GSM) en Hallo lokale shard-toewijzing (LSM) in een databaseomgeving met shard-. 

Hallo GSM en LSM bijhouden Hallo toewijzing van elke database in een shard-omgeving. In sommige gevallen kan wordt een einde ingevoegd tussen Hallo GSM en Hallo LSM. In dat geval gebruik Hallo RecoveryManager klasse toodetect en Hallo break herstellen.

Hallo RecoveryManager klasse maakt deel uit van Hallo [clientbibliotheek voor elastische Database](sql-database-elastic-database-client-library.md). 

![Shard-kaart][1]

Zie voor definities van de termijn [verklarende woordenlijst hulpprogramma's van elastische Database](sql-database-elastic-scale-glossary.md). toounderstand hoe Hallo **ShardMapManager** gebruikte toomanage gegevens in een shard-oplossing, Zie [Shard kaart management](sql-database-elastic-scale-shard-map-management.md).

## <a name="why-use-hello-recovery-manager"></a>Waarom Hallo recovery manager gebruiken?
In een databaseomgeving shard-is een tenant per database en veel databases per server. Er kan ook worden veel servers in Hallo-omgeving. Elke database, is toegewezen in Hallo shard-kaart, zodat aanroepen gerouteerd toohello juiste server en database worden kunnen. Databases worden bijgehouden volgens tooa **sharding sleutel**, en elke shard is toegewezen een **sleutel waardenbereik**. Een sharding-sleutel kan vertegenwoordigen bijvoorbeeld Hallo klantnamen uit "D" te 'F.' Hallo toewijzing van alle shards (aka databases) en hun toewijzing bereiken zijn opgenomen in Hallo **globale shard-toewijzing (GSM)**. Elke database bevat een overzicht van Hallo bereiken op Hallo shard waarvan bekend is als Hallo opgenomen **lokale shard-toewijzing (LSM)**. Wanneer een app verbinding tooa shard maakt, Hallo toewijzing in de cache geplaatst met Hallo-app voor snel ophalen. Hallo LSM is gebruikte toovalidate in de cache opgeslagen gegevens. 

Hallo GSM en LSM mogelijk niet synchroon voor Hallo volgende redenen:

1. Hallo-verwijdering van een shard waarvan bereik ervan uit langer toono dat gaat zijn in gebruik of de naam wijzigen van een shard. Verwijderen van een shard resulteert in een **shard-toewijzing zwevende**. Op deze manier kan een nieuwe naam database leiden tot een zwevende shard-toewijzing. Afhankelijk van hetzelfde doel Hallo Hallo wijziging Hallo shard wellicht toobe verwijderd of Hallo shard-locatie moet toobe bijgewerkt. Zie een verwijderde database toorecover [een verwijderde database terugzetten](sql-database-recovery-using-backups.md).
2. Een geo-failover van de gebeurtenis. toocontinue, moet een Hallo-servernaam en databasenaam van shard-toewijzing manager in de toepassing hello en vervolgens details van de update Hallo shard-toewijzing voor alle shards in een shard-toewijzing bijwerken. Als er een geo-failover, moet deze logica herstel binnen de werkstroom van Hallo worden geautomatiseerd. Herstelacties automatiseren kunt een frictionless beheerbaarheid voor geo geschikte databases en handmatige menselijke acties voorkomt. toolearn over opties toorecover een database als er een datacentrum Zie [bedrijfscontinuïteit](sql-database-business-continuity.md) en [herstel na noodgevallen](sql-database-disaster-recovery.md).
3. Een shard- of Hallo ShardMapManager-database is een herstelde tooan eerdere punt in tijd. toolearn over herstelpunt met behulp van back-ups, Zie [herstel met behulp van back-ups](sql-database-recovery-using-backups.md).

Zie voor meer informatie over Azure SQL Database elastische Database-hulpprogramma's, geo-replicatie en terugzetten Hallo volgende: 

* [Overzicht: Cloud zakelijke continuïteit en database noodherstel met SQL Database](sql-database-business-continuity.md) 
* [Aan de slag met hulpprogramma's voor elastische database](sql-database-elastic-scale-get-started.md)  
* [ShardMap Management](sql-database-elastic-scale-shard-map-management.md)

## <a name="retrieving-recoverymanager-from-a-shardmapmanager"></a>RecoveryManager ophalen uit een ShardMapManager
de eerste stap Hallo is toocreate een RecoveryManager-exemplaar. Hallo [GetRecoveryManager methode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getrecoverymanager.aspx) retourneert Hallo recovery manager voor de huidige Hallo [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) exemplaar. tooaddress inconsistenties in de shard Hallo toewijzen, moet u eerst Hallo RecoveryManager voor bepaalde shard-kaart Hallo ophalen. 

   ```
    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString,  
             ShardMapManagerLoadPolicy.Lazy);
             RecoveryManager rm = smm.GetRecoveryManager(); 
   ```

In dit voorbeeld is Hallo RecoveryManager van Hallo ShardMapManager geïnitialiseerd. Hallo ShardMapManager met een ShardMap is ook al geïnitialiseerd. 

Omdat deze toepassingscode hello shard-toewijzing zelf bewerkt, referenties die worden gebruikt in fabrieksmethode Hallo Hallo (in het voorgaande voorbeeld Hallo smmConnectionString) moet de referenties die alleen-lezen-machtigingen op Hallo GSM database waarnaar wordt verwezen door Hallo hebben verbindingstekenreeks. Deze referenties zijn meestal af van de verbindingen van tooopen referenties die worden gebruikt voor het doorsturen van afhankelijk zijn van gegevens. Zie voor meer informatie [met behulp van referenties in Hallo elastische databaseclient](sql-database-elastic-scale-manage-credentials.md).

## <a name="removing-a-shard-from-hello-shardmap-after-a-shard-is-deleted"></a>Verwijderen van een shard uit Hallo ShardMap nadat een shard is verwijderd
Hallo [DetachShard methode](https://msdn.microsoft.com/library/azure/dn842083.aspx) hello shard gegeven uit Hallo shard-toewijzing wordt losgekoppeld en toewijzingen die zijn gekoppeld aan Hallo shard verwijderd.  

* Hallo locatieparameter is Hallo shard locatie, speciaal servernaam en databasenaam van Hallo shard wordt losgekoppeld. 
* Hallo shardMapName parameter is Hallo shard toewijzingsnaam. Dit is alleen vereist wanneer meerdere shard-maps worden beheerd door Hallo dezelfde shard-toewijzing manager. Optioneel. 


> [!IMPORTANT]
> Deze methode alleen gebruiken als u er zeker van bent dat Hallo bereik voor het toewijzen van Hallo bijgewerkt leeg is. Hallo-methoden die hierboven niet controleren voor Hallo bereik worden verplaatst, dus is het beste tooinclude controleert in uw code.
>

In dit voorbeeld verwijdert shards uit Hallo shard-toewijzing. 

   ```
   rm.DetachShard(s.Location, customerMap);
   ``` 

Hallo shard-toewijzing weerspiegelt Hallo shard-locatie in Hallo GSM vóór de verwijdering van shard Hallo Hallo. Omdat Hallo shard is verwijderd, wordt ervan uitgegaan dit opzettelijk was en Hallo sharding sleutel bereik is niet langer in gebruik. Als dat niet het geval is, kunt u een punt in tijd herstel uitvoeren. toorecover hello shard van een eerder punt in tijd. (Raadpleeg Hallo volgende sectie In dat geval toodetect shard inconsistenties.) toorecover, Zie [herstelpunt](sql-database-recovery-using-backups.md).

Omdat ervan wordt uitgegaan verwijderen van een database Hallo opzettelijk was, hello laatste beheerdersrechten opschonen actie is toodelete Hallo vermelding toohello shard in Hallo shard-toewijzing beheer. Dit voorkomt dat Hallo toepassing per ongeluk schrijven informatie tooa bereik dat wordt niet verwacht.

## <a name="toodetect-mapping-differences"></a>toodetect toewijzing verschillen
Hallo [DetectMappingDifferences methode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.detectmappingdifferences.aspx) selecteert en retourneert een van de Hallo shard maps (lokaal of globaal) als bron van waarheid Hallo en toewijzingen op beide kaarten shard (GSM en LSM) voor overeenstemming zorgt.

   ```
   rm.DetectMappingDifferences(location, shardMapName);
   ```

* Hallo *locatie* Hallo-servernaam en de databasenaam. 
* Hallo *shardMapName* -parameter is Hallo shard toewijzingsnaam. Dit is alleen vereist als er meerdere shard-maps worden beheerd door Hallo dezelfde shard-toewijzing manager. Optioneel. 

## <a name="tooresolve-mapping-differences"></a>tooresolve toewijzing verschillen
Hallo [ResolveMappingDifferences methode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.resolvemappingdifferences.aspx) selecteert u een van de Hallo shard maps (lokaal of globaal) als bron van waarheid Hallo en toewijzingen op beide kaarten shard (GSM en LSM) voor overeenstemming zorgt.

   ```
   ResolveMappingDifferences (RecoveryToken, MappingDifferenceResolution.KeepShardMapping);
   ```

* Hallo *RecoveryToken* parameter Hallo verschillen in Hallo toewijzingen tussen Hallo GSM en Hallo LSM voor Hallo specifieke shard inventariseert. 
* Hallo [MappingDifferenceResolution opsomming](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.mappingdifferenceresolution.aspx) gebruikte tooindicate Hallo methode voor het oplossen van Hallo verschil tussen Hallo shard toewijzingen. 
* **MappingDifferenceResolution.KeepShardMapping** is raadzaam om bij Hallo LSM nauwkeurige toewijzing Hallo bevat en daarom Hallo toewijzing in Hallo shard moet worden gebruikt. Dit is doorgaans Hallo geval als er een failover: Hallo shard zich nu bevindt op een nieuwe server. Aangezien Hallo shard moet eerst worden verwijderd uit Hallo GSM (met Hallo RecoveryManager.DetachShard methode), bestaat een toewijzing niet meer op Hallo GSM. Hallo LSM moet daarom gebruikte toore-Hallo shard-toewijzing tot stand brengen.

## <a name="attach-a-shard-toohello-shardmap-after-a-shard-is-restored"></a>Een shard-toohello ShardMap koppelen nadat een shard is hersteld
Hallo [AttachShard methode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.attachshard.aspx) wordt Hallo opgegeven shard toohello shard-toewijzing. Inconsistenties kaart shard detecteert en het Hallo toewijzingen toomatch hello shard op Hallo punt Hallo shard herstelprocedure-updates. Ervan wordt uitgegaan dat Hallo de database ook hernoemde tooreflect Hallo oorspronkelijke databasenaam (voordat Hallo shard is hersteld), aangezien Hallo punt in tijd herstelbewerking standaard tooa nieuwe database met Hallo tijdstempel toegevoegd. 

   ```
   rm.AttachShard(location, shardMapName)
   ``` 

* Hallo *locatie* parameter is Hallo-servernaam en databasenaam van Hallo shard wordt gekoppeld. 
* Hallo *shardMapName* -parameter is Hallo shard toewijzingsnaam. Dit is alleen vereist wanneer meerdere shard-maps worden beheerd door Hallo dezelfde shard-toewijzing manager. Optioneel. 

Dit voorbeeld wordt een shard toohello shard-toewijzing die onlangs is hersteld van een eerder tijdstip punt in. Aangezien Hallo shard (namelijk hello toewijzing voor Hallo shard in Hallo LSM) is hersteld, is het mogelijk inconsistent is met Hallo shard-vermelding in Hallo GSM. Buiten deze voorbeeldcode Hallo shard is hersteld en toohello oorspronkelijke naam van de database Hallo gewijzigd. Omdat deze is teruggezet, wordt ervan uitgegaan Hallo toewijzing in Hallo LSM Hallo vertrouwde toewijzing. 

   ```
   rm.AttachShard(s.Location, customerMap); 
   var gs = rm.DetectMappingDifferences(s.Location); 
      foreach (RecoveryToken g in gs) 
       { 
       rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
       } 
   ```

## <a name="updating-shard-locations-after-a-geo-failover-restore-of-hello-shards"></a>Bijwerken van shard-locaties na een geo-failover (herstel) van Hallo shards
Als er een geo-failover, staat Hallo secundaire database schrijven toegankelijk en wordt de nieuwe primaire database Hallo. Hallo naam van het Hallo-server en mogelijk Hallo-database (afhankelijk van uw configuratie), kan afwijken van de oorspronkelijke primaire Hallo. Daarom Hallo toewijzingen voor Hallo shard in Hallo GSM en LSM moet worden vastgesteld. Op dezelfde manier als Hallo-database is teruggezet tooa andere naam of locatie of tooan eerdere punt in tijd hierdoor mogelijk inconsistenties Hallo shard Maps. Hallo Shard kaart Manager verwerkt Hallo distributie van geopende verbindingen toohello juiste database. Distributie is gebaseerd op Hallo-gegevens in Hallo shard-toewijzing en Hallo-waarde van Hallo sharding-sleutel die Hallo doel van Hallo toepassingen aanvraag. Na een geo-failover, moet deze gegevens worden bijgewerkt met de Hallo nauwkeurige servernaam, databasenaam en shard-toewijzing van de herstelde database Hallo. 

## <a name="best-practices"></a>Aanbevolen procedures
Zijn gewoonlijk beheerd door een cloudbeheerder van Hallo van een toepassing met opzet op een Azure SQL-Databases zakelijke continuïteit functies operations geo-failover en herstel. Zakelijke continuïteit planning vereist processen, procedures en metingen tooensure die zakelijke activiteiten zonder onderbreking kunnen worden voortgezet. Hallo methoden beschikbaar als onderdeel van Hallo RecoveryManager klasse moet worden gebruikt binnen deze werkstroom tooensure Hallo GSM en LSM altijd zijn bijgewerkt op basis van de uitgevoerde actie Hallo herstel. Er zijn vijf eenvoudige stappen tooproperly gezorgd Hallo GSM en LSM weerspiegelen Hallo nauwkeurige informatie na een failover. Hallo toepassing code tooexecute die deze stappen kunnen worden geïntegreerd in de werkstroom en bestaande hulpprogramma's. 

1. Hallo RecoveryManager uit Hallo ShardMapManager ophalen. 
2. Loskoppelen van de oude shard Hallo uit Hallo shard-toewijzing.
3. Hallo nieuwe shard toohello shard kaart, inclusief nieuwe shard-locatie Hallo koppelen.
4. Inconsistenties in de toewijzing tussen Hallo GSM en LSM Hallo detecteren. 
5. Verschillen tussen Hallo GSM en Hallo LSM, vertrouwende Hallo LSM oplossen. 

In dit voorbeeld voert Hallo stappen te volgen:

1. Hiermee verwijdert u shards uit Hallo Shard-toewijzing die aan shard-locaties voordat Hallo failover-gebeurtenis.
2. Shards toohello Shard-toewijzing reflecterende Hallo nieuwe shard locaties koppelt (Hallo parameter 'Configuration.SecondaryServer' hello nieuwe servernaam is, maar Hallo dezelfde databasenaam).
3. Haalt Hallo herstel tokens door toewijzing verschillen tussen Hallo GSM en Hallo LSM voor elke shard detecteren. 
4. Hallo inconsistenties oplossing door vertrouwende Hallo-toewijzing van Hallo LSM van elke shard. 
   
   ```
   var shards = smm.GetShards(); 
   foreach (shard s in shards) 
   { 
     if (s.Location.Server == Configuration.PrimaryServer) 
   
         { 
          ShardLocation slNew = new ShardLocation(Configuration.SecondaryServer, s.Location.Database); 
   
          rm.DetachShard(s.Location); 
   
          rm.AttachShard(slNew); 
   
          var gs = rm.DetectMappingDifferences(slNew); 
   
          foreach (RecoveryToken g in gs) 
            { 
               rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
            } 
        } 
    } 
   ```

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-database-recovery-manager/recovery-manager.png

