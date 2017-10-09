---
title: aaaGet gestart met hulpprogramma's voor elastische database | Microsoft Docs
description: Basic uitleg van onderdeel voor elastische database tools Hallo van Azure SQL Database, met inbegrip van een eenvoudig run voorbeeld-app.
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: CarlRabeler
ms.assetid: b6911f8d-2bae-4d04-9fa8-f79a3db7129d
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: a84e05c39dffbaef440538602f898acee6e0483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-elastic-database-tools"></a>Aan de slag met hulpprogramma's voor elastische database
Dit document vindt u toohello ontwikkelaarservaring helpen u toorun Hallo voorbeeld-app. Hallo voorbeeld maakt een eenvoudige shard-toepassing en behandelt de belangrijkste mogelijkheden van hulpprogramma's voor elastische database. functies van Hallo ziet u het Hallo [clientbibliotheek voor elastische database](sql-database-elastic-database-client-library.md).

tooinstall hello bibliotheek, gaat u te[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). Hallo voorbeeld-app die wordt beschreven in de volgende sectie Hallo is Hallo-bibliotheek geïnstalleerd.

## <a name="prerequisites"></a>Vereisten
* Visual Studio 2012 of hoger met C#. Download een gratis versie op [Visual Studio-Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).
* NuGet 2.7 of hoger. meest recente versie tooget hello, Zie [NuGet installeren](http://docs.nuget.org/docs/start-here/installing-nuget).

## <a name="download-and-run-hello-sample-app"></a>Hallo voorbeeld-app downloaden en uitvoeren
Hallo **elastische DB-hulpprogramma's voor Azure SQL - aan de slag** voorbeeldtoepassing illustreert de belangrijkste aspecten Hallo van Hallo ontwikkeling biedt voor shard toepassingen die gebruikmaken van hulpprogramma's voor elastische database. Dit artikel gaat over de belangrijkste gebruiksvoorbeelden voor [shard kaart management](sql-database-elastic-scale-shard-map-management.md), [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md), en [opvragen van meerdere shard](sql-database-elastic-scale-multishard-querying.md). Ga als volgt toodownload en Voer Hallo-voorbeeld: 

1. Hallo downloaden [elastische DB-hulpprogramma's voor Azure SQL - voorbeeld aan de slag](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-a80d8dc6) van MSDN. Pak Hallo voorbeeld tooa locatie die u kiest.

2. toocreate een project openen Hallo **ElasticScaleStarterKit.sln** oplossing van Hallo **C#** directory.

3. Open in Hallo-oplossing voor het voorbeeldproject Hallo Hallo **app.config** bestand. Volg de instructies Hallo in Hallo bestand tooadd de naam van uw Azure SQL Database-server en uw gegevens aanmelden (gebruikersnaam en wachtwoord).

4. Toepassing bouwen en uitvoeren Hallo. Wanneer u wordt gevraagd, schakel Visual Studio toorestore hello NuGet-pakketten van Hallo-oplossing. Hallo meest recente versie van Hallo elastische database-clientbibliotheek vanuit NuGet gedownload.

5. Experimenteer met Hallo verschillende opties toolearn meer informatie over mogelijkheden voor Hallo client-bibliotheek. Houd er rekening mee Hallo stappen toepassing vindt in de console-uitvoer Hallo Hallo en kunnen u gratis tooexplore Hallo code achter de schermen Hallo.
   
    ![Voortgang][4]

Gefeliciteerd, hebt u gebouwd en uw eerste shard-toepassing uitvoeren met behulp van hulpprogramma's voor elastische database op SQL-Database. Gebruik Visual Studio of SQL Server Management Studio tooconnect tooyour SQL-database en bekijk snel Hallo shards die Hallo voorbeeld gemaakt. U zult nieuwe voorbeeld shard-databases en een manager-database van de shard-toewijzing dat voorbeeld Hallo heeft gemaakt.

> [!IMPORTANT]
> U wordt aangeraden de meest recente versie van Management Studio Hallo altijd te gebruiken zodat u gesynchroniseerd met updates tooAzure en SQL-Database blijven. [SQL Server Management Studio bijwerken](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

### <a name="key-pieces-of-hello-code-sample"></a>Belangrijkste stukjes Hallo-codevoorbeeld
* **Toewijzingen beheren shards en shard**: Hallo code laat zien hoe toowork met shards, bereiken en toewijzingen in Hallo bestand **ShardManagementUtils.cs**. Zie voor meer informatie [Scale-out databases met Hallo shard-toewijzing manager](http://go.microsoft.com/?linkid=9862595).  

* **Gegevensafhankelijke routering**: routering van transacties toohello rechts shard wordt weergegeven in **DataDependentRoutingSample.cs**. Zie voor meer informatie [gegevensafhankelijke routering](http://go.microsoft.com/?linkid=9862596). 

* **Uitvoeren van query's via meerdere shards**: uitvoeren van query's over shards wordt weergegeven in het Hallo-bestand **MultiShardQuerySample.cs**. Zie voor meer informatie [opvragen van meerdere shard](http://go.microsoft.com/?linkid=9862597).

* **Toe te voegen leeg shards**: Hallo iteratieve toevoegen van nieuwe leeg shards wordt uitgevoerd door Hallo-code in Hallo bestand **CreateShardSample.cs**. Zie voor meer informatie [Scale-out databases met Hallo shard-toewijzing manager](http://go.microsoft.com/?linkid=9862595).

### <a name="other-elastic-scale-operations"></a>Andere bewerkingen elastisch schalen
* **Het splitsen van een bestaande shard**: Hallo mogelijkheid toosplit shards wordt geleverd door Hallo **gesplitste merge tool**. Zie voor meer informatie [verplaatsen van gegevens tussen cloud uitgebreide databases](sql-database-elastic-scale-overview-split-and-merge.md).

* **Samenvoegen van bestaande shards**: Shard samenvoegingen ook worden uitgevoerd met behulp van Hallo **gesplitste merge tool**. Zie voor meer informatie [verplaatsen van gegevens tussen cloud uitgebreide databases](sql-database-elastic-scale-overview-split-and-merge.md).   

## <a name="cost"></a>Kosten
Hallo-hulpprogramma's voor elastische database zijn gratis. Wanneer u hulpprogramma's voor elastische database gebruikt, kunt u eventuele extra kosten boven op Hallo kosten van het gebruik van uw Azure niet ontvangt. 

Hallo-voorbeeldtoepassing maakt bijvoorbeeld nieuwe databases. Hallo kosten voor deze afhankelijk zijn van Hallo SQL Database versie die u kiest en hello Azure gebruik van uw toepassing.

Zie voor informatie over prijzen, [SQL-Database prijsinformatie](https://azure.microsoft.com/pricing/details/sql-database/).

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over hulpprogramma's voor elastische database Hallo pagina's te volgen:

* Codevoorbeelden: 
  * [Elastische DB-hulpprogramma's voor Azure SQL - aan de slag](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-a80d8dc6?SRC=VSIDE)
  * [Elastische DB-hulpprogramma's voor Azure SQL - Entity Framework-integratie](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-bae904ba?SRC=VSIDE)
  * [Shard-elasticiteit op Script Center](https://gallery.technet.microsoft.com/scriptcenter/Elastic-Scale-Shard-c9530cbe)
* Blog: [aankondiging elastisch schalen](https://azure.microsoft.com/blog/2014/10/02/introducing-elastic-scale-preview-for-azure-sql-database/)
* Microsoft Virtual Academy: [Scale-Out implementeren met behulp van Sharding Hello elastische Database Client bibliotheek-Video](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554?l=lWyQhF1fC_6306218965) 
* Channel 9: [elastische Schaalfunctionaliteit van video-overzicht](http://channel9.msdn.com/Shows/Data-Exposed/Azure-SQL-Database-Elastic-Scale)
* Discussieforum: [-forum Azure SQL Database](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)
* toomeasure prestaties: [prestatiemeteritems voor het beheer van shard-kaart](sql-database-elastic-database-client-library.md)

<!--Anchors-->
[hello Elastic Scale Sample Application]: #The-Elastic-Scale-Sample-Application
[Download and Run hello Sample App]: #Download-and-Run-the-Sample-App
[Cost]: #Cost
[Next steps]: #next-steps

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-get-started/newProject.png
[2]: ./media/sql-database-elastic-scale-get-started/click-online.png
[3]: ./media/sql-database-elastic-scale-get-started/click-CSharp.png
[4]: ./media/sql-database-elastic-scale-get-started/output2.png

