---
title: 'Azure-portal: SQL-Database geo-replicatie | Microsoft Docs'
description: "Geo-replicatie configureren voor Azure SQL Database in hello Azure-portal en initiëren failover"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a>Actieve geo-replicatie configureren voor Azure SQL Database in hello Azure-portal en initiëren failover

Dit artikel ziet u hoe tooconfigure actieve geo-replicatie voor SQL-Database in Hallo [Azure-portal](http://portal.azure.com) en tooinitiate failover.

tooinitiate failover Hello Azure-portal, Zie [initiëren van een geplande of niet-geplande failover voor Azure SQL Database met hello Azure-portal](sql-database-geo-replication-portal.md).

tooconfigure actieve geo-replicatie met behulp van hello Azure-portal, moet u Hallo resource te volgen:

* Een Azure SQL database: Hallo primaire database die u wilt dat tooreplicate tooa verschillende geografische regio.

> [!Note]
Actieve geo-replicatie moet liggen tussen databases in Hallo hetzelfde abonnement.

## <a name="add-a-secondary-database"></a>Toevoegen van een secundaire database
Hallo volgende stappen een nieuwe secundaire database maken in een associatie geo-replicatie.  

tooadd een secundaire database, moet u de eigenaar van de Hallo-abonnement of mede-eigenaar.

Hallo secundaire database heeft dezelfde naam als de primaire database Hallo Hallo en Hallo heeft, standaard hetzelfde serviceniveau. Hallo secundaire database is een individuele database of een database in een elastische pool. Zie voor meer informatie [Servicelagen](sql-database-service-tiers.md).
Nadat Hallo secundaire is gemaakt en wordt gemaakt, begint de gegevens van Hallo primaire database toohello nieuwe secundaire database te repliceren.

> [!NOTE]
> Als er al Hallo partner-database bestaat (bijvoorbeeld als gevolg van een vorige geo-replicatie relatie beëindigd) mislukt Hallo-opdracht.
> 

1. In Hallo [Azure-portal](http://portal.azure.com), toohello database die u tooset voor geo-replicatie wilt bladeren.
2. Selecteer op de pagina van het Hallo SQL database **geo-replicatie**, en selecteer vervolgens Hallo regio toocreate Hallo secundaire database. U kunt een andere regio dan Hallo regio die als host fungeert voor de primaire database Hallo selecteren, maar we raden Hallo [gekoppelde regio](../best-practices-availability-paired-regions.md).
   
    ![Geo-replicatie configureren](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. Selecteer of Hallo-server en prijscategorie voor de secundaire database Hallo configureren.
   
    ![Secundaire configureren](./media/sql-database-geo-replication-portal/create-secondary.png)
4. U kunt desgewenst een secundaire database tooan elastische groep toevoegen. toocreate hello secundaire database in een groep, klikt u op **elastische pool** en selecteer een groep op de doelserver Hallo. Een groep moet al bestaan op de doelserver Hallo. Deze werkstroom wordt niet gemaakt voor een groep.
5. Klik op **maken** tooadd Hallo secundaire.
6. Hallo secundaire database wordt gemaakt en Hallo seeding proces wordt gestart.
   
    ![Secundaire configureren](./media/sql-database-geo-replication-portal/seeding0.png)
7. Wanneer Hallo seeding van proces voltooid is, weergegeven Hallo secundaire database de status ervan.
   
    ![Seeding voltooid](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a>Initieer een failover

Hallo secundaire database kan worden uitgeschakeld toobecome Hallo primaire.  

1. In Hallo [Azure-portal](http://portal.azure.com), primaire database toohello Hallo geo-replicatie samen te bladeren.
2. Selecteer op de blade SQL-Database Hallo **alle instellingen** > **geo-replicatie**.
3. In Hallo **SECUNDAIREN** lijst, selecteer Hallo database gewenste toobecome Hallo nieuwe primaire en klik op **Failover**.
   
    ![failover](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. Klik op **Ja** toobegin Hallo failover.

Hallo opdracht switches onmiddellijk Hallo secundaire database aan Hallo primaire rol. 

Er is een korte periode gedurende welke beide databases niet beschikbaar (in volgorde van de Hallo van 0 too25 seconden zijn) tijdens het Hallo-rollen worden omgeschakeld. Als de primaire database Hallo meerdere secundaire databases, Hallo opdracht automatisch heeft Hallo configureren andere secundaire replica's tooconnect toohello nieuwe primaire. Hallo hele bewerking duurt minder dan een minuut toocomplete onder normale omstandigheden. 

> [!NOTE]
> Met deze opdracht is ontworpen voor snel herstel van database Hallo bij een stroomstoring. Dit activeert failover zonder gegevenssynchronisatie (gedwongen failover).  Als de primaire Hallo online is en het doorvoeren van transacties wanneer Hallo-opdracht wordt gegeven gegevensverlies optreden. 
> 
> 

## <a name="remove-secondary-database"></a>Secundaire database verwijderen
Deze bewerking permanent Hallo toohello secundaire replicatiedatabase wordt beëindigd en wijzigingen Hallo rol van Hallo secundaire tooa normale alleen-lezen database. Als Hallo connectiviteit toohello secundaire database verbroken is, Hallo-opdracht is geslaagd, maar Hallo secundaire biedt niet lezen-schrijven pas nadat de verbinding is hersteld.  

1. In Hallo [Azure-portal](http://portal.azure.com), primaire database toohello Hallo geo-replicatie samen te bladeren.
2. Selecteer op de pagina van het Hallo SQL database **geo-replicatie**.
3. In Hallo **SECUNDAIREN** lijst, de gewenste tooremove van Hallo geo-replicatie samenwerking Selecteer Hallo-database.
4. Klik op **Stop replicatie al**.
   
    ![Secundaire verwijderen](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. Er wordt een bevestigingsvenster geopend. Klik op **Ja** tooremove Hallo-database van Hallo geo-replicatie samenwerking. (Deze instellen tooa alleen-lezen database geen deel uit van replicatie.)

## <a name="next-steps"></a>Volgende stappen
* toolearn meer informatie over actieve geo-replicatie, Zie [actieve geo-replicatie](sql-database-geo-replication-overview.md).
* Zie voor een overzicht van zakelijke continuïteit en scenario's [Business continuity overview](sql-database-business-continuity.md).

