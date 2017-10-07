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
# <a name="monitor-and-improve-performance"></a><span data-ttu-id="32240-103">Prestaties bewaken en verbeteren</span><span class="sxs-lookup"><span data-stu-id="32240-103">Monitor and improve performance</span></span>
<span data-ttu-id="32240-104">Azure SQL Database identificeert potentiële problemen in uw database en raadt aan om de acties die de prestaties van uw werkbelasting verbeteren kunnen door intelligent afstemmen acties en aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="32240-104">Azure SQL Database identifies potential problems in your database and recommends actions that can improve performance of your workload by providing intelligent tuning actions and recommendations.</span></span>

<span data-ttu-id="32240-105">tooreview uw databaseprestaties, gebruik Hallo **prestaties** tegel op de pagina overzicht Hallo of omlaag te gaan 'Ondersteuning + probleemoplossing' sectie:</span><span class="sxs-lookup"><span data-stu-id="32240-105">tooreview your database performance, use hello **Performance** tile on hello Overview page, or navigate down too"Support + troubleshooting" section:</span></span>

   ![Weergaveprestaties](./media/sql-database-performance/entries.png)

<span data-ttu-id="32240-107">In de sectie Hallo 'Ondersteuning + probleemoplossing', kunt u Hallo pagina's te volgen:</span><span class="sxs-lookup"><span data-stu-id="32240-107">In hello "Support + troubleshooting" section, you can use hello following pages:</span></span>


