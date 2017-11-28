---
title: aaaMonitor Apps in Azure App Service | Microsoft Docs
description: Meer informatie over hoe toomonitor Apps in Azure App Service met behulp van Azure Portal Hallo.
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a><span data-ttu-id="ffeda-103">How to: in Azure App Service-Apps bewaken</span><span class="sxs-lookup"><span data-stu-id="ffeda-103">How to: Monitor Apps in Azure App Service</span></span>
<span data-ttu-id="ffeda-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) biedt ingebouwde bewaking functionaliteit in Hallo [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ffeda-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in hello [Azure Portal](https://portal.azure.com).</span></span>
<span data-ttu-id="ffeda-105">Dit omvat Hallo mogelijkheid tooreview **quota** en **metrische gegevens** voor een app evenals Hallo App Service-abonnement in te stellen **waarschuwingen** en zelfs **schalen** automatisch op basis van deze metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="ffeda-105">This includes hello ability tooreview **quotas** and **metrics** for an app as well as hello App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a><span data-ttu-id="ffeda-106">Understanding quota's en metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="ffeda-106">Understanding Quotas and Metrics</span></span>
### <a name="quotas"></a><span data-ttu-id="ffeda-107">Quota</span><span class="sxs-lookup"><span data-stu-id="ffeda-107">Quotas</span></span>
<span data-ttu-id="ffeda-108">Toepassingen die worden gehost in App Service zijn onderwerp toocertain *limieten* op de bronnen die ze kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ffeda-108">Applications hosted in App Service are subject toocertain *limits* on the resources they can use.</span></span> <span data-ttu-id="ffeda-109">Hallo limieten, worden gedefinieerd door Hallo **App Service-abonnement** Hallo app gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="ffeda-109">hello limits are defined by hello **App Service plan** associated with hello app.</span></span>

<span data-ttu-id="ffeda-110">Als de toepassing hello wordt gehost een **vrije** of **gedeelde** plant, en vervolgens Hallo limieten op Hallo bronnen Hallo app kunt gebruiken, zijn gedefinieerd door **quota**.</span><span class="sxs-lookup"><span data-stu-id="ffeda-110">If hello application is hosted in a **Free** or **Shared** plan, then hello limits on hello resources hello app can use are defined by **Quotas**.</span></span>

<span data-ttu-id="ffeda-111">Als de toepassing hello wordt gehost een **Basic**, **standaard** of **Premium** plant, en vervolgens Hallo limieten op Hallo bronnen kan worden gebruikt zijn ingesteld door Hallo **grootte** (Klein, normaal, groot) en **aantal exemplaar** (1, 2, 3,...) Hallo **App Service-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="ffeda-111">If hello application is hosted in a **Basic**, **Standard** or **Premium** plan, then hello limits on hello resources they can use are set by hello **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of hello **App Service plan**.</span></span>

<span data-ttu-id="ffeda-112">**Quota's** voor **vrije** of **gedeelde** apps zijn:</span><span class="sxs-lookup"><span data-stu-id="ffeda-112">**Quotas** for **Free** or **Shared** apps are:</span></span>

* <span data-ttu-id="ffeda-113">**CPU(Short)**</span><span class="sxs-lookup"><span data-stu-id="ffeda-113">**CPU(Short)**</span></span>
  * <span data-ttu-id="ffeda-114">De hoeveelheid CPU toegestaan voor deze toepassing in een interval van 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="ffeda-114">Amount of CPU allowed for this application in a 5-minute interval.</span></span> <span data-ttu-id="ffeda-115">Dit quotum wordt opnieuw ingesteld om de 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="ffeda-115">This quota re-sets every 5 minutes.</span></span>
* <span data-ttu-id="ffeda-116">**CPU(Day)**</span><span class="sxs-lookup"><span data-stu-id="ffeda-116">**CPU(Day)**</span></span>
  * <span data-ttu-id="ffeda-117">Totale hoeveelheid CPU toegestaan voor deze toepassing in een dag.</span><span class="sxs-lookup"><span data-stu-id="ffeda-117">Total amount of CPU allowed for this application in a day.</span></span> <span data-ttu-id="ffeda-118">Dit quotum wordt opnieuw ingesteld voor elke 24 uur om middernacht UTC.</span><span class="sxs-lookup"><span data-stu-id="ffeda-118">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="ffeda-119">**Geheugen**</span><span class="sxs-lookup"><span data-stu-id="ffeda-119">**Memory**</span></span>
  * <span data-ttu-id="ffeda-120">Totale hoeveelheid geheugen die is toegestaan voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="ffeda-120">Total amount of memory allowed for this application.</span></span>
