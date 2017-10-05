---
title: SQL Database - automatische afstemming | Microsoft Docs
description: SQL-Database analyseert SQL-query en wordt automatisch aangepast aan de werkbelasting van de gebruiker.
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
ms.openlocfilehash: f5552793db2d89542782b7d9e8f996314f62e429
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="automatic-tuning"></a>Automatisch instellen

Azure SQL-Database is een volledig beheerde gegevensservice dat de query's die worden uitgevoerd op de database en kunnen de prestaties van de werkbelasting automatisch verbeterd bewaakt. Azure SQL-Database heeft een ingebouwde intelligentie mechanisme waarmee automatisch kunt afstemmen en prestaties van uw query's verbeteren door dynamisch aanpassing van de database naar uw workload. Automatische afstemming in Azure SQL Database is mogelijk een van de belangrijkste functies dat u in Azure SQL-Database inschakelen kunt om de prestaties van uw query's te optimaliseren.

Raadpleeg dit artikel voor de stappen voor het [inschakelen automatische afstemming](sql-database-automatic-tuning-enable.md) met de Azure portal.

## <a name="why-automatic-tuning"></a>Waarom automatische afstemming?

Een van de belangrijkste taken in de klassieke databasebeheer wordt bewaakt door de werkbelasting, kritieke SQL-query's, indexen die moeten worden toegevoegd om prestaties te verbeteren en zelden gebruikte indexen te identificeren. Azure SQL Database biedt gedetailleerde inzicht in de query's en indexen die u wilt bewaken. Maar doorlopende databasebewaking is een moeilijke, tijdrovende taak, zeker wanneer het om vele databases gaat. Het beheren van een zeer groot aantal databases mogelijk niet mogelijk om u te doen efficiënt zelfs met alle beschikbare hulpprogramma's en rapporten die Azure SQL Database en de Azure-portal bieden. In plaats van controleren en de database handmatig afstemmen, kunt u enkele van de acties controleren en afstemmen met Azure SQL Database met behulp van de functie voor automatisch afstemmen delegeren. 


