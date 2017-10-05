---
title: Prestaties aanbevelingen - Azure SQL Database | Microsoft Docs
description: De Azure SQL-Database bevat aanbevelingen voor de SQL-Databases die u kunt de huidige queryprestaties verbeteren.
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: 1db441ff-58f5-45da-8d38-b54dc2aa6145
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 357a25a665894c86ddb0f93beeb4dd59d8837489
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="performance-recommendations"></a>Aanbevelingen voor prestaties

Azure SQL Database leert en aanpast aan uw toepassing en bevat aangepaste aanbevelingen zodat u voor de prestaties van uw SQL-databases. Prestaties van uw wordt continu beoordeeld door het analyseren van uw gebruiksgeschiedenis SQL-Database. De aanbevelingen die worden verstrekt zijn gebaseerd op een patroon van de unieke werkbelasting database en de prestaties te verbeteren.

> [!NOTE]
> Het is raadzaam van het gebruik van aanbevelingen doordat automatische afstemming van uw database. Zie voor meer informatie [automatische afstemming](sql-database-automatic-tuning.md).
>

## <a name="create-index-recommendations"></a>Indexaanbevelingen maken
Azure SQL Database continu bewaakt de query's wordt uitgevoerd en identificeert de indexen die de prestaties kunnen verbeteren. Als voldoende vertrouwen is gebouwd die een bepaalde index ontbreekt, zal een nieuwe **Create index** aanbeveling wordt gemaakt. Azure SQL Database bouwt vertrouwen door het schatten van de index via tijd brengen wilt prestatieverbetering te bereiken. Afhankelijk van de geschatte prestatieverbetering te bereiken, aanbevelingen gecategoriseerd als hoog, Gemiddeld of laag. 

Indexen die zijn gemaakt met behulp van de aanbevelingen zijn altijd gemarkeerd als auto_created indexen. U kunt zien welke indexen zijn auto_created door te kijken sys.indexes weergeven. Automatisch gemaakt indexen blokkeren niet ALTER/RENAME-opdrachten. Als u probeert te verwijderen van de kolom met een index worden gemaakt van het automatisch, de opdracht is geslaagd en de automatische index gemaakt met de opdracht ook is verwijderd. Gewone indexen zou de opdracht ALTER/RENAME op kolommen die zijn geïndexeerd blokkeren.

Zodra de indexaanbeveling maken wordt toegepast, wordt in Azure SQL Database prestaties van de query's met de basislijn vergelijken. Als u nieuwe index gebracht verbeteringen in de prestaties, aanbeveling gemarkeerd als geslaagd en impact rapport beschikbaar. Als de index niet doen om de voordelen, worden deze automatisch hersteld. Op deze manier Azure SQL Database zorgt ervoor dat met behulp van aanbevelingen alleen de prestaties van de database verbeteren wordt.

Alle **Create index** aanbeveling heeft een vorige uit beleid dat wordt toegestaan als de database of een groep DTU-gebruik hoger dan 80% in de afgelopen 20 minuten of is als de opslag dan 90% van het gebruik van is de aanbeveling zijn toegepast. In dit geval wordt de aanbeveling worden uitgesteld.

## <a name="drop-index-recommendations"></a>Aanbevelingen voor indexen verwijderen
Naast het herkennen van een ontbrekende index in Azure SQL Database voortdurend de prestaties van de bestaande indexen analyseert. Als de index wordt niet gebruikt, wordt Azure SQL Database het beste neer te zetten. Verwijderen van een index wordt in beide gevallen aangeraden:
* Index is een duplicaat van een andere index (dezelfde geïndexeerd en kolom, partitie-schema en filters opgenomen)
* Index wordt niet gebruikt voor een langere periode (93 dagen)

Aanbevelingen voor indexen verwijderen worden ook de controle na implementatie doorlopen. Het rapport gevolgen zijn beschikbaar als de prestaties worden verbeterd. Als de prestaties zijn afgenomen, wordt er aanbeveling hersteld.


## <a name="parameterize-queries-recommendations"></a>Aanbevelingen voor query's voorzien
**Query's voorzien** aanbevelingen worden weergegeven wanneer u een of meer query's die zijn voortdurend wordt gecompileerd maar end hebt met hetzelfde abonnement voor de query kan worden uitgevoerd. Deze voorwaarde Hiermee opent u de gelegenheid om toe te passen geforceerde parameterisering, waardoor queryplannen worden in de cache opgeslagen en opnieuw worden gebruikt in de toekomstige verbeterde prestaties en Resourcegebruik verminderen. 

