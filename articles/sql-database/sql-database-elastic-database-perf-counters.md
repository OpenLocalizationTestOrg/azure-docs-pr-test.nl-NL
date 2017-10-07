---
title: aaaPerformance meteritems voor het beheer van shard-kaart
description: ShardMapManager klasse- en afhankelijke routering prestatiemeteritems
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: b090aba0-2e30-454c-96b3-dffa281f539a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: ddove
ms.openlocfilehash: d24198563d9fa88d12e6c464dbe89bc300e72ca0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-counters-for-shard-map-manager"></a>Prestatiemeteritems voor shard-toewijzingsbeheer
U kunt vastleggen Hallo prestaties van een [shard kaart manager](sql-database-elastic-scale-shard-map-management.md), met name wanneer u [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md). Items worden met methoden van Hallo Microsoft.Azure.SqlDatabase.ElasticScale.Client klasse gemaakt.  

De prestatiemeteritems zijn gebruikte tootrack Hallo prestaties van [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md) bewerkingen. Deze items zijn toegankelijk in Prestatiemeter Hallo onder Hallo 'Elastische Database: Shard Management' categorie.

**Voor de nieuwste versie Hallo:** te gaan[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). Zie ook [upgraden van een app toouse Hallo nieuwste elastische database clientbibliotheek](sql-database-elastic-scale-upgrade-client-library.md).

## <a name="prerequisites"></a>Vereisten
* Hallo toocreate hello prestatiecategorie en prestatiemeteritems, gebruiker moet een deel van de lokale Hallo **beheerders** groep op Hallo machine Hallo-toepassing te hosten.  
* toocreate prestaties teller exemplaar en bijwerken Hallo tellers, Hallo gebruiker moet lid zijn van beide Hallo **beheerders** of **Prestatiemetergebruikers** groep. 

## <a name="create-performance-category-and-counters"></a>Categorie van prestatiemeteritem en prestatiemeteritems maken
toocreate hello tellers, roept u Hallo CreatePeformanceCategoryAndCounters methode Hallo [ShardMapManagmentFactory klasse](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx). Alleen beheerders kan Hallo methode uitvoeren: 

    ShardMapManagerFactory.CreatePerformanceCategoryAndCounters()  

U kunt ook [dit](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283) PowerShell script tooexecute Hallo-methode. Hallo-methode maakt u Hallo prestatiemeteritems te volgen:  

* **In de cache opgeslagen toewijzingen**: aantal toewijzingen voor Hallo shard-toewijzing in de cache opgeslagen.
* **DDR-bewerkingen per seconde**: het aantal afhankelijke routering gegevensbewerkingen voor Hallo shard-kaart. Deze teller wordt bijgewerkt wanneer een oproep te[OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) resulteert in een geslaagde verbinding toohello bestemming shard. 
* **Toewijzing van lookup cache treffers per seconde**: verhouding van geslaagde cache lookup bewerkingen voor toewijzingen in Hallo shard-toewijzing. 
* **Toewijzing van lookup cache missers per seconde**: frequentie van mislukte cache lookup bewerkingen voor toewijzingen in Hallo shard-toewijzing.
* **Toewijzingen toegevoegd of bijgewerkt in de cache per seconde**: snelheid welke toewijzingen worden toegevoegd of bijgewerkt in cache voor Hallo shard-kaart. 
* **Toewijzingen verwijderd uit de cache per seconde**: snelheid waarmee de toewijzingen worden verwijderd uit de cache voor Hallo shard-kaart. 

Prestatiemeteritems zijn gemaakt voor elke kaart in de cache shard per proces.  

## <a name="notes"></a>Opmerkingen
Hallo volgende gebeurtenissen worden geactiveerd door Hallo maken van Hallo prestatiemeteritems:  

* Initialisatie van Hallo [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) met [enthousiaste laden](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx)als Hallo ShardMapManager bevat shard-kaarten. Deze omvatten Hallo [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29) en Hallo [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx) methoden.
* Geslaagde opzoeken van een shard-toewijzing (met behulp van [GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx), [GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) of [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx)). 
* Het is gemaakt van shard-toewijzing met CreateShardMap().

Hallo-prestatiemeteritems worden bijgewerkt door alle cachebewerkingen die worden uitgevoerd op Hallo shard-toewijzing en toewijzingen. Geslaagde verwijdering van Hallo shard-toewijzing met DeleteShardMap () reults Hallo prestatie-items exemplaar worden verwijderd.  

## <a name="best-practices"></a>Aanbevolen procedures
* Maken van de categorie van prestatiemeteritem Hallo en prestatiemeteritems moet slechts één keer worden uitgevoerd voordat de Hallo van ShardMapManager-object is gemaakt. Elke uitvoering van de opdracht Hallo CreatePerformanceCategoryAndCounters() wist vorige Hallo-tellers (verlies van gegevens die zijn gerapporteerd door alle exemplaren) en nieuwe regels worden gemaakt.  
* Prestaties teller exemplaren worden per proces gemaakt. Een crash van de toepassing of het verwijderen van een shard-toewijzing uit het Hallo-cache leidt Hallo prestaties tellers instanties worden verwijderd.  

### <a name="see-also"></a>Zie ook
[Overzicht van de functies elastische Database](sql-database-elastic-scale-introduction.md)  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->

