---
title: aaaWork met proxy's in Azure Functions | Microsoft Docs
description: Overzicht van hoe toouse Azure Functions-proxy's
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="62c5b-103">Werken met Azure Functions-proxy's (preview)</span><span class="sxs-lookup"><span data-stu-id="62c5b-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="62c5b-104">Azure Functions-proxy's is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="62c5b-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="62c5b-105">Het is gratis terwijl in preview, maar standaardfuncties facturering tooproxy uitvoeringen toegepast.</span><span class="sxs-lookup"><span data-stu-id="62c5b-105">It is free while in preview, but standard Functions billing applies tooproxy executions.</span></span> <span data-ttu-id="62c5b-106">Zie voor meer informatie [prijzen van Azure Functions](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="62c5b-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="62c5b-107">Dit artikel wordt uitgelegd hoe tooconfigure en werken met Azure Functions-proxy's.</span><span class="sxs-lookup"><span data-stu-id="62c5b-107">This article explains how tooconfigure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="62c5b-108">Met deze functie kunt u eindpunten op de functie-app die zijn geïmplementeerd door een andere resource.</span><span class="sxs-lookup"><span data-stu-id="62c5b-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="62c5b-109">Terwijl u nog steeds één API-gebied voor clients kunt u deze toobreak proxy's een grote API in meerdere functie-apps (zoals in een microservice-architectuur).</span><span class="sxs-lookup"><span data-stu-id="62c5b-109">You can use these proxies toobreak a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="62c5b-110"><a name="enable"></a>Azure Functions-proxy's inschakelen</span><span class="sxs-lookup"><span data-stu-id="62c5b-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="62c5b-111">Proxy's worden niet standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="62c5b-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="62c5b-112">U kunt de proxy's maken bij het Hallo-functie is uitgeschakeld, maar ze niet kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="62c5b-112">You can create proxies while hello feature is disabled, but they will not execute.</span></span> <span data-ttu-id="62c5b-113">tooenable proxy's, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="62c5b-113">tooenable proxies, do hello following:</span></span>

1. <span data-ttu-id="62c5b-114">Open Hallo [Azure-portal], en ga tooyour functie-app.</span><span class="sxs-lookup"><span data-stu-id="62c5b-114">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="62c5b-115">Selecteer **werken app-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="62c5b-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="62c5b-116">Switch **inschakelen Azure Functions-proxy's (preview)** te**op**.</span><span class="sxs-lookup"><span data-stu-id="62c5b-116">Switch **Enable Azure Functions Proxies (preview)** too**On**.</span></span>

<span data-ttu-id="62c5b-117">U kunt ook teruggaan hier tooupdate Hallo proxy runtime nieuwe functies beschikbaar komen.</span><span class="sxs-lookup"><span data-stu-id="62c5b-117">You can also return here tooupdate hello proxy runtime as new features become available.</span></span>


## <span data-ttu-id="62c5b-118"><a name="create"></a>Maken van een proxy</span><span class="sxs-lookup"><span data-stu-id="62c5b-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="62c5b-119">Deze sectie leest u hoe toocreate een proxy in Hallo Functions-portal.</span><span class="sxs-lookup"><span data-stu-id="62c5b-119">This section shows you how toocreate a proxy in hello Functions portal.</span></span>

