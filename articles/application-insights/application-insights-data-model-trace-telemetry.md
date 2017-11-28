---
title: aaaAzure Application Insights telemetrie Data Model - Tracetelemetrie | Microsoft Docs
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
ms.openlocfilehash: dfdee958e07d57448ff41abc5cd33bfd05dac090
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="trace-telemetry-application-insights-data-model"></a><span data-ttu-id="a8dfe-103">Telemetrie traceren: Application Insights-gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="a8dfe-103">Trace telemetry: Application Insights data model</span></span>

<span data-ttu-id="a8dfe-104">Telemetrie traceren (in [Application Insights](app-insights-overview.md)) vertegenwoordigt `printf` stijl trace-instructies die tekst doorzocht.</span><span class="sxs-lookup"><span data-stu-id="a8dfe-104">Trace telemetry (in [Application Insights](app-insights-overview.md)) represents `printf` style trace statements that are text-searched.</span></span> <span data-ttu-id="a8dfe-105">`Log4Net`, `NLog`, en andere vermeldingen in logboekbestanden op basis van tekst worden vertaald naar exemplaren van dit type.</span><span class="sxs-lookup"><span data-stu-id="a8dfe-105">`Log4Net`, `NLog`, and other text-based log file entries are translated into instances of this type.</span></span> <span data-ttu-id="a8dfe-106">Hallo trace heeft geen metingen als een uitbreidbaarheid.</span><span class="sxs-lookup"><span data-stu-id="a8dfe-106">hello trace does not have measurements as an extensibility.</span></span>

## <a name="message"></a><span data-ttu-id="a8dfe-107">Bericht</span><span class="sxs-lookup"><span data-stu-id="a8dfe-107">Message</span></span>

<span data-ttu-id="a8dfe-108">Trace-bericht.</span><span class="sxs-lookup"><span data-stu-id="a8dfe-108">Trace message.</span></span>

<span data-ttu-id="a8dfe-109">Maximale lengte: 32768 tekens</span><span class="sxs-lookup"><span data-stu-id="a8dfe-109">Max length: 32768 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="a8dfe-110">Ernstniveau</span><span class="sxs-lookup"><span data-stu-id="a8dfe-110">Severity level</span></span>

<span data-ttu-id="a8dfe-111">Ernstniveau traceren.</span><span class="sxs-lookup"><span data-stu-id="a8dfe-111">Trace severity level.</span></span> <span data-ttu-id="a8dfe-112">Waarde kan zijn `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="a8dfe-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="a8dfe-113">Aangepaste eigenschappen</span><span class="sxs-lookup"><span data-stu-id="a8dfe-113">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="a8dfe-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a8dfe-114">Next steps</span></span>

- <span data-ttu-id="a8dfe-115">[.NET-traceerlogboeken in Application Insights verkennen](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a8dfe-115">[Explore .NET trace logs in Application Insights](app-insights-asp-net-trace-logs.md).</span></span>
- <span data-ttu-id="a8dfe-116">[Java in Application Insights traceerlogboeken verkennen](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a8dfe-116">[Explore Java trace logs in Application Insights](app-insights-java-trace-logs.md).</span></span>
- <span data-ttu-id="a8dfe-117">Zie [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.</span><span class="sxs-lookup"><span data-stu-id="a8dfe-117">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="a8dfe-118">Aangepaste traceersessie telemetrie schrijven</span><span class="sxs-lookup"><span data-stu-id="a8dfe-118">Write custom trace telemetry</span></span>](app-insights-api-custom-events-metrics.md#tracktrace)
- <span data-ttu-id="a8dfe-119">Bekijk [platforms](app-insights-platforms.md) ondersteund door de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a8dfe-119">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
