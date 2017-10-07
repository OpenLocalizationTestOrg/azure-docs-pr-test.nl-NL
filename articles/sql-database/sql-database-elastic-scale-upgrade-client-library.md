---
title: aaaUpgrade toohello nieuwste elastische database-clientbibliotheek | Microsoft Docs
description: Apps en -bibliotheek via Nuget upgraden
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 0a546510-76e7-465e-9271-f15ff0cfa959
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: cc2c9179be4c53ca59cd24d832127cf277c6e695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-app-toouse-hello-latest-elastic-database-client-library"></a>Upgrade van een app toouse Hallo nieuwste elastische database-clientbibliotheek
Nieuwe versies van Hallo [clientbibliotheek voor elastische Database](sql-database-elastic-database-client-library.md) zijn beschikbaar via NuGetand hello NuGetPackage Manager interface in Visual Studio. Upgrades bevatten oplossingen voor problemen en ondersteuning voor nieuwe mogelijkheden van de clientbibliotheek Hallo.

**Voor de nieuwste versie Hallo:** te gaan[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

Opnieuw maken van uw toepassing met de nieuwe bibliotheek hello, evenals wijzigen van uw bestaande Shard kaart Manager metagegevens die zijn opgeslagen in uw Azure SQL-Databases toosupport nieuwe functies.

Deze stappen uitvoert in volgorde zorgt ervoor dat oude versies van de clientbibliotheek Hallo niet langer aanwezig zijn in uw omgeving zijn wanneer metagegevensobjecten zijn bijgewerkt, wat betekent dat de van de oude versie metagegevensobjecten won't worden gemaakt na de upgrade.   

## <a name="upgrade-steps"></a>Upgradestappen
**1. Werk uw toepassingen.** In Visual Studio, downloaden en verwijzing Hallo nieuwste clientbibliotheek van de versie in alle ontwikkelingsprojecten die gebruikmaken van de bibliotheek Hallo; vervolgens opnieuw maken en implementeren. 

* Selecteer in Visual Studio-oplossing **extra** --> **NuGet Package Manager** -->  **NuGet-pakketten beheren voor oplossing**. 
* (Visual Studio 2013) Selecteer in het linkerdeelvenster Hallo **Updates**, en selecteer vervolgens Hallo **Update** knop op Hallo pakket **Azure SQL Database-clientbibliotheek met elastische Scale** dat wordt weergegeven in Hallo venster.
* (Visual Studio 2015) Hallo filtervak te ingesteld**Upgrade beschikbaar**. Hallo pakket tooupdate selecteren en op Hallo **Update** knop.
* (Visual Studio 2017) Selecteer boven Hallo van dialoogvenster Hallo, **Updates**. Hallo pakket tooupdate selecteren en op Hallo **Update** knop.
* Bouwen en implementeren. 

**2. Werk uw scripts.** Als u **PowerShell** toomanage shards, scripts [Hallo nieuwe bibliotheekversie downloaden](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) en kopieer dit naar Hallo directory waarin u scripts uitvoeren. 

**3. Upgrade uw service gesplitste samenvoegen.** Als u Hallo elastische database gesplitste merge tool tooreorganize gedeelde gegevens, [downloaden en implementeren van de meest recente versie van Hallo hulpprogramma Hallo](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/). Gedetailleerde stappen voor Hallo Service vindt u de upgrade [hier](sql-database-elastic-scale-overview-split-and-merge.md). 

**4. Upgrade van uw databases Shard kaart Manager**. Hallo metagegevens van de Shard-kaarten ondersteunende in Azure SQL Database bijwerken.  Er zijn twee manieren waarop u kunt dit doen met PowerShell of C#. Beide opties worden hieronder weergegeven.

***Optie 1: Upgrade metagegevens met behulp van PowerShell***

1. Download Hallo nieuwste-opdrachtregelprogramma voor NuGet van [hier](http://nuget.org/nuget.exe) en tooa map op te slaan. 
2. Open een opdrachtprompt, gaat u toohello dezelfde map en probleem Hallo-opdracht:`nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`
3. Navigeer toohello submap die Hallo nieuwe client DLL versie die u hebt zojuist hebt gedownload, bijvoorbeeld:`cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`
4. Hallo-elastische database-upgrade scriptlet client downloaden van Hallo [Script Center](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), en sla dit in Hallo dezelfde map met Hallo dll-bestand.
5. 'PowerShell.\upgrade.ps1' uitvoeren vanaf de opdrachtprompt Hallo en volg de aanwijzingen Hallo van die map.

***Optie 2: Upgrade metagegevens met C#***

U kunt ook een Visual Studio-toepassing maken die uw ShardMapManager wordt geopend, doorloopt over alle shards en Hallo metagegevens upgradeprocedure uitvoert door het aanroepen van methoden Hallo [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) en [ UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) zoals in dit voorbeeld: 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

Deze technieken voor upgrades van de metagegevens kunnen meerdere malen worden toegepast zonder schade. Bijvoorbeeld, als een oudere clientversie per ongeluk een shard maakt nadat u al hebt bijgewerkt, kunt u uitvoeren upgrade opnieuw over alle shards tooensure die Hallo meest recente metagegevensversie in uw infrastructuur aanwezig is. 

**Opmerking:** nieuwe versies van de clientbibliotheek Hallo gepubliceerd tot datum blijven toowork met eerdere versies van metagegevens van de Manager van Shard-toewijzing Hallo op Azure SQL DB en vice versa.   Tootake profiteren van een aantal nieuwe functies in de nieuwste client hello, metagegevens Hallo moet echter toobe bijgewerkt.   Houd er rekening mee dat upgrades van de metagegevens niet van invloed op alle gebruikersgegevens of toepassingsspecifieke gegevens, alleen objecten door Hallo Shard kaart Manager gemaakt en gebruikt.  En toepassingen blijven toooperate via Hallo updatevolgorde die hierboven worden beschreven. 

## <a name="elastic-database-client-version-history"></a>Versiegeschiedenis van client elastische database
Ga te voor versiegeschiedenis,[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

