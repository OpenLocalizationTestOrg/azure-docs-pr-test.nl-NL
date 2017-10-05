---
title: Azure Application Insights telemetrie gegevensmodel - Uitzonderingstelemetrie | Microsoft Docs
description: Application Insights-gegevensmodel voor uitzonderingstelemetrie
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 6b220b0cb6719bac606f599d657d08ab847c7590
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="9a063-103">Uitzonderingstelemetrie: Application Insights-gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="9a063-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="9a063-104">In [Application Insights](app-insights-overview.md), een exemplaar van de uitzondering vertegenwoordigt een verwerkt of niet-verwerkte uitzondering die is opgetreden tijdens het uitvoeren van de bewaakte toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a063-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of the monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="9a063-105">Probleem-Id</span><span class="sxs-lookup"><span data-stu-id="9a063-105">Problem Id</span></span>

<span data-ttu-id="9a063-106">Id van waar de uitzondering is opgetreden in de code.</span><span class="sxs-lookup"><span data-stu-id="9a063-106">Identifier of where the exception was thrown in code.</span></span> <span data-ttu-id="9a063-107">Gebruikt voor het groeperen van uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="9a063-107">Used for exceptions grouping.</span></span> <span data-ttu-id="9a063-108">Doorgaans is dit een combinatie van uitzonderingstype en een functie uit de aanroepstack.</span><span class="sxs-lookup"><span data-stu-id="9a063-108">Typically a combination of exception type and a function from the call stack.</span></span>

<span data-ttu-id="9a063-109">Maximale lengte: 1024 tekens</span><span class="sxs-lookup"><span data-stu-id="9a063-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="9a063-110">Ernstniveau</span><span class="sxs-lookup"><span data-stu-id="9a063-110">Severity level</span></span>

<span data-ttu-id="9a063-111">Ernstniveau traceren.</span><span class="sxs-lookup"><span data-stu-id="9a063-111">Trace severity level.</span></span> <span data-ttu-id="9a063-112">Waarde kan zijn `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="9a063-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="9a063-113">Details van uitzondering</span><span class="sxs-lookup"><span data-stu-id="9a063-113">Exception details</span></span>

<span data-ttu-id="9a063-114">(Om te worden uitgebreid)</span><span class="sxs-lookup"><span data-stu-id="9a063-114">(To be extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="9a063-115">Aangepaste eigenschappen</span><span class="sxs-lookup"><span data-stu-id="9a063-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="9a063-116">Aangepaste metingen</span><span class="sxs-lookup"><span data-stu-id="9a063-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="9a063-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9a063-117">Next steps</span></span>

- <span data-ttu-id="9a063-118">Zie [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.</span><span class="sxs-lookup"><span data-stu-id="9a063-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="9a063-119">Meer informatie over hoe [onderzoeken uitzonderingen in uw web-apps met Application Insights](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="9a063-119">Learn how to [diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="9a063-120">Bekijk [platforms](app-insights-platforms.md) ondersteund door de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9a063-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
