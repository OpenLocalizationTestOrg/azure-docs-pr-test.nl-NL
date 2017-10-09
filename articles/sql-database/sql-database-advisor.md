---
title: aaaPerformance aanbevelingen - Azure SQL Database | Microsoft Docs
description: Hello Azure SQL Database bevat aanbevelingen voor de SQL-Databases die u kunt de huidige queryprestaties verbeteren.
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
ms.openlocfilehash: 77db338a0a395aec78c9e02849ae5ba4f2d01680
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-recommendations"></a>Aanbevelingen voor prestaties

Azure SQL Database leert en aanpast aan uw toepassing en aangepaste aanbevelingen zodat u toomaximize Hallo prestaties van uw SQL-databases. Prestaties van uw wordt continu beoordeeld door het analyseren van uw gebruiksgeschiedenis SQL-Database. Hallo aanbevelingen die beschikbaar zijn in een database unieke werkbelasting patroon zijn gebaseerd en de prestaties te verbeteren.

> [!NOTE]
> Het is raadzaam van het gebruik van aanbevelingen doordat automatische afstemming van uw database. Zie voor meer informatie [automatische afstemming](sql-database-automatic-tuning.md).
>

## <a name="create-index-recommendations"></a>Indexaanbevelingen maken
Azure SQL Database continu bewaakt Hallo query's wordt uitgevoerd en identificeert Hallo-indexen die Hallo prestaties kunnen verbeteren. Als voldoende vertrouwen is gebouwd die een bepaalde index ontbreekt, zal een nieuwe **Create index** aanbeveling wordt gemaakt. Azure SQL Database builds vertrouwen door het schatten van de prestaties beter Hallo index zou via tijd doen. Afhankelijk van Hallo geschatte prestatieverbetering te bereiken, aanbevelingen gecategoriseerd als hoog, Gemiddeld of laag. 

Indexen die zijn gemaakt met behulp van de aanbevelingen zijn altijd gemarkeerd als auto_created indexen. U kunt zien welke indexen zijn auto_created door te kijken sys.indexes weergeven. Automatisch gemaakt indexen blokkeren niet ALTER/RENAME-opdrachten. Als u toodrop Hallo kolom van een index worden gemaakt van het automatisch probeert, Hallo-opdracht is geslaagd en Hallo automatisch index gemaakt met Hallo opdracht ook is verwijderd. Gewone indexen blokkeren Hallo ALTER/Wijzig de naam van de opdracht bij de kolommen die zijn geïndexeerd.

Zodra Hallo maakt indexaanbeveling wordt toegepast, Azure SQL Database prestaties van query's Hallo met Hallo basislijnprestaties wordt vergeleken. Als een nieuwe index gebracht verbeteringen in de prestaties van hello, aanbeveling gemarkeerd als geslaagd en impact rapport beschikbaar. Als Hallo-index niet Hallo voordelen zetten, worden deze automatisch hersteld. Op deze manier Azure SQL Database zorgt ervoor dat met behulp van aanbevelingen worden alleen de Hallo databaseprestaties.

Alle **Create index** aanbeveling heeft een vorige uit beleid dat Hallo aanbeveling toepassen als Hallo database of een groep DTU-gebruik hoger dan 80% in laatste 20 minuten of is als Hallo opslag hoger dan 90% van het gebruik van is niet wordt toegestaan. Hallo-aanbeveling wordt in dit geval worden uitgesteld.

## <a name="drop-index-recommendations"></a>Aanbevelingen voor indexen verwijderen
Daarnaast analyseert toodetecting een ontbrekende index, Azure SQL Database continu Hallo prestaties van de bestaande indexen. Als de index wordt niet gebruikt, wordt Azure SQL Database het beste neer te zetten. Verwijderen van een index wordt in beide gevallen aangeraden:
* Index is een duplicaat van een andere index (dezelfde geïndexeerd en kolom, partitie-schema en filters opgenomen)
* Index wordt niet gebruikt voor een langere periode (93 dagen)

Aanbevelingen voor indexen verwijderen doorlopen ook Hallo controle na implementatie. Hallo impact rapport zijn beschikbaar als Hallo prestaties worden verbeterd. Als de prestaties zijn afgenomen, wordt er aanbeveling hersteld.


## <a name="parameterize-queries-recommendations"></a>Aanbevelingen voor query's voorzien
**Query's voorzien** aanbevelingen worden weergegeven wanneer er een of meer query's die zijn voortdurend wordt gecompileerd maar uiteindelijk Hallo uitvoeringsplan voor dezelfde query. Deze voorwaarde een kans tooapply parameterisering, waardoor queryplannen toobe in de cache opgeslagen en opnieuw gebruikt in toekomstige prestaties verbeteren en de beperking van Resourcegebruik Hallo gedwongen wordt geopend. 

Elke query uitgegeven voor de SQL Server in eerste instantie moet toobe gecompileerd toogenerate een plan kan worden uitgevoerd. Elk gegenereerde plan wordt toegevoegd toohello plancache en een volgende uitvoering Hallo dezelfde query opnieuw kunt gebruiken bij dit abonnement vanuit de cache hello, hoeft u Hallo aanvullende compilatie. 

