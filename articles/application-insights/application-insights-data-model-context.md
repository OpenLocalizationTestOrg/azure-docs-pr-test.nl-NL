---
title: Azure Application Insights telemetrie gegevensmodel - telemetrie Context | Microsoft Docs
description: Application Insights telemetrie context-gegevensmodel
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: d6a0cad8bda6ca68aa691867e84f540c5ac9f6f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="97df2-103">Telemetrie-context: Application Insights-gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="97df2-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="97df2-104">Elk telemetrie-item heeft mogelijk een sterk getypeerde context-velden.</span><span class="sxs-lookup"><span data-stu-id="97df2-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="97df2-105">Elk veld kunt een specifiek scenario voor bewaking.</span><span class="sxs-lookup"><span data-stu-id="97df2-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="97df2-106">Gebruik de verzameling aangepaste eigenschappen aangepaste of toepassingsspecifieke contextuele informatie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="97df2-106">Use the custom properties collection to store custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="97df2-107">Toepassingsversie</span><span class="sxs-lookup"><span data-stu-id="97df2-107">Application version</span></span>

<span data-ttu-id="97df2-108">Informatie in de velden van de context is altijd over de toepassing die de telemetrie verzendt.</span><span class="sxs-lookup"><span data-stu-id="97df2-108">Information in the application context fields is always about the application that is sending the telemetry.</span></span> <span data-ttu-id="97df2-109">Toepassingsversie wordt gebruikt voor het analyseren van wijzigingen van de trend in het gedrag van toepassingen en correlatie voor de implementaties.</span><span class="sxs-lookup"><span data-stu-id="97df2-109">Application version is used to analyze trend changes in the application behavior and its correlation to the deployments.</span></span>

<span data-ttu-id="97df2-110">Maximale lengte: 1024</span><span class="sxs-lookup"><span data-stu-id="97df2-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="97df2-111">IP-clientadres</span><span class="sxs-lookup"><span data-stu-id="97df2-111">Client IP address</span></span>

<span data-ttu-id="97df2-112">Het IP-adres van het clientapparaat.</span><span class="sxs-lookup"><span data-stu-id="97df2-112">The IP address of the client device.</span></span> <span data-ttu-id="97df2-113">IPv4 en IPv6 worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="97df2-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="97df2-114">Wanneer telemetrie van een service wordt verzonden, wordt de locatie-context is over de gebruiker die de bewerking in de service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="97df2-114">When telemetry is sent from a service, the location context is about the user that initiated the operation in the service.</span></span> <span data-ttu-id="97df2-115">Application Insights geografische locatie gegevens ophalen uit de client-IP en vervolgens worden afgekapt.</span><span class="sxs-lookup"><span data-stu-id="97df2-115">Application Insights extract the geo-location information from the client IP and then truncate it.</span></span> <span data-ttu-id="97df2-116">Client-IP op zichzelf kan dus niet worden gebruikt als identificeerbare informatie voor de eindgebruiker.</span><span class="sxs-lookup"><span data-stu-id="97df2-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="97df2-117">Maximale lengte: 46</span><span class="sxs-lookup"><span data-stu-id="97df2-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="97df2-118">Apparaattype</span><span class="sxs-lookup"><span data-stu-id="97df2-118">Device type</span></span>

<span data-ttu-id="97df2-119">Dit veld is oorspronkelijk gebruikt om aan te geven van het type van het apparaat dat de eindgebruiker van de toepassing wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="97df2-119">Originally this field was used to indicate the type of the device the end user of the application is using.</span></span> <span data-ttu-id="97df2-120">Vandaag de dag worden gebruikt voor het onderscheiden van JavaScript telemetrie met het apparaattype typt 'PC' u 'Browser"serverzijde telemetrie met het apparaat.</span><span class="sxs-lookup"><span data-stu-id="97df2-120">Today used primarily to distinguish JavaScript telemetry with the device type 'Browser' from server-side telemetry with the device type 'PC'.</span></span>

<span data-ttu-id="97df2-121">Maximale lengte: 64</span><span class="sxs-lookup"><span data-stu-id="97df2-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="97df2-122">Bewerkings-id</span><span class="sxs-lookup"><span data-stu-id="97df2-122">Operation id</span></span>

