---
title: aaaManage uw eerste API in Azure API Management | Microsoft Docs
description: Ontdek hoe toocreate API's, bewerkingen toevoegen en aan de slag met API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="c1d8b-103">Uw eerste API beheren in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="c1d8b-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="c1d8b-104"><a name="overview"> </a>Overzicht</span><span class="sxs-lookup"><span data-stu-id="c1d8b-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="c1d8b-105">Deze handleiding wordt beschreven hoe tooquickly aan de slag met Azure API Management en uw eerste API-aanroep.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-105">This guide shows you how tooquickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="c1d8b-106"><a name="concepts"> </a>Wat is Azure API Management?</span><span class="sxs-lookup"><span data-stu-id="c1d8b-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="c1d8b-107">U kunt elke back-end voor Azure API Management tootake gebruiken en start een volwaardig API-programma op basis van deze.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-107">You can use Azure API Management tootake any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="c1d8b-108">Algemene scenario's omvatten de volgende:</span><span class="sxs-lookup"><span data-stu-id="c1d8b-108">Common scenarios include:</span></span>

* <span data-ttu-id="c1d8b-109">**Mobiele infrastructuur beveiligen** door het beperken van toegang met API-sleutels, het voorkomen van DOS-aanvallen door middel van beperking, of het gebruiken van geavanceerd beveiligingsbeleid zoals validatie van JWT-tokens.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="c1d8b-110">**ISV-partner-partnerecosystemen inschakelen** door het aanbieden van snelle onboarding via Hallo developer-portal en het bouwen van een API-façade toodecouple van interne implementaties die zijn niet gereed zijn voor partner.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through hello developer portal and building an API facade toodecouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="c1d8b-111">**Een intern API-programma uitvoeren** door het aanbieden van een centrale locatie voor Hallo organisatie toocommunicate over Hallo beschikbaarheid en de meest recente tooAPIs wijzigt, beperken van toegang op basis van organisatieaccounts, alle gebaseerd op een veilig kanaal tussen Hallo API-gateway en het Hallo-back-end.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-111">**Running an internal API program** by offering a centralized location for hello organization toocommunicate about hello availability and latest changes tooAPIs, gating access based on organizational accounts, all based on a secured channel between hello API gateway and hello backend.</span></span>

<span data-ttu-id="c1d8b-112">Hallo-systeem bestaat uit Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="c1d8b-112">hello system is made up of hello following components:</span></span>

* <span data-ttu-id="c1d8b-113">Hallo **API-gateway** Hallo eindpunt waarmee:</span><span class="sxs-lookup"><span data-stu-id="c1d8b-113">hello **API gateway** is hello endpoint that:</span></span>
  
  * <span data-ttu-id="c1d8b-114">API-aanroepen ontvangen en doorgestuurd tooyour back-ends accepteert.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-114">Accepts API calls and routes them tooyour backends.</span></span>
  * <span data-ttu-id="c1d8b-115">API-sleutels, JWT-tokens, certificaten en andere referenties worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="c1d8b-116">Quota voor gebruik en frequentielimieten worden afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="c1d8b-117">Hiermee transformeert u uw API snel Hallo zonder codewijzigingen.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-117">Transforms your API on hello fly without code modifications.</span></span>
  * <span data-ttu-id="c1d8b-118">Antwoorden van de back-end in de cache worden opgeslagen indien ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="c1d8b-119">Aanroepmetagegevens worden voor analysedoeleinden aan het logboek toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="c1d8b-120">Hallo **publicatieportal** is Hallo beheerinterface waar u uw API-programma instelt.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-120">hello **publisher portal** is hello administrative interface where you set up your API program.</span></span> <span data-ttu-id="c1d8b-121">Gebruik deze voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="c1d8b-121">Use it to:</span></span>
  
  * <span data-ttu-id="c1d8b-122">API-schema definiëren of importeren.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-122">Define or import API schema.</span></span>
  * <span data-ttu-id="c1d8b-123">API's verpakken in producten.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-123">Package APIs into products.</span></span>
  * <span data-ttu-id="c1d8b-124">Beleidsregels instellen zoals quota of transformaties voor Hallo API's.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-124">Set up policies like quotas or transformations on hello APIs.</span></span>
  * <span data-ttu-id="c1d8b-125">Inzicht krijgen van analytische gegevens.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="c1d8b-126">Gebruikers beheren.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-126">Manage users.</span></span>
