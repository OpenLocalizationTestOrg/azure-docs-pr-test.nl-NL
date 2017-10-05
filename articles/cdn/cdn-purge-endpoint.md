---
title: Een Azure CDN-eindpunt leegmaken | Microsoft Docs
description: Informatie over het wissen van alle inhoud in cache van een Azure CDN-eindpunt.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: b035c232bb58d653960190d4974cc3789d55a51d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="afd3c-103">Een Azure CDN-eindpunt leegmaken</span><span class="sxs-lookup"><span data-stu-id="afd3c-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="afd3c-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="afd3c-104">Overview</span></span>
<span data-ttu-id="afd3c-105">Azure CDN edge-knooppunten cache activa totdat de asset time to live (TTL) is verlopen.</span><span class="sxs-lookup"><span data-stu-id="afd3c-105">Azure CDN edge nodes will cache assets until the asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="afd3c-106">Nadat de asset TTL is verlopen wanneer een client de asset-van het edge-knooppunt aanvragen, het edge-knooppunt wordt een nieuwe, bijgewerkte kopie van de asset voor aanvraag van de client opgehaald en store Vernieuw het cachegeheugen.</span><span class="sxs-lookup"><span data-stu-id="afd3c-106">After the asset's TTL expires, when a client requests the asset from the edge node, the edge node will retrieve a new updated copy of the asset to serve the client request and store refresh the cache.</span></span>