> [!VIDEO https://channel9.msdn.com/Blogs/Azure-in-the-Enterprise/Enabling-Azure-SQL-Database-Auto-Tuning-at-Scale-for-Microsoft-IT/player]
>

## <a name="how-does-automatic-tuning-work"></a>Hoe werkt automatische afstemmen?

Azure SQL-Database heeft een continue prestaties en -analyse proces dat voortdurend gegevens verzamelt over de kenmerken van uw werkbelasting en identificeren van mogelijke problemen en verbeteringen.

![Automatische afstemmen-proces](./media/sql-database-automatic-tuning/tuning-process.png)

Dit proces kunnen Azure SQL Database dynamisch aanpassen aan uw werkbelasting door te zoeken welke indexen en planningen mogelijk voor betere prestaties van uw werkbelastingen en welke indexen van invloed op uw werkbelastingen. Op basis van deze resultaten, maatregelen automatische afstemming afstemmen ter verbetering van de prestaties van uw workload. Bovendien voortdurend Azure SQL Database prestaties na elke wijziging door automatische afstemming om ervoor te zorgen dat het verbetert de prestaties van uw workload. Een actie op die u hebt niet de prestaties verbeteren, wordt automatisch hersteld. Dit verificatieproces is een belangrijke functie die ervoor zorgt dat elke wijziging door automatische afstemming niet is van de prestaties van uw workload verkleinen.

Er zijn twee automatische afstemmen aspecten die beschikbaar in Azure SQL Database zijn:

 -  **Automatische indexbeheer** die identificeert indexen die moeten worden toegevoegd in de database en indexen die moeten worden verwijderd.
 -  **Automatische plan correctie** (binnenkort beschikbaar, al beschikbaar in SQL Server 2017) die problematisch plannen identificeert en correcties SQL plan prestatieproblemen.

## <a name="automatic-index-management"></a>Automatische indexbeheer

Beheer van de index is in Azure SQL Database eenvoudig omdat Azure SQL Database gegevens over uw werkbelasting verzamelt en zorgt ervoor dat uw gegevens altijd optimaal is geïndexeerd. Ontwerp voor de juiste index is van cruciaal belang voor optimale prestaties van uw werkbelasting en beheer van de automatische index kunt u de indexen optimaliseren. Automatische indexbeheer kunt prestatieproblemen oplossen in onjuist geïndexeerde databases of onderhouden en verbeteren van indexen voor het schema van de bestaande database. 

### <a name="why-do-you-need-index-management"></a>Waarom moet u beheer van de index?

Indexen te versnellen enkele van uw query's die gegevens uit de tabellen lezen. ze kunnen echter de query's die gegevens bijwerken vertragen. U moet zorgvuldig analyseren wanneer een index te maken en welke kolommen u wilt opnemen in de index. Sommige indexen mogelijk niet na enige tijd nodig. Daarom moet u regelmatig identificeren en verwijder de indexen die niet in de voordelen weergegeven worden. Als u de ongebruikte indexen negeert, zouden de prestaties van de query's die gegevens bijwerken zonder geen voordeel op de query's die gegevens lezen worden verlaagd. Ongebruikte indexen ook van invloed op prestaties van het systeem omdat aanvullende updates onnodige logboekregistratie vereisen.

Zoeken naar de optimale reeks indexen ter verbetering van de prestaties van de query's die gegevens lezen uit de tabellen en minimale invloed hebben op updates mogelijk continue en complexe analyse.

Azure SQL Database maakt gebruik van ingebouwde intelligentie en geavanceerde regels die het analyseren van uw query's, het identificeren van indexen die optimaal is voor de werkbelasting van uw huidige en de indexen mogelijk verwijderd. Azure SQL Database zorgt ervoor dat u hebt een minimaal benodigde aantal indexen die de query's die lezen van gegevens, met de geminimaliseerd gevolgen voor de andere query's optimaliseren.

### <a name="how-to-identify-indexes-that-need-to-be-changed-in-your-database"></a>Het identificeren van indexen die moeten worden gewijzigd in de database?

Azure SQL Database kunt gemakkelijk beheerproces van de index. In plaats van de klus zijn van een handmatige werkbelasting analyse en bewaking van de index, Azure SQL Database analyseert uw werkbelasting identificeert de query's die snel kunnen worden uitgevoerd met een nieuwe index en niet-gebruikte of dubbele indexen identificeert. Meer informatie over de identificatie van de indexen die moeten worden gewijzigd op [indexaanbevelingen vinden in Azure portal](sql-database-advisor-portal.md).

### <a name="automatic-index-management-considerations"></a>Automatische index beheeroverwegingen

Als u merkt dat de ingebouwde regels de prestaties van uw database verbeteren, kunt u mogelijk uw indexen automatisch beheren van Azure SQL-database.

Acties die zijn vereist voor het maken van de benodigde indexen in Azure SQL-Databases mogelijk gebruik van bronnen en ondersteuningsbeheerder invloed hebben op prestaties van de werkbelasting. Om te beperken van de impact van de index is gemaakt op de prestaties van de werkbelasting, zoekt Azure SQL Database het juiste tijdvenster voor een bewerking voor het beheer van een index. Actie afstemmen is uitgesteld als de database bronnen moet voor het uitvoeren van uw workload en gestart wanneer de database voldoende heeft ongebruikte bronnen die kunnen worden gebruikt voor de onderhoudstaak. Een belangrijk onderdeel in automatische indexbeheer is een verificatie van de acties. Wanneer Azure SQL Database maakt of index zakt, analyseert een controleproces prestaties van uw werkbelasting om te controleren dat de actie die de prestaties verbeterd. Als dit niet aanzienlijke verbetering – opleveren wordt de actie onmiddellijk ongedaan gemaakt. Op deze manier voor Azure SQL Database zorgt ervoor dat automatische acties dit geen negatieve invloed prestaties van uw workload. Indexen die zijn gemaakt door automatische afstemming NLB is zichtbaar voor de onderhoudsbewerking op het onderliggende schema. Wijzigingen in het schema zoals verwijderen of hernoemen van kolommen worden niet geblokkeerd door de aanwezigheid van automatisch gemaakte indexen. Indexen die automatisch worden gemaakt met Azure SQL Database worden onmiddellijk verwijderd wanneer gerelateerde tabel- of -kolommen wordt verwijderd.

## <a name="automatic-plan-choice-correction"></a>Automatische plan keuze correctie

Correctie van automatische planning is een nieuwe automatische afstemmen functie toegevoegd in SQL Server 2017 CTP2.0 waarmee SQL-schema's die zijn vastgelopen. Deze optie voor automatisch afstemmen is binnenkort beschikbaar in Azure SQL-Database. Meer informatie op [automatische afstemming in SQL Server 2017](https://docs.microsoft.com/sql/relational-databases/automatic-tuning/automatic-tuning).

## <a name="next-steps"></a>Volgende stappen

- Als u wilt inschakelen automatische afstemming in Azure SQL Database en laat functie voor automatisch afstemmen uw werkbelasting volledig te beheren, Zie [inschakelen automatische afstemming](sql-database-automatic-tuning-enable.md).
- Als u wilt gebruiken voor handmatige afstemmen, kunt u bekijken [afstemmen aanbevelingen in Azure-portal](sql-database-advisor-portal.md) en de waarden die de prestaties van uw query's verbeteren handmatig toepassen.
