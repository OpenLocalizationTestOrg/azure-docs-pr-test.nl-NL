---
title: aaaAzure Application Insights telemetrie Data Model - telemetrie Context | Microsoft Docs
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
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="b9f59-103">Telemetrie-context: Application Insights-gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="b9f59-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="b9f59-104">Elk telemetrie-item heeft mogelijk een sterk getypeerde context-velden.</span><span class="sxs-lookup"><span data-stu-id="b9f59-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="b9f59-105">Elk veld kunt een specifiek scenario voor bewaking.</span><span class="sxs-lookup"><span data-stu-id="b9f59-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="b9f59-106">Gebruik Hallo aangepaste eigenschappen verzameling toostore aangepaste of toepassingsspecifieke contextuele informatie.</span><span class="sxs-lookup"><span data-stu-id="b9f59-106">Use hello custom properties collection toostore custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="b9f59-107">Toepassingsversie</span><span class="sxs-lookup"><span data-stu-id="b9f59-107">Application version</span></span>

<span data-ttu-id="b9f59-108">Informatie in de context de velden van Hallo is altijd over toepassing hello dat Hallo telemetrie verzendt.</span><span class="sxs-lookup"><span data-stu-id="b9f59-108">Information in hello application context fields is always about hello application that is sending hello telemetry.</span></span> <span data-ttu-id="b9f59-109">Toepassingsversie is gebruikte tooanalyze trend wijzigingen in gedrag van de toepassing hello en correlatie toohello implementaties.</span><span class="sxs-lookup"><span data-stu-id="b9f59-109">Application version is used tooanalyze trend changes in hello application behavior and its correlation toohello deployments.</span></span>

<span data-ttu-id="b9f59-110">Maximale lengte: 1024</span><span class="sxs-lookup"><span data-stu-id="b9f59-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="b9f59-111">IP-clientadres</span><span class="sxs-lookup"><span data-stu-id="b9f59-111">Client IP address</span></span>

<span data-ttu-id="b9f59-112">Hallo IP-adres van het clientapparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="b9f59-112">hello IP address of hello client device.</span></span> <span data-ttu-id="b9f59-113">IPv4 en IPv6 worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b9f59-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="b9f59-114">Wanneer telemetrie van een service wordt verzonden, is het Hallo locatie context over Hallo-gebruiker die Hallo-bewerking in Hallo-service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="b9f59-114">When telemetry is sent from a service, hello location context is about hello user that initiated hello operation in hello service.</span></span> <span data-ttu-id="b9f59-115">Application Insights Hallo geografische locatie gegevens extraheren uit Hallo client-IP- en vervolgens worden afgekapt.</span><span class="sxs-lookup"><span data-stu-id="b9f59-115">Application Insights extract hello geo-location information from hello client IP and then truncate it.</span></span> <span data-ttu-id="b9f59-116">Client-IP op zichzelf kan dus niet worden gebruikt als identificeerbare informatie voor de eindgebruiker.</span><span class="sxs-lookup"><span data-stu-id="b9f59-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="b9f59-117">Maximale lengte: 46</span><span class="sxs-lookup"><span data-stu-id="b9f59-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="b9f59-118">Apparaattype</span><span class="sxs-lookup"><span data-stu-id="b9f59-118">Device type</span></span>

<span data-ttu-id="b9f59-119">Oorspronkelijk dit veld is gebruikt tooindicate Hallo Hallo apparaat Hallo eindgebruiker van de toepassing hello wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b9f59-119">Originally this field was used tooindicate hello type of hello device hello end user of hello application is using.</span></span> <span data-ttu-id="b9f59-120">Vandaag voornamelijk toodistinguish JavaScript telemetrie met Hallo apparaattype "Browser" vanuit serverzijde telemetrie met apparaattype Hallo 'PC' gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b9f59-120">Today used primarily toodistinguish JavaScript telemetry with hello device type 'Browser' from server-side telemetry with hello device type 'PC'.</span></span>

<span data-ttu-id="b9f59-121">Maximale lengte: 64</span><span class="sxs-lookup"><span data-stu-id="b9f59-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="b9f59-122">Bewerkings-id</span><span class="sxs-lookup"><span data-stu-id="b9f59-122">Operation id</span></span>