<span data-ttu-id="97df2-123">Een unieke id van de basis-bewerking.</span><span class="sxs-lookup"><span data-stu-id="97df2-123">A unique identifier of the root operation.</span></span> <span data-ttu-id="97df2-124">Deze id kunt groep telemetrie over meerdere onderdelen.</span><span class="sxs-lookup"><span data-stu-id="97df2-124">This identifier allows to group telemetry across multiple components.</span></span> <span data-ttu-id="97df2-125">Zie [telemetrie correlatie](application-insights-correlation.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="97df2-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="97df2-126">De bewerkings-id is gemaakt door een aanvraag of een paginaweergave.</span><span class="sxs-lookup"><span data-stu-id="97df2-126">The operation id is created by either a request or a page view.</span></span> <span data-ttu-id="97df2-127">Dit veld alle andere telemetrie ingesteld op de waarde voor de weergave van het insluitende aanvraag of pagina.</span><span class="sxs-lookup"><span data-stu-id="97df2-127">All other telemetry sets this field to the value for the containing request or page view.</span></span> 

<span data-ttu-id="97df2-128">Maximale lengte: 128</span><span class="sxs-lookup"><span data-stu-id="97df2-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="97df2-129">Bovenliggende bewerkings-ID</span><span class="sxs-lookup"><span data-stu-id="97df2-129">Parent operation ID</span></span>

<span data-ttu-id="97df2-130">De unieke id van bovenliggende venster van de telemetrie-item.</span><span class="sxs-lookup"><span data-stu-id="97df2-130">The unique identifier of the telemetry item's immediate parent.</span></span> <span data-ttu-id="97df2-131">Zie [telemetrie correlatie](application-insights-correlation.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="97df2-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="97df2-132">Maximale lengte: 128</span><span class="sxs-lookup"><span data-stu-id="97df2-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="97df2-133">De naam van bewerking</span><span class="sxs-lookup"><span data-stu-id="97df2-133">Operation name</span></span>

<span data-ttu-id="97df2-134">De naam (groeps) van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="97df2-134">The name (group) of the operation.</span></span> <span data-ttu-id="97df2-135">De naam van de bewerking wordt gemaakt door een aanvraag of een paginaweergave.</span><span class="sxs-lookup"><span data-stu-id="97df2-135">The operation name is created by either a request or a page view.</span></span> <span data-ttu-id="97df2-136">Dit veld instelt alle telemetrie-items op de waarde voor de weergave van het insluitende aanvraag of pagina.</span><span class="sxs-lookup"><span data-stu-id="97df2-136">All other telemetry items set this field to the value for the containing request or page view.</span></span> <span data-ttu-id="97df2-137">Naam van de bewerking wordt gebruikt voor het zoeken naar alle telemetrie-items voor een groep bewerkingen (bijvoorbeeld ' GET-startpagina/Index').</span><span class="sxs-lookup"><span data-stu-id="97df2-137">Operation name is used for finding all the telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="97df2-138">Deze contexteigenschap wordt gebruikt om te beantwoorden vragen zoals "Wat zijn de gebruikelijke uitzonderingen op deze pagina."</span><span class="sxs-lookup"><span data-stu-id="97df2-138">This context property is used to answer questions like "what are the typical exceptions thrown on this page."</span></span>

<span data-ttu-id="97df2-139">Maximale lengte: 1024</span><span class="sxs-lookup"><span data-stu-id="97df2-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-the-operation"></a><span data-ttu-id="97df2-140">Synthetische bron van de bewerking</span><span class="sxs-lookup"><span data-stu-id="97df2-140">Synthetic source of the operation</span></span>

<span data-ttu-id="97df2-141">Naam van de synthetische bron.</span><span class="sxs-lookup"><span data-stu-id="97df2-141">Name of synthetic source.</span></span> <span data-ttu-id="97df2-142">Telemetrie van de toepassing mogelijk synthetisch verkeer vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="97df2-142">Some telemetry from the application may represent synthetic traffic.</span></span> <span data-ttu-id="97df2-143">Webcrawler indexeren van de website, site-beschikbaarheidstests of traces van diagnostische bibliotheken zoals Application Insights-SDK zelf kan zijn.</span><span class="sxs-lookup"><span data-stu-id="97df2-143">It may be web crawler indexing the web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="97df2-144">Maximale lengte: 1024</span><span class="sxs-lookup"><span data-stu-id="97df2-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="97df2-145">Sessie-id</span><span class="sxs-lookup"><span data-stu-id="97df2-145">Session id</span></span>

<span data-ttu-id="97df2-146">Sessie-ID - het exemplaar van de gebruikersinteractie met de app.</span><span class="sxs-lookup"><span data-stu-id="97df2-146">Session ID - the instance of the user's interaction with the app.</span></span> <span data-ttu-id="97df2-147">Gegevens in de context sessie velden is altijd over de eindgebruiker.</span><span class="sxs-lookup"><span data-stu-id="97df2-147">Information in the session context fields is always about the end user.</span></span> <span data-ttu-id="97df2-148">Wanneer telemetrie van een service wordt verzonden, wordt de sessiecontext is over de gebruiker die de bewerking in de service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="97df2-148">When telemetry is sent from a service, the session context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="97df2-149">Maximale lengte: 64</span><span class="sxs-lookup"><span data-stu-id="97df2-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="97df2-150">Anonieme gebruikers-id</span><span class="sxs-lookup"><span data-stu-id="97df2-150">Anonymous user id</span></span>

<span data-ttu-id="97df2-151">Anonieme gebruikers-id.</span><span class="sxs-lookup"><span data-stu-id="97df2-151">Anonymous user id.</span></span> <span data-ttu-id="97df2-152">Hiermee geeft u de gebruiker van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="97df2-152">Represents the end user of the application.</span></span> <span data-ttu-id="97df2-153">Wanneer telemetrie van een service wordt verzonden, is de context van de gebruiker over de gebruiker die de bewerking in de service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="97df2-153">When telemetry is sent from a service, the user context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="97df2-154">[Steekproef nemen](app-insights-sampling.md) is een van de technieken om de hoeveelheid verzamelde telemetriegegevens te minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="97df2-154">[Sampling](app-insights-sampling.md) is one of the techniques to minimize the amount of collected telemetry.</span></span> <span data-ttu-id="97df2-155">Steekproeven algoritme probeert met een steekproef in of uit de gecorreleerde telemetrie.</span><span class="sxs-lookup"><span data-stu-id="97df2-155">Sampling algorithm attempts to either sample in or out all the correlated telemetry.</span></span> <span data-ttu-id="97df2-156">Anonieme gebruikers-id wordt gebruikt voor de steekproef nemen score generatie.</span><span class="sxs-lookup"><span data-stu-id="97df2-156">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="97df2-157">Anonieme gebruikers-id moet dus een willekeurige genoeg waarde.</span><span class="sxs-lookup"><span data-stu-id="97df2-157">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="97df2-158">Met anonieme gebruikers-id voor het opslaan van de gebruikersnaam is een misbruik van het veld.</span><span class="sxs-lookup"><span data-stu-id="97df2-158">Using anonymous user id to store user name is a misuse of the field.</span></span> <span data-ttu-id="97df2-159">Geverifieerde gebruikers-id gebruiken.</span><span class="sxs-lookup"><span data-stu-id="97df2-159">Use Authenticated user id.</span></span>

<span data-ttu-id="97df2-160">Maximale lengte: 128</span><span class="sxs-lookup"><span data-stu-id="97df2-160">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="97df2-161">Geverifieerde gebruikers-id</span><span class="sxs-lookup"><span data-stu-id="97df2-161">Authenticated user id</span></span>

<span data-ttu-id="97df2-162">Geverifieerde gebruikers-id.</span><span class="sxs-lookup"><span data-stu-id="97df2-162">Authenticated user id.</span></span> <span data-ttu-id="97df2-163">Het tegenovergestelde van anonieme gebruikers-id, dit veld wordt de gebruiker met een beschrijvende naam.</span><span class="sxs-lookup"><span data-stu-id="97df2-163">The opposite of anonymous user id, this field represents the user with a friendly name.</span></span> <span data-ttu-id="97df2-164">Sinds de persoonlijke gegevens is deze standaard niet verzameld door de meeste SDK.</span><span class="sxs-lookup"><span data-stu-id="97df2-164">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="97df2-165">Maximale lengte: 1024</span><span class="sxs-lookup"><span data-stu-id="97df2-165">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="97df2-166">Account-id</span><span class="sxs-lookup"><span data-stu-id="97df2-166">Account id</span></span>

<span data-ttu-id="97df2-167">Dit is de account-ID of naam, die de gebruiker met optreedt in een multitenant-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="97df2-167">In multi-tenant applications this is the account ID or name, which the user is acting with.</span></span> <span data-ttu-id="97df2-168">Voorbeelden mogelijk abonnements-ID voor de Azure portal of blog naam weblog-platform.</span><span class="sxs-lookup"><span data-stu-id="97df2-168">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="97df2-169">Maximale lengte: 1024</span><span class="sxs-lookup"><span data-stu-id="97df2-169">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="97df2-170">Cloud-rol</span><span class="sxs-lookup"><span data-stu-id="97df2-170">Cloud role</span></span>

<span data-ttu-id="97df2-171">Naam van de rol van de toepassing is een onderdeel van.</span><span class="sxs-lookup"><span data-stu-id="97df2-171">Name of the role the application is a part of.</span></span> <span data-ttu-id="97df2-172">Maps rechtstreeks naar de naam van de rol in azure.</span><span class="sxs-lookup"><span data-stu-id="97df2-172">Maps directly to the role name in azure.</span></span> <span data-ttu-id="97df2-173">Kan ook worden gebruikt om te onderscheiden micro services die deel van één toepassing uitmaken.</span><span class="sxs-lookup"><span data-stu-id="97df2-173">Can also be used to distinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="97df2-174">Maximale lengte: 256</span><span class="sxs-lookup"><span data-stu-id="97df2-174">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="97df2-175">Cloud-rolinstantie</span><span class="sxs-lookup"><span data-stu-id="97df2-175">Cloud role instance</span></span>

<span data-ttu-id="97df2-176">Naam van het exemplaar waarop de toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="97df2-176">Name of the instance where the application is running.</span></span> <span data-ttu-id="97df2-177">Computernaam voor on-premises exemplaarnaam voor Azure.</span><span class="sxs-lookup"><span data-stu-id="97df2-177">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="97df2-178">Maximale lengte: 256</span><span class="sxs-lookup"><span data-stu-id="97df2-178">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="97df2-179">Intern: SDK-versie</span><span class="sxs-lookup"><span data-stu-id="97df2-179">Internal: SDK version</span></span>

<span data-ttu-id="97df2-180">SDK-versie.</span><span class="sxs-lookup"><span data-stu-id="97df2-180">SDK version.</span></span> <span data-ttu-id="97df2-181">Zie https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="97df2-181">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="97df2-182">Maximale lengte: 64</span><span class="sxs-lookup"><span data-stu-id="97df2-182">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="97df2-183">Intern: Naam van het knooppunt</span><span class="sxs-lookup"><span data-stu-id="97df2-183">Internal: Node name</span></span>

<span data-ttu-id="97df2-184">Dit veld wordt de naam van het knooppunt voor facturering doeleinden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="97df2-184">This field represents the node name used for billing purposes.</span></span> <span data-ttu-id="97df2-185">Gebruik dit voor het overschrijven van de standaard detectie van knooppunten.</span><span class="sxs-lookup"><span data-stu-id="97df2-185">Use it to override the standard detection of nodes.</span></span>

<span data-ttu-id="97df2-186">Maximale lengte: 256</span><span class="sxs-lookup"><span data-stu-id="97df2-186">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="97df2-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="97df2-187">Next steps</span></span>

- <span data-ttu-id="97df2-188">Meer informatie over hoe [uitbreiden en het filteren van telemetrie](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="97df2-188">Learn how to [extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="97df2-189">Zie [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.</span><span class="sxs-lookup"><span data-stu-id="97df2-189">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="97df2-190">Bekijk standaard context eigenschappen verzameling [configuratie](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span><span class="sxs-lookup"><span data-stu-id="97df2-190">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
