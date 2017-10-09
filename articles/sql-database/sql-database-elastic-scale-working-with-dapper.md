---
title: aaaUsing elastische database-clientbibliotheek met Dapper | Microsoft Docs
description: Gebruik de clientbibliotheek voor elastische database met Dapper.
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 463d2676-3b19-47c2-83df-f8c50492c9d2
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: c22ece2a977265e93850f0ad3f3ca48f0a8733ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-elastic-database-client-library-with-dapper"></a>Clientbibliotheek voor elastische database gebruiken met Dapper
Dit document is bedoeld voor ontwikkelaars die afhankelijk zijn van Dapper toobuild toepassingen, maar ook wilt tooembrace [elastische database tooling](sql-database-elastic-scale-introduction.md) toocreate toepassingen die sharding tooscale-out hun gegevenslaag implementeren.  Dit document ziet u Hallo wijzigingen in Dapper-toepassingen die nodig zijn toointegrate met hulpprogramma's voor elastische database zijn. Onze focus is op het samenstellen van Hallo elastische database shard-beheer en afhankelijk van de gegevens routering met Dapper. 

**Voorbeeldcode**: [hulpmiddelen voor elastische databases voor Azure SQL Database - Dapper integratie](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).

Integratie van **Dapper** en **DapperExtensions** Hello elastische database-clientbibliotheek voor Azure SQL Database is eenvoudig. Uw toepassingen kunnen gebruikmaken van afhankelijke routering door het wijzigen van Hallo maken en openen van nieuwe gegevens [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objecten toouse hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) aanroepen vanuit Hallo [client bibliotheek](http://msdn.microsoft.com/library/azure/dn765902.aspx). Dit beperkt de wijzigingen in uw toepassing tooonly waarbij nieuwe verbindingen zijn gemaakt en geopend. 

## <a name="dapper-overview"></a>Overzicht van dapper
**Dapper** is een object-relationele toewijzen. Het .NET-objecten uit uw toepassing tooa relationele database (en omgekeerd) worden toegewezen. Hallo eerste deel van Hallo voorbeeldcode ziet u hoe u Hallo-clientbibliotheek voor elastische database kunt integreren met Dapper gebaseerde toepassingen. Hallo secondegedeelte van Hallo voorbeeldcode ziet u hoe toointegrate bij gebruik van zowel Dapper en DapperExtensions.  

Hallo mapper-functionaliteit in Dapper biedt uitbreidingsmethoden op databaseverbindingen die verzenden T-SQL-instructies voor uitvoering of opvragen Hallo-database vereenvoudigen. Bijvoorbeeld: Dapper maakt het eenvoudig toomap tussen uw .NET-objecten en het Hallo-parameters van de SQL-instructies voor **Execute** aanroepen of tooconsume Hallo resultaten van uw SQL-query's in .NET-objecten met behulp van **Query**aanroepen vanuit Dapper. 

Wanneer u DapperExtensions gebruikt, moet u niet langer tooprovide Hallo SQL-instructies. Extensies methoden zoals **GetList** of **invoegen** maken via de databaseverbinding Hallo HALLO hallo achtergrond SQL-instructies.

Een ander voordeel van Dapper en ook DapperExtensions is dat Hallo toepassing besturingselementen maken van verbinding met database Hallo Hallo. Dit helpt communiceren met de clientbibliotheek van Hallo elastische database die beleggingsmakelaars-databaseverbindingen op basis van Hallo toewijzing van shardlets toodatabases.

tooget hello Dapper verzamelingen, Zie [Dapper punt net](http://www.nuget.org/packages/Dapper/). Zie voor Dapper Hallo-extensies [DapperExtensions](http://www.nuget.org/packages/DapperExtensions).

## <a name="a-quick-look-at-hello-elastic-database-client-library"></a>Een kort overzicht van Hallo-clientbibliotheek voor elastische database
Met Hallo elastische database-clientbibliotheek, definieert u de partities van de toepassingsgegevens aangeroepen *shardlets* toodatabases toewijzen en deze door herkennen *sharding sleutels*. U kunt zoveel databases als u uw shardlets verdelen over deze databases nodig hebben. Hallo-toewijzing van sharding sleutelwaarden toohello databases is door een shard-toewijzing geleverd door de API's Hallo-bibliotheek opgeslagen. Deze mogelijkheid wordt aangeroepen **shard kaart management**. Hallo shard kaart fungeert ook als Hallo broker databaseverbindingen voor aanvragen die een sharding-sleutel bevatten. Deze mogelijkheid is waarnaar wordt verwezen tooas **gegevensafhankelijke routering**.

![Shard-kaarten en gegevensafhankelijke routering][1]

Hallo shard-toewijzing manager beveiligt gebruikers tegen inconsistente weergaven in shardlet gegevens die optreden kunnen wanneer de gelijktijdige shardlet bewerkingen plaatsvinden op Hallo-databases. toodo Hallo dus shard maps broker Hallo-databaseverbindingen voor een toepassing die is gebouwd met Hallo-bibliotheek. Wanneer de shard-beheerbewerkingen kunnen invloed hebben op Hallo shardlet, hierdoor Hallo shard kaart functionaliteit tooautomatically kill een databaseverbinding. 

In plaats van Hallo traditionele manier toocreate verbindingen voor Dapper, moeten we toouse hello [OpenConnectionForKey methode](http://msdn.microsoft.com/library/azure/dn824099.aspx). Dit zorgt ervoor dat alle Hallo validatie plaats vindt en verbindingen correct worden beheerd als er gegevens worden verplaatst tussen shards.

### <a name="requirements-for-dapper-integration"></a>Vereisten voor Dapper-integratie
Als u werkt met Hallo-clientbibliotheek voor elastische database en Hallo Dapper API's, willen we tooretain Hallo volgende eigenschappen:

* **Scaleout**: We wilt tooadd of databases uit de gegevenslaag Hallo van shard toepassing hello die nodig zijn voor Hallo capaciteit eisen van de toepassing hello verwijderen. 
* **Consistentie**: omdat de toepassing is uitgebreid met behulp van sharding, moeten we tooperform gegevensafhankelijke routering. Willen we dus toouse Hallo gegevens afhankelijke routering mogelijkheden van Hallo bibliotheek toodo. In het bijzonder, willen we tooretain Hallo validatie en consistentie wordt geleverd door verbindingen die worden geleverd door Hallo shard kaart manager in volgorde tooavoid beschadiging of onjuiste queryresultaten. Dit zorgt ervoor dat verbindingen tooa shardlet gegeven zijn afgewezen of gestopt als (bijvoorbeeld) Hallo shardlet momenteel verplaatste tooa verschillende shard met gesplitste/Merge-API's.
* **Objecttoewijzing**: We willen tooretain Hallo gemak geleverd door Dapper tootranslate tussen klassen in de toepassing hello en onderliggende databasestructuren Hallo Hallo-toewijzingen. 

Hallo volgende sectie bevat hulp voor deze vereisten voor toepassingen op basis van **Dapper** en **DapperExtensions**.

## <a name="technical-guidance"></a>Technische richtlijnen
### <a name="data-dependent-routing-with-dapper"></a>Afhankelijke routering met Dapper gegevens
Met Dapper is de toepassing hello gewoonlijk verantwoordelijk is voor het maken en openen van Hallo verbindingen toohello onderliggende database. Een type T gezien door de toepassing hello, retourneert Dapper queryresultaten zoals .NET verzamelingen van het type T. Dapper voert Hallo toewijzing van Hallo T-SQL rijen toohello resultaatobjecten van het type T. Op deze manier maps Dapper .NET-objecten in SQL-waarden of de parameters voor instructies voor data manipulatie language (DML). Dapper biedt deze functionaliteit via uitbreidingsmethoden op Hallo reguliere [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) object uit Hallo ADO .NET SQL clientbibliotheken. Hallo SQL-verbinding die wordt geretourneerd door Hallo Elastic Scale API's voor DDR zijn ook reguliere [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objecten. Hierdoor kunnen ons toodirectly gebruik Dapper extensies via Hallo type dat wordt geretourneerd door Hallo-clientbibliotheek van DDR-API, zoals het is ook een eenvoudige SQL Client verbinding.

Deze opmerkingen kunnen u eenvoudig toouse verbindingen brokered door Hallo elastische database-clientbibliotheek voor Dapper.

Dit codevoorbeeld (van Hallo begeleidende voorbeeld) ziet u Hallo benadering waarbij Hallo sharding-sleutel wordt geleverd door Hallo toepassing toohello bibliotheek toobroker Hallo verbinding toohello rechts shard.   

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                     key: tenantId1, 
                     connectionString: connStrBldr.ConnectionString, 
                     options: ConnectionOptions.Validate))
    {
        var blog = new Blog { Name = name };
        sqlconn.Execute(@"
                      INSERT INTO
                            Blog (Name)
                            VALUES (@name)", new { name = blog.Name }
                        );
    }

Hallo aanroep toohello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API vervangt Hallo standaard maken en openen van een SQL-clientverbinding. Hallo [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) aanroep heeft Hallo argumenten die vereist voor het gegevensafhankelijke routering zijn: 

* Hallo shard-toewijzing tooaccess Hallo afhankelijke routeringsinterfaces gegevens
* Hallo sharding key tooidentify hello shardlet
* Hallo referenties (gebruikersnaam en wachtwoord) tooconnect toohello shard

Hallo shard-toewijzingsobject maakt een verbinding toohello shard die Hallo shardlet voor Hallo opgegeven sharding-sleutel bevat. Hallo elastische databaseclient-API's ook labelen Hallo verbinding tooimplement wordt gegarandeerd dat de consistentie. Sinds Hallo aanroepen te[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) retourneert een object reguliere SQL clientverbinding, Hallo volgende aanroep toohello **Execute** uitbreidingsmethode van Dapper volgt Hallo standaard Dapper Oefening.

Query's werk te veel Hallo dezelfde manier - u eerst opent Hallo verbinding met [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) van Hallo client-API. U Hallo reguliere Dapper uitbreiding methoden toomap Hallo resultaten van uw SQL-query in .NET-objecten gebruiken:

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId1, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate ))
    {    
           // Display all Blogs for tenant 1
           IEnumerable<Blog> result = sqlconn.Query<Blog>(@"
                                SELECT * 
                                FROM Blog
                                ORDER BY Name");

           Console.WriteLine("All blogs for tenant id {0}:", tenantId1);
           foreach (var item in result)
           {
                Console.WriteLine(item.Name);
            }
    }

Houd er rekening mee dat Hallo **met** blokkeren met Hallo DDR verbinding scopes alle databasebewerkingen in Hallo blok toohello één shard waar tenantId1 wordt gehouden. Hallo query retourneert alleen blogs opgeslagen op de huidige shard hello, maar niet Hallo die zijn opgeslagen op een andere shards. 

## <a name="data-dependent-routing-with-dapper-and-dapperextensions"></a>Afhankelijke routering met Dapper en DapperExtensions gegevens
Dapper wordt geleverd met een ecosysteem van de aanvullende extensies die verdere gemak en abstractie uit hello database bieden kunnen bij het ontwikkelen van databasetoepassingen. DapperExtensions is een voorbeeld. 

DapperExtensions gebruiken in uw toepassing wordt niet gewijzigd hoe databaseverbindingen gemaakt en beheerd. Nog steeds van toepassing hello verantwoordelijkheid tooopen verbindingen en reguliere SQL Client connection-objecten door Hallo uitbreidingsmethoden worden verwacht. We kunnen vertrouwen op Hallo [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) hierboven. Hallo tonen volgende codevoorbeelden, Hallo enige wijziging is dat er niet langer hoeft toowrite Hallo T-SQL-instructies:

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           var blog = new Blog { Name = name2 };
           sqlconn.Insert(blog);
    }

