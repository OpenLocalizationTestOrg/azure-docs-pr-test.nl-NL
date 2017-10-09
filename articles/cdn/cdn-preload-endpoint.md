---
title: aaaPre load activa op een Azure CDN-eindpunt | Microsoft Docs
description: Meer informatie over hoe toopre laden in de cache opgeslagen inhoud op een Azure CDN-eindpunt.
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
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="1daef-103">Vooraf assets op een Azure CDN-eindpunt laden</span><span class="sxs-lookup"><span data-stu-id="1daef-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="1daef-104">Standaard activa eerst in de cache opgeslagen als ze worden aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="1daef-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="1daef-105">Dit betekent dat de eerste aanvraag Hallo van elke regio kan het langer duren, omdat de randservers Hallo niet Hallo inhoud in de cache opgeslagen en moet tooforward Hallo aanvraag toohello-bronserver.</span><span class="sxs-lookup"><span data-stu-id="1daef-105">This means that hello first request from each region may take longer, since hello edge servers will not have hello content cached and will need tooforward hello request toohello origin server.</span></span> <span data-ttu-id="1daef-106">Vooraf laden van inhoud, wordt dit eerste treffers latentie voorkomen.</span><span class="sxs-lookup"><span data-stu-id="1daef-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="1daef-107">Bovendien kan tooproviding een betere klantervaring uw assets in de cache vooraf laden ook netwerkverkeer op de bronserver Hallo verminderen.</span><span class="sxs-lookup"><span data-stu-id="1daef-107">In addition tooproviding a better customer experience, pre-loading your cached assets can also reduce network traffic on hello origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="1daef-108">Vooraf laden van de activa is handig voor grote gebeurtenissen of inhoud die wordt gelijktijdig beschikbare tooa groot aantal gebruikers, zoals een nieuwe film release of een software-update.</span><span class="sxs-lookup"><span data-stu-id="1daef-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available tooa large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="1daef-109">Deze zelfstudie leert u de inhoud op alle knooppunten van Azure CDN edge cache vooraf laden.</span><span class="sxs-lookup"><span data-stu-id="1daef-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="1daef-110">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="1daef-110">Walkthrough</span></span>
1. <span data-ttu-id="1daef-111">In Hallo [Azure Portal](https://portal.azure.com), bladeren toohello CDN-profiel met de gewenste toopre load Hallo-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="1daef-111">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopre-load.</span></span>  <span data-ttu-id="1daef-112">Hallo profiel blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="1daef-112">hello profile blade opens.</span></span>
2. <span data-ttu-id="1daef-113">Klik op Hallo eindpunt in Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="1daef-113">Click hello endpoint in hello list.</span></span>  <span data-ttu-id="1daef-114">Hallo eindpunt blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="1daef-114">hello endpoint blade opens.</span></span>
3. <span data-ttu-id="1daef-115">Klik op Hallo load knop Hallo CDN-eindpunt blade.</span><span class="sxs-lookup"><span data-stu-id="1daef-115">From hello CDN endpoint blade, click hello load button.</span></span>
   
    ![Blade CDN-eindpunt](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="1daef-117">Hallo Load blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="1daef-117">hello Load blade opens.</span></span>
   
    ![Load-blade CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="1daef-119">Geef het volledige pad Hallo van elk actief gewenst tooload (bijv, `/pictures/kitten.png`) in Hallo **pad** textbox.</span><span class="sxs-lookup"><span data-stu-id="1daef-119">Enter hello full path of each asset you wish tooload (e.g., `/pictures/kitten.png`) in hello **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="1daef-120">Meer **pad** tekstvakken wordt weergegeven nadat u hebt ingevoerd tekst tooallow toobuild een lijst met meerdere elementen.</span><span class="sxs-lookup"><span data-stu-id="1daef-120">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="1daef-121">U kunt activa verwijderen uit de lijst Hallo door te klikken op de knop met het weglatingsteken (...) Hallo.</span><span class="sxs-lookup"><span data-stu-id="1daef-121">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="1daef-122">Paden moeten een relatieve URL die past bij de volgende Hallo [reguliere expressie](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="1daef-122">Paths must be a relative URL that fits hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="1daef-123">Het pad naar een enkel bestand laden `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span><span class="sxs-lookup"><span data-stu-id="1daef-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="1daef-124">Laden van één bestand met de query-tekenreeks`@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="1daef-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="1daef-125">Elke asset moet een eigen pad hebben.</span><span class="sxs-lookup"><span data-stu-id="1daef-125">Each asset must have its own path.</span></span>  <span data-ttu-id="1daef-126">Er is geen functionaliteit jokerteken voor bedrijfsmiddelen die vooraf laden.</span><span class="sxs-lookup"><span data-stu-id="1daef-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Knop laden](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="1daef-128">Klik op Hallo **Load** knop.</span><span class="sxs-lookup"><span data-stu-id="1daef-128">Click hello **Load** button.</span></span>
   
    ![Knop laden](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="1daef-130">Er is een beperking van 10 load aanvragen per minuut per CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="1daef-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="1daef-131">50 paden zijn toegestaan per aanvraag.</span><span class="sxs-lookup"><span data-stu-id="1daef-131">50 paths are allowed per request.</span></span> <span data-ttu-id="1daef-132">Elk pad heeft een limiet lengte van 1024 tekens.</span><span class="sxs-lookup"><span data-stu-id="1daef-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="1daef-133">Zie ook</span><span class="sxs-lookup"><span data-stu-id="1daef-133">See also</span></span>
* [<span data-ttu-id="1daef-134">Een Azure CDN-eindpunt leegmaken</span><span class="sxs-lookup"><span data-stu-id="1daef-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="1daef-135">Naslaginformatie over Azure CDN REST-API - opschonen of een eindpunt vooraf laden</span><span class="sxs-lookup"><span data-stu-id="1daef-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