1. <span data-ttu-id="62c5b-120">Open Hallo [Azure-portal], en ga tooyour functie-app.</span><span class="sxs-lookup"><span data-stu-id="62c5b-120">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="62c5b-121">Selecteer in het linkerdeelvenster Hallo **nieuwe proxy**.</span><span class="sxs-lookup"><span data-stu-id="62c5b-121">In hello left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="62c5b-122">Geef een naam voor de proxy.</span><span class="sxs-lookup"><span data-stu-id="62c5b-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="62c5b-123">Hallo-eindpunt dat wordt weergegeven op deze functie-app configureren door te geven van Hallo **Routesjabloon** en **HTTP-methoden**.</span><span class="sxs-lookup"><span data-stu-id="62c5b-123">Configure hello endpoint that's exposed on this function app by specifying hello **route template** and **HTTP methods**.</span></span> <span data-ttu-id="62c5b-124">Deze parameters zich gedragen volgens toohello regels voor [HTTP-triggers].</span><span class="sxs-lookup"><span data-stu-id="62c5b-124">These parameters behave according toohello rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="62c5b-125">Set Hallo **back-end-URL** tooanother eindpunt.</span><span class="sxs-lookup"><span data-stu-id="62c5b-125">Set hello **backend URL** tooanother endpoint.</span></span> <span data-ttu-id="62c5b-126">Dit eindpunt kan een functie in een andere functie-app, of andere API kan zijn.</span><span class="sxs-lookup"><span data-stu-id="62c5b-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="62c5b-127">Hallo waarde hoeft niet toobe statisch en deze kan verwijzen naar [toepassingsinstellingen] en [parameters uit de oorspronkelijke clientaanvraag Hallo].</span><span class="sxs-lookup"><span data-stu-id="62c5b-127">hello value does not need toobe static, and it can reference [application settings] and [parameters from hello original client request].</span></span>
6. <span data-ttu-id="62c5b-128">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="62c5b-128">Click **Create**.</span></span>

<span data-ttu-id="62c5b-129">De proxy bestaat nu als een nieuw eindpunt op functie-app.</span><span class="sxs-lookup"><span data-stu-id="62c5b-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="62c5b-130">Vanuit het clientperspectief van een is het equivalent tooan HttpTrigger in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="62c5b-130">From a client perspective, it is equivalent tooan HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="62c5b-131">U kunt uw nieuwe proxy uitproberen door Hallo Proxy URL kopiëren en testen van het met uw favoriete HTTP-client.</span><span class="sxs-lookup"><span data-stu-id="62c5b-131">You can try out your new proxy by copying hello Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="62c5b-132"><a name="modify-requests-responses"></a>Aanvragen en antwoorden wijzigen</span><span class="sxs-lookup"><span data-stu-id="62c5b-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="62c5b-133">U kunt aanvragen tooand reacties van de back-end Hallo wijzigen met Azure Functions-proxy's.</span><span class="sxs-lookup"><span data-stu-id="62c5b-133">With Azure Functions Proxies, you can modify requests tooand responses from hello back end.</span></span> <span data-ttu-id="62c5b-134">Deze transformaties kunnen variabelen gebruiken zoals gedefinieerd in [variabelen gebruiken].</span><span class="sxs-lookup"><span data-stu-id="62c5b-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="62c5b-135"><a name="modify-backend-request"></a>Hallo back-end aanvraag wijzigen</span><span class="sxs-lookup"><span data-stu-id="62c5b-135"><a name="modify-backend-request"></a>Modify hello back-end request</span></span>

<span data-ttu-id="62c5b-136">Hallo back-end-aanvraag is standaard geïnitialiseerd als een kopie van de oorspronkelijke aanvraag Hallo.</span><span class="sxs-lookup"><span data-stu-id="62c5b-136">By default, hello back-end request is initialized as a copy of hello original request.</span></span> <span data-ttu-id="62c5b-137">Bovendien toosetting Hallo back-end-URL, kunt u wijzigingen toohello HTTP-methode, headers en querytekenreeksparameters.</span><span class="sxs-lookup"><span data-stu-id="62c5b-137">In addition toosetting hello back-end URL, you can make changes toohello HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="62c5b-138">Hallo gewijzigde waarden kunnen verwijzen naar [toepassingsinstellingen] en [parameters uit de oorspronkelijke clientaanvraag Hallo].</span><span class="sxs-lookup"><span data-stu-id="62c5b-138">hello modified values can reference [application settings] and [parameters from hello original client request].</span></span>

