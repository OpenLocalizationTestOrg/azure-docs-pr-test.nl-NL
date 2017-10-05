---
title: Realtime-gebeurtenissen verwerken met de verwerking van de Stream Analytics-gebeurtenis | Microsoft Docs
description: Meer informatie over hoe een set van Azure-services kan samenwerken voor het inschakelen van de verwerking van realtime-gebeurtenissen en analyses.
keywords: realtime verwerking, verwerking van gebeurtenissen, referentiearchitectuur
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: b3057be995e551aac0761c3ce40a8dbf828a5f29
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a><span data-ttu-id="d0be6-104">Verwijzen naar architectuur: realtime-gebeurtenissen verwerken met Microsoft Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d0be6-104">Reference architecture: Real-time event processing with Microsoft Azure Stream Analytics</span></span>
<span data-ttu-id="d0be6-105">De referentiearchitectuur voor realtime-gebeurtenissen verwerken met Azure Stream Analytics is bedoeld voor een algemene blauwdruk voor het implementeren van een realtime platform als een oplossing voor de stroom-de verwerking van service (PaaS) met Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d0be6-105">The reference architecture for real-time event processing with Azure Stream Analytics is intended to provide a generic blueprint for deploying a real-time platform as a service (PaaS) stream-processing solution with Microsoft Azure.</span></span>

## <a name="summary"></a><span data-ttu-id="d0be6-106">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="d0be6-106">Summary</span></span>
<span data-ttu-id="d0be6-107">Traditioneel zijn analytics-oplossingen gebaseerd op de mogelijkheden, zoals ETL (extract, transform, load) en datawarehousing, waar gegevens worden opgeslagen voordat de analyse.</span><span class="sxs-lookup"><span data-stu-id="d0be6-107">Traditionally, analytics solutions have been based on capabilities such as ETL (extract, transform, load) and data warehousing, where data is stored prior to analysis.</span></span> <span data-ttu-id="d0be6-108">Veranderende vereisten, met inbegrip van meer snel binnenkomende gegevens, zijn dit bestaande model om de limiet te pushen.</span><span class="sxs-lookup"><span data-stu-id="d0be6-108">Changing requirements, including more rapidly arriving data, are pushing this existing model to the limit.</span></span> <span data-ttu-id="d0be6-109">De mogelijkheid voor het analyseren van gegevens binnen het verplaatsen van streams voorafgaand aan de opslag is een oplossing en terwijl het is niet een nieuwe mogelijkheid, de methode niet algemeen is vastgesteld tussen alle bedrijfstak verticalen.</span><span class="sxs-lookup"><span data-stu-id="d0be6-109">The ability to analyze data within moving streams prior to storage is one solution, and while it is not a new capability, the approach has not been widely adopted across all industry verticals.</span></span> 

<span data-ttu-id="d0be6-110">Microsoft Azure biedt een uitgebreide catalogus analytics-technologieën die u kunnen ondersteunen een matrix van de oplossing voor verschillende scenario's en vereisten.</span><span class="sxs-lookup"><span data-stu-id="d0be6-110">Microsoft Azure provides an extensive catalog of analytics technologies that are capable of supporting an array of different solution scenarios and requirements.</span></span> <span data-ttu-id="d0be6-111">Selecteren welke Azure-services te implementeren voor een end-to-end-oplossing, kan een gegeven van de breedte van de offerings uitdaging zijn.</span><span class="sxs-lookup"><span data-stu-id="d0be6-111">Selecting which Azure services to deploy for an end-to-end solution can be a challenge given the breadth of offerings.</span></span> <span data-ttu-id="d0be6-112">Dit artikel is ontworpen om de mogelijkheden en de interoperabiliteit van de verschillende Azure-services die ondersteuning bieden voor een gebeurtenis streaming-oplossing te beschrijven.</span><span class="sxs-lookup"><span data-stu-id="d0be6-112">This paper is designed to describe the capabilities and interoperation of the various Azure services that support an event-streaming solution.</span></span> <span data-ttu-id="d0be6-113">Hierin wordt uitgelegd sommige scenario's waarin klanten van dit type benadering profiteren kunnen.</span><span class="sxs-lookup"><span data-stu-id="d0be6-113">It also explains some of the scenarios in which customers can benefit from this type of approach.</span></span>

