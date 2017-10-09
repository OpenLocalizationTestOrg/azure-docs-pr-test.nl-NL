---
title: een Azure SQL-database vanuit een back-up aaaRestore | Microsoft Docs
description: Meer informatie over punt in tijd herstellen, waarmee u tooroll back een Azure SQL Database tooa vorige punt in tijd (omhoog too35 dagen).
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: fd1d334d-a035-4a55-9446-d1cf750d9cf7
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.openlocfilehash: 84ecc306a2072445c10dbf1e9d7cf3d1b43860cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="recover-an-azure-sql-database-using-automated-database-backups"></a>Een Azure SQL-database herstelt via automatische databaseback-ups
SQL Database biedt deze opties voor het gebruik van de database recovery [automatische databaseback-ups](sql-database-automated-backups.md) en [back-ups in lange bewaartermijn](sql-database-long-term-retention.md). U kunt herstellen met een databaseback-up naar:

* Een nieuwe database op dezelfde logische server hersteld Hallo tooa opgegeven punt in tijd binnen de bewaarperiode Hallo. 
* Een database op Hallo dezelfde logische server tijd voor het verwijderen van toohello voor een verwijderde database herstellen.
* Een nieuwe database op een logische server in elke regio hersteld toohello punt van Hallo meest recente dagelijkse back-ups in geogerepliceerde blob-opslag (RA-GRS).

> [!IMPORTANT]
> Een bestaande database kan niet worden overschreven tijdens het terugzetten.
>

U kunt ook [automatische databaseback-ups](sql-database-automated-backups.md) toocreate een [kopiëren van de database](sql-database-copy.md) op een logische server in elke regio. 

## <a name="recovery-time"></a>Hersteltijd
Hallo herstel tijd toorestore een database met behulp van automatische databaseback-ups is beïnvloed door diverse factoren: 

* Hallo-grootte van Hallo-database
* Hallo prestatieniveau van Hallo-database
* het aantal betrokken transactielogboeken Hallo
* Hallo hoeveelheid activiteit die toobe behoeften replay toorecover toohello herstelpunt
* Hallo-netwerkbandbreedte is als Hallo herstellen tooa andere regio 
* het aantal gelijktijdige terugzetten Hallo aanvragen in Hallo doelregio wordt verwerkt. 
  
  Voor een database erg groot en/of actieve kan Hallo terugzetten enkele uren duren. Als er langdurige storing in een regio, is het mogelijk dat er grote aantallen geo-restore-aanvragen worden verwerkt door een andere regio's zijn. Wanneer er veel aanvragen, kan de hersteltijd Hallo verhogen voor databases in deze regio. De meeste database herstelt voltooid binnen de 12 uur.
  