* <span data-ttu-id="c1d8b-127">Hallo **ontwikkelaarsportal** fungeert als Hallo hoofdweb aanwezigheid voor ontwikkelaars, ze kunnen hier:</span><span class="sxs-lookup"><span data-stu-id="c1d8b-127">hello **developer portal** serves as hello main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="c1d8b-128">API-documentatie lezen.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-128">Read API documentation.</span></span>
  * <span data-ttu-id="c1d8b-129">Een API via de interactieve console Hallo uitproberen.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-129">Try out an API via hello interactive console.</span></span>
  * <span data-ttu-id="c1d8b-130">Een account maken en zich abonneren tooget API-sleutels.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-130">Create an account and subscribe tooget API keys.</span></span>
  * <span data-ttu-id="c1d8b-131">Analytische gegevens openen over hun eigen gebruik.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="c1d8b-132"><a name="create-service-instance"> </a>Een API Management-exemplaar maken</span><span class="sxs-lookup"><span data-stu-id="c1d8b-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="c1d8b-133">toocomplete in deze zelfstudie, moet u een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-133">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="c1d8b-134">Als u geen account hebt, kunt u binnen een paar minuten een gratis account maken.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="c1d8b-135">Zie [Gratis proefversie van Azure][Azure Free Trial] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="c1d8b-136">Hallo eerste stap bij het werken met API Management is toocreate een service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-136">hello first step in working with API Management is toocreate a service instance.</span></span> <span data-ttu-id="c1d8b-137">Meld u aan toohello [Azure Portal] [ Azure Portal] en klik op **nieuw**, **Web en mobiel**, **API Management**.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-137">Sign in toohello [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![Nieuw API Management-exemplaar][api-management-create-instance-menu]

<span data-ttu-id="c1d8b-139">Voor **naam**, Geef een unieke subdomeinnaam naam toouse voor Hallo service-URL.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-139">For **Name**, specify a unique sub-domain name toouse for hello service URL.</span></span>

<span data-ttu-id="c1d8b-140">Kies Hallo gewenst **abonnement**, **resourcegroep** en **locatie** voor uw service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-140">Choose hello desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="c1d8b-141">Voer **Contoso Ltd.** voor Hallo **organisatienaam**, en voer uw e-mailadres in Hallo **E-Mail beheerder** veld.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-141">Enter **Contoso Ltd.** for hello **Organization Name**, and enter your email address in hello **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="c1d8b-142">Dit e-mailadres wordt gebruikt voor meldingen van Hallo API Management-systeem.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-142">This email address is used for notifications from hello API Management system.</span></span> <span data-ttu-id="c1d8b-143">Zie voor meer informatie [hoe tooconfigure meldingen en e-mailsjablonen in Azure API Management][How tooconfigure notifications and email templates in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="c1d8b-143">For more information, see [How tooconfigure notifications and email templates in Azure API Management][How tooconfigure notifications and email templates in Azure API Management].</span></span>
> 
> 

![Nieuwe API Management-service][api-management-create-instance-step1]

<span data-ttu-id="c1d8b-145">Service-exemplaren van API Management zijn beschikbaar in drie categorieën: Developer, Standard en Premium.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-145">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="c1d8b-146">Hallo categorie Developer is voor ontwikkeling, testen en test API-programma's waar maximale beschikbaarheid niet van belang is.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-146">hello Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="c1d8b-147">In Hallo Standard en Premium-categorieën, kunt u uw aantal gereserveerde eenheid toohandle meer verkeer schalen.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-147">In hello Standard and Premium tiers, you can scale your reserved unit count toohandle more traffic.</span></span> <span data-ttu-id="c1d8b-148">Hallo-categorieën Standard en Premium bieden uw API Management-service met Hallo meeste verwerkingskracht en prestaties.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-148">hello Standard and Premium tiers provide your API Management service with hello most processing power and performance.</span></span> <span data-ttu-id="c1d8b-149">U kunt elke categorie gebruiken om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-149">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="c1d8b-150">Zie voor meer informatie over API Management-categorieën [API Management-prijzen][API Management pricing].</span><span class="sxs-lookup"><span data-stu-id="c1d8b-150">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="c1d8b-151">Klik op **maken** toostart inrichting van uw service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-151">Click **Create** toostart provisioning your service instance.</span></span>

![Nieuwe API Management-service][api-management-instance-created]

<span data-ttu-id="c1d8b-153">Zodra Hallo service-exemplaar is gemaakt, wordt de volgende stap Hallo toocreate is of een API importeren.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-153">Once hello service instance is created, hello next step is toocreate or import an API.</span></span>

## <span data-ttu-id="c1d8b-154"><a name="create-api"> </a>Een API importeren</span><span class="sxs-lookup"><span data-stu-id="c1d8b-154"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="c1d8b-155">Een API bestaat uit een reeks bewerkingen die vanuit een clienttoepassing kunnen worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-155">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="c1d8b-156">API-bewerkingen worden via proxy tooexisting webservices.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-156">API operations are proxied tooexisting web services.</span></span>

<span data-ttu-id="c1d8b-157">API's kunnen handmatig worden gemaakt (en bewerkingen kunnen handmatig worden toegevoegd) of ze kunnen worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-157">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="c1d8b-158">In deze zelfstudie importeren we Hallo API voor een voorbeeldrekenmachinewebservice door Microsoft geleverd en gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-158">In this tutorial, we will import hello API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="c1d8b-159">Zie voor instructies over het maken van een API en handmatig toevoegen van bewerkingen [hoe toocreate API's](api-management-howto-create-apis.md) en [hoe tooadd operations tooan API](api-management-howto-add-operations.md).</span><span class="sxs-lookup"><span data-stu-id="c1d8b-159">For guidance on creating an API and manually adding operations, see [How toocreate APIs](api-management-howto-create-apis.md) and [How tooadd operations tooan API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="c1d8b-160">API's worden geconfigureerd in de publicatieportal Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-160">APIs are configured from hello publisher portal.</span></span> <span data-ttu-id="c1d8b-161">tooreach, klikt u op **publicatieportal** Hallo service werkbalk van.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-161">tooreach it, click **Publisher portal** from hello service toolbar.</span></span>

![Publicatieportal][api-management-management-console]

<span data-ttu-id="c1d8b-163">tooimport hello Rekenmachine-API, klikt u op **API's** van Hallo **API Management** menu op Hallo links en klik vervolgens op **Import API**.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-163">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![Knop API importeren][api-management-import-api]

<span data-ttu-id="c1d8b-165">Voer Hallo tooconfigure hello basisrekenmachine-API stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c1d8b-165">Perform hello following steps tooconfigure hello calculator API:</span></span>

1. <span data-ttu-id="c1d8b-166">Klik op **van URL**, voer **http://calcapi.cloudapp.net/calcapi.json** in Hallo **URL specificatiedocument** tekst vak en klikt u op Hallo **Swagger**  keuzerondje.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-166">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into hello **Specification document URL** text box, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="c1d8b-167">Type **calc** in Hallo **achtervoegsel URL Web-API** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-167">Type **calc** into hello **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="c1d8b-168">Klik in het Hallo **producten (optioneel)** vak en kies **Starter**.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-168">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="c1d8b-169">Klik op **opslaan** tooimport Hallo API.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-169">Click **Save** tooimport hello API.</span></span>

![Nieuwe API toevoegen][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="c1d8b-171">In **API Management** wordt momenteel zowel versie 1.2 als versie 2.0 van het Swagger-document voor import ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-171">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="c1d8b-172">Hoewel in de [Swagger 2.0-specificatie](http://swagger.io/specification) wordt aangegeven dat eigenschappen `host`, `basePath` en `schemes` optioneel zijn, **MOET** uw Swagger 2.0-document deze eigenschappen bevatten, anders wordt het niet geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-172">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="c1d8b-173">Zodra het Hallo-API is geïmporteerd, wordt hello overzichtspagina voor Hallo API weergegeven in de publicatieportal Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-173">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![API-overzicht][api-management-imported-api-summary]

<span data-ttu-id="c1d8b-175">Hallo API-sectie bevat meerdere tabbladen.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-175">hello API section has several tabs.</span></span> <span data-ttu-id="c1d8b-176">Hallo **samenvatting** tabblad worden basismetrieken en informatie over Hallo API.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-176">hello **Summary** tab displays basic metrics and information about hello API.</span></span> <span data-ttu-id="c1d8b-177">Hallo [instellingen](api-management-howto-create-apis.md#configure-api-settings) tabblad gebruikte tooview en bewerk Hallo configuratie voor een API is.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-177">hello [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used tooview and edit hello configuration for an API.</span></span> <span data-ttu-id="c1d8b-178">Hallo [Operations](api-management-howto-add-operations.md) tabblad is gebruikte toomanage Hallo van API-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-178">hello [Operations](api-management-howto-add-operations.md) tab is used toomanage hello API's operations.</span></span> <span data-ttu-id="c1d8b-179">Hallo **beveiliging** tabblad gebruikte tooconfigure gatewayverificatie voor de back-endserver Hallo kan worden met behulp van basisverificatie of [wederzijdse certificaatverificatie](api-management-howto-mutual-certificates.md), en tooconfigure [ gebruikersautorisatie met behulp van OAuth 2.0](api-management-howto-oauth2.md).</span><span class="sxs-lookup"><span data-stu-id="c1d8b-179">hello **Security** tab can be used tooconfigure gateway authentication for hello backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and tooconfigure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="c1d8b-180">Hallo **problemen** tabblad is gebruikte tooview problemen die worden gerapporteerd door Hallo-ontwikkelaars die uw API's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-180">hello **Issues** tab is used tooview issues reported by hello developers who are using your APIs.</span></span> <span data-ttu-id="c1d8b-181">Hallo **producten** tabblad is gebruikte tooconfigure Hallo producten die deze API bevatten.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-181">hello **Products** tab is used tooconfigure hello products that contain this API.</span></span>

<span data-ttu-id="c1d8b-182">Standaard wordt elk API Management-exemplaar geleverd met twee voorbeeldproducten:</span><span class="sxs-lookup"><span data-stu-id="c1d8b-182">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="c1d8b-183">**Starter**</span><span class="sxs-lookup"><span data-stu-id="c1d8b-183">**Starter**</span></span>
* <span data-ttu-id="c1d8b-184">**Onbeperkt**</span><span class="sxs-lookup"><span data-stu-id="c1d8b-184">**Unlimited**</span></span>

<span data-ttu-id="c1d8b-185">In deze zelfstudie is Hallo basisrekenmachine-API toohello Starter-product toegevoegd wanneer Hallo API is geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-185">In this tutorial, hello Basic Calculator API was added toohello Starter product when hello API was imported.</span></span>

<span data-ttu-id="c1d8b-186">In de volgorde toomake aanroepen tooan API ontwikkelaars moeten zich eerst abonneren tooa product waarmee ze toegang tooit.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-186">In order toomake calls tooan API, developers must first subscribe tooa product that gives them access tooit.</span></span> <span data-ttu-id="c1d8b-187">Ontwikkelaars kunnen zich abonneren tooproducts in Hallo developer-portal of beheerders kunnen ontwikkelaars tooproducts in de publicatieportal Hallo abonneren.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-187">Developers can subscribe tooproducts in hello developer portal, or administrators can subscribe developers tooproducts in hello publisher portal.</span></span> <span data-ttu-id="c1d8b-188">U bent een beheerder omdat u Hallo API Management-exemplaar in Hallo vorige stappen in de zelfstudie hello, gemaakt zodat u al geabonneerd tooevery product standaard bent.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-188">You are an administrator since you created hello API Management instance in hello previous steps in hello tutorial, so you are already subscribed tooevery product by default.</span></span>

## <span data-ttu-id="c1d8b-189"><a name="call-operation"></a>Een bewerking aanroepen vanuit de ontwikkelaarsportal Hallo</span><span class="sxs-lookup"><span data-stu-id="c1d8b-189"><a name="call-operation"> </a>Call an operation from hello developer portal</span></span>
<span data-ttu-id="c1d8b-190">Bewerkingen rechtstreeks vanuit de ontwikkelaarsportal hello, waardoor een handige manier tooview kunnen worden aangeroepen en Hallo bewerkingen van een API testen.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-190">Operations can be called directly from hello developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="c1d8b-191">In deze zelfstudiestap roept u Hallo basisrekenmachine-API van **twee gehele getallen toevoegen** bewerking.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-191">In this tutorial step, you will call hello Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="c1d8b-192">Klik op **-portal voor ontwikkelaars** in Hallo Hallo menu rechts van de publicatieportal Hallo top.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-192">Click **Developer portal** from hello menu at hello top right of hello publisher portal.</span></span>

![ontwikkelaarsportal][api-management-developer-portal-menu]

<span data-ttu-id="c1d8b-194">Klik op **API's** van Hallo bovenste menu en klik vervolgens op **basisrekenmachine** toosee Hallo beschikbare bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-194">Click **APIs** from hello top menu, and then click **Basic Calculator** toosee hello available operations.</span></span>

![ontwikkelaarsportal][api-management-developer-portal-calc-api]

<span data-ttu-id="c1d8b-196">Houd er rekening mee Hallo voorbeeldbeschrijvingen en parameters die zijn geïmporteerd samen met de Hallo API en bewerkingen, om documentatie voor ontwikkelaars Hallo die wordt gebruikt voor deze bewerking te bieden.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-196">Note hello sample descriptions and parameters that were imported along with hello API and operations, providing documentation for hello developers that will use this operation.</span></span> <span data-ttu-id="c1d8b-197">Deze beschrijvingen kunnen ook worden toegevoegd wanneer bewerkingen handmatig worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-197">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="c1d8b-198">Hallo toocall **twee gehele getallen toevoegen** bewerking, klikt u op **Try it**.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-198">toocall hello **Add two integers** operation, click **Try it**.</span></span>

![Probeer het nu][api-management-developer-portal-calc-api-console]

<span data-ttu-id="c1d8b-200">Sommige waarden opgeven voor Hallo parameters of houden Hallo standaardwaarden en klik op **verzenden**.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-200">You can enter some values for hello parameters or keep hello defaults, and then click **Send**.</span></span>

![HTTP Get][api-management-invoke-get]

<span data-ttu-id="c1d8b-202">Nadat een bewerking is aangeroepen, Hallo ontwikkelaarsportal hello **antwoordstatus**, Hallo **antwoordheaders**, en er is een **antwoordinhoud**.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-202">After an operation is invoked, hello developer portal displays hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![Antwoord][api-management-invoke-get-response]

## <span data-ttu-id="c1d8b-204"><a name="view-analytics"> </a>Analytische gegevens bekijken</span><span class="sxs-lookup"><span data-stu-id="c1d8b-204"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="c1d8b-205">tooview analytics voor de basisrekenmachine switch back toohello publicatieportal door te selecteren **beheren** in Hallo Hallo menu rechts van de ontwikkelaarsportal Hallo top.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-205">tooview analytics for Basic Calculator, switch back toohello publisher portal by selecting **Manage** from hello menu at hello top right of hello developer portal.</span></span>

![Beheren][api-management-manage-menu]

<span data-ttu-id="c1d8b-207">Hallo standaardweergave voor de publicatieportal Hallo is Hallo **Dashboard**, waarmee u een overzicht van uw exemplaar van API Management.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-207">hello default view for hello publisher portal is hello **Dashboard**, which provides an overview of your API Management instance.</span></span>

![Dashboard][api-management-dashboard]

<span data-ttu-id="c1d8b-209">Aanwijzen Hallo muis over Hallo-grafiek voor **basisrekenmachine** toosee Hallo specifieke metrische gegevens voor het gebruik van Hallo Hallo API voor een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-209">Hover hello mouse over hello chart for **Basic Calculator** toosee hello specific metrics for hello usage of hello API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="c1d8b-210">Als u niet alle regels in uw grafiek ziet, switch back toohello developer-portal en voert u enkele aanroepen in Hallo API, wacht even en vervolgens terugkeren toohello dashboard.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-210">If you don't see any lines on your chart, switch back toohello developer portal and make some calls into hello API, wait a few moments, and then come back toohello dashboard.</span></span>
> 
> 

<span data-ttu-id="c1d8b-211">Klik op **Details weergeven** tooview Hallo overzichtspagina voor Hallo API, met inbegrip van een grotere versie van Hallo weergegeven metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-211">Click **View Details** tooview hello summary page for hello API, including a larger version of hello displayed metrics.</span></span>

![Analytische gegevens][api-management-mouse-over]

![Samenvatting][api-management-api-summary-metrics]

<span data-ttu-id="c1d8b-214">Klik voor gedetailleerde metrische gegevens en rapporten **Analytics** van Hallo **API Management** menu aan de linkerkant Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-214">For detailed metrics and reports, click **Analytics** from hello **API Management** menu on hello left.</span></span>

![Overzicht][api-management-analytics-overview]

<span data-ttu-id="c1d8b-216">Hallo **Analytics** sectie heeft Hallo volgende vier tabbladen:</span><span class="sxs-lookup"><span data-stu-id="c1d8b-216">hello **Analytics** section has hello following four tabs:</span></span>

* <span data-ttu-id="c1d8b-217">**In een oogopslag** bevat algemene informatie over het gebruik en status metrische gegevens, evenals Hallo belangrijkste ontwikkelaars, producten, API's en bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-217">**At a glance** provides overall usage and health metrics, as well as hello top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="c1d8b-218">**Gebruik** biedt een diepgaande blik op API-aanroepen en bandbreedte, met inbegrip van een geografische weergave.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-218">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="c1d8b-219">**Status** richt zich op statuscodes, succespercentages van de cache, reactietijden, en reactietijden van de API en de service.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-219">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="c1d8b-220">**Activiteit** biedt rapporten die Inzoomen op Hallo specifieke activiteit per ontwikkelaar, product, API en bewerking.</span><span class="sxs-lookup"><span data-stu-id="c1d8b-220">**Activity** provides reports that drill down on hello specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="c1d8b-221"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c1d8b-221"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="c1d8b-222">Meer informatie over hoe te[uw API beveiligen met frequentielimieten](api-management-howto-product-with-rules.md).</span><span class="sxs-lookup"><span data-stu-id="c1d8b-222">Learn how too[Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
