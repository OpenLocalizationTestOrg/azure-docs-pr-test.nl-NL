---
title: Vooraf laden van assets op een Azure CDN-eindpunt | Microsoft Docs
description: Informatie over het vooraf laden van inhoud in cache op een Azure CDN-eindpunt.
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 1f2dcd9a91bb6e883cbef06373c1acd98bf8d45f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="050f3-103">Vooraf assets op een Azure CDN-eindpunt laden</span><span class="sxs-lookup"><span data-stu-id="050f3-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="050f3-104">Standaard activa eerst in de cache opgeslagen als ze worden aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="050f3-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="050f3-105">Dit betekent dat de eerste aanvraag vanuit elke regio kan het langer duren, omdat de randservers niet de inhoud in cache en moet de aanvraag doorsturen naar de oorspronkelijke server.</span><span class="sxs-lookup"><span data-stu-id="050f3-105">This means that the first request from each region may take longer, since the edge servers will not have the content cached and will need to forward the request to the origin server.</span></span> <span data-ttu-id="050f3-106">Vooraf laden van inhoud, wordt dit eerste treffers latentie voorkomen.</span><span class="sxs-lookup"><span data-stu-id="050f3-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="050f3-107">Naast het bieden van een betere klantervaring vooraf laden van uw assets in de cache kan ook leiden tot minder netwerkverkeer op de bronserver.</span><span class="sxs-lookup"><span data-stu-id="050f3-107">In addition to providing a better customer experience, pre-loading your cached assets can also reduce network traffic on the origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="050f3-108">Vooraf laden van de activa is handig voor grote gebeurtenissen of inhoud die tegelijkertijd beschikbaar voor een groot aantal gebruikers, zoals een nieuwe film release of een software-update.</span><span class="sxs-lookup"><span data-stu-id="050f3-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available to a large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="050f3-109">Deze zelfstudie leert u de inhoud op alle knooppunten van Azure CDN edge cache vooraf laden.</span><span class="sxs-lookup"><span data-stu-id="050f3-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="050f3-110">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="050f3-110">Walkthrough</span></span>
1. <span data-ttu-id="050f3-111">In de [Azure Portal](https://portal.azure.com), blader naar de CDN-profiel met het eindpunt dat u wilt vooraf laden.</span><span class="sxs-lookup"><span data-stu-id="050f3-111">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to pre-load.</span></span>  <span data-ttu-id="050f3-112">De profiel-blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="050f3-112">The profile blade opens.</span></span>
2. <span data-ttu-id="050f3-113">Klik op het eindpunt in de lijst.</span><span class="sxs-lookup"><span data-stu-id="050f3-113">Click the endpoint in the list.</span></span>  <span data-ttu-id="050f3-114">De eindpunt-blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="050f3-114">The endpoint blade opens.</span></span>
3. <span data-ttu-id="050f3-115">Klik op de knop laden op de blade CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="050f3-115">From the CDN endpoint blade, click the load button.</span></span>
   
    ![Blade CDN-eindpunt](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="050f3-117">De Load-blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="050f3-117">The Load blade opens.</span></span>
   
    ![Load-blade CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="050f3-119">Geef het volledige pad van elk actief die u wilt laden (bijv, `/pictures/kitten.png`) in de **pad** textbox.</span><span class="sxs-lookup"><span data-stu-id="050f3-119">Enter the full path of each asset you wish to load (e.g., `/pictures/kitten.png`) in the **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="050f3-120">Meer **pad** tekstvakken wordt weergegeven nadat u tekst zodat u kunt een lijst samenstellen van meerdere elementen.</span><span class="sxs-lookup"><span data-stu-id="050f3-120">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="050f3-121">U kunt activa verwijderen uit de lijst door te klikken op de knop met het weglatingsteken (...).</span><span class="sxs-lookup"><span data-stu-id="050f3-121">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="050f3-122">Paden moeten een relatieve URL die past bij de volgende [reguliere expressie](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="050f3-122">Paths must be a relative URL that fits the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="050f3-123">Het pad naar een enkel bestand laden `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span><span class="sxs-lookup"><span data-stu-id="050f3-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="050f3-124">Laden van één bestand met de query-tekenreeks`@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="050f3-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="050f3-125">Elke asset moet een eigen pad hebben.</span><span class="sxs-lookup"><span data-stu-id="050f3-125">Each asset must have its own path.</span></span>  <span data-ttu-id="050f3-126">Er is geen functionaliteit jokerteken voor bedrijfsmiddelen die vooraf laden.</span><span class="sxs-lookup"><span data-stu-id="050f3-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Knop laden](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="050f3-128">Klik op de **Load** knop.</span><span class="sxs-lookup"><span data-stu-id="050f3-128">Click the **Load** button.</span></span>
   
    ![Knop laden](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="050f3-130">Er is een beperking van 10 load aanvragen per minuut per CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="050f3-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="050f3-131">50 paden zijn toegestaan per aanvraag.</span><span class="sxs-lookup"><span data-stu-id="050f3-131">50 paths are allowed per request.</span></span> <span data-ttu-id="050f3-132">Elk pad heeft een limiet lengte van 1024 tekens.</span><span class="sxs-lookup"><span data-stu-id="050f3-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="050f3-133">Zie ook</span><span class="sxs-lookup"><span data-stu-id="050f3-133">See also</span></span>
* [<span data-ttu-id="050f3-134">Een Azure CDN-eindpunt leegmaken</span><span class="sxs-lookup"><span data-stu-id="050f3-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="050f3-135">Naslaginformatie over Azure CDN REST-API - opschonen of een eindpunt vooraf laden</span><span class="sxs-lookup"><span data-stu-id="050f3-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