Er is geen ingebouwde functionaliteit toodo bulksgewijs herstel. Hallo [Azure SQL Database: volledige Server Recovery](https://gallery.technet.microsoft.com/Azure-SQL-Database-Full-82941666) script is een voorbeeld van een manier van deze taak uitvoeren.

> [!IMPORTANT]
> met behulp van toorecover geautomatiseerde back-ups, moet u lid zijn van Hallo Inzender van SQL Server-rol in Hallo abonnement of Hallo abonnement eigenaar. U kunt herstellen met behulp van hello Azure-portal, PowerShell of Hallo REST-API. U kunt Transact-SQL niet gebruiken. 
> 

## <a name="point-in-time-restore"></a>Punt In tijd terugzetten

U kunt een bestaande database terugzetten tooan eerder punt in tijd als een nieuwe database op Hallo dezelfde logische server met behulp van Azure-portal Hallo [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), of Hallo [REST-API](https://msdn.microsoft.com/library/azure/mt163685.aspx). 

> [!TIP]
> Voor een PowerShell-voorbeeldscript die laat zien hoe tooperform punt in tijd terugzetten van een database, Zie [herstellen van een SQL-database met behulp van PowerShell](scripts/sql-database-restore-database-powershell.md).
>

Hallo-database kan worden herstelde tooany servicelaag of de prestaties, en als een individuele database of in een elastische pool. Controleer of er voldoende bronnen op Hallo logische server of in Hallo elastische pool toowhich u Hallo database terugzet. Hierna kunt is hersteld Hallo database een normale, volledig toegankelijk zijn, online database. Hallo hersteld database wordt in rekening gebracht volgens de normale tarieven op basis van het serviceniveau prijscategorie en prestatieniveau. U bent niet worden kosten in rekening totdat Hallo database terugzetten voltooid is.

U doorgaans een tooan database terugzetten eerder punt herstellen. Wanneer u dit doet, kunt u ze Hallo database teruggezet als vervanging voor de oorspronkelijke database Hallo of gebruik het tooretrieve gegevens uit en werk vervolgens de oorspronkelijke database Hallo. 

* ***Vervanging van de database:*** als Hallo hersteld database is bedoeld als vervanging voor de oorspronkelijke database hello, moet u controleren of het prestatieniveau Hallo en/of servicelaag geschikt zijn en schalen Hallo database indien nodig. U kunt Hallo oorspronkelijke database wijzigen en vervolgens geven Hallo hersteld Hallo oorspronkelijke databasenaam met de opdracht ALTER DATABASE Hallo in T-SQL. 
* ***Herstel van gegevens:*** als u van plan tooretrieve gegevens uit de database-toorecover Hallo hersteld van een gebruiker of toepassing fout bent, u moet toowrite en Hallo gegevens die nodig zijn scripts tooextract herstelgegevens van Hallo hersteld database toohello uitvoeren oorspronkelijke database. Hoewel Hallo restore-bewerking een toocomplete lange tijd duren kan, is Hallo herstellen van database zichtbaar in Hallo databaselijst tijdens het herstelproces Hallo. Als u tijdens het terugzetten van Hallo Hallo database hebt verwijderd, Hallo restore-bewerking is geannuleerd en u niet weet in rekening gebracht voor Hallo-database die Hallo restore kan niet worden voltooid. 

### <a name="azure-portal"></a>Azure Portal

toorecover tooa punt in tijd met behulp van Azure-portal, open Hallo-pagina voor uw database en klik op Hallo **herstellen** op Hallo-werkbalk.

![punt in tijd terugzetten](./media/sql-database-recovery-using-backups/point-in-time-recovery.png)

## <a name="deleted-database-restore"></a>Herstellen van verwijderde database
U kunt een verwijderde database-tijd voor het verwijderen van toohello herstellen voor een verwijderde database op Hallo Azure-portal met behulp van dezelfde logische server Hallo [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), of Hallo [REST (createMode = herstellen)](https://msdn.microsoft.com/library/azure/mt163685.aspx). 

> [!TIP]
> Voor een voorbeeld van een PowerShell script tonen hoe een verwijderde database toorestore zien [herstellen van een SQL-database met behulp van PowerShell](scripts/sql-database-restore-database-powershell.md).
>

> [!IMPORTANT]
> Als u een exemplaar van Azure SQL Database-server verwijdert, worden alle bijbehorende databases worden ook verwijderd en kunnen niet worden hersteld. Er is momenteel geen ondersteuning voor het herstellen van een server verwijderd.
> 

### <a name="azure-portal"></a>Azure Portal

toorecover een verwijderde database gedurende de [bewaarperiode](sql-database-service-tiers.md) met hello Azure-portal openen Hallo pagina voor uw server en in Hallo Operations gebied, klikt u op **databases verwijderd**.

![verwijderd-database-restore-1](./media/sql-database-recovery-using-backups/deleted-database-restore-1.png)


![verwijderd-database-restore-2](./media/sql-database-recovery-using-backups/deleted-database-restore-2.png)

## <a name="geo-restore"></a>Geo-herstel
U kunt een SQL-database op elke server in een Azure-regio van Hallo meest recente geogerepliceerde volledige differentiële back-ups en herstellen. Geo-herstel een geografisch redundante back-up gebruikt als de bron- en kan worden gebruikt toorecover een database zelfs als het Hallo-database of een datacenter niet toegankelijk vanwege tooan storing is. 

Geo-restore is de standaardoptie herstel Hallo wanneer uw database is niet beschikbaar vanwege een incident in Hallo regio waar Hallo-database wordt gehost. Als een grootschalige incident in een regio, worden niet beschikbaar zijn van uw databasetoepassing, kunt u een database herstellen van Hallo geogerepliceerde back-ups tooa server in een andere regio. Er is een vertraging tussen wanneer een differentiële back-up is gemaakt en wanneer is het geogerepliceerde tooan Azure blob in een andere regio. Deze vertraging van tooan uur, dus als er een ramp optreedt, kunnen er up tooone uur gegevens verloren gaan. Hallo volgende afbeelding ziet u het herstellen van database Hallo van Hallo laatste beschikbare back-up in een andere regio.

![geo-herstel](./media/sql-database-geo-restore/geo-restore-2.png)

> [!TIP]
> Voor een voorbeeld van een PowerShell script weergeeft hoe tooperform geo-restore zien [herstellen van een SQL-database met behulp van PowerShell](scripts/sql-database-restore-database-powershell.md).
> 

Punt in tijd terugzetten op een secundaire geo-server is momenteel niet ondersteund. Punt in tijd terugzetten kan alleen op een primaire database worden uitgevoerd. Zie voor gedetailleerde informatie over het gebruik van toorecover geo-herstel van een storing [herstellen van een storing](sql-database-disaster-recovery.md).

> [!IMPORTANT]
> Herstel van back-ups Hallo meest eenvoudige van Hallo noodherstel is beschikbaar in SQL Database met oplossingen voor herstel Hallo langste RPO en schatting herstel tijd (invoegen). Geo-restore is voor oplossingen met behulp van Basic databases, vaak een redelijke DR-oplossing met een invoegen van 12 uur. Voor oplossingen met behulp van grotere Standard of Premium-databases die korter hersteltijden nodig hebt, moet u overwegen [actieve geo-replicatie](sql-database-geo-replication-overview.md). Actieve geo-replicatie biedt een veel lager RPO en invoegen als alleen u moet een failover tooa continu gerepliceerd secundaire initiëren. Zie voor meer informatie over zakelijke contiuity keuzes [van zakelijke continuïteit](sql-database-business-continuity.md).
> 

### <a name="azure-portal"></a>Azure Portal

toogeo-terugzetten van een database tijdens de [bewaarperiode](sql-database-service-tiers.md) hello Azure-portal gebruikt, open Hallo SQL-Databases pagina en klik vervolgens op **toevoegen**. In Hallo **Select bron** in het tekstvak, selecteer **back-up**. Geef Hallo back-up uit welke tooperform Hallo recovery in Hallo regio en op Hallo van server van uw keuze. 

## <a name="programmatically-performing-recovery-using-automated-backups"></a>Herstel met behulp van automatische back-ups uitvoeren via een programma
Als eerder beschreven bovendien toohello Azure-portal databaseherstel kan worden uitgevoerd via een programma met Azure PowerShell of Hallo REST-API. Hallo volgende tabellen beschrijven Hallo reeks opdrachten die beschikbaar zijn.

### <a name="powershell"></a>PowerShell
| Cmdlet | Beschrijving |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |Hiermee haalt u een of meer databases. |
| [Get-AzureRMSqlDeletedDatabaseBackup](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | Hiermee haalt u een verwijderde database die u kunt herstellen. |
| [Get-AzureRmSqlDatabaseGeoBackup](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) |Hiermee haalt u een geografisch redundante back-up van een database. |
| [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) |Een SQL-database herstelt. |
|  | |

### <a name="rest-api"></a>REST API
| API | Beschrijving |
| --- | --- |
| [REST (createMode = Recovery)](https://msdn.microsoft.com/library/azure/mt163685.aspx) |Hiermee herstelt u een database |
| [Get maken of bijwerken van de databasestatus](https://msdn.microsoft.com/library/azure/mt643934.aspx) |Retourneert Hallo status tijdens een terugzetbewerking |
|  | |

## <a name="summary"></a>Samenvatting
Automatische back-ups beveiligen uw databases van gebruikers- en toepassingsfouten, verwijderen van een database per ongeluk en langdurige uitval. Deze ingebouwde functie is beschikbaar voor alle Servicelagen en prestatieniveaus. 

## <a name="next-steps"></a>Volgende stappen
* Zie voor een overzicht van zakelijke continuïteit en scenario's [Business continuity-overzicht](sql-database-business-continuity.md)
* toolearn over Azure SQL Database automatische back-ups, Zie [geautomatiseerde back-ups van SQL-Database](sql-database-automated-backups.md)
* toolearn over het bewaren van back-up op lange termijn, Zie [lange bewaartermijn van de back-up](sql-database-long-term-retention.md)
* tooconfigure, beheren en herstellen van lange bewaartermijn van automatische back-ups in een Azure Recovery Services-kluis Hallo met Azure portal, Zie [configureren en gebruiken op lange termijn back-up bewaren](sql-database-long-term-backup-retention-configure.md). 
* Zie toolearn over opties voor sneller herstel [actieve geo-replicatie](sql-database-geo-replication-overview.md)  
