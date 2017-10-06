---
title: cachegedrag van Azure CDN met queryreeksen - Premium aaaControl | Microsoft Docs
description: Azure CDN-queryreeks opslaan in cache bepaalt hoe bestanden toobe worden wanneer ze queryreeksen bevatten in de cache opgeslagen.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="8dab2-103">Besturingselement Azure CDN cachegedrag met queryreeksen - Premium</span><span class="sxs-lookup"><span data-stu-id="8dab2-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8dab2-104">Standard</span><span class="sxs-lookup"><span data-stu-id="8dab2-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="8dab2-105">Azure CDN Premium van Verizon</span><span class="sxs-lookup"><span data-stu-id="8dab2-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="8dab2-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8dab2-106">Overview</span></span>
<span data-ttu-id="8dab2-107">Queryreeks opslaan in cache bepaalt hoe bestanden toobe worden wanneer ze queryreeksen bevatten in de cache opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8dab2-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8dab2-108">Hallo Standard en Premium-CDN-producten bieden Hallo dezelfde tekenreeks in het cachegeheugen functionaliteit query, maar het Hallo-gebruikersinterface verschilt.</span><span class="sxs-lookup"><span data-stu-id="8dab2-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="8dab2-109">Dit document beschrijft Hallo-interface voor **Azure CDN Premium van Verizon**.</span><span class="sxs-lookup"><span data-stu-id="8dab2-109">This document describes hello interface for **Azure CDN Premium from Verizon**.</span></span>  <span data-ttu-id="8dab2-110">Voor deze query opslaan in cache met **Azure CDN Standard van Akamai** en **Azure CDN Standard van Verizon**, Zie [beheren cachegedrag van CDN aanvragen met querytekenreeksen](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="8dab2-110">For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).</span></span>
> 
> 

<span data-ttu-id="8dab2-111">Drie beschikbare modi zijn beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="8dab2-111">Three modes are available:</span></span>

* <span data-ttu-id="8dab2-112">**Standard-cache**: dit is de standaardmodus Hallo.</span><span class="sxs-lookup"><span data-stu-id="8dab2-112">**standard-cache**:  This is hello default mode.</span></span>  <span data-ttu-id="8dab2-113">op de eerste aanvraag Hallo en cache Hallo asset geeft Hallo CDN edge-knooppunt Hallo queryreeks vanuit Hallo aanvrager toohello oorsprong.</span><span class="sxs-lookup"><span data-stu-id="8dab2-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="8dab2-114">Alle volgende aanvragen voor de activa die worden aangeboden via edge-knooppunt Hallo negeert Hallo queryreeks totdat Hallo in de cache asset verloopt.</span><span class="sxs-lookup"><span data-stu-id="8dab2-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="8dab2-115">**Er is geen cache**: In deze modus kan aanvragen met querytekenreeksen in cache zijn niet opgeslagen op Hallo CDN edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="8dab2-115">**no-cache**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="8dab2-116">Hallo edge-knooppunt Hallo asset haalt rechtstreeks vanuit de oorsprong Hallo en geeft deze door de aanvrager toohello bij elke aanvraag.</span><span class="sxs-lookup"><span data-stu-id="8dab2-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="8dab2-117">**unieke cache**: in deze modus wordt elke aanvraag met een queryreeks beschouwd als een unieke activum met een eigen cache.</span><span class="sxs-lookup"><span data-stu-id="8dab2-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="8dab2-118">Bijvoorbeeld, Hallo reactie van de oorsprong Hallo voor een aanvraag voor *foo.ashx?q=bar* zou worden in de cache opgeslagen op Hallo edge-knooppunt en voor daaropvolgende caches met die dezelfde querytekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="8dab2-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="8dab2-119">Een aanvraag voor *foo.ashx?q=somethingelse* zou in de cache opgeslagen als een afzonderlijk actief met een eigen toolive tijd.</span><span class="sxs-lookup"><span data-stu-id="8dab2-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="8dab2-120">Het wijzigen van de queryreeks opslaan in cache-instellingen voor premium-CDN-profielen</span><span class="sxs-lookup"><span data-stu-id="8dab2-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="8dab2-121">Blade voor Hallo CDN-profiel, klik op Hallo **beheren** knop.</span><span class="sxs-lookup"><span data-stu-id="8dab2-121">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Knop blade CDN-profiel beheren](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="8dab2-123">Hallo CDN-beheerportal geopend.</span><span class="sxs-lookup"><span data-stu-id="8dab2-123">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="8dab2-124">Houd de muis boven Hallo **HTTP grote** tabblad en houd de muis boven Hallo **Cache-instellingen** doel.</span><span class="sxs-lookup"><span data-stu-id="8dab2-124">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="8dab2-125">Klik op **queryreeks Caching**.</span><span class="sxs-lookup"><span data-stu-id="8dab2-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="8dab2-126">Queryreeks cache-opties worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8dab2-126">Query string caching options are displayed.</span></span>
   
    ![CDN-queryreeks cacheopties](./media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="8dab2-128">Nadat u hebt geselecteerd, klikt u op Hallo **Update** knop.</span><span class="sxs-lookup"><span data-stu-id="8dab2-128">After making your selection, click hello **Update** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8dab2-129">Hallo instellingen wijzigingen zijn mogelijk niet direct weergegeven als het duurt voor Hallo registratie toopropagate via Hallo CDN.</span><span class="sxs-lookup"><span data-stu-id="8dab2-129">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="8dab2-130">Profielen van <b>Azure CDN van Verizon</b> worden doorgaans binnen 90 minuten doorgegeven, maar in sommige gevallen kan dit langer duren.</span><span class="sxs-lookup"><span data-stu-id="8dab2-130">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

