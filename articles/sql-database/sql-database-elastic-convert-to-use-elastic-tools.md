---
title: aaaMigrate bestaande databases tooscale-out | Microsoft Docs
description: Converteren van hulpprogramma's shard databases toouse elastische database door het maken van een manager shard-kaart
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a>Migreren van bestaande databases tooscale-out
Uw bestaande uitgebreid shard databases met hulpprogramma's van Azure SQL Database database eenvoudig te beheren (zoals Hallo [clientbibliotheek voor elastische Database](sql-database-elastic-database-client-library.md)). U moet eerst een bestaande set van databases toouse Hallo converteren [shard kaart manager](sql-database-elastic-scale-shard-map-management.md). 

## <a name="overview"></a>Overzicht
een bestaande database in de shard toomigrate: 

1. Hallo voorbereiden [shard-toewijzing manager-database](sql-database-elastic-scale-shard-map-management.md).
2. Hallo shard-toewijzing worden gemaakt.
3. Bereid Hallo afzonderlijke shards.  
4. Toewijzingen toohello shard-toewijzing toevoegen.

Deze technieken kunnen worden geïmplementeerd met de Hallo [clientbibliotheek voor .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), of de PowerShell-scripts Hallo gevonden op [Azure SQL DB - elastische Database extra scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db). Hier voorbeelden Hallo Hallo PowerShell-scripts gebruiken.

Zie voor meer informatie over Hallo ShardMapManager [Shard kaart management](sql-database-elastic-scale-shard-map-management.md). Zie voor een overzicht van Hallo elastische database-hulpprogramma's [elastische Database functies overzicht](sql-database-elastic-scale-introduction.md).

## <a name="prepare-hello-shard-map-manager-database"></a>Hallo shard kaart manager-database voorbereiden
Hallo shard-toewijzing manager is een speciale database die Hallo gegevens toomanage uitgebreide databases bevat. U kunt een bestaande database gebruiken of een nieuwe database maken. Houd er rekening mee dat een database, fungeert als shard kaart manager mag geen Hallo dezelfde database als een shard. Houd er ook rekening mee dat Hallo PowerShell-script niet Hallo-database voor u maken. 

## <a name="step-1-create-a-shard-map-manager"></a>Stap 1: Maak een shard kaart manager
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a>manager tooretrieve hello shard-kaart
Na het maken, kunt u Hallo shard-toewijzing manager met deze cmdlet ophalen. Deze stap is nodig voor elke keer dat u moet toouse hello ShardMapManager object.

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a>Stap 2: Maak Hallo shard-kaart
U kunt shard-toewijzing toocreate Hallo type moet selecteren. Hallo keuze is afhankelijk van Hallo database-architectuur: 

1. Één tenant per database (voor termen, Zie Hallo [verklarende woordenlijst](sql-database-elastic-scale-glossary.md).) 
2. Meerdere tenants per database (twee typen):
   1. Toewijzing van de lijst
   2. Bereik toewijzing

Voor een model voor één tenant, maakt u een **lijst toewijzing** shard-toewijzing. Hallo één tenant model wijst één database per tenant. Dit is een doeltreffend model voor SaaS-ontwikkelaars aangezien vereenvoudigt het beheer.

![Toewijzing van de lijst][1]

Hallo multitenant model wijst verschillende tenants tooa één database (en u kunt groepen van tenants verdelen over meerdere databases). Dit model gebruiken wanneer u verwacht dat elke tenant toohave kleine hoeveelheden gegevens nodig heeft. In dit model we een bereik van het gebruik van tenants tooa database toewijzen **bereik toewijzing**. 

![Bereik toewijzing][2]

Of u kunt implementeren met een multitenant database model met een *lijst toewijzing* tooassign meerdere tenants tooa één database. Bijvoorbeeld, DB1 is gebruikte toostore informatie over de tenant-id 1 en 5 en DB2 slaat gegevens voor de tenant 7- en 10. 

![Muliple tenants in één DB][3] 

**Op basis van uw keuze, kies een van de volgende opties:**

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a>Optie 1: een shard-toewijzing voor de toewijzing van een lijst maken
Maakt een shard-toewijzing Hallo ShardMapManager object gebruiken. 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a>Optie 2: Maak een shard-toewijzing voor de toewijzing van een bereik
Houd er rekening mee dat tooutilize dit patroon van een toewijzing, tenant-id-waarden moet toobe continue bereiken en acceptabele toohave gat in Hallo bereiken door gewoon Hallo bereik wordt overgeslagen bij het maken van databases Hallo is.

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a>Optie 3: De toewijzingen van de lijst op een individuele database
Instellen van dit patroon vereist ook het maken van een kaart lijst zoals u in stap 2, optie 1.

## <a name="step-3-prepare-individual-shards"></a>Stap 3: Afzonderlijke shards voorbereiden
Voeg elke manager shard (database) toohello shard-toewijzing toe. Hallo afzonderlijke databases nu voorbereid voor het opslaan van informatie over de Identiteitstoewijzing. Deze methode niet uitvoeren op elke shard.

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a>Stap 4: Toewijzingen toevoegen
Hallo toewijzingen toe te voegen, is afhankelijk van Hallo soort shard-toewijzing die u hebt gemaakt. Als u een lijst kaart hebt gemaakt, kunt u de toewijzingen van de lijst toevoegen. Als u een bereik kaart hebt gemaakt, voegt u bereik toewijzingen.

### <a name="option-1-map-hello-data-for-a-list-mapping"></a>Optie 1: Hallo-gegevens voor een lijst toewijzing toewijzen
Hallo gegevens moeten worden toegewezen door de toewijzing van een lijst toe te voegen voor elke tenant.  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a>Optie 2: Hallo-gegevens voor de toewijzing van een bereik toewijzen
Hallo bereik toewijzingen voor alle Hallo tenant bereik-id - database koppelingen toevoegen:

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a>Stap 4-optie 3: Hallo gegevens moeten worden toegewezen voor meerdere tenants op een individuele database
Voer voor elke tenant Hallo toevoegen ListMapping (optie 1, hierboven). 

## <a name="checking-hello-mappings"></a>Hallo toewijzingen controleren
Informatie over Hallo bestaande shards en Hallo-toewijzingen die zijn gekoppeld aan deze kan worden opgevraagd met volgende opdrachten:  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a>Samenvatting
Nadat u Hallo-installatie hebt voltooid, kunt u beginnen toouse Hallo elastische Database-clientbibliotheek. U kunt ook [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md) en [query meerdere shard](sql-database-elastic-scale-multishard-querying.md).

## <a name="next-steps"></a>Volgende stappen
Ophalen van de PowerShell-scripts Hallo van [Azure SQL DB elastische Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

Hallo-hulpprogramma's zijn ook op GitHub: [/elastische-db-hulpprogramma's van Azure](https://github.com/Azure/elastic-db-tools).

Hallo gesplitste merge tool toomove gegevens tooor van een multi-tenant model tooa één tenant-model gebruiken. Zie [gesplitste merge tool](sql-database-elastic-scale-get-started.md).

## <a name="additional-resources"></a>Aanvullende bronnen
Zie voor informatie over algemene gegevensarchitectuurpatronen van multitenant software as a service (SaaS)-databasetoepassingen, [Ontwerppatronen voor multitenant SaaS-toepassingen met Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).

## <a name="questions-and-feature-requests"></a>Vragen en Functieaanvragen
Voor vragen kunt contact toous op Hallo [SQL Database-forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) en voor functieaanvragen, deze toe te voegen toohello [forum met feedback van SQL-Database](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

