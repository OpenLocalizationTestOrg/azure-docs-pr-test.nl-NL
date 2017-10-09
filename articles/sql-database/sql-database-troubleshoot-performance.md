---
title: aaaMonitoring & prestatieafstemming - Azure SQL Database | Microsoft Docs
description: Tips voor het afstemmen in Azure SQL Database via evaluatie en verbetering van de prestaties.
services: sql-database
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
keywords: prestaties van SQL databaseprestaties afstemmen, tips voor het afstemmen van de sql prestaties afstemmen prestatieafstemming voor sql-database
ms.assetid: eb7b3f66-3b33-4e1b-84fb-424a928a6672
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: v-shysun
ms.openlocfilehash: 9e196831902aa6ea841ef14caf5713e82ebfc62d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-performance-tuning"></a>Bewaking en prestaties afstemmen

Azure SQL-Database wordt automatisch beheerd en flexibele gegevensservice waarin u kunt eenvoudig gebruik controleren, toevoegen of verwijderen resources (CPU, geheugen, i/o) aanbevelingen die kunnen verbeteren de prestaties van de database of database tooyour werkbelasting passen, kunnen vinden en automatisch optimaliseren.

In dit artikel biedt een overzicht van controle en prestaties afstemmen van de opties die beschikbaar in Azure SQL Database zijn.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="monitoring-and-troubleshooting-database-performance"></a>Bewaking en probleemoplossing van de prestaties van de database

Azure SQL Database kunt u tooeasily controleren van het Databasegebruik van uw en query's die leiden prestatieproblemen hello tot mogelijk te identificeren. U kunt met behulp van Azure portal of het systeem weergaven databaseprestaties bewaken. Hebt u Hallo opties voor bewaking en probleemoplossing van de prestaties van de database te volgen:

1. In Hallo [Azure-portal](https://portal.azure.com), klikt u op **SQL-databases**Hallo-database en selecteer vervolgens Hallo bewaking grafiek toolook gebruiken voor bronnen bijna de maximale. DTU-verbruik wordt standaard weergegeven. Klik op **bewerken** toochange Hallo tijdsbereik en waarden die worden weergegeven.
2. Gebruik [Query Performance Insight](sql-database-query-performance.md) tooidentify Hallo query's te besteden aan de meest Hallo van resources.
3. U kunt dynamische beheerweergaven (DMV's), Extended Events (`XEvents`), en Hallo Query Store in SSMS tooget prestatieparameters in realtime.

Zie Hallo [prestaties richtlijnen onderwerp](sql-database-performance-guidance.md) toofind technieken waarmee u tooimprove prestaties van Azure SQL Database kunt als u een probleem met deze rapporten of weergaven identificeren.

> [!IMPORTANT] 
> Het verdient aanbeveling dat u altijd hello gebruiken meest recente versie van Management Studio tooremain gesynchroniseerd met updates tooMicrosoft Azure en SQL-Database. [SQL Server Management Studio bijwerken](https://msdn.microsoft.com/library/mt238290.aspx).
>

## <a name="optimize-database-tooimprove-performance"></a>Database-tooimprove optimaliseren

Azure SQL Database kunt u tooidentify verkoopkansen tooimprove en query's optimaliseren zonder resources aan de hand van [prestaties afstemmen aanbevelingen](sql-database-advisor.md). Ontbrekende indexen en onvoldoende geoptimaliseerde query's zijn veelvoorkomende redenen voor slechte databaseprestaties. U kunt deze afstemmen aanbevelingen tooimprove prestaties van uw workload toepassen.
U kunt ook laten Azure SQL-database te[automatisch de prestaties van uw query's optimaliseren](sql-database-automatic-tuning.md) door toe te passen alle aanbevelingen en verifiëren van de verbetering van prestaties van de database hebt geïdentificeerd. U kunt Hallo opties tooimprove prestaties van uw database te volgen:

1. Gebruik [SQL Database Advisor](sql-database-advisor-portal.md) tooview aanbevelingen voor het maken en verwijderen van indexen, parameters voorzien van query's en het oplossen van problemen met schema.
2. [Schakel automatische afstemming](sql-database-automatic-tuning-enable.md) en laat Azure SQL database automatisch prestatieproblemen fix geïdentificeerd.

## <a name="improving-database-performance-with-more-resources"></a>Verbeterde databaseprestaties met meer bronnen

Als er geen bruikbare items die u de prestaties van uw database verbeteren zijn kunnen, kunt u tot slot Hallo hoeveelheid beschikbare resources in Azure SQL Database wijzigen. U kunt meer bronnen toewijzen door Hallo wijzigen [servicelaag](sql-database-service-tiers.md) van een zelfstandige database of verhoog de Hallo edtu's van een elastische pool op elk gewenst moment.
1. Voor zelfstandige databases, kunt u [Servicelagen wijzigen](sql-database-service-tiers.md) op aanvraag tooimprove databaseprestaties.
2. Voor meerdere databases kunt u overwegen [elastische pools](sql-database-elastic-pool-guidance.md) tooscale resources automatisch.

## <a name="tune-and-refactor-application-or-database-code"></a>Afstemmen en verander toepassing of databasecode

U kunt de toepassing code toomore optimaal wijzigen Hallo database gebruiken, indexen wijzigt, forceren plannen of hints toomanually Hallo database tooyour werkbelasting aanpassen. Sommige richtlijnen en tips vinden voor handmatige afstemmen en herschrijven van code in Hallo Hallo [prestaties richtlijnen onderwerp](sql-database-performance-guidance.md) artikel.


## <a name="next-steps"></a>Volgende stappen

- tooenable automatische afstemming in Azure SQL Database en kunnen automatische afstemming functie volledig uw werkbelasting beheren, Zie [inschakelen automatische afstemming](sql-database-automatic-tuning-enable.md).
- toouse handmatige afstemmen, kunt u bekijken [afstemmen aanbevelingen in Azure-portal](sql-database-advisor-portal.md) en handmatig toepassen Hallo die de prestaties van uw query's verbeteren.
- Bronnen die beschikbaar in de database door te wijzigen zijn wijzigen [Azure SQL Database Servicelagen](sql-database-performance-guidance.md)