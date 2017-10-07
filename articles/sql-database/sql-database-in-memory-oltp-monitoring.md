---
title: aaaMonitor XTP in het geheugen opslag | Microsoft Docs
description: Schatting en monitor XTP geheugenopslag gebruiken, capaciteit; capaciteit fout 41823 oplossen
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a>OLTP-opslag in het geheugen controleren
Wanneer u [In het geheugen OLTP](sql-database-in-memory.md), gegevens in tabellen geoptimaliseerd voor geheugen en tabelvariabelen bevindt zich in In het geheugen OLTP-opslag. Elke servicelaag Premium heeft een maximale In het geheugen OLTP opslaggrootte, die wordt beschreven in Hallo [SQL Database servicecategorieën artikel](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels). Wanneer deze limiet wordt overschreden, invoegen en bijwerken bewerkingen mogelijk mislukken (met de fout 41823). Op dat moment wordt u tooeither verwijderen gegevens tooreclaim geheugen nodig hebben of upgrade van de prestatielaag Hallo van uw database.

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a>Bepalen of gegevens binnen het Hallo-geheugenopslag cap past
Hallo opslag cap bepalen: Raadpleeg Hallo [SQL Database servicecategorieën artikel](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) voor Hallo opslag caps van Hallo verschillende Premium-Servicelagen.

Het schatten van de vereisten voor een tabel geoptimaliseerd voor geheugen werkt Hallo dezelfde geheugen komt manier voor SQL Server als het in Azure SQL Database. Een paar minuten tooreview dat onderwerp nemen op [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).

Houd er rekening mee dat Hallo tabel en variabele tabelrijen, evenals indexen, voor Hallo max gebruiker gegevensgrootte meetellen. ALTER TABLE moet bovendien voldoende ruimte toocreate een nieuwe versie van de gehele tabel Hallo en de indexen ervan.

## <a name="monitoring-and-alerting"></a>Bewaking en waarschuwingen
U kunt bewaken opslaggebruik in het geheugen als percentage van Hallo [cap opslag voor de prestatielaag](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in hello Azure [portal](https://portal.azure.com/): 

* Op de databaseblade Hallo, Ga naar Hallo Resource gebruik vak en klik op bewerken.
* Selecteer vervolgens de metriek Hallo `In-Memory OLTP Storage percentage`.
* tooadd een waarschuwing, klikt u op Hallo Resourcegebruik vak tooopen Hallo metrische blade en klik vervolgens op waarschuwing toevoegen.

Of gebruik Hallo query tooshow Hallo in het geheugen opslaggebruik te volgen:

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a>Juiste-geheugen situaties - fout 41823
-Geheugen resultaten uitgevoerd in invoegen, bijwerken en bewerkingen is mislukt met foutbericht 41823 maakt.

Foutbericht 41823 geeft aan dat Hallo geheugen geoptimaliseerde tabellen en tabelvariabelen Hallo maximale grootte overschreden.

tooresolve deze fout, hetzij:

* Gegevens verwijderen uit het Hallo geheugen geoptimaliseerde tabellen, mogelijk offloading Hallo gegevens tootraditional, schijfgebaseerde tabellen. of,
* Hallo service tier tooone upgraden met voldoende opslagruimte in het geheugen voor Hallo gegevens moet u tookeep in tabellen geoptimaliseerd voor geheugen.

## <a name="next-steps"></a>Volgende stappen
Zie voor richtlijnen bewaking, [bewaking Azure SQL Database met dynamische beheerweergaven](sql-database-monitoring-with-dmvs.md).
