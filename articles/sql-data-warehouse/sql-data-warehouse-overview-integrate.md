---
title: "aaaBuild oplossingen geïntegreerd met SQL Data Warehouse | Microsoft Docs"
description: "Hulpprogramma's en partners met oplossingen die zijn geïntegreerd met SQL Data Warehouse. "
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: c8a4202dd84305bea4e4c2faf0e4791d026e794f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="c50b4-103">Gebruikmaken van andere services met SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c50b4-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="c50b4-104">Bovendien tooits functionaliteit core, SQL Data Warehouse kunnen gebruikers tooleverage veel van andere services in Azure ernaast Hallo.</span><span class="sxs-lookup"><span data-stu-id="c50b4-104">In addition tooits core functionality, SQL Data Warehouse enables users tooleverage many of hello other services in Azure alongside it.</span></span>  <span data-ttu-id="c50b4-105">In het bijzonder hebben we stappen toodeeply integreren met de volgende Hallo momenteel genomen:</span><span class="sxs-lookup"><span data-stu-id="c50b4-105">Specifically, we have currently taken steps toodeeply integrate with hello following:</span></span>

* <span data-ttu-id="c50b4-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="c50b4-106">Power BI</span></span>
* <span data-ttu-id="c50b4-107">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c50b4-107">Azure Data Factory</span></span>
* <span data-ttu-id="c50b4-108">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c50b4-108">Azure Machine Learning</span></span>
* <span data-ttu-id="c50b4-109">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c50b4-109">Azure Stream Analytics</span></span>

<span data-ttu-id="c50b4-110">We werken tooconnect met meer services via hello Azure-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="c50b4-110">We are working tooconnect with more services across hello Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="c50b4-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="c50b4-111">Power BI</span></span>
<span data-ttu-id="c50b4-112">Integratie van Power BI kunt u tooleverage Hallo rekencapaciteit van SQL Data Warehouse met dynamische Hallo-rapportage en visualisatie van Power BI.</span><span class="sxs-lookup"><span data-stu-id="c50b4-112">Power BI integration allows you tooleverage hello compute power of SQL Data Warehouse with hello dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="c50b4-113">Power BI-integratie omvat momenteel:</span><span class="sxs-lookup"><span data-stu-id="c50b4-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="c50b4-114">**Verbinding maken met directe**: een meer geavanceerde verbinding met logische naar beneden duwen tegen SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c50b4-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="c50b4-115">Dit biedt sneller analyse op grotere schaal.</span><span class="sxs-lookup"><span data-stu-id="c50b4-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="c50b4-116">**Openen in Power BI**: 'Te openen in Power BI' Hallo-knop exemplaar informatie tooPower BI, waardoor het een meer naadloze verbinding is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="c50b4-116">**Open in Power BI**: hello 'Open in Power BI' button passes instance information tooPower BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="c50b4-117">Zie [integreren met Power BI](sql-data-warehouse-integrate-power-bi.md) of Hallo [Power BI-documentatie](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c50b4-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or hello [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="c50b4-118">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c50b4-118">Azure Data Factory</span></span>
<span data-ttu-id="c50b4-119">Azure Data Factory biedt gebruikers een beheerd platform toocreate die complexe Extract belasting pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="c50b4-119">Azure Data Factory gives users a managed platform toocreate complex Extract-Load pipelines.</span></span>  <span data-ttu-id="c50b4-120">SQL Data Warehouse-integratie met Azure Data Factory bevat Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="c50b4-120">SQL Data Warehouse's integration with Azure Data Factory includes hello following:</span></span>

* <span data-ttu-id="c50b4-121">**Opgeslagen Procedures**: indelen Hallo uitvoering van opgeslagen procedures op de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c50b4-121">**Stored Procedures**: Orchestrate hello execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="c50b4-122">**Kopiëren**: gebruik ADF toomove gegevens in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c50b4-122">**Copy**: Use ADF toomove data into SQL Data Warehouse.</span></span>  <span data-ttu-id="c50b4-123">Deze bewerking kunt ADF standaardgegevens gegevensverplaatsing mechanisme gebruiken of PolyBase onder Hallo worden behandeld.</span><span class="sxs-lookup"><span data-stu-id="c50b4-123">This operation can use ADF's standard data movement mechanism or PolyBase under hello covers.</span></span> 

<span data-ttu-id="c50b4-124">Zie [integreren met Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) of Hallo [documentatie Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c50b4-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="c50b4-125">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c50b4-125">Azure Machine Learning</span></span>
<span data-ttu-id="c50b4-126">Azure Machine Learning is een volledig beheerde analytics-service waarmee gebruikers toocreate complexe modellen gebruik te maken van een groot aantal voorspellende hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="c50b4-126">Azure Machine Learning is a fully managed analytics service which allows users toocreate intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="c50b4-127">SQL Data Warehouse wordt ondersteund als een bron- en doel voor deze modellen Hello functionaliteit te volgen:</span><span class="sxs-lookup"><span data-stu-id="c50b4-127">SQL Data Warehouse is supported as both a source and destination for these models with hello following functionality:</span></span>

* <span data-ttu-id="c50b4-128">**Gegevens lezen:** modellen station op grote schaal met T-SQL met SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c50b4-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="c50b4-129">**Schrijven van gegevens:** wijzigingen van een model back-tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c50b4-129">**Write Data:** Commit changes from any model back tooSQL Data Warehouse.</span></span>

<span data-ttu-id="c50b4-130">Zie [integreren met Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) of Hallo [Azure Machine Learning-documentatie](https://azure.microsoft.com/services/machine-learning/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c50b4-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or hello [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="c50b4-131">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c50b4-131">Azure Stream Analytics</span></span>
<span data-ttu-id="c50b4-132">Azure Stream Analytics is een volledig beheerde complexe infrastructuur voor het verwerken en gebruiken van gebeurtenisgegevens die zijn gegenereerd uit Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="c50b4-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="c50b4-133">Integratie met SQL Data Warehouse kan voor streaming gegevens toobe effectief verwerkt en opgeslagen samen met relationele gegevens beter inschakelen, meer geavanceerde analyse.</span><span class="sxs-lookup"><span data-stu-id="c50b4-133">Integration with SQL Data Warehouse allows for streaming data toobe effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="c50b4-134">**Taakuitvoer:** verzenden uitvoer van de Stream Analytics taken rechtstreeks tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c50b4-134">**Job Output:** Send output from Stream Analytics jobs directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="c50b4-135">Zie [integreren met Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) of Hallo [Azure Stream Analytics-documentatie](https://azure.microsoft.com/documentation/services/stream-analytics/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c50b4-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or hello [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
