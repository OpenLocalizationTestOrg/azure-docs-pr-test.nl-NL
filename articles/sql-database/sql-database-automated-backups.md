---
title: aaaAzure SQL-Database automatisch, geografisch redundante back-ups | Microsoft Docs
description: SQL-Database maakt een back-up van de lokale database om de paar minuten en maakt gebruik van Azure geografisch redundante opslag met leestoegang voor geografische redundantie automatisch.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 3ee3d49d-16fa-47cf-a3ab-7b22aa491a8d
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 8aff5356e8142707dd7cd2533a4aa5ea8fec866d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-automatic-sql-database-backups"></a>Meer informatie over automatische back-ups van SQL-Database

SQL-Database maakt databaseback-ups en maakt gebruik van geografisch redundante opslag met Azure-leestoegang (RA-GRS) tooprovide geografische redundantie automatisch. Deze back-ups worden gemaakt, automatisch en zonder extra kosten. U hoeft niet toodo alles toomake die ze gebeuren. Databaseback-ups zijn een essentieel onderdeel van een zakelijke continuïteit en noodherstel herstelstrategie omdat ze uw gegevens tegen per ongeluk beschadigd of verwijderd beschermen. Als u wilt dat back-ups tookeep in uw eigen storage-container, kunt u een lange termijn back-up bewaarbeleid kunt configureren. Zie [Langetermijnretentie](sql-database-long-term-retention.md) voor meer informatie.

## <a name="what-is-a-sql-database-backup"></a>Wat is er een back-up van de SQL-Database?

