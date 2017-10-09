---
title: Database - aaaSQL automatische afstemming | Microsoft Docs
description: SQL-Database analyseert SQL-query en wordt automatisch aanpast toouser werkbelasting.
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: jovanpop
ms.openlocfilehash: 897a8deaabedb6727dc49958c64d0433c5f2e4f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-tuning"></a>Automatisch instellen

Azure SQL-Database is een volledig beheerde gegevensservice die wordt bewaakt Hallo-query's die worden uitgevoerd op Hallo-database en kunnen de prestaties van de werkbelasting Hallo automatisch verbeteren. Azure SQL-Database heeft een ingebouwde intelligentie mechanisme waarmee automatisch kunt afstemmen en de prestaties van uw query's verbeteren door dynamisch aan te passen Hallo database tooyour werkbelasting. Automatische afstemming in Azure SQL Database is mogelijk een van de belangrijkste Hallo-functies die u op de Azure SQL Database toooptimize prestaties van uw query's inschakelen kunt.

Raadpleeg dit artikel voor stappen hello te[inschakelen automatische afstemming](sql-database-automatic-tuning-enable.md) met behulp van hello Azure-portal.

## <a name="why-automatic-tuning"></a>Waarom automatische afstemming?

Een van de belangrijkste taken in de klassieke databasebeheer Hallo Hallo werkbelasting, bewaakt het identificeren van essentiële SQL query's, indexen die moeten worden toegevoegd als tooimprove prestaties en indexen wordt zelden gebruikt. Azure SQL Database biedt gedetailleerde inzicht in de Hallo query's en indexen, moet u toomonitor. Maar doorlopende databasebewaking is een moeilijke, tijdrovende taak, zeker wanneer het om vele databases gaat. Het beheren van een zeer groot aantal databases mogelijk onmogelijk toodo efficiënt zelfs met alle beschikbare hulpprogramma's en rapporten die Azure SQL Database en de Azure-portal bieden. In plaats van controleren en de database handmatig afstemmen, kunt u overwegen delegeren aantal Hallo controleren en afstemmen acties tooAzure SQL-Database met behulp van de functie voor automatisch afstemmen. 


