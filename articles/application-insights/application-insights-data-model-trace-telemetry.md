---
title: Azure Application Insights telemetrie gegevensmodel - Tracetelemetrie | Microsoft Docs
description: Application Insights-gegevensmodel voor tracetelemetrie
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
ms.openlocfilehash: e1da0d6a6fbd9ca5486936c326ade667d7b01006
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="trace-telemetry-application-insights-data-model"></a><span data-ttu-id="fb2f9-103">Telemetrie traceren: Application Insights-gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="fb2f9-103">Trace telemetry: Application Insights data model</span></span>

<span data-ttu-id="fb2f9-104">Telemetrie traceren (in [Application Insights](app-insights-overview.md)) vertegenwoordigt `printf` stijl trace-instructies die tekst doorzocht.</span><span class="sxs-lookup"><span data-stu-id="fb2f9-104">Trace telemetry (in [Application Insights](app-insights-overview.md)) represents `printf` style trace statements that are text-searched.</span></span> <span data-ttu-id="fb2f9-105">`Log4Net`, `NLog`, en andere vermeldingen in logboekbestanden op basis van tekst worden vertaald naar exemplaren van dit type.</span><span class="sxs-lookup"><span data-stu-id="fb2f9-105">`Log4Net`, `NLog`, and other text-based log file entries are translated into instances of this type.</span></span> <span data-ttu-id="fb2f9-106">De tracering heeft geen metingen als een uitbreidbaarheid.</span><span class="sxs-lookup"><span data-stu-id="fb2f9-106">The trace does not have measurements as an extensibility.</span></span>

## <a name="message"></a><span data-ttu-id="fb2f9-107">Bericht</span><span class="sxs-lookup"><span data-stu-id="fb2f9-107">Message</span></span>

<span data-ttu-id="fb2f9-108">Trace-bericht.</span><span class="sxs-lookup"><span data-stu-id="fb2f9-108">Trace message.</span></span>

<span data-ttu-id="fb2f9-109">Maximale lengte: 32768 tekens</span><span class="sxs-lookup"><span data-stu-id="fb2f9-109">Max length: 32768 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="fb2f9-110">Ernstniveau</span><span class="sxs-lookup"><span data-stu-id="fb2f9-110">Severity level</span></span>

<span data-ttu-id="fb2f9-111">Ernstniveau traceren.</span><span class="sxs-lookup"><span data-stu-id="fb2f9-111">Trace severity level.</span></span> <span data-ttu-id="fb2f9-112">Waarde kan zijn `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="fb2f9-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="fb2f9-113">Aangepaste eigenschappen</span><span class="sxs-lookup"><span data-stu-id="fb2f9-113">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="fb2f9-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fb2f9-114">Next steps</span></span>

- <span data-ttu-id="fb2f9-115">[.NET-traceerlogboeken in Application Insights verkennen](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="fb2f9-115">[Explore .NET trace logs in Application Insights](app-insights-asp-net-trace-logs.md).</span></span>
- <span data-ttu-id="fb2f9-116">[Java in Application Insights traceerlogboeken verkennen](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="fb2f9-116">[Explore Java trace logs in Application Insights](app-insights-java-trace-logs.md).</span></span>
- <span data-ttu-id="fb2f9-117">Zie [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.</span><span class="sxs-lookup"><span data-stu-id="fb2f9-117">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="fb2f9-118">Aangepaste traceersessie telemetrie schrijven</span><span class="sxs-lookup"><span data-stu-id="fb2f9-118">Write custom trace telemetry</span></span>](app-insights-api-custom-events-metrics.md#tracktrace)
- <span data-ttu-id="fb2f9-119">Bekijk [platforms](app-insights-platforms.md) ondersteund door de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fb2f9-119">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
