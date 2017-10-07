---
title: aaaStore Azure SQL Database back-ups voor up too10 jaar | Microsoft Docs
description: Meer informatie over hoe Azure SQL Database ondersteunt opslag back-ups voor up too10 jaar.
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a>Azure SQL Database back-ups opslaan voor up too10 jaar
Veel toepassingen hebben regelgeving, compatibiliteit of andere zakelijke doeleinden die vereisen dat u tooretain databaseback-ups buiten Hallo 7 35 dagen geleverd door de Azure SQL Database [automatische back-ups](sql-database-automated-backups.md). Hallo op lange termijn bewaren van back-functie gebruikt, kunt u uw back-ups van SQL database opslaan in een Azure Recovery Services-kluis voor up too10 jaar. U kunt opslaan van too1, 000 databases per kluis. Vervolgens kunt u back-up in Hallo kluis toorestore als een nieuwe database.

> [!IMPORTANT]
> Lange bewaartermijn van de back-up is momenteel in preview en beschikbaar zijn in de volgende regio's Hallo: Australië-Oost, Australië-Zuidoost, Brazilië-Zuid, VS-midden, Oost-Azië, VS-Oost, VS-Oost 2, India centraal, India-Zuid, Japan-Oost, Japan-West, Noordelijk Centraal, VS, Noord Europa, Zuid-centraal VS, Zuidoost-Azië, West-Europa en VS-West.
>

> [!NOTE]
> U kunt inschakelen van de databases too200 per kluis gedurende een periode van 24 uur. Het is raadzaam dat u een afzonderlijke kluis voor elke server toominimize Hallo gevolgen van deze limiet gebruiken. 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a>De werking van de back-up op lange termijn bewaren van SQL-Database

Met bewaren van back-up op lange termijn, kunt u een SQL database-server koppelen aan een Azure Recovery Services-kluis. 

* U moet Hallo kluis maken in dezelfde Azure-abonnement dat Hallo SQL-server gemaakt Hallo en Hallo in dezelfde geografische regio en resource-groep. 
* Configureert u een bewaarbeleid voor elke database. Hallo beleid oorzaken Hallo wekelijkse volledige databaseback-ups toobe gekopieerd toohello Recovery Services-kluis en bewaard voor de opgegeven bewaarperiode hello (omhoog too10 jaar). 
* Vervolgens kunt u Hallo database terugzetten vanuit een van deze back-ups tooa nieuwe database in een willekeurige server in het Hallo-abonnement. Azure-opslag maakt een kopie van de bestaande back-ups en Hallo-exemplaar heeft geen invloed prestaties op Hallo bestaande database.

> [!TIP]
> Zie voor een hoe tooguide [en herstel van back-up op lange termijn bewaren van Azure SQL Database configureren](sql-database-long-term-backup-retention-configure.md).

## <a name="enable-long-term-backup-retention"></a>Lange bewaartermijn van de back-up inschakelen

tooconfigure lange Backup-bewaartermijn voor een database:

1. Een Azure Recovery Services-kluis maken in Hallo dezelfde regio, abonnement en resource-groep als uw SQL database-server. 
2. Hallo server toohello kluis registreren.
3. Maak een beleid voor Azure Recovery Services-beveiliging.
4. Toepassing hello beveiliging beleid toohello databases waarvoor het langdurig bewaren van back-up.

tooconfigure, beheren, en een database herstellen via langdurig bewaren van back-up van automatische back-ups in een Azure Recovery Services-kluis en voer een van de volgende Hallo:

