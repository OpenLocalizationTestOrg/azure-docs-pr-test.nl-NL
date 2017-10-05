---
title: "Geïntegreerde oplossingen bouwen met SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: d407c29f99fd7537590ec787febd84a9e3f4f353
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="65fe7-103">Gebruikmaken van andere services met SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="65fe7-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="65fe7-104">Naast de kernfunctionaliteit kunnen SQL Data Warehouse gebruikers gebruikmaken van veel van de andere services in Azure ernaast.</span><span class="sxs-lookup"><span data-stu-id="65fe7-104">In addition to its core functionality, SQL Data Warehouse enables users to leverage many of the other services in Azure alongside it.</span></span>  <span data-ttu-id="65fe7-105">In het bijzonder hebben we stappen diep integreren met de volgende momenteel genomen:</span><span class="sxs-lookup"><span data-stu-id="65fe7-105">Specifically, we have currently taken steps to deeply integrate with the following:</span></span>

* <span data-ttu-id="65fe7-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="65fe7-106">Power BI</span></span>
* <span data-ttu-id="65fe7-107">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="65fe7-107">Azure Data Factory</span></span>
* <span data-ttu-id="65fe7-108">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="65fe7-108">Azure Machine Learning</span></span>
* <span data-ttu-id="65fe7-109">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="65fe7-109">Azure Stream Analytics</span></span>

<span data-ttu-id="65fe7-110">We werken aan verbinding maken met meer services die via het Azure-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="65fe7-110">We are working to connect with more services across the Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="65fe7-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="65fe7-111">Power BI</span></span>
<span data-ttu-id="65fe7-112">Integratie van Power BI kunt u gebruikmaken van de rekencapaciteit van SQL Data Warehouse met dynamische rapportage en visualisatie van Power BI.</span><span class="sxs-lookup"><span data-stu-id="65fe7-112">Power BI integration allows you to leverage the compute power of SQL Data Warehouse with the dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="65fe7-113">Power BI-integratie omvat momenteel:</span><span class="sxs-lookup"><span data-stu-id="65fe7-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="65fe7-114">**Verbinding maken met directe**: een meer geavanceerde verbinding met logische naar beneden duwen tegen SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="65fe7-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="65fe7-115">Dit biedt sneller analyse op grotere schaal.</span><span class="sxs-lookup"><span data-stu-id="65fe7-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="65fe7-116">**Openen in Power BI**: de knop 'Openen in Power BI' geeft informatie over het exemplaar aan Power BI zodat voor een meer naadloze verbinding.</span><span class="sxs-lookup"><span data-stu-id="65fe7-116">**Open in Power BI**: The 'Open in Power BI' button passes instance information to Power BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="65fe7-117">Zie [integreren met Power BI](sql-data-warehouse-integrate-power-bi.md) of de [Power BI-documentatie](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="65fe7-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or the [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="65fe7-118">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="65fe7-118">Azure Data Factory</span></span>
<span data-ttu-id="65fe7-119">Azure Data Factory biedt gebruikers een beheerd platform voor het maken van complexe Extract Load pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="65fe7-119">Azure Data Factory gives users a managed platform to create complex Extract-Load pipelines.</span></span>  <span data-ttu-id="65fe7-120">SQL Data Warehouse-integratie met Azure Data Factory omvat het volgende:</span><span class="sxs-lookup"><span data-stu-id="65fe7-120">SQL Data Warehouse's integration with Azure Data Factory includes the following:</span></span>

* <span data-ttu-id="65fe7-121">**Opgeslagen Procedures**: indelen van de uitvoering van opgeslagen procedures op de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="65fe7-121">**Stored Procedures**: Orchestrate the execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="65fe7-122">**Kopiëren**: ADF gebruiken om gegevens te verplaatsen naar SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="65fe7-122">**Copy**: Use ADF to move data into SQL Data Warehouse.</span></span>  <span data-ttu-id="65fe7-123">Deze bewerking kunt ADF standaardgegevens gegevensverplaatsing mechanisme of PolyBase gebruiken onder de behandelt.</span><span class="sxs-lookup"><span data-stu-id="65fe7-123">This operation can use ADF's standard data movement mechanism or PolyBase under the covers.</span></span> 

<span data-ttu-id="65fe7-124">Zie [integreren met Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) of de [documentatie Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="65fe7-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="65fe7-125">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="65fe7-125">Azure Machine Learning</span></span>
<span data-ttu-id="65fe7-126">Azure Machine Learning is een volledig beheerde analytics-service waarmee gebruikers om complexe modellen gebruik te maken van een groot aantal voorspellende hulpprogramma's te maken.</span><span class="sxs-lookup"><span data-stu-id="65fe7-126">Azure Machine Learning is a fully managed analytics service which allows users to create intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="65fe7-127">SQL Data Warehouse wordt ondersteund als een bron- en doel voor deze modellen met de volgende functies:</span><span class="sxs-lookup"><span data-stu-id="65fe7-127">SQL Data Warehouse is supported as both a source and destination for these models with the following functionality:</span></span>

* <span data-ttu-id="65fe7-128">**Gegevens lezen:** modellen station op grote schaal met T-SQL met SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="65fe7-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="65fe7-129">**Schrijven van gegevens:** doorvoeren wordt gewijzigd van een model terug naar SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="65fe7-129">**Write Data:** Commit changes from any model back to SQL Data Warehouse.</span></span>

<span data-ttu-id="65fe7-130">Zie [integreren met Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) of de [Azure Machine Learning-documentatie](https://azure.microsoft.com/services/machine-learning/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="65fe7-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or the [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="65fe7-131">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="65fe7-131">Azure Stream Analytics</span></span>
<span data-ttu-id="65fe7-132">Azure Stream Analytics is een volledig beheerde complexe infrastructuur voor het verwerken en gebruiken van gebeurtenisgegevens die zijn gegenereerd uit Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="65fe7-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="65fe7-133">Integratie met SQL Data Warehouse kan voor streaming gegevens effectief worden verwerkt en opgeslagen samen met relationele gegevens diepere, meer geavanceerde analyse inschakelen.</span><span class="sxs-lookup"><span data-stu-id="65fe7-133">Integration with SQL Data Warehouse allows for streaming data to be effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="65fe7-134">**Taakuitvoer:** uitvoer van de Stream Analytics-taken rechtstreeks naar SQL Data Warehouse verzenden.</span><span class="sxs-lookup"><span data-stu-id="65fe7-134">**Job Output:** Send output from Stream Analytics jobs directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="65fe7-135">Zie [integreren met Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) of de [Azure Stream Analytics-documentatie](https://azure.microsoft.com/documentation/services/stream-analytics/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="65fe7-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or the [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

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