> [!VIDEO https://channel9.msdn.com/Blogs/Azure-in-the-Enterprise/Enabling-Azure-SQL-Database-Auto-Tuning-at-Scale-for-Microsoft-IT/player]
>

## <a name="how-does-automatic-tuning-work"></a>Hoe werkt automatische afstemmen?

Azure SQL-Database heeft een continue prestaties en -analyse proces dat voortdurend gegevens verzamelt over Hallo die kenmerkend zijn voor uw workload en identificeren van mogelijke problemen en verbeteringen.

![Automatische afstemmen-proces](./media/sql-database-automatic-tuning/tuning-process.png)

In dit proces kunt Azure SQL Database toodynamically tooyour werkbelasting aanpassen door te zoeken welke indexen en abonnementen op de prestaties van uw werkbelastingen verbeteren kunnen en wat indexen van invloed op uw werkbelastingen. Op basis van deze resultaten, maatregelen automatische afstemming afstemmen ter verbetering van de prestaties van uw workload. Bovendien voortdurend Azure SQL Database prestaties na elke wijziging door automatische afstemmen tooensure dat verbetert de prestaties van uw workload. Een actie op die u hebt niet de prestaties verbeteren, wordt automatisch hersteld. Dit verificatieproces is een belangrijke functie die ervoor zorgt dat elke wijziging door automatische afstemming Hallo prestaties van uw workload komt niet verkleinen.

Er zijn twee automatische afstemmen aspecten die beschikbaar in Azure SQL Database zijn:

 -  **Automatische indexbeheer** die identificeert indexen die moeten worden toegevoegd in de database en indexen die moeten worden verwijderd.
 -  **Automatische plan correctie** (binnenkort beschikbaar, al beschikbaar in SQL Server 2017) die problematisch plannen identificeert en correcties SQL plan prestatieproblemen.

## <a name="automatic-index-management"></a>Automatische indexbeheer

Beheer van de index is in Azure SQL Database eenvoudig omdat Azure SQL Database gegevens over uw werkbelasting verzamelt en zorgt ervoor dat uw gegevens altijd optimaal is geïndexeerd. Ontwerp voor de juiste index is van cruciaal belang voor optimale prestaties van uw werkbelasting en beheer van de automatische index kunt u de indexen optimaliseren. Automatische indexbeheer kunt prestatieproblemen in onjuist geïndexeerde databases corrigeren of onderhouden en verbetert u de indexen op Hallo bestaande databaseschema. 

### <a name="why-do-you-need-index-management"></a>Waarom moet u beheer van de index?

Indexen versnellen de zoekopdrachten die gegevens uit het Hallo-tabellen lezen. ze kunnen echter Hallo-query's die gegevens bijwerken vertragen. U moet toocarefully analyseren wanneer toocreate een index en welke kolommen moet tooinclude in Hallo index. Sommige indexen mogelijk niet na enige tijd nodig. Daarom moet u tooperiodically identificeren en verwijder Hallo-indexen die niet in de voordelen weergegeven worden. Als u negeren Hallo ongebruikte indexen, prestaties van query's Hallo die gegevens bijwerken zonder een voordeel op Hallo-query's die gegevens lezen zou worden verlaagd. Ongebruikte indexen ook van invloed op prestaties van Hallo system omdat aanvullende updates onnodige logboekregistratie vereisen.

Hallo optimale set indexen ter verbetering van de prestaties van query's Hallo die gegevens lezen uit de tabellen en minimale invloed hebben op updates te zoeken, mogelijk continue en complexe analyse.

Azure SQL Database maakt gebruik van ingebouwde intelligentie en geavanceerde regels die het analyseren van uw query's, indexen die optimaal is voor de werkbelasting van uw huidige identificeren en Hallo indexen mogelijk verwijderd. Azure SQL Database zorgt ervoor dat u hebt een minimaal benodigde aantal indexen die optimaliseren Hallo-query's die gegevens lezen, Hallo Hallo geminimaliseerd impact op de andere query's.

### <a name="how-tooidentify-indexes-that-need-toobe-changed-in-your-database"></a>Hoe indexeert tooidentify die behoefte toobe gewijzigd in de database?

Azure SQL Database kunt gemakkelijk beheerproces van de index. In plaats van Hallo klus zijn van een handmatige werkbelasting analyse en bewaking van de index, Azure SQL Database analyseert uw werkbelasting identificeert Hallo-query's die snel kunnen worden uitgevoerd met een nieuwe index en niet-gebruikte of dubbele indexen identificeert. Meer informatie over de identificatie van de indexen die moeten worden gewijzigd op [indexaanbevelingen vinden in Azure portal](sql-database-advisor-portal.md).

### <a name="automatic-index-management-considerations"></a>Automatische index beheeroverwegingen

Als u merkt dat ingebouwde regels Hallo Hallo prestaties van uw database, kunt u mogelijk uw indexen automatisch beheren van Azure SQL-database.

Acties vereist toocreate nodig indexen in Azure SQL-Databases mogelijk gebruik van bronnen en ondersteuningsbeheerder invloed hebben op prestaties van de werkbelasting. toominimize hello gevolgen van het maken van een index op de prestaties van de werkbelasting, Azure SQL Database vindt de juiste tijdvenster Hallo voor een bewerking voor het beheer van een index. Actie afstemming is uitgesteld als Hallo-database resources tooexecute uw werkbelasting moet en gestart wanneer het Hallo-database heeft voldoende ongebruikte bronnen die kunnen worden gebruikt voor de onderhoudstaak Hallo. Een belangrijk onderdeel in automatische indexbeheer is een verificatie van Hallo acties. Wanneer Azure SQL Database maakt of index zakt, analyseert een controleproces prestaties van uw werkbelasting tooverify dat Hallo actie Hallo prestaties verbeterd. Als dit niet aanzienlijke verbetering opleveren – Hallo actie onmiddellijk wordt teruggedraaid. Op deze manier voor Azure SQL Database zorgt ervoor dat automatische acties dit geen negatieve invloed prestaties van uw workload. Indexen die zijn gemaakt door automatische afstemming NLB is zichtbaar voor de onderhoudsbewerking Hallo op Hallo onderliggende schema. Wijzigingen in het schema zoals verwijderen of hernoemen van kolommen worden niet geblokkeerd door Hallo aanwezigheid van automatisch gemaakte indexen. Indexen die automatisch worden gemaakt met Azure SQL Database worden onmiddellijk verwijderd wanneer gerelateerde tabel- of -kolommen wordt verwijderd.

## <a name="automatic-plan-choice-correction"></a>Automatische plan keuze correctie

Correctie van automatische planning is een nieuwe automatische afstemmen functie toegevoegd in SQL Server 2017 CTP2.0 waarmee SQL-schema's die zijn vastgelopen. Deze optie voor automatisch afstemmen is binnenkort beschikbaar in Azure SQL-Database. Meer informatie op [automatische afstemming in SQL Server 2017](https://docs.microsoft.com/sql/relational-databases/automatic-tuning/automatic-tuning).

## <a name="next-steps"></a>Volgende stappen

- tooenable automatische afstemming in Azure SQL Database en kunnen automatische afstemming functie volledig uw werkbelasting beheren, Zie [inschakelen automatische afstemming](sql-database-automatic-tuning-enable.md).
- toouse handmatige afstemmen, kunt u bekijken [afstemmen aanbevelingen in Azure-portal](sql-database-advisor-portal.md) en handmatig toepassen Hallo die de prestaties van uw query's verbeteren.