## <a name="contents"></a><span data-ttu-id="d0be6-114">Inhoud</span><span class="sxs-lookup"><span data-stu-id="d0be6-114">Contents</span></span>
* <span data-ttu-id="d0be6-115">Managementsamenvatting</span><span class="sxs-lookup"><span data-stu-id="d0be6-115">Executive Summary</span></span>
* <span data-ttu-id="d0be6-116">Inleiding tot realtime-analyses</span><span class="sxs-lookup"><span data-stu-id="d0be6-116">Introduction to Real-Time Analytics</span></span>
* <span data-ttu-id="d0be6-117">Toegevoegde waarde van realtime-gegevens in Azure</span><span class="sxs-lookup"><span data-stu-id="d0be6-117">Value Proposition of Real-Time Data in Azure</span></span>
* <span data-ttu-id="d0be6-118">Algemene scenario's voor realtime-analyses</span><span class="sxs-lookup"><span data-stu-id="d0be6-118">Common Scenarios for Real-Time Analytics</span></span>
* <span data-ttu-id="d0be6-119">Architectuur en onderdelen</span><span class="sxs-lookup"><span data-stu-id="d0be6-119">Architecture and Components</span></span>
  * <span data-ttu-id="d0be6-120">Gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="d0be6-120">Data Sources</span></span>
  * <span data-ttu-id="d0be6-121">Gegevensintegratie laag</span><span class="sxs-lookup"><span data-stu-id="d0be6-121">Data-Integration Layer</span></span>
  * <span data-ttu-id="d0be6-122">Realtime-analyses laag</span><span class="sxs-lookup"><span data-stu-id="d0be6-122">Real-time Analytics Layer</span></span>
  * <span data-ttu-id="d0be6-123">Data Storage-laag</span><span class="sxs-lookup"><span data-stu-id="d0be6-123">Data Storage Layer</span></span>
  * <span data-ttu-id="d0be6-124">Presentatie / laag-verbruik</span><span class="sxs-lookup"><span data-stu-id="d0be6-124">Presentation / Consumption Layer</span></span>
* <span data-ttu-id="d0be6-125">Conclusie</span><span class="sxs-lookup"><span data-stu-id="d0be6-125">Conclusion</span></span>

<span data-ttu-id="d0be6-126">**Auteur:** Jeroen Feddersen, Solution Architect Datacenter Insights van uitmuntende Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="d0be6-126">**Author:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span></span>

<span data-ttu-id="d0be6-127">**Gepubliceerd:** januari 2015</span><span class="sxs-lookup"><span data-stu-id="d0be6-127">**Published:** January 2015</span></span>

<span data-ttu-id="d0be6-128">**Revisie:** 1.0</span><span class="sxs-lookup"><span data-stu-id="d0be6-128">**Revision:** 1.0</span></span>

<span data-ttu-id="d0be6-129">**Download:** [realtime-gebeurtenissen verwerken met Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span><span class="sxs-lookup"><span data-stu-id="d0be6-129">**Download:** [Real-Time Event Processing with Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span></span>

## <a name="get-help"></a><span data-ttu-id="d0be6-130">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="d0be6-130">Get help</span></span>
<span data-ttu-id="d0be6-131">Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="d0be6-131">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0be6-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d0be6-132">Next steps</span></span>
* [<span data-ttu-id="d0be6-133">Inleiding tot Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d0be6-133">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="d0be6-134">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d0be6-134">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="d0be6-135">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="d0be6-135">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="d0be6-136">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="d0be6-136">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="d0be6-137">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="d0be6-137">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

