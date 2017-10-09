---
title: 'Machine Learning aanbevelingen: JavaScript-integratie | Microsoft Docs'
description: Azure Machine Learning aanbevelingen - integratie van JavaScript - documentatie
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="666da-103">Aanbevelingen voor Azure Machine Learning - JavaScript-integratie</span><span class="sxs-lookup"><span data-stu-id="666da-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="666da-104">U moet beginnen met Hallo cognitieve aanbevelingen API-Service in plaats van deze versie.</span><span class="sxs-lookup"><span data-stu-id="666da-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="666da-105">Hallo aanbevelingen cognitieve Service vervangt deze service en alle nieuwe functies in Hallo er zal worden ontwikkeld.</span><span class="sxs-lookup"><span data-stu-id="666da-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="666da-106">Heeft nieuwe mogelijkheden, zoals batchverwerking ondersteuning, beter API Explorer, een schonere API surface, consistente aanmelding/facturering ervaring, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="666da-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="666da-107">Meer informatie over [migreren toohello nieuwe cognitieve Service](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="666da-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="666da-108">Dit document weer hoe toointegrate uw site met JavaScript.</span><span class="sxs-lookup"><span data-stu-id="666da-108">This document depict how toointegrate your site using JavaScript.</span></span> <span data-ttu-id="666da-109">Hallo JavaScript kunt u toosend gegevens overname gebeurtenissen en tooconsume aanbevelingen als u een aanbeveling model maakt.</span><span class="sxs-lookup"><span data-stu-id="666da-109">hello JavaScript enables you toosend Data Acquisition events and tooconsume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="666da-110">Alle bewerkingen die worden uitgevoerd via JS kunnen ook worden gedaan vanuit serverzijde.</span><span class="sxs-lookup"><span data-stu-id="666da-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="666da-111">1. Algemeen-overzicht</span><span class="sxs-lookup"><span data-stu-id="666da-111">1. General Overview</span></span>
<span data-ttu-id="666da-112">Uw site integreren met Azure ML aanbevelingen bestaan op 2 fasen:</span><span class="sxs-lookup"><span data-stu-id="666da-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="666da-113">Gebeurtenissen verzenden naar Azure ML-aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="666da-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="666da-114">Hiermee schakelt u toobuild een aanbeveling-model.</span><span class="sxs-lookup"><span data-stu-id="666da-114">This will enable toobuild a recommendation model.</span></span>
2. <span data-ttu-id="666da-115">Hallo aanbevelingen in beslag nemen.</span><span class="sxs-lookup"><span data-stu-id="666da-115">Consume hello recommendations.</span></span> <span data-ttu-id="666da-116">Nadat het Hallo-model is gebouwd kunt u Hallo aanbevelingen verbruiken.</span><span class="sxs-lookup"><span data-stu-id="666da-116">After hello model is built you can consume hello recommendations.</span></span> <span data-ttu-id="666da-117">(Dit document wordt niet uitgelegd hoe toobuild een model lezen Hallo tooget voor snel starten-handleiding voor meer informatie over het).</span><span class="sxs-lookup"><span data-stu-id="666da-117">(This document does not explain how toobuild a model, read hello quick start guide tooget more information on how).</span></span>

<span data-ttu-id="666da-118"><ins>Fase I</ins></span><span class="sxs-lookup"><span data-stu-id="666da-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="666da-119">Eerste fase die u wilt invoegen in uw HTML-pagina's een kleine JavaScript-bibliotheek waarmee Hallo in Hallo toosend gebeurtenissen op pagina als deze problemen op Hallo HTML-pagina in de Azure ML aanbevelingen-servers (via Data markt optreden):</span><span class="sxs-lookup"><span data-stu-id="666da-119">In hello first phase you insert into your html pages a small JavaScript library that enables hello page toosend events as they occur on hello html page into Azure ML Recommendations servers (via Data Market):</span></span>

![Tekening1][1]

<span data-ttu-id="666da-121"><ins>Fase II</ins></span><span class="sxs-lookup"><span data-stu-id="666da-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="666da-122">Hallo Selecteer tweede fase als u wilt dat tooshow Hallo aanbevelingen op Hallo pagina u in een Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="666da-122">In hello second phase when you want tooshow hello recommendations on hello page you select one of hello following options:</span></span>

<span data-ttu-id="666da-123">1. de server (op het Hallo-fase van de paginaweergave) roept Azure ML aanbevelingen Server (via Data markt) tooget aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="666da-123">1.Your server (on hello phase of page rendering) calls Azure ML Recommendations Server (via Data Market) tooget recommendations.</span></span> <span data-ttu-id="666da-124">Hallo resultaten bevatten een lijst met items-id. Uw server moet tooenrich Hallo resultaten Hallo items, metagegevens (bijvoorbeeld afbeeldingen, beschrijving) en pagina toohello browser gemaakt Hallo verzenden.</span><span class="sxs-lookup"><span data-stu-id="666da-124">hello results include a list of items id. Your server needs tooenrich hello results with hello items Meta data (e.g. images, description) and send hello created page toohello browser.</span></span>

![Drawing2][2]

<span data-ttu-id="666da-126">2. hello is andere optie toouse Hallo klein JavaScript-bestand van fase één tooget een eenvoudige lijst met aanbevolen items.</span><span class="sxs-lookup"><span data-stu-id="666da-126">2.hello other option is toouse hello small JavaScript file from phase one tooget a simple list of recommended items.</span></span> <span data-ttu-id="666da-127">Hallo gegevens ontvangen hier is minder dan Hallo in de eerste optie Hallo complex.</span><span class="sxs-lookup"><span data-stu-id="666da-127">hello data received here is leaner than hello one in hello first option.</span></span>

![Drawing3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="666da-129">2. Vereisten</span><span class="sxs-lookup"><span data-stu-id="666da-129">2. Prerequisites</span></span>
1. <span data-ttu-id="666da-130">Maak een nieuw model met Hallo API's.</span><span class="sxs-lookup"><span data-stu-id="666da-130">Create a new model using hello APIs.</span></span> <span data-ttu-id="666da-131">Zie de Snelstartgids Hallo over het toodo deze.</span><span class="sxs-lookup"><span data-stu-id="666da-131">See hello Quick start guide on how toodo it.</span></span>
2. <span data-ttu-id="666da-132">Codeer uw &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; met base64.</span><span class="sxs-lookup"><span data-stu-id="666da-132">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="666da-133">(Dit wordt gebruikt voor Hallo basisverificatie tooenable Hallo JS code toocall Hallo API's).</span><span class="sxs-lookup"><span data-stu-id="666da-133">(This will be used for hello basic authentication tooenable hello JS code toocall hello APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="666da-134">3. Verzenden van gegevens overname gebeurtenissen met JavaScript</span><span class="sxs-lookup"><span data-stu-id="666da-134">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="666da-135">Hallo stappen te volgen vergemakkelijken verzenden gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="666da-135">hello following steps facilitate sending events:</span></span>

1. <span data-ttu-id="666da-136">JQuery-bibliotheek opnemen in uw code.</span><span class="sxs-lookup"><span data-stu-id="666da-136">Include JQuery library in your code.</span></span> <span data-ttu-id="666da-137">U kunt dit downloaden van nuget in Hallo URL te volgen.</span><span class="sxs-lookup"><span data-stu-id="666da-137">You can download it from nuget in hello following URL.</span></span>
   
     <span data-ttu-id="666da-138">http://www.nuget.org/Packages/jQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="666da-138">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="666da-139">Hallo aanbevelingen JavaScript-bibliotheek van Hallo volgende URL: http://aka.ms/RecoJSLib1</span><span class="sxs-lookup"><span data-stu-id="666da-139">Include hello Recommendations Java Script library from hello following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="666da-140">Aanbevelingen voor Azure ML-bibliotheek met de juiste parameters Hallo initialiseren.</span><span class="sxs-lookup"><span data-stu-id="666da-140">Initialize Azure ML Recommendations library with hello appropriate parameters.</span></span>
   
     <span data-ttu-id="666da-141"><script>AzureMLRecommendationsStart ('<base64encoding of username:key>', "< model_id >"); </script> 
4. Gebeurtenis Hallo verzenden.</span><span class="sxs-lookup"><span data-stu-id="666da-141"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send hello appropriate event.</span></span> <span data-ttu-id="666da-142">Zie het detailgedeelte hieronder op alle typen gebeurtenissen (voorbeeld van Klik gebeurtenis) <script> als (typeof AzureMLRecommendationsEvent == 'undefined') {</span><span class="sxs-lookup"><span data-stu-id="666da-142">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="666da-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({event: "click", item: "18321116"});</script></span><span class="sxs-lookup"><span data-stu-id="666da-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="666da-144">3.1.</span><span class="sxs-lookup"><span data-stu-id="666da-144">3.1.</span></span>    <span data-ttu-id="666da-145">Beperkingen en ondersteuning van browsers</span><span class="sxs-lookup"><span data-stu-id="666da-145">Limitations and Browser Support</span></span>
<span data-ttu-id="666da-146">Dit is een verwijzing implementatie en krijgt, omdat de.</span><span class="sxs-lookup"><span data-stu-id="666da-146">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="666da-147">Deze moet alle belangrijke browsers ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="666da-147">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="666da-148">3.2.</span><span class="sxs-lookup"><span data-stu-id="666da-148">3.2.</span></span>    <span data-ttu-id="666da-149">Type van gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="666da-149">Type of Events</span></span>
<span data-ttu-id="666da-150">Er zijn 5 typen gebeurtenissen die bibliotheek ondersteunt Hallo: klikt u op, aanbeveling op klikt, tooShop winkelwagen, toevoegen verwijderen uit de winkelwagen Shop en aankoop.</span><span class="sxs-lookup"><span data-stu-id="666da-150">There are 5 types of event that hello library supports: Click, Recommendation Click, Add tooShop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="666da-151">Er is een extra gebeurtenis die is gebruikt tooset Hallo gebruikerscontext aanmelding aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="666da-151">There is an additional event that is used tooset hello user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="666da-152">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="666da-152">3.2.1.</span></span> <span data-ttu-id="666da-153">Klik op gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="666da-153">Click Event</span></span>
<span data-ttu-id="666da-154">Deze gebeurtenis moet worden gebruikt als elk gewenst moment een gebruiker op een item wordt geklikt.</span><span class="sxs-lookup"><span data-stu-id="666da-154">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="666da-155">Meestal wanneer de gebruiker klikt op een item wordt een nieuwe pagina geopend met Hallo itemgegevens; Deze gebeurtenis moet worden gestart op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="666da-155">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="666da-156">Parameters:</span><span class="sxs-lookup"><span data-stu-id="666da-156">Parameters:</span></span>

* <span data-ttu-id="666da-157">gebeurtenis (string, verplichte) 'Klik'</span><span class="sxs-lookup"><span data-stu-id="666da-157">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="666da-158">item (string, verplichte) - de unieke id van het Hallo-item</span><span class="sxs-lookup"><span data-stu-id="666da-158">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="666da-159">itemName (string, optioneel) - Hallo-naam van Hallo-item</span><span class="sxs-lookup"><span data-stu-id="666da-159">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="666da-160">itemDescription (string, optioneel) - Hallo beschrijving van Hallo-item</span><span class="sxs-lookup"><span data-stu-id="666da-160">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="666da-161">itemCategory (string, optioneel) - Hallo categorie van het Hallo-item</span><span class="sxs-lookup"><span data-stu-id="666da-161">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="666da-162">Of met optionele gegevens:</span><span class="sxs-lookup"><span data-stu-id="666da-162">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="666da-163">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="666da-163">3.2.2.</span></span> <span data-ttu-id="666da-164">Aanbeveling klikt u op de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="666da-164">Recommendation Click Event</span></span>
<span data-ttu-id="666da-165">Deze gebeurtenis moet worden gebruikt als elk gewenst moment een gebruiker op een item dat is ontvangen van Azure ML aanbevelingen als een aanbevolen item wordt geklikt.</span><span class="sxs-lookup"><span data-stu-id="666da-165">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="666da-166">Meestal wanneer de gebruiker klikt op een item wordt een nieuwe pagina geopend met Hallo itemgegevens; Deze gebeurtenis moet worden gestart op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="666da-166">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="666da-167">Parameters:</span><span class="sxs-lookup"><span data-stu-id="666da-167">Parameters:</span></span>

* <span data-ttu-id="666da-168">gebeurtenis (string, verplichte) 'recommendationclick'</span><span class="sxs-lookup"><span data-stu-id="666da-168">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="666da-169">item (string, verplichte) - de unieke id van het Hallo-item</span><span class="sxs-lookup"><span data-stu-id="666da-169">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="666da-170">itemName (string, optioneel) - Hallo-naam van Hallo-item</span><span class="sxs-lookup"><span data-stu-id="666da-170">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="666da-171">itemDescription (string, optioneel) - Hallo beschrijving van Hallo-item</span><span class="sxs-lookup"><span data-stu-id="666da-171">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="666da-172">itemCategory (string, optioneel) - Hallo categorie van het Hallo-item</span><span class="sxs-lookup"><span data-stu-id="666da-172">itemCategory (string, optional) - hello category of hello item</span></span>
* <span data-ttu-id="666da-173">zaden (string-matrix, optioneel) - Hallo zaden die Hallo aanbeveling query gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="666da-173">seeds (string array, optional) - hello seeds that generated hello recommendation query.</span></span>
* <span data-ttu-id="666da-174">recoList (string-matrix, optioneel) - Hallo resultaat van Hallo aanbeveling aanvraag die gegenereerd Hallo-item waarop is geklikt.</span><span class="sxs-lookup"><span data-stu-id="666da-174">recoList (string array, optional) - hello result of hello recommendation request that generated hello item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="666da-175">Of met optionele gegevens:</span><span class="sxs-lookup"><span data-stu-id="666da-175">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="666da-176">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="666da-176">3.2.3.</span></span> <span data-ttu-id="666da-177">Winkelwagen winkelwagen gebeurtenis toevoegen</span><span class="sxs-lookup"><span data-stu-id="666da-177">Add Shopping Cart Event</span></span>
<span data-ttu-id="666da-178">Deze gebeurtenis moet worden gebruikt wanneer Hallo gebruiker een item toohello winkelwagen toevoegt.</span><span class="sxs-lookup"><span data-stu-id="666da-178">This event should be used when hello user add an item toohello shopping cart.</span></span>
<span data-ttu-id="666da-179">Parameters:</span><span class="sxs-lookup"><span data-stu-id="666da-179">Parameters:</span></span>

* <span data-ttu-id="666da-180">gebeurtenis (string, verplichte) 'addshopcart'</span><span class="sxs-lookup"><span data-stu-id="666da-180">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="666da-181">item (string, verplichte) - de unieke id van het Hallo-item</span><span class="sxs-lookup"><span data-stu-id="666da-181">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="666da-182">itemName (string, optioneel) - Hallo-naam van Hallo-item</span><span class="sxs-lookup"><span data-stu-id="666da-182">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="666da-183">itemDescription (string, optioneel) - Hallo beschrijving van Hallo-item</span><span class="sxs-lookup"><span data-stu-id="666da-183">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="666da-184">itemCategory (string, optioneel) - Hallo categorie van het Hallo-item</span><span class="sxs-lookup"><span data-stu-id="666da-184">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="666da-185">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="666da-185">3.2.4.</span></span> <span data-ttu-id="666da-186">Verwijder winkelen winkelwagen gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="666da-186">Remove Shopping Cart Event</span></span>
<span data-ttu-id="666da-187">Deze gebeurtenis moet worden gebruikt wanneer Hallo gebruiker een item toohello-winkelwagen verwijdert.</span><span class="sxs-lookup"><span data-stu-id="666da-187">This event should be used when hello user removes an item toohello shopping cart.</span></span>

<span data-ttu-id="666da-188">Parameters:</span><span class="sxs-lookup"><span data-stu-id="666da-188">Parameters:</span></span>

* <span data-ttu-id="666da-189">gebeurtenis (string, verplichte) 'removeshopcart'</span><span class="sxs-lookup"><span data-stu-id="666da-189">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="666da-190">item (string, verplichte) - de unieke id van het Hallo-item</span><span class="sxs-lookup"><span data-stu-id="666da-190">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="666da-191">itemName (string, optioneel) - Hallo-naam van Hallo-item</span><span class="sxs-lookup"><span data-stu-id="666da-191">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="666da-192">itemDescription (string, optioneel) - Hallo beschrijving van Hallo-item</span><span class="sxs-lookup"><span data-stu-id="666da-192">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="666da-193">itemCategory (string, optioneel) - Hallo categorie van het Hallo-item</span><span class="sxs-lookup"><span data-stu-id="666da-193">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="666da-194">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="666da-194">3.2.5.</span></span> <span data-ttu-id="666da-195">Aankoop gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="666da-195">Purchase Event</span></span>
<span data-ttu-id="666da-196">Deze gebeurtenis moet worden gebruikt wanneer het Hallo-gebruiker zijn winkelwagen hebt aangeschaft.</span><span class="sxs-lookup"><span data-stu-id="666da-196">This event should be used when hello user purchased his shopping cart.</span></span>

<span data-ttu-id="666da-197">Parameters:</span><span class="sxs-lookup"><span data-stu-id="666da-197">Parameters:</span></span>

* <span data-ttu-id="666da-198">gebeurtenis (tekenreeks) - 'kopen'</span><span class="sxs-lookup"><span data-stu-id="666da-198">event (string) - “purchase”</span></span>
* <span data-ttu-id="666da-199">objecten (aangekocht []) - matrix met een vermelding voor elk item hebt aangeschaft.</span><span class="sxs-lookup"><span data-stu-id="666da-199">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="666da-200">Gekochte indeling:</span><span class="sxs-lookup"><span data-stu-id="666da-200">Purchased format:</span></span>
  * <span data-ttu-id="666da-201">item (tekenreeks) - de unieke id van het Hallo-item.</span><span class="sxs-lookup"><span data-stu-id="666da-201">item (string) - Unique identifier of hello item.</span></span>
  * <span data-ttu-id="666da-202">aantal (int of string) - aantal items dat is aangeschaft.</span><span class="sxs-lookup"><span data-stu-id="666da-202">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="666da-203">prijs (float of tekenreeks) - optioneel veld - Hallo prijs van Hallo-item.</span><span class="sxs-lookup"><span data-stu-id="666da-203">price (float or string) - optional field - hello price of hello item.</span></span>

<span data-ttu-id="666da-204">Hallo in het volgende voorbeeld toont de aankoop van 3 items (33, 34, 35), twee met alle velden ingevuld (item, count, prijs) en één (item 34) zonder een prijs.</span><span class="sxs-lookup"><span data-stu-id="666da-204">hello example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="666da-205">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="666da-205">3.2.6.</span></span> <span data-ttu-id="666da-206">Gebruikersgebeurtenis-aanmelding</span><span class="sxs-lookup"><span data-stu-id="666da-206">User Login Event</span></span>
<span data-ttu-id="666da-207">Azure ML aanbevelingen gebeurtenis bibliotheek maakt en gebruikt een cookie in volgorde tooidentify gebeurtenissen die afkomstig zijn van Hallo dezelfde browser.</span><span class="sxs-lookup"><span data-stu-id="666da-207">Azure ML Recommendations Event library creates and use a cookie in order tooidentify events that came from hello same browser.</span></span> <span data-ttu-id="666da-208">In volgorde tooimprove Hallo model kunnen resultaten Azure ML aanbevelingen tooset een unieke gebruikers-id die het gebruik van Hallo cookie overschrijft.</span><span class="sxs-lookup"><span data-stu-id="666da-208">In order tooimprove hello model results Azure ML Recommendations enables tooset a user unique identification that will override hello cookie usage.</span></span>

<span data-ttu-id="666da-209">Deze gebeurtenis moet worden gebruikt na Hallo gebruiker aanmelding tooyour site.</span><span class="sxs-lookup"><span data-stu-id="666da-209">This event should be used after hello user login tooyour site.</span></span>

<span data-ttu-id="666da-210">Parameters:</span><span class="sxs-lookup"><span data-stu-id="666da-210">Parameters:</span></span>

* <span data-ttu-id="666da-211">gebeurtenis (tekenreeks) - 'userlogin'</span><span class="sxs-lookup"><span data-stu-id="666da-211">event (string) - “userlogin”</span></span>
* <span data-ttu-id="666da-212">gebruiker (tekenreeks) - unieke identificatie van het Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="666da-212">user (string) - unique identification of hello user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="666da-213">4. Aanbevelingen via JavaScript gebruiken</span><span class="sxs-lookup"><span data-stu-id="666da-213">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="666da-214">Hallo-code die Hallo aanbeveling verbruikt wordt door sommige JavaScript-gebeurtenis geactiveerd door webpagina Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="666da-214">hello code that consumes hello recommendation is triggered by some JavaScript event by hello client’s webpage.</span></span> <span data-ttu-id="666da-215">Hallo aanbeveling antwoord bevat Hallo aanbevolen items-id's, namen en hun classificatie.</span><span class="sxs-lookup"><span data-stu-id="666da-215">hello recommendation response includes hello recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="666da-216">Het is aanbevolen toouse deze optie alleen voor een lijst weergeven van Hallo aanbevolen items - complexere verwerken (zoals het toevoegen van het item Hallo metagegevens) moet worden gedaan op Hallo server side-integratie.</span><span class="sxs-lookup"><span data-stu-id="666da-216">It’s best toouse this option only for a list display of hello recommended items - more complex handling (such as adding hello item’s metadata) should be done on hello server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="666da-217">4.1 aanbevelingen gebruiken</span><span class="sxs-lookup"><span data-stu-id="666da-217">4.1 Consume Recommendations</span></span>
<span data-ttu-id="666da-218">tooconsume aanbevelingen moet u tooinclude Hallo vereist JavaScript-bibliotheken in uw pagina en toocall AzureMLRecommendationsStart.</span><span class="sxs-lookup"><span data-stu-id="666da-218">tooconsume recommendations you need tooinclude hello required JavaScript libraries in your page and toocall AzureMLRecommendationsStart.</span></span> <span data-ttu-id="666da-219">Zie de sectie 2.</span><span class="sxs-lookup"><span data-stu-id="666da-219">See section 2.</span></span>

<span data-ttu-id="666da-220">tooconsume aanbevelingen voor een of meer items moet u een methode aangeroepen toocall: AzureMLRecommendationsGetI2IRecommendation.</span><span class="sxs-lookup"><span data-stu-id="666da-220">tooconsume recommendations for one or more items you need toocall a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="666da-221">Parameters:</span><span class="sxs-lookup"><span data-stu-id="666da-221">Parameters:</span></span>

* <span data-ttu-id="666da-222">Een of meer items tooget aanbevelingen voor de (matrix met tekenreeksen) - artikelen.</span><span class="sxs-lookup"><span data-stu-id="666da-222">items (array of strings) - One or more items tooget recommendations for.</span></span> <span data-ttu-id="666da-223">Als u een build Fbt verbruiken kunt vervolgens u instellen hier slechts één item.</span><span class="sxs-lookup"><span data-stu-id="666da-223">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="666da-224">numberOfResults (int) - aantal vereiste resultaten.</span><span class="sxs-lookup"><span data-stu-id="666da-224">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="666da-225">includeMetadata (boolean, optioneel) - als too'true ingesteld ' geeft aan dat Hallo metagegevens-veld moet gevuld worden in Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="666da-225">includeMetadata (boolean, optional) - if set too‘true’ indicates that hello metadata field must be populated in hello result.</span></span>
* <span data-ttu-id="666da-226">Verwerking van de functie, een functie die wordt afgehandeld Hallo aanbevelingen geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="666da-226">Processing function - a function that will handle hello recommendations returned.</span></span> <span data-ttu-id="666da-227">Hallo-gegevens worden geretourneerd als een matrix met:</span><span class="sxs-lookup"><span data-stu-id="666da-227">hello data is returned as an array of:</span></span>
  * <span data-ttu-id="666da-228">Artikel - item unieke id</span><span class="sxs-lookup"><span data-stu-id="666da-228">Item - item unique id</span></span>
  * <span data-ttu-id="666da-229">naam - item naam (indien aanwezig zijn in de catalogus)</span><span class="sxs-lookup"><span data-stu-id="666da-229">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="666da-230">beoordeling - aanbeveling waardering</span><span class="sxs-lookup"><span data-stu-id="666da-230">rating - recommendation rating</span></span>
  * <span data-ttu-id="666da-231">metagegevens - een tekenreeks met metagegevens Hallo Hallo-item</span><span class="sxs-lookup"><span data-stu-id="666da-231">metadata - a string that represents hello metadata of hello item</span></span>

<span data-ttu-id="666da-232">Voorbeeld: 8 aanbevelingen voor het item '64f6eb0d-947a-4c18-a16c-888da9e228ba' hello na de code-aanvragen (en op te geven niet includeMetadata - wordt impliciet aangegeven dat er geen metagegevens vereist is), het Hallo-resultaten vervolgens samenvoegen in een buffer.</span><span class="sxs-lookup"><span data-stu-id="666da-232">Example: hello following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate hello results into a buffer.</span></span>

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
