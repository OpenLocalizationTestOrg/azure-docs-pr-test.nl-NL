---
title: aaaTroubleshoot prestaties problemen en de database te optimaliseren | Microsoft Docs
description: Prestaties aanbevelingen tooyour SQL-Database, evenals wissen hoe toogain insights over de prestaties van Hallo query's uitvoeren in uw database Hallo toepassen
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a>Oplossen van prestatieproblemen en de database te optimaliseren

Ontbrekende indexen en onvoldoende geoptimaliseerde query's zijn veelvoorkomende redenen voor slechte databaseprestaties. In deze zelfstudie leert u naar:
> [!div class="checklist"]
> * Bekijk, toepassing en aanbevelingen voor verbetering van prestaties te herstellen
> * Query's met hoge Resourcegebruik vinden
> * Langdurige query 's

> U moet een continue workload op een database met prestatieproblemen: een index bijvoorbeeld tooreceive een aanbeveling ontbreekt.
>

## <a name="log-in-toohello-azure-portal"></a>Meld u bij toohello Azure-portal

Meld u bij toohello [Azure-portal](https://portal.azure.com/).

## <a name="review-and-apply-a-recommendation"></a>Bekijken en toepassen van een aanbeveling

Volg deze stappen tooapply een aanbeveling van Hallo-systeem voor uw database:

1. Klik op Hallo **prestaties aanbevelingen** menu in de blade Hallo-database.

    ![prestaties aanbeveling](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. Selecteer een actieve aanbeveling in Hallo lijst met aanbevelingen. In dit voorbeeld wordt een Index maken.

    ![Selecteer de aanbeveling](./media/sql-database-performance-tutorial/create_index.png)

3. Hallo aanbeveling toepassen door te klikken op Hallo **toepassen** knop. Desgewenst Hallo aanbeveling gedetailleerde gegevens bekijken en Zie Hallo T-SQL-script te worden uitgevoerd door te klikken op **Script weergeven** knop.

    ![Aanbeveling toepassen](./media/sql-database-performance-tutorial/apply.png)

4. [Optioneel] Schakel automatische afstemming voor aanbevelingen toobe automatisch toegepast.

    ![Automatische afstemming](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a>Een aanbeveling te herstellen

Hallo Database Advisor bewaakt elke aanbeveling geïmplementeerd. Als een aanbeveling niet Hallo werkbelasting verbetert, automatisch worden teruggedraaid. Handmatig een aanbeveling terugzetten is mogelijk, maar in de meeste gevallen niet nodig is. een aanbeveling toorevert:

1. Ga toohello prestaties aanbevelingen menu en selecteer een van de aanbevelingen Hallo toegepast.

    ![Selecteer de aanbeveling](./media/sql-database-performance-tutorial/select.png)

2. Klik in de detailweergave Hallo **Revert**.

    ![aanbeveling te herstellen](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a>Hallo-query die Hallo verbruikt vinden de meeste bronnen

Volg deze stappen toofind Hallo query verbruikt Hallo zoveel mogelijk bronnen:

1. Klik op Hallo **Query Performance Insight** menu in de blade Hallo-database.

    ![query insights](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. Selecteer een resourcetype.

    ![query insights](./media/sql-database-performance-tutorial/select_resource_type.png)

3. Selecteer de eerste query Hallo in Hallo tabel.

    ![query insights](./media/sql-database-performance-tutorial/select_query.png)

4. Bekijk de details van de Hallo-query.

    ![query insights](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a>Hallo langste actieve query vinden

1. Ga tooQuery Performance Insight en selecteer Hallo **langlopende query's** tabblad.

    ![query insights](./media/sql-database-performance-tutorial/long_running.png)

3. Selecteer de eerste query Hallo in Hallo tabel.

    ![query insights](./media/sql-database-performance-tutorial/select_first_query.png)

4. Bekijk de details van de Hallo-query.

    ![query insights](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a>Volgende stappen 
Ontbrekende indexen en onvoldoende geoptimaliseerde query's zijn veelvoorkomende redenen voor slechte databaseprestaties. In deze zelfstudie hebt u geleerd:
> [!div class="checklist"]
> * Bekijk, toepassing en aanbevelingen voor verbetering van prestaties te herstellen
> * Query's met hoge Resourcegebruik vinden
> * Langdurige query 's

[SQL Database-tips voor betere prestaties afstemmen](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
