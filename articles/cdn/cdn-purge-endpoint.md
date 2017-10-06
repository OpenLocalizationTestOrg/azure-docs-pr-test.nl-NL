---
title: een Azure CDN-eindpunt aaaPurge | Microsoft Docs
description: Meer informatie over hoe alle toopurge in de cache opgeslagen inhoud van een Azure CDN-eindpunt.
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
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="58d95-103">Een Azure CDN-eindpunt leegmaken</span><span class="sxs-lookup"><span data-stu-id="58d95-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="58d95-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="58d95-104">Overview</span></span>
<span data-ttu-id="58d95-105">Azure CDN edge-knooppunten cache activa totdat van Hallo actief time to live (TTL) is verlopen.</span><span class="sxs-lookup"><span data-stu-id="58d95-105">Azure CDN edge nodes will cache assets until hello asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="58d95-106">Nadat van Hallo actief TTL verloopt, wanneer een client Hallo asset bij Hallo edge-knooppunt aanvraagt, wordt de Hallo edge-knooppunt een nieuwe, bijgewerkte kopie van Hallo asset tooserve Hallo-clientaanvraag ophalen en de vernieuwen Hallo cache opslaan.</span><span class="sxs-lookup"><span data-stu-id="58d95-106">After hello asset's TTL expires, when a client requests hello asset from hello edge node, hello edge node will retrieve a new updated copy of hello asset tooserve hello client request and store refresh hello cache.</span></span>