SQL-Database maakt gebruik van SQL Server-technologie toocreate [volledige](https://msdn.microsoft.com/library/ms186289.aspx), [differentiële](https://msdn.microsoft.com/library/ms175526.aspx), en [transactielogboek](https://msdn.microsoft.com/library/ms191429.aspx) back-ups. elke 5-10 minuten Hallo transactielogboekback-ups in het algemeen gebeuren met Hallo frequentie op basis van Hallo prestatieniveau en de hoeveelheid activiteit in een database. Transactielogboekback-ups, volledige en differentiële back-ups maakt, kunnen u een database tooa specifieke punt in tijd toohello toorestore dezelfde server die als host fungeert voor Hallo-database. Wanneer u een database herstelt, service-cijfers af welke vol is, differentiële Hallo en transactielogboekback-ups moeten toobe hersteld.


U kunt deze back-ups te gebruiken:

* Een database tooa point-in-time binnen de bewaarperiode Hallo herstellen. Deze bewerking wordt een nieuwe database maken in Hallo dezelfde server als de oorspronkelijke database Hallo.
* Een verwijderde database toohello tijd die is verwijderd of binnen de bewaarperiode Hallo herstellen. Hallo verwijderd database kan alleen worden teruggezet in Hallo dezelfde server waarop de oorspronkelijke database Hallo is gemaakt.
* Herstellen van een database tooanother geografische regio. Hiermee kunt u toorecover na een noodgeval geografische wanneer u geen toegang uw server en database tot. Deze maakt een nieuwe database in een bestaande server overal ter wereld Hallo. 
* Een database terugzetten vanaf een specifieke back-up zijn opgeslagen in uw Azure Recovery Services-kluis. Hiermee kunt u een oude versie van Hallo database toosatisfy een aanvraag voor naleving toorestore of een oude versie van de toepassing hello toorun. Zie [lange bewaartermijn](sql-database-long-term-retention.md).
* Zie tooperform een terugzetbewerking [database terugzetten vanaf back-ups](sql-database-recovery-using-backups.md).

> [!NOTE]
> In Azure storage Hallo term *replicatie* toocopying bestanden vanaf één locatie tooanother verwijst. De SQL *databasereplicatie* tookeeping toomultiple secundaire databases gesynchroniseerd met een primaire database verwijst. 
> 

## <a name="how-much-backup-storage-is-included-at-no-cost"></a>Hoeveel back-upopslag is opgenomen kosteloos?
SQL-Database biedt een too200% van de maximale ingerichte databaseopslag als back-upopslag zonder extra kosten. Bijvoorbeeld, als er een Standard database-exemplaar met een ingerichte DB-grootte van 250 GB, hebt u 500 GB aan back-upopslag zonder extra kosten. Als uw database groter is dan de opgegeven back-upopslag hello, kunt u tooreduce Hallo bewaarperiode contact opnemen met de ondersteuning van Azure. Een andere optie is toopay voor aanvullende back-up die wordt gefactureerd snelheid Hallo standard-geografisch redundante opslag met leestoegang (RA-GRS). 

## <a name="how-often-do-backups-happen"></a>Hoe vaak gebeuren back-ups?
Volledige databaseback-ups gebeuren wekelijks, differentiële back-ups in het algemeen gebeuren elk paar uur en transactielogboek back-ups in het algemeen gebeuren elke 5-10 minuten. Hallo eerste volledige back-up is gepland onmiddellijk nadat een database wordt gemaakt. Meestal is voltooid binnen 30 minuten, maar het kan langer duren wanneer omvangrijke Hallo-database. De eerste back-up Hallo kan bijvoorbeeld duurt langer op een herstelde database of een databasekopie. Na het Hallo eerste volledige back-up, alle verdere back-ups worden automatisch gepland en achtergrond beheerd op Hallo achtergrond. Hallo precieze timing van alle databaseback-ups wordt bepaald door Hallo SQL Database-service omdat het een compromis tussen de algehele Hallo system werkbelasting. 

Hallo back-upopslag geo-replicatie vindt plaats op basis van hello Azure Storage-replicatieschema.

## <a name="how-long-do-you-keep-my-backups"></a>Hoe lang houdt u de back-ups?
De back-up van elke SQL-Database heeft een bewaarperiode die is gebaseerd op Hallo [servicelaag](sql-database-service-tiers.md) van Hallo-database. Hallo bewaarperiode voor een database in de:


* Basic-servicelaag is 7 dagen.
* Standaard-servicelaag is 35 dagen.
* Premium servicecategorie is 35 dagen.

Als u de database van Hallo Standard of Premium service lagen tooBasic downgraden, worden back-ups Hallo opgeslagen voor de zeven dagen. Alle bestaande back-ups ouder zijn dan zeven dagen zijn niet meer beschikbaar. 

Als u de database vanaf Hallo Basic service tier tooStandard of Premium bijwerkt, houdt bij SQL-Database bestaande back-ups totdat deze 35 dagen oud zijn. Nieuwe back-ups blijven wanneer deze zich voor 35 dagen voordoen.

Als u een database verwijdert, SQL Database Hallo back-ups blijft in Hallo dezelfde manier zou voor een online-database. Stel bijvoorbeeld dat u een Basic-database met een bewaarperiode van zeven dagen verwijderd. Een back-up die is vier dagen oud is opgeslagen voor drie dagen.

> [!IMPORTANT]
> Als u hello Azure SQL-server die als host fungeert voor SQL-Databases verwijdert, worden alle databases die deel uitmaken van de server toohello worden ook verwijderd en kunnen niet worden hersteld. U kunt een verwijderde server niet herstellen.
> 

## <a name="how-tooextend-hello-backup-retention-period"></a>Hoe tooextend Hallo back-up bewaarperiode?
Als uw toepassing vereist dat back-ups Hallo beschikbaar voor langere tijd zijn kunt u Hallo ingebouwde bewaarperiode uitbreiden door Hallo op lange termijn back-up bewaarbeleid voor afzonderlijke databases (LTR beleid) configureren. Hiermee kunt u tooextend Hallo gebouwd it bewaarperiode van 35 dagen tooup too10 jaar. Zie [Langetermijnretentie](sql-database-long-term-retention.md) voor meer informatie.

Als u Hallo LTR beleid tooa database via Azure portal of API toevoegt, Hallo wekelijkse volledige back-ups worden automatisch gekopieerd tooyour eigenaar van de Azure Backup-Service-kluis. Als uw database is versleuteld met worden automatisch TDE Hallo back-ups in rust versleuteld.  Hallo Services-kluis worden automatisch verwijderd van uw verlopen back-ups op basis van hun timestamp en Hallo LTR beleid.  Zodat u niet nodig toomanage Hallo back-upschema of zorgen over het opruimen van Hallo Hallo oude bestanden. Hallo terugzetten API ondersteunt back-ups opgeslagen in Hallo vault zolang Hallo kluis Hallo hetzelfde abonnement als uw SQL-database. U kunt hello Azure-portal of PowerShell tooaccess gebruiken deze back-ups.

> [!TIP]
> Zie voor een hoe tooguide [en herstel van back-up op lange termijn bewaren van Azure SQL Database configureren](sql-database-long-term-backup-retention-configure.md)
>

## <a name="are-backups-encrypted"></a>Back-ups versleuteld?

Als TDE is ingeschakeld voor een Azure SQL database, worden back-ups eveneens versleuteld. Alle nieuwe Azure SQL-databases zijn geconfigureerd met TDE standaard ingeschakeld. Zie voor meer informatie over TDE [Transparent Data Encryption met Azure SQL Database](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database).

## <a name="next-steps"></a>Volgende stappen

- Databaseback-ups zijn een essentieel onderdeel van een zakelijke continuïteit en noodherstel herstelstrategie omdat ze uw gegevens tegen per ongeluk beschadigd of verwijderd beschermen. toolearn over andere oplossingen Azure SQL Database business continuity hello, Zie [Business continuity overview](sql-database-business-continuity.md).
- Zie toorestore tooa punt in tijd hello Azure-portal met [herstelpunt database tooa met behulp van Azure-portal Hallo](sql-database-recovery-using-backups.md).
- toorestore tooa punt in tijd met behulp van PowerShell, Zie [herstelpunt database tooa met behulp van PowerShell](scripts/sql-database-restore-database-powershell.md).
- tooconfigure, beheren en herstellen van lange bewaartermijn van automatische back-ups in een Azure Recovery Services-kluis Hallo met Azure portal, Zie [beheren op lange termijn bewaren van back-up met behulp van Azure-portal Hallo](sql-database-long-term-backup-retention-configure.md).
- tooconfigure, beheren, en herstel van lange bewaartermijn van automatische back-ups in een Azure Recovery Services-kluis met behulp van PowerShell, Zie [lange Backup-bewaartermijn met behulp van PowerShell beheren](sql-database-long-term-backup-retention-configure.md).