* Azure-portal met behulp van Hallo: klik op **lange bewaartermijn van de back-**, selecteert u een database en klik vervolgens op **configureren**. 

   ![Selecteer een database voor lange bewaartermijn van de back-up](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* Met behulp van PowerShell: Ga te[en herstel van back-up op lange termijn bewaren van Azure SQL Database configureren](sql-database-long-term-backup-retention-configure.md).

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a>Herstellen van een database die opgeslagen met Hallo op lange termijn bewaren van back-functie

toorecover van back-up op lange termijn bewaren van back-up:

1. Lijst Hallo kluis waar Hallo back-up is opgeslagen.
2. Lijst Hallo-container die is toegewezen tooyour logische server.
3. Hallo lijstgegevensbron binnen Hallo kluis die is toegewezen tooyour-database.
4. Lijst Hallo herstelpunten die toorestore beschikbaar zijn.
5. Hallo-database terugzetten vanaf Hallo herstelpunt toohello doelserver binnen uw abonnement.

tooconfigure, beheren, en een database herstellen via langdurig bewaren van back-up van automatische back-ups in een Azure Recovery Services-kluis en voer een van de volgende Hallo:

* Azure-portal met behulp van Hallo: Ga te[beheren op lange termijn bewaren van back-up met behulp van Azure-portal Hallo](sql-database-long-term-backup-retention-configure.md). 

* Met behulp van PowerShell: Ga te[lange Backup-bewaartermijn met behulp van PowerShell beheren](sql-database-long-term-backup-retention-configure.md).

## <a name="get-pricing-for-long-term-backup-retention"></a>Prijzen voor lange bewaartermijn van de back-ophalen

Lange bewaartermijn van back-up van een SQL-database wordt in rekening gebracht volgens toohello [Azure Backup-services prijzen tarieven](https://azure.microsoft.com/pricing/details/backup/).

Nadat de Hallo SQL database-server is geregistreerd toohello kluis, worden in rekening gebracht voor Hallo totale opslag die wordt gebruikt door Hallo wekelijkse back-ups opgeslagen in de kluis Hallo.

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a>Beschikbare back-ups weergeven die zijn opgeslagen in lange bewaartermijn van de back-up

tooconfigure, beheren, en een database herstellen via langdurig bewaren van back-up van automatische back-ups in een Azure Recovery Services-kluis via hello Azure-portal, een van de volgende Hallo:

* Azure-portal met behulp van Hallo: Ga te[beheren op lange termijn bewaren van back-up met behulp van Azure-portal Hallo](sql-database-long-term-backup-retention-configure.md). 

* Met behulp van PowerShell: Ga te[lange Backup-bewaartermijn met behulp van PowerShell beheren](sql-database-long-term-backup-retention-configure.md).

## <a name="disable-long-term-retention"></a>Lange bewaartermijn uitschakelen

Hallo-recovery-service verwerkt automatisch opschonen van back-ups op basis van opgegeven bewaarbeleid Hallo Hallo. 

toostop verzenden Hallo-back-ups voor een specifieke database toohello-kluis verwijderen Hallo bewaarbeleid voor die database.
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> Hallo back-ups die zich al in de kluis Hallo worden hierdoor niet beïnvloed. Ze worden automatisch verwijderd door de herstelservice Hallo wanneer de bewaartermijn is verstreken.

## <a name="long-term-backup-retention-faq"></a>Lange bewaartermijn in back-Veelgestelde vragen

**Kan ik specifieke back-ups in de kluis Hallo handmatig verwijderen?**

Momenteel niet. back-ups ruimt Hallo kluis automatisch wanneer Hallo bewaarperiode is verlopen.

**Kan ik mijn server toostore back-ups toomore dan een kluis registreren?**

U kunt een kluis voor back-ups tooonly Nee, momenteel opslaan op een tijdstip.

**Kan ik een kluis en de server hebben met verschillende abonnementen?**

Nee, momenteel Hallo kluis en server moeten zich op Hallo hetzelfde abonnement en de resource-groep.

**Kan ik een kluis die ik in een regio die verschilt van mijn server regio gemaakt gebruiken?**

Nee, Hallo kluis en server moeten zich in Hallo dezelfde regio toominimize tijd kopiëren en te voorkomen dat verkeer kosten.

**Hoeveel databases kan ik opslaan in een kluis?**

Op dit moment ondersteunen we up too1, 000 databases per kluis. 

**Het aantal kluizen kan ik maken per abonnement?**

U kunt maken van too25 kluizen per abonnement.

**Hoeveel databases kan ik per dag per kluis configureren?**

U kunt 200 databases per dag per kluis instellen.

**Werkt langdurig bewaren van back-up met elastische pools?**

Ja. Elke database in de groep Hallo kan worden geconfigureerd met Hallo bewaarbeleid.

**Kan ik kiezen Hallo tijdstip waarop Hallo back-up is gemaakt?**

Nee, bepaalt de SQL-Database Hallo back-upschema toominimize Hallo invloed op de prestaties van uw databases.

**Ik heb transparante gegevensversleuteling is ingeschakeld voor de database. Kan ik deze met de kluis hello gebruiken?** 

Ja, transparante gegevensversleuteling wordt ondersteund. Zelfs als de oorspronkelijke database Hallo niet meer bestaat, kunt u uit de kluis Hallo Hallo-database herstellen.

**Wat gebeurt er met Hallo back-ups in de kluis Hallo als mijn abonnement wordt onderbroken?** 

Als uw abonnement wordt onderbroken, behouden we Hallo bestaande databases en de back-ups. Nieuwe back-ups zijn niet gekopieerd toohello kluis. Nadat u Hallo abonnement opnieuw activeert, hervat Hallo service kluis voor back-ups toohello kopiëren. Uw kluis wordt toegankelijk toohello herstelbewerkingen met behulp van Hallo back-ups die zijn gekopieerd er voordat het Hallo-abonnement is onderbroken. 

**Krijg ik toegang tot toohello SQL database back-upbestanden zodat ik kan downloaden of ze toohello SQL server herstellen?**

Nee, momenteel niet.

**Is het mogelijk toohave meerdere plant (dagelijks, wekelijks, maandelijks, jaarlijks) binnen een bewaarbeleid SQL.**

Nee, meerdere schema's zijn momenteel alleen beschikbaar voor back-ups van virtuele machine.

**Wat gebeurt er als we langdurig bewaren van back-up voor een database die is een secundaire actieve geo-replicatie-database hebt ingesteld?**

Omdat er geen back-ups op replica's onderneemt, is er momenteel geen optie voor het bewaren van de lange termijn back-up op secundaire databases. Het is echter belangrijk voor gebruikers tooset up langdurig bewaren van back-up op een secundaire actieve geo-replicatie-database om deze redenen:
* Wanneer een failover gebeurt en Hallo-database een primaire database wordt, duurt we een volledige back-up, namelijk geüploade toovault.
* Er is geen extra kosten toohello klant voor het instellen van langdurig bewaren van back-up op een secundaire database.

## <a name="next-steps"></a>Volgende stappen
Omdat de databaseback-ups voorkomen dat gegevens per ongeluk beschadigd of verwijderd, zijn ze een essentieel onderdeel van een zakelijke continuïteit en noodherstelplan. toolearn over andere SQL-Database-oplossingen voor bedrijfscontinuïteit hello, Zie [Business continuity overview](sql-database-business-continuity.md).
