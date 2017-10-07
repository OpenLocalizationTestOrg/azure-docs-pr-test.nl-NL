---
title: aaaManaging referenties in Hallo-clientbibliotheek voor elastische database | Microsoft Docs
description: Hoe tooset Hallo juiste niveau van de referenties van beheerder tooread alleen-lezen, voor apps voor elastische database
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
ms.openlocfilehash: 218783ca2a07e3c0a4b089aa92634f32c41386e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="credentials-used-tooaccess-hello-elastic-database-client-library"></a>Referenties gebruikt clientbibliotheek van tooaccess Hallo elastische Database
Hallo [clientbibliotheek voor elastische Database](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) maakt gebruik van drie verschillende soorten referenties tooaccess hello [shard kaart manager](sql-database-elastic-scale-shard-map-management.md). Afhankelijk van de noodzaak hello, Hallo credential niet gebruiken bij Hallo laagste niveau van toegang mogelijk.

* **Beheerreferenties**: voor het maken of bewerken van een manager shard-toewijzing. (Zie Hallo [verklarende woordenlijst](sql-database-elastic-scale-glossary.md).) 
* **Toegang tot de referenties**: manager tooobtain gegevens over shards worden toegewezen aan een bestaande shard tooaccess.
* **Verbindingsreferenties**: tooconnect tooshards. 

Zie ook [databases en aanmeldingen in Azure SQL Database beheren](sql-database-manage-logins.md). 

## <a name="about-management-credentials"></a>Informatie over van beheerreferenties
Van beheerreferenties gebruikte toocreate zijn een [ **ShardMapManager** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) object voor toepassingen die manipuleren van shard-kaarten. (Zie bijvoorbeeld [toevoegen van een shard met hulpprogramma's van elastische Database](sql-database-elastic-scale-add-a-shard.md) en [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md)) Hallo gebruiker van de clientbibliotheek van Hallo elastisch schalen maakt Hallo SQL-gebruikers en SQL-aanmeldingen en zorgt ervoor dat elk is verleend toewijzen Hallo lezen/schrijven machtigingen op Hallo globale shard-database en alle shard-databases ook. Deze referenties zijn gebruikte toomaintain Hallo globale shard-toewijzing en Hallo lokale shard maps wanneer wijzigingen toohello shard-toewijzing worden uitgevoerd. Hallo management referenties toocreate hello shard kaart manager object voor het exemplaar te gebruiken (met behulp van [ **GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx): 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

Hallo variabele **smmAdminConnectionString** een verbindingsreeks die Hallo management referenties bevat. Hallo-gebruikersnaam en wachtwoord biedt lezen/schrijven access tooboth shard-toewijzing database en afzonderlijke shards. Hallo management verbindingsreeks omvatten ook Hallo-server en de database naam tooidentify Hallo globale shard kaart-database. Hier volgt een typische verbindingsreeks daarvoor:

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

Gebruik geen waarden in de vorm van Hallo 'username@server', gebruiken in plaats daarvan Hallo 'gebruikersnaam'-waarde.  Dit komt doordat de referenties moeten werken op basis van zowel Hallo shard kaart manager-database en afzonderlijke shards die mogelijk op verschillende servers.

## <a name="access-credentials"></a>Referenties voor toegang
Gebruik de referenties die alleen-lezen-machtigingen op Hallo globale shard-toewijzing hebben bij het maken van een shard kaart manager in een toepassing die wordt shard-kaarten niet beheren. Hallo gegevens opgehaald uit de globale shard-toewijzing Hallo onder deze referenties worden gebruikt voor [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md) en toopopulate hello shard-cache op Hallo client toewijzen. Hallo referenties zijn opgegeven via Hallo dezelfde patroon aanroep te**GetSqlShardMapManager** zoals hierboven beschreven: 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

Houd er rekening mee Hallo gebruik van Hallo **smmReadOnlyConnectionString** tooreflect Hallo gebruik van andere referenties voor dit type toegang namens **niet-beheerders** gebruikers: deze referenties dient niet schrijven machtigingen op Hallo globale shard-kaart. 

## <a name="connection-credentials"></a>Verbindingsreferenties
Aanvullende referenties nodig zijn bij gebruik van Hallo [ **OpenConnectionForKey** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) methode tooaccess een shard gekoppeld aan een sharding-sleutel. Deze referenties moeten tooprovide machtigingen voor alleen-lezentoegang toohello lokale shard kaart tabellen die zich op Hallo shard. Dit is de validatie van de benodigde tooperform verbinding voor het gegevensafhankelijke routering op Hallo shard. Dit codefragment kunt toegang tot gegevens in de context van het gegevensafhankelijke routering Hallo: 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

In dit voorbeeld **smmUserConnectionString** Hallo-verbindingsreeks voor Hallo gebruikersreferenties bevat. Hier volgt een typische verbindingsreeks voor de gebruikersreferenties voor Azure SQL DB: 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

Net als bij Hallo beheerdersreferenties, komen niet in waarden Hallo vorm van "username@server'. In plaats daarvan gebruikt u 'gebruikersnaam'.  Let op: Hallo verbindingsreeks bevat ook geen een servernaam en databasenaam op. Dat komt doordat Hallo **OpenConnectionForKey** aanroep wordt automatisch doorverwezen Hallo verbinding toohello juiste shard op basis van Hallo-sleutel. Hallo-databasenaam en servernaam zijn daarom niet opgegeven. 

## <a name="see-also"></a>Zie ook
[Databases en aanmeldingen beheren in Azure SQL Database](sql-database-manage-logins.md)

[Uw SQL-database beveiligen](sql-database-security-overview.md)

[Aan de slag met taken voor elastische Database](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