* <span data-ttu-id="ffeda-121">**Bandbreedte**</span><span class="sxs-lookup"><span data-stu-id="ffeda-121">**Bandwidth**</span></span>
  * <span data-ttu-id="ffeda-122">Totale hoeveelheid bandbreedte voor uitgaande toegestaan voor deze toepassing in een dag.</span><span class="sxs-lookup"><span data-stu-id="ffeda-122">Total amount of outgoing bandwidth allowed for this application in a day.</span></span>
    <span data-ttu-id="ffeda-123">Dit quotum wordt opnieuw ingesteld voor elke 24 uur om middernacht UTC.</span><span class="sxs-lookup"><span data-stu-id="ffeda-123">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="ffeda-124">**Bestandssysteem**</span><span class="sxs-lookup"><span data-stu-id="ffeda-124">**Filesystem**</span></span>
  * <span data-ttu-id="ffeda-125">Totale hoeveelheid opslag dat is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="ffeda-125">Total amount of storage allowed.</span></span>

<span data-ttu-id="ffeda-126">alleen quotum toepasselijke tooapps gehost op Hallo **Basic**, **standaard** en **Premium** plannen is **bestandssysteem**.</span><span class="sxs-lookup"><span data-stu-id="ffeda-126">hello only quota applicable tooapps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span></span>

<span data-ttu-id="ffeda-127">Meer informatie over specifieke quota hello, limieten en functies beschikbaar zijn voor verschillende App Service-SKU's Hallo vindt u hier: [Servicelimieten voor Azure-abonnement](../azure-subscription-service-limits.md#app-service-limits)</span><span class="sxs-lookup"><span data-stu-id="ffeda-127">More information about hello specific quotas, limits and features available to hello different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span></span>

#### <a name="quota-enforcement"></a><span data-ttu-id="ffeda-128">Het afdwingen van quota</span><span class="sxs-lookup"><span data-stu-id="ffeda-128">Quota Enforcement</span></span>
<span data-ttu-id="ffeda-129">Als een toepassing in het gebruik ervan Hallo overschrijdt **CPU (korte)**, **CPU (dag)**, of **bandbreedte** quotum vervolgens Hallo toepassing wordt gestopt tot Hallo quotum opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ffeda-129">If an application in its usage exceeds hello **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then hello application will be stopped until hello quota re-sets.</span></span> <span data-ttu-id="ffeda-130">Tijdens deze periode kunnen alle inkomende aanvragen resulteert in een **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="ffeda-130">During this time, all incoming requests will result in an **HTTP 403**.</span></span>
![][http403]

<span data-ttu-id="ffeda-131">Als toepassing hello **geheugen** quotum wordt overschreden, wordt de toepassing hello instelling opnieuw is gestart.</span><span class="sxs-lookup"><span data-stu-id="ffeda-131">If hello application **memory** quota is exceeded, then hello application will be re-started.</span></span>

<span data-ttu-id="ffeda-132">Als hello **bestandssysteem** quotum wordt overschreden, en vervolgens een bewerking mislukt, dit omvat toologs schrijven schrijven.</span><span class="sxs-lookup"><span data-stu-id="ffeda-132">If hello **Filesystem** quota is exceeded, then any write operation will fail, this includes writing toologs.</span></span>

<span data-ttu-id="ffeda-133">Quota's kunnen worden verhoogd of verwijderd uit uw app door het upgraden van uw App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ffeda-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span></span>

### <a name="metrics"></a><span data-ttu-id="ffeda-134">Metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="ffeda-134">Metrics</span></span>
<span data-ttu-id="ffeda-135">**Metrische gegevens** bevatten informatie over het Hallo-app, of het gedrag van de App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ffeda-135">**Metrics** provide information about hello app, or App Service plan's behavior.</span></span>

<span data-ttu-id="ffeda-136">Voor een **toepassing**, Hallo beschikbare metrische gegevens zijn:</span><span class="sxs-lookup"><span data-stu-id="ffeda-136">For an **Application**, hello available metrics are:</span></span>