Toepassingen die verzenden van query's die niet-geparametriseerde waarden bevatten, kunnen leiden prestatieoverhead tooa, waarbij elke dergelijke query met andere parameterwaarden Hallo uitvoeringsplan wordt gecompileerd opnieuw. In veel gevallen Hallo dezelfde query's met verschillende parameter waarden genereren Hallo dezelfde uitvoering plannen, maar deze plannen worden nog steeds afzonderlijk toohello plancache toegevoegd. Compileren uitvoering plannen database bronnen gebruiken, Hallo duur van de tijd en overloop Hallo queryplan cache veroorzaakt toobe verwijderd uit de cache Hallo-abonnementen te verhogen. Dit gedrag van SQL Server kan worden gewijzigd door in te stellen Hallo gedwongen parameterisering optie op Hallo-database. 

toohelp u schatten Hallo gevolgen van deze aanbeveling, u zijn opgegeven met een vergelijking tussen de werkelijke CPU Hallo gebruiks- en Hallo geprojecteerd CPU-gebruik (alsof Hallo aanbeveling werd toegepast). Bovendien tooCPU besparingen, de duur van uw query verlaagt voor Hallo-tijd besteed aan de compilatie. Er worden ook veel minder overhead op plancache, zodat de meerderheid van Hallo toostay in de cache-abonnementen en opnieuw worden gebruikt. U kunt deze aanbeveling toepassen snel en eenvoudig door te klikken op Hallo **toepassen** opdracht. 

Als u deze aanbeveling uitvoert, geforceerde parameterisering binnen enkele minuten in de database wordt het ingeschakeld en wordt het Hallo bewaking van proces ongeveer 24 uur duurt. U gaat na deze periode worden kunnen toosee Hallo validatierapport waarin CPU-gebruik van uw database 24 uur vóór en na Hallo aanbeveling is toegepast. SQL Database Advisor is een beveiligingsmechanisme dat Hallo toegepast aanbeveling automatisch teruggezet als de regressie van een prestaties is gedetecteerd.

## <a name="fix-schema-issues-recommendations"></a>Aanbevelingen voor schema-problemen oplossen
**Los de problemen schema** aanbevelingen worden weergegeven wanneer hello SQL Database-service een afwijkingsdetectie in Hallo aantal schema-gerelateerde SQL fouten op uw Azure SQL Database plaatsvinden meldingen. Deze aanbeveling wordt doorgaans weergegeven wanneer de database meerdere fouten over schema (ongeldige kolomnaam, Ongeldige objectnaam, enzovoort) binnen een uur optreedt.

'Problemen met het schema' vormen een klasse syntaxisfouten in SQL Server die gebeuren wanneer de definitie van de SQL-query Hallo Hallo en Hallo definitie van Hallo-databaseschema zijn niet uitgelijnd. Bijvoorbeeld, een Hallo kolommen werd verwacht door Hallo query ontbreekt mogelijk in de doeltabel Hallo of vice versa. 

Aanbeveling 'Schema probleem op te lossen' wordt weergegeven wanneer Azure SQL Database-service een afwijkingsdetectie in Hallo aantal schema-gerelateerde SQL fouten op uw Azure SQL Database plaatsvinden meldingen. Hallo volgende tabel toont Hallo fouten die gerelateerd tooschema problemen zijn:

| SQL-foutcode | Bericht |
| --- | --- |
| 201 |Procedure of functie '*'verwacht dat de parameter'*', die niet is opgegeven. |
| 207 |Ongeldige kolomnaam ' *'. |
| 208 |Ongeldige objectnaam ' *'. |
| 213 |Kolomnaam of -nummer van opgegeven waarden komt niet overeen met tabeldefinitie. |
| 2812 |Kan de opgeslagen procedure niet vinden ' *'. |
| 8144 |Procedure of functie * heeft te veel argumenten opgegeven. |

## <a name="next-steps"></a>Volgende stappen
Uw aanbevelingen controleren en doorgaan tooapply ze toorefine prestaties. Database-werkbelastingen zijn dynamisch en continu wijzigen. SQL-Database advisor toomonitor blijft en aanbevelingen die potentieel prestaties van uw database kunt verbeteren. 

* Zie [prestaties aanbevelingen in hello Azure-portal](sql-database-advisor-portal.md) voor stapsgewijze instructies voor hoe toouse prestaties aanbevelingen in hello Azure-portal.
* Zie [inzichten voor queryprestaties](sql-database-query-performance.md) toolearn over en bekijkt hello prestatie-invloed van de meest gebruikte query's.

## <a name="additional-resources"></a>Aanvullende bronnen
* [Query Store](https://msdn.microsoft.com/library/dn817826.aspx)
* [INDEX MAKEN](https://msdn.microsoft.com/library/ms188783.aspx)
* [Toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-what-is.md)

