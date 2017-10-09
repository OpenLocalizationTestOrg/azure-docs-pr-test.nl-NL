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
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a><span data-ttu-id="b4953-103">Oplossen van prestatieproblemen en de database te optimaliseren</span><span class="sxs-lookup"><span data-stu-id="b4953-103">Troubleshoot performance issues and optimize your database</span></span>

<span data-ttu-id="b4953-104">Ontbrekende indexen en onvoldoende geoptimaliseerde query's zijn veelvoorkomende redenen voor slechte databaseprestaties.</span><span class="sxs-lookup"><span data-stu-id="b4953-104">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="b4953-105">In deze zelfstudie leert u naar:</span><span class="sxs-lookup"><span data-stu-id="b4953-105">In this tutorial you learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="b4953-106">Bekijk, toepassing en aanbevelingen voor verbetering van prestaties te herstellen</span><span class="sxs-lookup"><span data-stu-id="b4953-106">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="b4953-107">Query's met hoge Resourcegebruik vinden</span><span class="sxs-lookup"><span data-stu-id="b4953-107">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="b4953-108">Langdurige query 's</span><span class="sxs-lookup"><span data-stu-id="b4953-108">Find long running queries</span></span>

> <span data-ttu-id="b4953-109">U moet een continue workload op een database met prestatieproblemen: een index bijvoorbeeld tooreceive een aanbeveling ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="b4953-109">You need a continuous workload on a database with performance issues – missing an index for example tooreceive a recommendation.</span></span>
>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="b4953-110">Meld u bij toohello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="b4953-110">Log in toohello Azure portal</span></span>

<span data-ttu-id="b4953-111">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b4953-111">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="review-and-apply-a-recommendation"></a><span data-ttu-id="b4953-112">Bekijken en toepassen van een aanbeveling</span><span class="sxs-lookup"><span data-stu-id="b4953-112">Review and apply a recommendation</span></span>

<span data-ttu-id="b4953-113">Volg deze stappen tooapply een aanbeveling van Hallo-systeem voor uw database:</span><span class="sxs-lookup"><span data-stu-id="b4953-113">Follow these steps tooapply a recommendation from hello system for your database:</span></span>