<span data-ttu-id="62c5b-139">Er is momenteel geen portal ervaring voor het wijzigen van de back-end-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="62c5b-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="62c5b-140">toolearn hoe tooapply deze mogelijkheid van proxies.json, Zie [definiëren van een object requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="62c5b-140">toolearn how tooapply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="62c5b-141"><a name="modify-response"></a>Hallo-antwoord worden gewijzigd</span><span class="sxs-lookup"><span data-stu-id="62c5b-141"><a name="modify-response"></a>Modify hello response</span></span>

<span data-ttu-id="62c5b-142">Standaard is antwoord Hallo-client als een kopie van het antwoord van de back-end Hallo geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="62c5b-142">By default, hello client response is initialized as a copy of hello back-end response.</span></span> <span data-ttu-id="62c5b-143">U kunt wijzigingen toohello van code voor antwoordstatus, reden, kopteksten en hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="62c5b-143">You can make changes toohello response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="62c5b-144">Hallo gewijzigde waarden kunnen verwijzen naar [toepassingsinstellingen], [parameters uit de oorspronkelijke clientaanvraag Hallo], en [parameters uit het antwoord van de back-end Hallo].</span><span class="sxs-lookup"><span data-stu-id="62c5b-144">hello modified values can reference [application settings], [parameters from hello original client request], and [parameters from hello back-end response].</span></span>

<span data-ttu-id="62c5b-145">Er is momenteel geen portal ervaring voor het wijzigen van antwoorden.</span><span class="sxs-lookup"><span data-stu-id="62c5b-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="62c5b-146">toolearn hoe tooapply deze mogelijkheid van proxies.json, Zie [definiëren van een object responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="62c5b-146">toolearn how tooapply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="62c5b-147"><a name="using-variables"></a>Variabelen gebruiken</span><span class="sxs-lookup"><span data-stu-id="62c5b-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="62c5b-148">Hallo-configuratie voor een proxy hoeft niet toobe statisch.</span><span class="sxs-lookup"><span data-stu-id="62c5b-148">hello configuration for a proxy does not need toobe static.</span></span> <span data-ttu-id="62c5b-149">U kunt deze voorwaarde toouse variabelen van de oorspronkelijke aanvraag hello, back-end-antwoord Hallo of toepassingsinstellingen.</span><span class="sxs-lookup"><span data-stu-id="62c5b-149">You can condition it toouse variables from hello original request, hello back-end response, or application settings.</span></span>

### <span data-ttu-id="62c5b-150"><a name="request-parameters"></a>Aanvraagparameters verwijzing</span><span class="sxs-lookup"><span data-stu-id="62c5b-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="62c5b-151">U kunt parameters van de aanvraag als eigenschap toohello back-end-URL-ingangen of als onderdeel van het wijzigen van aanvragen en antwoorden.</span><span class="sxs-lookup"><span data-stu-id="62c5b-151">You can use request parameters as inputs toohello back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="62c5b-152">Sommige parameters kunnen afhankelijk zijn van Hallo Routesjabloon die opgegeven in de base proxyconfiguratie Hallo en anderen kunnen afkomstig zijn uit de eigenschappen voor inkomende hello-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="62c5b-152">Some parameters can be bound from hello route template that's specified in hello base proxy configuration, and others can come from properties of hello incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="62c5b-153">Route-Sjabloonparameters</span><span class="sxs-lookup"><span data-stu-id="62c5b-153">Route template parameters</span></span>
<span data-ttu-id="62c5b-154">Parameters die worden gebruikt in de Routesjabloon Hallo zijn beschikbaar toobe waarnaar wordt verwezen door de naam.</span><span class="sxs-lookup"><span data-stu-id="62c5b-154">Parameters that are used in hello route template are available toobe referenced by name.</span></span> <span data-ttu-id="62c5b-155">Hallo parameternamen zijn tussen accolades ({}).</span><span class="sxs-lookup"><span data-stu-id="62c5b-155">hello parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="62c5b-156">Bijvoorbeeld, als een proxy heeft een Routesjabloon zoals `/pets/{petId}`, Hallo back-end-URL kan bevatten Hallo-waarde van `{petId}`als in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="62c5b-156">For example, if a proxy has a route template, such as `/pets/{petId}`, hello back-end URL can include hello value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="62c5b-157">Als Routesjabloon hello wordt beëindigd in een jokerteken, zoals `/api/{*restOfPath}`, Hallo waarde `{restOfPath}` is een tekenreeksrepresentatie van Hallo resterende padsegmenten van inkomende hello-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="62c5b-157">If hello route template terminates in a wildcard, such as `/api/{*restOfPath}`, hello value `{restOfPath}` is a string representation of hello remaining path segments from hello incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="62c5b-158">Aanvullende aanvraagparameters</span><span class="sxs-lookup"><span data-stu-id="62c5b-158">Additional request parameters</span></span>
<span data-ttu-id="62c5b-159">Bovendien toohello Sjabloonparameters routeren, Hallo volgende waarden kan worden gebruikt in configuratiewaarden:</span><span class="sxs-lookup"><span data-stu-id="62c5b-159">In addition toohello route template parameters, hello following values can be used in config values:</span></span>

