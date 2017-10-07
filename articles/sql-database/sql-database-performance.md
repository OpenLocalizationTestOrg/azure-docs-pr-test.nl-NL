---
title: aaaMonitor en verbeterde prestaties - Azure SQL Database | Microsoft Docs
description: Hello die Azure SQL Database prestaties biedt van hulpprogramma's voor toohelp u identificeren gebieden die u kunnen de huidige queryprestaties verbeteren.
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 84b8a1bc62698a29deb49e765f208bd7e14d0870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-improve-performance"></a>Prestaties bewaken en verbeteren
Azure SQL Database identificeert potentiële problemen in uw database en raadt aan om de acties die de prestaties van uw werkbelasting verbeteren kunnen door intelligent afstemmen acties en aanbevelingen.

tooreview uw databaseprestaties, gebruik Hallo **prestaties** tegel op de pagina overzicht Hallo of omlaag te gaan 'Ondersteuning + probleemoplossing' sectie:

   ![Weergaveprestaties](./media/sql-database-performance/entries.png)

In de sectie Hallo 'Ondersteuning + probleemoplossing', kunt u Hallo pagina's te volgen:


1. [Prestatieoverzicht van de](#performance-overview) toomonitor prestaties van uw database. 
2. [Prestaties aanbevelingen](#performance-recommendations) toofind prestaties aanbevelingen op grond van de prestaties van uw werkbelasting kunnen verbeteren.
3. [Query Performance Insight](#query-performance-insight) toofind bovenste resource verbruikt query's.
4. [Automatische afstemming](#automatic-tuning) toolet Azure SQL Database automatisch de database te optimaliseren.

## <a name="performance-overview"></a>Prestatieoverzicht van de
Deze weergave bevat een samenvatting van de databaseprestaties van uw en helpt u bij de prestaties afstemmen en probleemoplossing. 

![Prestaties](./media/sql-database-performance/performance.png)

* Hallo **aanbevelingen** tegel bevat een verdeling van aanbevelingen voor uw database afstemmen (drie belangrijkste aanbevelingen worden weergegeven als er meer zijn). Deze tegel te klikken gaat u verder te**[prestaties aanbevelingen](#performance-recommendations)**. 
* Hallo **afstemmen activiteit** tegel bevat een samenvatting van Hallo voltooide acties voor uw database afstemmen, zodat u snel inzicht in Hallo geschiedenis van het afstemmen van de activiteit. Deze tegel te klikken, gaat u toohello volledige afstemmen geschiedenisweergave voor uw database.
* Hallo **automatische afstemming** tegel ziet Hallo [automatische afstemming configuratie](sql-database-automatic-tuning-enable.md) voor uw database (tuning opties die automatisch toegepaste tooyour database zijn). Hallo automation configuratiedialoogvenster te klikken op deze tegel worden geopend.
* Hallo **databasequery's** tegel bevat Hallo van Hallo queryprestaties voor uw database (algehele DTU-gebruik en de bovenkant resource verbruikt query's). Deze tegel te klikken gaat u verder te**[Query Performance Insight](#query-performance-insight)**.

## <a name="performance-recommendations"></a>Aanbevelingen voor prestaties
Deze pagina bevat intelligent [afstemmen aanbevelingen](sql-database-advisor.md) die de prestaties van uw database kunt verbeteren. Hallo volgende typen aanbevelingen worden weergegeven op deze pagina:

* Aanbevelingen op welke indexen toocreate of drop.
* Aanbevelingen wanneer schema problemen zijn geïdentificeerd in Hallo-database.
* Aanbevelingen wanneer query's van query's profiteren kunnen.

![Prestaties](./media/sql-database-performance/recommendations.png)

U kunt ook volledige geschiedenis van het afstemmen van de acties die zijn toegepast in de afgelopen Hallo vinden.

Meer informatie over hoe een apply toofind prestaties aanbevelingen in [zoeken en toepassen van aanbevelingen voor prestaties](sql-database-advisor-portal.md) artikel.

## <a name="automatic-tuning"></a>Automatisch instellen
Azure SQL-Databases kunt automatisch afstemmen van de databaseprestaties door toe te passen [prestaties aanbevelingen](sql-database-advisor.md). toolearn meer lezen [automatische afstemmen artikel](sql-database-automatic-tuning.md). tooenable, lezen [hoe tooenable automatische afstemming](sql-database-automatic-tuning-enable.md).

## <a name="query-performance-insight"></a>Inzicht in queryprestaties
[Query Performance Insight](sql-database-query-performance.md) kunt u toospend minder tijd databaseprestaties oplossen door op te geven:

* Dieper inzicht in uw databases brongebruik (DTU). 
* Hallo bovenste CPU verbruikt query's mogelijk voor verbeterde prestaties kunnen worden afgestemd. 
* Hallo mogelijkheid toodrill omlaag in de details op Hallo van een query. 

  ![Prestatiedashboard](./media/sql-database-query-performance/performance.png)

Meer informatie over deze pagina niet vinden in Hallo artikel  **[hoe toouse Query Performance Insight](sql-database-query-performance.md)**.

## <a name="additional-resources"></a>Aanvullende bronnen
* [Azure SQL Database-prestaties richtlijnen voor individuele databases](sql-database-performance-guidance.md)
* [Wanneer een elastische groep moet worden gebruikt?](sql-database-elastic-pool-guidance.md)

