---
title: TSQL:initiate failover voor Azure SQL Database | Microsoft Docs
description: Start een geplande of niet-geplande failover voor Azure SQL Database met behulp van Transact-SQL
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5eb2d256-025d-4f5a-99d4-17f702b37f14
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 418953e044ba84ce758063d56a371af45d5cdfe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="initiate-a-planned-or-unplanned-failover-for-azure-sql-database-with-transact-sql"></a>Een geplande of niet-geplande failover initiëren voor Azure SQL Database met Transact-SQL

Dit artikel ziet u hoe tooinitiate failover tooa secundaire SQL-Database met behulp van Transact-SQL. tooconfigure geo-replicatie, Zie [geo-replicatie configureren voor Azure SQL Database](sql-database-geo-replication-transact-sql.md).

tooinitiate failover, moet u de volgende Hallo:

* Een aanmelding die DBManager op Hallo primaire
* Hebt u db_ownership van Hallo lokale database dat u geo-replicatie gaat
* DBManager worden op Hallo partner (s) toowhich configureert u geo-replicatie
* Meest recente versie van SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> Het verdient aanbeveling dat u altijd hello gebruiken meest recente versie van Management Studio tooremain gesynchroniseerd met updates tooMicrosoft Azure en SQL-Database. [SQL Server Management Studio bijwerken](https://msdn.microsoft.com/library/mt238290.aspx).
>  

## <a name="initiate-a-planned-failover-promoting-a-secondary-database-toobecome-hello-new-primary"></a>Start een geplande failover promoveren van een secundaire database toobecome Hallo nieuwe primaire
U kunt Hallo **ALTER DATABASE** instructie toopromote een secundaire database toobecome Hallo nieuwe primaire database op een geplande wijze, degraderen van de bestaande primaire toobecome Hallo een secundaire database. Deze instructie is uitgevoerd voor de hoofddatabase Hallo op Hallo Azure SQL Database logische server in welke Hallo geo-replicatie secundaire database die wordt gepromoveerd zich bevindt. Deze functionaliteit is ontworpen voor geplande failover, zoals tijdens Hallo DR-zoomt en vereist dat de primaire database Hallo beschikbaar zijn.

Hallo-opdracht verricht Hallo workflow volgen:

1. Tijdelijk leeggemaakte switches toosynchronous replicatiemodus, waardoor alle openstaande transacties toobe toohello secundaire en de blokkering van alle nieuwe transacties;
2. Switches Hallo rollen van de twee databases Hallo Hallo geo-replicatie samen.  

Deze reeks wordt gegarandeerd dat Hallo twee databases zijn gesynchroniseerd voordat Hallo rollen switch en daarom geen verlies van gegevens wordt uitgevoerd. Er is een korte periode gedurende welke beide databases niet beschikbaar (in volgorde van de Hallo van 0 too25 seconden zijn) tijdens het Hallo-rollen worden omgeschakeld. Als de primaire database Hallo meerdere secundaire databases, Hallo-opdracht heeft wordt automatisch opnieuw Hallo andere secundaire replica's tooconnect toohello nieuwe primaire.  Hallo hele bewerking duurt minder dan een minuut toocomplete onder normale omstandigheden. Zie voor meer informatie [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) en [Servicelagen](sql-database-service-tiers.md).

Gebruik Hallo stappen tooinitiate een geplande failover te volgen.

1. In Management Studio verbinding met toohello Azure SQL Database logische server waarin een geo-replicatie secundaire database zich bevindt.
2. Open de map Hallo-Databases, vouw Hallo **systeemdatabases** map, klik met de rechtermuisknop op **master**, en klik vervolgens op **nieuwe Query**.
3. Gebruik de volgende Hallo **ALTER DATABASE** instructie tooswitch Hallo secundaire database toohello primaire rol.
   
        ALTER DATABASE <MyDB> FAILOVER;
4. Klik op **Execute** toorun Hallo query.

> [!NOTE]
> In zeldzame gevallen is het mogelijk dat Hallo-bewerking kan niet worden voltooid en vastgelopen lijkt. Hallo-gebruiker kan in dit geval Hallo force failover-opdracht uitvoeren en verlies van gegevens te accepteren.
> 
> 

## <a name="initiate-an-unplanned-failover-from-hello-primary-database-toohello-secondary-database"></a>Start een niet-geplande failover uit Hallo primaire database toohello secundaire database
U kunt Hallo **ALTER DATABASE** instructie toopromote een secundaire database toobecome Hallo nieuwe primaire database op een niet-geplande wijze, waardoor Hallo degradatie van de bestaande primaire toobecome Hallo een secundaire database op een tijdstip wanneer Hallo primaire database is niet meer beschikbaar. Deze instructie is uitgevoerd voor de hoofddatabase Hallo op Hallo Azure SQL Database logische server in welke Hallo geo-replicatie secundaire database die wordt gepromoveerd zich bevindt.

Deze functionaliteit is ontworpen voor herstel na noodgevallen wanneer herstellen beschikbaarheid voor Hallo-database is van essentieel belang en er gegevens verloren gaan acceptabel is. Wanneer geforceerde failover wordt gestart, opgegeven Hallo secundaire database onmiddellijk wordt het Hallo primaire database en begint schrijftransacties accepteren. Als de oorspronkelijke primaire database Hallo kunnen tooreconnect met deze nieuwe primaire database is, een incrementele back-up wordt gemaakt op de oorspronkelijke primaire database Hallo en Hallo oude primaire database wordt gemaakt in een secundaire database voor de nieuwe primaire database Hallo; het is alleen een synchroniseren replica van de nieuwe primaire Hallo.

Echter, omdat punt In tijd herstellen niet wordt ondersteund op Hallo secundaire databases als Hallo gebruiker toorecover gegevens die zijn toegewezen wenst toohello oude primaire database die niet is gerepliceerd toohello nieuwe primaire database voordat Hallo geforceerde failover is opgetreden, Hallo gebruiker moet tooengage ondersteuning toorecover dit gegevens verloren gegaan.

Als de primaire database Hallo meerdere secundaire databases, Hallo-opdracht heeft wordt automatisch opnieuw Hallo andere secundaire replica's tooconnect toohello nieuwe primaire.

Gebruik Hallo stappen tooinitiate een niet-geplande failover te volgen.

1. In Management Studio verbinding met toohello Azure SQL Database logische server waarin een geo-replicatie secundaire database zich bevindt.
2. Open de map Hallo-Databases, vouw Hallo **systeemdatabases** map, klik met de rechtermuisknop op **master**, en klik vervolgens op **nieuwe Query**.
3. Gebruik de volgende Hallo **ALTER DATABASE** instructie tooswitch Hallo secundaire database toohello primaire rol.
   
        ALTER DATABASE <MyDB>   FORCE_FAILOVER_ALLOW_DATA_LOSS;
4. Klik op **Execute** toorun Hallo query.

> [!NOTE]
> Als het Hallo-opdracht wordt verstrekt wanneer zowel primaire als secundaire online oude primaire hello, worden nieuwe secundaire onmiddellijk zonder gegevenssynchronisatie Hallo. Als primaire Hallo optreden doorvoeren van transacties wanneer Hallo-opdracht wordt gegeven kunnen gegevens verloren gaan.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* Controleert de verificatievereisten Hallo voor uw server en database zijn geconfigureerd op de nieuwe primaire Hallo na een failover. Zie voor meer informatie [beveiliging van SQL Database na het herstel na noodgevallen](sql-database-geo-replication-security-config.md).
* Zie toolearn herstellen na een noodgeval van actieve geo-replicatie, inclusief stappen voor herstel vóór en na het herstel en het uitvoeren van een detailanalyse van het herstel na noodgevallen [herstel na noodgevallen](sql-database-disaster-recovery.md)
* Zie voor een blogbericht Sasha Nosov over actieve geo-replicatie, [Spotlight op nieuwe mogelijkheden van geo-replicatie](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/)
* Zie voor meer informatie over het ontwerpen van cloud-toepassingen toouse actieve geo-replicatie [cloud-toepassingen ontwerpen voor bedrijfscontinuïteit van geo-replicatie](sql-database-designing-cloud-solutions-for-disaster-recovery.md)
* Zie voor meer informatie over het gebruik van actieve geo-replicatie met elastische pools [elastische Pool disaster recovery strategieën](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
* Zie voor een overzicht van zakelijke continuïteit [Business Continuity Overview](sql-database-business-continuity.md)

