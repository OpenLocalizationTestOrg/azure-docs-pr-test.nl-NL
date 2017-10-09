---
title: aaaData afhankelijke routering met Azure SQL Database | Microsoft Docs
description: Hoe toouse Hallo ShardMapManager klasse in .NET-toepassingen voor gegevensafhankelijke routering, een functie van shard-databases in Azure SQL Database
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: cad09e15-5561-4448-aa18-b38f54cda004
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ddove
ms.openlocfilehash: 34014508ae01905686791fe096bb275cb84f53b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-dependent-routing"></a>Gegevensafhankelijke routering
**Gegevensafhankelijke routering** Hallo mogelijkheid toouse Hallo gegevens in een query tooroute Hallo aanvraag tooan juiste database is. Dit is een fundamenteel patroon bij het werken met shard-databases. Hallo-aanvraagcontext mogelijk ook de gebruikte tooroute Hallo aanvraag, vooral als Hallo sharding sleutel geen deel uit van Hallo query maakt. Elke specifieke query transactie is of in een toepassing met gegevensafhankelijke routering beperkt tooaccessing een individuele database per aanvraag. Voor hello Azure SQL Database elastische hulpprogramma's voor deze routering wordt gerealiseerd met Hallo  **[ShardMapManager klasse](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)**  in ADO.NET-toepassingen.

Hallo toepassing hoeft niet tootrack verschillende verbindingsreeksen of DB locaties die zijn gekoppeld aan andere delen van gegevens in Hallo shard-omgeving. In plaats daarvan Hallo [Shard kaart Manager](sql-database-elastic-scale-shard-map-management.md) wordt geopend verbindingen toohello juiste databases, indien nodig op basis van Hallo-gegevens in Hallo shard-toewijzing en Hallo-waarde van Hallo sharding-sleutel die Hallo doel van de aanvraag van de toepassing hello. Hallo-sleutel is doorgaans Hallo *customer_id*, *tenant_id*, *date_key*, of enige andere specifieke id die is een fundamenteel parameter van het Hallo-verzoek voor database). 