* <span data-ttu-id="62c5b-160">**{request.method}** : HTTP-methode die wordt gebruikt op de oorspronkelijke aanvraag Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="62c5b-160">**{request.method}**: hello HTTP method that's used on hello original request.</span></span>
* <span data-ttu-id="62c5b-161">**{request.headers. \<HeaderName is opgeslagen\>}**: een header die kan worden gelezen vanaf de oorspronkelijke aanvraag Hallo.</span><span class="sxs-lookup"><span data-stu-id="62c5b-161">**{request.headers.\<HeaderName\>}**: A header that can be read from hello original request.</span></span> <span data-ttu-id="62c5b-162">Vervang  *\<HeaderName is opgeslagen\>*  met Hallo-naam van dat u wilt dat tooread Hallo-header.</span><span class="sxs-lookup"><span data-stu-id="62c5b-162">Replace *\<HeaderName\>* with hello name of hello header that you want tooread.</span></span> <span data-ttu-id="62c5b-163">Als het Hallo-header wordt niet geleverd op Hallo aanvraag, worden Hallo waarde Hallo lege tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="62c5b-163">If hello header is not included on hello request, hello value will be hello empty string.</span></span>
* <span data-ttu-id="62c5b-164">**{request.querystring. \<ParameterName\>}**: een queryreeksparameter opgeven die kan worden gelezen vanaf de oorspronkelijke aanvraag Hallo.</span><span class="sxs-lookup"><span data-stu-id="62c5b-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from hello original request.</span></span> <span data-ttu-id="62c5b-165">Vervang  *\<ParameterName\>*  met Hallo naam van de gewenste tooread Hallo-parameter.</span><span class="sxs-lookup"><span data-stu-id="62c5b-165">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooread.</span></span> <span data-ttu-id="62c5b-166">Als het Hallo-parameter niet is opgenomen op Hallo aanvraag, worden Hallo waarde Hallo lege tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="62c5b-166">If hello parameter is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="62c5b-167"><a name="response-parameters"></a>Verwijzing naar back-end antwoord parameters</span><span class="sxs-lookup"><span data-stu-id="62c5b-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="62c5b-168">Antwoord parameters kunnen worden gebruikt als onderdeel van het Hallo-antwoord toohello client wijzigen.</span><span class="sxs-lookup"><span data-stu-id="62c5b-168">Response parameters can be used as part of modifying hello response toohello client.</span></span> <span data-ttu-id="62c5b-169">Hallo volgende waarden kan worden gebruikt in configuratiewaarden:</span><span class="sxs-lookup"><span data-stu-id="62c5b-169">hello following values can be used in config values:</span></span>