En dit codevoorbeeld Hallo voor Hallo-query is: 

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           // Display all Blogs for tenant 2
           IEnumerable<Blog> result = sqlconn.GetList<Blog>();
           Console.WriteLine("All blogs for tenant id {0}:", tenantId2);
           foreach (var item in result)
           {
               Console.WriteLine(item.Name);
           }
    }

### <a name="handling-transient-faults"></a>Afhandeling van tijdelijke fouten
Hallo Microsoft Patterns en procedures in een team gepubliceerde Hallo [tijdelijke fout afhandeling van Application Block](http://msdn.microsoft.com/library/hh680934.aspx) toohelp toepassingsontwikkelaars algemene tijdelijke storingen opgetreden tijdens het uitvoeren in de cloud Hallo beperken. Zie voor meer informatie [Perseverance, geheim van alle successen: Hallo tijdelijke fout afhandeling van Application Block met](http://msdn.microsoft.com/library/dn440719.aspx).

Hallo-codevoorbeeld is afhankelijk van Hallo tijdelijke fout bibliotheek tooprotect tegen tijdelijke fouten. 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
    {
       using (SqlConnection sqlconn = 
          shardingLayer.ShardMap.OpenConnectionForKey(tenantId2, connStrBldr.ConnectionString, ConnectionOptions.Validate))
          {
              var blog = new Blog { Name = name2 };
              sqlconn.Insert(blog);
          }
    });