1. <span data-ttu-id="b4953-114">Klik op Hallo **prestaties aanbevelingen** menu in de blade Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="b4953-114">Click hello **Performance recommendations** menu in hello database blade.</span></span>

    ![prestaties aanbeveling](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. <span data-ttu-id="b4953-116">Selecteer een actieve aanbeveling in Hallo lijst met aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="b4953-116">From hello list of recommendations, select an active recommendation.</span></span> <span data-ttu-id="b4953-117">In dit voorbeeld wordt een Index maken.</span><span class="sxs-lookup"><span data-stu-id="b4953-117">In this example, Create Index.</span></span>

    ![Selecteer de aanbeveling](./media/sql-database-performance-tutorial/create_index.png)

3. <span data-ttu-id="b4953-119">Hallo aanbeveling toepassen door te klikken op Hallo **toepassen** knop.</span><span class="sxs-lookup"><span data-stu-id="b4953-119">Apply hello recommendation by clicking hello **Apply** button.</span></span> <span data-ttu-id="b4953-120">Desgewenst Hallo aanbeveling gedetailleerde gegevens bekijken en Zie Hallo T-SQL-script te worden uitgevoerd door te klikken op **Script weergeven** knop.</span><span class="sxs-lookup"><span data-stu-id="b4953-120">Optionally, review hello recommendation details and see hello T-SQL script too be executed by clicking on **View Script** button.</span></span>

    ![Aanbeveling toepassen](./media/sql-database-performance-tutorial/apply.png)

4. <span data-ttu-id="b4953-122">[Optioneel] Schakel automatische afstemming voor aanbevelingen toobe automatisch toegepast.</span><span class="sxs-lookup"><span data-stu-id="b4953-122">[Optional] Enable automatic tuning for recommendations toobe applied automatically.</span></span>

    ![Automatische afstemming](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a><span data-ttu-id="b4953-124">Een aanbeveling te herstellen</span><span class="sxs-lookup"><span data-stu-id="b4953-124">Revert a recommendation</span></span>

<span data-ttu-id="b4953-125">Hallo Database Advisor bewaakt elke aanbeveling geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b4953-125">hello Database Advisor monitors every recommendation implemented.</span></span> <span data-ttu-id="b4953-126">Als een aanbeveling niet Hallo werkbelasting verbetert, automatisch worden teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="b4953-126">If a recommendation doesn't improve hello workload it will be automatically reverted.</span></span> <span data-ttu-id="b4953-127">Handmatig een aanbeveling terugzetten is mogelijk, maar in de meeste gevallen niet nodig is.</span><span class="sxs-lookup"><span data-stu-id="b4953-127">Manually reverting a recommendation is possible, but not necessary in most cases.</span></span> <span data-ttu-id="b4953-128">een aanbeveling toorevert:</span><span class="sxs-lookup"><span data-stu-id="b4953-128">toorevert a recommendation:</span></span>

1. <span data-ttu-id="b4953-129">Ga toohello prestaties aanbevelingen menu en selecteer een van de aanbevelingen Hallo toegepast.</span><span class="sxs-lookup"><span data-stu-id="b4953-129">Go toohello performance recommendations menu and select one of hello applied recommendations.</span></span>

    ![Selecteer de aanbeveling](./media/sql-database-performance-tutorial/select.png)

2. <span data-ttu-id="b4953-131">Klik in de detailweergave Hallo **Revert**.</span><span class="sxs-lookup"><span data-stu-id="b4953-131">In hello details view, click **Revert**.</span></span>

    ![aanbeveling te herstellen](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a><span data-ttu-id="b4953-133">Hallo-query die Hallo verbruikt vinden de meeste bronnen</span><span class="sxs-lookup"><span data-stu-id="b4953-133">Find hello query that consumes hello most resources</span></span>

<span data-ttu-id="b4953-134">Volg deze stappen toofind Hallo query verbruikt Hallo zoveel mogelijk bronnen:</span><span class="sxs-lookup"><span data-stu-id="b4953-134">Follow these steps toofind hello query consuming hello most resources:</span></span>

1. <span data-ttu-id="b4953-135">Klik op Hallo **Query Performance Insight** menu in de blade Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="b4953-135">Click on hello **Query Performance Insight** menu in hello database blade.</span></span>

    ![query insights](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. <span data-ttu-id="b4953-137">Selecteer een resourcetype.</span><span class="sxs-lookup"><span data-stu-id="b4953-137">Select a resource type.</span></span>

    ![query insights](./media/sql-database-performance-tutorial/select_resource_type.png)

3. <span data-ttu-id="b4953-139">Selecteer de eerste query Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="b4953-139">Select hello first query in hello table.</span></span>

    ![query insights](./media/sql-database-performance-tutorial/select_query.png)

4. <span data-ttu-id="b4953-141">Bekijk de details van de Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="b4953-141">Review hello query details.</span></span>

    ![query insights](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a><span data-ttu-id="b4953-143">Hallo langste actieve query vinden</span><span class="sxs-lookup"><span data-stu-id="b4953-143">Find hello longest running query</span></span>

1. <span data-ttu-id="b4953-144">Ga tooQuery Performance Insight en selecteer Hallo **langlopende query's** tabblad.</span><span class="sxs-lookup"><span data-stu-id="b4953-144">Go tooQuery Performance Insight and select hello **Long running queries** tab.</span></span>

    ![query insights](./media/sql-database-performance-tutorial/long_running.png)

3. <span data-ttu-id="b4953-146">Selecteer de eerste query Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="b4953-146">Select hello first query in hello table.</span></span>

    ![query insights](./media/sql-database-performance-tutorial/select_first_query.png)

4. <span data-ttu-id="b4953-148">Bekijk de details van de Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="b4953-148">Review hello query details.</span></span>

    ![query insights](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a><span data-ttu-id="b4953-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b4953-150">Next steps</span></span> 
<span data-ttu-id="b4953-151">Ontbrekende indexen en onvoldoende geoptimaliseerde query's zijn veelvoorkomende redenen voor slechte databaseprestaties.</span><span class="sxs-lookup"><span data-stu-id="b4953-151">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="b4953-152">In deze zelfstudie hebt u geleerd:</span><span class="sxs-lookup"><span data-stu-id="b4953-152">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="b4953-153">Bekijk, toepassing en aanbevelingen voor verbetering van prestaties te herstellen</span><span class="sxs-lookup"><span data-stu-id="b4953-153">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="b4953-154">Query's met hoge Resourcegebruik vinden</span><span class="sxs-lookup"><span data-stu-id="b4953-154">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="b4953-155">Langdurige query 's</span><span class="sxs-lookup"><span data-stu-id="b4953-155">Find long running queries</span></span>

[<span data-ttu-id="b4953-156">SQL Database-tips voor betere prestaties afstemmen</span><span class="sxs-lookup"><span data-stu-id="b4953-156">SQL Database performance tuning tips</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
