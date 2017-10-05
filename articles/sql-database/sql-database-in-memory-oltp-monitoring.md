---
title: XTP geheugenopslag bewaken | Microsoft Docs
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
ms.openlocfilehash: 5afb2209f18b1ba2aa0a916a439509b01afd80da
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="5faab-103">OLTP-opslag in het geheugen controleren</span><span class="sxs-lookup"><span data-stu-id="5faab-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="5faab-104">Wanneer u [In het geheugen OLTP](sql-database-in-memory.md), gegevens in tabellen geoptimaliseerd voor geheugen en tabelvariabelen bevindt zich in In het geheugen OLTP-opslag.</span><span class="sxs-lookup"><span data-stu-id="5faab-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="5faab-105">Elke servicelaag Premium heeft een maximale In het geheugen OLTP opslaggrootte, die wordt beschreven in de [SQL Database servicecategorieën artikel](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="5faab-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="5faab-106">Wanneer deze limiet wordt overschreden, invoegen en bijwerken bewerkingen mogelijk mislukken (met de fout 41823).</span><span class="sxs-lookup"><span data-stu-id="5faab-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="5faab-107">Op dat moment wordt u nodig aan gegevens om geheugen vrij te verwijderen of upgraden van de prestatielaag van de database.</span><span class="sxs-lookup"><span data-stu-id="5faab-107">At that point you will need to either delete data to reclaim memory, or upgrade the performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-the-in-memory-storage-cap"></a><span data-ttu-id="5faab-108">Bepalen of gegevens binnen het kapje in het geheugen, opslag past</span><span class="sxs-lookup"><span data-stu-id="5faab-108">Determine whether data will fit within the in-memory storage cap</span></span>
<span data-ttu-id="5faab-109">Bepalen van het kapje opslag: Raadpleeg de [SQL Database servicecategorieën artikel](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) voor de opslag caps van de verschillende Servicelagen van Premium.</span><span class="sxs-lookup"><span data-stu-id="5faab-109">Determine the storage cap: consult the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for the storage caps of the different Premium service tiers.</span></span>

<span data-ttu-id="5faab-110">Het schatten van geheugenvereisten voor een tabel geoptimaliseerd voor geheugen works voor SQL Server dezelfde manier als het komt in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="5faab-110">Estimating memory requirements for a memory-optimized table works the same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="5faab-111">Enkele minuten duren om te controleren dat onderwerp op [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span><span class="sxs-lookup"><span data-stu-id="5faab-111">Take a few minutes to review that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="5faab-112">Houd er rekening mee dat de tabel en variabele tabelrijen, evenals indexen, voor de gegevensgrootte max gebruiker meetellen.</span><span class="sxs-lookup"><span data-stu-id="5faab-112">Note that the table and table variable rows, as well as indexes, count toward the max user data size.</span></span> <span data-ttu-id="5faab-113">ALTER TABLE moet bovendien voldoende ruimte voor het maken van een nieuwe versie van de gehele tabel en de indexen ervan.</span><span class="sxs-lookup"><span data-stu-id="5faab-113">In addition, ALTER TABLE needs enough room to create a new version of the entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="5faab-114">Bewaking en waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="5faab-114">Monitoring and alerting</span></span>
<span data-ttu-id="5faab-115">U kunt bewaken opslaggebruik in het geheugen als percentage van de [cap opslag voor de prestatielaag](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in Azure [portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="5faab-115">You can monitor in-memory storage use as a percentage of the [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in the Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="5faab-116">Zoek het gebruik van Resource op de blade Database en klik op bewerken.</span><span class="sxs-lookup"><span data-stu-id="5faab-116">On the Database blade, locate the Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="5faab-117">Selecteer vervolgens de metriek `In-Memory OLTP Storage percentage`.</span><span class="sxs-lookup"><span data-stu-id="5faab-117">Then select the metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="5faab-118">Als u wilt een waarschuwing toevoegen, klikt u op in het vak Resourcegebruik om de metriek blade te openen en klik vervolgens op waarschuwing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5faab-118">To add an alert, click on the Resource Utilization box to open the Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="5faab-119">Of gebruik de volgende query voor het gebruik van de opslag in het geheugen weergeven:</span><span class="sxs-lookup"><span data-stu-id="5faab-119">Or use the following query to show the in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="5faab-120">Juiste-geheugen situaties - fout 41823</span><span class="sxs-lookup"><span data-stu-id="5faab-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="5faab-121">-Geheugen resultaten uitgevoerd in invoegen, bijwerken en bewerkingen is mislukt met foutbericht 41823 maakt.</span><span class="sxs-lookup"><span data-stu-id="5faab-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="5faab-122">Foutbericht 41823 geeft aan dat de tabellen geoptimaliseerd voor geheugen en tabelvariabelen de maximale grootte overschreden.</span><span class="sxs-lookup"><span data-stu-id="5faab-122">Error message 41823 indicates that the memory-optimized tables and table variables have exceeded the maximum size.</span></span>

<span data-ttu-id="5faab-123">Deze fout, ofwel oplossen:</span><span class="sxs-lookup"><span data-stu-id="5faab-123">To resolve this error, either:</span></span>

* <span data-ttu-id="5faab-124">Gegevens verwijderen uit de tabellen geoptimaliseerd voor geheugen, mogelijk offloading van de gegevens naar de traditionele, schijfgebaseerde tabellen. of,</span><span class="sxs-lookup"><span data-stu-id="5faab-124">Delete data from the memory-optimized tables, potentially offloading the data to traditional, disk-based tables; or,</span></span>
* <span data-ttu-id="5faab-125">De servicetier upgraden naar een met voldoende opslagruimte in het geheugen voor de gegevens die u wilt bewaren in tabellen geoptimaliseerd voor geheugen.</span><span class="sxs-lookup"><span data-stu-id="5faab-125">Upgrade the service tier to one with enough in-memory storage for the data you need to keep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5faab-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5faab-126">Next steps</span></span>
<span data-ttu-id="5faab-127">Zie voor richtlijnen bewaking, [bewaking Azure SQL Database met dynamische beheerweergaven](sql-database-monitoring-with-dmvs.md).</span><span class="sxs-lookup"><span data-stu-id="5faab-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>