**SqlDatabaseUtils.SqlRetryPolicy** in Hallo bovenstaande code wordt gedefinieerd als een **SqlDatabaseTransientErrorDetectionStrategy** met een aantal nieuwe pogingen van 10 en 5 seconden wachttijd tussen nieuwe pogingen. Als u van transacties gebruikmaakt, zorgt u ervoor dat uw bereik opnieuw terug toohello begin van de transactie in geval van een tijdelijke fout Hallo Hallo.

## <a name="limitations"></a>Beperkingen
Hallo-methoden die worden beschreven in dit document leidt tot een aantal beperkingen:

* Hallo voorbeeldcode voor dit document biedt niet laten zien hoe toomanage schema via shards.
* Een aanvraag opgegeven, gaan we ervan uit dat alle bijbehorende verwerken van de database zich in een enkel shard aangeduid met de Hallo sharding sleutel van het Hallo-aanvraag. Echter, deze aanname niet altijd bijhoudt, bijvoorbeeld wanneer het niet mogelijk toomake een sharding-sleutel beschikbaar. tooaddress deze, Hallo clientbibliotheek voor elastische databases bevat Hallo [MultiShardQuery klasse](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx). Hallo klasse implementeert een abstractie van de verbinding voor het uitvoeren van query's via meerdere shards. MultiShardQuery gebruiken in combinatie met Dapper valt buiten bereik Hallo van dit document.

## <a name="conclusion"></a>Conclusie
Toepassingen met Dapper en DapperExtensions kunnen eenvoudig profiteren van de hulpmiddelen voor elastische databases voor Azure SQL Database. Via Hallo stappen in dit document, die toepassingen de mogelijkheid Hallo-hulpprogramma kunnen gebruiken voor afhankelijke routering door het wijzigen van Hallo maken en openen van nieuwe gegevens [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objecten toouse hello [ OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) aanroep van Hallo-clientbibliotheek voor elastische database. Dit beperkt Hallo toepassing wijzigingen vereist toothose plaatsen waar nieuwe verbindingen zijn gemaakt en geopend. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-working-with-dapper/dapperimage1.png