<span data-ttu-id="58d95-107">Hallo best practice toomake ervoor dat uw gebruikers altijd de meest recente versie Hallo van uw assets ophalen is tooversion uw assets voor elke update en deze publiceren als nieuwe URL's.</span><span class="sxs-lookup"><span data-stu-id="58d95-107">hello best practice toomake sure your users always obtain hello latest copy of your assets is tooversion your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="58d95-108">CDN wordt onmiddellijk Hallo nieuwe activa voor de volgende clientaanvragen Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="58d95-108">CDN will immediately retrieve hello new assets for hello next client requests.</span></span>  <span data-ttu-id="58d95-109">U kunt soms desgewenst toopurge in de cache opgeslagen inhoud van alle knooppunten van de rand en zorgen dat ze alle tooretrieve nieuwe bijgewerkte activa.</span><span class="sxs-lookup"><span data-stu-id="58d95-109">Sometimes you may wish toopurge cached content from all edge nodes and force them all tooretrieve new updated assets.</span></span>  <span data-ttu-id="58d95-110">Dit kan zijn vanwege tooupdates tooyour-webtoepassing of tooquickly update assets die onjuiste gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="58d95-110">This might be due tooupdates tooyour web application, or tooquickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="58d95-111">Opmerking dat alleen Hallo opschonen wist in cache opgeslagen inhoud op Hallo CDN edge-servers.</span><span class="sxs-lookup"><span data-stu-id="58d95-111">Note that purging only clears hello cached content on hello CDN edge servers.</span></span>  <span data-ttu-id="58d95-112">Eventuele downstream caches, zoals proxyservers en caches van lokale, kunnen nog steeds een cachekopie van Hallo-bestand worden gehouden.</span><span class="sxs-lookup"><span data-stu-id="58d95-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of hello file.</span></span>  <span data-ttu-id="58d95-113">Het is belangrijk tooremember dit tijdens het instellen van een bestand time to live.</span><span class="sxs-lookup"><span data-stu-id="58d95-113">It's important tooremember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="58d95-114">U kunt een downstream toorequest Hallo meest recente clientversie van uw bestand afdwingen door een unieke naam geven telkens wanneer u deze bijwerken of door gebruik te maken van [query opslaan in cache](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="58d95-114">You can force a downstream client toorequest hello latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="58d95-115">Deze zelfstudie leert u het opschonen van de activa van alle knooppunten van de rand van een eindpunt.</span><span class="sxs-lookup"><span data-stu-id="58d95-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="58d95-116">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="58d95-116">Walkthrough</span></span>
1. <span data-ttu-id="58d95-117">In Hallo [Azure Portal](https://portal.azure.com), bladeren toohello CDN-profiel met de gewenste toopurge Hallo-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="58d95-117">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopurge.</span></span>
2. <span data-ttu-id="58d95-118">Klik op Hallo opschonen knop Hallo CDN-profiel blade.</span><span class="sxs-lookup"><span data-stu-id="58d95-118">From hello CDN profile blade, click hello purge button.</span></span>
   
    ![Blade CDN-profiel](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="58d95-120">Hallo opschonen blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="58d95-120">hello Purge blade opens.</span></span>
   
    ![Blade CDN-opschonen](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="58d95-122">Op Hallo opschonen blade, Hallo serviceadres toopurge uit Hallo URL vervolgkeuzelijst wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="58d95-122">On hello Purge blade, select hello service address you wish toopurge from hello URL dropdown.</span></span>
   
    ![Formulier opschonen](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="58d95-124">U kunt ook toohello opschonen blade opvragen door te klikken op Hallo **opschonen** knop op de blade Hallo CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="58d95-124">You can also get toohello Purge blade by clicking hello **Purge** button on hello CDN endpoint blade.</span></span>  <span data-ttu-id="58d95-125">In dat geval Hallo **URL** veld worden vooraf ingevuld met het adres van Hallo van dat specifieke eindpunt.</span><span class="sxs-lookup"><span data-stu-id="58d95-125">In that case, hello **URL** field will be pre-populated with hello service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="58d95-126">Selecteer welke activa u wenst toopurge van Hallo edge-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="58d95-126">Select what assets you wish toopurge from hello edge nodes.</span></span>  <span data-ttu-id="58d95-127">Als u wenst dat tooclear alle activa, klikt u op Hallo **Alles opschonen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="58d95-127">If you wish tooclear all assets, click hello **Purge all** checkbox.</span></span>  <span data-ttu-id="58d95-128">Anders tekst hello pad van elk actief gewenste toopurge in Hallo **pad** textbox.</span><span class="sxs-lookup"><span data-stu-id="58d95-128">Otherwise, type hello path of each asset you wish toopurge in hello **Path** textbox.</span></span> <span data-ttu-id="58d95-129">Hieronder indelingen worden ondersteund in Hallo-pad.</span><span class="sxs-lookup"><span data-stu-id="58d95-129">Below formats are supported in hello path.</span></span>
    1. <span data-ttu-id="58d95-130">**Opschonen van één URL**: individuele asset opschonen door te geven van de volledige URL hello, met of zonder Hallo bestandsextensie, bijvoorbeeld`/pictures/strasbourg.png`;`/pictures/strasbourg`</span><span class="sxs-lookup"><span data-stu-id="58d95-130">**Single URL purge**: Purge individual asset by specifying hello full URL, with or without hello file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="58d95-131">**Jokertekens opschonen**: sterretje (\*) kan worden gebruikt als een jokerteken.</span><span class="sxs-lookup"><span data-stu-id="58d95-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="58d95-132">Opschonen van mappen, submappen en bestanden onder een eindpunt met `/*` in pad Hallo of opschonen van alle submappen en bestanden in een specifieke map die door te geven Hallo map gevolgd door `/*`, bijvoorbeeld`/pictures/*`.</span><span class="sxs-lookup"><span data-stu-id="58d95-132">Purge all folders, sub-folders and files under an endpoint with `/*` in hello path or purge all sub-folders and files under a specific folder by specifying hello folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="58d95-133">Houd er rekening mee dat leegmaken met jokertekens wordt momenteel niet ondersteund door Azure CDN van Akamai.</span><span class="sxs-lookup"><span data-stu-id="58d95-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="58d95-134">**Opschonen van domein hoofdmap**: opschonen Hallo hoofdmap van het Hallo-eindpunt met '/' Hallo-pad.</span><span class="sxs-lookup"><span data-stu-id="58d95-134">**Root domain purge**: Purge hello root of hello endpoint with "/" in hello path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="58d95-135">Paden moeten worden opgegeven voor opschonen en moet een relatieve URL die voldoen aan de volgende Hallo [reguliere expressie](https://msdn.microsoft.com/library/az24scfc.aspx).</span><span class="sxs-lookup"><span data-stu-id="58d95-135">Paths must be specified for purge and must be a relative URL that fit hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="58d95-136">**Alles opschonen** en **jokertekens opschonen** niet wordt ondersteund door **Azure CDN van Akamai** momenteel.</span><span class="sxs-lookup"><span data-stu-id="58d95-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="58d95-137">Opschonen van één URL`@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="58d95-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="58d95-138">Queryreeks`@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="58d95-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="58d95-139">Jokertekens opschonen `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span><span class="sxs-lookup"><span data-stu-id="58d95-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="58d95-140">Meer **pad** tekstvakken wordt weergegeven nadat u hebt ingevoerd tekst tooallow toobuild een lijst met meerdere elementen.</span><span class="sxs-lookup"><span data-stu-id="58d95-140">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="58d95-141">U kunt activa verwijderen uit de lijst Hallo door te klikken op de knop met het weglatingsteken (...) Hallo.</span><span class="sxs-lookup"><span data-stu-id="58d95-141">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="58d95-142">Klik op Hallo **opschonen** knop.</span><span class="sxs-lookup"><span data-stu-id="58d95-142">Click hello **Purge** button.</span></span>
   
    ![Knop verwijderen](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="58d95-144">Opschonen aanvragen nemen ongeveer 2-3 minuten tooprocess met **Azure CDN van Verizon** (standaard en Premium), en ongeveer 7 minuten met **Azure CDN van Akamai**.</span><span class="sxs-lookup"><span data-stu-id="58d95-144">Purge requests take approximately 2-3 minutes tooprocess with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="58d95-145">Azure CDN heeft een limiet van 50 gelijktijdige aanvragen op elk moment verwijderen.</span><span class="sxs-lookup"><span data-stu-id="58d95-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="58d95-146">Zie ook</span><span class="sxs-lookup"><span data-stu-id="58d95-146">See also</span></span>
* [<span data-ttu-id="58d95-147">Vooraf assets op een Azure CDN-eindpunt laden</span><span class="sxs-lookup"><span data-stu-id="58d95-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="58d95-148">Naslaginformatie over Azure CDN REST-API - opschonen of een eindpunt vooraf laden</span><span class="sxs-lookup"><span data-stu-id="58d95-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