<span data-ttu-id="afd3c-107">De beste manier om ervoor te zorgen dat uw gebruikers altijd de meest recente kopie van uw assets ophalen is versie van uw assets voor elke update en deze publiceren als nieuwe URL's.</span><span class="sxs-lookup"><span data-stu-id="afd3c-107">The best practice to make sure your users always obtain the latest copy of your assets is to version your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="afd3c-108">CDN haalt onmiddellijk nieuwe elementen voor de volgende aanvragen van clients.</span><span class="sxs-lookup"><span data-stu-id="afd3c-108">CDN will immediately retrieve the new assets for the next client requests.</span></span>  <span data-ttu-id="afd3c-109">Soms wilt u mogelijk de inhoud in cache wissen van alle knooppunten van de rand en zorgen dat ze alle nieuwe bijgewerkte activa ophalen.</span><span class="sxs-lookup"><span data-stu-id="afd3c-109">Sometimes you may wish to purge cached content from all edge nodes and force them all to retrieve new updated assets.</span></span>  <span data-ttu-id="afd3c-110">Dit kan zijn vanwege updates op uw webtoepassing, of op snel update assets die onjuiste gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="afd3c-110">This might be due to updates to your web application, or to quickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="afd3c-111">Houd er rekening mee dat alleen de inhoud in de cache op de servers van de rand CDN opschonen wist.</span><span class="sxs-lookup"><span data-stu-id="afd3c-111">Note that purging only clears the cached content on the CDN edge servers.</span></span>  <span data-ttu-id="afd3c-112">Eventuele downstream caches, zoals proxyservers en caches van lokale, kunnen nog steeds een kopie van het bestand worden gehouden.</span><span class="sxs-lookup"><span data-stu-id="afd3c-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of the file.</span></span>  <span data-ttu-id="afd3c-113">Het is belangrijk om te onthouden dit als u een bestand time to live.</span><span class="sxs-lookup"><span data-stu-id="afd3c-113">It's important to remember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="afd3c-114">U kunt een downstream-client om aan te vragen van de meest recente versie van het bestand door een unieke naam geven telkens wanneer u deze bijwerken of door gebruik te maken van afdwingen [query opslaan in cache](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="afd3c-114">You can force a downstream client to request the latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="afd3c-115">Deze zelfstudie leert u het opschonen van de activa van alle knooppunten van de rand van een eindpunt.</span><span class="sxs-lookup"><span data-stu-id="afd3c-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="afd3c-116">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="afd3c-116">Walkthrough</span></span>
1. <span data-ttu-id="afd3c-117">In de [Azure Portal](https://portal.azure.com), blader naar de CDN-profiel met het eindpunt dat u wilt wissen.</span><span class="sxs-lookup"><span data-stu-id="afd3c-117">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to purge.</span></span>
2. <span data-ttu-id="afd3c-118">Klik op de knop opschonen van de blade CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="afd3c-118">From the CDN profile blade, click the purge button.</span></span>
   
    ![Blade CDN-profiel](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="afd3c-120">De blade opschonen wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="afd3c-120">The Purge blade opens.</span></span>
   
    ![Blade CDN-opschonen](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="afd3c-122">Selecteer op de blade opschonen het serviceadres die u wilt verwijderen uit de vervolgkeuzelijst URL.</span><span class="sxs-lookup"><span data-stu-id="afd3c-122">On the Purge blade, select the service address you wish to purge from the URL dropdown.</span></span>
   
    ![Formulier opschonen](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="afd3c-124">U kunt ook naar de blade opschonen opvragen door te klikken op de **opschonen** knop op de blade CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="afd3c-124">You can also get to the Purge blade by clicking the **Purge** button on the CDN endpoint blade.</span></span>  <span data-ttu-id="afd3c-125">In dat geval de **URL** veld worden vooraf ingevuld met het serviceadres van dat specifieke eindpunt.</span><span class="sxs-lookup"><span data-stu-id="afd3c-125">In that case, the **URL** field will be pre-populated with the service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="afd3c-126">Selecteer welke elementen die u wilt verwijderen uit de edge-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="afd3c-126">Select what assets you wish to purge from the edge nodes.</span></span>  <span data-ttu-id="afd3c-127">Als u wenst te wissen van alle activa, klikt u op de **Alles opschonen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="afd3c-127">If you wish to clear all assets, click the **Purge all** checkbox.</span></span>  <span data-ttu-id="afd3c-128">Anders, typ het pad van elke asset die u wissen wilt de **pad** textbox.</span><span class="sxs-lookup"><span data-stu-id="afd3c-128">Otherwise, type the path of each asset you wish to purge in the **Path** textbox.</span></span> <span data-ttu-id="afd3c-129">Hieronder indelingen worden ondersteund in het pad.</span><span class="sxs-lookup"><span data-stu-id="afd3c-129">Below formats are supported in the path.</span></span>
    1. <span data-ttu-id="afd3c-130">**Opschonen van één URL**: individuele asset opschonen door te geven van de volledige URL met of zonder de bestandsextensie, bijvoorbeeld`/pictures/strasbourg.png`;`/pictures/strasbourg`</span><span class="sxs-lookup"><span data-stu-id="afd3c-130">**Single URL purge**: Purge individual asset by specifying the full URL, with or without the file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="afd3c-131">**Jokertekens opschonen**: sterretje (\*) kan worden gebruikt als een jokerteken.</span><span class="sxs-lookup"><span data-stu-id="afd3c-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="afd3c-132">Opschonen van mappen, submappen en bestanden onder een eindpunt met `/*` in het pad of opschonen alle submappen en bestanden in een specifieke map die door het opgeven van de map gevolgd door `/*`, bijvoorbeeld`/pictures/*`.</span><span class="sxs-lookup"><span data-stu-id="afd3c-132">Purge all folders, sub-folders and files under an endpoint with `/*` in the path or purge all sub-folders and files under a specific folder by specifying the folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="afd3c-133">Houd er rekening mee dat leegmaken met jokertekens wordt momenteel niet ondersteund door Azure CDN van Akamai.</span><span class="sxs-lookup"><span data-stu-id="afd3c-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="afd3c-134">**Opschonen van domein hoofdmap**: opschonen van de hoofdmap van het eindpunt met '/' in het pad.</span><span class="sxs-lookup"><span data-stu-id="afd3c-134">**Root domain purge**: Purge the root of the endpoint with "/" in the path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="afd3c-135">Paden moeten worden opgegeven voor opschonen en moet een relatieve URL die voldoen aan de volgende [reguliere expressie](https://msdn.microsoft.com/library/az24scfc.aspx).</span><span class="sxs-lookup"><span data-stu-id="afd3c-135">Paths must be specified for purge and must be a relative URL that fit the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="afd3c-136">**Alles opschonen** en **jokertekens opschonen** niet wordt ondersteund door **Azure CDN van Akamai** momenteel.</span><span class="sxs-lookup"><span data-stu-id="afd3c-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="afd3c-137">Opschonen van één URL`@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="afd3c-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="afd3c-138">Queryreeks`@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="afd3c-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="afd3c-139">Jokertekens opschonen `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span><span class="sxs-lookup"><span data-stu-id="afd3c-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="afd3c-140">Meer **pad** tekstvakken wordt weergegeven nadat u tekst zodat u kunt een lijst samenstellen van meerdere elementen.</span><span class="sxs-lookup"><span data-stu-id="afd3c-140">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="afd3c-141">U kunt activa verwijderen uit de lijst door te klikken op de knop met het weglatingsteken (...).</span><span class="sxs-lookup"><span data-stu-id="afd3c-141">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="afd3c-142">Klik op de **opschonen** knop.</span><span class="sxs-lookup"><span data-stu-id="afd3c-142">Click the **Purge** button.</span></span>
   
    ![Knop verwijderen](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="afd3c-144">Opschonen aanvragen minuten duren voordat ongeveer 2-3 verwerkt met **Azure CDN van Verizon** (standaard en Premium), en ongeveer 7 minuten met **Azure CDN van Akamai**.</span><span class="sxs-lookup"><span data-stu-id="afd3c-144">Purge requests take approximately 2-3 minutes to process with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="afd3c-145">Azure CDN heeft een limiet van 50 gelijktijdige aanvragen op elk moment verwijderen.</span><span class="sxs-lookup"><span data-stu-id="afd3c-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="afd3c-146">Zie ook</span><span class="sxs-lookup"><span data-stu-id="afd3c-146">See also</span></span>
* [<span data-ttu-id="afd3c-147">Vooraf assets op een Azure CDN-eindpunt laden</span><span class="sxs-lookup"><span data-stu-id="afd3c-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="afd3c-148">Naslaginformatie over Azure CDN REST-API - opschonen of een eindpunt vooraf laden</span><span class="sxs-lookup"><span data-stu-id="afd3c-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

