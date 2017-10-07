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
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="20ef9-103">OLTP-opslag in het geheugen controleren</span><span class="sxs-lookup"><span data-stu-id="20ef9-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="20ef9-104">Wanneer u [In het geheugen OLTP](sql-database-in-memory.md), gegevens in tabellen geoptimaliseerd voor geheugen en tabelvariabelen bevindt zich in In het geheugen OLTP-opslag.</span><span class="sxs-lookup"><span data-stu-id="20ef9-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="20ef9-105">Elke servicelaag Premium heeft een maximale In het geheugen OLTP opslaggrootte, die wordt beschreven in Hallo [SQL Database servicecategorieën artikel](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="20ef9-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="20ef9-106">Wanneer deze limiet wordt overschreden, invoegen en bijwerken bewerkingen mogelijk mislukken (met de fout 41823).</span><span class="sxs-lookup"><span data-stu-id="20ef9-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="20ef9-107">Op dat moment wordt u tooeither verwijderen gegevens tooreclaim geheugen nodig hebben of upgrade van de prestatielaag Hallo van uw database.</span><span class="sxs-lookup"><span data-stu-id="20ef9-107">At that point you will need tooeither delete data tooreclaim memory, or upgrade hello performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a><span data-ttu-id="20ef9-108">Bepalen of gegevens binnen het Hallo-geheugenopslag cap past</span><span class="sxs-lookup"><span data-stu-id="20ef9-108">Determine whether data will fit within hello in-memory storage cap</span></span>
<span data-ttu-id="20ef9-109">Hallo opslag cap bepalen: Raadpleeg Hallo [SQL Database servicecategorieën artikel](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) voor Hallo opslag caps van Hallo verschillende Premium-Servicelagen.</span><span class="sxs-lookup"><span data-stu-id="20ef9-109">Determine hello storage cap: consult hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for hello storage caps of hello different Premium service tiers.</span></span>

<span data-ttu-id="20ef9-110">Het schatten van de vereisten voor een tabel geoptimaliseerd voor geheugen werkt Hallo dezelfde geheugen komt manier voor SQL Server als het in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="20ef9-110">Estimating memory requirements for a memory-optimized table works hello same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="20ef9-111">Een paar minuten tooreview dat onderwerp nemen op [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span><span class="sxs-lookup"><span data-stu-id="20ef9-111">Take a few minutes tooreview that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="20ef9-112">Houd er rekening mee dat Hallo tabel en variabele tabelrijen, evenals indexen, voor Hallo max gebruiker gegevensgrootte meetellen.</span><span class="sxs-lookup"><span data-stu-id="20ef9-112">Note that hello table and table variable rows, as well as indexes, count toward hello max user data size.</span></span> <span data-ttu-id="20ef9-113">ALTER TABLE moet bovendien voldoende ruimte toocreate een nieuwe versie van de gehele tabel Hallo en de indexen ervan.</span><span class="sxs-lookup"><span data-stu-id="20ef9-113">In addition, ALTER TABLE needs enough room toocreate a new version of hello entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="20ef9-114">Bewaking en waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="20ef9-114">Monitoring and alerting</span></span>
<span data-ttu-id="20ef9-115">U kunt bewaken opslaggebruik in het geheugen als percentage van Hallo [cap opslag voor de prestatielaag](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in hello Azure [portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="20ef9-115">You can monitor in-memory storage use as a percentage of hello [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in hello Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="20ef9-116">Op de databaseblade Hallo, Ga naar Hallo Resource gebruik vak en klik op bewerken.</span><span class="sxs-lookup"><span data-stu-id="20ef9-116">On hello Database blade, locate hello Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="20ef9-117">Selecteer vervolgens de metriek Hallo `In-Memory OLTP Storage percentage`.</span><span class="sxs-lookup"><span data-stu-id="20ef9-117">Then select hello metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="20ef9-118">tooadd een waarschuwing, klikt u op Hallo Resourcegebruik vak tooopen Hallo metrische blade en klik vervolgens op waarschuwing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="20ef9-118">tooadd an alert, click on hello Resource Utilization box tooopen hello Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="20ef9-119">Of gebruik Hallo query tooshow Hallo in het geheugen opslaggebruik te volgen:</span><span class="sxs-lookup"><span data-stu-id="20ef9-119">Or use hello following query tooshow hello in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="20ef9-120">Juiste-geheugen situaties - fout 41823</span><span class="sxs-lookup"><span data-stu-id="20ef9-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="20ef9-121">-Geheugen resultaten uitgevoerd in invoegen, bijwerken en bewerkingen is mislukt met foutbericht 41823 maakt.</span><span class="sxs-lookup"><span data-stu-id="20ef9-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="20ef9-122">Foutbericht 41823 geeft aan dat Hallo geheugen geoptimaliseerde tabellen en tabelvariabelen Hallo maximale grootte overschreden.</span><span class="sxs-lookup"><span data-stu-id="20ef9-122">Error message 41823 indicates that hello memory-optimized tables and table variables have exceeded hello maximum size.</span></span>

<span data-ttu-id="20ef9-123">tooresolve deze fout, hetzij:</span><span class="sxs-lookup"><span data-stu-id="20ef9-123">tooresolve this error, either:</span></span>

* <span data-ttu-id="20ef9-124">Gegevens verwijderen uit het Hallo geheugen geoptimaliseerde tabellen, mogelijk offloading Hallo gegevens tootraditional, schijfgebaseerde tabellen. of,</span><span class="sxs-lookup"><span data-stu-id="20ef9-124">Delete data from hello memory-optimized tables, potentially offloading hello data tootraditional, disk-based tables; or,</span></span>
* <span data-ttu-id="20ef9-125">Hallo service tier tooone upgraden met voldoende opslagruimte in het geheugen voor Hallo gegevens moet u tookeep in tabellen geoptimaliseerd voor geheugen.</span><span class="sxs-lookup"><span data-stu-id="20ef9-125">Upgrade hello service tier tooone with enough in-memory storage for hello data you need tookeep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20ef9-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="20ef9-126">Next steps</span></span>
<span data-ttu-id="20ef9-127">Zie voor richtlijnen bewaking, [bewaking Azure SQL Database met dynamische beheerweergaven](sql-database-monitoring-with-dmvs.md).</span><span class="sxs-lookup"><span data-stu-id="20ef9-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>
