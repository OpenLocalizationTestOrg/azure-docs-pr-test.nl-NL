---
title: Azure Application Insights telemetrie gegevensmodel - Afhankelijkheidstelemetrie | Microsoft Docs
description: Application Insights-gegevensmodel voor afhankelijkheidstelemetrie
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/17/2017
ms.author: bwren
ms.openlocfilehash: 2e97c3f951f46c32802aea543b93d5ab1bb76228
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a><span data-ttu-id="58847-103">Afhankelijkheidstelemetrie: Application Insights-gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="58847-103">Dependency telemetry: Application Insights data model</span></span>

<span data-ttu-id="58847-104">Afhankelijkheidstelemetrie (in [Application Insights](app-insights-overview.md)) vertegenwoordigt een interactie van het bewaakte onderdeel met een externe component zoals SQL of een HTTP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="58847-104">Dependency Telemetry (in [Application Insights](app-insights-overview.md)) represents an interaction of the monitored component with a remote component such as SQL or an HTTP endpoint.</span></span>

## <a name="name"></a><span data-ttu-id="58847-105">Naam</span><span class="sxs-lookup"><span data-stu-id="58847-105">Name</span></span>

<span data-ttu-id="58847-106">De naam van de opdracht die is gestart met deze afhankelijkheidsaanroep.</span><span class="sxs-lookup"><span data-stu-id="58847-106">Name of the command initiated with this dependency call.</span></span> <span data-ttu-id="58847-107">De kardinaliteit van de lage waarde.</span><span class="sxs-lookup"><span data-stu-id="58847-107">Low cardinality value.</span></span> <span data-ttu-id="58847-108">Voorbeelden zijn opgeslagen procedurenaam en sjabloon voor URL-pad.</span><span class="sxs-lookup"><span data-stu-id="58847-108">Examples are stored procedure name and URL path template.</span></span>

## <a name="id"></a><span data-ttu-id="58847-109">Id</span><span class="sxs-lookup"><span data-stu-id="58847-109">ID</span></span>

<span data-ttu-id="58847-110">Id van een exemplaar van de aanroep van afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="58847-110">Identifier of a dependency call instance.</span></span> <span data-ttu-id="58847-111">Gebruikt voor correlatie met de aanvraag telemetrie-item dat overeenkomt met deze afhankelijkheidsaanroep.</span><span class="sxs-lookup"><span data-stu-id="58847-111">Used for correlation with the request telemetry item corresponding to this dependency call.</span></span> <span data-ttu-id="58847-112">Zie voor meer informatie [correlatie](application-insights-correlation.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="58847-112">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="data"></a><span data-ttu-id="58847-113">Gegevens</span><span class="sxs-lookup"><span data-stu-id="58847-113">Data</span></span>

<span data-ttu-id="58847-114">Opdracht die door deze afhankelijkheidsaanroep gestart.</span><span class="sxs-lookup"><span data-stu-id="58847-114">Command initiated by this dependency call.</span></span> <span data-ttu-id="58847-115">Voorbeelden zijn SQL-instructie en HTTP-URL met alle queryparameters.</span><span class="sxs-lookup"><span data-stu-id="58847-115">Examples are SQL statement and HTTP URL with all query parameters.</span></span>

## <a name="type"></a><span data-ttu-id="58847-116">Type</span><span class="sxs-lookup"><span data-stu-id="58847-116">Type</span></span>

<span data-ttu-id="58847-117">Afhankelijkheid typenaam.</span><span class="sxs-lookup"><span data-stu-id="58847-117">Dependency type name.</span></span> <span data-ttu-id="58847-118">De waarde van de lage kardinaliteit voor logische groepering van afhankelijkheden en de interpretatie van andere velden zoals commandName en resultCode.</span><span class="sxs-lookup"><span data-stu-id="58847-118">Low cardinality value for logical grouping of dependencies and interpretation of other fields like commandName and resultCode.</span></span> <span data-ttu-id="58847-119">Voorbeelden zijn SQL Azure-tabel en HTTP.</span><span class="sxs-lookup"><span data-stu-id="58847-119">Examples are SQL, Azure table, and HTTP.</span></span>

## <a name="target"></a><span data-ttu-id="58847-120">doel</span><span class="sxs-lookup"><span data-stu-id="58847-120">Target</span></span>

<span data-ttu-id="58847-121">Site van het doel van een afhankelijkheidsaanroep van.</span><span class="sxs-lookup"><span data-stu-id="58847-121">Target site of a dependency call.</span></span> <span data-ttu-id="58847-122">Voorbeelden zijn servernaam, hostadres.</span><span class="sxs-lookup"><span data-stu-id="58847-122">Examples are server name, host address.</span></span> <span data-ttu-id="58847-123">Zie voor meer informatie [correlatie](application-insights-correlation.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="58847-123">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="duration"></a><span data-ttu-id="58847-124">Duur</span><span class="sxs-lookup"><span data-stu-id="58847-124">Duration</span></span>

<span data-ttu-id="58847-125">Duur in de indeling van aanvraag: `DD.HH:MM:SS.MMMMMM`.</span><span class="sxs-lookup"><span data-stu-id="58847-125">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="58847-126">Moet kleiner zijn dan `1000` dagen.</span><span class="sxs-lookup"><span data-stu-id="58847-126">Must be less than `1000` days.</span></span>

## <a name="result-code"></a><span data-ttu-id="58847-127">Resultaatcode</span><span class="sxs-lookup"><span data-stu-id="58847-127">Result code</span></span>

<span data-ttu-id="58847-128">De resultaatcode van een afhankelijkheidsaanroep van.</span><span class="sxs-lookup"><span data-stu-id="58847-128">Result code of a dependency call.</span></span> <span data-ttu-id="58847-129">Voorbeelden zijn SQL-foutcode en HTTP-statuscode.</span><span class="sxs-lookup"><span data-stu-id="58847-129">Examples are SQL error code and HTTP status code.</span></span>

## <a name="success"></a><span data-ttu-id="58847-130">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="58847-130">Success</span></span>

<span data-ttu-id="58847-131">De vermelding van geslaagde of mislukte aanroep.</span><span class="sxs-lookup"><span data-stu-id="58847-131">Indication of successful or unsuccessful call.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="58847-132">Aangepaste eigenschappen</span><span class="sxs-lookup"><span data-stu-id="58847-132">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="58847-133">Aangepaste metingen</span><span class="sxs-lookup"><span data-stu-id="58847-133">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a><span data-ttu-id="58847-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="58847-134">Next steps</span></span>

- <span data-ttu-id="58847-135">Instellen voor bijhouden van afhankelijkheid [.NET](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="58847-135">Set up dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span></span>
- <span data-ttu-id="58847-136">Instellen voor bijhouden van afhankelijkheid [Java](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="58847-136">Set up dependency tracking for [Java](app-insights-java-agent.md).</span></span>
- [<span data-ttu-id="58847-137">Aangepaste afhankelijkheidstelemetrie schrijven</span><span class="sxs-lookup"><span data-stu-id="58847-137">Write custom dependency telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackdependency)
- <span data-ttu-id="58847-138">Zie [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.</span><span class="sxs-lookup"><span data-stu-id="58847-138">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="58847-139">Bekijk [platforms](app-insights-platforms.md) ondersteund door de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="58847-139">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
