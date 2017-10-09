---
title: aaaAzure Application Insights telemetrie Data Model - gebeurtenis telemetrie | Microsoft Docs
description: Application Insights-gegevensmodel voor telemetrie van gebeurtenis
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
ms.openlocfilehash: cd7dc3c5f4f3df22b7a52ee79fcad566a27a9f4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-telemetry-application-insights-data-model"></a><span data-ttu-id="364b5-103">Gebeurtenis telemetrie: Application Insights-gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="364b5-103">Event telemetry: Application Insights data model</span></span>

<span data-ttu-id="364b5-104">Kunt u de gebeurtenis telemetrie-items maken (in [Application Insights](app-insights-overview.md)) toorepresent een gebeurtenis die is opgetreden in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="364b5-104">You can create event telemetry items (in [Application Insights](app-insights-overview.md)) toorepresent an event that occurred in your application.</span></span> <span data-ttu-id="364b5-105">Het is doorgaans een gebruikersinteractie zoals knop klikt u op of afhandeling bestellen.</span><span class="sxs-lookup"><span data-stu-id="364b5-105">Typically it is a user interaction such as button click or order checkout.</span></span> <span data-ttu-id="364b5-106">Het kan ook een gebeurtenis van de levenscyclus van de toepassing zoals configuratie of de initialisatie van de update zijn.</span><span class="sxs-lookup"><span data-stu-id="364b5-106">It can also be an application life cycle event like initialization or configuration update.</span></span> 

<span data-ttu-id="364b5-107">Semantisch, gebeurtenissen al dan niet gecorreleerde toorequests.</span><span class="sxs-lookup"><span data-stu-id="364b5-107">Semantically, events may or may not be correlated toorequests.</span></span> <span data-ttu-id="364b5-108">Gebeurtenis telemetrie is echter belangrijker dan de wijzigingsaanvragen of traceringen als goed gebruikt.</span><span class="sxs-lookup"><span data-stu-id="364b5-108">However, if used properly, event telemetry is more important than requests or traces.</span></span> <span data-ttu-id="364b5-109">Gebeurtenissen vertegenwoordigen de zakelijke Telemetrie en moet een onderwerpnaam tooseparate minder agressieve [steekproeven](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="364b5-109">Events represent business telemetry and should be a subject tooseparate, less aggressive [sampling](app-insights-api-filtering-sampling.md).</span></span>

## <a name="name"></a><span data-ttu-id="364b5-110">Naam</span><span class="sxs-lookup"><span data-stu-id="364b5-110">Name</span></span>

<span data-ttu-id="364b5-111">De naam van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="364b5-111">Event name.</span></span> <span data-ttu-id="364b5-112">de juiste groepering tooallow en nuttig metrische gegevens, beperkt uw toepassing zodat er een klein aantal afzonderlijke gebeurtenisnamen gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="364b5-112">tooallow proper grouping and useful metrics, restrict your application so that it generates a small number of separate event names.</span></span> <span data-ttu-id="364b5-113">Bijvoorbeeld, gebruik niet een afzonderlijke naam voor elk gegenereerde exemplaar van een gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="364b5-113">For example, don't use a separate name for each generated instance of an event.</span></span>

<span data-ttu-id="364b5-114">Maximale lengte: 512 tekens</span><span class="sxs-lookup"><span data-stu-id="364b5-114">Max length: 512 characters</span></span>

## <a name="custom-properties"></a><span data-ttu-id="364b5-115">Aangepaste eigenschappen</span><span class="sxs-lookup"><span data-stu-id="364b5-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="364b5-116">Aangepaste metingen</span><span class="sxs-lookup"><span data-stu-id="364b5-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="364b5-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="364b5-117">Next steps</span></span>

- <span data-ttu-id="364b5-118">Zie [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.</span><span class="sxs-lookup"><span data-stu-id="364b5-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="364b5-119">Aangepaste gebeurtenis telemetrie schrijven</span><span class="sxs-lookup"><span data-stu-id="364b5-119">Write custom event telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackevent)
- <span data-ttu-id="364b5-120">Bekijk [platforms](app-insights-platforms.md) ondersteund door de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="364b5-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