1. <span data-ttu-id="32240-108">[Prestatieoverzicht van de](#performance-overview) toomonitor prestaties van uw database.</span><span class="sxs-lookup"><span data-stu-id="32240-108">[Performance overview](#performance-overview) toomonitor performance of your database.</span></span> 
2. <span data-ttu-id="32240-109">[Prestaties aanbevelingen](#performance-recommendations) toofind prestaties aanbevelingen op grond van de prestaties van uw werkbelasting kunnen verbeteren.</span><span class="sxs-lookup"><span data-stu-id="32240-109">[Performance recommendations](#performance-recommendations) toofind performance recommendations that can improve performance of your workload.</span></span>
3. <span data-ttu-id="32240-110">[Query Performance Insight](#query-performance-insight) toofind bovenste resource verbruikt query's.</span><span class="sxs-lookup"><span data-stu-id="32240-110">[Query Performance Insight](#query-performance-insight) toofind top resource consuming queries.</span></span>
4. <span data-ttu-id="32240-111">[Automatische afstemming](#automatic-tuning) toolet Azure SQL Database automatisch de database te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="32240-111">[Automatic tuning](#automatic-tuning) toolet Azure SQL Database automatically optimize your database.</span></span>

## <a name="performance-overview"></a><span data-ttu-id="32240-112">Prestatieoverzicht van de</span><span class="sxs-lookup"><span data-stu-id="32240-112">Performance Overview</span></span>
<span data-ttu-id="32240-113">Deze weergave bevat een samenvatting van de databaseprestaties van uw en helpt u bij de prestaties afstemmen en probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="32240-113">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![Prestaties](./media/sql-database-performance/performance.png)

* <span data-ttu-id="32240-115">Hallo **aanbevelingen** tegel bevat een verdeling van aanbevelingen voor uw database afstemmen (drie belangrijkste aanbevelingen worden weergegeven als er meer zijn).</span><span class="sxs-lookup"><span data-stu-id="32240-115">hello **Recommendations** tile provides a breakdown of tuning recommendations for your database (top three recommendations are shown if there are more).</span></span> <span data-ttu-id="32240-116">Deze tegel te klikken gaat u verder te**[prestaties aanbevelingen](#performance-recommendations)**.</span><span class="sxs-lookup"><span data-stu-id="32240-116">Clicking this tile takes you too**[Performance recommendations](#performance-recommendations)**.</span></span> 
* <span data-ttu-id="32240-117">Hallo **afstemmen activiteit** tegel bevat een samenvatting van Hallo voltooide acties voor uw database afstemmen, zodat u snel inzicht in Hallo geschiedenis van het afstemmen van de activiteit.</span><span class="sxs-lookup"><span data-stu-id="32240-117">hello **Tuning activity** tile provides a summary of hello ongoing and completed tuning actions for your database, giving you a quick view into hello history of tuning activity.</span></span> <span data-ttu-id="32240-118">Deze tegel te klikken, gaat u toohello volledige afstemmen geschiedenisweergave voor uw database.</span><span class="sxs-lookup"><span data-stu-id="32240-118">Clicking this tile takes you toohello full tuning history view for your database.</span></span>
* <span data-ttu-id="32240-119">Hallo **automatische afstemming** tegel ziet Hallo [automatische afstemming configuratie](sql-database-automatic-tuning-enable.md) voor uw database (tuning opties die automatisch toegepaste tooyour database zijn).</span><span class="sxs-lookup"><span data-stu-id="32240-119">hello **Auto-tuning** tile shows hello [auto-tuning configuration](sql-database-automatic-tuning-enable.md) for your database (tuning options that are automatically applied tooyour database).</span></span> <span data-ttu-id="32240-120">Hallo automation configuratiedialoogvenster te klikken op deze tegel worden geopend.</span><span class="sxs-lookup"><span data-stu-id="32240-120">Clicking this tile opens hello automation configuration dialog.</span></span>
* <span data-ttu-id="32240-121">Hallo **databasequery's** tegel bevat Hallo van Hallo queryprestaties voor uw database (algehele DTU-gebruik en de bovenkant resource verbruikt query's).</span><span class="sxs-lookup"><span data-stu-id="32240-121">hello **Database queries** tile shows hello summary of hello query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="32240-122">Deze tegel te klikken gaat u verder te**[Query Performance Insight](#query-performance-insight)**.</span><span class="sxs-lookup"><span data-stu-id="32240-122">Clicking this tile takes you too**[Query Performance Insight](#query-performance-insight)**.</span></span>

## <a name="performance-recommendations"></a><span data-ttu-id="32240-123">Aanbevelingen voor prestaties</span><span class="sxs-lookup"><span data-stu-id="32240-123">Performance recommendations</span></span>
<span data-ttu-id="32240-124">Deze pagina bevat intelligent [afstemmen aanbevelingen](sql-database-advisor.md) die de prestaties van uw database kunt verbeteren.</span><span class="sxs-lookup"><span data-stu-id="32240-124">This page provides intelligent [tuning recommendations](sql-database-advisor.md) that can improve your database's performance.</span></span> <span data-ttu-id="32240-125">Hallo volgende typen aanbevelingen worden weergegeven op deze pagina:</span><span class="sxs-lookup"><span data-stu-id="32240-125">hello following types of recommendations are shown on this page:</span></span>

* <span data-ttu-id="32240-126">Aanbevelingen op welke indexen toocreate of drop.</span><span class="sxs-lookup"><span data-stu-id="32240-126">Recommendations on which indexes toocreate or drop.</span></span>
* <span data-ttu-id="32240-127">Aanbevelingen wanneer schema problemen zijn geïdentificeerd in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="32240-127">Recommendations when schema issues are identified in hello database.</span></span>
* <span data-ttu-id="32240-128">Aanbevelingen wanneer query's van query's profiteren kunnen.</span><span class="sxs-lookup"><span data-stu-id="32240-128">Recommendations when queries can benefit from parameterized queries.</span></span>

![Prestaties](./media/sql-database-performance/recommendations.png)

<span data-ttu-id="32240-130">U kunt ook volledige geschiedenis van het afstemmen van de acties die zijn toegepast in de afgelopen Hallo vinden.</span><span class="sxs-lookup"><span data-stu-id="32240-130">You can also find complete history of tuning actions that were applied in hello past.</span></span>

<span data-ttu-id="32240-131">Meer informatie over hoe een apply toofind prestaties aanbevelingen in [zoeken en toepassen van aanbevelingen voor prestaties](sql-database-advisor-portal.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="32240-131">Learn how toofind an apply performance recommendations in [Find and apply performance recommendations](sql-database-advisor-portal.md) article.</span></span>

## <a name="automatic-tuning"></a><span data-ttu-id="32240-132">Automatisch instellen</span><span class="sxs-lookup"><span data-stu-id="32240-132">Automatic tuning</span></span>
<span data-ttu-id="32240-133">Azure SQL-Databases kunt automatisch afstemmen van de databaseprestaties door toe te passen [prestaties aanbevelingen](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="32240-133">Azure SQL Databases can automatically tune database performance by applying [performance recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="32240-134">toolearn meer lezen [automatische afstemmen artikel](sql-database-automatic-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="32240-134">toolearn more, read [Automatic tuning article](sql-database-automatic-tuning.md).</span></span> <span data-ttu-id="32240-135">tooenable, lezen [hoe tooenable automatische afstemming](sql-database-automatic-tuning-enable.md).</span><span class="sxs-lookup"><span data-stu-id="32240-135">tooenable it, read [how tooenable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="32240-136">Inzicht in queryprestaties</span><span class="sxs-lookup"><span data-stu-id="32240-136">Query Performance Insight</span></span>
<span data-ttu-id="32240-137">[Query Performance Insight](sql-database-query-performance.md) kunt u toospend minder tijd databaseprestaties oplossen door op te geven:</span><span class="sxs-lookup"><span data-stu-id="32240-137">[Query Performance Insight](sql-database-query-performance.md) allows you toospend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="32240-138">Dieper inzicht in uw databases brongebruik (DTU).</span><span class="sxs-lookup"><span data-stu-id="32240-138">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="32240-139">Hallo bovenste CPU verbruikt query's mogelijk voor verbeterde prestaties kunnen worden afgestemd.</span><span class="sxs-lookup"><span data-stu-id="32240-139">hello top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="32240-140">Hallo mogelijkheid toodrill omlaag in de details op Hallo van een query.</span><span class="sxs-lookup"><span data-stu-id="32240-140">hello ability toodrill down into hello details of a query.</span></span> 

  ![Prestatiedashboard](./media/sql-database-query-performance/performance.png)

<span data-ttu-id="32240-142">Meer informatie over deze pagina niet vinden in Hallo artikel  **[hoe toouse Query Performance Insight](sql-database-query-performance.md)**.</span><span class="sxs-lookup"><span data-stu-id="32240-142">Find more information about this page in hello article **[How toouse Query Performance Insight](sql-database-query-performance.md)**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32240-143">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="32240-143">Additional resources</span></span>
* [<span data-ttu-id="32240-144">Azure SQL Database-prestaties richtlijnen voor individuele databases</span><span class="sxs-lookup"><span data-stu-id="32240-144">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="32240-145">Wanneer een elastische groep moet worden gebruikt?</span><span class="sxs-lookup"><span data-stu-id="32240-145">When should an elastic pool be used?</span></span>](sql-database-elastic-pool-guidance.md)

