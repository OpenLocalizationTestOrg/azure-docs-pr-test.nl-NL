---
title: Het beheer van referenties in de clientbibliotheek voor elastische database | Microsoft Docs
description: Het instellen van het juiste niveau van de referenties van beheerder zijn om de alleen-lezen, voor apps voor elastische database
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 72e0edaf-795e-4856-84a5-6594f735fb7e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 46908be2846062a0520d21e06db3091a4d711b0b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="credentials-used-to-access-the-elastic-database-client-library"></a>Referenties gebruikt voor toegang tot de clientbibliotheek voor elastische Database
De [clientbibliotheek voor elastische Database](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) drie verschillende soorten referenties gebruikt voor toegang tot de [shard kaart manager](sql-database-elastic-scale-shard-map-management.md). Gebruik de referenties met het laagste niveau van toegang mogelijk afhankelijk van de behoeften.

* **Beheerreferenties**: voor het maken of bewerken van een manager shard-toewijzing. (Zie de [verklarende woordenlijst](sql-database-elastic-scale-glossary.md).) 
* **Toegang tot de referenties**: voor toegang tot een bestaande shard-toewijzing manager voor informatie over shards.
* **Verbindingsreferenties**: verbinding maken met shards. 

Zie ook [databases en aanmeldingen in Azure SQL Database beheren](sql-database-manage-logins.md). 

## <a name="about-management-credentials"></a>Informatie over van beheerreferenties
Van beheerreferenties worden gebruikt voor het maken van een [ **ShardMapManager** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) object voor toepassingen die manipuleren van shard-kaarten. (Zie bijvoorbeeld [toevoegen van een shard met hulpprogramma's van elastische Database](sql-database-elastic-scale-add-a-shard.md) en [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md)) de gebruiker van de clientbibliotheek elastisch schalen wordt gemaakt van de SQL-gebruikers en de SQL-aanmeldingen en zorgt ervoor dat elk is verleend de machtiging lezen/schrijven voor de database voor globale shard en ook alle shard-databases. Deze referenties worden gebruikt voor het onderhouden van de globale shard-toewijzing en het lokale shard-kaarten wanneer wijzigingen in de shard-toewijzing worden uitgevoerd. Gebruik bijvoorbeeld de beheerreferenties voor het maken van het beheerobject shard-toewijzing (met behulp van [ **GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx): 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

De variabele **smmAdminConnectionString** een verbindingsreeks die de beheerreferenties bevat. De gebruikersnaam en wachtwoord biedt lees-/ schrijftoegang tot shard kaart database- en afzonderlijke shards. De management-verbindingsreeks bevat ook de servernaam en databasenaam op voor het identificeren van de database globale shard-toewijzing. Hier volgt een typische verbindingsreeks daarvoor:

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

Gebruik geen waarden in de vorm van "username@server', in plaats daarvan de waarde 'gebruikersnaam' gebruiken.  Dit komt doordat de referenties moeten werken op basis van de shard-toewijzing manager-database en de afzonderlijke shards die mogelijk op verschillende servers.

## <a name="access-credentials"></a>Referenties voor toegang
Gebruik referenties met alleen-lezen-machtigingen voor de globale shard-toewijzing bij het maken van een shard kaart manager in een toepassing die wordt shard-kaarten niet beheren. De informatie die is opgehaald uit de globale shard-toewijzing onder deze referenties worden gebruikt voor [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md) en voor het vullen van de shard-toewijzing-cache op de client. De referenties worden geleverd via hetzelfde patroon aanroep naar **GetSqlShardMapManager** zoals hierboven beschreven: 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

Let op het gebruik van de **smmReadOnlyConnectionString** in overeenstemming met het gebruik van andere referenties voor deze toegang namens **niet-beheerders** gebruikers: deze referenties mag geen schrijfmachtigingen op de globale shard-toewijzing. 

## <a name="connection-credentials"></a>Verbindingsreferenties
Aanvullende referenties nodig zijn bij gebruik van de [ **OpenConnectionForKey** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) methode voor toegang tot een shard gekoppeld aan een sharding-sleutel. Deze referenties moeten machtigingen voor alleen-lezen toegang tot de tabellen voor lokale shard-toewijzing die zich op de shard opgeven. Dit is nodig voor het uitvoeren van de verbindingsvalidatie voor het gegevensafhankelijke routering op de shard. Dit codefragment kunt toegang tot gegevens in de context van het gegevensafhankelijke routering: 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

In dit voorbeeld **smmUserConnectionString** bevat de verbindingsreeks voor referenties van de gebruiker. Hier volgt een typische verbindingsreeks voor de gebruikersreferenties voor Azure SQL DB: 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

Net als bij de beheerdersreferenties komen niet de waarden in de vorm van "username@server'. In plaats daarvan gebruikt u 'gebruikersnaam'.  Houd er ook rekening mee dat de verbindingsreeks bevat geen een servernaam en databasenaam op. Dat komt doordat de **OpenConnectionForKey** aanroep wordt de verbinding met de juiste shard op basis van de sleutel automatisch doorverwezen. De databasenaam en servernaam zijn daarom niet opgegeven. 

## <a name="see-also"></a>Zie ook
[Databases en aanmeldingen beheren in Azure SQL Database](sql-database-manage-logins.md)

[Uw SQL-database beveiligen](sql-database-security-overview.md)

[Aan de slag met taken voor elastische Database](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