* <span data-ttu-id="62c5b-170">**{backend.response.statusCode}** : HTTP-statuscode geretourneerd op antwoord van de back-end Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="62c5b-170">**{backend.response.statusCode}**: hello HTTP status code that's returned on hello back-end response.</span></span>
* <span data-ttu-id="62c5b-171">**{backend.response.statusReason}** : Hallo HTTP reden dat op antwoord van de back-end Hallo wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="62c5b-171">**{backend.response.statusReason}**: hello HTTP reason phrase that's returned on hello back-end response.</span></span>
* <span data-ttu-id="62c5b-172">**{backend.response.headers. \<HeaderName is opgeslagen\>}**: een header die kan worden gelezen vanaf de back-end-antwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="62c5b-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from hello back-end response.</span></span> <span data-ttu-id="62c5b-173">Vervang  *\<HeaderName is opgeslagen\>*  met de naam van Hallo header Hallo gewenste tooread.</span><span class="sxs-lookup"><span data-stu-id="62c5b-173">Replace *\<HeaderName\>* with hello name of hello header you want tooread.</span></span> <span data-ttu-id="62c5b-174">Als het Hallo-header wordt niet geleverd op Hallo aanvraag, worden Hallo waarde Hallo lege tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="62c5b-174">If hello header is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="62c5b-175"><a name="use-appsettings"></a>Toepassingsinstellingen-verwijzing</span><span class="sxs-lookup"><span data-stu-id="62c5b-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="62c5b-176">U kunt ook verwijzen naar [toepassingsinstellingen gedefinieerd voor de functie-app Hallo](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) door Hallo Instellingsnaam tussen procenttekens (%).</span><span class="sxs-lookup"><span data-stu-id="62c5b-176">You can also reference [application settings defined for hello function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding hello setting name with percent signs (%).</span></span>

<span data-ttu-id="62c5b-177">Bijvoorbeeld, een back-end-URL van *https://%ORDER_PROCESSING_HOST%/api/orders* "% ORDER_PROCESSING_HOST %" vervangen door de waarde Hallo van Hallo ORDER_PROCESSING_HOST instelling zou hebben.</span><span class="sxs-lookup"><span data-stu-id="62c5b-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with hello value of hello ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="62c5b-178">Toepassingsinstellingen voor back-end-hosts gebruiken wanneer u meerdere implementaties of testomgeving.</span><span class="sxs-lookup"><span data-stu-id="62c5b-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="62c5b-179">Op die manier kunt u ervoor zorgen dat u altijd praten toohello terugkeren beëindigen voor die omgeving.</span><span class="sxs-lookup"><span data-stu-id="62c5b-179">That way, you can make sure that you are always talking toohello right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="62c5b-180">Geavanceerde configuratie</span><span class="sxs-lookup"><span data-stu-id="62c5b-180">Advanced configuration</span></span>

<span data-ttu-id="62c5b-181">Hallo-proxy's die u configureert, worden opgeslagen in een proxies.json-bestand bevindt zich in de hoofdmap Hallo van een functie app-map.</span><span class="sxs-lookup"><span data-stu-id="62c5b-181">hello proxies that you configure are stored in a proxies.json file, which is located in hello root of a function app directory.</span></span> <span data-ttu-id="62c5b-182">U handmatig dit bestand bewerken en implementeren als onderdeel van uw app als u een Hallo [implementatiemethoden](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) die functies worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="62c5b-182">You can manually edit this file and deploy it as part of your app when you use any of hello [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="62c5b-183">Hallo-functie moet [ingeschakeld](#enable) voor Hallo bestand toobe verwerkt.</span><span class="sxs-lookup"><span data-stu-id="62c5b-183">hello feature must be [enabled](#enable) for hello file toobe processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="62c5b-184">Als u hebt niet een van de methoden voor het implementeren van hello, kunt u ook werken met Hallo proxies.json bestand in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="62c5b-184">If you have not set up one of hello deployment methods, you can also work with hello proxies.json file in hello portal.</span></span> <span data-ttu-id="62c5b-185">Ga tooyour functie-app, selecteer **platformfuncties**, en selecteer vervolgens **App Service-Editor**.</span><span class="sxs-lookup"><span data-stu-id="62c5b-185">Go tooyour function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="62c5b-186">U kunt op deze manier Hallo hele bestandsstructuur van uw app functie bekijken en brengt wijzigingen aan.</span><span class="sxs-lookup"><span data-stu-id="62c5b-186">By doing so, you can view hello entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="62c5b-187">Proxies.JSON wordt gedefinieerd door een object proxy's, die bestaan uit benoemde proxy's en de bijbehorende definities.</span><span class="sxs-lookup"><span data-stu-id="62c5b-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="62c5b-188">Eventueel, als uw editor ondersteunt, kunt u verwijzen naar een [JSON-schema](http://json.schemastore.org/proxies) voor de codevoltooiing.</span><span class="sxs-lookup"><span data-stu-id="62c5b-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="62c5b-189">Een voorbeeld van een bestand lijkt Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="62c5b-189">An example file might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

<span data-ttu-id="62c5b-190">Elke proxy heeft een beschrijvende naam, zoals *proxy1* in het voorgaande voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="62c5b-190">Each proxy has a friendly name, such as *proxy1* in hello preceding example.</span></span> <span data-ttu-id="62c5b-191">Hallo bijbehorende proxy definitie van object wordt gedefinieerd door Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="62c5b-191">hello corresponding proxy definition object is defined by hello following properties:</span></span>

* <span data-ttu-id="62c5b-192">**matchCondition**: vereist--een object definiëren Hallo-aanvragen die Hallo uitvoering van deze proxy activeren.</span><span class="sxs-lookup"><span data-stu-id="62c5b-192">**matchCondition**: Required--an object defining hello requests that trigger hello execution of this proxy.</span></span> <span data-ttu-id="62c5b-193">Deze twee eigenschappen die worden gedeeld met bevat [HTTP-triggers]:</span><span class="sxs-lookup"><span data-stu-id="62c5b-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="62c5b-194">_methoden_: een matrix van Hallo HTTP-methoden die Hallo proxy reageert op.</span><span class="sxs-lookup"><span data-stu-id="62c5b-194">_methods_: An array of hello HTTP methods that hello proxy responds to.</span></span> <span data-ttu-id="62c5b-195">Als deze niet is opgegeven, reageert Hallo proxy tooall HTTP-methoden op Hallo route.</span><span class="sxs-lookup"><span data-stu-id="62c5b-195">If it is not specified, hello proxy responds tooall HTTP methods on hello route.</span></span>
    * <span data-ttu-id="62c5b-196">_route_: vereist--definieert Hallo-Routesjabloon beheren die aanvragen URL's van uw proxy reageert op.</span><span class="sxs-lookup"><span data-stu-id="62c5b-196">_route_: Required--defines hello route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="62c5b-197">In tegenstelling tot in de HTTP-triggers is er geen standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="62c5b-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="62c5b-198">**backendUri**: Hallo-URL van Hallo back-end-resource toowhich Hallo aanvraag moet via proxy.</span><span class="sxs-lookup"><span data-stu-id="62c5b-198">**backendUri**: hello URL of hello back-end resource toowhich hello request should be proxied.</span></span> <span data-ttu-id="62c5b-199">Deze waarde kan verwijzen naar toepassingsinstellingen en parameters van de oorspronkelijke clientaanvraag Hallo.</span><span class="sxs-lookup"><span data-stu-id="62c5b-199">This value can reference application settings and parameters from hello original client request.</span></span> <span data-ttu-id="62c5b-200">Als deze eigenschap niet opgenomen is, wordt Azure Functions reageert met een HTTP 200 OK.</span><span class="sxs-lookup"><span data-stu-id="62c5b-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="62c5b-201">**requestOverrides**: een object dat transformaties toohello back-end-aanvraag bepaalt.</span><span class="sxs-lookup"><span data-stu-id="62c5b-201">**requestOverrides**: An object that defines transformations toohello back-end request.</span></span> <span data-ttu-id="62c5b-202">Zie [definiëren van een object requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="62c5b-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="62c5b-203">**responseOverrides**: een object dat transformaties toohello client antwoord bepaalt.</span><span class="sxs-lookup"><span data-stu-id="62c5b-203">**responseOverrides**: An object that defines transformations toohello client response.</span></span> <span data-ttu-id="62c5b-204">Zie [definiëren van een object responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="62c5b-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="62c5b-205">Hallo route eigenschap Azure Functions-proxy's worden niet door Hallo routePrefix eigenschap van hostconfiguratie Hallo-functies.</span><span class="sxs-lookup"><span data-stu-id="62c5b-205">hello route property Azure Functions Proxies does not honor hello routePrefix property of hello Functions host configuration.</span></span> <span data-ttu-id="62c5b-206">Als u een voorvoegsel zoals /api tooinclude wilt, moet worden opgenomen in Hallo route-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="62c5b-206">If you want tooinclude a prefix such as /api, it must be included in hello route property.</span></span>

### <span data-ttu-id="62c5b-207"><a name="requestOverrides"></a>Een object requestOverrides definiëren</span><span class="sxs-lookup"><span data-stu-id="62c5b-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="62c5b-208">Hallo requestOverrides object definieert toohello aanvraag voor wijzigingen als Hallo back-end bron wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="62c5b-208">hello requestOverrides object defines changes made toohello request when hello back-end resource is called.</span></span> <span data-ttu-id="62c5b-209">Hallo-object wordt gedefinieerd door Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="62c5b-209">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="62c5b-210">**backend.Request.Method**: Hallo HTTP-methode die is gebruikt toocall Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="62c5b-210">**backend.request.method**: hello HTTP method that's used toocall hello back end.</span></span>
* <span data-ttu-id="62c5b-211">**backend.Request.QueryString. \<ParameterName\>**: een queryreeksparameter opgeven die kan worden ingesteld voor Hallo toohello back-end-aanroep.</span><span class="sxs-lookup"><span data-stu-id="62c5b-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for hello call toohello back end.</span></span> <span data-ttu-id="62c5b-212">Vervang  *\<ParameterName\>*  met Hallo naam van de gewenste tooset Hallo-parameter.</span><span class="sxs-lookup"><span data-stu-id="62c5b-212">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooset.</span></span> <span data-ttu-id="62c5b-213">Als Hallo lege tekenreeks is opgegeven, wordt Hallo-parameter is niet opgenomen op Hallo back-end-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="62c5b-213">If hello empty string is provided, hello parameter is not included on hello back-end request.</span></span>
* <span data-ttu-id="62c5b-214">**backend.Request.headers. \<HeaderName is opgeslagen\>**: een header die kan worden ingesteld voor Hallo toohello back-end-aanroep.</span><span class="sxs-lookup"><span data-stu-id="62c5b-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for hello call toohello back end.</span></span> <span data-ttu-id="62c5b-215">Vervang  *\<HeaderName is opgeslagen\>*  met Hallo-naam van dat u wilt dat tooset Hallo-header.</span><span class="sxs-lookup"><span data-stu-id="62c5b-215">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="62c5b-216">Als u een lege tekenreeks Hallo opgeeft, wordt Hallo-header is niet opgenomen op Hallo back-end-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="62c5b-216">If you provide hello empty string, hello header is not included on hello back-end request.</span></span>

<span data-ttu-id="62c5b-217">Waarden kunnen verwijzen naar toepassingsinstellingen en parameters van de oorspronkelijke clientaanvraag Hallo.</span><span class="sxs-lookup"><span data-stu-id="62c5b-217">Values can reference application settings and parameters from hello original client request.</span></span>

<span data-ttu-id="62c5b-218">Een voorbeeldconfiguratie lijkt Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="62c5b-218">An example configuration might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <span data-ttu-id="62c5b-219"><a name="responseOverrides"></a>Een object responseOverrides definiëren</span><span class="sxs-lookup"><span data-stu-id="62c5b-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="62c5b-220">Hallo requestOverrides object definieert wijzigingen die zijn aangebracht toohello antwoord back toohello client is verstreken.</span><span class="sxs-lookup"><span data-stu-id="62c5b-220">hello requestOverrides object defines changes that are made toohello response that's passed back toohello client.</span></span> <span data-ttu-id="62c5b-221">Hallo-object wordt gedefinieerd door Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="62c5b-221">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="62c5b-222">**response.statusCode**: Hallo HTTP status code toobe toohello client geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="62c5b-222">**response.statusCode**: hello HTTP status code toobe returned toohello client.</span></span>
* <span data-ttu-id="62c5b-223">**response.statusReason**: Hallo HTTP reden woordgroep toobe toohello client geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="62c5b-223">**response.statusReason**: hello HTTP reason phrase toobe returned toohello client.</span></span>
* <span data-ttu-id="62c5b-224">**Response.BODY**: Hallo tekenreeksweergave van Hallo hoofdtekst toobe toohello client geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="62c5b-224">**response.body**: hello string representation of hello body toobe returned toohello client.</span></span>
* <span data-ttu-id="62c5b-225">**Response.headers. \<HeaderName is opgeslagen\>**: een koptekst voor Hallo antwoord toohello client kan worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="62c5b-225">**response.headers.\<HeaderName\>**: A header that can be set for hello response toohello client.</span></span> <span data-ttu-id="62c5b-226">Vervang  *\<HeaderName is opgeslagen\>*  met Hallo-naam van dat u wilt dat tooset Hallo-header.</span><span class="sxs-lookup"><span data-stu-id="62c5b-226">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="62c5b-227">Als u een lege tekenreeks Hallo opgeeft, is niet Hallo-header op antwoord Hallo opgenomen.</span><span class="sxs-lookup"><span data-stu-id="62c5b-227">If you provide hello empty string, hello header is not included on hello response.</span></span>

<span data-ttu-id="62c5b-228">Waarden kunnen verwijzen naar toepassingsinstellingen, parameters uit de oorspronkelijke clientaanvraag Hallo en parameters uit Hallo back-end-antwoord.</span><span class="sxs-lookup"><span data-stu-id="62c5b-228">Values can reference application settings, parameters from hello original client request, and parameters from hello back-end response.</span></span>

<span data-ttu-id="62c5b-229">Een voorbeeldconfiguratie lijkt Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="62c5b-229">An example configuration might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> <span data-ttu-id="62c5b-230">In dit voorbeeld Hallo-instantie wordt ingesteld rechtstreeks, dus er is geen `backendUri` eigenschap nodig is.</span><span class="sxs-lookup"><span data-stu-id="62c5b-230">In this example, hello body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="62c5b-231">Hallo-voorbeeld ziet u hoe u Azure Functions-proxy's kunt gebruiken voor mocking API's.</span><span class="sxs-lookup"><span data-stu-id="62c5b-231">hello example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

[Azure-portal]: https://portal.azure.com
[HTTP-triggers]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[definiëren van een object requestOverrides]: #requestOverrides
[definiëren van een object responseOverrides]: #responseOverrides
[toepassingsinstellingen]: #use-appsettings
[variabelen gebruiken]: #using-variables
[parameters uit de oorspronkelijke clientaanvraag Hallo]: #request-parameters
[parameters uit het antwoord van de back-end Hallo]: #response-parameters
