---
title: Beheren van Azure CDN cachegedrag met queryreeksen | Microsoft Docs
description: Azure CDN-queryreeks opslaan in cache bepaalt hoe bestanden worden in de cache worden opgeslagen wanneer ze queryreeksen bevatten.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 8d79626fa8516f226a82d3dac693c2033904c91d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a><span data-ttu-id="9c2b3-103">Besturingselement Azure CDN cachegedrag met queryreeksen</span><span class="sxs-lookup"><span data-stu-id="9c2b3-103">Control Azure CDN caching behavior with query strings</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c2b3-104">Standard</span><span class="sxs-lookup"><span data-stu-id="9c2b3-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="9c2b3-105">Azure CDN Premium van Verizon</span><span class="sxs-lookup"><span data-stu-id="9c2b3-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="9c2b3-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="9c2b3-106">Overview</span></span>
<span data-ttu-id="9c2b3-107">Queryreeks opslaan in cache bepaalt hoe bestanden worden in de cache worden opgeslagen wanneer ze queryreeksen bevatten.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-107">Query string caching controls how files are to be cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c2b3-108">De Standard en Premium-CDN-producten, bieden dezelfde querytekenreeks cache-functionaliteit, maar de gebruikersinterface verschilt.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-108">The Standard and Premium CDN products provide the same query string caching functionality, but the user interface differs.</span></span>  <span data-ttu-id="9c2b3-109">Dit document beschrijft de interface voor **Azure CDN Standard van Akamai** en **Azure CDN Standard van Verizon**.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-109">This document describes the interface for **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**.</span></span>  <span data-ttu-id="9c2b3-110">Voor deze query opslaan in cache met **Azure CDN Premium van Verizon**, Zie [beheren cachegedrag van CDN aanvragen met querytekenreeksen - Premium](cdn-query-string-premium.md).</span><span class="sxs-lookup"><span data-stu-id="9c2b3-110">For query string caching with **Azure CDN Premium from Verizon**, see [Controlling caching behavior of CDN requests with query strings - Premium](cdn-query-string-premium.md).</span></span>
> 
> 

<span data-ttu-id="9c2b3-111">Drie beschikbare modi zijn beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="9c2b3-111">Three modes are available:</span></span>

* <span data-ttu-id="9c2b3-112">**Querytekenreeksen negeren**: dit is de standaardmodus.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-112">**Ignore query strings**:  This is the default mode.</span></span>  <span data-ttu-id="9c2b3-113">Het CDN edge-knooppunt geeft de queryreeks van de aanvrager aan de oorsprong op de eerste aanvraag en cache de asset.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-113">The CDN edge node will pass the query string from the requestor to the origin on the first request and cache the asset.</span></span>  <span data-ttu-id="9c2b3-114">Alle volgende aanvragen voor de activa die worden aangeboden via het edge-knooppunt kan de query-tekenreeks worden genegeerd totdat de activa in de cache verloopt.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-114">All subsequent requests for that asset that are served from the edge node will ignore the query string until the cached asset expires.</span></span>
* <span data-ttu-id="9c2b3-115">**Overslaan voor URL's met querytekenreeksen**: In deze modus kan aanvragen met queryreeksen zijn niet in cache opgeslagen op de edge-knooppunt van het CDN.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-115">**Bypass caching for URL with query strings**:  In this mode, requests with query strings are not cached at the CDN edge node.</span></span>  <span data-ttu-id="9c2b3-116">Het edge-knooppunt ophalen van de asset rechtstreeks vanuit de oorsprong en wordt doorgegeven aan de aanvrager aan elke aanvraag.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-116">The edge node retrieves the asset directly from the origin and passes it to the requestor with each request.</span></span>
* <span data-ttu-id="9c2b3-117">**Elke unieke URL in de cache**: in deze modus wordt elke aanvraag met een queryreeks beschouwd als een unieke activum met een eigen cache.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-117">**Cache every unique URL**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="9c2b3-118">Bijvoorbeeld: de reactie van de oorsprong van een aanvraag voor *foo.ashx?q=bar* zou worden in de cache opgeslagen op de edge-knooppunt en voor daaropvolgende caches met die dezelfde querytekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-118">For example, the response from the origin for a request for *foo.ashx?q=bar* would be cached at the edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="9c2b3-119">Een aanvraag voor *foo.ashx?q=somethingelse* zou in de cache opgeslagen als een afzonderlijk actief met een eigen tijd levensduur.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time to live.</span></span>

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="9c2b3-120">Het wijzigen van de queryreeks opslaan in cache-instellingen voor standaard CDN-profielen</span><span class="sxs-lookup"><span data-stu-id="9c2b3-120">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="9c2b3-121">Klik in de blade CDN-profiel op het CDN-eindpunt dat u wilt beheren.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-121">From the CDN profile blade, click the CDN endpoint you wish to manage.</span></span>
   
    ![CDN-profiel blade-eindpunten](./media/cdn-query-string/cdn-endpoints.png)
   
    <span data-ttu-id="9c2b3-123">De blade CDN-eindpunt wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-123">The CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="9c2b3-124">Klik op de **configureren** knop.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-124">Click the **Configure** button.</span></span>
   
    ![Knop blade CDN-profiel beheren](./media/cdn-query-string/cdn-config-btn.png)
   
    <span data-ttu-id="9c2b3-126">De configuratie van CDN-blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-126">The CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="9c2b3-127">Selecteer een instelling van de **queryreeks cachegedrag** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-127">Select a setting from the **Query string caching behavior** dropdown.</span></span>
   
    ![CDN-queryreeks cacheopties](./media/cdn-query-string/cdn-query-string.png)
4. <span data-ttu-id="9c2b3-129">Nadat u hebt geselecteerd, klikt u op de **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-129">After making your selection, click the **Save** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c2b3-130">Wijzigingen in de instellingen zijn mogelijk niet direct weergegeven als het duurt om de registratie te geven in CDN.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-130">The settings changes may not be immediately visible, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="9c2b3-131">Profielen van <b>Azure CDN van Akamai</b> worden doorgaans binnen één minuut doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-131">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="9c2b3-132">Profielen van <b>Azure CDN van Verizon</b> worden doorgaans binnen 90 minuten doorgegeven, maar in sommige gevallen kan dit langer duren.</span><span class="sxs-lookup"><span data-stu-id="9c2b3-132">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