<span data-ttu-id="b9f59-123">Een unieke id van Hallo basis-bewerking.</span><span class="sxs-lookup"><span data-stu-id="b9f59-123">A unique identifier of hello root operation.</span></span> <span data-ttu-id="b9f59-124">Deze id kunt toogroup telemetrie over meerdere onderdelen.</span><span class="sxs-lookup"><span data-stu-id="b9f59-124">This identifier allows toogroup telemetry across multiple components.</span></span> <span data-ttu-id="b9f59-125">Zie [telemetrie correlatie](application-insights-correlation.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b9f59-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="b9f59-126">Hallo bewerkings-id is gemaakt door een aanvraag of een paginaweergave.</span><span class="sxs-lookup"><span data-stu-id="b9f59-126">hello operation id is created by either a request or a page view.</span></span> <span data-ttu-id="b9f59-127">Alle andere telemetrie stelt deze veldwaarde toohello voor Hallo met aanvraag of paginaweergave.</span><span class="sxs-lookup"><span data-stu-id="b9f59-127">All other telemetry sets this field toohello value for hello containing request or page view.</span></span> 

<span data-ttu-id="b9f59-128">Maximale lengte: 128</span><span class="sxs-lookup"><span data-stu-id="b9f59-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="b9f59-129">Bovenliggende bewerkings-ID</span><span class="sxs-lookup"><span data-stu-id="b9f59-129">Parent operation ID</span></span>

<span data-ttu-id="b9f59-130">de unieke id van de direct bovenliggende Hallo telemetrie item Hallo.</span><span class="sxs-lookup"><span data-stu-id="b9f59-130">hello unique identifier of hello telemetry item's immediate parent.</span></span> <span data-ttu-id="b9f59-131">Zie [telemetrie correlatie](application-insights-correlation.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b9f59-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="b9f59-132">Maximale lengte: 128</span><span class="sxs-lookup"><span data-stu-id="b9f59-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="b9f59-133">De naam van bewerking</span><span class="sxs-lookup"><span data-stu-id="b9f59-133">Operation name</span></span>

<span data-ttu-id="b9f59-134">Hallo-naam (groeps) van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="b9f59-134">hello name (group) of hello operation.</span></span> <span data-ttu-id="b9f59-135">naam van de bewerking Hello wordt gemaakt door een aanvraag of een paginaweergave.</span><span class="sxs-lookup"><span data-stu-id="b9f59-135">hello operation name is created by either a request or a page view.</span></span> <span data-ttu-id="b9f59-136">Alle overige telemetrie-items in dit veld toohello waarde instellen voor Hallo met aanvraag of paginaweergave.</span><span class="sxs-lookup"><span data-stu-id="b9f59-136">All other telemetry items set this field toohello value for hello containing request or page view.</span></span> <span data-ttu-id="b9f59-137">Naam van de bewerking wordt gebruikt voor het zoeken naar alle Hallo telemetrie-items voor een groep bewerkingen (bijvoorbeeld ' GET-startpagina/Index').</span><span class="sxs-lookup"><span data-stu-id="b9f59-137">Operation name is used for finding all hello telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="b9f59-138">Deze contexteigenschap is gebruikte tooanswer vragen zoals "Wat zijn Hallo typische uitzonderingen op deze pagina."</span><span class="sxs-lookup"><span data-stu-id="b9f59-138">This context property is used tooanswer questions like "what are hello typical exceptions thrown on this page."</span></span>

<span data-ttu-id="b9f59-139">Maximale lengte: 1024</span><span class="sxs-lookup"><span data-stu-id="b9f59-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-hello-operation"></a><span data-ttu-id="b9f59-140">Synthetische bron van het Hallo-bewerking</span><span class="sxs-lookup"><span data-stu-id="b9f59-140">Synthetic source of hello operation</span></span>

<span data-ttu-id="b9f59-141">Naam van de synthetische bron.</span><span class="sxs-lookup"><span data-stu-id="b9f59-141">Name of synthetic source.</span></span> <span data-ttu-id="b9f59-142">Telemetrie van de toepassing hello synthetisch verkeer kan worden aangeduid.</span><span class="sxs-lookup"><span data-stu-id="b9f59-142">Some telemetry from hello application may represent synthetic traffic.</span></span> <span data-ttu-id="b9f59-143">Web crawler indexering Hallo-website, site-beschikbaarheidstests of traces van diagnostische bibliotheken zoals Application Insights-SDK zelf kan zijn.</span><span class="sxs-lookup"><span data-stu-id="b9f59-143">It may be web crawler indexing hello web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="b9f59-144">Maximale lengte: 1024</span><span class="sxs-lookup"><span data-stu-id="b9f59-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="b9f59-145">Sessie-id</span><span class="sxs-lookup"><span data-stu-id="b9f59-145">Session id</span></span>

<span data-ttu-id="b9f59-146">Sessie-ID - Hallo exemplaar van Hallo van gebruikersinteractie met Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="b9f59-146">Session ID - hello instance of hello user's interaction with hello app.</span></span> <span data-ttu-id="b9f59-147">Hallo sessie context velden is altijd over Hallo eindgebruiker.</span><span class="sxs-lookup"><span data-stu-id="b9f59-147">Information in hello session context fields is always about hello end user.</span></span> <span data-ttu-id="b9f59-148">Wanneer telemetrie van een service wordt verzonden, is het Hallo sessiecontext over Hallo-gebruiker die Hallo-bewerking in Hallo-service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="b9f59-148">When telemetry is sent from a service, hello session context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="b9f59-149">Maximale lengte: 64</span><span class="sxs-lookup"><span data-stu-id="b9f59-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="b9f59-150">Anonieme gebruikers-id</span><span class="sxs-lookup"><span data-stu-id="b9f59-150">Anonymous user id</span></span>

<span data-ttu-id="b9f59-151">Anonieme gebruikers-id. De eindgebruiker Hallo van de toepassing hello vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="b9f59-151">Anonymous user id. Represents hello end user of hello application.</span></span> <span data-ttu-id="b9f59-152">Wanneer telemetrie van een service wordt verzonden, is het Hallo gebruikerscontext over Hallo-gebruiker die Hallo-bewerking in Hallo-service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="b9f59-152">When telemetry is sent from a service, hello user context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="b9f59-153">[Steekproef nemen](app-insights-sampling.md) is een Hallo technieken toominimize Hallo hoeveelheid verzamelde telemetrie.</span><span class="sxs-lookup"><span data-stu-id="b9f59-153">[Sampling](app-insights-sampling.md) is one of hello techniques toominimize hello amount of collected telemetry.</span></span> <span data-ttu-id="b9f59-154">Steekproef nemen algoritme pogingen tooeither gecorreleerde voorbeeld in- of alle Hallo telemetrie.</span><span class="sxs-lookup"><span data-stu-id="b9f59-154">Sampling algorithm attempts tooeither sample in or out all hello correlated telemetry.</span></span> <span data-ttu-id="b9f59-155">Anonieme gebruikers-id wordt gebruikt voor de steekproef nemen score generatie.</span><span class="sxs-lookup"><span data-stu-id="b9f59-155">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="b9f59-156">Anonieme gebruikers-id moet dus een willekeurige genoeg waarde.</span><span class="sxs-lookup"><span data-stu-id="b9f59-156">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="b9f59-157">Met anonieme gebruiker-id toostore gebruikersnaam is een misbruik van Hallo-veld.</span><span class="sxs-lookup"><span data-stu-id="b9f59-157">Using anonymous user id toostore user name is a misuse of hello field.</span></span> <span data-ttu-id="b9f59-158">Geverifieerde gebruikers-id gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b9f59-158">Use Authenticated user id.</span></span>

<span data-ttu-id="b9f59-159">Maximale lengte: 128</span><span class="sxs-lookup"><span data-stu-id="b9f59-159">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="b9f59-160">Geverifieerde gebruikers-id</span><span class="sxs-lookup"><span data-stu-id="b9f59-160">Authenticated user id</span></span>

<span data-ttu-id="b9f59-161">Geverifieerde gebruikers-id. Hallo tegenovergestelde van anonieme gebruikers-id, dit veld vertegenwoordigt Hallo-gebruiker met een beschrijvende naam.</span><span class="sxs-lookup"><span data-stu-id="b9f59-161">Authenticated user id. hello opposite of anonymous user id, this field represents hello user with a friendly name.</span></span> <span data-ttu-id="b9f59-162">Sinds de persoonlijke gegevens is deze standaard niet verzameld door de meeste SDK.</span><span class="sxs-lookup"><span data-stu-id="b9f59-162">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="b9f59-163">Maximale lengte: 1024</span><span class="sxs-lookup"><span data-stu-id="b9f59-163">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="b9f59-164">Account-id</span><span class="sxs-lookup"><span data-stu-id="b9f59-164">Account id</span></span>

<span data-ttu-id="b9f59-165">Dit is in toepassingen met meerdere tenants Hallo account-ID of naam, welke gebruiker Hallo met fungeert.</span><span class="sxs-lookup"><span data-stu-id="b9f59-165">In multi-tenant applications this is hello account ID or name, which hello user is acting with.</span></span> <span data-ttu-id="b9f59-166">Voorbeelden mogelijk abonnements-ID voor de Azure portal of blog naam weblog-platform.</span><span class="sxs-lookup"><span data-stu-id="b9f59-166">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="b9f59-167">Maximale lengte: 1024</span><span class="sxs-lookup"><span data-stu-id="b9f59-167">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="b9f59-168">Cloud-rol</span><span class="sxs-lookup"><span data-stu-id="b9f59-168">Cloud role</span></span>

<span data-ttu-id="b9f59-169">Naam van Hallo rol Hallo toepassing uitmaakt deel van.</span><span class="sxs-lookup"><span data-stu-id="b9f59-169">Name of hello role hello application is a part of.</span></span> <span data-ttu-id="b9f59-170">Maps rechtstreeks toohello rolnaam in azure.</span><span class="sxs-lookup"><span data-stu-id="b9f59-170">Maps directly toohello role name in azure.</span></span> <span data-ttu-id="b9f59-171">Ook kan worden veroorzaakt gebruikte toodistinguish micro services die deel van één toepassing uitmaken.</span><span class="sxs-lookup"><span data-stu-id="b9f59-171">Can also be used toodistinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="b9f59-172">Maximale lengte: 256</span><span class="sxs-lookup"><span data-stu-id="b9f59-172">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="b9f59-173">Cloud-rolinstantie</span><span class="sxs-lookup"><span data-stu-id="b9f59-173">Cloud role instance</span></span>

<span data-ttu-id="b9f59-174">Naam van het Hallo-exemplaar waarop de toepassing hello wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b9f59-174">Name of hello instance where hello application is running.</span></span> <span data-ttu-id="b9f59-175">Computernaam voor on-premises exemplaarnaam voor Azure.</span><span class="sxs-lookup"><span data-stu-id="b9f59-175">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="b9f59-176">Maximale lengte: 256</span><span class="sxs-lookup"><span data-stu-id="b9f59-176">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="b9f59-177">Intern: SDK-versie</span><span class="sxs-lookup"><span data-stu-id="b9f59-177">Internal: SDK version</span></span>

<span data-ttu-id="b9f59-178">SDK-versie.</span><span class="sxs-lookup"><span data-stu-id="b9f59-178">SDK version.</span></span> <span data-ttu-id="b9f59-179">Zie https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b9f59-179">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="b9f59-180">Maximale lengte: 64</span><span class="sxs-lookup"><span data-stu-id="b9f59-180">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="b9f59-181">Intern: Naam van het knooppunt</span><span class="sxs-lookup"><span data-stu-id="b9f59-181">Internal: Node name</span></span>

<span data-ttu-id="b9f59-182">Dit veld vertegenwoordigt Hallo knooppuntnaam voor facturering doeleinden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b9f59-182">This field represents hello node name used for billing purposes.</span></span> <span data-ttu-id="b9f59-183">Gebruik deze toooverride Hallo standaard detectie van knooppunten.</span><span class="sxs-lookup"><span data-stu-id="b9f59-183">Use it toooverride hello standard detection of nodes.</span></span>

<span data-ttu-id="b9f59-184">Maximale lengte: 256</span><span class="sxs-lookup"><span data-stu-id="b9f59-184">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="b9f59-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b9f59-185">Next steps</span></span>

- <span data-ttu-id="b9f59-186">Meer informatie over hoe te[uitbreiden en het filteren van telemetrie](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="b9f59-186">Learn how too[extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="b9f59-187">Zie [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.</span><span class="sxs-lookup"><span data-stu-id="b9f59-187">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="b9f59-188">Bekijk standaard context eigenschappen verzameling [configuratie](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span><span class="sxs-lookup"><span data-stu-id="b9f59-188">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
