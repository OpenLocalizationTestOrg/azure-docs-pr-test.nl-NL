---
title: cachegedrag van Azure CDN met queryreeksen aaaControl | Microsoft Docs
description: Azure CDN-queryreeks opslaan in cache bepaalt hoe bestanden toobe worden wanneer ze queryreeksen bevatten in de cache opgeslagen.
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
ms.openlocfilehash: e7a138b2decec624a29eb703ad9a291d19c44ee8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a><span data-ttu-id="74639-103">Besturingselement Azure CDN cachegedrag met queryreeksen</span><span class="sxs-lookup"><span data-stu-id="74639-103">Control Azure CDN caching behavior with query strings</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="74639-104">Standard</span><span class="sxs-lookup"><span data-stu-id="74639-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="74639-105">Azure CDN Premium van Verizon</span><span class="sxs-lookup"><span data-stu-id="74639-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="74639-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="74639-106">Overview</span></span>
<span data-ttu-id="74639-107">Queryreeks opslaan in cache bepaalt hoe bestanden toobe worden wanneer ze queryreeksen bevatten in de cache opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="74639-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74639-108">Hallo Standard en Premium-CDN-producten bieden Hallo dezelfde tekenreeks in het cachegeheugen functionaliteit query, maar het Hallo-gebruikersinterface verschilt.</span><span class="sxs-lookup"><span data-stu-id="74639-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="74639-109">Dit document beschrijft Hallo-interface voor **Azure CDN Standard van Akamai** en **Azure CDN Standard van Verizon**.</span><span class="sxs-lookup"><span data-stu-id="74639-109">This document describes hello interface for **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**.</span></span>  <span data-ttu-id="74639-110">Voor deze query opslaan in cache met **Azure CDN Premium van Verizon**, Zie [beheren cachegedrag van CDN aanvragen met querytekenreeksen - Premium](cdn-query-string-premium.md).</span><span class="sxs-lookup"><span data-stu-id="74639-110">For query string caching with **Azure CDN Premium from Verizon**, see [Controlling caching behavior of CDN requests with query strings - Premium](cdn-query-string-premium.md).</span></span>
> 
> 

<span data-ttu-id="74639-111">Drie beschikbare modi zijn beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="74639-111">Three modes are available:</span></span>

* <span data-ttu-id="74639-112">**Querytekenreeksen negeren**: dit is de standaardmodus Hallo.</span><span class="sxs-lookup"><span data-stu-id="74639-112">**Ignore query strings**:  This is hello default mode.</span></span>  <span data-ttu-id="74639-113">op de eerste aanvraag Hallo en cache Hallo asset geeft Hallo CDN edge-knooppunt Hallo queryreeks vanuit Hallo aanvrager toohello oorsprong.</span><span class="sxs-lookup"><span data-stu-id="74639-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="74639-114">Alle volgende aanvragen voor de activa die worden aangeboden via edge-knooppunt Hallo negeert Hallo queryreeks totdat Hallo in de cache asset verloopt.</span><span class="sxs-lookup"><span data-stu-id="74639-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="74639-115">**Overslaan voor URL's met querytekenreeksen**: In deze modus kan aanvragen met querytekenreeksen in cache zijn niet opgeslagen op Hallo CDN edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="74639-115">**Bypass caching for URL with query strings**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="74639-116">Hallo edge-knooppunt Hallo asset haalt rechtstreeks vanuit de oorsprong Hallo en geeft deze door de aanvrager toohello bij elke aanvraag.</span><span class="sxs-lookup"><span data-stu-id="74639-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="74639-117">**Elke unieke URL in de cache**: in deze modus wordt elke aanvraag met een queryreeks beschouwd als een unieke activum met een eigen cache.</span><span class="sxs-lookup"><span data-stu-id="74639-117">**Cache every unique URL**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="74639-118">Bijvoorbeeld, Hallo reactie van de oorsprong Hallo voor een aanvraag voor *foo.ashx?q=bar* zou worden in de cache opgeslagen op Hallo edge-knooppunt en voor daaropvolgende caches met die dezelfde querytekenreeks geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="74639-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="74639-119">Een aanvraag voor *foo.ashx?q=somethingelse* zou in de cache opgeslagen als een afzonderlijk actief met een eigen toolive tijd.</span><span class="sxs-lookup"><span data-stu-id="74639-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="74639-120">Het wijzigen van de queryreeks opslaan in cache-instellingen voor standaard CDN-profielen</span><span class="sxs-lookup"><span data-stu-id="74639-120">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="74639-121">Blade voor Hallo CDN-profiel, klik op Hallo gewenst toomanage CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="74639-121">From hello CDN profile blade, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![CDN-profiel blade-eindpunten](./media/cdn-query-string/cdn-endpoints.png)
   
    <span data-ttu-id="74639-123">Hallo CDN-eindpunt blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="74639-123">hello CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="74639-124">Klik op Hallo **configureren** knop.</span><span class="sxs-lookup"><span data-stu-id="74639-124">Click hello **Configure** button.</span></span>
   
    ![Knop blade CDN-profiel beheren](./media/cdn-query-string/cdn-config-btn.png)
   
    <span data-ttu-id="74639-126">Hallo CDN configuratie blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="74639-126">hello CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="74639-127">Selecteer een instelling in Hallo **queryreeks cachegedrag** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="74639-127">Select a setting from hello **Query string caching behavior** dropdown.</span></span>
   
    ![CDN-queryreeks cacheopties](./media/cdn-query-string/cdn-query-string.png)
4. <span data-ttu-id="74639-129">Nadat u hebt geselecteerd, klikt u op Hallo **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="74639-129">After making your selection, click hello **Save** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74639-130">Hallo instellingen wijzigingen zijn mogelijk niet direct weergegeven als het duurt voor Hallo registratie toopropagate via Hallo CDN.</span><span class="sxs-lookup"><span data-stu-id="74639-130">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="74639-131">Profielen van <b>Azure CDN van Akamai</b> worden doorgaans binnen één minuut doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="74639-131">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="74639-132">Profielen van <b>Azure CDN van Verizon</b> worden doorgaans binnen 90 minuten doorgegeven, maar in sommige gevallen kan dit langer duren.</span><span class="sxs-lookup"><span data-stu-id="74639-132">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