Zie voor meer informatie [schalen van SQL Server met gegevensafhankelijke routering](https://technet.microsoft.com/library/cc966448.aspx).

## <a name="download-hello-client-library"></a>Hallo-clientbibliotheek downloaden
tooget hello klasse, installatie Hallo [clientbibliotheek voor elastische Database](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a>Met behulp van een ShardMapManager in een gegevenstoepassing afhankelijke routering
Toepassingen moeten Hallo instantiëren **ShardMapManager** tijdens de initialisatie met Hallo factory aanroep  **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**. In dit voorbeeld wordt zowel een **ShardMapManager** en een specifieke **ShardMap** die deze bevat zijn geïnitialiseerd. In dit voorbeeld toont Hallo GetSqlShardMapManager en [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) methoden.

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-hello-shard-map"></a>Laagste bevoegdheid referenties mogelijk gebruiken voor het ophalen van Hallo shard-kaart
Als een toepassing Hallo shard-toewijzing zelf niet bewerken is, Hallo referenties in fabrieksmethode Hallo slechts alleen-lezen toegang moeten hebben op Hallo **globale Shard-toewijzing** database. Deze referenties zijn meestal af van de referenties die worden gebruikt tooopen verbindingen toohello shard kaart manager. Zie ook [referenties gebruikt tooaccess Hallo elastische Database-clientbibliotheek](sql-database-elastic-scale-manage-credentials.md). 

## <a name="call-hello-openconnectionforkey-method"></a>Hallo OpenConnectionForKey methode aanroepen
Hallo  **[ShardMap.OpenConnectionForKey methode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)**  retourneert een ADO.Net-verbinding gereed is voor het uitgeven van opdrachten toohello juiste database op basis van de Hallo Hallo **sleutel**parameter. Shard-gegevens in cache wordt opgeslagen in de toepassing hello door Hallo **ShardMapManager**, zodat deze aanvragen zoeken in de database tegen Hallo geen doorgaans worden **globale Shard-toewijzing** database. 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* Hallo **sleutel** parameter wordt gebruikt als een zoeksleutel in Hallo shard kaart toodetermine Hallo juiste database voor Hallo-aanvraag. 
* Hallo **connectionString** gebruikte toopass alleen Hallo gebruikersreferenties voor verbinding Hallo gewenst is. Er is geen databasenaam of servernaam zijn opgenomen in deze *connectionString* omdat het Hallo-methode wordt bepaald Hallo-database en de server met behulp van Hallo **ShardMap**. 
* Hallo  **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)**  te moet worden ingesteld**ConnectionOptions.Validate** als kan worden gewijzigd in een omgeving waar shard toegewezen en rijen tooother databases als verplaatsen kunnen een resultaat van de gesplitste of merge-bewerkingen. Hiervoor moet een korte query toohello lokale shard-toewijzing op Hallo doeldatabase (niet toohello globale shard toewijzen) voordat Hallo verbinding toohello toepassing wordt geleverd. 

Als Hallo validatie met het Hallo lokale shard-toewijzing is mislukt (waarmee wordt aangegeven dat Hallo cache onjuist is), Hallo Shard kaart Manager Hallo globale shard kaart tooobtain Hallo nieuwe correcte waarde query voor het opzoeken van Hallo Hallo-cache, bijwerken en verkrijgen en Hallo retourneren juiste databaseverbinding. 

Gebruik **ConnectionOptions.None** alleen wanneer shard-toewijzing wijzigingen wordt niet verwacht terwijl een toepassing online is. In dat geval kunnen Hallo in de cache opgeslagen waarden worden aangenomen tooalways juist zijn en Hallo extra round trip validatie aanroep toohello-doeldatabase veilig worden overgeslagen. Dat vermindert databaseverkeer. Hallo **connectionOptions** kan ook worden ingesteld via een waarde in een configuratie-bestand tooindicate of sharding wijzigingen worden verwacht, of tijdens een bepaalde tijd niet.  

In dit voorbeeld wordt Hallo-waarde van de sleutel van een geheel getal **CustomerID**met een **ShardMap** object met de naam **customerShardMap**.  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect toohello shard for that customer ID. No need toocall a SqlConnection 
    // constructor followed by hello Open method.
    using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, 
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
    { 
        // Execute a simple command. 
        SqlCommand cmd = conn.CreateCommand(); 
        cmd.CommandText = @"UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID"; 

        cmd.Parameters.AddWithValue("@customerID", customerId); 
        cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
        cmd.ExecuteNonQuery(); 
    }  

Hallo **OpenConnectionForKey** methode retourneert een nieuwe al-geopende verbinding toohello juiste database. Verbindingen gebruikt op deze manier kunnen nog steeds profiteren van de ADO.Net verbindingsgroepering. Zolang transacties en aanvragen kunnen worden voldaan door één shard tegelijk, moet dit enige aanpassing Hallo nodig in een toepassing die al met ADO.Net. 

Hallo  **[OpenConnectionForKeyAsync methode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**  is ook beschikbaar als uw toepassing gebruik van asynchrone programmering met ADO.Net maakt. Het gedrag is Hallo gegevens afhankelijke equivalent met ADO routering. De NET  **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)**  methode.

## <a name="integrating-with-transient-fault-handling"></a>Integratie met afhandeling van tijdelijke fout
Tooensure of tijdelijke fouten zijn opgepikt door het Hallo-app en dat Hallo operations meerdere keren worden geprobeerd voordat er wordt een fout is door een best practice bij het ontwikkelen van de data access-toepassingen in Hallo cloud. Tijdelijke fout verwerking voor cloud-toepassingen is besproken in [afhandeling van tijdelijke fout](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx). 

Afhandeling van tijdelijke fout kan natuurlijk worden gecombineerd met Hallo gegevensafhankelijke routering patroon. Hallo belangrijkste vereiste is tooretry Hallo gehele toegangsaanvraag inclusief Hallo **met** blok die Hallo gegevensafhankelijke routering verbinding hebt verkregen. Hallo in bovenstaand voorbeeld kan worden herschreven als volgt (Houd er rekening mee gemarkeerde wijzigen). 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a>Voorbeeld - afhankelijke routering met tijdelijke fout afhandeling van gegevens
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect toohello shard for a customer ID. 
        using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId,  
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
        { 
            // Execute a simple command 
            SqlCommand cmd = conn.CreateCommand(); 

            cmd.CommandText = @&quot;UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID&quot;; 

            cmd.Parameters.AddWithValue(&quot;@customerID&quot;, customerId); 
            cmd.Parameters.AddWithValue(&quot;@newPersonID&quot;, newPersonId); 
            cmd.ExecuteNonQuery(); 

            Console.WriteLine(&quot;Update completed&quot;); 
        } 
<span style="background-color:  #FFFF00">    }); </span> 
</code></pre>


Verwerking van de benodigde tooimplement tijdelijke fout zijn pakketten gedownload automatisch wanneer het bouwen van Hallo elastische database-voorbeeldtoepassing. Pakketten zijn ook verkrijgbaar afzonderlijk via [Enterprise Library - tijdelijke fout afhandeling van Application Block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/). Versie 6.0 of hoger gebruiken. 

## <a name="transactional-consistency"></a>Transactionele consistentie
Transactionele eigenschappen zijn voor alle bewerkingen lokale tooa shard gegarandeerd. Bijvoorbeeld, uitvoeren transacties die zijn verzonden via het gegevensafhankelijke routering binnen Hallo bereik van Hallo doel shard voor Hallo-verbinding. Op dit moment zijn er geen mogelijkheden voor het opnemen van meerdere verbindingen in een transactie en er zijn daarom geen transactionele garanties met betrekking tot de bewerkingen die worden uitgevoerd via shards.

## <a name="next-steps"></a>Volgende stappen
Zie voor een shard toodetach of tooreattach een shard [hello RecoveryManager klasse toofix shard kaart problemen met](sql-database-elastic-database-recovery-manager.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