* <span data-ttu-id="ffeda-137">**Gemiddelde reactietijd**</span><span class="sxs-lookup"><span data-stu-id="ffeda-137">**Average Response Time**</span></span>
  * <span data-ttu-id="ffeda-138">Hallo gemiddelde tijd voor Hallo app tooserve aanvragen in ms.</span><span class="sxs-lookup"><span data-stu-id="ffeda-138">hello average time taken for hello app tooserve requests in ms.</span></span>
* <span data-ttu-id="ffeda-139">**Gemiddelde geheugen werkset**</span><span class="sxs-lookup"><span data-stu-id="ffeda-139">**Average memory working set**</span></span>
  * <span data-ttu-id="ffeda-140">Hallo gemiddelde hoeveelheid geheugen in MIB's die worden gebruikt door het Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="ffeda-140">hello average amount of memory in MiBs used by hello app.</span></span>
* <span data-ttu-id="ffeda-141">**CPU-tijd**</span><span class="sxs-lookup"><span data-stu-id="ffeda-141">**CPU Time**</span></span>
  * <span data-ttu-id="ffeda-142">Hallo hoeveelheid CPU in seconden verbruikt door Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="ffeda-142">hello amount of CPU in seconds consumed by hello app.</span></span> <span data-ttu-id="ffeda-143">Voor meer informatie over deze metrische Zie: [tegenover CPU-percentage van CPU-tijd](#cpu-time-vs-cpu-percentage)</span><span class="sxs-lookup"><span data-stu-id="ffeda-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span></span>
* <span data-ttu-id="ffeda-144">**Gegevens In**</span><span class="sxs-lookup"><span data-stu-id="ffeda-144">**Data In**</span></span>
  * <span data-ttu-id="ffeda-145">Hallo hoeveelheid binnenkomende bandbreedte Hallo-app in MIB's.</span><span class="sxs-lookup"><span data-stu-id="ffeda-145">hello amount of incoming bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="ffeda-146">**Gegevens uit**</span><span class="sxs-lookup"><span data-stu-id="ffeda-146">**Data Out**</span></span>
  * <span data-ttu-id="ffeda-147">Hallo hoeveelheid bandbreedte voor uitgaande verbruikt door Hallo-app in MIB's.</span><span class="sxs-lookup"><span data-stu-id="ffeda-147">hello amount of outgoing bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="ffeda-148">**HTTP-2xx**</span><span class="sxs-lookup"><span data-stu-id="ffeda-148">**Http 2xx**</span></span>
  * <span data-ttu-id="ffeda-149">Aantal aanvragen, wat resulteert in een http-statuscode > = 200 maar < 300.</span><span class="sxs-lookup"><span data-stu-id="ffeda-149">Count of requests resulting in a http status code >= 200 but < 300.</span></span>
* <span data-ttu-id="ffeda-150">**HTTP-3xx**</span><span class="sxs-lookup"><span data-stu-id="ffeda-150">**Http 3xx**</span></span>
  * <span data-ttu-id="ffeda-151">Aantal aanvragen, wat resulteert in een http-statuscode > 300 maar 400 < =.</span><span class="sxs-lookup"><span data-stu-id="ffeda-151">Count of requests resulting in a http status code >= 300 but < 400.</span></span>
* <span data-ttu-id="ffeda-152">**401 HTTP**</span><span class="sxs-lookup"><span data-stu-id="ffeda-152">**Http 401**</span></span>
  * <span data-ttu-id="ffeda-153">Het aantal aanvragen, wat resulteert in een 401 HTTP-statuscode.</span><span class="sxs-lookup"><span data-stu-id="ffeda-153">Count of requests resulting in HTTP 401 status code.</span></span>
* <span data-ttu-id="ffeda-154">**HTTP-fout 403**</span><span class="sxs-lookup"><span data-stu-id="ffeda-154">**Http 403**</span></span>
  * <span data-ttu-id="ffeda-155">Het aantal aanvragen, wat resulteert in 403 HTTP-statuscode.</span><span class="sxs-lookup"><span data-stu-id="ffeda-155">Count of requests resulting in HTTP 403 status code.</span></span>
* <span data-ttu-id="ffeda-156">**HTTP 404**</span><span class="sxs-lookup"><span data-stu-id="ffeda-156">**Http 404**</span></span>
  * <span data-ttu-id="ffeda-157">Het aantal aanvragen, wat resulteert in een HTTP 404-statuscode.</span><span class="sxs-lookup"><span data-stu-id="ffeda-157">Count of requests resulting in HTTP 404 status code.</span></span>
* <span data-ttu-id="ffeda-158">**HTTP 406**</span><span class="sxs-lookup"><span data-stu-id="ffeda-158">**Http 406**</span></span>
  * <span data-ttu-id="ffeda-159">Het aantal aanvragen, wat resulteert in 406 HTTP-statuscode.</span><span class="sxs-lookup"><span data-stu-id="ffeda-159">Count of requests resulting in HTTP 406 status code.</span></span>
* <span data-ttu-id="ffeda-160">**HTTP-4xx**</span><span class="sxs-lookup"><span data-stu-id="ffeda-160">**Http 4xx**</span></span>
  * <span data-ttu-id="ffeda-161">Aantal aanvragen, wat resulteert in een http-statuscode > = 400 maar < 500.</span><span class="sxs-lookup"><span data-stu-id="ffeda-161">Count of requests resulting in a http status code >= 400 but < 500.</span></span>
* <span data-ttu-id="ffeda-162">**HTTP-Server-fouten**</span><span class="sxs-lookup"><span data-stu-id="ffeda-162">**Http Server Errors**</span></span>
  * <span data-ttu-id="ffeda-163">Aantal aanvragen, wat resulteert in een http-statuscode > = 500 maar < 600.</span><span class="sxs-lookup"><span data-stu-id="ffeda-163">Count of requests resulting in a http status code >= 500 but < 600.</span></span>
* <span data-ttu-id="ffeda-164">**Geheugen-werkset**</span><span class="sxs-lookup"><span data-stu-id="ffeda-164">**Memory working set**</span></span>
  * <span data-ttu-id="ffeda-165">Huidige hoeveelheid geheugen die wordt gebruikt door de app Hallo in MIB's.</span><span class="sxs-lookup"><span data-stu-id="ffeda-165">Current amount of memory used by hello app in MiBs.</span></span>
* <span data-ttu-id="ffeda-166">**Aanvragen**</span><span class="sxs-lookup"><span data-stu-id="ffeda-166">**Requests**</span></span>
  * <span data-ttu-id="ffeda-167">Totaal aantal aanvragen ongeacht hun resulterende HTTP-statuscode.</span><span class="sxs-lookup"><span data-stu-id="ffeda-167">Total number of requests regardless of their resulting HTTP status code.</span></span>

<span data-ttu-id="ffeda-168">Voor een **App Service-abonnement**, Hallo beschikbare metrische gegevens zijn:</span><span class="sxs-lookup"><span data-stu-id="ffeda-168">For an **App Service plan**, hello available metrics are:</span></span>

> [!NOTE]
> <span data-ttu-id="ffeda-169">App Service plan metrische gegevens zijn alleen beschikbaar voor abonnementen in **Basic**, **standaard** en **Premium** SKU.</span><span class="sxs-lookup"><span data-stu-id="ffeda-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span></span>
> 
> 

* <span data-ttu-id="ffeda-170">**CPU-Percentage**</span><span class="sxs-lookup"><span data-stu-id="ffeda-170">**CPU Percentage**</span></span>
  * <span data-ttu-id="ffeda-171">Hallo gemiddelde CPU-gebruik over alle exemplaren van Hallo plan.</span><span class="sxs-lookup"><span data-stu-id="ffeda-171">hello average CPU used across all instances of hello plan.</span></span>
* <span data-ttu-id="ffeda-172">**Geheugenpercentage**</span><span class="sxs-lookup"><span data-stu-id="ffeda-172">**Memory Percentage**</span></span>
  * <span data-ttu-id="ffeda-173">Hallo gemiddelde geheugen gebruikt in alle exemplaren van Hallo plan.</span><span class="sxs-lookup"><span data-stu-id="ffeda-173">hello average memory used across all instances of hello plan.</span></span>
* <span data-ttu-id="ffeda-174">**Gegevens In**</span><span class="sxs-lookup"><span data-stu-id="ffeda-174">**Data In**</span></span>
  * <span data-ttu-id="ffeda-175">Hallo gemiddelde binnenkomende bandbreedte die wordt gebruikt in alle exemplaren van Hallo plan.</span><span class="sxs-lookup"><span data-stu-id="ffeda-175">hello average incoming bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="ffeda-176">**Gegevens uit**</span><span class="sxs-lookup"><span data-stu-id="ffeda-176">**Data Out**</span></span>
  * <span data-ttu-id="ffeda-177">Hallo gemiddelde bandbreedte die wordt gebruikt in alle exemplaren van Hallo plan uitgaande.</span><span class="sxs-lookup"><span data-stu-id="ffeda-177">hello average outgoing bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="ffeda-178">**Wachtrijlengte voor schijf**</span><span class="sxs-lookup"><span data-stu-id="ffeda-178">**Disk Queue Length**</span></span>
  * <span data-ttu-id="ffeda-179">Hallo gemiddeld aantal lees door en schrijfaanvragen die in de wachtrij zijn geplaatst in de opslag.</span><span class="sxs-lookup"><span data-stu-id="ffeda-179">hello average number of both read and write requests that were queued on storage.</span></span> <span data-ttu-id="ffeda-180">Een hoge wachtrijlengte is een indicatie van een toepassing die mogelijk vanwege tooexcessive schijf-i/o vertragen.</span><span class="sxs-lookup"><span data-stu-id="ffeda-180">A high disk queue length is an indication of an application that might be slowing down due tooexcessive disk I/O.</span></span>
* <span data-ttu-id="ffeda-181">**HTTP-wachtrijlengte**</span><span class="sxs-lookup"><span data-stu-id="ffeda-181">**Http Queue Length**</span></span>
  * <span data-ttu-id="ffeda-182">Hallo gemiddelde aantal HTTP-aanvragen dat toosit op Hallo wachtrij had voordat het wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="ffeda-182">hello average number of HTTP requests that had toosit on hello queue before being fulfilled.</span></span> <span data-ttu-id="ffeda-183">Een hoog of toenemende HTTP-wachtrijlengte is een symptoom van een plan zwaar wordt belast.</span><span class="sxs-lookup"><span data-stu-id="ffeda-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span></span>

### <a name="cpu-time-vs-cpu-percentage"></a><span data-ttu-id="ffeda-184">Vs CPU-percentage van CPU-tijd</span><span class="sxs-lookup"><span data-stu-id="ffeda-184">CPU time vs CPU percentage</span></span>
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

<span data-ttu-id="ffeda-185">Er zijn 2 metrische gegevens die overeenkomen met het CPU-gebruik.</span><span class="sxs-lookup"><span data-stu-id="ffeda-185">There are 2 metrics that reflect CPU usage.</span></span> <span data-ttu-id="ffeda-186">**CPU-tijd** en **CPU-percentage**</span><span class="sxs-lookup"><span data-stu-id="ffeda-186">**CPU time** and **CPU percentage**</span></span>

<span data-ttu-id="ffeda-187">**CPU-tijd** is nuttig voor apps die worden gehost **vrije** of **gedeelde** plannen omdat een van hun quota is gedefinieerd in CPU minuten door Hallo app gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ffeda-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by hello app.</span></span>

<span data-ttu-id="ffeda-188">**CPU-percentage** op Hallo daarentegen is nuttig voor apps die worden gehost **basic**, **standaard** en **premium** plannen omdat ze kunnen worden uitgebreid en deze metrische gegevens is een goede indicatie van Hallo algemene gebruik in alle exemplaren.</span><span class="sxs-lookup"><span data-stu-id="ffeda-188">**CPU percentage** on hello other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of hello overall usage across all instances.</span></span>

## <a name="metrics-granularity-and-retention-policy"></a><span data-ttu-id="ffeda-189">Samenvattingen van de metrische gegevens en bewaarbeleid</span><span class="sxs-lookup"><span data-stu-id="ffeda-189">Metrics Granularity and Retention Policy</span></span>
<span data-ttu-id="ffeda-190">Metrische gegevens voor een toepassing en de app service-abonnement zijn geregistreerd en geaggregeerd door Hallo service Hello granulaties en bewaarbeleid te volgen:</span><span class="sxs-lookup"><span data-stu-id="ffeda-190">Metrics for an application and app service plan are logged and aggregated by hello service with hello following granularities and retention policies:</span></span>

* <span data-ttu-id="ffeda-191">**Minuut** granulatie metrische gegevens worden bewaard voor **48 uur**</span><span class="sxs-lookup"><span data-stu-id="ffeda-191">**Minute** granularity metrics are retained for **48 hours**</span></span>
* <span data-ttu-id="ffeda-192">**Uur** granulatie metrische gegevens worden bewaard voor **30 dagen**</span><span class="sxs-lookup"><span data-stu-id="ffeda-192">**Hour** granularity metrics are retained for **30 days**</span></span>
* <span data-ttu-id="ffeda-193">**Dag** granulatie metrische gegevens worden bewaard voor **90 dagen**</span><span class="sxs-lookup"><span data-stu-id="ffeda-193">**Day** granularity metrics are retained for **90 days**</span></span>

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a><span data-ttu-id="ffeda-194">Quota's en metrische gegevens controleren in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="ffeda-194">Monitoring Quotas and Metrics in hello Azure Portal.</span></span>
<span data-ttu-id="ffeda-195">U kunt de status Hallo Hallo verschillende bekijken **quota** en **metrische gegevens** die invloed hebben op een toepassing in Hallo [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ffeda-195">You can review hello status of hello different **quotas** and **metrics** affecting an application in hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="ffeda-196">![][quotas]
**Quota's** vindt u onder Instellingen >**quota**.</span><span class="sxs-lookup"><span data-stu-id="ffeda-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span></span> <span data-ttu-id="ffeda-197">Hallo UX kunt u bekijken: de naam van de quota's (1) hello, (2) het interval opnieuw instellen, (3) de huidige limiet en (4) de huidige waarde.</span><span class="sxs-lookup"><span data-stu-id="ffeda-197">hello UX allows you to review: (1) hello quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span></span>

<span data-ttu-id="ffeda-198">![][metrics]
**Metrische gegevens** toegang rechtstreeks vanaf de resourceblade Hallo kan zijn.</span><span class="sxs-lookup"><span data-stu-id="ffeda-198">![][metrics]
**Metrics** can be access directly from hello resource blade.</span></span> <span data-ttu-id="ffeda-199">U kunt ook aanpassen Hallo grafiek door: (1) **klikt u op** op en selecteert u (2) **grafiek bewerken**.</span><span class="sxs-lookup"><span data-stu-id="ffeda-199">You can also customize hello chart by: (1) **click** on it, and select (2) **edit chart**.</span></span>
<span data-ttu-id="ffeda-200">Hier kunt u hello (3) **tijdsbereik**, (4) **grafiektype**, en 5, **metrische gegevens** toodisplay.</span><span class="sxs-lookup"><span data-stu-id="ffeda-200">From here you can change hello (3) **time range**, (4) **chart type**, and (5) **metrics** toodisplay.</span></span>  

<span data-ttu-id="ffeda-201">U kunt meer informatie over metrische gegevens hier: [service metrische gegevens controleren](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="ffeda-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

## <a name="alerts-and-autoscale"></a><span data-ttu-id="ffeda-202">Waarschuwingen en voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="ffeda-202">Alerts and Autoscale</span></span>
<span data-ttu-id="ffeda-203">Metrische gegevens voor een App of een App Service-plan kan worden aangesloten tooalerts, toolearn meer over deze, Zie [ontvangen van meldingen van waarschuwingen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="ffeda-203">Metrics for an App or App Service plan can be hooked up tooalerts, toolearn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="ffeda-204">App Service-apps die zijn gehost in basic, standard of premium App Service-abonnementen ondersteunen **automatisch schalen**.</span><span class="sxs-lookup"><span data-stu-id="ffeda-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span></span> <span data-ttu-id="ffeda-205">Hiermee kunt u tooconfigure regels die de App Service plan metrische gegevens controleren en kunnen vergroten of verkleinen Hallo exemplaren verstrekken aanvullende bronnen die nodig is of opslaan money wanneer de toepassing hello te veel inrichten.</span><span class="sxs-lookup"><span data-stu-id="ffeda-205">This allows you tooconfigure rules that monitor the App Service plan metrics and can increase or decrease hello instance count providing additional resources as needed, or saving money when hello application is over-provision.</span></span> <span data-ttu-id="ffeda-206">U kunt meer informatie over automatisch schalen hier: [hoe tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) en hier [Best practices voor het bewaken van de Azure-automatisch schalen](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="ffeda-206">You can learn more about auto scale here: [How tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span></span>

> [!NOTE]
> <span data-ttu-id="ffeda-207">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="ffeda-207">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ffeda-208">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="ffeda-208">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="ffeda-209">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="ffeda-209">What's changed</span></span>
* <span data-ttu-id="ffeda-210">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="ffeda-210">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