Elke query uitgegeven voor de SQL Server in eerste instantie moet worden gecompileerd voor het genereren van een plan kan worden uitgevoerd. Elk gegenereerde plan wordt toegevoegd aan de plancache en een volgende uitvoering van dezelfde query opnieuw kunnen gebruiken voor dit abonnement uit de cache, hoeft u de aanvullende compilatie. 

Toepassingen die verzenden van query's die niet-geparametriseerde waarden bevatten, kunnen leiden tot een prestatieoverhead waarin voor elke dergelijke query met andere parameterwaarden het uitvoeringsplan wordt gecompileerd opnieuw. In veel gevallen de dezelfde query's met verschillende parameter waarden genereren de dezelfde uitvoering plannen, maar deze plannen nog steeds afzonderlijk worden toegevoegd aan de plancache. Compileren uitvoering plannen database bronnen gebruiken, duur van de query verhogen en de plancache plannen om te worden verwijderd uit de cache veroorzaakt overloop. Dit gedrag van SQL Server kan worden gewijzigd door de optie geforceerde parameterisering op de database. 

Als u de gevolgen van deze aanbeveling schatten, kunt worden u geleverd bij een vergelijking tussen de werkelijke CPU-gebruik en het verwachte CPU-gebruik (alsof de aanbeveling is toegepast). Naast van CPU-gebruik, verlaagt u hiermee de duur van de query voor de tijd doorgebracht in de compilatie. Er worden ook veel minder overhead op plancache, zodat de meerderheid van de abonnementen in de cache blijft en opnieuw worden gebruikt. U kunt deze aanbeveling toepassen snel en eenvoudig door te klikken op de **toepassen** opdracht. 

Als u deze aanbeveling uitvoert, geforceerde parameterisering binnen enkele minuten in de database wordt het ingeschakeld en wordt het bewakingsproces die het duurt ongeveer 24 uur. Na deze periode, kunt u zich kunt zien van het validatierapport voor CPU-gebruik van de database waarin de 24 uur voordat en nadat de aanbeveling is toegepast. SQL Database Advisor is een beveiligingsmechanisme dat de toegepaste aanbeveling automatisch teruggezet als de regressie van een prestaties is gedetecteerd.

## <a name="fix-schema-issues-recommendations"></a>Aanbevelingen voor schema-problemen oplossen
**Los de problemen schema** aanbevelingen worden weergegeven wanneer de service SQL Database meldingen een afwijkingsdetectie in het aantal schema-gerelateerde SQL fouten op uw Azure SQL Database plaatsvinden. Deze aanbeveling wordt doorgaans weergegeven wanneer de database meerdere fouten over schema (ongeldige kolomnaam, Ongeldige objectnaam, enzovoort) binnen een uur optreedt.

'Problemen met het schema' vormen een klasse syntaxisfouten in SQL Server die ontstaan wanneer de definitie van de SQL-query en de definitie van schema van de database zijn niet uitgelijnd. Bijvoorbeeld, een van de kolommen die werd verwacht door de query ontbreekt mogelijk in de doeltabel of vice versa. 

Aanbeveling 'Schema probleem op te lossen' wordt weergegeven wanneer Azure SQL Database-service een afwijkingsdetectie in het aantal schema-gerelateerde SQL fouten op uw Azure SQL Database plaatsvinden meldingen. De volgende tabel ziet u de fouten die betrekking op schema problemen hebben:

| SQL-foutcode | Bericht |
| --- | --- |
| 201 |Procedure of functie '*'verwacht dat de parameter'*', die niet is opgegeven. |
| 207 |Ongeldige kolomnaam ' *'. |
| 208 |Ongeldige objectnaam ' *'. |
| 213 |Kolomnaam of -nummer van opgegeven waarden komt niet overeen met tabeldefinitie. |
| 2812 |Kan de opgeslagen procedure niet vinden ' *'. |
| 8144 |Procedure of functie * heeft te veel argumenten opgegeven. |

## <a name="next-steps"></a>Volgende stappen
Bewaken van uw aanbevelingen en blijven toepassen om de prestaties te verfijnen. Database-werkbelastingen zijn dynamisch en continu wijzigen. SQL-Database advisor blijft om te controleren en aanbevelingen die potentieel prestaties van uw database kunt verbeteren. 

* Zie [prestaties aanbevelingen in de Azure portal](sql-database-advisor-portal.md) voor stapsgewijze instructies voor het gebruik van prestaties aanbevelingen in de Azure-portal.
* Zie [inzichten voor queryprestaties](sql-database-query-performance.md) leren kennen en de invloed op de prestaties van uw eerste query's weergeven.

## <a name="additional-resources"></a>Aanvullende bronnen
* [Query Store](https://msdn.microsoft.com/library/dn817826.aspx)
* [INDEX MAKEN](https://msdn.microsoft.com/library/ms188783.aspx)
* [Toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-what-is.md)

